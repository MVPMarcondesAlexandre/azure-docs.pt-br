---
author: diberry
ms.author: diberry
ms.service: cognitive-services
ms.topic: include
ms.date: 01/24/2019
ms.openlocfilehash: 08e6b5d109d6647f2a291f117f4993bae7598464
ms.sourcegitcommit: a7331d0cc53805a7d3170c4368862cad0d4f3144
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55302270"
---
Você deve primeiro preencher e enviar o [formulário Solicitação de Contêineres de Visão dos Serviços Cognitivos](https://aka.ms/VisionContainersPreview) para solicitar acesso ao contêiner. O formulário solicita informações sobre você, sua empresa e o cenário do usuário para o qual você usará o contêiner. Depois de submetida, a equipe de Serviços Cognitivos do Azure revisa o formulário para garantir que você atenda aos critérios de acesso ao registro do contêiner particular.

> [!IMPORTANT]
> Você deve usar um endereço de e-mail associado a uma Conta da Microsoft (MSA) ou uma conta do Microsoft Azure Active Directory (Azure AD) no formulário.

Se sua solicitação for aprovada, você receberá um e-mail com instruções descrevendo como obter suas credenciais e acessar o registro de contêiner privado.

## <a name="log-in-to-the-private-container-registry"></a>Efetue login no registro do contêiner particular

Há várias maneiras de autenticar com o registro de contêiner particular para Contêineres de Serviços Cognitivos, mas o método recomendado a partir da linha de comandos é usando a [CLI do Docker](https://docs.docker.com/engine/reference/commandline/cli/).

Use o comando [login do docker](https://docs.docker.com/engine/reference/commandline/login/), conforme mostrado no exemplo a seguir, para efetuar login no `containerpreview.azurecr.io`, o registro do contêiner particular para Contêineres de Serviços Cognitivos. Substitua *\<nome de usuário\>* pelo nome de usuário e *\<senha\>* com a senha fornecida nas credenciais recebidas da equipe do Azure Cognitive Services.

```docker
docker login containerpreview.azurecr.io -u <username> -p <password>
```

Se você tiver protegido suas credenciais em um arquivo de texto, poderá concatenar o conteúdo desse arquivo de texto, usando o `cat` comando, para o comando `docker login`, conforme mostrado no exemplo a seguir. Substitua *\<passwordFile\>* pelo caminho e nome do arquivo de texto que contém a senha e o *\<nome de usuário\>* com o nome de usuário fornecido em suas credenciais.

```docker
cat <passwordFile> | docker login containerpreview.azurecr.io -u <username> --password-stdin
```

