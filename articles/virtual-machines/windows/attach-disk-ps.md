---
title: Anexar um disco de dados a uma VM do Windows no Azure usando o PowerShell | Microsoft Docs
description: Como anexar um disco de dados novo ou existente a uma VM do Windows usando o PowerShell com o modelo de implantação do Resource Manager.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/16/2018
ms.author: cynthn
ms.subservice: disks
ms.openlocfilehash: abfaf76743f42a3fc4a13878d528c755feeef42a
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55458560"
---
# <a name="attach-a-data-disk-to-a-windows-vm-with-powershell"></a>Anexar um disco de dados a uma VM do Windows com o PowerShell

Este artigo mostra como anexar discos novos e existentes a uma máquina virtual do Windows usando o PowerShell. 

Primeiro, leia estas dicas:
* O tamanho da máquina virtual controla quantos discos de dados você pode anexar a ela. Para obter mais informações, confira [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para usar o armazenamento Premium, você precisará de um tipo de VM ativado para Armazenamento Premium, como a máquina virtual da série DS ou da série GS. Para saber mais, veja [Armazenamento Premium: Armazenamento de alto desempenho para cargas de trabalho de máquina virtual do Azure](premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

Para instalar e usar o PowerShell localmente, este tutorial requer o módulo do Azure PowerShell versão 6.0.0 ou posterior. Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão. Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/azurerm/install-azurerm-ps). Se você estiver executando o PowerShell localmente, também precisará executar `Connect-AzureRmAccount` para criar uma conexão com o Azure.


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a>Adicionar um disco de dados vazio a uma máquina virtual

Este exemplo mostra como adicionar um disco de dados vazio a uma máquina virtual existente.

### <a name="using-managed-disks"></a>Usar discos gerenciados

```azurepowershell-interactive
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'East US' 
$storageType = 'Premium_LRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -SkuName $storageType -Location $location -CreateOption Empty -DiskSizeGB 128
$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-managed-disks-in-an-availability-zone"></a>Usando discos gerenciados em uma zona de disponibilidade
Para criar um disco em uma zona de disponibilidade, use [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig) com o parâmetro `-Zone`. O exemplo a seguir cria um disco na zona *1*.


```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'East US 2' 
$storageType = 'Premium_LRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -SkuName $storageType -Location $location -CreateOption Empty -DiskSizeGB 128 -Zone 1
$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```


### <a name="initialize-the-disk"></a>Inicializar o disco

Depois de adicionar um disco vazio, você precisará inicializá-lo. Para inicializar o disco, você pode entrar em uma VM e usar o gerenciamento de disco. Se você ativou o [WinRM](https://docs.microsoft.com/windows/desktop/WinRM/portal) e um certificado na VM ao criá-lo, poderá usar o PowerShell remoto para inicializar o disco. Você também pode usar uma extensão de script personalizado: 

```azurepowershell-interactive
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
O arquivo de script pode conter código para inicializar os discos, por exemplo:

```azurepowershell-interactive
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a>Anexar um disco de dados existente a uma VM

Você pode anexar um disco gerenciado existente a uma VM como um disco de dados. 

```azurepowershell-interactive
$rgName = "myResourceGroup"
$vmName = "myVM"
$location = "East US" 
$dataDiskName = "myDisk"
$disk = Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $dataDiskName 

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -CreateOption Attach -Lun 0 -VM $vm -ManagedDiskId $disk.Id

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>Próximas etapas

Criar um [instantâneo](snapshot-copy-managed-disk.md).
