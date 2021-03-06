---
title: Arquivo de inclusão
description: Arquivo de inclusão
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 2c1a4a1931bc2e38b0bee5f90518b01fdf4767a1
ms.sourcegitcommit: 95d9a6acf29405a533db943b1688612980374272
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2018
ms.locfileid: "30196742"
---
Se você estiver trabalhando com o modelo de implantação do Gerenciador de Recursos, poderá alterar para as novas SKUs do gateway. Quando você muda de um SKU de gateway herdado para um novo SKU, você exclui o gateway VPN existente e cria um novo gateway de VPN.

Fluxo de trabalho:

1. Remova todas as conexões com o gateway de rede virtual.
2. Exclua o gateway de VPN antigo.
3. Crie o novo gateway de VPN.
4. Atualize os dispositivos VPN locaia com o novo endereço IP do gateway de VPN (para conexões Site a Site).
5. Atualize o valor de endereço IP do gateway para gateways de rede local VNet para VNet que se conectam a esse gateway.
6. Baixe novos pacotes de configuração do cliente VPN para clientes de P2S que se conectam à rede virtual por meio desse gateway de VPN.
7. Recrie as conexões para o gateway de rede virtual.

Considerações:

* Para mover para as novas SKUs, o gateway VPN deve estar no modelo de implantação do Gerenciador de Recursos.
* Se você tiver um gateway VPN clássico, você deve continuar usando os SKUs herdados mais antigos para esse gateway, no entanto, você pode redimensionar entre as SKUs herdadas. Você não pode mudar para as novas SKUs.
* Ao mudar de uma SKU herdada para uma nova SKU, você terá tempo de inatividade de conectividade.
* Ao mudar para uma nova SKU de gateway, o endereço IP público de seu gateway de VPN mudará. Isso acontece mesmo se você especificar o mesmo objeto de endereço IP público que usou anteriormente.