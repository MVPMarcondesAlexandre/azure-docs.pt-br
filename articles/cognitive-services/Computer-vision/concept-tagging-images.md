---
title: Aplicando as marcas de conteúdo para imagens – Pesquisa Visual Computacional
titleSuffix: Azure Cognitive Services
description: Aprenda mais sobre conceitos relacionados ao recurso de marcação de imagem da API da Pesquisa Visual Computacional.
services: cognitive-services
author: PatrickFarley
manager: cgronlun
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: conceptual
ms.date: 08/29/2018
ms.author: pafarley
ms.custom: seodec18
ms.openlocfilehash: 6724f95575e1f918fa29033cd53caaef8c97c81c
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55149646"
---
# <a name="applying-content-tags-to-images"></a>Aplicando as marcas de conteúdo para imagens

A Pesquisa Visual Computacional retorna marcas com base em milhares de objetos reconhecíveis, seres vivos, cenários e ações. Quando as marcações são ambíguas ou pertencem a um conhecimento não comum, a resposta da API fornece 'dicas' para esclarecer o significado da marcação no contexto de um cenário conhecido. As marcas não são organizadas como uma taxonomia e não existe nenhuma hierarquia de herança. Uma coleção de marcas de conteúdo constitui a base para uma 'description' de imagem exibida como uma linguagem legível por humanos formatada em frases completas. Observe que, no momento, para a descrição da imagem, o inglês é o único idioma compatível.

Depois de carregar uma imagem ou especificar um URL de imagem, os algoritmos de Visão da Computação emitem tags com base nos objetos, seres vivos e ações identificadas na imagem. A marcação não está limitada ao assunto principal, como uma pessoa em primeiro plano, mas também inclui o cenário (interno ou externo), móveis, ferramentas, plantas, animais, acessórios, gadgets, etc.

## <a name="image-tagging-example"></a>Exemplo de marcação de imagem

A resposta JSON a seguir ilustra o que o Computer Vision retorna ao marcar recursos visuais detectados na imagem de exemplo.

![Uma casa azul e o jardim da frente](./Images/house_yard.png).

```json
{
    "tags": [
        {
            "name": "grass",
            "confidence": 0.9999995231628418
        },
        {
            "name": "outdoor",
            "confidence": 0.99992108345031738
        },
        {
            "name": "house",
            "confidence": 0.99685388803482056
        },
        {
            "name": "sky",
            "confidence": 0.99532157182693481
        },
        {
            "name": "building",
            "confidence": 0.99436837434768677
        },
        {
            "name": "tree",
            "confidence": 0.98880356550216675
        },
        {
            "name": "lawn",
            "confidence": 0.788884699344635
        },
        {
            "name": "green",
            "confidence": 0.71250593662261963
        },
        {
            "name": "residential",
            "confidence": 0.70859086513519287
        },
        {
            "name": "grassy",
            "confidence": 0.46624681353569031
        }
    ],
    "requestId": "06f39352-e445-42dc-96fb-0a1288ad9cf1",
    "metadata": {
        "height": 200,
        "width": 300,
        "format": "Jpeg"
    }
}
```

## <a name="next-steps"></a>Próximas etapas

Aprenda conceitos sobre [categorizar imagens](concept-categorizing-images.md) e [descrevendo imagens](concept-describing-images.md).
