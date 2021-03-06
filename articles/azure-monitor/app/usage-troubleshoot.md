---
title: Solucionar problemas de ferramentas de análise de comportamento do usuário no Azure Application Insights
description: Guia de solução de problemas - analisando o uso do aplicativo e site com o Application Insights.
services: application-insights
documentationcenter: ''
author: NumberByColors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 07/11/2018
ms.reviewer: mbullwin
ms.pm_owner: daviste;NumberByColors
ms.author: daviste
ms.openlocfilehash: 7c903390af54d1771bce1b6aff96e9bb54397189
ms.sourcegitcommit: 8330a262abaddaafd4acb04016b68486fba5835b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54044988"
---
# <a name="troubleshoot-user-behavior-analytics-tools-in-application-insights"></a>Solucionar problemas de ferramentas de análise de comportamento do usuário no Application Insights
Solucionar problemas de ferramentas de análise de comportamento do [usuário no Application Insights](usage-overview.md): [Usuários, Sessões, Eventos](usage-segmentation.md), [Funis](usage-funnels.md), [Fluxos dos Usuários](usage-flows.md), [Retenção](usage-retention.md), ou Coortes? Aqui estão algumas respostas.

## <a name="counting-users"></a>Contagem de usuários
**As ferramentas de análise de comportamento do usuário mostram que o meu aplicativo tem um usuário/uma sessão, mas sei que meu aplicativo tem muitos usuários/sessões. Como corrigir essas contagens incorretas?**

Todos os eventos de telemetria do Application Insights possuem um [ID de usuário anônimo](../../azure-monitor/app/data-model-context.md) e uma [ID de sessão](../../azure-monitor/app/data-model-context.md) como duas de suas propriedades padrão. Por padrão, todas as ferramentas de análise de uso fazem a contagem de usuários e sessões com base nessas IDs. Se essas propriedades padrão não estiverem sendo populadas com IDs exclusivas para cada usuário e sessão do seu aplicativo, você verá uma contagem incorreta de usuários e sessões nas ferramentas de análise de uso.

Se você estiver monitorando um aplicativo Web, a solução mais fácil é adicionar o [SDK de JavaScript do Application Insights](../../azure-monitor/app/javascript.md) para seu aplicativo, e certifique-se de que o snippet de código de script tenha sido carregado em cada página que você deseja monitorar. O SDK de JavaScript gera automaticamente as IDs de usuário anônimo e sessões, e preenche os eventos de telemetria com essas IDs que são enviadas do seu aplicativo.

Se você estiver monitorando um serviço Web (sem interface de usuário), [Crie um inicializador de telemetria que preencha as propriedades de ID de usuário anônimo e de sessões](usage-send-user-context.md), de acordo com noções do serviço das sessões e usuários exclusivos.

Se o seu aplicativo estiver enviando [IDs de usuário autenticado](../../azure-monitor/app/api-custom-events-metrics.md#authenticated-users), você pode realizar a contagem com base nas IDs de usuários autenticados na ferramenta de usuários. Na lista suspensa "Mostrar", escolha "Usuários autenticados".

Atualmente, as ferramentas de análise de comportamento do usuário não são compatíveis com a contagem de usuários ou com sessões baseadas nas propriedades que não sejam o ID de usuário anônimo, ID de usuário autenticado ou ID de sessão.

## <a name="naming-events"></a>Nomeando Eventos
**Meu aplicativo tem milhares de exibições de página e nomes de evento personalizado diferentes. É difícil distingui-los, e as ferramentas de análise de comportamento do usuário normalmente não respondem. Como corrigir esses problemas de nomenclatura?**

A exibição de página e os nomes de eventos personalizados são usados nas ferramentas de análise de comportamento do usuário. Nomear bem os eventos é essencial para obter valor dessas ferramentas. A meta é um equilíbrio entre ter poucos nomes excessivamente genéricos ("Botão clicado") e ter muitos nomes excessivamente específicos ("Editar botão clicado http://www.contoso.com/index").

Para fazer alterações no modo de exibição de página e nos nomes de evento personalizado que seu aplicativo está enviando, você precisa alterar o código-fonte e a reimplantação do seu aplicativo. **Todos os dados de telemetria no Application Insights são armazenados por 90 dias e não podem ser excluídos**; portanto, as alterações feitas aos nomes de evento levarão 90 dias para se manifestarem completamente. A 90 dias depois de fazer as alterações no nome, ambos os nomes de evento antigo e novo serão mostrados em sua telemetria, então ajuste as consultas e se comunique com suas equipes adequadamente.

Se o seu aplicativo estiver enviando muitos nomes de exibição de página, verifique se esses nomes de exibição de página estão especificados manualmente no código ou se estão sendo enviados automaticamente pelo SDK do JavaScript do Application Insights:

* Se os nomes da exibição de página forem especificados manualmente no código usando a [`trackPageView` API](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md), altere o nome para que ele seja menos específico. Evite erros comuns, como colocar a URL no nome da exibição de página. Em vez disso, use o parâmetro de URL da API `trackPageView`. Mova outros detalhes do nome de exibição de página para as propriedades personalizadas.

* Se o SDK de JavaScript do Application Insights estiver enviando nomes de exibição de página automaticamente, você pode alterar os títulos de suas páginas ou alternar para enviar manualmente os nomes de exibição de página. O SDK envia o [título](https://developer.mozilla.org/docs/Web/HTML/Element/title) de cada página como o nome de exibição de página, por padrão. Você pode alterar os títulos para que sejam mais gerais, mas lembre-se de SEO e outros impactos que esta alteração pode ter. Especificar manualmente os nomes de exibição de página com a API `trackPageView` substitui os nomes automaticamente coletados; portanto, você pode enviar nomes mais gerais na telemetria sem alterar os títulos de página.   

Se o seu aplicativo estiver enviando um número excessivo de nomes de evento personalizado, altere o nome no código para ser menos específico. Novamente, evite colocar URLs e outras informações por página ou dinâmicas diretamente nos nomes de evento personalizado. Em vez disso, mova esses detalhes para as propriedades personalizadas do evento personalizado com a API `trackEvent`. Por exemplo, em vez de `appInsights.trackEvent("Edit button clicked on http://www.contoso.com/index")`, sugerimos algo como `appInsights.trackEvent("Edit button clicked", { "Source URL": "http://www.contoso.com/index" })`.

## <a name="next-steps"></a>Próximas etapas

* [Visão geral das ferramentas de análise de comportamento do usuário](usage-overview.md)

## <a name="get-help"></a>Obter ajuda
* [Stack Overflow](https://stackoverflow.com/questions/tagged/ms-application-insights)

