---
title: Criar e publicar um aplicativo gerenciado do catálogo de serviços do Azure | Microsoft Docs
description: Mostra como criar um aplicativo gerenciado do Azure destinado aos membros de sua organização.
services: managed-applications
author: tfitzmac
ms.service: managed-applications
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.date: 10/04/2018
ms.author: tomfitz
ms.openlocfilehash: 7e9db85fb91dd0c9a33cc8205bdb30a648dfd38a
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54438726"
---
# <a name="create-and-publish-a-managed-application-definition"></a>Criar e publicar uma definição de aplicativo gerenciado

Crie e publique [aplicativos gerenciados](overview.md) do Azure destinados aos membros de sua organização. Por exemplo, um departamento de TI pode publicar aplicativos gerenciados que atendem aos padrões organizacionais. Esses aplicativos gerenciados estão disponíveis por meio do catálogo de serviços, não pelo Azure Marketplace.

Para publicar um aplicativo gerenciado do catálogo de serviços, você deve:

* Crie um modelo que define os recursos para implantar com o aplicativo gerenciado.
* Defina os elementos da interface do usuário para o portal ao implantar o aplicativo gerenciado.
* Criar um pacote .zip que contenha os arquivos de modelo necessários.
* Decidir qual usuário, grupo ou aplicativo precisa de acesso ao grupo de recursos na assinatura do usuário.
* Criar a definição de aplicativo gerenciado que aponta para o pacote .zip e solicita o acesso à identidade.

Para este artigo, seu aplicativo gerenciado contém apenas uma conta de armazenamento. Sua finalidade é ilustrar as etapas da publicação de um aplicativo gerenciado. Para obter exemplos completos, consulte [Projetos de exemplo para aplicativos gerenciados pelo Azure](sample-projects.md).

Os exemplos de PowerShell neste artigo exigem a versão 6.2 ou posterior do Azure PowerShell. Se necessário, [atualize sua versão](/powershell/azure/azurerm/install-azurerm-ps).

## <a name="create-the-resource-template"></a>Criar o modelo de recurso

Cada definição de aplicativo gerenciado contém um arquivo chamado **mainTemplate.json**. Nele, você pode definir os recursos do Azure que serão implantados. O modelo não é diferente de um modelo normal do Resource Manager.

Crie um arquivo chamado **mainTemplate.json**. O nome diferencia maiúsculas de minúsculas.

