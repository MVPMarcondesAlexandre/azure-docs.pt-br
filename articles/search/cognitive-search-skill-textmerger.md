---
title: Habilidade de Mesclagem de Texto da pesquisa cognitiva – Azure Search
description: Mescle o texto de uma coleção de campos em um campo consolidado. Use essa habilidade cognitiva em um pipeline de enriquecimento do Azure Search.
services: search
manager: pablocas
author: luiscabrer
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: conceptual
ms.date: 01/17/2019
ms.author: luisca
ms.custom: seodec2018
ms.openlocfilehash: a3c64a26ed5ee7454fcfd22f47c1a161f65c6de7
ms.sourcegitcommit: 9b6492fdcac18aa872ed771192a420d1d9551a33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54445336"
---
#    <a name="text-merge-cognitive-skill"></a>Habilidade de percepção do Text Merge

A habilidade do **Text Merge** consolida o texto de uma coleção de campos em um único campo. 

> [!NOTE]
> Essa habilidade não está associada a uma API de Serviços Cognitivos e você não é cobrado por utilizá-la. No entanto, você ainda deverá [anexar um recurso dos Serviços Cognitivos](cognitive-search-attach-cognitive-services.md) para substituir a opção de recurso **Gratuito** que limita você a um pequeno número de enriquecimentos por dia.

## <a name="odatatype"></a>@odata.type  
Microsoft.Skills.Text.MergeSkill

## <a name="skill-parameters"></a>Parâmetros de habilidades

Os parâmetros diferenciam maiúsculas de minúsculas.

| Nome do parâmetro     | DESCRIÇÃO |
|--------------------|-------------|
| insertPreTag  | Cadeia de caracteres a serem incluídas antes de cada inserção. O valor padrão é `" "`. Para omitir o espaço, defina o valor como `""`.  |
| insertPostTag | Cadeia de caracteres a ser incluída antes de cada inserção. O valor padrão é `" "`. Para omitir o espaço, defina o valor como `""`.  |


##  <a name="sample-input"></a>Entrada de exemplo
Um documento JSON fornece entrada utilizável para esta habilidade JSON poderia ser:

```json
{
    "values": [
      {
        "recordId": "1",
        "data":
           {
             "text": "The brown fox jumps over the dog" ,
             "itemsToInsert": ["quick", "lazy"],
             "offsets": [3, 28],
           }
      }
    ]
}
```

##  <a name="sample-output"></a>Saída de exemplo
Este exemplo mostra a saída da entrada anterior, supondo que o *insertPreTag* seja definido como `" "`, e *insertPostTag* seja definido como `""`. 

```json
{
    "values": [
      {
        "recordId": "1",
        "data":
           {
             "mergedText": "The quick brown fox jumps over the lazy dog" 
           }
      }
    ]
}
```

## <a name="extended-sample-skillset-definition"></a>Definição do conjunto de habilidades de exemplo estendido

Um cenário comum para o Text Merge é a capacidade de mesclar a representação textual de imagens (texto de uma habilidade OCR ou a legenda de uma imagem) no campo de conteúdo de um documento. 

O conjunto de qualificações do exemplo a seguir usa a habilidade de OCR para extrair o texto de imagens inseridas no documento. Em seguida, cria um campo *merged_text* que contém texto original e OCRed de cada imagem. 

```json
{
  "description": "Extract text from images and merge with content text to produce merged_text",
  "skills":
  [
    {
        "name": "OCR skill",
        "description": "Extract text (plain and structured) from image.",
        "@odata.type": "#Microsoft.Skills.Vision.OcrSkill",
        "context": "/document/normalized_images/*",
        "defaultLanguageCode": "en",
        "detectOrientation": true,
        "inputs": [
          {
            "name": "image",
            "source": "/document/normalized_images/*"
          }
        ],
        "outputs": [
          {
            "name": "text"
          }
        ]
    },
    {
      "@odata.type": "#Microsoft.Skills.Text.MergeSkill",
      "description": "Create merged_text, which includes all the textual representation of each image inserted at the right location in the content field.",
      "context": "/document",
      "insertPreTag": " ",
      "insertPostTag": " ",
      "inputs": [
        {
          "name":"text", "source": "/document/content"
        },
        {
          "name": "itemsToInsert", "source": "/document/normalized_images/*/text"
        },
        {
          "name":"offsets", "source": "/document/normalized_images/*/contentOffset" 
        }
      ],
      "outputs": [
        {
          "name": "mergedText", "targetName" : "merged_text"
        }
      ]
    }
  ]
}
```
O exemplo acima presume que um campo de imagens normalizado existe. Para gerar esse campo, defina a configuração *imageAction* na definição do indexador para *generateNormalizedImages* conforme mostrado abaixo:

```json
{  
   //...rest of your indexer definition goes here ... 
  "parameters":{  
      "configuration":{  
         "dataToExtract":"contentAndMetadata",
         "imageAction":"generateNormalizedImages"
      }
   }
}
```

## <a name="see-also"></a>Consulte também

+ [Habilidades predefinidas](cognitive-search-predefined-skills.md)
+ [Como definir um conjunto de qualificações](cognitive-search-defining-skillset.md)
+ [Criar Indexador (REST)](https://docs.microsoft.com/rest/api/searchservice/create-indexer)
