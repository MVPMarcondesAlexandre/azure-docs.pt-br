---
title: Exibir ou analisar os dados coletados do Azure Log Analytics | Microsoft Docs
description: Este artigo inclui um tutorial que descreve como criar pesquisas de logs e analisar dados armazenados no recurso do Log Analytics usando o portal da Pesquisa de Logs.  O tutorial inclui executar algumas consultas simples para retornar diferentes tipos de dados e analisar os resultados.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 07/31/2018
ms.author: magoedte
ms.custom: mvc
ms.openlocfilehash: c64c0837956c59cf7a810bb06ca63bc21c5158d1
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53186422"
---
# <a name="view-or-analyze-data-collected-with-log-analytics-log-search"></a>Exibir ou analisar os dados coletados com a pesquisa de logs do Log Analytics

No Log Analytics, você pode aproveitar as pesquisas de logs construindo consultas para analisar os dados coletados e usar os painéis pré-existentes, que podem ser personalizados com exibições gráficas das pesquisas mais importantes.  Agora que você definiu a coleta de dados operacionais das VMs do Azure e dos Logs de Atividades, neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Realizar uma pesquisa simples de dados de eventos e usar recursos para modificar e filtrar os resultados 
> * Trabalhar com os dados de desempenho

Para concluir o exemplo neste tutorial, você deve ter uma máquina virtual existente [conectada ao workspace do Log Analytics](../../azure-monitor/learn/quick-collect-azurevm.md).  

Criar e editar consultas, além de trabalhar interativamente com dados retornados, pode ser realizado de duas maneiras.  Para consultas básicas, use a página de pesquisa de logs no portal do Azure, ou para consultas avançadas, você pode usar o portal de análise avançada. Para saber mais sobre as diferenças na funcionalidade entre os dois portais, consulte [Portais para criar e editar consultas de log no Log Analytics do Azure](../../azure-monitor/log-query/portals.md)

Neste tutorial, trabalhararemos com pesquisa de logs no portal do Azure. 

## <a name="log-in-to-azure-portal"></a>Fazer logon no portal do Azure
Faça logon no Portal do Azure em [https://portal.azure.com](https://portal.azure.com). 

## <a name="open-the-log-search-portal"></a>Abra o portal de Pesquisa de Logs 
Inicie abrindo o portal de Pesquisa de Logs.   

1. No portal do Azure, clique em **Todos os serviços**. Na lista de recursos, digite **Monitor**. Quando você começa a digitar, a lista é filtrada com base em sua entrada. Selecione **Monitor**.
2. No menu de navegação Monitor, selecione **Log Analytics**, em seguida, selecione um workspace.

## <a name="create-a-simple-search"></a>Crie uma pesquisa simples
A maneira mais rápida de recuperar alguns dados para trabalhar é uma consulta simples que retorna todos os registros na tabela.  Se você tiver algum cliente Windows ou Linux conectado ao seu workspace, você terá dados na tabela de Eventos (Windows) ou Syslog (Linux).

Digite um das seguintes consultas na caixa de pesquisa e clique no botão de pesquisa.  

```
Event
```
```
Syslog
```

Os dados são retornados na exibição de lista padrão e você poderá consultar quantos registros foram retornados no total.

![Consulta simples](media/tutorial-viewdata/log-analytics-portal-eventlist-01.png)

Apenas as primeiras propriedades de cada registro são exibidas.  Clique em **mostrar mais** para exibir todas as propriedades de um registro particular.

## <a name="filter-results-of-the-query"></a>Filtre os resultados da consulta
No lado esquerdo da tela está o painel de filtro que permite adicionar filtragem à consulta sem modificá-la diretamente.  Várias propriedades de registro são exibidas para esse tipo de registro e você pode selecionar um ou mais valores de propriedade para restringir os resultados da pesquisa.

Se você estiver trabalhando com **Evento**, marque a caixa de seleção próxima ao **Erro** em **EVENTLEVELNAME**.   Se estiver trabalhando com **Syslog**, marque a caixa de seleção próxima ao **erro** em **SEVERITYLEVEL**.  Isso altera a consulta para uma das seguintes opções para limitar os resultados aos eventos de erro.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/tutorial-viewdata/log-analytics-portal-eventlist-02.png)

Adicione propriedades ao painel de filtro, selecionando **Adicionar para filtros** do menu de propriedades em um dos registros.

![Adicionar ao menu de filtro](media/tutorial-viewdata/log-analytics-portal-eventlist-03.png)

É possível definir o mesmo filtro, selecionando **Filtro** no menu de propriedades para um registro com o valor que deseja filtrar.  

