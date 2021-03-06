---
title: 'Configurar conexões VPN site a site e de ExpressRoute – coexistir: PowerShell: Azure | Microsoft Docs'
description: Configure uma conexão VPN site a site e de ExpressRoute que pode coexistir para o modelo do Resource Manager usando o PowerShell.
services: expressroute
author: charwen
ms.service: expressroute
ms.topic: conceptual
ms.date: 01/07/2019
ms.author: charwen
ms.custom: seodec18
ms.openlocfilehash: a35bde6e89290fd2282ba6ec829f46cb4c6fc225
ms.sourcegitcommit: 30d23a9d270e10bb87b6bfc13e789b9de300dc6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54103308"
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-using-powershell"></a>Configurar conexões coexistentes Site a Site e ExpressRoute usando o PowerShell
> [!div class="op_single_selector"]
> * [PowerShell – Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - clássico](expressroute-howto-coexist-classic.md)
> 
> 


Este artigo descreve como configurar as conexões VPN site a site e de ExpressRoute que coexistam. Poder configurar a VPN site a site e o ExpressRoute tem várias vantagens. Você pode configurar um VPN Site a Site como um caminho de failover seguro para o ExpressRoute ou usar VPNs Site a Site para se conectar a sites que não estão conectados por meio do ExpressRoute. Neste artigo, analisaremos as etapas para configurar as duas situações. Este artigo se aplica ao modelo de implantação do Gerenciador de Recursos.

Configurar conexões coexistentes VPN Site a Site e a ExpressRoute tem várias vantagens:

* Você pode configurar uma VPN site a site como um caminho de failover seguro para o ExpressRoute. 
* Como alternativa, você pode usar VPNs Site a Site para se conectar a sites que não estão conectados por meio de ExpressRoute. 

As etapas para configurar as duas situações são cobertas neste artigo. Este artigo se aplica ao modelo de implantação do Gerenciador de Recursos e usa o PowerShell. Você também pode configurar esses cenários usando o portal do Azure, embora a documentação ainda não esteja disponível. Você pode configurar um gateway pela primeira vez. Normalmente, você não incorrerá em tempo de inatividade ao adicionar uma nova conexão de gateway ou gateway.



>[!NOTE]
>Se você quiser criar uma VPN Site a Site por um circuito ExpressRoute, consulte [este artigo](site-to-site-vpn-over-microsoft-peering.md).
>

