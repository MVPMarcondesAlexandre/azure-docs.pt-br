---
title: Como exibir a entidade de serviço de uma identidade gerenciada usando o PowerShell
description: Instruções passo a passo para exibir a entidade de serviço de uma identidade gerenciada usando o PowerShell.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: daveba
editor: ''
ms.service: active-directory
ms.subservice: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/29/2018
ms.author: priyamo
ms.openlocfilehash: 8c406dda1d6ce0fe7b73f400444d7bcd8a9e8400
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55185951"
---
# <a name="view-the-service-principal-of-a-managed-identity-using-powershell"></a>Exibir a entidade de serviço de uma identidade gerenciada usando o PowerShell

As identidades gerenciadas dos recursos do Azure fornecem aos serviços do Azure uma identidade gerenciada automaticamente no Azure Active Directory. Você pode usar essa identidade para autenticar em qualquer serviço que dá suporte à autenticação do Azure AD, incluindo o Key Vault, sem ter as credenciais no seu código. 

Neste artigo, você aprende a exibir a entidade de serviço de uma identidade gerenciada usando o PowerShell.

[!INCLUDE [az-powershell-update](../../../includes/updated-for-az.md)]

## <a name="prerequisites"></a>Pré-requisitos

- Se você não estiver familiarizado com identidades gerenciadas para recursos do Azure, confira a [seção de visão geral](overview.md).
- Caso ainda não tenha uma conta do Azure, [inscreva-se para obter uma conta gratuita](https://azure.microsoft.com/free/).
- Habilite a [identidade designada pelo sistema em uma máquina virtual](/azure/active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm#system-assigned-managed-identity) ou [aplicativo](/azure/app-service/overview-managed-identity#adding-a-system-assigned-identity).
- Instale a versão mais recente do [Azure PowerShell](/powershell/azure/install-az-ps)

## <a name="view-the-service-principal"></a>Exibir a entidade de serviço

O comando a seguir demonstra como exibir a entidade de serviço de um aplicativo ou VM com identidade atribuída pelo sistema habilitada. Substitua `<VM or application name>` pelos seus próprios valores.

```PowerShell
Get-AzADServicePrincipal -DisplayName <VM or application name>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como exibir entidades de serviço do Azure AD usando o PowerShell, confira [Get-AzADServicePrincipal](/powershell/module/az.resources/get-azadserviceprincipal).


