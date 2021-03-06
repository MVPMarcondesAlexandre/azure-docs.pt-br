---
title: Como configurar a política de registro de autenticação multifator no Azure Active Directory Identity Protection| Microsoft Docs
description: Saiba como configurar a política de registro de autenticação multifator do Azure AD Identity Protection.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança
documentationcenter: ''
author: MarkusVi
manager: daveba
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.subservice: identity-protection
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/13/2018
ms.author: markvi
ms.reviewer: raluthra
ms.openlocfilehash: ed1104d3e5ddf54657fb1f7b5c84a85ea855d95c
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55148568"
---
# <a name="how-to-configure-the-multi-factor-authentication-registration-policy"></a>Como: configurar a política de registro de autenticação multifator

O Azure AD Identity Protection ajuda a gerenciar a implementação do registro de MFA (autenticação multifator) configurando uma política. Este artigo explica para o que a política pode ser usada e como configurá-la.

## <a name="what-is-the-multi-factor-authentication-registration-policy"></a>O que é a política de registro de autenticação multifator?

A autenticação multifator do Azure é um método de verificar quem você é e que requer o uso de mais do que apenas um nome de usuário e uma senha. Ele fornece uma segunda camada de segurança para logons de usuário e transações.  

Recomendamos exigir a autenticação multifator do Azure para entradas de usuário porque:

- fornece autenticação forte com uma variedade de opções de verificação fácil

- desempenha um papel fundamental na preparação de sua organização para proteger e recuperar comprometimentos de conta


Para obter mais detalhes, veja [O que é a Autenticação Multifator do Azure?](../authentication/multi-factor-authentication.md)


## <a name="how-do-i-access-the-mfa-registration-policy"></a>Como fazer para acessar a política de registro de MFA?
   
A política de risco de MFA encontra-se na seção **Configurar** na página do [Azure AD Identity Protection](https://portal.azure.com/#blade/Microsoft_AAD_ProtectionCenter/IdentitySecurityDashboardMenuBlade/SignInPolicy).
   
![Política do MFA](./media/howto-mfa-policy/1014.png)




## <a name="policy-settings"></a>Configurações de política

Ao configurar a política de risco de entrada, será necessário definir:

- Os usuários e grupos aos quais a política se aplica:

    ![Usuários e grupos](./media/howto-mfa-policy/11.png)

- O tipo de acesso que você deseja impor:  

    ![Usuários e grupos](./media/howto-mfa-policy/12.png)

- O estado da sua política:

    ![Impor a política](./media/howto-mfa-policy/14.png)


A caixa de diálogo de configuração de política fornece uma opção para estimar o impacto da sua configuração.

![Impacto estimado](./media/howto-mfa-policy/15.png)




## <a name="user-experience"></a>Experiência do usuário


Para obter uma visão geral da experiência do usuário relacionada, confira:

* [Fluxo do registro de autenticação multifator](flows.md#multi-factor-authentication-registration).  
* [Experiências de entrada com o Azure AD Identity Protection](flows.md).  



## <a name="next-steps"></a>Próximas etapas

Para obter uma visão geral do Azure AD Identity Protection, veja a [Visão geral do Azure AD Identity Protection](overview.md).
