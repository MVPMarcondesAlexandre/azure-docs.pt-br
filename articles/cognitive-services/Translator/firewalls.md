---
title: Traduzir atrás de firewalls – API de Tradução de Texto
titlesuffix: Azure Cognitive Services
description: Traduzir atrás de firewalls de IP com a API de Tradução de Texto.
services: cognitive-services
author: Jann-Skotdal
manager: cgronlun
ms.service: cognitive-services
ms.subservice: translator-text
ms.topic: conceptual
ms.date: 11/20/2018
ms.author: v-jansko
ms.openlocfilehash: 7dec156eeb49f7b9f088fb721893f6c82239d509
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55219644"
---
# <a name="how-to-translate-behind-ip-firewalls-with-the-translator-text-api"></a>Como traduzir atrás de firewalls de IP com a API de Tradução de Texto

A API de Tradução de Texto pode ser traduzida por trás de firewalls usando filtragem de IP ou nome de domínio. A filtragem de nome de domínio é o método preferencial. **Não é recomendável** executar o Microsoft Translator por trás de um firewall filtrado por IP. A configuração é suscetível a interrupção no futuro sem aviso prévio. 

## <a name="translator-ip-addresses"></a>Endereços IP do Tradutor
Os endereços IP para api.cognitive.microsofttranslator.com – API de Tradução de Texto da Microsoft a partir de 20 de novembro de 2018:

* **Pacífico Asiático:** 40.90.139.163, 104.44.89.44
* **Europa:** 40.90.138.4, 40.90.141.99
* **América do Norte** 40.90.139.36, 40.90.139.2


## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Traduzir atrás de firewalls de IP na chamada à API do Tradutor](reference/v3-0-translate.md)
