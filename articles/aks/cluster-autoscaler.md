---
title: Usar o dimensionador automático de cluster no AKS (Serviço de Kubernetes do Azure)
description: Saiba como usar o dimensionador automático de cluster para dimensionar automaticamente seu cluster e atender às demandas de aplicativo em um cluster do AKS (Serviço de Kubernetes do Azure).
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 01/29/2019
ms.author: iainfou
ms.openlocfilehash: 6b2302e69c9412170b55df4bfd8c1df5a9f75ef3
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55479093"
---
# <a name="automatically-scale-a-cluster-to-meet-application-demands-on-azure-kubernetes-service-aks"></a>Dimensionar automaticamente um cluster para atender às demandas de aplicativo no AKS (Serviço de Kubernetes do Azure)

Para se manter atualizado com as demandas de aplicativo no AKS (Serviço de Kubernetes do Azure), talvez você precise ajustar o número de nós que executam as cargas de trabalho. O componente de dimensionador automático de cluster pode inspecionar os pods no cluster que não podem ser agendados devido a restrições de recursos. Quando problemas são detectados, o número de nós é aumentado para atender à demanda de aplicativo. Os nós também são regularmente verificados quanto à falta de pods em execução, com o número de nós diminuído posteriormente conforme necessário. Essa capacidade de escalar ou reduzir verticalmente o número de nós no cluster do AKS permite a execução de um cluster eficiente e econômico.

Este artigo mostra como habilitar e gerenciar o dimensionador automático de cluster em um cluster do AKS.

> [!IMPORTANT]
> Esse recurso está atualmente na visualização. As versões prévias são disponibilizadas com a condição de que você concorde com os [termos de uso complementares][terms-of-use]. Alguns aspectos desse recurso podem alterar antes da GA (disponibilidade geral).

## <a name="before-you-begin"></a>Antes de começar

Este artigo exige a execução da CLI do Azure versão 2.0.55 ou posterior. Execute `az --version` para encontrar a versão. Se precisar instalar ou atualizar, consulte [Instalar a CLI do Azure][azure-cli-install].

Os clusters do AKS que dão suporte ao dimensionador automático de cluster precisam usar conjuntos de dimensionamento de máquinas virtuais e executar o Kubernetes versão *1.12.4* ou posterior. Esse suporte do conjunto de dimensionamento está em versão prévia. Para aceitar e criar clusters que usam conjuntos de dimensionamento, instale a extensão da CLI do Azure *aks-preview* usando o comando [az extension add][az-extension-add], conforme mostrado no seguinte exemplo:

```azurecli-interactive
az extension add --name aks-preview
```

> [!NOTE]
> Quando você instala a extensão *aks-preview*, cada cluster do AKS criado usa o modelo de implantação de versão prévia do conjunto de dimensionamento. Para recusar e criar clusters regulares com suporte total, remova a extensão usando `az extension remove --name aks-preview`.

## <a name="about-the-cluster-autoscaler"></a>Sobre o dimensionador automático de cluster

Para se ajustar às mudanças nas demandas de aplicativo, como entre a jornada de trabalho e a noite ou em um fim de semana, os clusters geralmente precisam de uma maneira de serem dimensionados automaticamente. Os clusters do AKS podem ser dimensionados de uma das duas maneiras:

* O **dimensionador automático de cluster** inspeciona os pods que não podem ser agendados em nós devido a restrições de recursos. Em seguida, o cluster aumenta automaticamente o número de nós.
* O **dimensionador automático de pod horizontal** usa o Servidor de Métricas em um cluster do Kubernetes para monitorar a demanda de recursos dos pods. Se um serviço precisa de mais recursos, o número de pods é automaticamente aumentado para atender à demanda.

![O dimensionador automático de cluster e o dimensionador automático de pod horizontal geralmente trabalham juntos para dar suporte às demandas necessárias de aplicativo](media/autoscaler/cluster-autoscaler.png)

O dimensionador automático de pod horizontal e o dimensionador automático de cluster também podem, em seguida, diminuir o número de pods e nós conforme necessário. O dimensionador automático de cluster diminui o número de nós quando a capacidade não é utilizada por um período. Os pods em um nó a serem removidos pelo dimensionador automático de cluster são agendados com segurança em outro lugar no cluster. O dimensionador automático de cluster poderá não conseguir fazer a redução vertical se os pods não puderem ser movidos, como nas seguintes situações:

* Um pod criado diretamente e que não tem o suporte de um objeto de controlador, como uma implantação ou um conjunto de réplicas.
* Um PDB (orçamento de interrupção de pod) é muito restritivo e não permite que o número de pods fique abaixo de determinado limite.
* Um pod usa seletores de nó ou uma antiafinidade que não pode ser cumprida se ele está agendado em outro nó.

Para obter mais informações sobre como o dimensionador automático de cluster pode não conseguir fazer a redução vertical, confira [Quais tipos de pods podem impedir que o dimensionador automático de cluster remova um nó?][autoscaler-scaledown]

O dimensionador automático de cluster usa parâmetros de inicialização para itens como intervalos de tempo entre eventos de escala e limites de recursos. Esses parâmetros são definidos pela plataforma Azure e atualmente não são expostos para seu ajuste. Para obter mais informações sobre quais parâmetros são usados pelo dimensionador automático de cluster, confira [Quais são os parâmetros do dimensionador automático de cluster?][autoscaler-parameters].

Os dois dimensionadores automáticos podem trabalhar juntos e geralmente são implantados em um cluster. Quando combinados, o dimensionador automático de pod horizontal se concentra na execução do número de pods necessários para atender à demanda de aplicativo. O dimensionador automático de cluster se concentra na execução do número de nós necessários para dar suporte aos pods agendados.

