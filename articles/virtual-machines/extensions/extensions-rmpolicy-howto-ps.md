---
title: Usar a Azure Policy para restringir a instalação da extensão VM | Microsoft Docs
description: Use a Azure Policy para restringir as implantações de extensão.
services: virtual-machines-linux
documentationcenter: ''
author: roiyz-msft
manager: jeconnoc
editor: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/23/2018
ms.author: roiyz;cynthn
ms.openlocfilehash: 82b01cec892f15f7f85f6b5f822475114b5b73c6
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54434982"
---
# <a name="use-azure-policy-to-restrict-extensions-installation-on-windows-vms"></a>Usar a Azure Policy para restringir a instalação de extensões nas VMs do Windows

Se você quiser impedir o uso ou a instalação de certas extensões de suas VMs do Windows, você pode criar uma política do Azure usando o PowerShell para restringir as extensões de máquinas virtuais dentro de um grupo de recursos. 

Este tutorial usa o Azure PowerShell na Cloud Shell, que é constantemente atualizada para a versão mais recente. Se você optar por instalar e usar o PowerShell localmente, este tutorial exigirá o módulo do Azure PowerShell versão 3.6 ou posterior. Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão. Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/azurerm/install-azurerm-ps). 

## <a name="create-a-rules-file"></a>Criar um arquivo de regras

Para restringir quais extensões podem ser instaladas, você precisa ter uma [regra](/azure/azure-policy/policy-definition#policy-rule) para fornecer a lógica para identificar a extensão.

Este exemplo mostra como negar extensões publicadas por 'Microsoft. Compute' criando um arquivo de regras na Cloud Shell do Azure, mas se você estiver trabalhando localmente no PowerShell, você também pode criar um arquivo local e substituir o caminho ($home/clouddrive) pelo caminho para o arquivo local no seu computador.

Em um [Cloud Shell](https://shell.azure.com/powershell), digite:

```azurepowershell-interactive
nano $home/clouddrive/rules.json
```

Copie e cole o seguinte .json no arquivo.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "in": "[parameters('notAllowedExtensions')]"
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

Quando terminar, pressione o **Ctrl + O** e **Enter** para salvar o arquivo. Aperte **Ctrl + X** para fechar o arquivo e saia.

## <a name="create-a-parameters-file"></a>Criar um arquivo de parâmetros

Você também precisa de um arquivo de [parâmetros](/azure/azure-policy/policy-definition#parameters) que cria uma estrutura para usar para passar uma lista de extensões para bloquear. 

Este exemplo mostra como criar um arquivo de parâmetros para VMs no Cloud Shell, mas se você estiver trabalhando localmente no PowerShell, você também pode criar um arquivo local e substituir o caminho ($home/clouddrive) pelo caminho para o arquivo local no seu computador.

Em um [Cloud Shell](https://shell.azure.com/powershell), digite:

```azurepowershell-interactive
nano $home/clouddrive/parameters.json
```

Copie e cole o seguinte .json no arquivo.

```json
{
    "notAllowedExtensions": {
        "type": "Array",
        "metadata": {
            "description": "The list of extensions that will be denied.",
            "strongType": "type",
            "displayName": "Denied extension"
        }
    }
}
```

Quando terminar, pressione o **Ctrl + O** e **Enter** para salvar o arquivo. Aperte **Ctrl + X** para fechar o arquivo e saia.

## <a name="create-the-policy"></a>Criar a política

Uma definição de política é um objeto usado para armazenar a configuração que você deseja usar. A definição de política usa os arquivos de regras e parâmetros para definir a política. Crie uma definição de política usando o cmdlet [New-AzureRmPolicyDefinition](/powershell/module/azurerm.resources/new-azurermpolicydefinition).

 Os parâmetros e as regras de política são os arquivos criados e armazenados como arquivos. .json no seu cloud shell.


```azurepowershell-interactive
$definition = New-AzureRmPolicyDefinition `
   -Name "not-allowed-vmextension-windows" `
   -DisplayName "Not allowed VM Extensions" `
   -description "This policy governs which VM extensions that are explicitly denied."   `
   -Policy 'C:\Users\ContainerAdministrator\clouddrive\rules.json' `
   -Parameter 'C:\Users\ContainerAdministrator\clouddrive\parameters.json'
```




## <a name="assign-the-policy"></a>Atribuir a política

Este exemplo atribui a regra a um grupo de recursos usando [New-AzureRMPolicyAssignment](/powershell/module/azurerm.resources/new-azurermpolicyassignment). Qualquer VM criada no grupo de recursos **myResourceGroup** não será capaz de instalar as extensões do agente de VM de acesso ou Script personalizado. 

Use o cmdlet do [Get-AzureRMSubscription | Format-Table](/powershell/module/azurerm.profile/get-azurermsubscription) para obter sua ID de assinatura para usar no lugar no exemplo.

```azurepowershell-interactive
$scope = "/subscriptions/<subscription id>/resourceGroups/myResourceGroup"
$assignment = New-AzureRMPolicyAssignment `
   -Name "not-allowed-vmextension-windows" `
   -Scope $scope `
   -PolicyDefinition $definition `
   -PolicyParameter '{
    "notAllowedExtensions": {
        "value": [
            "VMAccessAgent",
            "CustomScriptExtension"
        ]
    }
}'
$assignment
```

## <a name="test-the-policy"></a>Testar a política

Para testar a política, tente usar a extensão de acesso da VM. O seguinte deve falhar com a mensagem "Set-AzureRmVMAccessExtension: O recurso 'myVMAccess' foi desautorizado pela política."

```azurepowershell-interactive
Set-AzureRmVMAccessExtension `
   -ResourceGroupName "myResourceGroup" `
   -VMName "myVM" `
   -Name "myVMAccess" `
   -Location EastUS 
```

No portal, a alteração da senha deve falhar com "A implantação do modelo falhou por causa de violação de política". mensagem.

## <a name="remove-the-assignment"></a>Remover a atribuição

```azurepowershell-interactive
Remove-AzureRMPolicyAssignment -Name not-allowed-vmextension-windows -Scope $scope
```

## <a name="remove-the-policy"></a>Remover a política

```azurepowershell-interactive
Remove-AzureRmPolicyDefinition -Name not-allowed-vmextension-windows
```
    
## <a name="next-steps"></a>Próximas etapas
Para saber mais, veja [Azure Policy](../../azure-policy/azure-policy-introduction.md).
