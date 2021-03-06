---
title: Gerenciar permissões aos recursos por usuário no Azure Stack (administrador de serviços e locatário) | Microsoft Docs
description: Como um administrador de serviços ou Locatário, saiba como gerenciar permissões de RBAC.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/14/2019
ms.author: mabrigg
ms.reviewer: thoroet
ms.lastreviewed: 01/14/2019
ms.openlocfilehash: f20cd877e4cc53490016d251c5bdb343ab0cb4b0
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55250326"
---
# <a name="manage-role-based-access-control"></a>Gerenciar o controle de acesso baseado em função

*Aplica-se a: Integrados do Azure Stack, sistemas e o Kit de desenvolvimento do Azure Stack*

Um usuário do Azure Stack pode ser um leitor, proprietário ou colaborador para cada instância de uma assinatura, um grupo de recursos ou serviço. Por exemplo, o usuário A pode ter permissões de leitura para uma assinatura, mas ter permissões de proprietário para sete de máquina Virtual.

 - Leitor: Usuário pode ver tudo, mas não é possível fazer alterações.
 - Colaborador: Usuário pode gerenciar tudo, exceto o acesso aos recursos.
 - Proprietário: Usuário pode gerenciar tudo, incluindo o acesso aos recursos.

## <a name="set-access-permissions-for-a-user"></a>Definir permissões de acesso para um usuário

1. Entre com uma conta que tenha permissões de proprietário ao recurso que deseja gerenciar.
2. Na folha do recurso, clique o **acesso** ícone ![](media/azure-stack-manage-permissions/image1.png).
3. No **os usuários** folha, clique em **funções**.
4. No **funções** folha, clique em **Add** para adicionar permissões para o usuário.

## <a name="set-access-permissions-for-a-universal-group"></a>Definir permissões de acesso para um grupo universal 

> [!Note]  
Aplicável somente ao Active Directory Federated Services (AD FS).

1. Entre com uma conta que tenha permissões de proprietário ao recurso que deseja gerenciar.
2. Na folha do recurso, clique o **acesso** ícone ![](media/azure-stack-manage-permissions/image1.png).
3. No **os usuários** folha, clique em **funções**.
4. No **funções** folha, clique em **Add** adicionar permissões para Universal grupo grupo do Active Directory.

## <a name="next-steps"></a>Próximas etapas
[Adicionar um locatário do Azure Stack](azure-stack-add-new-user-aad.md)

