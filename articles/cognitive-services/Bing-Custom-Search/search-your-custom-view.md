---
title: Pesquisar uma exibição personalizada – Pesquisa Personalizada do Bing
titlesuffix: Azure Cognitive Services
description: Descreve como pesquisar um modo de exibição personalizado da Web.
services: cognitive-services
author: aahill
manager: cgronlun
ms.service: cognitive-services
ms.subservice: bing-custom-search
ms.topic: conceptual
ms.date: 09/28/2017
ms.author: maheshb
ms.openlocfilehash: c2fb387026f077ac2b111f2d482cc6c5226642aa
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55198173"
---
# <a name="call-your-bing-custom-search-instance-from-the-portal"></a>Chame sua instância de Pesquisa Personalizada do Bing no Portal

Depois de configurar sua experiência de pesquisa personalizada, você pode testar a partir do [portal](https://customsearch.ai) de Pesquisa Personalizada do Bing. 

![Uma captura de tela do portal de Pesquisa Personalizada do Bing](media/portal-search-screen.png)
## <a name="create-a-search-query"></a>Criar uma consulta de pesquisa 

Depois que você entrou no [portal](https://customsearch.ai) de Pesquisa Personalizada do Bing, selecione sua instância de pesquisa e clique na guia **Produção**. Em **Pontos de extremidade**, selecione um ponto de extremidade de API (por exemplo, API Web). Sua assinatura determina quais pontos de extremidade são mostrados.

Para criar uma consulta de pesquisa, insira os valores de parâmetro para seu ponto de extremidade. Observe que os parâmetros exibidos no portal podem mudar dependendo do ponto de extremidade queescolher. Consulte a [Referência da API de Pesquisa Personalizada](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#query-parameters) para mais informações. 

Alguns parâmetros importantes estão abaixo:


|Parâmetro  |DESCRIÇÃO  |
|---------|---------|
|Consultar     | O termo de pesquisa a ser pesquisado. Disponível somente para pontos de extremidade da Web, de Imagem, de Vídeo e da Sugestão Automática |
|ID de configuração personalizada | O ID de configuração da instância selecionada de Pesquisa Personalizada. Este campo é somente leitura. |
|Mercado     | O mercado que os resultados serão originados. Disponível somente para Web, Imagem, Vídeo e ponto de extremidade da Interface do Usuário Hospedada.        |
|Chave de Assinatura | A chave de assinatura para o teste. Selecione uma chave na lista suspensa ou inserir uma manualmente.          |

Clicar em **Parâmetros adicionais** revela os seguintes parâmetros:  

|Parâmetro  |DESCRIÇÃO  |
|---------|---------|
|Salvar pesquisa     | Um filtro usado para filtrar as páginas da Web para conteúdo adulto. Disponível somente para Web, Imagem, Vídeo e ponto de extremidade da Interface do Usuário Hospedada.        |
|Linguagens de Interface do Usuário    | A linguagem a ser usada para cadeias de caracteres de interface do usuário. Por exemplo, se você habilitar imagens e vídeos na interface do usuário hospedada, as guias **Imagem** e **Vídeo** usarão o idioma especificado.        |
|Contagem     | O número de resultados da pesquisa a ser retornado na resposta. Disponível somente para pontos de extremidade da Web, de Imagem e de Vídeo.         |
|Deslocamento    | O número de resultados da pesquisa a ignorar antes de retornar resultados. Disponível somente para pontos de extremidade da Web, de Imagem e de Vídeo.        |
    
Depois de especificar todas as opções necessárias, clique em **Chamar** para exibir a resposta JSON no painel direito. Se você selecionar o ponto de extremidade da Interface do Usuário Hospedada, poderá testar a experiência de pesquisa no painel inferior.

## <a name="next-steps"></a>Próximas etapas

- [Chamar o modo de exibição personalizado com C#](./call-endpoint-csharp.md)
- [Chamar o modo de exibição personalizado com Java](./call-endpoint-java.md)
- [Chamar o modo de exibição personalizado com NodeJs](./call-endpoint-nodejs.md)
- [Chamar o modo de exibição personalizado com Python](./call-endpoint-python.md)

- [Chamar a exibição personalizada com o SDK do C#](./sdk-csharp-quick-start.md)
