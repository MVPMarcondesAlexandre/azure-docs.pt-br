---
title: Manutenção planejada - SQL Data Warehouse do Azure | Microsoft Docs
description: Aprenda como preparar-se para eventos de manutenção planejada no SQL Data Warehouse do Azure.
services: sql-data-warehouse
author: antvgski
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.subservice: manage
ms.date: 04/19/2018
ms.author: anvang
ms.reviewer: igorstan
ms.openlocfilehash: 05f82ae571bea41c15099b52282f4efe29b2c763
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55468403"
---
# <a name="planning-for-maintenance-on-your-azure-sql-data-warehouse"></a>Planejar a manutenção no SQL Data Warehouse do Azure

Saiba como preparar-se para eventos de manutenção planejados no SQL Data Warehouse do Azure.

## <a name="what-is-a-planned-maintenance-event"></a>O que é um evento de manutenção planejada?
Um evento de manutenção planejado é uma janela de tempo em que o data warehouse precisa estar offline para uma operação de manutenção. Esses eventos são oportunidades para aplicar atualizações de serviço, novos recursos ou patches. 

## <a name="frequency"></a>Frequência
Em média, pelo menos um evento de manutenção planejada ocorre a cada mês. 

## <a name="notifications-and-downtime"></a>Notificações e tempo de inatividade
Você receberá uma notificação antes de cada evento de manutenção planejada. O evento de manutenção cancela todas as consultas em execução e coloca o data warehouse offline. O tempo de inatividade esperado para cada data warehouse é de aproximadamente 30 minutos. Você pode esperar uma notificação quando a manutenção for concluída. 

## <a name="setting-up-alerts"></a>Configurar Alertas

É recomendável usar o [Azure Monitor](../azure-monitor/platform/alerts-activity-log-service-notifications.md) para configurar alertas de log de manutenção planejada. Os alertas podem ajudá-lo a planejar a manutenção necessária para minimizar o impacto nos negócios. 

Para configurar notificações, use estas [instruções de alerta de log](../azure-monitor/platform/alerts-activity-log-service-notifications.md). 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre monitoramento, consulte [Monitorar a carga de trabalho](sql-data-warehouse-manage-monitor.md).
