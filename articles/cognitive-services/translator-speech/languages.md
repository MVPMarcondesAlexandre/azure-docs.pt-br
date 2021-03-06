---
title: Idiomas com suporte – API de Tradução de Fala
titlesuffix: Azure Cognitive Services
description: Exibir idiomas com suporte da API de Tradução de Fala.
services: cognitive-services
author: Jann-Skotdal
manager: cgronlun
ms.service: cognitive-services
ms.subservice: translator-speech
ms.topic: conceptual
ms.date: 3/5/2018
ms.author: v-jansko
ms.openlocfilehash: c2b518b695fa18a2babb5c5bc4ee84a1193b69d4
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55460328"
---
# <a name="languages-supported-by-the-translator-speech-api"></a>Idiomas com suporte da API de Tradução de Fala

[!INCLUDE [Deprecation note](../../../includes/cognitive-services-translator-speech-deprecation-note.md)]

Os idiomas a seguir são compatíveis com tradução de fala. Se ambos os idiomas forem compatíveis com tradução de fala, a conversão de fala em fala ou a conversão de fala em texto estará disponível. Se não houver suporte para o idioma de destino para a tradução de fala, apenas a tradução com conversão de fala em texto estará disponível. 

| Idioma de fala    |
|:----------- |
| Árabe (padrão moderno)      |
| Chinês (mandarim)      |
| Inglês      |
| Francês      |
| Alemão      |
| Italiano      |
| Japonês      |
| Português (Brasil)     |
| Russo      |
| Espanhol      | 

A API de Tradução de Fala dá suporte aos seguintes idiomas como destino para tradução com conversão de fala em texto. 

| Idioma de texto    | Código de idioma |
|:----------- |:-------------:|
| Africâner      | `af`          |
| Árabe       | `ar`          |
| Bangla      | `bn`          |
| Bósnio (latim)      | `bs`          |
| Búlgaro      | `bg`          |
| Cantonês (tradicional)      | `yue`          |
| Catalão      | `ca`          |
| Chinês (simplificado)      | `zh-Hans`          | 
| Chinês (tradicional)      | `zh-Hant`          |
| Croata      | `hr`          |
| Tcheco      | `cs`          |
| Dinamarquês      | `da`          |
| Holandês      | `nl`          |
| Inglês      | `en`          |
| Estoniano      | `et`          |
| Fijiano      | `fj`          |
| Filipino      | `fil`          |
| Finlandês      | `fi`          |
| Francês      | `fr`          |
| Alemão      | `de`          |
| Grego      | `el`          |
| Crioulo haitiano      | `ht`          |
| Hebraico      | `he`          |
| Híndi      | `hi`          |
| Hmong Daw      | `mww`          |
| Húngaro      | `hu`          |
|Islandês|`is`          |
| Indonésio      | `id`          |
| Italiano      | `it`          |
| Japonês      | `ja`          |
| Suaíli      | `sw`          |
| Klingon      | `tlh`          |
| Klingon (plqaD)      | `tlh-Qaak`          |
| Coreano      | `ko`          |
| Letão      | `lv`          |
| Lituano      | `lt`          |
| Malgaxe      | `mg`          |
| Malaio      | `ms`          |
| Maltês      | `mt`          |
| Norueguês      | `nb`          |
| Persa      | `fa`          |
| Polonês      | `pl`          |
| Português      | `pt`          |
| Queretaro Otomi      | `otq`          |
| Romeno      | `ro`          |
| Russo      | `ru`          |
| Samoano      | `sm`          |
| Sérvio (cirílico)      | `sr-Cyrl`          |
| Sérvio (latino)      | `sr-Latn`          |
| Eslovaco     | `sk`          |
| Esloveno      | `sl`          |
| Espanhol      | `es`          |
| Sueco      | `sv`          |
| Taitiano      | `ty`          |
| Tâmil      | `ta`          |
| Tailandês      | `th`          |
| Tongan      | `to`          |
| Turco      | `tr`          |
| Ucraniano      | `uk`          |
| Urdu      | `ur`          |
| Vietnamita      | `vi`          |
| Galês      | `cy`          |
| Yucatec Maya      | `yua`          |

## <a name="access-the-list-programmatically"></a>Acessar a lista programaticamente

Você pode acessar a lista de idiomas compatíveis programaticamente usando o recurso de idiomas. A lista fornece o código de idioma, bem como o nome do idioma em inglês ou em qualquer outro idioma compatível. Essa lista é atualizada automaticamente pelo serviço de Tradução de Fala conforme novos idiomas são disponibilizados.

O recurso de Idiomas retorna a lista de idiomas compatíveis para fala, texto e conversão de texto em fala. O recurso de idiomas não requer autenticação.

[Visite a referência de API para experimentar o método de idiomas](languages-reference.md)

## <a name="access-the-list-on-the-microsoft-translator-website"></a>Acesse a lista no site do Microsoft Translator

Para uma rápida olhada nos idiomas, o site Microsoft Translator mostra todos os idiomas compatíveis com a Speech API e a API de Tradução de Texto. Esta lista não inclui informações específicas do desenvolvedor, como códigos de idioma.

[Veja a lista de idiomas](https://www.microsoft.com/translator/languages.aspx) 
