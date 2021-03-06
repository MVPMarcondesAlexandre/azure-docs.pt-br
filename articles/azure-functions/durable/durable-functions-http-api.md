---
title: APIs HTTP nas Funções Duráveis – Azure
description: Saiba como implementar APIs HTTP na extensão de Funções Duráveis do Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 12/07/2018
ms.author: azfuncdf
ms.openlocfilehash: c2ffa623ad7a6c6da5b799d2c7d5f35c9f65e503
ms.sourcegitcommit: e7312c5653693041f3cbfda5d784f034a7a1a8f1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54215398"
---
# <a name="http-apis-in-durable-functions-azure-functions"></a>APIs HTTP nas Funções Duráveis (Azure Functions)

A extensão de Tarefa Durável expõe um conjunto de APIs HTTP que podem ser usadas para executar as seguintes tarefas:

* Buscar o status de uma instância de orquestração.
* Enviar um evento a uma instância de orquestração em espera.
* Encerrar uma instância de orquestração em execução.

Cada uma dessas APIs HTTP é uma operação de webhook manipulada diretamente pela extensão de Tarefa Durável. Eles não são específicas a nenhuma função do aplicativo de funções.

> [!NOTE]
> Essas operações também podem ser invocadas diretamente usando as APIs de gerenciamento de instância na classe [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html). Para obter mais informações, consulte [Gerenciamento de Instâncias](durable-functions-instance-management.md).

## <a name="http-api-url-discovery"></a>Descoberta de URL na API HTTP

A classe [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) expõe uma API [CreateCheckStatusResponse](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateCheckStatusResponse_) que pode ser usada para gerar uma carga de resposta HTTP que contém links para todas as operações com suporte. Veja um exemplo de função de gatilho HTTP que demonstra como usar essa API:

### <a name="c"></a>C#

[!code-csharp[Main](~/samples-durable-functions/samples/csx/HttpStart/run.csx)]

### <a name="javascript-functions-2x-only"></a>JavaScript (apenas Funções 2.x)

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/HttpStart/index.js)]

Estas funções de exemplo produzem os seguintes dados de resposta JSON. O tipo de dados de todos os campos é `string`.

| Campo             |DESCRIÇÃO                           |
|-------------------|--------------------------------------|
| ID                |A ID da instância de orquestração. |
| statusQueryGetUri |A URL de status da instância de orquestração. |
| sendEventPostUri  |A URL "acionar evento" da instância de orquestração. |
| terminatePostUri  |A URL "encerrar" da instância de orquestração. |
| rewindPostUri     |A URL para “retroceder” do status da instância de orquestração. |

Aqui está um exemplo de resposta:

```http
HTTP/1.1 202 Accepted
Content-Length: 923
Content-Type: application/json; charset=utf-8
Location: https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2?taskHub=DurableFunctionsHub&connection=Storage&code=XXX

{
    "id":"34ce9a28a6834d8492ce6a295f1a80e2",
    "statusQueryGetUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2?taskHub=DurableFunctionsHub&connection=Storage&code=XXX",
    "sendEventPostUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection=Storage&code=XXX",
    "terminatePostUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2/terminate?reason={text}&taskHub=DurableFunctionsHub&connection=Storage&code=XXX",
    "rewindPostUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2/rewind?reason={text}&taskHub=DurableFunctionsHub&connection=Storage&code=XXX"
}
```

> [!NOTE]
> O formato das URLs de webhook pode variar dependendo de qual versão do host do Azure Functions você está executando. O exemplo acima refere-se ao host do Azure Functions 2.x.

## <a name="async-operation-tracking"></a>Acompanhamento de operação assíncrona

A resposta HTTP mencionada anteriormente foi criada para ajudar a implementar APIs assíncronas HTTP de execução longa com as Durable Functions. Às vezes, isso é chamado de *Padrão de consumidor de sondagem*. O fluxo de cliente/servidor funciona da seguinte maneira:

1. O cliente emite uma solicitação HTTP para iniciar um processo de execução longa, como uma função de orquestrador.
2. O gatilho HTTP de destino retorna uma resposta de HTTP 202 com um cabeçalho `Location` com o valor `statusQueryGetUri`.
3. O cliente sonda a URL no cabeçalho `Location`. Ela continua vendo respostas de HTTP 202 com um cabeçalho `Location`.
4. Quando a instância é concluída (ou falha), o ponto de extremidade no cabeçalho `Location` retorna HTTP 200.

