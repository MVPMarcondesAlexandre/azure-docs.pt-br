---
title: Elevar o acesso para gerenciar todas as assinaturas e grupos de gerenciamento do Azure | Microsoft Docs
description: Descreve como elevar o acesso para um Administrador Global gerenciar todas as assinaturas e grupos de gerenciamento no Azure Active Directory usando a API REST ou o portal do Azure.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: bagovind
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: role-based-access-control
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2019
ms.author: rolyon
ms.reviewer: bagovind
ms.openlocfilehash: 7552018c32078295c164023f909a604c6522c32f
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54437463"
---
# <a name="elevate-access-to-manage-all-azure-subscriptions-and-management-groups"></a>Elevar o acesso para gerenciar todas as assinaturas e grupos de gerenciamento do Azure

Como um Administrador Global no Azure AD (Azure Active Directory), talvez você não tenha acesso a todas as assinaturas e grupos de gerenciamento em seu diretório. Este artigo descreve maneiras de elevar o acesso para todas as assinaturas e grupos de gerenciamento.

[!INCLUDE [gdpr-dsr-and-stp-note](../../includes/gdpr-dsr-and-stp-note.md)]

## <a name="why-would-you-need-to-elevate-your-access"></a>Por que você precisa elevar o acesso?

Se você for um Administrador Global, poderá haver ocasiões em que você queira fazer o seguinte:

- Recuperar o acesso a um grupo de gerenciamento ou assinatura do Azure quando um usuário tiver perdido o acesso
- Conceder a outro usuário ou a você mesmo acesso a uma assinatura ou grupo de gerenciamento do Azure
- Ver todas as assinaturas ou grupos de gerenciamento do Azure em uma organização
- Permitir o acesso de um aplicativo de automação (como um aplicativo de faturamento ou de auditoria) a todas as assinaturas do Azure ou grupos de gerenciamento

## <a name="how-does-elevate-access-work"></a>Como elevar um trabalho de acesso?