> [!NOTE]
> O dimensionamento manual é desabilitado quando o dimensionador automático de cluster é usado. Deixe o dimensionador automático de cluster determinar o número de nós necessários. Caso deseje dimensionar o cluster manualmente, [desabilite o dimensionador automático de cluster](#disable-the-cluster-autoscaler).

## <a name="create-an-aks-cluster-and-enable-the-cluster-autoscaler"></a>Criar um cluster do AKS e habilitar o dimensionador automático de cluster

Caso precise criar um cluster do AKS, use o comando [az aks create][az-aks-create]. Especifique uma *--kubernetes-version* que atenda ao número de versão mínima necessário ou que exceda esse número, conforme descrito na seção anterior [Antes de começar](#before-you-begin). Para habilitar e configurar o dimensionador automático de cluster, use o parâmetro *--enable-cluster-autoscaler* e especifique um nó *--min-count* e *--max-count*.

O seguinte exemplo cria um cluster do AKS com o conjunto de dimensionamento de máquinas virtuais habilitado e usa um mínimo de *1* e um máximo de *3* nós:

```azurecli-interactive
# First create a resource group
az group create --name myResourceGroup --location canadaeast

# Now create the AKS cluster and enable the cluster autoscaler
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --kubernetes-version 1.12.4 \
  --node-count 1 \
  --enable-vmss \
  --enable-cluster-autoscaler \
  --min-count 1 \
  --max-count 3
```

São necessários alguns minutos para criar o cluster e definir as configurações do dimensionador automático de cluster.

### <a name="enable-the-cluster-autoscaler-on-an-existing-aks-cluster"></a>Habilitar o dimensionador automático de cluster em um cluster do AKS existente

Habilite o dimensionador automático de cluster em um cluster do AKS existente que atenda aos requisitos, conforme descrito na seção anterior [Antes de começar](#before-you-begin). Use o comando [az aks update][az-aks-update], escolha *--enable-cluster-autoscaler* e, em seguida, especifique um nó *--min-count* e *--max-count*. O seguinte exemplo habilita o dimensionador automático de cluster em um cluster existente que usa um mínimo de *1* e um máximo de *3* nós:

```azurecli-interactive
az aks update \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --enable-cluster-autoscaler \
  --min-count 1 \
  --max-count 3
```

Se a contagem mínima de nós for maior que o número de nós existentes no cluster, serão necessários alguns minutos para criar os nós adicionais.

## <a name="change-the-cluster-autoscaler-settings"></a>Alterar as configurações do dimensionador automático de cluster

Na etapa anterior para criar ou atualizar um cluster do AKS existente, a contagem mínima de nós do dimensionador automático de cluster foi definida como *1* e a contagem máxima de nós foi definida como *3*. Conforme as demandas de aplicativo mudam, você pode precisar ajustar a contagem de nós do dimensionador automático de cluster.

Para alterar a contagem de nós, use o comando [az aks update][az-aks-update] e especifique um valor mínimo e máximo. O seguinte exemplo define a *--min-count* como *1* e a *--max-count* como *5*:

```azurecli-interactive
az aks update \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --update-cluster-autoscaler \
  --min-count 1 \
  --max-count 5
```

> [!NOTE]
> Durante a versão prévia, não é possível definir uma contagem mínima de nós maior que a atualmente definida para o cluster. Por exemplo, se atualmente você tiver uma contagem mínima definida como *1*, não poderá atualizar a contagem mínima para *3*.

Monitore o desempenho de seus aplicativos e serviços e ajuste as contagens de nós do dimensionador automático de cluster para que correspondam ao desempenho necessário.

## <a name="disable-the-cluster-autoscaler"></a>Desabilitar o dimensionador automático de cluster

Se você não deseja mais usar o dimensionador automático de cluster, desabilite-o usando o comando [az aks update][az-aks-update]. Os nós não são removidos quando o dimensionador automático de cluster é desabilitado.

Para remover o dimensionador automático de cluster, especifique o parâmetro *--disable-cluster-autoscaler*, conforme mostrado no seguinte exemplo:

```azurecli-interactive
az aks update \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --disable-cluster-autoscaler
```

Dimensione o cluster manualmente usando o comando [az aks scale][az-aks-scale]. Se você usar o dimensionador automático de pod horizontal, esse recurso continuará sendo executado com o dimensionador automático de cluster desabilitado, mas os pods poderão acabar não conseguindo ser agendados se os recursos do nó estiverem todos em uso.

## <a name="next-steps"></a>Próximas etapas

Este artigo mostrou como dimensionar automaticamente o número de nós do AKS. Você também pode usar o dimensionador automático de pod horizontal para ajustar automaticamente o número de pods que executam o aplicativo. Para obter as etapas de como usar o dimensionador automático de pod horizontal, confira [Dimensionar aplicativos no AKS][aks-scale-apps].

<!-- LINKS - internal -->
[aks-upgrade]: upgrade-cluster.md
[azure-cli-install]: /cli/azure/install-azure-cli
[az-aks-show]: /cli/azure/aks#az-aks-show
[az-extension-add]: /cli/azure/extension#az-extension-add
[aks-scale-apps]: tutorial-kubernetes-scale.md
[az-aks-create]: /cli/azure/aks#az-aks-create
[az-aks-scale]: /cli/azure/aks#az-aks-scale

<!-- LINKS - external -->
[az-aks-update]: https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview
[terms-of-use]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[autoscaler-scaledown]: https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-types-of-pods-can-prevent-ca-from-removing-a-node
[autoscaler-parameters]: https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-are-the-parameters-to-ca
