---
title: 'Azure AD Connect: Autenticação de passagem – Atualização de agentes de autenticação | Microsoft Docs'
description: Este artigo descreve como atualizar sua configuração da Autenticação de passagem do Azure AD (Azure Active Directory).
services: active-directory
keywords: Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único
documentationcenter: ''
author: billmath
manager: daveba
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/27/2018
ms.subservice: hybrid
ms.author: billmath
ms.custom: seohack1
ms.openlocfilehash: 3243f1956b2d373a20aa3aac8171678190f6ffbf
ms.sourcegitcommit: 5978d82c619762ac05b19668379a37a40ba5755b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55492939"
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Autenticação de passagem do Azure Active Directory: Fazer upgrade da versão prévia dos Agentes de Autenticação

## <a name="overview"></a>Visão geral

Este artigo é para clientes que usam a Autenticação de passagem do Azure AD por meio da versão prévia. Nós recentemente atualizamos (e remodelamos) o software do Agente de autenticação. Você precisa atualizar _manualmente_ os Agentes de autenticação da versão prévia instalados nos seus servidores locais. Esta atualização manual é uma ação que deve ser realizada uma única vez. Todas as atualizações futuras dos Agentes de autenticação serão automáticas. Os motivos para atualizar são os seguintes:

- As versões prévias dos Agentes de autenticação não receberão mais correções de segurança ou de bugs.
-   As versões prévias dos Agentes de autenticação não podem ser instaladas em servidores adicionais para obter alta disponibilidade.

## <a name="check-versions-of-your-authentication-agents"></a>Verificar as versões dos seus Agentes de autenticação

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Etapa 1: Verificar o local em que os Agentes de autenticação estão instalados

Siga essas etapas para verificar o local em que os Agentes de autenticação estão instalados:

1. Entre no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) com as credenciais do Administrador Global do seu locatário.
2. Selecione **Azure Active Directory** na navegação à esquerda.
3. Selecione **Azure AD Connect**. 
4. Selecione **Autenticação de passagem**. Essa folha lista os servidores em que os Agentes de autenticação estão instalados.

![Centro de administração do Azure Active Directory - folha Autenticação de Passagem](./media/how-to-connect-pta-upgrade-preview-authentication-agents/pta8.png)

### <a name="step-2-check-the-versions-of-your-authentication-agents"></a>Etapa 2: Verificar as versões dos Agentes de autenticação

Para verificar as versões dos seus Agentes de autenticação em cada servidor identificado na etapa anterior, siga estas instruções:

1. Acesse **Painel de controle -> Programas -> Programas e recursos** no servidor local.
2. Se houver uma entrada para "**Agente de autenticação do Microsoft Azure AD Connect**", você não precisará realizar nenhuma ação nesse servidor.
3. Se houver uma entrada para "**Conector de Proxy de Aplicativo do Microsoft Azure AD**", você precisará atualizar manualmente nesse servidor.

![Versão prévia do Agente de autenticação](./media/how-to-connect-pta-upgrade-preview-authentication-agents/pta6.png)

## <a name="best-practices-to-follow-before-starting-the-upgrade"></a>Melhores práticas a serem seguidas antes de iniciar a atualização

Antes de atualizar, verifique se você tem os seguintes itens no lugar:

