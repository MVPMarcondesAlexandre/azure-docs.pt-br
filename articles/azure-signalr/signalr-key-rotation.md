---
title: Rotação de chaves de acesso para o Serviço do Azure SignalR
description: Uma visão geral sobre o motivo pelo qual o cliente precisa girar as chaves de acesso de forma rotineira e como fazer isso com a GUI do portal do Azure e a CLI do Azure.
author: sffamily
ms.service: signalr
ms.topic: overview
ms.date: 09/13/2018
ms.author: zhshang
ms.openlocfilehash: 04321e62ea41b58e9ee4314b600c77e6c39b7ade
ms.sourcegitcommit: 3ab534773c4decd755c1e433b89a15f7634e088a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2019
ms.locfileid: "54065827"
---
# <a name="access-key-rotation-for-azure-signalr-service"></a>Rotação de chaves de acesso para o Serviço do Azure SignalR

Cada instância do Serviço do Azure SignalR tem um par de chaves de acesso chamadas chaves Primária e Secundária. Elas são usadas para autenticar clientes do SignalR ao fazer solicitações para o serviço. As chaves são associadas à URL de ponto de extremidade da instância. Proteja suas chaves e gire-as regularmente. Você recebe duas chaves de acesso, de modo que possa manter conexões usando uma chave enquanto regenera a outra.

## <a name="why-rotate-access-keys"></a>Por que girar as chaves de acesso?

Por razões de segurança e requisitos de conformidade, gire rotineiramente as chaves de acesso.

## <a name="regenerate-access-keys"></a>Regenerar chaves de acesso

1. Vá para o [portal do Azure](https://portal.azure.com/) e entre com suas credenciais.

1. Encontre a seção **Chaves** na instância do Serviço do Azure SignalR com as chaves que você deseja regenerar.

1. Selecione **Chaves** no menu de navegação.

1. Selecione **Regenerar Chave Primária** ou **Regenerar Chave Secundária**.

   Uma nova chave e a cadeia de conexão correspondente serão criadas e exibidas.

   ![Regenerar chaves](media/signalr-key-rotation/regenerate-keys.png)

Você também pode regenerar chaves usando a [CLI do Azure](/cli/azure/ext/signalr/signalr/key?view=azure-cli-latest#ext-signalr-az-signalr-key-renew).

## <a name="update-configurations-with-new-connection-strings"></a>Atualizar configurações com novas cadeias de conexão

1. Copie a cadeia de conexão recém-gerada.

1. Atualize todas as configurações para que usem a nova cadeia de conexão.

1. Reinicie o aplicativo, conforme necessário.

## <a name="forced-access-key-regeneration"></a>Regeneração forçada de chaves de acesso

O Serviço do Azure SignalR pode impor uma regeneração obrigatória de chaves de acesso em determinada situação. O serviço notifica os clientes por email e pela notificação no portal. Se você receber essa comunicação ou se houver uma falha do serviço devido à chave de acesso, gire as chaves seguindo as instruções neste guia.

## <a name="next-steps"></a>Próximas etapas

Como uma boa prática de segurança, gire suas chaves de acesso regularmente.

Neste guia, você aprendeu a regenerar as chaves de acesso. Continue para os próximos tutoriais sobre autenticação com o OAuth ou o Azure Functions.

> [!div class="nextstepaction"]
> [Integração com o ASP.NET Core Identity](./signalr-authenticate-oauth.md)

> [!div class="nextstepaction"]
> [Criar um aplicativo em tempo real sem servidor com a autenticação](./signalr-authenticate-azure-functions.md)