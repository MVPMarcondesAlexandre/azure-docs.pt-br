---
title: Exemplo de CLI para monitorar e dimensionar um único Banco de Dados SQL do Azure | Microsoft Docs
description: Script de exemplo de CLI do Azure para monitorar e dimensionar um único banco de dados SQL do Azure
services: sql-database
ms.service: sql-database
ms.subservice: performance
ms.custom: ''
ms.devlang: azurecli
ms.topic: sample
author: juliemsft
ms.author: jrasnick
ms.reviewer: carlrab
manager: craigg
ms.date: 01/25/2019
ms.openlocfilehash: 18d4127e8babfcb541312d14b80d2d5477feb331
ms.sourcegitcommit: 415742227ba5c3b089f7909aa16e0d8d5418f7fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55766415"
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a>Usar a CLI para monitorar e dimensionar um único Banco de Dados SQL

Este exemplo de script da CLI do Azure dimensiona um banco de dados SQL do Azure individual para um tamanho de computação diferente depois de consultar as informações de tamanho do banco de dados. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este artigo exigirá que seja executada a CLI do Azure versão 2.0 ou posterior. Execute `az --version` para encontrar a versão. Se você precisar instalar ou atualizar, confira [Instalar a CLI do Azure]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

> [!TIP]
> Use [az sql db op list](/cli/azure/sql/db/op?#az-sql-db-op-list) para obter uma lista das operações executadas no banco de dados, e use [az sql db op cancel](/cli/azure/sql/db/op#az-sql-db-op-cancel) para cancelar uma operação de atualização no banco de dados.

## <a name="clean-up-deployment"></a>Limpar a implantação

Após a execução do script de exemplo, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando da tabela é vinculado à documentação específica do comando.

| Comando | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az-group-create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#az-sql-server-create) | Cria um servidor de Banco de Dados SQL que hospeda bancos de dados individuais e pools elásticos. |
| [az sql db show-usage](https://docs.microsoft.com/cli/azure/sql/db) | Mostra as informações de uso de tamanho de um banco de dados individual ou em pool. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#az-sql-db-update) | Atualiza as propriedades do banco de dados (como a camada de serviço ou o tamanho de computação) ou move um banco de dados para dentro, para fora ou para a posição entre pools elásticos. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az-vm-extension-set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure).

Os exemplos de script da CLI do Banco de Dados SQL adicionais podem ser encontrados na [documentação do Banco de Dados SQL do Azure](../sql-database-cli-samples.md).
