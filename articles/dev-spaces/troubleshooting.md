---
title: Solução de problemas | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.subservice: azds-kubernetes
author: zr-msft
ms.author: zarhoads
ms.date: 09/11/2018
ms.topic: article
description: Desenvolvimento rápido de Kubernetes com contêineres e microsserviços no Azure
keywords: Docker, Kubernetes, Azure, AKS, Serviço do Kubernetes do Azure, contêineres
ms.openlocfilehash: 37ee9fec8940231a01b0014b020ca3f0dffb53bf
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55467094"
---
# <a name="troubleshooting-guide"></a>Guia de Solução de Problemas

Este guia contém informações sobre problemas comuns que você pode ter ao usar o Azure Dev Spaces.

## <a name="enabling-detailed-logging"></a>Ativando o log detalhado

Para solucionar problemas de maneira mais eficaz, pode ser útil criar registros mais detalhados para revisão.

Para ver a extensão do Visual Studio, defina a variável de ambiente `MS_VS_AZUREDEVSPACES_TOOLS_LOGGING_ENABLED` como 1. Certifique-se de reiniciar o Visual Studio para que a variável de ambiente tenha efeito. Uma vez ativado, os registros detalhados serão gravados no seu diretório `%TEMP%\Microsoft.VisualStudio.Azure.DevSpaces.Tools`.

Na CLI, você pode gerar mais informações durante a execução do comando usando o switch `--verbose`. Também é possível pesquisar logs mais detalhados em `%TEMP%\Azure Dev Spaces`. Em um Mac, o diretório TEMP pode ser encontrado executando `echo $TMPDIR` em uma janela de terminal. Em um computador Linux, o diretório TEMP é geralmente `/tmp`.

## <a name="debugging-services-with-multiple-instances"></a>Serviços de depuração com várias instâncias

Neste momento, o Azure Dev Spaces funciona melhor ao depurar uma única instância (pod). O arquivo azds.yaml contém uma configuração, replicaCount, que indica o número de pods que será executado para seu serviço. Se você alterar o replicaCount para configurar seu aplicativo para executar vários pods para um determinado serviço, o depurador será anexado ao primeiro pod (quando listadas em ordem alfabética). Se o pod for reciclado por algum motivo, o depurador será anexado a um pod diferente, provavelmente causando um comportamento inesperado.

## <a name="error-failed-to-create-azure-dev-spaces-controller"></a>Erro "Falha ao criar o controlador do Azure Dev Spaces"

Você pode ver esse erro quando algo der errado com a criação do controlador. Se for um erro transitório, a exclusão e a recriação do controlador o corrigirá.

### <a name="try"></a>Experimente:

Para excluir o controlador, use a CLI do Azure Dev Spaces. Não é possível fazê-lo no Visual Studio ou no Cloud Shell. Para instalar a CLI do AZDS, primeiro instale a CLI do Azure e, em seguida, execute este comando:

```cmd
az aks use-dev-spaces -g <resource group name> -n <cluster name>
```

E, em seguida, execute este comando para excluir o controlador:

```cmd
azds remove -g <resource group name> -n <cluster name>
```

Recriar o controlador pode ser feito a partir do CLI ou Visual Studio. Siga as instruções nos tutoriais como se estivesse começando pela primeira vez.


## <a name="error-service-cannot-be-started"></a>Erro "O serviço não pode ser iniciado."

Você pode ver esse erro quando seu código de serviço não pode ser iniciado. Frequentemente, a causa está no código do usuário. Para obter mais informações de diagnóstico, faça as seguintes alterações em suas configurações e comandos:

### <a name="try"></a>Experimente:

Na linha de comando:

Quando estiver usando _azds.exe_, use a opção de linha de comando -- verbose e use a opção de linha de comando --output para especificar o formato de saída.
 
```cmd
azds up --verbose --output json
```

No Visual Studio:

