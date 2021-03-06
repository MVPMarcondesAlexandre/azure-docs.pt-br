---
title: Configurar um servidor de processos no Azure para o failback durante a recuperação de desastres de VMs e servidores físicos VMware com o Azure Site Recovery | Microsoft Docs’
description: Este artigo descreve como configurar um servidor de processos no Azure para fazer o failback do Azure para o local durante a recuperação de desastre de VMs e servidores físicos do VMware.
author: Rajeswari-Mamilla
manager: rochakm
ms.service: site-recovery
ms.topic: conceptual
ms.date: 12/11/2018
ms.author: mayg
ms.openlocfilehash: f2d8d070a8adbe7992795b06722427da2830cb50
ms.sourcegitcommit: 1c1f258c6f32d6280677f899c4bb90b73eac3f2e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53253673"
---
# <a name="scale-for-failback-with-additional-process-servers"></a>Escala para failback com servidores de processo adicionais

Por padrão, quando você estiver replicando VMs do VMware ou servidores físicos no Azure usando o [Site Recovery](site-recovery-overview.md), um servidor de processo será instalado no computador do servidor de configuração e usado para coordenar a transferência de dados entre o Site Recovery e sua infraestrutura local. Para aumentar a capacidade e escalar horizontalmente a implantação de replicação, você pode adicionar outros servidores de processo autônomos. Este artigo descreve como fazer isso.

## <a name="before-you-start"></a>Antes de começar

### <a name="capacity-planning"></a>planejamento de capacidade

Verifique se você realizou o [planejamento de capacidade](site-recovery-plan-capacity-vmware.md) para replicação de VMware. Isso ajuda a identificar como e quando você deve implantar servidores de processo adicionais.

>[!NOTE]
Não há suporte para o uso de um componente do Servidor de Processo clonado. Siga as etapas deste artigo para cada expansão de PS.

### <a name="sizing-requirements"></a>Requisitos de dimensionamento 

Verifique os requisitos de dimensionamento resumidos na tabela. Em geral, se for necessário escalar horizontalmente sua implantação para além de 200 computadores de origem ou se você tiver uma taxa de rotatividade diária total acima de 2 TB, serão necessários servidores de processo adicionais para lidar com o volume do tráfego.

| **Servidor de processo adicional** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos** |
| --- | --- | --- | --- |
|4 vCPUs (2 soquetes * 2 núcleos \@ 2,5 GHz), 8 GB de memória |300 GB |250 GB ou menos |Replique 85 computadores ou menos. |
|8 vCPUs (2 soquetes * 4 núcleos \@ 2,5 GHz), 12 GB de memória |600 GB |250 GB a 1 TB |Replique entre 85 e 150 computadores. |
|12 vCPUs (2 soquetes * 6 núcleos \@ 2,5 GHz), 24 GB de memória |1 TB |1 TB a 2 TB |Replique entre 150 e 225 computadores. |

Onde cada computador de origem protegido é configurado com três discos de 100 GB cada.

### <a name="prerequisites"></a>Pré-requisitos

Os pré-requisitos para o servidor de processo adicional são resumidos na tabela a seguir.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]



## <a name="download-installation-file"></a>Baixar o arquivo de instalação

Baixe o arquivo de instalação para o servidor de processo da seguinte maneira:

1. Faça logon no portal do Azure e navegue até seu Cofre dos Serviços de Recuperação.
2. Abra **Infraestrutura do Site Recovery** > **VMWare e Computadores Físicos** > **Servidores de Configuração** (sob Para VMware e Computadores Físicos).
3. Selecione o servidor de configuração para fazer drill down nos detalhes do servidor. Clique em **+ Servidor de processo**.
4. Em **Adicionar servidor de processo** >  **, escolha onde você quer implantar um servidor de processo** e selecione **Implantar uma expansão de servidor de processo local**.

  ![Página Adicionar Servidores](./media/vmware-azure-set-up-process-server-scale/add-process-server.png)
1. Clique em **Baixar a Configuração Unificada do Microsoft Azure Site Recovery**. A versão mais recente do arquivo de instalação será baixada.

  > [!WARNING]
  A versão de instalação do servidor de processo deve ser a mesma ou anterior à versão do servidor de configuração executado. Uma maneira simples de garantir a compatibilidade de versão é usar o mesmo instalador usado recentemente para instalar ou atualizar o servidor de configuração.

## <a name="install-from-the-ui"></a>Instalar da interface do usuário

Instale da seguinte maneira. Depois de configurar o servidor, você migrará os computadores de origem para usá-lo.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="install-from-the-command-line"></a>Instalar usando a linha de comando

Instale o executando o seguinte comando:

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

Em que os parâmetros de linha de comando são os seguintes:

[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]

Por exemplo: 

```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /x:C:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```
### <a name="create-a-proxy-settings-file"></a>Criar um arquivo de configurações de proxy

Se for necessário configurar um proxy, o parâmetro ProxySettingsFilePath utilizará um arquivo como entrada. É possível criar o arquivo da seguinte maneira, bem como passá-lo como parâmetro de entrada ProxySettingsFilePath.

```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [gerenciar as configurações do servidor de processo](vmware-azure-manage-process-server.md)
