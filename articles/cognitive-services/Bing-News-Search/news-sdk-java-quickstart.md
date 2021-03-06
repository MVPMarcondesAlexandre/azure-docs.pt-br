---
title: 'Início Rápido: Executar uma pesquisa de notícias – SDK de Pesquisa de Notícias do Bing para Java'
titleSuffix: Azure Cognitive Services
description: Use este Início Rápido para pesquisar notícias usando o SDK de Pesquisa de Notícias do Bing para Java e processar a resposta.
services: cognitive-services
author: mikedodaro
manager: cgronlun
ms.service: cognitive-services
ms.subservice: bing-news-search
ms.topic: quickstart
ms.date: 01/10/2019
ms.author: v-gedod
ms.custom: seodec2018
ms.openlocfilehash: 5bfd07eb11fd4504fa8c674ecb144c5fe328cc06
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55149570"
---
# <a name="quickstart-search-for-news-with-the-bing-news-search-sdk-for-java"></a>Início Rápido: Pesquisar notícias com o SDK de Pesquisa de Notícias do Bing para Java

Use este início rápido para começar a pesquisar notícias com o SDK de Pesquisa de Notícias do Bing para Java. Embora a Pesquisa de Notícias do Bing tenha uma API REST compatível com a maioria das linguagens de programação, o SDK fornece uma maneira fácil de integrar o serviço aos seus aplicativos. O código-fonte desta amostra pode ser encontrado no [GitHub](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingNewsSearch).

## <a name="prerequisites"></a>Pré-requisitos

Instale as dependências do SDK de Pesquisa de Notícias do Bing usando o Maven, o Gradle ou outro sistema de gerenciamento de dependências. O arquivo POM Maven requer a seguinte declaração:

```xml
    <dependencies>
    <dependency>
        <groupId>com.microsoft.azure.cognitiveservices</groupId>
        <artifactId>azure-cognitiveservices-newssearch</artifactId>
        <version>0.0.1-beta-SNAPSHOT</version>
    </dependency>
    </dependencies>
```

[!INCLUDE [cognitive-services-bing-news-search-signup-requirements](../../../includes/cognitive-services-bing-news-search-signup-requirements.md)]

## <a name="create-and-initialize-a-project"></a>Criar e inicializar um projeto

Crie um novo projeto Java em seu IDE ou editor favorito e importe as bibliotecas a seguir.

```java
import com.microsoft.azure.cognitiveservices.newssearch.*;
import com.microsoft.azure.cognitiveservices.newssearch.implementation.NewsInner;
import com.microsoft.azure.cognitiveservices.newssearch.implementation.NewsSearchAPIImpl;
import com.microsoft.azure.cognitiveservices.newssearch.implementation.TrendingTopicsInner;
import com.microsoft.rest.credentials.ServiceClientCredentials;
import okhttp3.Interceptor;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.io.IOException;
```

## <a name="create-a-search-client-and-store-credentials"></a>Criar um cliente de pesquisa e credenciais de armazenamento

1. Criar um método chamado `getClient()` que retorna um novo cliente de pesquisa `NewsSearchAPIImpl`. Adicione o ponto de extremidade como o primeiro parâmetro para o novo objeto `NewsSearchAPIImpl` e um novo objeto `ServiceClientCredentials` para armazenar as credenciais.

    ```java
    public static NewsSearchAPIImpl getClient(final String subscriptionKey) {
        return new NewsSearchAPIImpl("https://api.cognitive.microsoft.com/bing/v7.0/",
                new ServiceClientCredentials() {
                });
    }
    ```

2. Para criar o objeto `ServiceClientCredentials`, substitua a função `applyCredentialsFilter()`. Passe um `OkHttpClient.Builder` para o método e use o método `addNetworkInterceptor()` do construtor para criar as credenciais para a chamada do SDK.

    ```java
    new ServiceClientCredentials() {
        @Override
        public void applyCredentialsFilter(OkHttpClient.Builder builder) {
            builder.addNetworkInterceptor(
                    new Interceptor() {
                        @Override
                        public Response intercept(Chain chain) throws IOException {
                            Request request = null;
                            Request original = chain.request();
                            // Request customization: add request headers.
                            Request.Builder requestBuilder = original.newBuilder()
                                    .addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
                            request = requestBuilder.build();
                            return chain.proceed(request);
                        }
                    });
        }
    });
    ```

## <a name="send-and-receive-a-search-request"></a>Enviar e receber uma solicitação de pesquisa

1. Crie um método que chama `getClient()` e envia uma solicitação de pesquisa para o serviço de Pesquisa de Notícias do Bing. Filtre a pesquisa com os parâmetros *market* e *count* e, em seguida, imprima informações sobre o primeiro resultado de notícias: nome, URL, data de publicação, descrição, nome do provedor e número total de correspondências estimadas da pesquisa.

    ```java
    public static void newsSearch(String subscriptionKey)
    {
        NewsSearchAPIImpl client = getClient(subscriptionKey);
        String searchTerm = "Quantum Computing";
    
        NewsInner newsResults = client.searchs().list(searchTerm, null, null, null,
                null, null, 100, null, "en-us",
                null, null, null, null, null,
                null, null);
    
        if (newsResults.value().size() > 0)
        {
            NewsArticle firstNewsResult = newsResults.value().get(0);
    
            System.out.println(String.format("TotalEstimatedMatches value: %d", newsResults.totalEstimatedMatches()));
            System.out.println(String.format("News result count: %d", newsResults.value().size()));
            System.out.println(String.format("First news name: %s", firstNewsResult.name()));
            System.out.println(String.format("First news url: %s", firstNewsResult.url()));
            System.out.println(String.format("First news description: %s", firstNewsResult.description()));
            System.out.println(String.format("First news published time: %s", firstNewsResult.datePublished()));
            System.out.println(String.format("First news provider: %s", firstNewsResult.provider().get(0).name()));
        }
        else
        {
            System.out.println("Couldn't find news results!");
        }
    
    }
    
    ```

2. Adicione o método de pesquisa a um método `main()` para executar o código.

    ```java 
    public static void main(String[] args) {
        String subscriptionKey = "YOUR-SUBSCRIPTION-KEY";
        NewsSearchSDK.newsSearch(subscriptionKey);
    }
    ```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
[Criar um aplicativo Web de página única](tutorial-bing-news-search-single-page-app.md)
