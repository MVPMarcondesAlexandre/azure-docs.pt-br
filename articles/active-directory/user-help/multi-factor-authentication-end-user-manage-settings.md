---
title: Gerenciar configurações de verificação em duas etapas – Azure Active Directory | Microsoft Docs
description: Gerencie como usar Autenticação Multifator do Azure incluindo alterar suas informações de contato ou configurar seus dispositivos.
services: active-directory
keywords: autenticação multifator do cliente, problema de autenticação, ID de correlação
author: eross-msft
manager: daveba
ms.reviewer: richagi
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.workload: identity
ms.service: active-directory
ms.subservice: user-help
ms.topic: conceptual
ms.date: 05/23/2017
ms.author: lizross
ms.openlocfilehash: 2129b1f70ea19bdb2144f0f2a9ca4a6dbac0acbd
ms.sourcegitcommit: 415742227ba5c3b089f7909aa16e0d8d5418f7fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55766802"
---
# <a name="manage-your-settings-for-two-step-verification"></a>Gerenciar as configurações de verificação em duas etapas
Este artigo responde a perguntas sobre como atualizar as configurações de autenticação multifator ou de verificação em duas etapas. Se você estiver tendo problemas ao se conectar à sua conta, confira [Tendo problemas com a verificacão em duas etapas](multi-factor-authentication-end-user-troubleshoot.md) para a resolução de problemas.

## <a name="where-to-find-the-settings-page"></a>Onde encontrar a página de configurações
Dependendo de como a sua empresa usa a Autenticação Multifator do Azure, há alguns lugares onde você pode alterar as configurações, como o número de seu telefone.

Se o suporte da empresa envia uma URL específica ou etapas para gerenciar a verificação em duas etapas, siga as instruções. Caso contrário, as instruções a seguir devem funcionar para todos os outros. Se você seguir estas etapas, mas não vê as mesmas opções, isso significa que sua empresa ou escola personalizaram o próprio portal. Peça ao administrador o link para o portal de Autenticação Multifator do Azure.

**Vá para a página Verificação de segurança adicional**

- Vá para https://aka.ms/MFASetup.

    ![Prova](./media/multi-factor-authentication-end-user-manage-settings/proofup.png)

Se clicar nesse link não funcionar para você, você também pode acessar a página **Verificação de segurança adicional** seguindo estas etapas:

1. Entrar no [https://myapps.microsoft.com](https://myapps.microsoft.com)  

2. Selecione o nome da conta no canto superior direito e selecione **perfil**.

3. Escolha **Verificação de segurança adicional**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage-settings/myapps1.png)

4. A página de Verificação de segurança adicional carrega com suas configurações.

    ![Prova](./media/multi-factor-authentication-end-user-manage-settings/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a>Desejo alterar meu número de telefone ou adicionar um número secundário
É importante configurar um número de telefone de autenticação secundário.  Como seu número de telefone principal e seu aplicativo móvel provavelmente estão no mesmo telefone, o número de telefone secundário é a única maneira de poder retornar à sua conta caso seu telefone seja roubado ou você o perca.

> [!NOTE]
> Se você não tem acesso ao seu número de telefone principal e precisa de ajuda para entrar em sua conta, confira os o artigo [Tendo problemas com a verificação em duas etapas](multi-factor-authentication-end-user-troubleshoot.md) para obter mais ajuda.  

**Para alterar o número de telefone principal:**  

1. Na página de **Verificação de segurança** adicional, marque a caixa de texto com seu número de telefone atual e edite com o seu novo número de telefone.  
2. Clique em **Salvar**.  
3. Se este é o número que você usa para a opção de verificação preferencial, você precisa verificar o novo número antes de salvá-lo.  

**Para adicionar um número de telefone secundário:**  

1. Na página de Verificação de segurança adicional, marque a caixa ao lado de **Telefone de autenticação alternativo.**  
2. Insira o número de telefone secundário na caixa de texto.  
3. Selecione **Salvar** e suas alterações são concluídas.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Exigir verificação em duas etapas novamente em um dispositivo que você marcou como confiável

Dependendo das configurações de sua organização, uma caixa de seleção "Não pergunte novamente por **X** dias" pode ser exibida quando você executa a verificação em duas etapas em seu navegador. Se você marcar essa caixa de seleção e perder seu dispositivo ou achar que sua conta foi comprometida, restaure a verificação em duas etapas para todos os seus dispositivos.

1. Na página Verificação de segurança adicional, selecione **Restaurar autenticação multifator em dispositivos anteriormente confiáveis**.
2. Na próxima vez que você entrar em qualquer dispositivo, receberá uma solicitação para executar a verificação de duas etapas.

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a>Como limpar o Microsoft Authenticator de meu dispositivo antigo e movê-lo para um novo?
Quando você desinstala o aplicativo do dispositivo ou reinicia o dispositivo, ele não remove a ativação no back-end. Para saber mais, veja [Microsoft Authenticator](user-help-auth-app-download-install.md).

## <a name="next-steps"></a>Próximas etapas
* Obter dicas de solução de problemas e ajuda em [Tendo problemas com a verificação em duas etapas](multi-factor-authentication-end-user-troubleshoot.md)
* Configure [senhas de aplicativo](multi-factor-authentication-end-user-app-passwords.md) para quaisquer aplicativos que não dão suporte à verificação em duas etapas.
