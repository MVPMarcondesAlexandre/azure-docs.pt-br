---
title: Exemplo do PowerShell para detecção de ameaças e auditoria do Banco de Dados SQL do Azure | Microsoft Docs
description: Script de exemplo do Azure PowerShell para configurar a detecção de ameaças e auditoria em um Banco de Dados SQL do Azure
services: sql-database
ms.service: sql-database
ms.subservice: threat-detection
ms.custom: security
ms.devlang: PowerShell
ms.topic: sample
author: ronitr
ms.author: ronitr
ms.reviewer: carlrab
manager: craigg
ms.date: 01/25/2019
ms.openlocfilehash: f25e41b8669922474c92919c3c29ad013d9a1609
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55452653"
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a>Use o PowerShell para configurar a detecção de ameaças e auditoria do Banco de Dados SQL

Este exemplo de script do PowerShell configura a detecção de ameaças e auditoria do Banco de Dados SQL.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

Se você optar por instalar e usar o PowerShell localmente, este tutorial exigirá o módulo do Azure PowerShell versão 5.7.0 ou posterior. Execute `Get-Module -ListAvailable AzureRM` para encontrar a versão. Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-az-ps). Se você estiver executando o PowerShell localmente, também precisará executar o `Connect-AzureRmAccount` para criar uma conexão com o Azure.

## <a name="sample-script"></a>Script de exemplo

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a>Limpar a implantação

Após a execução do script de exemplo, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando da tabela é vinculado à documentação específica do comando.

| Comando | Observações |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Cria um servidor de Banco de Dados SQL que hospeda um banco de dados individual ou um pool elástico. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Cria um banco de dados individual ou um pool elástico. |
| [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) | Cria uma conta de armazenamento. |
| [Set-AzureRmSqlDatabaseAuditingPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | Define a política de auditoria para um banco de dados. |
| [Set-AzureRmSqlDatabaseThreatDetectionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | Define uma política de detecção de ameaças em um banco de dados. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).

Outros exemplos de script do PowerShell para Banco de Dados SQL podem ser encontrados nos [scripts do PowerShell para Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).
