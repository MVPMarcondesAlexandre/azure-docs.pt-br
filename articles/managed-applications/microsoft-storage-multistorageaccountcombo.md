---
title: Elemento de interface do usuário do Azure MultiStorageAccountCombo | Microsoft Docs
description: Descreve o elemento de interface do usuário Microsoft.Storage.MultiStorageAccountCombo para o Portal do Azure.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2018
ms.author: tomfitz
ms.openlocfilehash: f5fa81d53e1728e8f566a2a39aed8311828b20c7
ms.sourcegitcommit: 5a7f13ac706264a45538f6baeb8cf8f30c662f8f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37108698"
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Elemento de interface do usuário Microsoft.Storage.MultiStorageAccountCombo
Um grupo de controles para criar várias contas de armazenamento com nomes que começam com um prefixo comum.

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- O valor de `defaultValue.prefix` é concatenado com um ou mais números inteiros para gerar a sequência de nomes de conta de armazenamento. Por exemplo, se `defaultValue.prefix` é **sa** e `count` é **2**, os nomes de conta de armazenamento **sa1** e **sa2** são gerados. Os nomes de conta de armazenamento gerados são validados por exclusividade automaticamente.
- Os nomes de conta de armazenamento são gerados lexicograficamente com base em `count`. Por exemplo, se `count` for 10, os nomes de conta de armazenamento terminarão com números inteiros de 2 dígitos (01, 02, 03).
- O valor padrão de `defaultValue.prefix` é **null**e `defaultValue.type` é **Premium_LRS**.
- Os tipos não especificados em `constraints.allowedTypes` ficam ocultos e os tipos não especificados em `constraints.excludedTypes` são mostrados. `constraints.allowedTypes` e `constraints.excludedTypes` são opcionais, mas não podem ser usados simultaneamente.
- Além de gerar nomes de conta de armazenamento, `count` é usado para definir o multiplicador apropriado para o elemento. Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').storageAccountCount]`. O valor padrão é **1**.

## <a name="sample-output"></a>Saída de exemplo

```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Próximas etapas
* Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](create-uidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](create-uidefinition-elements.md).
