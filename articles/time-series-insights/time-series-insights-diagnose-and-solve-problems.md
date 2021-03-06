---
title: Diagnosticar e solucionar problemas no Azure Time Series Insights | Microsoft Docs
description: Este artigo descreve como diagnosticar e solucionar problemas comuns que podem ser encontrados em seu ambiente do Azure Time Series Insights.
ms.service: time-series-insights
services: time-series-insights
author: ashannon7
ms.author: anshan
manager: cshankar
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.workload: big-data
ms.topic: troubleshooting
ms.date: 04/09/2018
ms.custom: seodec18
ms.openlocfilehash: 36ea2b8d3649fbda5a5cd6cc5f2cd05cdc095902
ms.sourcegitcommit: b767a6a118bca386ac6de93ea38f1cc457bb3e4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53555805"
---
# <a name="diagnose-and-solve-issues-in-your-time-series-insights-environment"></a>Diagnosticar e resolver problemas no ambiente do Time Series Insights

Este artigo descreve alguns problemas que você pode encontrar em seu ambiente do Azure Time Series Insights. O artigo fornece possíveis causas e soluções para resolução.

## <a name="video"></a>Vídeo: 

Neste vídeo, abordamos desafios comuns dos clientes no Time Series Insights e suas mitigações:</br>

