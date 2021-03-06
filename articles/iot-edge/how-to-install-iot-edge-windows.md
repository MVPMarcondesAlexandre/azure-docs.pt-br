---
title: Instalar o Azure IoT Edge no Windows | Microsoft Docs
description: Instruções de instalação do Azure IoT Edge no Windows 10, Windows Server e Windows IoT Core
author: kgremban
manager: philmea
ms.reviewer: veyalla
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 01/25/2019
ms.author: kgremban
ms.custom: seodec18
ms.openlocfilehash: 27478de68cde9a097dcc160a4553839aef9a018c
ms.sourcegitcommit: 644de9305293600faf9c7dad951bfeee334f0ba3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54902798"
---
# <a name="install-the-azure-iot-edge-runtime-on-windows"></a>Instalar o tempo de execução do IoT Edge no Windows

O tempo de execução do Azure IoT Edge é o que transforma um dispositivo em um dispositivo do IoT Edge. O tempo de execução pode ser implantado em dispositivos pequenos como um Raspberry Pi ou grandes como um servidor industrial. Após um dispositivo ser configurado com o tempo de execução do IoT Edge, você poderá começar a implantar a lógica de negócios da nuvem nele. 

Para saber mais sobre o tempo de execução do IoT Edge, consulte [Reconhecer o tempo de execução do Azure IoT Edge e sua arquitetura](iot-edge-runtime.md).

Este artigo lista as etapas para instalar o tempo de execução do Azure IoT Edge no sistema Windows x64 (AMD/Intel). Atualmente, o suporte do Windows está em versão prévia.

>[!NOTE]
O uso de contêineres do Linux no sistema Windows não é uma configuração de produção com suporte ou recomendada para o Azure IoT Edge. No entanto, pode ser utilizado para fins de desenvolvimento e teste.

## <a name="prerequisites"></a>Pré-requisitos

Use esta seção para verificar se o dispositivo Windows pode dar suporte ao IoT Edge e prepará-lo para um mecanismo de contêiner antes da instalação. 

### <a name="supported-windows-versions"></a>Versões do Windows com suporte

O Azure IoT Edge dá suporte a diferentes versões do Windows, dependendo se está executando contêineres do Windows ou contêineres do Linux. 

A última versão do Azure IoT Edge com contêineres do Windows pode ser executada nas seguintes versões do Windows:
* Windows 10 ou IoT Core com atualização de outubro de 2018 (build 17763)
* Windows Server 2019 (build 17763)

A última versão do Azure IoT Edge com contêineres Linux pode ser executada nas seguintes versões do Windows: 
* Atualização de Aniversário do Windows 10 (build 14393) ou mais recente
* Windows Server 2016 ou mais recente