Este protocolo permite coordenar processos de execução longa com clientes ou serviços externos que dão suporte a sondar um ponto de extremidade HTTP e a seguir o cabeçalho `Location`. As partes fundamentais já fazem parte das APIs HTTP das Funções Duráveis.

> [!NOTE]
> Todas as ações baseadas em HTTP fornecidas pelos [Aplicativos Lógicos do Azure](https://azure.microsoft.com/services/logic-apps/) dão suporte ao padrão de operação assíncrona padrão. Essa capacidade possibilita inserir uma função durável de execução longa como parte de um fluxo de trabalho dos Aplicativos Lógicos. Mais detalhes sobre o suporte dos Aplicativos Lógicos a padrões de HTTP assíncronos podem ser encontrados na [Documentação de ações e gatilhos de fluxo de trabalho dos Aplicativos Lógicos do Azure](../../logic-apps/logic-apps-workflow-actions-triggers.md#asynchronous-patterns).

## <a name="http-api-reference"></a>Referência de API HTTP

Todas as APIs HTTP implementadas pela extensão têm os seguintes parâmetros. O tipo de dados de todos os parâmetros é `string`.

| Parâmetro  | Tipo de Parâmetro  | DESCRIÇÃO |
|------------|-----------------|-------------|
| instanceId | URL             | A ID da instância de orquestração. |
| taskHub    | Cadeia de consulta    | O nome do [hub de tarefas](durable-functions-task-hubs.md). Se não for especificado, o nome do hub de tarefas do aplicativo de funções será presumido. |
| connection | Cadeia de consulta    | O **nome** da cadeia de conexão para a conta de armazenamento. Se não for especificada, a cadeia de conexão padrão do aplicativo de funções será presumida. |
| systemKey  | Cadeia de consulta    | A chave de autorização necessária para invocar a API. |
| showInput  | Cadeia de consulta    | Parâmetro opcional; somente solicitação de instância única. Se definido para `false`, a entrada de execução não será incluída no conteúdo de resposta.|
| showHistory| Cadeia de consulta    | Parâmetro opcional; somente solicitação de instância única. Se definido como `true`, o histórico de execução da orquestração será incluído na carga da resposta.|
| showHistoryOutput| Cadeia de consulta    | Parâmetro opcional; somente solicitação de instância única. Se definido como `true`, as saídas da atividade serão incluídas no histórico de execução da orquestração.|
| createdTimeFrom  | Cadeia de consulta    | Parâmetro opcional. Quando especificado, filtra a lista de instâncias retornadas que foram criadas no ou após o registro de data e hora ISO8601 especificado.|
| createdTimeTo    | Cadeia de consulta    | Parâmetro opcional. Quando especificado, filtra a lista de instâncias retornadas que foram criadas em ou antes do timestamp ISO8601 especificado.|
| runtimeStatus    | Cadeia de consulta    | Parâmetro opcional. Quando especificado, filtra a lista de instâncias retornadas com base em seu status de tempo de execução. Para ver a lista de possíveis valores de status de tempo de execução, consulte o tópico [Consultando Instâncias](durable-functions-instance-management.md). |
| top    | Cadeia de consulta    | Parâmetro opcional. Quando especificado, divida os resultados da consulta em páginas e limite o número máximo de resultados por página. |

`systemKey` é uma chave de autorização gerada automaticamente pelo host do Azure Functions. Ela concede acesso especificamente às APIs da extensão de Tarefas Duráveis e pode ser gerenciada da mesma maneira que as [outras chaves de autorização](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Key-management-API). A maneira mais simples de descobrir o valor de `systemKey` é usar a API `CreateCheckStatusResponse` mencionada anteriormente.

As próximas seções tratam das APIs HTTP específicas com suporte da extensão e fornecem exemplos de como elas podem ser usadas.

### <a name="get-instance-status"></a>Obter status da instância

Obtém o status de uma instância de orquestração especificada.

#### <a name="request"></a>Solicitação

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
GET /admin/extensions/DurableTaskExtension/instances/{instanceId}?taskHub={taskHub}&connection={connection}&code={systemKey}
```

O formato do Functions 2.0 tem os mesmos parâmetros, mas tem um prefixo de URL ligeiramente diferente:

```http
GET /runtime/webhooks/durabletask/instances/{instanceId}?taskHub={taskHub}&connection={connection}&code={systemKey}&showHistory={showHistory}&showHistoryOutput={showHistoryOutput}
```

#### <a name="response"></a>Response

Vários valores de código de status possíveis podem ser retornados.

* **HTTP 200 (OK)**: A instância especificada está em um estado concluído.
* **HTTP 202 (Aceito)**: A instância especificada está em andamento.
* **HTTP 400 (Solicitação Incorreta)**: A instância especificada falhou ou foi encerrada.
* **HTTP 404 (Não Encontrado)**: A instância especificada não existe ou não começou a ser executada.
* **HTTP 500 (Erro Interno do Servidor)**: A instância especificada falhou com uma exceção sem tratamento.

A carga de resposta para os casos de **HTTP 200** e **HTTP 202** é um objeto JSON com os campos a seguir:

| Campo           | Tipo de dados | DESCRIÇÃO |
|-----------------|-----------|-------------|
| runtimeStatus   | string    | O status de tempo de execução da instância. Os valores incluem *Em execução*, *Pendente*, *Falha*, *Cancelado*, *Encerrado*, *Concluído*. |
| input           | JSON      | Os dados JSON usados para inicializar a instância. Este campo é `null` se o `showInput` parâmetro da cadeia de caracteres de consulta for definido para `false`.|
| customStatus    | JSON      | Os dados JSON usados para status de orquestração personalizado. Este campo é `null` se não for definido. |
| output          | JSON      | A saída JSON da instância. Este campo será `null` se a instância não estiver no estado concluído. |
| createdTime     | string    | A hora em que a instância foi criada. Usa a notação estendida ISO 8601. |
| lastUpdatedTime | string    | A hora em que a instância foi persistida pela última vez. Usa a notação estendida ISO 8601. |
| historyEvents   | JSON      | Uma matriz JSON contendo o histórico de execução da orquestração. Esse campo é `null`, exceto se o parâmetro da cadeia de caracteres de consulta `showHistory` estiver definido como `true`. |

Aqui está um exemplo de carga de resposta, incluindo o histórico de execução de orquestração e saídas de atividades (formatado para legibilidade):

```json
{
  "createdTime": "2018-02-28T05:18:49Z",
  "historyEvents": [
      {
          "EventType": "ExecutionStarted",
          "FunctionName": "E1_HelloSequence",
          "Timestamp": "2018-02-28T05:18:49.3452372Z"
      },
      {
          "EventType": "TaskCompleted",
          "FunctionName": "E1_SayHello",
          "Result": "Hello Tokyo!",
          "ScheduledTime": "2018-02-28T05:18:51.3939873Z",
          "Timestamp": "2018-02-28T05:18:52.2895622Z"
      },
      {
          "EventType": "TaskCompleted",
          "FunctionName": "E1_SayHello",
          "Result": "Hello Seattle!",
          "ScheduledTime": "2018-02-28T05:18:52.8755705Z",
          "Timestamp": "2018-02-28T05:18:53.1765771Z"
      },
      {
          "EventType": "TaskCompleted",
          "FunctionName": "E1_SayHello",
          "Result": "Hello London!",
          "ScheduledTime": "2018-02-28T05:18:53.5170791Z",
          "Timestamp": "2018-02-28T05:18:53.891081Z"
      },
      {
          "EventType": "ExecutionCompleted",
          "OrchestrationStatus": "Completed",
          "Result": [
              "Hello Tokyo!",
              "Hello Seattle!",
              "Hello London!"
          ],
          "Timestamp": "2018-02-28T05:18:54.3660895Z"
      }
  ],
  "input": null,
  "customStatus": { "nextActions": ["A", "B", "C"], "foo": 2 },
  "lastUpdatedTime": "2018-02-28T05:18:54Z",
  "output": [
      "Hello Tokyo!",
      "Hello Seattle!",
      "Hello London!"
  ],
  "runtimeStatus": "Completed"
}
```

A resposta **HTTP 202** também inclui um cabeçalho de resposta **Local** que faz referência à mesma URL que o campo `statusQueryGetUri` mencionado anteriormente.

### <a name="get-all-instances-status"></a>Obter status de todas as instâncias

Também é possível consultar o status de todas as instâncias. Remova `instanceId` da solicitação 'Obter status da instância'. Os parâmetros são os mesmos que os do status 'Obter status da instância.'

Uma coisa a lembrar é que `connection` e `code` são opcionais. Se você tiver uma autenticação anônima na função, o código não será necessário.
Se você não quiser usar uma cadeia de conexão de armazenamento de blob diferente da definida na configuração do aplicativo AzureWebJobsStorage, poderá ignorar com segurança o parâmetro da cadeia de consulta de conexão.

#### <a name="request"></a>Solicitação

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
GET /admin/extensions/DurableTaskExtension/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}
```

O formato do Functions 2.0 tem todos os mesmos parâmetros, mas um prefixo de URL ligeiramente diferente:

```http
GET /runtime/webhooks/durabletask/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}
```

#### <a name="request-with-filters"></a>Solicitação com filtros

Você pode filtrar a solicitação.

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
GET /admin/extensions/DurableTaskExtension/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}&createdTimeFrom={createdTimeFrom}&createdTimeTo={createdTimeTo}&runtimeStatus={runtimeStatus,runtimeStatus,...}&showInput={showInput}&showHistory={showHistory}&showHistoryOutput={showHistoryOutput}
```

O formato do Functions 2.0 tem todos os mesmos parâmetros, mas um prefixo de URL ligeiramente diferente:

```http
GET /runtime/webhooks/durableTask/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}&createdTimeFrom={createdTimeFrom}&createdTimeTo={createdTimeTo}&runtimeStatus={runtimeStatus,runtimeStatus,...}&showInput={showInput}&showHistory={showHistory}&showHistoryOutput={showHistoryOutput}
```

#### <a name="response"></a>Response

Aqui está um exemplo de cargas de resposta, incluindo o status de orquestração (formatado para legibilidade):

```json
[
    {
        "instanceId": "7af46ff000564c65aafbfe99d07c32a5",
        "runtimeStatus": "Completed",
        "input": null,
        "customStatus": null,
        "output": [
            "Hello Tokyo!",
            "Hello Seattle!",
            "Hello London!"
        ],
        "createdTime": "2018-06-04T10:46:39Z",
        "lastUpdatedTime": "2018-06-04T10:46:47Z"
    },
    {
        "instanceId": "80eb7dd5c22f4eeba9f42b062794321e",
        "runtimeStatus": "Running",
        "input": null,
        "customStatus": null,
        "output": null,
        "createdTime": "2018-06-04T15:18:28Z",
        "lastUpdatedTime": "2018-06-04T15:18:38Z"
    },
    {
        "instanceId": "9124518926db408ab8dfe84822aba2b1",
        "runtimeStatus": "Completed",
        "input": null,
        "customStatus": null,
        "output": [
            "Hello Tokyo!",
            "Hello Seattle!",
            "Hello London!"
        ],
        "createdTime": "2018-06-04T10:46:54Z",
        "lastUpdatedTime": "2018-06-04T10:47:03Z"
    },
    {
        "instanceId": "d100b90b903c4009ba1a90868331b11b",
        "runtimeStatus": "Pending",
        "input": null,
        "customStatus": null,
        "output": null,
        "createdTime": "2018-06-04T15:18:39Z",
        "lastUpdatedTime": "2018-06-04T15:18:39Z"
    }
]
```

> [!NOTE]
> Essa operação pode ser muito cara em termos de E/S de Armazenamento do Microsoft Azure, se houver muitas linhas na tabela Instâncias. Mais detalhes sobre a tabela de Instâncias podem ser encontrados na documentação [Desempenho e escala nas Funções Duráveis (Azure Functions)](durable-functions-perf-and-scale.md#instances-table).
>

#### <a name="request-with-paging"></a>Solicitação com paginação

Você pode definir o `top` parâmetro para dividir os resultados da consulta em páginas.

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
GET /admin/extensions/DurableTaskExtension/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}&top={top}
```

