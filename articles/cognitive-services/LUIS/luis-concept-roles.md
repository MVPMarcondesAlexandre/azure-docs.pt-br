---
title: Funções para entidades
titleSuffix: Azure Cognitive Services
description: As funções são subtipos nomeados e contextuais de uma entidade usada apenas em padrões. Por exemplo, na declaração `buy a ticket from New York to London`, New York e London são cidades, mas cada uma tem um significado diferente na frase. Nova York é a cidade de origem e Londres é a cidade de destino.
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: diberry
ms.openlocfilehash: f5768012a03629190a65dd86d004dc842d99912e
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55215939"
---
# <a name="entity-roles-in-patterns-are-contextual-subtypes"></a>Papéis de entidades em padrões são subtipos contextuais
As funções são subtipos nomeados, contextuais de uma entidade usada apenas em [padrões](luis-concept-patterns.md).

Por exemplo, na declaração `buy a ticket from New York to London`, New York e London são cidades, mas cada uma tem um significado diferente na frase. Nova York é a cidade de origem e Londres é a cidade de destino. 

As funções dão um nome para essas diferenças:

|Entidade|Função|Finalidade|
|--|--|--|
|Local padrão|origin|de onde o avião parte|
|Local padrão|destino|onde o avião pousa|
|datetimeV2 predefinido|para|Data de término|
|datetimeV2 predefinido|de|Data de início|

## <a name="how-are-roles-used-in-patterns"></a>Como as funções são usadas em padrões?
Na declaração modelo do padrão, as funções são usadas dentro da declaração: 

|Padrão com funções de entidade|
|--|
|`buy a ticket from {Location:origin} to {Location:destination}`|


## <a name="role-syntax-in-patterns"></a>Sintaxe da função em padrões
A entidade e a função estão entre parênteses, `{}`. A entidade e a função são separadas por dois-pontos. 


[!INCLUDE [H2 Roles versus hierarchical entities](../../../includes/cognitive-services-luis-hier-roles.md)] 

## <a name="example-role-for-entities"></a>Função de exemplo para Entidades

Uma função é apenas uma colocação contextualmente adquirida de uma entidade dentro de um enunciado. Ele é mais eficaz quando a expressão tem mais de um tipo de entidade. O exemplo mais fácil para qualquer tipo de entidade é para distinguir entre um local de e para. O local pode ser representado por muitos tipos de entidade diferentes. 

Um exemplo de caso de uso é a transferência de um funcionário de um departamento para outro em que cada departamento é um item em uma lista. Por exemplo:  

`Move [PersonName] from [Department:from] to [Department:to]`. 

Na previsão retornada, ambas as entidades de departamento serão retornadas na resposta JSON e cada uma incluirá o nome da função. 

## <a name="roles-with-prebuilt-entities"></a>Funções com entidades pré-construídas

Use funções com entidades pré-construídas para dar significado a diferentes instâncias da entidade pré-construída em um enunciado. 

### <a name="roles-with-datetimev2"></a>Funções com datetimeV2

A entidade predefinida, datetimeV2, faz um ótimo trabalho compreender uma ampla variedade de variedade em datas e horas em declarações. Você talvez queira especificar datas e intervalos de datas, diferentemente da compreensão de padrão da entidade predefinidas. 

## <a name="next-steps"></a>Próximas etapas

* Saiba como adicionar [funções](luis-how-to-add-entities.md#add-a-role-to-pattern-based-entity)