1. Abra **Ferramentas > Opções** e, em **Projetos e Soluções**, escolha **Compilar e executar**.
2. Altere as configurações de **Detalhamento da saída de compilação do projeto no MSBuild** para **Detalhado** ou **Diagnóstico**.

    ![Captura de tela da caixa de diálogo Opções de ferramentas](media/common/VerbositySetting.PNG)
    
### <a name="multi-stage-dockerfiles"></a>Dockerfiles de vários estágios:
Você poderá ver esse erro ao tentar usar um Dockerfile de vários estágios. A saída detalhada se parecerá com esta:

```cmd
$ azds up
Using dev space 'default' with target 'AksClusterName'
Synchronizing files...6s
Installing Helm chart...2s
Waiting for container image build...10s
Building container image...
Step 1/12 : FROM [imagename:tag] AS base
Error parsing reference: "[imagename:tag] AS base" is not a valid repository/tag: invalid reference format
Failed to build container image.
Service cannot be started.
```

Isso ocorre porque os nós do AKS executam uma versão mais antiga do Docker que não é compatível com builds de vários estágios. Será necessário reescrever seu Dockerfile para evitar builds de vários estágios.

### <a name="re-running-a-service-after-controller-re-creation"></a>Executar novamente um serviço após a recriação do controlador
É possível visualizar esse erro ao tentar executar novamente um serviço após ter removido e, em seguida, recriado o controlador do Azure Dev Spaces associado a esse cluster. A saída detalhada se parecerá com esta:

```cmd
Installing Helm chart...
Release "azds-33d46b-default-webapp1" does not exist. Installing it now.
Error: release azds-33d46b-default-webapp1 failed: services "webapp1" already exists
Helm install failed with exit code '1': Release "azds-33d46b-default-webapp1" does not exist. Installing it now.
Error: release azds-33d46b-default-webapp1 failed: services "webapp1" already exists
```

Isso ocorre porque a remoção do controlador do Dev Spaces não remove os serviços anteriormente instalados por esse controlador. Recriar o controlador e, em seguida, tentar executar os serviços usando o novo controlador falha porque os serviços antigos ainda estão implantados.

Para corrigir isso, use o comando `kubectl delete` para remover manualmente os serviços antigos do cluster e, em seguida, execute novamente os Dev Spaces para instalar os novos serviços.

## <a name="dns-name-resolution-fails-for-a-public-url-associated-with-a-dev-spaces-service"></a>A resolução de nomes DNS falha para uma URL pública associada a um serviço do Azure Dev Spaces

Quando a resolução do nome DNS falha, é possível ver um erro "A página não pode ser exibida" ou "Este site não pode ser acessado" no navegador da Web ao tentar conectar a URL pública associada a um serviço do Dev Spaces.

### <a name="try"></a>Experimente:

Usar o seguinte comando para listar todas as URLs associadas aos serviços do Azure Dev Spaces:

```cmd
azds list-uris
```

Se uma URL estiver no estado *Pendente*, isso significa que o Azure Dev Spaces ainda está aguardando a conclusão do registro DNS. Às vezes, leva alguns minutos para que esse registro seja concluído. O Azure Dev Spaces também abre um túnel de localhost para cada serviço, que pode ser usado enquanto aguarda o registro DNS.

Se uma URL permanecer no estado *Pendente* por mais de 5 minutos, isso pode indicar um problema com o pod DNS externo que cria o ponto de extremidade público e/ou o pod controlador de entrada nginx que adquire o ponto de extremidade público. Você pode usar os comandos a seguir para excluir esses pods. Eles serão recriados automaticamente.

```cmd
kubectl delete pod -n kube-system -l app=addon-http-application-routing-external-dns
kubectl delete pod -n kube-system -l app=addon-http-application-routing-nginx-ingress
```

## <a name="error-required-tools-and-configurations-are-missing"></a>Erro "Ferramentas e configurações necessárias estão ausentes"

Este erro pode ocorrer ao iniciar o VS Code: "Ferramentas e configurações do [Azure Dev Spaces] necessárias para compilar e depurar '[nome do projeto]' estão ausentes."
O erro significa que azds.exe não está na variável de ambiente PATH, como visto no VS Code.

