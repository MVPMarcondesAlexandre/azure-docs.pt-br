---
title: Criar base de dados de conhecimento
titleSuffix: QnA Maker - Azure Cognitive Services
description: Use o portal do QnA Maker para criar uma base de dados de conhecimento com bate-papo. Isso torna seu aplicativo envolvente. Adicione um conjunto pré-populado do bate-papo principal à sua base de dados de conhecimento como ponto de partida para o bate-papo do seu bot, economizando o tempo e o custo de escrevê-lo do zero.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: article
ms.date: 12/11/2018
ms.author: tulasim
ms.custom: seodec18
ms.openlocfilehash: cb62be34f7f294bda83920f95c9f7c7bd63cfbda
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55219678"
---
# <a name="quickstart-create-a-knowledge-base-using-the-qna-maker-portal"></a>Início Rápido: Criar uma base de dados de conhecimento usando portal do QnA Maker

O QnA Maker simplifica a adição das fontes de dados existentes ao criar uma base de dados de conhecimento. Você pode criar uma nova base de dados de conhecimento do QnA Maker dos seguintes tipos de documento:

<!-- added for scanability -->
* Páginas de perguntas frequentes
* Manuais de produtos
* Documentos estruturados

Inclua uma personalidade de bate-papo para tornar suas informações mais interessantes para seus usuários.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar. 

## <a name="create-a-new-knowledge-base"></a>Como criar uma nova base de dados de conhecimento

1. Entre no [portal do QnA Maker](https://qnamaker.ai) com suas credenciais do Azure e selecione **Criar uma base de dados de conhecimento**.

1. Se você ainda não criou um serviço do QnA Maker, selecione **Criar um serviço do QnA**. 

1. Selecione seu locatário do Azure, o nome da assinatura do Azure e o nome do recurso do Azure associados ao serviço do QnA Maker nas listas na **Etapa 2** no portal do QnA Maker. Selecione o serviço do QnA Maker do Azure que hospedará a Base de dados de Conhecimento.

    ![Configurar serviço do QnA](../media/qnamaker-how-to-create-kb/setup-qna-resource.png)

1. Insira o nome da sua base de dados de conhecimento e as fontes de dados para a nova base de dados de conhecimento.

    ![Definir fontes de dados](../media/qnamaker-how-to-create-kb/set-data-sources.png)

    - Forneça um **nome** ao serviço. Nomes duplicados e caracteres especiais são compatíveis.
    - Adicione URLs para os dados que você deseja extrair. Consulte mais informações sobre os tipos de fontes com suporte [aqui](../Concepts/data-sources-supported.md).
    - Carregue arquivos para os dados que você deseja extrair. Consulte as [informações sobre preços](https://aka.ms/qnamaker-pricing) para ver quantos documentos é possível adicionar.
    - Se você quiser adicionar manualmente QnAs, poderá ignorar a **Etapa 4** mostrada na imagem anterior.

1. Adicione **Bate-papo** à sua base de dados de conhecimento. Opte por adicionar o suporte de bate-papo ao bot escolhendo uma das três personalidades. 

    ![Adicionar bate-papo à base de dados de conhecimento ](../media/qnamaker-how-to-create-kb/create-kb-chit-chat.png)

1. Selecione **Criar sua KB**.

    ![Criar uma base de dados de conhecimento](../media/qnamaker-how-to-create-kb/create-kb.png)

1. Demora alguns minutos para os dados serem extraídos.

    ![Extração](../media/qnamaker-how-to-create-kb/hang-tight-extraction.png)

1. Quando a base de dados de conhecimento for criada com êxito, você será redirecionado para a página **Base de dados de conhecimento**.

## <a name="clean-up-resources"></a>Limpar recursos

Quando terminar de usar a base de dados de conhecimento, remova a base no portal do QnA Maker.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Adicionar personalidade ao bate-papo](./chit-chat-knowledge-base.md)
