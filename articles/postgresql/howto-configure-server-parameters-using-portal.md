---
title: Configurar os parâmetros do servidor no Banco de Dados do Azure para PostgreSQL por meio do Portal do Azure
description: Este artigo descreve como configurar os parâmetros de servidor disponíveis no Banco de Dados do Azure para PostgreSQL usando o portal do Azure.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 02/28/2018
ms.openlocfilehash: 0d0626c48ecebdead604aab93ab0602c698d0d77
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2018
ms.locfileid: "53540530"
---
# <a name="configure-server-parameters-in-azure-portal"></a>Configure parâmetros de servidor no Portal do Azure
Você pode listar, exibir e atualizar os parâmetros de configuração de um Banco de Dados do Azure para servidor PostgreSQL via portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Para seguir este guia de instruções, você precisa:
- [Servidor do Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="viewing-and-editing-parameters"></a>Exibir e editar parâmetros
1. Abra o [Portal do Azure](https://portal.azure.com).

2. Selecione seu servidor de Banco de Dados do Azure para PostgreSQL.

3. Sob a seção **configurações**, selecione **parâmetros de servidor**. A página mostra uma lista de parâmetros, valores e descrições.
![Página de visão geral de parâmetros](./media/howto-configure-server-parameters-in-portal/3-overview-of-parameters.png)

4. Selecione o botão **suspenso** para ver os possíveis valores para parâmetros de tipo enumerado como client_min_messages.
![Enumerar a lista suspensa](./media/howto-configure-server-parameters-in-portal/4-enum-drop-down.png)

5. Selecione ou passe o mouse sobre o botão **i** (informações) para ver o intervalo de valores possíveis para parâmetros numéricos como cpu_index_tuple_cost.
![Botão informação](./media/howto-configure-server-parameters-in-portal/4-information-button.png)

6. Se necessário, use a **caixa de pesquisa** para restringir rapidamente a um parâmetro específico. A busca está no nome e na descrição dos parâmetros.
![Pesquisar resultados](./media/howto-configure-server-parameters-in-portal/5-search.png)

7. Altere os valores de parâmetro que você deseja ajustar. Todas as alterações feitas nessa sessão são realçadas em roxo. Depois de alterar os valores, você pode selecionar **Salvar**. Ou então, você pode **Descartar** suas alterações.
![Clique em salvar ou descartar mudanças](./media/howto-configure-server-parameters-in-portal/6-save-and-discard-buttons.png)

8. Se você tiver salvo os novos valores para os parâmetros, você sempre pode reverter tudo o que fazer com os valores padrão selecionando **Redefinir tudo para o padrão**.
![Redefinir tudo para padrão](./media/howto-configure-server-parameters-in-portal/7-reset-to-default-button.png)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre:
- [Visão geral dos parâmetros do servidor no Banco de Dados do Azure para PostgreSQL](concepts-servers.md)
- [Configurando parâmetros usando a CLI do Azure](howto-configure-server-parameters-using-cli.md)