O formato do Functions 2.0 tem todos os mesmos parâmetros, mas um prefixo de URL ligeiramente diferente:

```http
GET /runtime/webhooks/durableTask/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}&top={top}
```

Se existir a próxima página, um token de continuação será retornado no cabeçalho de resposta.  O nome do cabeçalho `x-ms-continuation-token`.

Se você definir o valor do token de continuação no próximo cabeçalho da solicitação, você pode obter a próxima página.  Essa chave no cabeçalho de solicitação é `x-ms-continuation-token`.

### <a name="raise-event"></a>Acionar evento

Envia uma mensagem de notificação de evento para uma instância de orquestração em execução.

#### <a name="request"></a>Solicitação

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection={connection}&code={systemKey}
```

O formato do Functions 2.0 tem os mesmos parâmetros, mas tem um prefixo de URL ligeiramente diferente:

```http
POST /runtime/webhooks/durabletask/instances/{instanceId}/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection={connection}&code={systemKey}
```

Parâmetros de solicitação para essa API incluem o conjunto padrão mencionado anteriormente, bem como o parâmetro exclusivo a seguir:

| Campo       | Tipo de parâmetro  | Tipo de dados | DESCRIÇÃO |
|-------------|-----------------|-----------|-------------|
| eventName   | URL             | string    | O nome do evento que a instância de orquestração de destino está esperando. |
| {content}   | Conteúdo da solicitação | JSON      | A carga do evento em formato JSON. |

#### <a name="response"></a>Response

Vários valores de código de status possíveis podem ser retornados.

* **HTTP 202 (Aceito)**: O evento gerado foi aceito para processamento.
* **HTTP 400 (Solicitação Incorreta)**: O conteúdo da solicitação não era do tipo `application/json` ou não era um JSON válido.
* **HTTP 404 (Não Encontrado)**: A instância especificada não foi encontrada.
* **HTTP 410 (Não existe mais)**: A instância especificada foi concluída ou falhou e não pode processar os eventos gerados.

Veja um exemplo de solicitação que envia a cadeia de caracteres JSON `"incr"` para uma instância que aguarda um evento nomeado **operation**:

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/raiseEvent/operation?taskHub=DurableFunctionsHub&connection=Storage&code=XXX
Content-Type: application/json
Content-Length: 6

"incr"
```

