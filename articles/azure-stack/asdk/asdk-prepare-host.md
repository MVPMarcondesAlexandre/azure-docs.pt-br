---
title: Preparar o computador de host do Kit de desenvolvimento na pilha do Azure (ASDK) | Microsoft Docs
description: Descreve como preparar o computador de host do Kit de desenvolvimento na pilha do Azure (ASDK) para a instalação de ASDK.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/22/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.lastreviewed: 10/22/2018
ms.openlocfilehash: ec7b56a7324f3c8c3e3459639e4fd00e92d93e8f
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55249741"
---
# <a name="prepare-the-asdk-host-computer"></a>Preparar o computador de host ASDK
Antes de instalar o ASDK no computador host, o ambiente ASDK deve estar preparado para a instalação. Quando o computador de host do kit de desenvolvimento foi preparado, ele será inicializado do disco rígido de máquina virtual CloudBuilder.vhdx para iniciar a implantação de ASDK.

## <a name="prepare-the-development-kit-host-computer"></a>Preparar o computador de host do kit de desenvolvimento
Antes de instalar o ASDK no computador host, o ambiente do computador host ASDK deve ser preparado.
1. Entrar como Administrador Local em seu computador de host do kit de desenvolvimento.
2. Certifique-se de que o arquivo CloudBuilder.vhdx foi movido para a raiz da unidade C:\ (C:\CloudBuilder.vhdx).
3. Execute o script a seguir para baixar o arquivo de instalador do kit de desenvolvimento (asdk installer.ps1) a partir o [repositório de ferramentas do Azure Stack no GitHub](https://github.com/Azure/AzureStack-Tools) para o **C:\AzureStack_Installer** pasta no seu computador de host do kit de desenvolvimento:

  ```powershell
  # Variables
  $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
  $LocalPath = 'C:\AzureStack_Installer'
  # Create folder
  New-Item $LocalPath -Type directory
  # Enforce usage of TLSv1.2 to download from GitHub
  [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
  # Download file
  Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
  ```

4. Em um console do PowerShell com privilégios elevados, inicie o **C:\AzureStack_Installer\asdk-installer.ps1** script e, em seguida, clique em **preparar o ambiente**.

    ![](media/asdk-prepare-host/1.PNG) 

5. No **Cloudbuilder selecione vhdx** página do instalador, navegue até e selecione o **cloudbuilder.vhdx** arquivo que você baixou e extraiu na [as etapas anteriores](asdk-download.md). Nessa página, você também pode, opcionalmente, habilitar o **adicionar drivers** caixa de seleção se você precisar adicionar drivers adicionais para o computador de host do kit de desenvolvimento. Clique em **Avançar**.  

    ![](media/asdk-prepare-host/2.PNG)

6. Sobre o **configurações opcionais** , forneça o administrador local informações de conta para o computador de host do kit de desenvolvimento e, em seguida, clique em **próxima**. Você também pode fornecer valores para as seguintes configurações opcionais:
  - **ComputerName**: Essa opção define o nome do host do kit de desenvolvimento. O nome deve atender aos requisitos de FQDN e deve ser de 15 caracteres ou menos. O padrão é um nome aleatório gerado pelo Windows.
  - **Configuração de IP estático**: Define sua implantação usar um endereço IP estático. Caso contrário, quando o instalador for reinicializado no cloudbuilder.vhdx, as interfaces de rede são configuradas com DHCP.

    ![](media/asdk-prepare-host/3.PNG)

  > [!IMPORTANT]
  > Se você não fornecer as credenciais de administrador local nesta etapa, você precisará direta ou acesso KVM para o host após reiniciar o computador como parte de como configurar o kit de desenvolvimento.

7. Se você escolher uma configuração de IP estático na etapa anterior, agora você deve:
    - Selecione um adaptador de rede. Verifique se você pode se conectar ao adaptador antes de clicar em **próxima**.
    - Certifique-se de que o **endereço IP**, **Gateway**, e **DNS** valores estão corretos e, em seguida, clique em **Avançar**.
13. Clique em **próxima** para iniciar o processo de preparação.
14. Quando a preparação indica **Completed**, clique em **próxima**.
15. Clique em **reinicializar agora** para inicializar o computador de host do kit de desenvolvimento no cloudbuilder.vhdx e [continuar o processo de implantação](asdk-install.md).

    ![](media/asdk-prepare-host/4.PNG)


## <a name="next-steps"></a>Próximas etapas
[Instalar o ASDK](asdk-install.md)
