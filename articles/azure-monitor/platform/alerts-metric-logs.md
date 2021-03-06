---
title: Como criar Alertas de métrica para logs no Azure Monitor
description: Tutorial sobre como criar alertas de métrica quase em tempo real para dados populares do Log Analytics.
author: msvijayn
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 09/17/2018
ms.author: vinagara
ms.subservice: alerts
ms.openlocfilehash: ac4391b91d818b21e392e134115294fb84473e69
ms.sourcegitcommit: 9b6492fdcac18aa872ed771192a420d1d9551a33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54449633"
---
# <a name="create-metric-alerts-for-logs-in-azure-monitor"></a>Criar Alertas de métrica para Logs no Azure Monitor

## <a name="overview"></a>Visão geral

O Azure Monitor presta suporte a um [tipo de alerta de métrica](../../azure-monitor/platform/alerts-metric-near-real-time.md) que tem vantagens sobre os [alertas clássicos](../../azure-monitor/platform/alerts-classic-portal.md). As métricas estão disponíveis para uma [ampla lista de serviços do Azure](../../azure-monitor/platform/metrics-supported.md). Este artigo explica o uso de um subconjunto para o recurso - `Microsoft.OperationalInsights/workspaces`.

Você pode usar os alertas de métrica nos registros conhecidos do Log Analytics extraídos como métricas como parte das Métricas de Logs, incluindo recursos no Azure ou locais. As soluções do Log Analytics com suporte estão listadas abaixo:

- [Contadores de desempenho](../../azure-monitor/platform/data-sources-performance-counters.md) para computadores Windows e Linux
- [Registros de pulsação para Integridade do Agente](../../azure-monitor/insights/solution-agenthealth.md)
- Registros de [gerenciamento de atualizações](../../automation/automation-update-management.md)
- Logs de [dados de evento](../../azure-monitor/platform/data-sources-windows-events.md)

Há muitos benefícios de se usar os **Alertas de métrica para logs** em vez dos [Alertas de log](../../azure-monitor/platform/alerts-log.md) no Azure. Alguns deles são listados abaixo:

- Os Alertas de métrica oferecem a capacidade de monitoramento quase em tempo real e Alertas de métrica para dados de logs bifurcados do log de origem para garantir a uniformidade.
- Os Alertas de Métrica são com estado. Eles só notificam uma vez depois que o alerta é disparado e uma vez depois que o alerta é resolvido. Diferentemente dos alertas de log que são sem estado e disparam a cada intervalo se a condição de alerta é atendida.
- Os Alertas de métrica para logs fornecem várias dimensões, permitindo a filtragem com valores específicos mais simples, como Computadores, Tipo de sistema operacional e afins, sem ser necessário criar uma consulta no Analytics.

> [!NOTE]
> A métrica e/ou dimensão específica só será exibida se os respectivos dados existirem no período escolhido. Essas métricas estão disponíveis para clientes com workspaces do Log Analytics do Azure.