### <a name="try"></a>Experimente:

Inicie o VS Code de um prompt de comando em que a variável de ambiente PATH está definida corretamente.

## <a name="error-required-tools-to-build-and-debug-projectname-are-out-of-date"></a>Erro "As ferramentas necessárias para compilar e depurar 'projectname' estão desatualizadas."

Esse erro será exibido no Visual Studio Code se você tiver uma versão mais recente da extensão do VS Code para o Azure Dev Spaces, mas uma versão anterior da CLI do Azure Dev Spaces.

### <a name="try"></a>Experimente

Baixe e instale a última versão da CLI do Azure Dev Spaces:

* [Windows](http://aka.ms/get-azds-windows)
* [Mac](http://aka.ms/get-azds-mac)
* [Linux](https://aka.ms/get-azds-linux)

## <a name="error-azds-is-not-recognized-as-an-internal-or-external-command-operable-program-or-batch-file"></a>O erro "azds" não é reconhecido como um comando interno ou externo, programa operável ou arquivo em lote
 
Você poderá ver esse erro se azds.exe não estiver instalado ou configurado corretamente.

### <a name="try"></a>Experimente:

1. Verifique se azds.exe está no local %ProgramFiles%/Microsoft SDKs\Azure\CLI do Azure Dev Spaces (Versão Prévia). Se estiver lá, adicione o local à variável de ambiente PATH.
2. Se azds.exe não estiver instalado, execute o seguinte comando:

    ```cmd
    az aks use-dev-spaces -n <cluster-name> -g <resource-group>
    ```

## <a name="warning-dockerfile-could-not-be-generated-due-to-unsupported-language"></a>Aviso 'O Dockerfile não pôde ser gerado devido a um idioma não suportado'
O Azure Dev Spaces fornece suporte nativo para C# e Node.js. Quando você executar *azds prep* em um diretório que contenha código escrito em um desses idiomas, o Azure Dev Spaces criará automaticamente um Dockerfile apropriado para você.

Você ainda pode usar os Espaços de Desenvolvimento do Azure com código escrito em outros idiomas, mas precisará criar o Dockerfile você mesmo antes de executar o *azds up* pela primeira vez.

### <a name="try"></a>Experimente:
Se seu aplicativo for escrito em um idioma que o Azure Dev Spaces não oferece suporte nativo, você precisará fornecer um Dockerfile apropriado para criar uma imagem de contêiner executando seu código. O Docker fornece uma lista de [melhores práticas para gravar Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/), bem como uma [referência Dockerfile](https://docs.docker.com/engine/reference/builder/) que pode ajudá-lo a gravar um Dockerfile que se ajuste às suas necessidades.

Depois que você tiver um Dockerfile apropriado em vigor, você poderá continuar executando *azds up* para executar seu aplicativo no Azure Dev Spaces.

## <a name="error-upstream-connect-error-or-disconnectreset-before-headers"></a>Erro 'erro de conexão de upstream ou desconectar/reiniciar antes dos cabeçalhos'
É possível ver esse erro ao tentar acessar o serviço. Por exemplo, ao acessa a URL do serviço em um navegador. 

### <a name="reason"></a>Motivo 
A porta do contêiner não está disponível. Esse problema pode ocorrer porque: 
* O contêiner ainda está em processo de ser compilado e implantado. Esse problema poderá ocorrer se você executar `azds up` ou iniciar o depurador e, em seguida, tentar acessar o contêiner antes dele ser implantado com êxito.
* A configuração de porta não é uniforme em todo o _Dockerfile_, Helm Chart e em qualquer código de servidor que abra uma porta.

### <a name="try"></a>Experimente:
1. Se o contêiner estiver sendo compilado/implantado, você poderá aguardar de 2 a 3 segundos e tentar acessar o serviço novamente. 
1. Verifique a configuração de porta. Os números de porta especificados devem ser **idênticos** em todos os ativos abaixo:
    * **Dockerfile:** Especificado pela instrução `EXPOSE`.
    * **[Pacote do Helm](https://docs.helm.sh):** Especificado pelos valores `externalPort` e `internalPort` para um serviço (geralmente localizado em um arquivo `values.yml`),
    * Quaisquer portas sendo abertas no código do aplicativo, por exemplo, no Node.js: `var server = app.listen(80, function () {...}`


## <a name="config-file-not-found"></a>Arquivo de configuração não encontrado
Você executa `azds up` e obtém o erro a seguir: `Config file not found: .../azds.yaml`

### <a name="reason"></a>Motivo
É necessário executar `azds up` a partir do diretório raiz do código que deseja executar e inicializar a pasta de código para execução com o Azure Dev Spaces.

### <a name="try"></a>Experimente:
1. Altere o diretório atual para a pasta raiz que contém o código de serviço. 
1. Caso não tenha um arquivo _azds.yaml_ na pasta de código, execute `azds prep` para gerar ativos do Azure Dev Spaces, Docker e Kubernetes.

## <a name="error-the-pipe-program-azds-exited-unexpectedly-with-code-126"></a>Erro: 'O programa do pipe 'azds' saiu inesperadamente com o código 126.'
Iniciar o depurador de VS Code pode, às vezes, resultar nesse erro.

### <a name="try"></a>Experimente:
1. Feche e abra novamente o VS Code.
2. Pressione F5 novamente.

## <a name="debugging-error-failed-to-find-debugger-extension-for-typecoreclr"></a>Depurar erro 'Falha ao localizar a extensão do depurador para type:coreclr'
Executar o depurador de VS Code relata o erro: `Failed to find debugger extension for type:coreclr.`

### <a name="reason"></a>Motivo
Não é necessário ter a extensão do VS Code para C# instalada no computador de desenvolvimento. A extensão do C# inclui o suporte à depuração para .Net Core (CoreCLR).

### <a name="try"></a>Experimente:
Instalar a [extensão do VS Code para C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).

## <a name="debugging-error-configured-debug-type-coreclr-is-not-supported"></a>Erro de depuração 'não há suporte para tipo de depuração configurado 'coreclr' '
Executar o depurador de VS Code relata o erro: `Configured debug type 'coreclr' is not supported.`

### <a name="reason"></a>Motivo
Você não tem a extensão do VS Code para Azure Dev Spaces instalados no computador de desenvolvimento.

### <a name="try"></a>Experimente:
Instale a [Extensão do VS Code para Azure Dev Spaces](get-started-netcore.md).

## <a name="debugging-error-invalid-cwd-value-src-the-system-cannot-find-the-file-specified-or-launch-program-srcpath-to-project-binary-does-not-exist"></a>Erro de depuração "Invalid 'cwd' value '/src'. O sistema não pode localizar o arquivo especificado." ou "launch: o programa '/src/[caminho para o projeto binário] 'não existe "
Executar o depurador do VS Code relata o erro `Invalid 'cwd' value '/src'. The system cannot find the file specified.` e/ou `launch: program '/src/[path to project executable]' does not exist`

### <a name="reason"></a>Motivo
Por padrão, a extensão do VS Code usa `src` como o diretório de trabalho do projeto no contêiner. Se você atualizou `Dockerfile` para especificar um diretório de trabalho diferente, poderá visualizar esse erro.

### <a name="try"></a>Experimente:
Atualize o arquivo `launch.json` no subdiretório `.vscode` da pasta do projeto. Altere a diretiva `configurations->cwd` para apontar para o mesmo diretório que `WORKDIR` definiu no `Dockerfile` do projeto. Além disso, talvez seja necessário atualizar a diretiva `configurations->program`.

## <a name="the-type-or-namespace-name-mylibrary-could-not-be-found"></a>O tipo ou o nome do namespace 'MyLibrary' não foi encontrado

### <a name="reason"></a>Motivo 
O contexto de compilação está no nível de projeto/serviço por padrão, portanto, um projeto de biblioteca que você está usando não será encontrado.

### <a name="try"></a>Experimente:
O que precisa ser feito:
1. Modifique o arquivo _azds.yaml_ para configurar o contexto de compilação para o nível da solução.
2. Modifique os arquivos _Dockerfile_ e _Dockerfile.develop_ para fazer referência aos arquivos (_.csproj_) do projeto corretamente, relativos ao novo contexto de compilação.
3. Implante um arquivo _.dockerignore_ ao lado do arquivo .sln e modifique conforme necessário.

Você pode encontrar um exemplo em https://github.com/sgreenmsft/buildcontextsample

## <a name="microsoftdevspacesregisteraction-authorization-error"></a>Erro de autorização “Microsoft.DevSpaces/register/action"
Você pode ver o seguinte erro quando estiver gerenciando um Azure Dev Space e trabalhando em uma assinatura do Azure para a qual não possui acesso de Proprietário ou Colaborador.
`The client '<User email/Id>' with object id '<Guid>' does not have authorization to perform action 'Microsoft.DevSpaces/register/action' over scope '/subscriptions/<Subscription Id>'.`

### <a name="reason"></a>Motivo
A assinatura do Azure selecionada não registrou o namespace `Microsoft.DevSpaces`.

### <a name="try"></a>Experimente:
Alguém com acesso Proprietário ou de Colaborador à assinatura do Azure pode executar o comando da CLI do Azure a seguir para registrar manualmente o namespace `Microsoft.DevSpaces`:

```cmd
az provider register --namespace Microsoft.DevSpaces
```

## <a name="error-could-not-find-a-ready-tiller-pod-when-launching-dev-spaces"></a>“Erro: não foi possível encontrar um pod tiller pronto” ao abrir o Dev Spaces

### <a name="reason"></a>Motivo
Esse erro ocorrerá se o cliente do Helm não puder mais se comunicar com o pod Tiller em execução no cluster.

### <a name="try"></a>Experimente:
Reiniciar os nós de agente em seu cluster geralmente resolve esse problema.

## <a name="azure-dev-spaces-proxy-can-interfere-with-other-pods-running-in-a-dev-space"></a>o Azure Dev Spaces pode interferir com outros pods em execução em um espaço de desenvolvimento

### <a name="reason"></a>Motivo
Quando você habilita espaços de desenvolvimento em um namespace em seu cluster do AKS, um contêiner adicional chamado _mindaro proxy_ é instalado em cada um dos pods em execução dentro desse namespace. Esse contêiner intercepta as chamadas para os serviços no pod, que é parte integrante de recursos de desenvolvimento de equipe de desenvolvimento dos espaços.

Infelizmente, ele pode interferir com determinados serviços em execução nos pods. Especificamente, ele interfere nos pods que executam o Cache do Azure para Redis, causando erros de conexão e falhas na comunicação de mestre/subordinado.

### <a name="try"></a>Experimente:
Você pode mover o (s) pod de afetado (s) para um namespace dentro do cluster que _não_ tenha Espaços de desenvolvimento habilitados, enquanto continua executando o restante de seu aplicativo dentro de um namespace habilitado para Dev Spaces. Espaços de desenvolvimento não instalará o _mindaro proxy_ namespaces habilitados do contêiner dentro de espaços não - Dev.

## <a name="azure-dev-spaces-doesnt-seem-to-use-my-existing-dockerfile-to-build-a-container"></a>O Azure Dev Spaces parece não usar o Dockerfile existente para criar um contêiner 

### <a name="reason"></a>Motivo
O Azure Dev Spaces pode ser configurado para apontar para um _Dockerfile_ específico no projeto. Se parecer que o Azure Dev Spaces não está usando o _Dockerfile_ que você espera para compilar seus contêineres, talvez seja necessário informar explicitamente ao Azure Dev Spaces onde ele está. 

### <a name="try"></a>Experimente:
Abra o arquivo _azds.yaml_ que foi gerado pelo Azure Dev Spaces no projeto. Use a diretiva `configurations->develop->build->dockerfile` para apontar para o Dockerfile que você deseja usar:

```
...
configurations:
  develop:
    build:
      dockerfile: Dockerfile.develop
```