> [!VIDEO https://www.youtube.com/embed/7U0SwxAVSKw]

## <a name="problem-1-no-data-is-shown"></a>Problema 1: nenhum dado é exibido

Há vários motivos comuns pelos quais você não pode ver seus dados no [gerenciador do Azure Time Series Insights](https://insights.timeseries.azure.com):

### <a name="cause-a-event-source-data-isnt-in-json-format"></a>Causa A: os dados de origem do evento não estão no formato JSON

O Azure Time Series Insights dá suporte somente a dados JSON. Para obter exemplos do JSON, consulte [Formas de JSON com suporte](./how-to-shape-query-json.md).

### <a name="cause-b-the-event-source-key-is-missing-a-required-permission"></a>Causa B: a chave da origem do evento não tem uma permissão necessária

* Para um hub IoT no Hub IoT do Azure, você precisa fornecer a chave com as permissões de **conexão de serviço**. Qualquer uma das políticas **iothubowner** ou **serviço** funcionará porque ambas têm permissões de **conexão de serviço**.

   ![Permissões de conexão de serviço do Hub IoT](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)


* Para um hub de eventos nos Hubs de Eventos do Azure, você precisa fornecer a chave que tem a permissão de **escuta**. Qualquer umas das políticas de **ler** ou **gerenciar** funcionará porque ambas têm permissões para **escutar**.

   ![Permissão de escuta do hub de eventos](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

### <a name="cause-c-the-consumer-group-provided-isnt-exclusive-to-time-series-insights"></a>Causa C: o grupo de consumidores fornecido não é exclusivo do Time Series Insights

Quando você registra um hub IoT ou um hub de eventos, é importante definir o grupo de consumidores que deseja usar para ler os dados. Esse grupo de consumidores *não pode ser compartilhado*. Se o grupo de consumidores for compartilhado, o hub IoT ou o hub de eventos subjacente desconectará de forma automática e aleatória um dos leitores. Forneça um grupo de consumidores exclusivo para o Time Series Insights para leitura.

## <a name="problem-2-some-data-is-shown-but-data-is-missing"></a>Problema 2: alguns dados são exibidos, mas alguns estão ausentes

Quando dados são exibidos apenas parcialmente e parecem estar apresentando retardo, você deve considerar várias possibilidades.

### <a name="cause-a-your-environment-is-being-throttled"></a>Causa A: o ambiente está sofrendo limitação

A limitação é um problema comum quando os ambientes são provisionados após você criar uma origem do evento que tem dados. Os Hubs de Eventos do Azure e o Hub IoT do Azure armazenam dados por até sete dias. O Time Series Insights sempre começa com o evento mais antigo na origem do evento (primeiro a entrar, primeiro a sair ou *PEPS*). 

Por exemplo, se você tiver 5 milhões de eventos em uma origem do evento quando se conecta a um ambiente do Time Series Insights S1, de unidade única, o Time Series Insights lerá aproximadamente 1 milhão de eventos por dia. Pode parecer que o Time Series Insights está apresentando cinco dias de latência. No entanto, o que está acontecendo é que o ambiente está sendo limitado. 

Se houver eventos antigos na origem do evento, você poderá lidar com a limitação de duas maneiras:

- Alterar os limites de retenção da origem do evento para ajudar a eliminar eventos antigos que você não quer exibir no Time Series Insights.
- Provisionar um tamanho de ambiente maior (número de unidades) para aumentar a taxa de transferência de eventos antigos. Usando o exemplo anterior, se você aumentou o mesmo ambiente S1 para cinco unidades por um dia, o ambiente deverá atualizar durante o dia. Se a produção de evento de estado contínuo for de um milhão ou menos de eventos por dia, será possível reduzir a capacidade do evento para uma unidade após ele ser atualizado.

A limitação é imposta com base na capacidade e no tipo de SKU do ambiente. Todas as origens do evento no ambiente compartilham essa capacidade. Se a origem do evento do hub de eventos ou do hub IoT enviar dados por push além dos limites impostos, você verá a limitação e um retardo.

A figura a seguir mostra um ambiente do Time Series Insights com um SKU S1 e uma capacidade 3. Ele pode ingressar 3 milhões de eventos por dia.

![Capacidade atual do SKU do ambiente](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Por exemplo, suponha que esse ambiente esteja ingerindo mensagens de um hub de eventos. A figura a seguir mostra a taxa de entrada:

![Taxa de entrada de exemplo para um hub de eventos](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

A taxa de entrada diária é de cerca de 67.000 mensagens. Essa taxa é equivalente a aproximadamente 46 mensagens por minuto. Se cada mensagem do hub de eventos for nivelada para um único evento do Time Series Insights, a limitação não ocorrerá. Se cada mensagem do hub de eventos for nivelada para 100 eventos do Time Series Insights, 4.600 eventos deverão ser ingeridos a cada minuto. Um ambiente de SKU S1 que tem uma capacidade de 3 pode ingressar apenas 2.100 eventos por minuto (1 milhão de eventos por dia = 700 eventos por minuto em 3 unidades = 2.100 eventos por minuto). Para essa configuração, você observa um retardo devido à limitação. 

Para obter um entendimento de alto nível sobre como funciona a lógica de nivelamento, consulte a seção [Formas de JSON com suporte](./how-to-shape-query-json.md).

#### <a name="recommended-resolutions-for-excessive-throttling"></a>Resolução recomendadas para limitação excessiva

Para corrigir o retardo, aumente a capacidade do SKU do ambiente. Para obter mais informações, confira [Dimensionar o ambiente do Time Series Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="cause-b-initial-ingestion-of-historical-data-slows-ingress"></a>Causa B: entrada inicial de dados históricos retarda a entrada

Se você se conectar a uma origem do evento existente, provavelmente o hub IoT ou o hub de eventos já conterá dados. O ambiente inicia o pull dos dados desde o início do período de retenção de mensagens da origem do evento. Esse é o processamento padrão, que não pode ser substituído. Você pode acionar a limitação. A limitação pode levar algum tempo para ficar atualizada conforme ela consome os dados históricos.

#### <a name="recommended-resolutions-for-large-initial-ingestion"></a>Soluções recomendadas de ingestão inicial grande

Para corrigir o retardo:

1. aumente a capacidade do SKU para o valor máximo permitido (10, neste caso). Após você aumentar a capacidade, o processo de entrada começará a se atualizar muito mais rapidamente. Você é cobrado pelo aumento da capacidade. Para visualizar a rapidez da atualização, você pode exibir o do gráfico de disponibilidade no [gerenciador do Time Series Insights](https://insights.timeseries.azure.com). 

2. Depois que o retardo for atualizado, diminua a capacidade do SKU para a taxa de entrada normal.

## <a name="problem-3-my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Problema 3: a configuração de nome da propriedade do carimbo de data/hora de minha origem do evento não funciona

Verifique se o nome e o valor da propriedade de nome do carimbo de data/hora estão em conformidade com as seguintes regras:
* O nome da propriedade do carimbo de data/hora diferencia maiúsculas de minúsculas.
* O valor da propriedade do carimbo de data/hora é obtido da origem do evento, como uma cadeia de caracteres JSON, deve ter o formato _yyyy-MM-ddTHH:mm:ss.FFFFFFFK_. Um exemplo é **2008-04-12T12:53Z**.

A maneira mais fácil de assegurar que o nome da propriedade Carimbo de data/hora seja capturado e funcione corretamente é usar o gerenciador do Time Series Insights. No gerenciador do Time Series Insights, usando o gráfico, selecione um período de tempo após fornecer o nome da propriedade de carimbo de data/hora. Clique com o botão direito do mouse na seleção e escolha a opção **Explorar eventos**. 

O cabeçalho da primeira coluna deve ser o nome da propriedade de carimbo de data/hora. Ao lado da palavra **Timestamp**, você deverá ver **($ts)**. 

Você não deverá ver os seguintes valores:
- *(abc)*: indica que o Time Series Insights está lendo os valores de dados como cadeias de caracteres.
- *Ícone de calendário*: indica que o Time Series Insights está lendo os valores de dados como *datetime*.
- *#*: indica que o Time Series Insights está lendo os valores de dados como um inteiro.


## <a name="next-steps"></a>Próximas etapas

- Para obter assistência, inicie uma conversa no [fórum do MSDN](https://social.msdn.microsoft.com/Forums/home?forum=AzureTimeSeriesInsights) ou no [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-timeseries-insights). 
- Use o [suporte do Azure](https://azure.microsoft.com/support/options/) para obter opções de suporte assistido.