## <a name="metrics-and-dimensions-supported-for-logs"></a>Métricas e dimensões com suporte para logs

 Os alertas de métrica são compatíveis com a emissão de alertas para métricas que usam dimensões. É possível usar dimensões para filtrar sua métrica para o nível certo. A lista completa de métricas com suporte para Logs dos [workspaces do Log Analytics](../../azure-monitor/platform/metrics-supported.md#microsoftoperationalinsightsworkspaces) está indicada entre as soluções com suporte.

> [!NOTE]
> Para exibir as métricas com suporte para extração do workspace do Log Analytics por meio do [Azure Monitor - Métricas](../../azure-monitor/platform/metrics-charts.md), um alerta de métrica para logs deve ser criado para tal métrica. As dimensões escolhidas no Alerta de métrica para logs só aparecerá para exploração no Azure Monitor - Métricas.

## <a name="creating-metric-alert-for-log-analytics"></a>Como criar um alerta de métrica para o Log Analytics

Os dados de métricas de logs populares são canalizados no Azure Monitor - Métricas antes de serem processados no Log Analytics. Isso permite que os usuários aproveitem os recursos da Plataforma de métricas e o alerta de métricas, incluindo o fato de poderem ter alertas com frequências de até 1 minuto.
Os meios para se criar um alerta de métrica para os logs estão listados abaixo.

## <a name="prerequisites-for-metric-alert-for-logs"></a>Pré-requisitos do Alerta de métrica para logs

Para que as Métricas para logs coletadas de dados do Log Analytics funcionem, o seguinte deve ser configurado e disponibilizado:

1. **Espaço de trabalho do Log Analytics Ativo**: É necessário ter um workspace ativo e válido do Log Analytics. Para obter mais informações, confira [Criar um workspace do Log Analytics no portal do Azure](../../azure-monitor/learn/quick-create-workspace.md).
2. **Agente está configurado para o espaço de trabalho do Log Analytics**: O agente precisa estar configurado para que as VMs do Azure (e/ou) VMs locais enviem dados para o Workspace do Log Analytics usado na etapa anterior. Para saber mais, confira [Log Analytics - Visão geral do agente](../../azure-monitor/platform/agents-overview.md).
3. **As Soluções do Log Analytics com suporte estão listadas abaixo**: A solução do Log Analytics deve estar configurada e enviando dados para o workspace do Log Analytics. As soluções com suporte são [Contadores de desempenho para Windows e Linux](../../azure-monitor/platform/data-sources-performance-counters.md), [Registros de pulsação para a Integridade do Agente](../../azure-monitor/insights/solution-agenthealth.md), [Gerenciamento de atualizações e [Dados de evento](../../azure-monitor/platform/data-sources-windows-events.md).
4. **Soluções do Log Analytics configuradas para enviar logs**: A solução Log Analytics deve ter os logs / dados correspondentes a [métricas compatíveis com espaços de trabalho do Log Analytics](../../azure-monitor/platform/metrics-supported.md#microsoftoperationalinsightsworkspaces) ativados. Por exemplo, para *% de memória disponível*, o contador deve ser configurado na solução [Contadores de desempenho](../../azure-monitor/platform/data-sources-performance-counters.md) primeiro.

## <a name="configuring-metric-alert-for-logs"></a>Como configurar o Alerta de métrica para logs

 Os alertas de métrica podem ser criados e gerenciados usando o portal do Azure, os modelos do Resource Manager, a API REST, o PowerShell e a CLI do Azure. Uma vez que o recurso de Alertas de Métrica para Logs é uma variante dos alertas de métrica, depois que os pré-requisitos estiverem concluídos, o alerta de métrica para logs poderá ser criado para o workspace especificado do Log Analytics. Todas as características e funcionalidades dos [ alertas de métrica](../../azure-monitor/platform/alerts-metric-near-real-time.md) serão aplicáveis também aos alertas de métrica para logs, incluindo esquema de conteúdo, limites de cota aplicáveis e preço cobrado.

Para obter detalhes passo a passo e exemplos, confira [como criar e gerenciar alertas de métrica](https://aka.ms/createmetricalert). Especificamente para Alertas de métrica para logs, siga as instruções para gerenciar alertas de métrica e verifique o seguinte:

- O destino do alerta de métrica é um *workspace do Log Analytics* válido
- O sinal escolhido para o alerta de métrica do *workspace do Log Analytics* escolhido é do tipo **Métrica**
- Use filtros para condições ou recursos específicos usando filtros de dimensão. As métricas para logs são multidimensionais
- Ao configurar a *Lógica de sinal*, um único alerta pode ser criado para abranger vários valores de dimensão (como Computador)
- Se **não** estiver usando o portal do Azure para criar alertas de métrica para o *workspace do Log Analytics* escolhido, o usuário deverá primeiro criar uma regra explícita manualmente para converter dados de log em uma métrica usando o [Azure Monitor – Regras de consulta agendada](https://docs.microsoft.com/rest/api/monitor/scheduledqueryrules).

> [!NOTE]
> Durante a criação de alertas de métrica para o workspace do Log Analytics no portal do Azure, a regra correspondente para a conversão de dados de log em métrica usando [Azure Monitor – Regras de consulta agendada](https://docs.microsoft.com/rest/api/monitor/scheduledqueryrules) é criada automaticamente em segundo plano,  *sem a necessidade de qualquer intervenção ou ação do usuário*. Para o alerta de métricas na criação de logs usando outros meios além do portal do Azure, confira a seção [Modelo de recurso para Alertas de métrica para logs](#resource-template-for-metric-alerts-for-logs) para ver formas de se criar um log baseado em ScheduledQueryRule para a regra de conversão de métrica antes da criação do alerta de métrica. Caso contrário, não haverá dados para alertas de métrica nos logs criados.

## <a name="resource-template-for-metric-alerts-for-logs"></a>Modelo de recurso para os Alertas de métrica para logs

Conforme mencionado anteriormente, o processo de criação de alertas de métrica de logs tem duas partes:

1. Criar uma regra para a extração de métricas dos logs com suporte usando a API scheduledQueryRule
2. Criar um alerta de métrica para métricas extraídas do log (na etapa 1) e o workspace do Log Analytics como um recurso de destino

### <a name="metric-alerts-for-logs-with-static-threshold"></a>Alertas de métrica para Logs com limite estático

Para obter o mesmo resultado, é possível usar o exemplo de modelo do Azure Resource Manager abaixo, em que a criação de um alerta de métrica de limite estático depende do êxito na criação da regra para extrair as métricas de logs por meio de scheduledQueryRule.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "convertRuleName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the rule to convert log to metric"
            }
        },
        "convertRuleDescription": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Description for log converted to metric"
            }
        },
        "convertRuleRegion": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the region used by workspace"
            }
        },
        "convertRuleStatus": {
            "type": "string",
            "defaultValue": "true",
            "metadata": {
                "description": "Specifies whether the log conversion rule is enabled"
            }
        },
        "convertRuleMetric": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the metric once extraction done from logs."
            }
        },
        "alertName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "This is a metric alert",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "alertSeverity": {
            "type": "int",
            "defaultValue": 3,
            "allowedValues": [
                0,
                1,
                2,
                3,
                4
            ],
            "metadata": {
                "description": "Severity of alert {0,1,2,3,4}"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether the alert is enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Full Resource ID of the resource emitting the metric that will be used for the comparison. For example /subscriptions/00000000-0000-0000-0000-0000-00000000/resourceGroups/ResourceGroupName/providers/Microsoft.compute/virtualMachines/VM_xyz"
            }
        },
        "metricName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the metric used in the comparison to activate the alert."
            }
        },
        "operator": {
            "type": "string",
            "defaultValue": "GreaterThan",
            "allowedValues": [
                "Equals",
                "NotEquals",
                "GreaterThan",
                "GreaterThanOrEqual",
                "LessThan",
                "LessThanOrEqual"
            ],
            "metadata": {
                "description": "Operator comparing the current value with the threshold value."
            }
        },
        "threshold": {
            "type": "string",
            "defaultValue": "0",
            "metadata": {
                "description": "The threshold value at which the alert is activated."
            }
        },
        "timeAggregation": {
            "type": "string",
            "defaultValue": "Average",
            "allowedValues": [
                "Average",
                "Minimum",
                "Maximum",
                "Total"
            ],
            "metadata": {
                "description": "How the data that is collected should be combined over time."
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used to monitor alert activity based on the threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "evaluationFrequency": {
            "type": "string",
            "defaultValue": "PT1M",
            "metadata": {
                "description": "how often the metric alert is evaluated represented in ISO 8601 duration format"
            }
        },
        "actionGroupId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "The ID of the action group that is triggered when the alert is activated or deactivated"
            }
        }
    },
    "variables": {
        "convertRuleTag": "hidden-link:/subscriptions/1234-56789-1234-567a/resourceGroups/resourceGroupName/providers/Microsoft.OperationalInsights/workspaces/workspaceName",
        "convertRuleSourceWorkspace": {
            "SourceId": "/subscriptions/1234-56789-1234-567a/resourceGroups/resourceGroupName/providers/Microsoft.OperationalInsights/workspaces/workspaceName"
        }
    },
    "resources": [
        {
            "name": "[parameters('convertRuleName')]",
            "type": "Microsoft.Insights/scheduledQueryRules",
            "apiVersion": "2018-04-16",
            "location": "[parameters('convertRuleRegion')]",
            "tags": {
                "[variables('convertRuleTag')]": "Resource"
            },
            "properties": {
                "description": "[parameters('convertRuleDescription')]",
                "enabled": "[parameters('convertRuleStatus')]",
                "source": {
                    "dataSourceId": "[variables('convertRuleSourceWorkspace').SourceId]"
                },
                "action": {
                    "odata.type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.Microsoft.AppInsights.Nexus.DataContracts.Resources.ScheduledQueryRules.LogToMetricAction",
                    "criteria": [{
                            "metricName": "[parameters('convertRuleMetric')]",
                            "dimensions": []
                        }
                    ]
                }
            }
        },
        {
            "name": "[parameters('alertName')]",
            "type": "Microsoft.Insights/metricAlerts",
            "location": "global",
            "apiVersion": "2018-03-01",
            "tags": {},
            "dependsOn":["[resourceId('Microsoft.Insights/scheduledQueryRules',parameters('convertRuleName'))]"],
            "properties": {
                "description": "[parameters('alertDescription')]",
                "severity": "[parameters('alertSeverity')]",
                "enabled": "[parameters('isEnabled')]",
                "scopes": ["[parameters('resourceId')]"],
                "evaluationFrequency":"[parameters('evaluationFrequency')]",
                "windowSize": "[parameters('windowSize')]",
                "criteria": {
                    "odata.type": "Microsoft.Azure.Monitor.SingleResourceMultipleMetricCriteria",
                    "allOf": [
                        {
                            "name" : "1st criterion",
                            "metricName": "[parameters('metricName')]",
                            "dimensions":[],
                            "operator": "[parameters('operator')]",
                            "threshold" : "[parameters('threshold')]",
                            "timeAggregation": "[parameters('timeAggregation')]"
                        }
                    ]
                },
                "actions": [
                    {
                        "actionGroupId": "[parameters('actionGroupId')]"
                    }
                ]
            }
        }
    ]
}
```

Digamos que o JSON acima seja salvo como metricfromLogsAlertStatic.json, então ele poderá ser combinado com um arquivo JSON de parâmetro para criação com base no modelo de recursos. Um arquivo JSON de parâmetro de exemplo é listado abaixo:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "convertRuleName": {
            "value": "TestLogtoMetricRule" 
        },
        "convertRuleDescription": {
            "value": "Test rule to extract metrics from logs via template"
        },
        "convertRuleRegion": {
            "value": "West Central US"
        },
        "convertRuleStatus": {
            "value": "true"
        },
        "convertRuleMetric": {
            "value": "Average_% Idle Time"
        },
        "alertName": {
            "value": "TestMetricAlertonLog"
        },
        "alertDescription": {
            "value": "New multi-dimensional metric alert created via template"
        },
        "alertSeverity": {
            "value":3
        },
        "isEnabled": {
            "value": true
        },
        "resourceId": {
            "value": "/subscriptions/1234-56789-1234-567a/resourceGroups/myRG/providers/Microsoft.OperationalInsights/workspaces/workspaceName"
        },
        "metricName":{
            "value": "Average_% Idle Time"
        },
        "operator": {
            "value": "GreaterThan"
        },
        "threshold":{
            "value": "1"
        },
        "timeAggregation":{
            "value": "Average"
        },
        "actionGroupId": {
            "value": "/subscriptions/1234-56789-1234-567a/resourceGroups/myRG/providers/microsoft.insights/actionGroups/actionGroupName"
        }
    }
}
```

