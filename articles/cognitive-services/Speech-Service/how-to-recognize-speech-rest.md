---
title: Reconhecer fala usando a API REST
titleSuffix: Azure Cognitive Services
description: Saiba como usar a API de Conversão de Fala em Texto no serviço de Fala dos Serviços Cognitivos.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 07/16/2018
ms.author: erhopf
ms.openlocfilehash: 7c7bbaa986a6efdb82a50048c7c218f96cd4014a
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55220324"
---
# <a name="recognize-speech-by-using-the-rest-api"></a>Reconhecer fala usando a API REST

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-how-to-recognize-speech-selector.md)]

A API REST pode ser usada para reconhecer declarações curtas usando uma solicitação HTTP POST.

A API REST é a maneira mais simples de reconhecer a fala se você não está usando uma linguagem compatível com o [SDK](speech-sdk.md). Faça uma solicitação HTTP POST para o ponto de extremidade de serviço e passe a declaração inteira no corpo da solicitação. Você recebe uma resposta que contém o texto reconhecido.

> [!NOTE]
> As declarações ficam limitadas a 15 segundos ou menos ao usar a API REST.
> Fazer check-out a [Speech SDK](how-to-recognize-speech-csharp.md) para reconhecimento de declarações mais tempo.

Para saber mais sobre a API REST de **Conversão de Fala em Texto**, veja o artigo [APIs REST](rest-apis.md#speech-to-text-api). Para ver a API em ação, baixe os [exemplos de API REST](https://github.com/Azure-Samples/SpeechToText-REST) do GitHub.

## <a name="next-steps"></a>Próximas etapas

- Veja a [visão geral da API REST](rest-apis.md).
