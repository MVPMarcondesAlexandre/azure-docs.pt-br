---
title: Configurar alertas de métricas para o Banco de Dados do Azure para PostgreSQL no Portal do Azure
description: Este artigo descreve como configurar e acessar os alertas de métricas para o Banco de Dados do Azure para PostgreSQL usando o Portal do Azure.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 01/11/2019
ms.openlocfilehash: a999553d7ba26daba674534b1656e90ad0de4f5f
ms.sourcegitcommit: f4b78e2c9962d3139a910a4d222d02cda1474440
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54243960"
---
# <a name="use-the-azure-portal-to-set-up-alerts-on-metrics-for-azure-database-for-postgresql"></a>Usar o Portal do Azure para configurar alertas de métricas no Banco de Dados do Azure para PostgreSQL 

Este artigo mostra como configurar alertas do Banco de Dados do Azure para PostgreSQL usando o Portal do Azure. Você pode receber um alerta com base em métricas de monitoramento para seus serviços do Azure.

O alerta é disparado quando o valor de uma métrica especificada ultrapassa um limite atribuído por você. Ele dispara tanto quando a condição é atendida pela primeira vez e quanto posteriormente, quando essa condição não está mais sendo atendida. 

Você pode configurar um alerta para fazer as seguintes ações quando ele disparar:
* Enviar notificações por email para o administrador e coadministradores de serviços.
* Enviar um email para outros emails que você especificar.
* Chamar um webhook.

Você pode configurar e obter informações sobre as regras de alerta usando:
* [Portal do Azure](../azure-monitor/platform/alerts-metric.md#create-with-azure-portal)
* [CLI do Azure](../azure-monitor/platform/alerts-metric.md#with-azure-cli)
* [API REST do Monitor do Azure](https://docs.microsoft.com/rest/api/monitor/metricalerts)

## <a name="create-an-alert-rule-on-a-metric-from-the-azure-portal"></a>Criar uma regra de alerta em uma métrica no Portal do Azure
1. No [Portal do Azure](https://portal.azure.com/), selecione o servidor do Banco de Dados do Azure para PostgreSQL que você deseja monitorar.

2. Na seção **Monitoramento** da barra lateral, selecione **Alertas** como mostrado abaixo:

   ![Selecionar Regras de Alerta](./media/howto-alert-on-metric/2-alert-rules.png)

3. Selecione **Adicionar alerta de métrica** (ícone +).

4. A página **Criar regra** é aberta, conforme mostrado abaixo. Preencha as informações obrigatórias:

   ![Formulário Adicionar alerta de métrica](./media/howto-alert-on-metric/4-add-rule-form.png)

5. Dentro da seção **Condição**, selecione **Adicionar condição**.

6. Selecione uma métrica da lista de sinais sobre a qual deseja ser alertado. Neste exemplo, selecione "Porcentagem de armazenamento".
   
   ![Selecionar métrica](./media/howto-alert-on-metric/6-configure-signal-logic.png)

7. Configure a lógica de alerta, incluindo a **Condição** (por exemplo, "Maior que"), o **Limite** (por exemplo, 85%), a **Agregação de Tempo**, o **Período** durante o qual a regra de métrica deverá ser atendida antes de o alerta disparar (por exemplo, "Os últimos 30 minutos") e **Frequência**.
   
   Selecione **Concluído** ao concluir.

   ![Selecionar métrica](./media/howto-alert-on-metric/7-set-threshold-time.png)

8. Dentro da seção **Grupos de Ações**, selecione **Criar Novo** para criar um novo grupo para receber notificações sobre o alerta.

9. Preencha o formulário "Adicionar grupo de ações" com um nome, o nome curto, a assinatura e o grupo de recursos.

10. Configure o tipo de ação **Email/SMS/Push/Voz**.
    
   Escolha "Enviar email para a Função do Azure Resource Manager" para selecionar os Proprietários da assinatura, Colaboradores e Leitores para receber notificações.
   
   Opcionalmente, forneça um URI válido no campo **Webhook** se você quiser chamá-lo quando o alerta for disparado.

   Selecione **OK** ao concluir.

   ![Grupo de ações](./media/howto-alert-on-metric/10-action-group-type.png)

11. Especifique um Nome da regra de alerta, uma Descrição e uma Gravidade.

   ![Grupo de ações](./media/howto-alert-on-metric/11-name-description-severity.png) 

12. Selecione **Criar regra de alerta** para criar o alerta.

   Em alguns minutos, o alerta estará ativo e disparará conforme descrito anteriormente.

## <a name="manage-your-alerts"></a>Gerenciar seus alertas
Depois de criar um alerta, você poderá selecioná-lo e executar as seguintes ações:

* Exibir um grafo mostrando o limite de métrica e os valores reais do dia anterior relevante para este alerta.
* **Editar** ou **Excluir** a regra de alerta.
* **Desabilitar** ou **Habilitar** o alerta, se desejar interromper temporariamente ou retomar o recebimento de notificações.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre como [configurar webhooks em alertas](../azure-monitor/platform/alerts-webhooks.md).
* Tenha uma [visão geral da coleção de métricas](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para verificar se o serviço está disponível e responsivo.
