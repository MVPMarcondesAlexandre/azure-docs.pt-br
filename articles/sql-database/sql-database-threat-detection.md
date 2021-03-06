---
title: Detecção de ameaças – Banco de Dados SQL do Azure | Microsoft Docs
description: A Detecção de Ameaças detecta as atividades anormais do banco de dados que indicam possíveis ameaças de segurança contra o banco de dados em um banco de dados individual ou um pool elástico.
services: sql-database
ms.service: sql-database
ms.subservice: security
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: rmatchoro
ms.author: ronmat
ms.reviewer: vanto, carlrab
manager: craigg
ms.date: 01/30/2019
ms.openlocfilehash: 032146742c1a49fc8cdbda24d5c732add3cc5ea7
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55465343"
---
# <a name="azure-sql-database-threat-detection-for-standalone-or-pooled-database"></a>Detecção de ameaças do Banco de Dados SQL do Azure para banco de dados autônomo ou em pool

A [Detecção de Ameaças](sql-database-threat-detection-overview.md) do SQL do Azure para bancos de dados autônomos ou em pool detecta atividades anômalas que indicam tentativas incomuns e potencialmente prejudiciais de acessar ou explorar bancos de dados. A Detecção de Ameaças pode identificar **Possíveis injeções de SQL**, **Acesso de um data center ou localização incomum**, **Acesso de uma entidade de segurança desconhecida ou de um aplicativo potencialmente prejudicial** e **Credenciais SQL de força bruta** – veja mais detalhes em [Alertas da Detecção de Ameaças](sql-database-threat-detection-overview.md#azure-sql-database-threat-detection-alerts).

Você pode receber notificações sobre as ameaças detectadas por meio de [notificações por email](sql-database-threat-detection-overview.md#explore-anomalous-database-activities-upon-detection-of-a-suspicious-event) ou do [Portal do Azure](sql-database-threat-detection-overview.md#explore-threat-detection-alerts-for-your-database-in-the-azure-portal)

A [Detecção de Ameaças](sql-database-threat-detection-overview.md) faz parte da oferta [ADS](sql-advanced-threat-protection.md) (Segurança de Dados Avançada do SQL), um pacote unificado de funcionalidades avançadas de segurança do SQL. A Detecção de Ameaças pode ser acessada e gerenciada por meio do portal central da ADS do SQL. O pacote de Segurança de Dados Avançada é cobrado a USD 15/mês por servidor lógico, com os primeiros 30 dias gratuitos.

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a>Configurar a detecção de ameaças para seu banco de dados no Portal do Azure

1. Inicie o portal do Azure em [https://portal.azure.com](https://portal.azure.com).
2. Navegue para a página de configuração do servidor de Banco de Dados SQL do Azure que você deseja proteger. Nas configurações de segurança, selecione **Segurança de Dados Avançada**.
3. Na página de configuração **Segurança de Dados Avançada**:

   - Habilite a Segurança de Dados Avançada no servidor.
   - Em **Configurações de Detecção de Ameaças**, na caixa de texto **Enviar alertas para**, forneça a lista de endereços de email para receber alertas de segurança na detecção de atividades anômalas de banco de dados.
  
   ![Configurar detecção de ameaças](./media/sql-database-threat-detection/set_up_threat_detection.png)

## <a name="set-up-threat-detection-using-powershell"></a>Configurar a detecção de ameaças usando o PowerShell

Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre a [Detecção de Ameaças](sql-database-threat-detection-overview.md).
- Saiba mais sobre a [Detecção de Ameaças em uma Instância Gerenciada](sql-database-managed-instance-threat-detection.md).  
- Saiba mais sobre a [Segurança de Dados Avançada do SQL](sql-advanced-threat-protection.md).
- Saiba mais sobre a [Auditoria do Banco de Dados SQL do Azure](sql-database-auditing.md)
- Saiba mais sobre a [Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)
- Para saber mais sobre preços, visite a [página de Preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/)  