As respostas para esta API não têm nenhum conteúdo.

### <a name="terminate-instance"></a>Encerrar instância

Encerra uma instância de orquestração em execução.

#### <a name="request"></a>Solicitação

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/terminate?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

O formato do Functions 2.0 tem os mesmos parâmetros, mas tem um prefixo de URL ligeiramente diferente:

```http
POST /runtime/webhooks/durabletask/instances/{instanceId}/terminate?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

Parâmetros de solicitação para essa API incluem o conjunto padrão mencionado anteriormente, bem como o seguinte parâmetro exclusivo.

| Campo       | Tipo de Parâmetro  | Tipo de Dados | DESCRIÇÃO |
|-------------|-----------------|-----------|-------------|
| reason      | Cadeia de consulta    | string    | Opcional. O motivo para encerrar a instância de orquestração. |

#### <a name="response"></a>Response

Vários valores de código de status possíveis podem ser retornados.

* **HTTP 202 (Aceito)**: A solicitação de encerramento foi aceita para processamento.
* **HTTP 404 (Não Encontrado)**: A instância especificada não foi encontrada.
* **HTTP 410 (Não existe mais)**: A instância especificada foi concluída ou falhou.

Veja um exemplo de solicitação que encerra uma instância em execução e especifica o motivo **buggy**:

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/terminate?reason=buggy&taskHub=DurableFunctionsHub&connection=Storage&code=XXX
```