Supondo que o arquivo de parâmetro acima seja salvo como metricfromLogsAlertStatic.parameters.json, será possível criar o alerta de métrica para logs de usando o [modelo de recursos para criação no portal do Azure](../../azure-resource-manager/resource-group-template-deploy-portal.md).

Como alternativa, também é possível usar o comando do Azure Powershell abaixo:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myRG" -TemplateFile metricfromLogsAlertStatic.json TemplateParameterFile metricfromLogsAlertStatic.parameters.json
```

Ou use Implantar o modelo de recurso usando a CLI do Azure:

```CLI
az group deployment create --resource-group myRG --template-file metricfromLogsAlertStatic.json --parameters @metricfromLogsAlertStatic.parameters.json
```

### <a name="metric-alerts-for-logs-with-dynamic-thresholds"></a>Alertas de métrica para Logs com Limites Dinâmicos

Para obter o mesmo resultado, é possível usar o exemplo de modelo do Azure Resource Manager abaixo, em que a criação de um alerta de métrica de Limites Dinâmicos depende do êxito na criação da regra para extrair as métricas de logs por meio de scheduledQueryRule.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "convertRuleName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the rule to convert log to metric"
            }
        },
        "convertRuleDescription": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Description for log converted to metric"
            }
        },
        "convertRuleRegion": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the region used by workspace"
            }
        },
        "convertRuleStatus": {
            "type": "string",
            "defaultValue": "true",
            "metadata": {
                "description": "Specifies whether the log conversion rule is enabled"
            }
        },
        "convertRuleMetric": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the metric once extraction done from logs."
            }
        },
        "alertName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "This is a metric alert",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "alertSeverity": {
            "type": "int",
            "defaultValue": 3,
            "allowedValues": [
                0,
                1,
                2,
                3,
                4
            ],
            "metadata": {
                "description": "Severity of alert {0,1,2,3,4}"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether the alert is enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Full Resource ID of the resource emitting the metric that will be used for the comparison. For example /subscriptions/00000000-0000-0000-0000-0000-00000000/resourceGroups/ResourceGroupName/providers/Microsoft.compute/virtualMachines/VM_xyz"
            }
        },
        "metricName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the metric used in the comparison to activate the alert."
            }
        },
        "operator": {
            "type": "string",
            "defaultValue": "GreaterOrLessThan",
            "allowedValues": [
                "GreaterThan",
                "LessThan",
                "GreaterOrLessThan"
            ],
            "metadata": {
                "description": "Operator comparing the current value with the threshold value."
            }
        },
        "alertSensitivity": {
            "type": "string",
            "defaultValue": "Medium",
            "allowedValues": [
                "High",
                "Medium",
                "Low"
            ],
            "metadata": {
                "description": "Tunes how 'noisy' the Dynamic Thresholds alerts will be: 'High' will result in more alerts while 'Low' will result in fewer alerts."
            }
        },
        "numberOfEvaluationPeriods": {
            "type": "string",
            "defaultValue": "4",
            "metadata": {
                "description": "The number of periods to check in the alert evaluation."
            }
        },
        "minFailingPeriodsToAlert": {
            "type": "string",
            "defaultValue": "3",
            "metadata": {
                "description": "The number of unhealthy periods to alert on (must be lower or equal to numberOfEvaluationPeriods)."
            }
        },
        "timeAggregation": {
            "type": "string",
            "defaultValue": "Average",
            "allowedValues": [
                "Average",
                "Minimum",
                "Maximum",
                "Total"
            ],
            "metadata": {
                "description": "How the data that is collected should be combined over time."
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used to monitor alert activity based on the threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "evaluationFrequency": {
            "type": "string",
            "defaultValue": "PT1M",
            "metadata": {
                "description": "how often the metric alert is evaluated represented in ISO 8601 duration format"
            }
        },
        "actionGroupId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "The ID of the action group that is triggered when the alert is activated or deactivated"
            }
        }
    },
    "variables": {
        "convertRuleTag": "hidden-link:/subscriptions/1234-56789-1234-567a/resourceGroups/resourceGroupName/providers/Microsoft.OperationalInsights/workspaces/workspaceName",
        "convertRuleSourceWorkspace": {
            "SourceId": "/subscriptions/1234-56789-1234-567a/resourceGroups/resourceGroupName/providers/Microsoft.OperationalInsights/workspaces/workspaceName"
        }
    },
    "resources": [
        {
            "name": "[parameters('convertRuleName')]",
            "type": "Microsoft.Insights/scheduledQueryRules",
            "apiVersion": "2018-04-16",
            "location": "[parameters('convertRuleRegion')]",
            "tags": {
                "[variables('convertRuleTag')]": "Resource"
            },
            "properties": {
                "description": "[parameters('convertRuleDescription')]",
                "enabled": "[parameters('convertRuleStatus')]",
                "source": {
                    "dataSourceId": "[variables('convertRuleSourceWorkspace').SourceId]"
                },
                "action": {
                    "odata.type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.Microsoft.AppInsights.Nexus.DataContracts.Resources.ScheduledQueryRules.LogToMetricAction",
                    "criteria": [{
                            "metricName": "[parameters('convertRuleMetric')]",
                            "dimensions": []
                        }
                    ]
                }
            }
        },
        {
            "name": "[parameters('alertName')]",
            "type": "Microsoft.Insights/metricAlerts",
            "location": "global",
            "apiVersion": "2018-03-01",
            "tags": {},
            "dependsOn":["[resourceId('Microsoft.Insights/scheduledQueryRules',parameters('convertRuleName'))]"],
            "properties": {
                "description": "[parameters('alertDescription')]",
                "severity": "[parameters('alertSeverity')]",
                "enabled": "[parameters('isEnabled')]",
                "scopes": ["[parameters('resourceId')]"],
                "evaluationFrequency":"[parameters('evaluationFrequency')]",
                "windowSize": "[parameters('windowSize')]",
                "criteria": {
                    "odata.type": "Microsoft.Azure.Monitor.MultipleResourceMultipleMetricCriteria",
                    "allOf": [
                        {
                            "criterionType": "DynamicThresholdCriterion",
                            "name" : "1st criterion",
                            "metricName": "[parameters('metricName')]",
                            "dimensions":[],
                            "operator": "[parameters('operator')]",
                            "alertSensitivity": "[parameters('alertSensitivity')]",
                            "failingPeriods": {
                                "numberOfEvaluationPeriods": "[parameters('numberOfEvaluationPeriods')]",
                                "minFailingPeriodsToAlert": "[parameters('minFailingPeriodsToAlert')]"
                            },
                            "timeAggregation": "[parameters('timeAggregation')]"
                        }
                    ]
                },
                "actions": [
                    {
                        "actionGroupId": "[parameters('actionGroupId')]"
                    }
                ]
            }
        }
    ]
}
```