Os recursos do Azure AD e do Azure são protegidos independentemente um do outro. Ou seja, as atribuições de função do Azure AD não concedem acesso aos recursos do Azure, e as atribuições de função do Azure não concedem acesso ao Azure AD. No entanto, se você for um [Administrador Global](../active-directory/users-groups-roles/directory-assign-admin-roles.md#company-administrator) no Azure AD, poderá atribuir a si mesmo acesso a todas as assinaturas e grupos de gerenciamento do Azure em seu diretório. Use esse recurso se você não tiver acesso aos recursos do Azuresubscription, como máquinas virtuais ou contas de armazenamento, e quiser usar o privilégio de administrador global para obter acesso a esses recursos.

Quando você elevar seu acesso, você receberá a função [Administrador de Acesso do Usuário](built-in-roles.md#user-access-administrator) no Azure no escopo da raiz (`/`). Isso permite que você visualize todos os recursos e atribua acesso a qualquer assinatura ou grupo de gerenciamento no diretório. As atribuições de função do Administrador de Acesso do Usuário podem ser removidas usando o PowerShell.

Você deve remover esse acesso elevado depois de fazer as alterações necessárias no escopo raiz.

![Elevar o acesso](./media/elevate-access-global-admin/elevate-access.png)

## <a name="azure-portal"></a>Portal do Azure

Siga estas etapas para elevar o acesso de um administrador global usando o portal do Azure.

1. Faça login no [Portal do Azure](https://portal.azure.com) ou no [centro de administração do Active Directory do Azure](https://aad.portal.azure.com) como Administrador Global.

1. Na lista de navegação, clique em **Azure Active Directory**, depois clique em **Propriedades**.

   ![Azure Active Directory – captura de tela](./media/elevate-access-global-admin/aad-properties.png)

1. Em **Gerenciamento de acesso para recursos do Azure**, defina a alternância como **Sim**.

   ![Gerenciamento de acesso para recursos do Azure - captura de tela](./media/elevate-access-global-admin/aad-properties-global-admin-setting.png)

   Quando você define a alternância como **Sim**, recebe a função de Administrador do Acesso do Usuário no RBAC do Azure no escopo raiz (/). Isso concede a você permissão para atribuir funções a todas as assinaturas e grupos de gerenciamento do Azure associados a esse diretório do AD do Azure. Essa alternância está disponível apenas para usuários com a função de administrador global no Azure AD.

   Quando você define a alternância como **Não**, a função Administrador de Acesso do Usuário no RBAC do Azure é removida da sua conta de usuário. Você não pode mais atribuir funções a todas as assinaturas e grupos de gerenciamento do Azure associados a esse diretório do AD do Azure. Você pode exibir e gerenciar somente as assinaturas do Azure e os grupos de gerenciamento aos quais você recebeu acesso.

1. Clique em **Salvar**, para salvar suas configurações.

   Essa configuração não é uma propriedade global, aplicando-se somente ao usuário conectado no momento. Você não pode elevar o acesso para todos os membros da função de Administrador Global.

1. Saia e entre novamente para atualizar o seu acesso.

    Agora você deve ter acesso a todas as assinaturas e grupos de gerenciamento em seu diretório. Você observará que você foi atribuído à função de Administrador de Acesso do Usuário no escopo de raiz.

   ![Atribuições de função de assinatura com escopo de raiz – captura de tela](./media/elevate-access-global-admin/iam-root.png)

1. Faça as alterações que você precisa fazer no acesso com privilégios elevados.

    Para obter informações sobre como atribuir funções, veja [Gerenciar o acesso usando o portal do Azure e o RBAC](role-assignments-portal.md). Se você estiver usando o Azure AD PIM (Privileged Identity Management), veja [Descobrir recursos do Azure para gerenciar no PIM](../active-directory/privileged-identity-management/pim-resource-roles-discover-resources.md) ou [Atribuir funções de recurso do Azure no PIM](../active-directory/privileged-identity-management/pim-resource-roles-assign-roles.md).

1. Ao terminar, defina a alternância **Gerenciamento de acesso para recursos do Azure** de voltar como **Não**. Como essa é uma configuração por usuário, você deve estar conectado como o mesmo usuário que foi usado para elevar o acesso.

## <a name="azure-powershell"></a>Azure PowerShell

### <a name="list-role-assignment-at-the-root-scope-"></a>Listar atribuição de função no escopo raiz (/)

Para listar a atribuição de função de Administrador de Acesso do Usuário para um usuário no escopo raiz (`/`), use o comando [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment).

```azurepowershell
Get-AzureRmRoleAssignment | where {$_.RoleDefinitionName -eq "User Access Administrator" `
  -and $_.SignInName -eq "<username@example.com>" -and $_.Scope -eq "/"}
```

```Example
RoleAssignmentId   : /providers/Microsoft.Authorization/roleAssignments/098d572e-c1e5-43ee-84ce-8dc459c7e1f0
Scope              : /
DisplayName        : username
SignInName         : username@example.com
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : d65fd0e9-c185-472c-8f26-1dafa01f72cc
ObjectType         : User
CanDelegate        : False
```

### <a name="remove-a-role-assignment-at-the-root-scope-"></a>Remover uma atribuição de função no escopo raiz (/)

Para remover uma atribuição de função de Administrador de Acesso do Usuário para usuário no escopo de raiz (`/`), siga estas etapas.

1. Entre como um usuário que possa remover o acesso com privilégios elevados. Esse pode ser o mesmo usuário que foi usado para elevar o acesso ou outro Administrador Global com acesso elevado no escopo de raiz.


1. Use o comando [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment) para remover a atribuição de função de Administrador de Acesso do Usuário.

    ```azurepowershell
    Remove-AzureRmRoleAssignment -SignInName <username@example.com> `
      -RoleDefinitionName "User Access Administrator" -Scope "/"
    ```

## <a name="rest-api"></a>API REST

### <a name="elevate-access-for-a-global-administrator"></a>Elevar o acesso de um administrador global

Use as etapas básicas a seguir para elevar o acesso de um Administrador global usando a API REST.

1. Usando a REST, chame `elevateAccess`, que lhe concede a função de Administrador de Acesso do Usuário no escopo raiz (`/`).

   ```http
   POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
   ```

1. Crie uma [atribuição de função](/rest/api/authorization/roleassignments) para atribuir qualquer função em qualquer escopo. O exemplo a seguir mostra as propriedades para atribuir a função {roleDefinitionID} no escopo raiz (`/`):

   ```json
   { 
     "properties": {
       "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionID}",
       "principalId": "{objectID}",
       "scope": "/"
     },
     "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
     "type": "Microsoft.Authorization/roleAssignments",
     "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
   }
   ```

1. Enquanto Administrador de Acesso do Usuário, você também pode remover atribuições de função no escopo raiz (`/`).

1. Remova seus privilégios de Administrador de Acesso do Usuário até que sejam necessários novamente.

### <a name="list-role-assignments-at-the-root-scope-"></a>Listar atribuições de função no escopo raiz (/)

Você pode listar todas as atribuições de função para um usuário no escopo raiz (`/`).

- Chame [GET roleAssignments](/rest/api/authorization/roleassignments/listforscope), em que `{objectIdOfUser}` é a ID de objeto do usuário cujas atribuições de função que você deseja recuperar.

   ```http
   GET https://management.azure.com/providers/Microsoft.Authorization/roleAssignments?api-version=2015-07-01&$filter=principalId+eq+'{objectIdOfUser}'
   ```

### <a name="list-deny-assignments-at-the-root-scope-"></a>Listar atribuições de negação no escopo raiz (/)

É possível listar todas as atribuições de negação para um usuário no escopo raiz (`/`).

- Chame GET denyAssignments, em que `{objectIdOfUser}` é a ID de objeto do usuário cujas atribuições de negação você deseja recuperar.

   ```http
   GET https://management.azure.com/providers/Microsoft.Authorization/denyAssignments?api-version=2018-07-01-preview&$filter=gdprExportPrincipalId+eq+'{objectIdOfUser}'
   ```

### <a name="remove-elevated-access"></a>Remover acesso elevado

Ao chamar `elevateAccess`, você cria uma atribuição de função para si mesmo, de modo que, para revogar esses privilégios, é preciso remover a atribuição.

1. Chame [GET roleDefinitions](/rest/api/authorization/roledefinitions/get), em que `roleName` é igual a Administrador de Acesso do Usuário, para determinar a ID do nome da função de Administrador de Acesso do Usuário.

    ```http
    GET https://management.azure.com/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01&$filter=roleName+eq+'User Access Administrator'
    ```

    ```json
    {
      "value": [
        {
          "properties": {
        "roleName": "User Access Administrator",
        "type": "BuiltInRole",
        "description": "Lets you manage user access to Azure resources.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "*/read",
              "Microsoft.Authorization/*",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "0001-01-01T08:00:00.0000000Z",
        "updatedOn": "2016-05-31T23:14:04.6964687Z",
        "createdBy": null,
        "updatedBy": null
          },
          "id": "/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
          "type": "Microsoft.Authorization/roleDefinitions",
          "name": "18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"
        }
      ],
      "nextLink": null
    }
    ```

    Salve a ID do parâmetro `name`, nesse caso: `18d7d88d-d35e-4fb5-a5c3-7773c20a72d9`.

2. Você também precisa listar a atribuição de função para o administrador de diretório no escopo do diretório. Listar todas as atribuições no escopo de diretório para o `principalId` do administrador de diretório que fez a chamada de acesso elevar. Isso listará todas as atribuições no diretório para o objectid.

    ```http
    GET https://management.azure.com/providers/Microsoft.Authorization/roleAssignments?api-version=2015-07-01&$filter=principalId+eq+'{objectid}'
    ```
    
    >[!NOTE] 
    >Um administrador de diretório não deve ter muitas atribuições, se a consulta anterior retornar muitas atribuições, você também pode consultar todas as atribuições apenas no nível do escopo do diretório e, em seguida, filtrar os resultados: `GET https://management.azure.com/providers/Microsoft.Authorization/roleAssignments?api-version=2015-07-01&$filter=atScope()`
        
    2. As chamadas anteriores retornam uma lista de atribuições de função. Encontre a atribuição de função em que o escopo é `"/"` e o `roleDefinitionId` termina com o ID do nome da função que você encontrou na etapa 1 e `principalId` corresponde ao objectId do administrador de diretório. 
    
    Atribuição de função de amostra:

        ```json
        {
          "value": [
            {
              "properties": {
                "roleDefinitionId": "/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
                "principalId": "{objectID}",
                "scope": "/",
                "createdOn": "2016-08-17T19:21:16.3422480Z",
                "updatedOn": "2016-08-17T19:21:16.3422480Z",
                "createdBy": "93ce6722-3638-4222-b582-78b75c5c6d65",
                "updatedBy": "93ce6722-3638-4222-b582-78b75c5c6d65"
              },
              "id": "/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
              "type": "Microsoft.Authorization/roleAssignments",
              "name": "e7dd75bc-06f6-4e71-9014-ee96a929d099"
            }
          ],
          "nextLink": null
        }
        ```
        
    Novamente, salve a ID do parâmetro `name`, nesse caso: e7dd75bc-06f6-4e71-9014-ee96a929d099.

    3. Por fim, use a ID da atribuição de função para remover a atribuição adicionada por `elevateAccess`:

    ```http
    DELETE https://management.azure.com/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099?api-version=2015-07-01
    ```

## <a name="next-steps"></a>Próximas etapas

- [Entender as diferentes funções](rbac-and-directory-admin-roles.md)
- [Controle de acesso baseado em função com REST](role-assignments-rest.md)