1. **Criar conta de administrador global somente em nuvem**: não faça upgrade sem ter uma conta de administrador global somente em nuvem para ser usada em situações de emergência em que seus Agentes de Autenticação de Passagem não estejam funcionando adequadamente. Saiba mais sobre [adicionar uma conta de Administrador Global somente de nuvem](../active-directory-users-create-azure-portal.md). A realização dessa etapa é fundamental e garante que você não ficará bloqueado do seu locatário.
2.  **Garantir a alta disponibilidade**: se não tiver concluído anteriormente, instale um segundo Agente de Autenticação autônomo para fornecer uma alta disponibilidade para solicitações de entrada, usando estas [instruções](how-to-connect-pta-quick-start.md#step-4-ensure-high-availability).

## <a name="upgrading-the-authentication-agent-on-your-azure-ad-connect-server"></a>Atualizando o Agente de autenticação no servidor do Azure AD Connect

Você precisa atualizar o Azure AD Connect antes de atualizar o Agente de autenticação no mesmo servidor. Siga estas etapas em seus servidores primários e de preparo do Azure AD Connect:

1. **Atualizar o Azure AD Connect**: Siga as etapas deste [artigo](how-to-upgrade-previous-version.md) e faça a atualização para a versão mais recente do Azure AD Connect.
2. **Desinstale a versão prévia do Agente de Autenticação**: Faça o download [deste script do PowerShell](https://aka.ms/rmpreviewagent) e execute-o como Administrador no servidor.
3. **Faça o download da versão mais recente do Agente de Autenticação (versão 1.5.389.0 ou posteriores)**: Entre no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) com as credenciais do administrador global do seu locatário. Selecione **Azure Active Directory -> Azure AD Connect -> Autenticação de passagem -> Baixar agente**. Aceite os [termos de serviço](https://aka.ms/authagenteula) e baixe a versão mais recente do Agente de autenticação. Você também pode baixar o Agente de Autenticação [aqui](https://aka.ms/getauthagent).
4. **Instale a versão mais recente do Agente de Autenticação**: Execute o arquivo executável baixado na Etapa 3. Forneça as suas credenciais de Administrador Global do locatário quando solicitado.
5. **Verifique se a versão mais recente foi instalada**: conforme mostrado anteriormente, acesse **Painel de Controle -> Programas -> Programas e Recursos** e verifique se há uma entrada para "**Agente de Autenticação do Microsoft Azure AD Connect**".

>[!NOTE]
>Se você verificar a folha Autenticação de Passagem no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) após a conclusão das etapas anteriores, verá duas entradas do Agente de Autenticação por servidor - uma entrada mostrando o Agente de Autenticação como **Ativo** e o outro como **Inativo**. Isso é _esperado_. A entrada **Inativo** é descartada automaticamente depois de alguns dias.

## <a name="upgrading-the-authentication-agent-on-other-servers"></a>Atualizar o Agente de autenticação em outros servidores

Siga estas etapas para atualizar os Agentes de autenticação em outros servidores (em que o Azure AD Connect não está instalado):

1. **Desinstale a versão prévia do Agente de Autenticação**: Faça o download [deste script do PowerShell](https://aka.ms/rmpreviewagent) e execute-o como Administrador no servidor.
2. **Faça o download da versão mais recente do Agente de Autenticação (versão 1.5.389.0 ou posteriores)**: Entre no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) com as credenciais do administrador global do seu locatário. Selecione **Azure Active Directory -> Azure AD Connect -> Autenticação de passagem -> Baixar agente**. Aceite os termos do serviço e baixe a versão mais recente.
3. **Instale a versão mais recente do Agente de Autenticação**: Execute o arquivo executável baixado na Etapa 2. Forneça as suas credenciais de Administrador Global do locatário quando solicitado.
4. **Verifique se a versão mais recente foi instalada**: conforme mostrado anteriormente, acesse **Painel de Controle -> Programas -> Programas e Recursos** e verifique se há uma entrada para **Agente de Autenticação do Microsoft Azure AD Connect**.

>[!NOTE]
>Se você verificar a folha Autenticação de Passagem no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) após a conclusão das etapas anteriores, verá duas entradas do Agente de Autenticação por servidor - uma entrada mostrando o Agente de Autenticação como **Ativo** e o outro como **Inativo**. Isso é _esperado_. A entrada **Inativo** é descartada automaticamente depois de alguns dias.

## <a name="next-steps"></a>Próximas etapas
- [**Solução de problemas**](tshoot-connect-pass-through-authentication.md) – Saiba como resolver problemas comuns do recurso.
