---
title: Criar um Load Balancer com front-end de zona – Azure PowerShell
titlesuffix: Azure Load Balancer
description: Saiba como criar um Standard Load Balancer com front-end de zona usando o Azure PowerShell
services: load-balancer
documentationcenter: na
author: KumudD
manager: twooley
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.custom: seodec18
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/26/2018
ms.author: kumud
ms.openlocfilehash: 861759eec266f0ab66d30a466c06e7d2ee14bf06
ms.sourcegitcommit: f4b78e2c9962d3139a910a4d222d02cda1474440
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54247150"
---
#  <a name="create-a-standard-load-balancer-with-zonal-frontend-using-azure-powershell"></a>Criar um Standard Load Balancer com front-end de zona usando o Azure PowerShell

Este artigo segue as etapas para a criação de um [Standard Load Balancer](https://aka.ms/azureloadbalancerstandard) público com um front-end de zona usando um endereço IP Público Standard. Para entender como as zonas de disponibilidade funcionam com o Load Balancer Standard, consulte [Zonas de disponibilidade e Load Balancer Standard](load-balancer-standard-availability-zones.md). 

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

> [!NOTE]
> O suporte para Zonas de Disponibilidade está disponível para selecionar recursos e regiões do Azure e famílias de tamanho de VM. Para obter mais informações sobre como começar e com quais recursos, regiões e famílias de tamanhos de VM do Azure você pode experimentar as zonas de disponibilidade, confira [Visão geral das Zonas de Disponibilidade](https://docs.microsoft.com/azure/availability-zones/az-overview). Para obter suporte, entre em contato em [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) ou [abra um tíquete de suporte do Azure](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="log-in-to-azure"></a>Fazer logon no Azure

Faça logon na sua assinatura do Azure com o comando `Connect-AzureRmAccount` e siga as instruções na tela.

```powershell
Connect-AzureRmAccount
```

## <a name="create-resource-group"></a>Criar grupo de recursos

Crie um Grupo de Recursos usando o seguinte comando:

```powershell
New-AzureRmResourceGroup -Name myResourceGroupZLB -Location westeurope
```

## <a name="create-a-public-ip-standard"></a>Criar um IP público Standard 
Crie um IP Público Standard usando o seguinte comando:

```powershell
$publicIp = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupZLB -Name 'myPublicIPZonal' `
  -Location westeurope -AllocationMethod Static -Sku Standard -zone 1
```

## <a name="create-a-front-end-ip-configuration-for-the-website"></a>Criar uma configuração de IP de front-end para o site

Crie uma configuração de IP de front-end usando o seguinte comando:

```powershell
$feip = New-AzureRmLoadBalancerFrontendIpConfig -Name 'myFrontEnd' -PublicIpAddress $publicIp
```

## <a name="create-the-back-end-address-pool"></a>Criar o pool de endereços de back-end

Crie um pool de endereços de back-end usando o seguinte comando:

```powershell
$bepool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name 'myBackEndPool'
```

## <a name="create-a-load-balancer-probe-on-port-80"></a>Criar uma investigação do balanceador de carga na porta 80

Crie uma investigação de integridade para o balanceador de carga na porta 80 usando o seguinte comando:

```powershell
$probe = New-AzureRmLoadBalancerProbeConfig -Name 'myHealthProbe' -Protocol Http -Port 80 `
  -RequestPath / -IntervalInSeconds 360 -ProbeCount 5
```

## <a name="create-a-load-balancer-rule"></a>Criar uma regra de balanceador de carga
 Crie uma regra do balanceador de carga usando o seguinte comando:

```powershell
   $rule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $feip -BackendAddressPool  $bepool -Probe $probe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

## <a name="create-a-load-balancer"></a>Criar um balanceador de carga
Crie um Standard Load Balancer usando o comando a seguir:

```powershell
$lb = New-AzureRmLoadBalancer -ResourceGroupName myResourceGroupZLB -Name 'MyLoadBalancer' -Location westeurope `
  -FrontendIpConfiguration $feip -BackendAddressPool $bepool `
  -Probe $probe -LoadBalancingRule $rule -Sku Standard
```

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre o [Load Balancer Standard e Zonas de Disponibilidade](load-balancer-standard-availability-zones.md).