## <a name="limits-and-limitations"></a>Limites e limitações
* **Não há suporte para o roteamento do tráfego.** Não é possível fazer o roteamento (por meio do Azure) entre sua rede local conectada via VPN Site a Site e sua rede local conectada via ExpressRoute.
* **Não há suporte para o gateway SKU básico.** Você deve usar um gateway SKU não Básico para o [gateway de ExpressRoute](expressroute-about-virtual-network-gateways.md) e o [gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Há suporte para apenas um gateway de VPN baseado em rotas.** Você deve usar uma rota baseada no [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **O roteamento estático deve ser configurado para o gateway de VPN.** Se sua rede local estiver conectada à VPN Site a Site e de ExpressRoute, será necessário ter uma rota estática configurada em sua rede local para rotear a conexão VPN Site a Site para a Internet pública.
* **O Gateway de VPN usa ASN 65515 como padrão se essa opção não é especificada.** O Gateway de VPN do Azure dá suporte ao protocolo de roteamento BGP. Você pode especificar o ASN (número AS) de uma rede virtual adicionando a opção -Asn. Se você não especificar esse parâmetro, o número AS padrão será 65515. Você pode usar qualquer ASN para a configuração, mas se selecionar algo diferente de 65515, precisará redefinir o gateway para que a configuração entre em vigor.

## <a name="configuration-designs"></a>Designs de configuração
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurar uma VPN site a site como um caminho de failover para o ExpressRoute
Você pode configurar uma conexão VPN site a site como um backup para o ExpressRoute. Esta conexão se aplica apenas às redes virtuais vinculadas ao caminho de emparelhamento privado do Azure. Não há uma solução de failover com base em VPN para serviços acessíveis por meio de emparelhamentos do Azure e da Microsoft. O circuito do ExpressRoute sempre será o link principal. Os dados só fluirão pelo caminho da VPN Site a Site se o circuito do ExpressRoute falhar. Para evitar o roteamento assimétrico, sua configuração de rede local também deve preferir o circuito de ExpressRoute pela VPN Site a Site. Você pode preferir que o caminho de rota expressa por preferência mais alta local de configuração para as rotas que recebeu a ExpressRoute. 

> [!NOTE]
> Embora o circuito ExpressRoute seja preferencial em relação à VPN Site a Site quando ambas as rotas são as mesmas, o Azure usa a correspondência de prefixo mais longa para escolher a rota até o destino do pacote.
> 
> 

![Coexistência](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a>Configurar uma VPN site a site para se conectar a sites não conectados por meio do ExpressRoute
Você pode configurar sua rede de modo que alguns sites se conectem diretamente ao Azure através da VPN site a site, e alguns sites se conectem por meio do ExpressRoute. 

![Coexistência](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Não é possível configurar uma rede virtual como um roteador de trânsito.
> 
> 

## <a name="selecting-the-steps-to-use"></a>Selecionando as etapas de uso
Há dois conjuntos diferentes de procedimentos para escolher. O procedimento de configuração selecionado varia conforme você já tenha uma rede virtual à qual deseja se conectar ou queira criar uma nova rede virtual.

* Não tenho uma VNet e preciso criar uma.
  
    Se você ainda não tiver uma rede virtual, esse procedimento explica como criar uma nova rede virtual usando o modelo de implantação do Gerenciador de Recursos e criando novas conexões de VPN Site a Site e de ExpressRoute. Para configurar uma rede virtual, siga as etapas em [Para criar uma nova rede virtual e conexões coexistentes](#new).
* Eu já tenho uma VNet do modelo de implantação do Gerenciador de Recursos.
  
    Talvez você já tenha uma rede virtual implementada com uma conexão de VPN Site a Site ou uma conexão de ExpressRoute existente. Neste cenário, se a máscara de sub-rede de gateway é /28 ou menor (/28, /29, etc.), você precisa excluir o gateway existente. A seção [Para configurar conexões coexistentes para uma VNet já existente](#add) explica como excluir o gateway e, em seguida, criar novas conexões de VPN Site a Site e de ExpressRoute.
  
    Se você excluir e recriar o gateway, você terá tempo de inatividade para as conexões entre locais. Entretanto, suas VMs e serviços ainda poderão se comunicar por meio do balanceador de carga enquanto você configura o seu gateway, se estiverem configurados para fazer isso.

## <a name="new"></a>Para criar uma nova rede virtual e conexões coexistentes
Este procedimento orientará você na criação de uma VNet, bem como na criação das conexões Site a Site e de ExpressRoute que coexistirão.

1. Instale a versão mais recente dos cmdlets do Azure PowerShell. Para saber mais sobre como instalar os cmdlets do PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview). Os cmdlets que você usará para essa configuração podem ser ligeiramente diferentes daqueles com os quais você talvez esteja familiarizado. Certifique-se de usar os cmdlets especificados nestas instruções.

2. Entre sua conta e configurar o ambiente.

  ```powershell
  Connect-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65515
  ```
3. Crie uma rede virtual incluindo uma Sub-rede de Gateway. Para saber mais sobre como criar uma rede virtual, confira [Criar uma rede virtual](../virtual-network/manage-virtual-network.md#create-a-virtual-network). Para saber mais sobre como criar sub-redes, confira [Criar uma sub-rede](../virtual-network/virtual-network-manage-subnet.md#add-a-subnet)
   
   > [!IMPORTANT]
   > A Sub-rede de Gateway deve ser /27 ou um prefixo mais curto (como /26 ou /25).
   > 
   > 
   
    Crie uma nova VNet.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Adicione sub-redes.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Salve a configuração da VNet.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="vpngw"></a>Em seguida, crie seu gateway de VPN Site a Site. Para obter mais informações sobre a configuração do gateway de VPN, consulte [Configurar uma VNet com uma conexão Site a Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). O GatewaySku tem suporte para os gateway VPN em *VpnGw1*, *VpnGw2*, *VpnGw3*, *Standard* e *HighPerformance*. Configurações de coexistência de ExpressRoute-Gateway de VPN não têm suporte na SKU Básica. O VpnType deve ser *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "VpnGw1"
  ```
   
    O Gateway de VPN do Azure oferece suporte ao protocolo de roteamento BGP. Você pode especificar o ASN (número AS) para essa Rede Virtual, adicionando a opção -Asn ao comando a seguir. Não especificando que esse parâmetro terá como padrão o AS número 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "VpnGw1" -Asn $VNetASN
  ```
   
    Você pode encontrar o IP do emparelhamento BGP e o número AS que o Azure usa para o gateway de VPN em $azureVpn.BgpSettings.BgpPeeringAddress e $azureVpn.BgpSettings.Asn. Para obter mais informações, consulte [Configurar BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) para o gateway de VPN do Azure.
5. Crie uma entidade de gateway de VPN de site local. Esse comando não configura seu gateway de VPN local. Em vez disso, ele permite que você forneça as configurações de gateway local, como o IP público e o espaço para endereço local, para que o gateway de VPN do Azure possa se conectar a ele.
   
    Se seu dispositivo VPN local só dá suporte ao roteamento estático, você pode configurar as rotas estáticas da seguinte maneira:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Se seu dispositivo VPN local suporta o BGP e você deseja habilitar o roteamento dinâmico, é preciso saber o IP do emparelhamento BGP e o número AS que seu dispositivo VPN local usa.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
6. Configure seu dispositivo VPN local para conectar o novo gateway de VPN do Azure. Para obter mais informações sobre a configuração de dispositivo VPN, consulte [Configuração do Dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).

7. Vincule o gateway de VPN Site a Site no Azure ao gateway local.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```
 

8. Se você estiver se conectando a um circuito de ExpressRoute existente, ignore as etapas 8 e 9 e ir para a etapa 10. Configurar circuitos do ExpressRoute. Para obter mais informações sobre a configuração de circuito de ExpressRoute, consulte [criar um circuito de ExpressRoute](expressroute-howto-circuit-arm.md).


9. Configure o emparelhamento particular do Azure através do circuito de ExpressRoute. Para obter mais informações sobre como configurar o emparelhamento particular do Azure através do circuito de ExpressRoute, consulte [Configurar emparelhamento](expressroute-howto-routing-arm.md)

10. <a name="gw"></a>Crie um gateway de ExpressRoute. Para obter mais informações sobre a configuração do gateway de ExpressRoute, confira [Configuração do gateway de ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). O Gateway SKU deve ser *Standard*, *HighPerformance* ou *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
11. Vincule o gateway de ExpressRoute ao circuito de ExpressRoute. Após essa etapa for concluída, a conexão entre sua rede local e o Azure, por meio de ExpressRoute, é estabelecida. Para obter mais informações sobre a operação de vinculação, confira [Vincular VNets à ExpressRoute](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```

## <a name="add"></a>Para configurar conexões coexistentes para uma VNet já existente
Se você tiver uma rede virtual que tem apenas um gateway de rede virtual (por exemplo, o gateway VPN Site a Site) e quiser adicionar outro gateway de um tipo diferente (por exemplo, gateway de ExpressRoute), verifique o tamanho da sub-rede de gateway. Se a sub-rede de gateway for /27 ou maior, você poderá ignorar as etapas abaixo e executar as etapas na seção anterior para adicionar um gateway de VPN Site a Site ou um gateway de ExpressRoute. Se a sub-rede do gateway é /28 ou /29, você deve primeiro excluir o gateway da rede virtual e aumentar o tamanho de sub-rede do gateway. As etapas nesta seção mostram como fazer isso.

1. Você precisará instalar a versão mais recente dos cmdlets do Azure PowerShell. Para saber mais sobre como instalar cmdlets, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview). Os cmdlets que você usará para essa configuração podem ser ligeiramente diferentes daqueles com os quais você talvez esteja familiarizado. Certifique-se de usar os cmdlets especificados nestas instruções. 
2. Exclua o gateway de ExpressRoute ou gateway de VPN Site a Site existente.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Exclua a Sub-rede de Gateway.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Adicione uma Sub-rede de Gateway que seja /27 ou maior.
   
   > [!NOTE]
   > Se você não tiver endereços IP suficientes restantes em sua rede virtual para aumentar o tamanho da sub-rede do gateway, precisará adicionar mais espaço de endereço IP.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Salve a configuração da VNet.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. Neste ponto, você terá uma rede virtual sem gateways. Para criar novos gateways e configurar as conexões, execute as etapas na seção anterior.

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a>Para adicionar a configuração de ponto a site ao gateway de VPN
Você pode seguir as etapas abaixo para adicionar a configuração ponto a ponto ao seu gateway VPN em uma configuração de coexistência.

1. Adicione o pool de endereços do Cliente VPN.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Carregue o certificado-raiz da VPN para Azure para seu gateway de VPN. Neste exemplo, presume-se que o certificado raiz está armazenado no computador local onde os seguintes cmdlets do PowerShell são executados.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) 
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Para saber mais sobre a VPN de Ponto a Site, confira [Configurar uma conexão de Ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o ExpressRoute, consulte [Perguntas Frequentes sobre ExpressRoute](expressroute-faqs.md).