Adicione o seguinte JSON ao seu arquivo. Ele define os parâmetros para a criação de uma conta de armazenamento e especifica as propriedades dela.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        },
        "storageAccountType": {
            "type": "string"
        },
        "location": {
            "type": "string",
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {
        "storageAccountName": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[variables('storageAccountName')]",
            "apiVersion": "2016-01-01",
            "location": "[parameters('location')]",
            "sku": {
                "name": "[parameters('storageAccountType')]"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {
        "storageEndpoint": {
            "type": "string",
            "value": "[reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
        }
    }
}
```

Salve o arquivo mainTemplate.json.

## <a name="create-the-user-interface-definition"></a>Crie a definição da interface do usuário

O portal do Azure usa o arquivo **createUiDefinition.json** para gerar a interface do usuário para os usuários que criam o aplicativo gerenciado. Você define como os usuários fornecem a entrada para cada parâmetro. Você pode usar opções como uma lista suspensa, caixa de texto, caixa de senha e outras ferramentas de entrada. Para saber como criar um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução a CreateUiDefinition](create-uidefinition-overview.md).

Crie um arquivo chamado **createUiDefinition.json**. O nome diferencia maiúsculas de minúsculas.

Adicione o seguinte JSON ao arquivo.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json#",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {}
        ],
        "steps": [
            {
                "name": "storageConfig",
                "label": "Storage settings",
                "subLabel": {
                    "preValidation": "Configure the infrastructure settings",
                    "postValidation": "Done"
                },
                "bladeTitle": "Storage settings",
                "elements": [
                    {
                        "name": "storageAccounts",
                        "type": "Microsoft.Storage.MultiStorageAccountCombo",
                        "label": {
                            "prefix": "Storage account name prefix",
                            "type": "Storage account type"
                        },
                        "defaultValue": {
                            "type": "Standard_LRS"
                        },
                        "constraints": {
                            "allowedTypes": [
                                "Premium_LRS",
                                "Standard_LRS",
                                "Standard_GRS"
                            ]
                        }
                    }
                ]
            }
        ],
        "outputs": {
            "storageAccountNamePrefix": "[steps('storageConfig').storageAccounts.prefix]",
            "storageAccountType": "[steps('storageConfig').storageAccounts.type]",
            "location": "[location()]"
        }
    }
}
```

Salve o arquivo createUiDefinition.json.

## <a name="package-the-files"></a>Empacote os arquivos

Adicione os dois arquivos em um arquivo zip chamado app.zip. Os dois arquivos devem estar no nível raiz do arquivo .zip. Se você colocá-los em uma pasta, receberá um erro ao criar a definição de aplicativo gerenciado que indica que os arquivos necessários não estão presentes. 

Carregue o pacote em um local acessível no qual ele pode ser consumido. 

```powershell
New-AzureRmResourceGroup -Name storageGroup -Location eastus
$storageAccount = New-AzureRmStorageAccount -ResourceGroupName storageGroup `
  -Name "mystorageaccount" `
  -Location eastus `
  -SkuName Standard_LRS `
  -Kind Storage

$ctx = $storageAccount.Context

New-AzureStorageContainer -Name appcontainer -Context $ctx -Permission blob

Set-AzureStorageBlobContent -File "D:\myapplications\app.zip" `
  -Container appcontainer `
  -Blob "app.zip" `
  -Context $ctx 
```

## <a name="create-the-managed-application-definition"></a>Criar a definição de aplicativo gerenciado

### <a name="create-an-azure-active-directory-user-group-or-application"></a>Criar um grupo de usuários ou aplicativo do Azure Active Directory

A próxima etapa é selecionar um grupo de usuários ou um aplicativo para gerenciar os recursos em nome do cliente. Esse grupo de usuários ou aplicativo tem permissões no grupo de recursos gerenciados de acordo com a função atribuída. A função pode ser qualquer função interna de RBAC (Controle de acesso baseado em função) como Proprietário ou Colaborador. Também é possível conceder a um usuário individual permissões para gerenciar os recursos, mas, normalmente, você atribui essa permissão a um grupo de usuários. Para criar um novo grupo de usuários do Active Directory, consulte [Criar um grupo e adicionar membros no Azure Active Directory](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md).

É necessário usar a ID de objeto do grupo de usuários para gerenciar os recursos. 

```powershell
$groupID=(Get-AzureRmADGroup -DisplayName mygroup).Id
```

### <a name="get-the-role-definition-id"></a>Obter a ID de definição da função

Em seguida, é necessário o ID de definição de função da função RBAC interna para conceder acesso ao usuário, grupo de usuários ou aplicativo. Normalmente, você usa a função Proprietário, Colaborador ou Leitor. O comando a seguir mostra como obter a ID de definição de função para a função Proprietário:

```powershell
$ownerID=(Get-AzureRmRoleDefinition -Name Owner).Id
```

### <a name="create-the-managed-application-definition"></a>Criar a definição de aplicativo gerenciado

Se você ainda não tiver um grupo de recursos para armazenar a definição de aplicativo gerenciado, crie um agora:

```powershell
New-AzureRmResourceGroup -Name appDefinitionGroup -Location westcentralus
```

Agora, crie o recurso de definição de aplicativo gerenciado.

```powershell
$blob = Get-AzureStorageBlob -Container appcontainer -Blob app.zip -Context $ctx

New-AzureRmManagedApplicationDefinition `
  -Name "ManagedStorage" `
  -Location "westcentralus" `
  -ResourceGroupName appDefinitionGroup `
  -LockLevel ReadOnly `
  -DisplayName "Managed Storage Account" `
  -Description "Managed Azure Storage Account" `
  -Authorization "${groupID}:$ownerID" `
  -PackageFileUri $blob.ICloudBlob.StorageUri.PrimaryUri.AbsoluteUri
```

### <a name="make-sure-users-can-see-your-definition"></a>Verifique se os usuários podem ver sua definição

Você tem acesso à definição de aplicativo gerenciado, mas você deve certificar-se de que outros usuários na sua organização podem acessá-lo. Conceda a eles pelo menos a função de Leitor para a definição. Eles podem ter herdado esse nível de acesso da assinatura ou grupo de recursos. Para verificar quem tem acesso à definição e adicionar usuários ou grupos, consulte [Usar Controle de acesso baseado em função para gerenciar o acesso aos recursos da sua assinatura do Azure](../role-based-access-control/role-assignments-portal.md).

## <a name="next-steps"></a>Próximas etapas

* Para publicar o aplicativo gerenciado no Azure Marketplace, veja [Aplicativos Gerenciados do Azure no Marketplace](publish-marketplace-app.md).
* Para implantar uma instância de aplicativo gerenciado, veja [Implantar aplicativo do catálogo de serviços por meio do portal do Azure](deploy-service-catalog-quickstart.md).