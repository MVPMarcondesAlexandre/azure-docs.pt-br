---
title: Como remover o acesso de um usuário a um aplicativo | Microsoft Docs
description: Compreenda como remover o acesso de um usuário a um aplicativo
services: active-directory
documentationcenter: ''
author: barbkess
manager: daveba
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/17/2018
ms.author: barbkess
ms.openlocfilehash: 00f0df4612fe523b8b585bc2c9458386422256e8
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55180493"
---
# <a name="how-to-remove-a-users-access-to-an-application"></a>Como remover o acesso de um usuário a um aplicativo

Este artigo ajuda-lhe a compreender como remover o acesso de um usuário a um aplicativo.

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a>Quero remover a atribuição de um usuário ou grupo específico para um aplicativo

Para remover uma atribuição de um usuário ou grupo a um aplicativo, siga as etapas listadas no artigo [Remover uma atribuição de usuário ou grupo de um aplicativo empresarial no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a>Quero desabilitar todo o acesso a um aplicativo para todos os usuários

Para desabilitar todos os logons de usuário em um aplicativo, siga as etapas listadas no artigo [Desabilitar logons de usuário para um aplicativo empresarial no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).

## <a name="i-want-to-delete-an-application-entirely"></a>Quero excluir um aplicativo completamente

Para **excluir um aplicativo**, siga estas instruções:

1.  Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**

2.  Abra a **Extensão do Azure Active Directory** clicando em **Todos os serviços** na parte superior do menu de navegação esquerdo principal.

3.  Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.

4.  Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.

5.  Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.

   * Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**

6.  Selecione o aplicativo que deseja excluir.

7.  Após o carregamento do aplicativo, clique no ícone **Excluir** do painel **Visão Geral** do aplicativo.

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a>Quero desabilitar todas as futuras operações de consentimento do usuário para qualquer aplicativo

Desabilitar o consentimento do usuário para todo o seu diretório impede que os usuários finais consintam com qualquer aplicativo. Os administradores ainda podem consentir em nome dos usuários. Para obter mais informações sobre o consentimento de aplicativos e por que você pode ou não querer fazer isso, leia [Understanding user and admin consent](../develop/howto-convert-app-to-be-multi-tenant.md#understand-user-and-admin-consent) (Noções básicas sobre o consentimento do usuário e do administrador). Confira também, [Permissões e consentimento](../develop/v2-permissions-and-consent.md).

Para **desabilitar todas as futuras operações de consentimento do usuário no diretório inteiro**, siga estas instruções:

1.  Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Abra a **Extensão do Azure Active Directory** 

3.  Clique em **Aplicativos empresariais** no menu de navegação.

5.  Clique em **Configurações de usuário**.

6.  Defina a alternância de **Usuários podem permitir que aplicativos acessem dados empresariais em seu nome** como **Não** e clique no botão Salvar.


## <a name="next-steps"></a>Próximas etapas

[Gerenciamento do acesso aos aplicativos](what-is-access-management.md)