Você tem somente a opção **Filtro** para propriedades com o nome em azul ao focalizá-las.  Estes são campos *pesquisáveis* que estão indexados para as condições de pesquisa.  Os campos em cinza são *campos pesquisáveis de texto livre* que somente possuem a opção **Mostrar referências**.  Esta opção retorna registros que possuem esse valor em qualquer propriedade.

É possível agrupar os resultados em uma propriedade única, selecionando a opção **Agrupar por** no menu de registro.  Isso adicionará um operador [resumido](/azure/kusto/query/summarizeoperator) à sua consulta que exibirá os resultados em um gráfico.  É possível agrupar em mais de uma propriedade, mas será necessário editar a consulta diretamente.  Selecione o menu de registro próximo à propriedade **Computador** e selecione **Agrupar por 'Computador'**.  

![Agrupar por computador](media/tutorial-viewdata/log-analytics-portal-eventlist-04.png)

## <a name="work-with-results"></a>Trabalhar com os resultados
O portal de Pesquisa de Logs possui uma variedade de recursos para trabalhar com os resultados de uma consulta.  É possível classificar, filtrar e agrupar os resultados para analisar os dados sem modificar a consulta real.  Os resultados de uma consulta não são classificados por padrão.

Para exibir os dados em formulário de tabela que fornece opções adicionais para filtrar e classificar, clique em **Tabela**.  

![Exibição da tabela](media/tutorial-viewdata/log-search-portal-table-01.png)

Clique na seta por um registro para exibir os detalhes desse registro.

![Classificar resultados](media/tutorial-viewdata/log-search-portal-table-02.png)

Classifique em qualquer campo, clicando no cabeçalho de coluna.

![Classificar resultados](media/tutorial-viewdata/log-search-portal-table-03.png)

Filtre os resultados em um valor específico na coluna, clicando no botão de filtro e fornecendo uma condição de filtro.

![Resultados do filtro](media/tutorial-viewdata/log-search-portal-table-04.png)

Agrupe uma coluna, arrastando o cabeçalho da coluna para o topo dos resultados.  É possível agrupar em campos múltiplos, arrastando colunas múltiplas para o topo.

![Resultados de grupo](media/tutorial-viewdata/log-search-portal-table-05.png)


## <a name="work-with-performance-data"></a>Trabalhe com dados de desempenho
Os dados de desempenho para agentes do Windows e Linux são armazenados no workspace do Log Analytics na tabela **Perf**.  Os registros de desempenho são semelhante a qualquer outro registro e vamos escrever uma consulta simples que retorna todos os registros de desempenho, assim como ocorre com os eventos.

```
Perf
```

![Dados de desempenho](media/tutorial-viewdata/log-analytics-portal-perfsearch-01.png)

Retornando milhões de registros para todos contadores e objetos de desempenho, porém, não é muito útil.  É possível utilizar os mesmos métodos usados acima para filtrar os dados ou apenas digitar a seguinte consulta diretamente na caixa de pesquisa de logs.  Isso retorna somente os registros de utilização do processador para computadores Windows e Linux.

```
Perf | where ObjectName == "Processor"  | where CounterName == "% Processor Time"
```

![Utilização do processador](media/tutorial-viewdata/log-analytics-portal-perfsearch-02.png)

Isso limita os dados para um contador particular, mas ainda não o coloca em uma forma particularmente útil.  É possível exibir os dados em um gráfico de linhas, mas primeiro deverá agrupar por computador e TimeGenerated.  Para agrupar em campos múltiplo será necessário modificar a consulta diretamente, então, modifique a consulta para o seguinte.  Isso usa a função [avg](/azure/kusto/query/avg-aggfunction) na propriedade **CounterValue** para calcular o valor médio ao longo de cada hora.

```
Perf  
| where ObjectName == "Processor"  | where CounterName == "% Processor Time"
| summarize avg(CounterValue) by Computer, TimeGenerated
```

![Gráfico de dados de desempenho](media/tutorial-viewdata/log-analytics-portal-perfsearch-03.png)

Agora que os dados estão adequadamente agrupados, você poderá exibi-los em um gráfico visual, adicionando o operador [renderizar](/azure/kusto/query/renderoperator).  

```
Perf  
| where ObjectName == "Processor" | where CounterName == "% Processor Time" 
| summarize avg(CounterValue) by Computer, TimeGenerated 
| render timechart
```

![Gráfico de Linhas](media/tutorial-viewdata/log-analytics-portal-linechart-01.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu a criar pesquisas de logs básicas para analisar dados de desempenho e eventos.  Avance para o próximo tutorial para saber como visualizar os dados criando um painel.

> [!div class="nextstepaction"]
> [Criar e compartilhar painéis do Log Analytics](tutorial-logs-dashboards.md)