Para obter mais informações sobre quais sistemas operacionais atualmente têm suporte, consulte [Suporte do Azure IoT Edge](support.md#operating-systems). 

Para obter mais informações sobre o que está incluído na última versão do IoT Edge, consulte [Lançamentos do Azure IoT Edge](https://github.com/Azure/azure-iotedge/releases).

### <a name="prepare-for-a-container-engine"></a>Preparar para um mecanismo de contêiner 

O Azure IoT Edge depende de um mecanismo de contêiner [compatível com OCI](https://www.opencontainers.org/). Para cenários de produção, use o mecanismo Moby incluído no script de instalação para executar contêineres do Windows no dispositivo Windows. Para desenvolver e testar, você poderá executar contêineres do Linux no dispositivo Windows, mas será necessário instalar e configurar um mecanismo de contêiner antes de instalar o IoT Edge. Para qualquer um dos cenários, consulte as seções a seguir para pré-requisitos para preparar o dispositivo. 

#### <a name="moby-engine-for-windows-containers"></a>Mecanismo Moby para contêineres do Windows

Para dispositivos Windows que executam IoT Edge em cenários de produção, o Moby é o único mecanismo de contêiner oficialmente com suporte. O script de instalação instalará automaticamente o mecanismo Moby no dispositivo, antes de instalar o IoT Edge. Prepare o dispositivo, ativando o recurso Contêineres. 

1. Na barra de início, pesquise **Ativar ou desativar recursos do Windows** e abra o programa do painel de controle.
2. Localize e selecione **Contêineres**.
3. Selecione **OK**. 

#### <a name="docker-for-linux-containers"></a>Contêineres do Docker para Linux

Se você estiver usando o Windows para desenvolver e testar contêineres para dispositivos Linux, poderá usar o [Docker for Windows](https://www.docker.com/docker-windows) como o mecanismo de contêiner. O Docker pode ser configurado para [usar contêineres do Linux](https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers). Será necessário instalar o Docker e configurá-lo, antes de instalar o IoT Edge. Contêineres do Linux não têm suporte em dispositivos Windows em produção. 

Se o dispositivo do IoT Edge for um computador Windows, verifique se atende aos [requisitos do sistema](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements) para Hyper-V. Se for uma máquina virtual, habilite [ virtualização aninhada](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization) e aloque pelo menos 2 GB de memória.

## <a name="install-iot-edge-on-a-new-device"></a>Instalar o IoT Edge em um novo dispositivo

>[!NOTE]
>Os pacotes de software do Azure IoT Edge estão sujeitos aos termos de licença localizados nos pacotes (no diretório LICENSE). Leia os termos de licença antes de utilizar o pacote. A instalação e o uso do pacote constitui a aceitação desses termos. Se você não concorda com os termos de licença, não utilize o pacote.

Um script do PowerShell baixa e instala o daemon de segurança do Azure IoT Edge. Em seguida, o daemon de segurança inicia o primeiro dos dois módulos de tempo de execução, o agente do IoT Edge, que permite implantações remotas de outros módulos. 

Quando você instala o tempo de execução do IoT Edge pela primeira vez em um dispositivo, é necessário provisionar o dispositivo com uma identidade de um hub IoT. Um único dispositivo Azure IoT Edge pode ser provisionado manualmente usando uma cadeia de caracteres de conexões de dispositivo fornecida pelo Hub IoT. Ou, você também pode usar o Serviço de Provisionamento de Dispositivos para provisionar dispositivos automaticamente, o que é útil quando há muitos dispositivos para configurar. Dependendo de sua escolha de provisionamento, escolha o script de instalação apropriado. 

As seções a seguir descrevem os casos de uso comuns e os parâmetros do script de instalação do IoT Edge em um novo dispositivo. 

### <a name="option-1-install-and-manually-provision"></a>Opção 1: Instalar e provisionar manualmente

Nesta primeira opção, você fornece uma cadeia de conexão de dispositivo gerada pelo Hub IoT para provisionar o dispositivo. 

Siga as etapas em [Registrar um novo dispositivo Azure IoT Edge](how-to-register-device-portal.md) para registrar seu dispositivo e recuperar a cadeia de caracteres de conexão do dispositivo. 

Este exemplo mostra uma instalação manual com contêineres do Windows:

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Install-SecurityDaemon -Manual -ContainerOs Windows -DeviceConnectionString '<connection-string>'
```

Ao instalar e provisionar um dispositivo manualmente, é possível usar parâmetros adicionais para modificar a instalação, incluindo:
* Tráfego direto para passar por um servidor proxy
* Apontar o instalador para um diretório offline
* Declarar uma imagem de contêiner específica do agente e fornecer credenciais se estiver em um registro privado
* Ignorar a instalação da CLI do Moby

Para obter mais informações sobre essas opções de instalação, continue lendo este artigo ou ignore para saber mais sobre [Todos os parâmetros de instalação](#all-installation-parameters).

### <a name="option-2-install-and-automatically-provision"></a>Opção 2: Instalar e provisionar automaticamente

Nesta segunda opção, você provisiona o dispositivo usando o Serviço de Provisionamento de Dispositivos no Hub IoT. Forneça a **ID do Escopo** de uma instância de Serviço de Provisionamento de Dispositivos e a **ID de Registro** do seu dispositivo.

Siga as etapas em [Crie e provisione um dispositivo TPM Edge simulado no Windows](how-to-auto-provision-simulated-device-windows.md) para configurar o Serviço de Provisionamento de Dispositivo e recuperar seu **ID do escopo**, simular um dispositivo TPM e recuperar seu **Registro ID** e crie uma inscrição individual. Depois que o dispositivo é registrado no Hub IoT, continue com a instalação.  

   >[!TIP]
   >Mantenha a janela que está executando o simulador do TPM aberta durante a instalação e teste. 

O exemplo a seguir mostra uma instalação automática com contêineres do Windows:

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Install-SecurityDaemon -Dps -ContainerOs Windows -ScopeId <DPS scope ID> -RegistrationId <device registration ID>
```

Ao instalar e provisionar um dispositivo manualmente, é possível usar parâmetros adicionais para modificar a instalação, incluindo:
* Tráfego direto para passar por um servidor proxy
* Apontar o instalador para um diretório offline
* Declarar uma imagem de contêiner específica do agente e fornecer credenciais se estiver em um registro privado
* Ignorar a instalação da CLI do Moby

Para obter mais informações sobre essas opções de instalação, continue lendo este artigo ou ignore para saber mais sobre [Todos os parâmetros de instalação](#all-installation-parameters).

## <a name="update-an-existing-installation"></a>Atualizar uma instalação existente

Se você já instalou o tempo de execução do IoT Edge em um dispositivo antes e o provisionou com uma identidade do Hub IoT, poderá usar um script de instalação simplificado. O sinalizador `-ExistingConfig` declara que um arquivo de configuração do IoT Edge já existe no dispositivo. O arquivo de configuração contém informações sobre a identidade do dispositivo, além de certificados e configurações de rede. Será possível usar essa opção de instalação, se o dispositivo foi originalmente provisionado manual ou automaticamente. 

Para obter mais informações, consulte [Atualize o daemon de segurança e o tempo de execução do IoT Edge](how-to-update-iot-edge.md).

Este exemplo mostra uma instalação que aponta para um arquivo de configuração existente e usa contêineres do Windows: 

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Install-SecurityDaemon -ExistingConfig -ContainerOs Windows
```

Ao instalar o IoT Edge a partir de um arquivo de configuração existente, é possível usar parâmetros adicionais para modificar a instalação, incluindo:
* Tráfego direto para passar por um servidor proxy
* Apontar o instalador para um diretório offline ou, 
* Ignorar a instalação da CLI do Moby. 

Não é possível declarar uma imagem de contêiner do agente do IoT Edge com parâmetros de script, porque essas informações já foram definidas no arquivo de configuração da instalação anterior. Se você quiser modificar a imagem de contêiner do agente, faça isso no arquivo config.yaml. 

Para obter mais informações sobre essas opções de instalação, continue lendo este artigo ou ignore para saber mais sobre [Todos os parâmetros de instalação](#all-installation-parameters).

## <a name="offline-installation"></a>Instalação offline

Durante a instalação, quatro arquivos são baixados: 
* Zip do daemon de segurança do IoT Edge (iotedgd) 
* Zip do mecanismo Moby
* Zip da CLI do Moby
* MSI do pacote redistribuível do Visual C++ (tempo de execução de VC)

É possível baixar um ou todos esses arquivos antecipadamente no dispositivo e, em seguida, apontar o script de instalação para o diretório que contém os arquivos. O instalador primeiro verifica o diretório e, em seguida, baixa apenas os componentes que não são localizados. Se todos os quatro arquivos estiverem disponíveis offline, você poderá instalá-los sem conexão com a Internet. Você também pode usar esse recurso para substituir as versões online de um ou mais componentes.  

Para obter os arquivos de instalação mais recentes junto com as versões anteriores, consulte [Lançamentos do Azure IoT Edge](https://github.com/Azure/azure-iotedge/releases)

Para instalar com componentes offline, use o parâmetro `-OfflineInstallationPath` e forneça o caminho absoluto para o diretório de arquivos. Por exemplo,

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Install-SecurityDaemon -Manual -DeviceConnectionString '<connection-string>' -OfflineInstallationPath C:\Downloads\iotedgeoffline
```

## <a name="all-installation-parameters"></a>Todos os parâmetros de instalação

As seções anteriores introduziram cenários comuns de instalação com exemplos de como usar parâmetros para modificar o script de instalação. Esta seção fornece uma tabela de referência dos parâmetros válidos que podem ser usados para instalar o IoT Edge. Para obter mais informações, execute `get-help Install-SecurityDaemon -full` em uma janela do PowerShell. 

Para instalar o IoT Edge com uma configuração existente, o comando de instalação pode usar esses parâmetros comuns: 

| Parâmetro | Valores aceitos | Comentários |
| --------- | --------------- | -------- |
| **Manual** | Nenhum | **Parâmetro de opção**. Cada instalação deve ser declarada manual, DPS ou existingconfig.<br><br>Declara que você fornecerá uma cadeia de conexão de dispositivo para provisionar o dispositivo manualmente |
| **Dps** | Nenhum | **Parâmetro de opção**. Cada instalação deve ser declarada manual, DPS ou existingconfig.<br><br>Declara que você fornecerá uma ID do escopo do DPS (Serviço de Provisionamento de Dispositivos) e a ID de Registro do dispositivo para provisionar por meio do DPS.  |
| **ExistingConfig** | Nenhum | **Parâmetro de opção**. Cada instalação deve ser declarada manual, DPS ou existingconfig.<br><br>Declara que um arquivo config.yaml já existe no dispositivo com as informações de provisionamento. |
| **DeviceConnectionString** | Uma cadeia de conexão de um dispositivo do IoT Edge registrado em um Hub IoT, entre aspas simples | **Necessário** para instalação manual. Se você não fornecer uma cadeia de conexão nos parâmetros de script, durante a instalação será solicitado que você forneça uma. |
| **ScopeId** | Uma ID do escopo de uma instância do Serviço de Provisionamento de Dispositivos associada ao Hub IoT. | **Necessário** para instalação de DPS. Se você não fornecer uma ID do escopo nos parâmetros do script, durante a instalação será solicitado que você forneça uma. |
| **RegistrationId** | Uma ID de registro gerada pelo dispositivo | **Necessário** para instalação de DPS. Se você não fornecer uma ID de registro nos parâmetros de script, durante a instalação será solicitado que você forneça uma. |
| **ContainerOs** | **Windows** ou **Linux** | Se nenhum sistema operacional de contêiner for especificado, o Linux será o valor padrão. Para contêineres do Windows, um mecanismo de contêiner será incluído na instalação. Para contêineres do Linux, será necessário instalar um mecanismo de contêiner antes de iniciar a instalação. A execução de contêineres do Linux no Windows é um cenário de desenvolvimento útil, mas não tem suporte em produção. |
| **Proxy** | URL do Proxy | Inclua esse parâmetro se o dispositivo precisar passar por um servidor proxy para acessar a Internet. Para obter mais informações, consulte [Configurar um dispositivo IoT Edge para se comunicar por meio de um servidor proxy](how-to-configure-proxy-support.md). |
| **InvokeWebRequestParameters** | Tabela de hash de parâmetros e valores | Durante a instalação, várias solicitações da Web serão feitas. Use esse campo para definir parâmetros para essas solicitações da Web. Esse parâmetro é útil para configurar credenciais para servidores proxy. Para obter mais informações, consulte [Configurar um dispositivo IoT Edge para se comunicar por meio de um servidor proxy](how-to-configure-proxy-support.md). |
| **OfflineInstallationPath** | Caminho do diretório | Se esse parâmetro for incluído, o instalador verificará o diretório do zip iotedged, zip do mecanismo Moby, zip da CLI do Moby e os arquivos MSI do Tempo de Execução de VC necessários para a instalação. Se todos os quatro arquivos estiverem no diretório, você poderá instalar o IoT Edge enquanto estiver offline. Também é possível usar esse parâmetro para substituir a versão online de um componente específico. |
| **AgentImage** | URI de imagem do agente do IoT Edge | Por padrão, uma nova instalação do IoT Edge usa a marca sem interrupção mais recente para a imagem do agente do IoT Edge. Use esse parâmetro para definir uma marca específica para a versão da imagem ou para fornecer a própria imagem de agente. Para obter mais informações, consulte [Reconhecer as marcas do IoT Edge](how-to-update-iot-edge.md#understand-iot-edge-tags). |
| **Nome de Usuário** | Nome de usuário do registro de contêiner | Use esse parâmetro somente se você definir o parâmetro -AgentImage como um contêiner em um registro privado. Forneça um nome de usuário com acesso ao registro. |
| **Senha** | Cadeia de caracteres de senha de segurança | Use esse parâmetro somente se você definir o parâmetro -AgentImage como um contêiner em um registro privado. Forneça a senha para acessar o registro. | 
| **SkipMobyCli** | Nenhum | Aplicável apenas se -ContainerOS estiver configurado para Windows. Não instale a CLI do Moby (docker.exe) no $MobyInstallDirectory. |

## <a name="verify-successful-installation"></a>Verifique se a instalação bem-sucedida

É possível verificar o status do serviço do IoT Edge por: 

```powershell
Get-Service iotedge
```

Examine os logs de serviço pelos últimos 5 minutos usando:

```powershell

# Displays logs from last 5 min, newest at the bottom.

Get-WinEvent -ea SilentlyContinue `
  -FilterHashtable @{ProviderName= "iotedged";
    LogName = "application"; StartTime = [datetime]::Now.AddMinutes(-5)} |
  select TimeCreated, Message |
  sort-object @{Expression="TimeCreated";Descending=$false} |
  format-table -autosize -wrap
```

Além disso, lista de módulos com em execução:

```powershell
iotedge list
```

## <a name="uninstall-iot-edge"></a>Desinstalar o IoT Edge

Se você quiser remover a instalação do IoT Edge do dispositivo Windows, use o seguinte comando em uma janela administrativa do PowerShell. Esse comando remove o tempo de execução do IoT Edge, juntamente com a configuração existente e os dados do mecanismo Moby. 

```PowerShell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Uninstall-SecurityDaemon -DeleteConfig -DeleteMobyDataRoot
```

Se você pretende reinstalar o IoT Edge no dispositivo, deixe de fora os parâmetros `-DeleteConfig` e `-DeleteMobyDataRoot` para poder reinstalar o daemon de segurança posteriormente, com as informações de configuração existentes. 

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um dispositivo IoT Edge provisionado com o tempo de execução instalado, é possível [implantar os módulos do IoT Edge](how-to-deploy-modules-portal.md).

Se você estiver tendo problemas com a instalação correta do IoT Edge, consulte a página de [solução de problemas](troubleshoot.md).

Para atualizar uma instalação existente para a versão mais recente do IoT Edge, consulte [Atualizar o daemon de segurança e o tempo de execução do IoT Edge](how-to-update-iot-edge.md).