Digamos que o JSON acima seja salvo como metricfromLogsAlertDynamic.json, então ele poderá ser combinado com um arquivo JSON de parâmetro para criação com base no modelo de recursos. Um arquivo JSON de parâmetro de exemplo é listado abaixo:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "convertRuleName": {
            "value": "TestLogtoMetricRule"
        },
        "convertRuleDescription": {
            "value": "Test rule to extract metrics from logs via template"
        },
        "convertRuleRegion": {
            "value": "West Central US"
        },
        "convertRuleStatus": {
            "value": "true"
        },
        "convertRuleMetric": {
            "value": "Average_% Idle Time"
        },
        "alertName": {
            "value": "TestMetricAlertonLog"
        },
        "alertDescription": {
            "value": "New multi-dimensional metric alert created via template"
        },
        "alertSeverity": {
            "value":3
        },
        "isEnabled": {
            "value": true
        },
        "resourceId": {
            "value": "/subscriptions/1234-56789-1234-567a/resourceGroups/myRG/providers/Microsoft.OperationalInsights/workspaces/workspaceName"
        },
        "metricName":{
            "value": "Average_% Idle Time"
        },
        "operator": {
            "value": "GreaterOrLessThan"
          },
          "alertSensitivity": {
              "value": "Medium"
          },
          "numberOfEvaluationPeriods": {
              "value": "4"
          },
          "minFailingPeriodsToAlert": {
              "value": "3"
          },
        "timeAggregation":{
            "value": "Average"
        },
        "actionGroupId": {
            "value": "/subscriptions/1234-56789-1234-567a/resourceGroups/myRG/providers/microsoft.insights/actionGroups/actionGroupName"
        }
    }
}
```

Supondo que o arquivo de parâmetro acima seja salvo como metricfromLogsAlertDynamic.parameters.json, será possível criar o alerta de métrica para logs de usando o [modelo de recursos para criação no portal do Azure](../../azure-resource-manager/resource-group-template-deploy-portal.md).

Como alternativa, também é possível usar o comando do Azure Powershell abaixo:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myRG" -TemplateFile metricfromLogsAlertDynamic.json TemplateParameterFile metricfromLogsAlertDynamic.parameters.json
```

Ou use Implantar o modelo de recurso usando a CLI do Azure:

```CLI
az group deployment create --resource-group myRG --template-file metricfromLogsAlertDynamic.json --parameters @metricfromLogsAlertDynamic.parameters.json
```

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [alertas de métrica](alerts-metric.md).
- Saiba mais sobre os [alertas de log no Azure](../../azure-monitor/platform/alerts-unified-log.md).
- Saiba mais sobre os [Alertas no Azure](alerts-overview.md).