As respostas para esta API não têm nenhum conteúdo.

## <a name="rewind-instance-preview"></a>Instância Gerenciada (versão prévia)

Restaura uma instância de orquestração com falha em um estado de execução ao reproduzir novamente as operações com falha mais recentes.

### <a name="request"></a>Solicitação

Para o Functions 1.0, o formato da solicitação é o seguinte:

```http
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/rewind?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

O formato do Functions 2.0 tem os mesmos parâmetros, mas tem um prefixo de URL ligeiramente diferente:

```http
POST /runtime/webhooks/durabletask/instances/{instanceId}/rewind?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

Parâmetros de solicitação para essa API incluem o conjunto padrão mencionado anteriormente, bem como o seguinte parâmetro exclusivo.

| Campo       | Tipo de Parâmetro  | Tipo de Dados | DESCRIÇÃO |
|-------------|-----------------|-----------|-------------|
| reason      | Cadeia de consulta    | string    | Opcional. O motivo para retroceder a instância de orquestração. |

### <a name="response"></a>Response

Vários valores de código de status possíveis podem ser retornados.

* **HTTP 202 (Aceito)**: A solicitação de retroceder foi aceita para processamento.
* **HTTP 404 (Não Encontrado)**: A instância especificada não foi encontrada.
* **HTTP 410 (Não existe mais)**: A instância especificada foi concluída ou encerrada.

Veja um exemplo de solicitação que retrocede uma instância com falha e especifica o motivo **corrigido**:

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/rewind?reason=fixed&taskHub=DurableFunctionsHub&connection=Storage&code=XXX
```

As respostas para esta API não têm nenhum conteúdo.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Saiba como tratar erros](durable-functions-error-handling.md)
