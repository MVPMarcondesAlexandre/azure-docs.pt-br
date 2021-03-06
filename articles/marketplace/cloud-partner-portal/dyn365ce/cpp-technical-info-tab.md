---
title: Guia Informações técnicas do Dynamics 365 for Customer Engagement – Azure Marketplace | Microsoft Docs
description: Como especificar as informações técnicas para um aplicativo do Dynamics 365 for Customer Engagement no AppSource Marketplace.
services: Dynamics 365 for Customer Engagement Offer, Azure, Marketplace, Cloud Partner Portal, AppSource
documentationcenter: ''
author: v-miclar
manager: Patrick.Butler
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: conceptual
ms.date: 01/02/2019
ms.author: pbutlerm
ms.openlocfilehash: 214abd64232130dd3fd5fdde510f7545732ac82e
ms.sourcegitcommit: fbf0124ae39fa526fc7e7768952efe32093e3591
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54081449"
---
# <a name="dynamics-365-for-customer-engagement-technical-info-tab"></a>Guia Informações técnicas do Dynamics 365 for Customer Engagement

A guia **Informações técnicas** da página **Nova Oferta** permite que você especifique informações detalhadas sobre o aplicativo do Dynamics 365 for Customer Engagement, incluindo ativos de logotipo de marketing e de pacote de CRM.  Essa guia é dividida em quatro seções: **Informações do Aplicativo**, **Pacote de CRM**, **Disponibilidade do Pacote de CRM** e **Artefatos de Marketing**. Um asterisco anexado (*) em um nome do campo indica que ele é obrigatório. 


## <a name="application-info-section"></a>Seção Informações do aplicativo

Você fornecerá detalhes sobre seu aplicativo do Dynamics 365 nesta seção.

![Seção Informações do aplicativo da guia Informações técnicas](./media/dynce-technical-info-tab1.png)

A tabela a seguir descreve cada um desses campos.

|      Campo                    |    DESCRIÇÃO                  |
|    ---------                  |  ---------------                |
|   Modelo de licença básica          |  O modelo de licença determina como os clientes são atribuídos a seu aplicativo no Centro de Administração do Dynamics 365. O licenciamento de **Recursos** é baseado na instância, enquanto licenças de **Usuário** são atribuídas uma por locatário.  |
|  Saída de S2S & Acesso ao Repositório Seguro de CRM |  Permite a configuração do Repositório Seguro de CRM ou o acesso S2S (servidor para servidor) de saída. *Este recurso exige uma consideração especializada da equipe do Dynamics 365 durante a fase de certificação.* Microsoft entrará em contato com você para concluir as etapas adicionais para dar suporte ao recurso.  |
| Assinar eventos de ciclo de vida do CRM | A integração com eventos de ciclo de vida do Dynamics 365 exige que você forneça um serviço dedicado, registrado por meio de um contrato especial com a Microsoft. *Este recurso exige uma consideração especializada da equipe do Dynamics 365 durante a fase de certificação.* Você será contatado para concluir etapas adicionais para dar suporte a essa funcionalidade.  |
| URL de Configuração do Aplicativo | URL da página da Web que permite ao usuário configurar o aplicativo |
| Produtos aplicáveis do Dynamics 365  | Selecione os produtos do Dynamics 365 a que essa oferta se aplica. Esta oferta será exibida em produtos selecionados no AppSource.  |
| Somente Alterações de Marketing         | Configurar esta opção como Sim indica que apenas alterações de marketing/descritivas foram feitas na oferta existente.  Essas alterações permitem que a oferta ignore os estágios de certificação e provisionamento.  |
|  |  |


## <a name="crm-package-section"></a>Seção Pacote de CRM

Você fornecerá detalhes sobre o arquivo do pacote do AppSource nesta seção.  Essas informações serão usadas pelas equipes de validação e certificação do Dynamics 365.

![Seção Pacote de CRM da guia Informações técnicas](./media/dynce-technical-info-tab2.png)

A tabela a seguir descreve cada um desses campos.

|      Campo                    |    DESCRIÇÃO                  |
|    ---------                  |  ---------------                |
|  Nome do arquivo do seu pacote     |  Nome do arquivo do seu pacote (.zip).  Esse nome *não* é público e será usado internamente pela equipe de certificação do Dynamics 365.  |
|  Url                          |  URL de uma conta de Armazenamento do Azure que contém o arquivo do pacote carregado. Essa URL deve incluir uma chave SAS somente leitura para permitir que a nossa equipe obtenha seu pacote para verificação.  |
| Mais de um pacote de CRM     | Selecione Sim APENAS se você estiver dando suporte a várias versões de CRM com pacotes diferentes.  Cada versão terá um arquivo de pacote correspondente que você precisa criar individualmente.  |
| Ativo de cenário e caso de uso   | Habilita o upload de um documento de especificação funcional para seu aplicativo, para uso pela equipe de validação do Dynamics 365.  O formato preferencial dessa especificação é o [Modelo de cenário do usuário E2E](http://download.microsoft.com/download/5/1/8/51812AC9-BCD8-489F-937C-5D439C494EC1/E2E%20User%20Scenario%20Template.docx).  |
|  |  |


## <a name="crm-package-availability-section"></a>Seção Disponibilidade do Pacote de CRM

Nesta seção, selecione em quais regiões geográficas seu aplicativo estará disponível para os clientes.  A implantação nas seguintes regiões soberanas *exigem uma permissão e validação especial* durante o processo de certificação: [Alemanha](https://docs.microsoft.com/azure/germany/), [Nuvem do Governo dos EUA](https://docs.microsoft.com/azure/azure-government/documentation-government-welcome) e TIP.


## <a name="marketing-artifacts-section"></a>Seção de artefatos de marketing

Essa seção exige que você carregue um logotipo do aplicativo que será usado para representar seu pacote no AppSource Marketplace.  A imagem do logotipo deve estar no formato PNG e deve ter o tamanho de 255 x 115 pixels.


## <a name="next-steps"></a>Próximas etapas

É recomendável que você ofereça uma demonstração de seu aplicativo completando a [guia de Test Drive](./cpp-testdrive-tab.md)
