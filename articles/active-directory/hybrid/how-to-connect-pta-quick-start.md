---
title: Autenticação de passagem do Azure AD – Início rápido | Microsoft Docs
description: Este artigo descreve como começar a usar a autenticação de passagem do Azure AD (Azure Active Directory).
services: active-directory
keywords: Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único
documentationcenter: ''
author: billmath
manager: daveba
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 11/27/2018
ms.subservice: hybrid
ms.author: billmath
ms.openlocfilehash: 6cde81fd647c4f0eb4923bf9e69cf618f6f2d53a
ms.sourcegitcommit: 5978d82c619762ac05b19668379a37a40ba5755b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55494785"
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Autenticação de passagem do Azure Active Directory: Início rápido

## <a name="deploy-azure-ad-pass-through-authentication"></a>Implantar a autenticação de passagem do Azure AD

A autenticação de passagem do Azure Active Directory (Azure AD) permite que os usuários entrem em aplicativos locais e baseados em nuvem usando as mesmas senhas. Ela permite a entrada de usuários validando suas senhas diretamente no Active Directory local.

>[!IMPORTANT]
>Se você estiver migrando do AD FS (ou outras tecnologias de federação) para Autenticação de Passagem, é altamente recomendável seguir nosso guia detalhado de implantação publicado [aqui](https://aka.ms/adfstoPTADPDownload).

Siga estas instruções para implantar a Autenticação de Passagem no seu locatário:

## <a name="step-1-check-the-prerequisites"></a>Etapa 1: Verificar os pré-requisitos

Verifique se os pré-requisitos a seguir estão em vigor.

### <a name="in-the-azure-active-directory-admin-center"></a>No centro de administração do Azure Active Directory

1. Crie uma conta de administrador global somente em nuvem no seu locatário do Azure AD. Dessa forma, você pode gerenciar a configuração do seu locatário caso seus serviços locais falhem ou fiquem indisponíveis. Saiba mais sobre [adicionar uma conta de administrador global somente em nuvem](../active-directory-users-create-azure-portal.md). A conclusão dessa etapa é essencial para garantir que você não seja bloqueado de seu locatário.
2. Adicione um ou mais [nomes de domínio personalizados](../active-directory-domains-add-azure-portal.md) ao seu locatário do Azure AD. Os usuários podem entrar com um desses nomes de domínio.

### <a name="in-your-on-premises-environment"></a>Em seu ambiente local

1. Identifique um servidor que execute o Windows Server 2012 R2 ou posterior para executar o Azure AD Connect. Se já não foi habilitado, [habilite o TLS 1.2 no servidor](./how-to-connect-install-prerequisites.md#enable-tls-12-for-azure-ad-connect). Adicione o servidor à mesma floresta do Active Directory dos usuários cujas senhas você precisa validar.
2. Instale a [última versão do Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) no servidor identificado na etapa anterior. Se o Azure AD Connect já está em execução, verifique se a versão é a 1.1.750.0 ou posterior.

    >[!NOTE]
    >As versões 1.1.557.0, 1.1.558.0, 1.1.561.0 e 1.1.614.0 do Azure AD Connect têm um problema relacionado à sincronização de hash de senha. Se você _não_ pretende usar a sincronização de hash de senha em conjunto com a Autenticação de passagem, leia as [Notas de versão do Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/reference-connect-version-history#116470).

3. Identifique um ou mais servidores adicionais (que execute o Windows Server 2012 R2 ou posterior, com o TLS 1.2 habilitado) no qual você possa executar Agentes de Autenticação autônomos. Esses servidores adicionais são necessários para garantir a alta disponibilidade de solicitações de entrada. Adicione os servidores à mesma floresta do Active Directory dos usuários cujas senhas você precisa validar.

    >[!IMPORTANT]
    >Em ambientes de produção, recomendamos ter um mínimo de três Agentes de Autenticação em execução no seu locatário. Há um limite do sistema de 12 Agentes de Autenticação por locatário. Como melhor prática, trate todos os servidores que estão executando Agentes de Autenticação como sistemas de Camada 0 (veja a [referência](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material)).

4. Se houver um firewall entre os servidores e o Azure AD, configure os seguintes itens:
   - Certifique-se de que os Agentes de Autenticação podem fazer solicitações de *saída* ao Azure AD sobre as seguintes portas:

     | Número da porta | Como ele é usado |
     | --- | --- |
     | **80** | Baixa as listas de certificados revogados (CRLs) enquanto valida o certificado SSL |
     | **443** | Lida com toda a comunicação de saída com o serviço |
     | **8080** (opcional) | Agentes de Autenticação relatam seu status de cada dez minutos através da porta 8080, se a porta 443 não estiver disponível. Esse status é exibido no portal do Azure Active Directory. A porta 8080 _não_ é usada para entradas do usuário. |
     
     Se o firewall impõe as regras de acordo com os usuários originadores, abra essas portas para o tráfego proveniente dos serviços Windows que são executados como um serviço de rede.
   - Se o seu firewall ou proxy permitirem lista de permissões de DNS, adicione as conexões a **\*msappproxy.net** e **\*servicebus.windows.net** à lista de permissões. Caso contrário, permita o acesso aos [Intervalos de IP do datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653), os quais são atualizados semanalmente.
   - Os seus Agentes de autenticação devem acessar **login.windows.net** e **login.microsoftonline.net** para o registro inicial. Abra seu firewall para essas URLs também.
   - Para validação de certificado, desbloqueie as seguintes URLs: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** e **www.microsoft.com:80**. Uma vez que essas URLs são usadas para a validação de certificado com outros produtos da Microsoft, você talvez já tenha essas URLs desbloqueadas.

## <a name="step-2-enable-the-feature"></a>Etapa 2: habilitar o recurso

Habilite a Autenticação de passagem por meio do [Azure AD Connect](whatis-hybrid-identity.md).

>[!IMPORTANT]
>É possível habilitar a Autenticação de passagem no servidor primário ou de preparo do Azure AD Connect. É altamente recomendável habilitá-la do servidor primário. Se você estiver configurando um servidor de preparo do Azure AD Connect no futuro, você **devem** continuar para escolher a autenticação de passagem como a opção de entrada; escolhendo outra opção será **desabilitar** Autenticação de passagem no locatário e substituir a configuração no servidor primário.

Se estiver instalando o Azure AD Connect pela primeira vez, escolha o [caminho de instalação personalizado](how-to-connect-install-custom.md). Na página **Entrada de usuário** escolha **Autenticação de Passagem** como o **Método de logon**. Após a conclusão bem-sucedida, um Agente de autenticação de passagem estará instalado no mesmo servidor do Azure AD Connect. Além disso, o recurso de autenticação de passagem estará habilitado em seu locatário.

![Azure AD Connect: Entrada do usuário](./media/how-to-connect-pta-quick-start/sso3.png)

Se já tiver instalado o Azure AD Connect usando o caminho de [instalação expressa](how-to-connect-install-express.md) ou de [instalação personalizada](how-to-connect-install-custom.md), selecione a tarefa **Alterar entrada do usuário** no Azure AD Connect e selecione **Avançar**. Depois selecione **Autenticação de Passagem** como o método de entrada. Após a conclusão bem-sucedida, um Agente de autenticação de passagem estará instalado no mesmo servidor que o Azure AD Connect, e o recurso estará habilitado em seu locatário.

![Azure AD Connect: Alterar a entrada do usuário](./media/how-to-connect-pta-quick-start/changeusersignin.png)

>[!IMPORTANT]
>A Autenticação de Passagem é um recurso no nível do locatário. A ativação desse recurso afeta a entrada de usuários em _todos_ os domínios gerenciados no seu locatário. Se estiver alternando dos Serviços de Federação do Active Directory (AD FS) para Autenticação de passagem, você deve esperar pelo menos 12 horas antes de desligar a infraestrutura do AD FS. Esse tempo de espera é para garantir que os usuários continuem entrando no Exchange ActiveSync durante a transição. Para obter mais ajuda sobre a migração do AD FS para Autenticação de Passagem, veja o nosso plano detalhado de implantação publicado [aqui](https://aka.ms/adfstoptadpdownload).

## <a name="step-3-test-the-feature"></a>Etapa 3: Testar o recurso

Siga estas instruções para verificar se você habilitou a Autenticação de passagem corretamente:

1. Entre no [Centro de administração do Azure Active Directory](https://aad.portal.azure.com) com as credenciais do administrador global do seu locatário.
2. Selecione **Azure Active Directory** no painel esquerdo.
3. Selecione **Azure AD Connect**.
4. Verifique se o recurso **Autenticação de passagem** aparece como **Habilitado**.
5. Selecione **Autenticação de passagem**. Esse painel da **Autenticação de passagem** lista os servidores em que os Agentes de autenticação estão instalados.

![Centro de administração do Azure Active Directory: painel do Azure AD Connect](./media/how-to-connect-pta-quick-start/pta7.png)

![Centro de administração do Azure Active Directory: painel de autenticação de passagem](./media/how-to-connect-pta-quick-start/pta8.png)

Nesse momento, os usuários de todos os domínios gerenciados no seu locatário podem entrar usando a Autenticação de passagem. No entanto, os usuários de domínios federados continuam a entrar usando o AD FS ou outro provedor de federação que já esteja configurado. Se você converter um domínio de federado para gerenciado, todos os usuários nesse domínio passarão automaticamente a entrar usando a Autenticação de passagem. O recurso de Autenticação de passagem os não afeta os usuários somente de nuvem.

## <a name="step-4-ensure-high-availability"></a>Etapa 4: garantir a alta disponibilidade

Se você planeja implantar autenticação de passagem em um ambiente de produção, instale um Agente de Autenticação autônomo. Instale esses Agentes de Autenticação no(s) servidor(es) _diferente(s)_ do que está executando o Azure AD Connect. Esta configuração fornece alta disponibilidade para solicitações de entrada de usuário.

>[!IMPORTANT]
>Em ambientes de produção, recomendamos ter um mínimo de três Agentes de Autenticação em execução no seu locatário. Há um limite do sistema de 12 Agentes de Autenticação por locatário. Como melhor prática, trate todos os servidores que estão executando Agentes de Autenticação como sistemas de Camada 0 (veja a [referência](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material)).

Siga estas instruções para fazer o download do software do Agente de Autenticação:

1. Para fazer o download da versão mais recente do Agente de Autenticação (versões 1.5.193.0 ou posteriores), entre no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) com as credenciais de administrador global do seu locatário.
2. Selecione **Azure Active Directory** no painel esquerdo.
3. Selecione **Azure AD Connect**, **Autenticação de passagem** e depois **Baixar Agente**.
4. Selecione o botão **Aceitar termos e baixar**.

![Centro de administração do Azure Active Directory: botão Baixar o Agente de Autenticação](./media/how-to-connect-pta-quick-start/pta9.png)

![Centro de administração do Azure Active Directory: painel Baixar Agente](./media/how-to-connect-pta-quick-start/pta10.png)

>[!NOTE]
>Você também pode [baixar o software Agente de Autenticação](https://aka.ms/getauthagent) diretamente. Leia e aceite os [Termos de Serviço](https://aka.ms/authagenteula) do Agente de Autenticação _antes_ de instalá-lo.

Existem duas formas de implantar um Agente de Autenticação autônomo:

Primeiro, você pode fazer isso de forma interativa simplesmente executando o executável do Agente de Autenticação baixado e fornecendo credenciais de administrador global do locatário quando solicitado.

Segundo, você pode criar e executar um script de implantação autônomo. Isso é útil quando você deseja implantar vários Agentes de Autenticação ao mesmo tempo, ou instalar Agentes de Autenticação em servidores Windows que não possuem a interface do usuário ativada ou que você não pode acessar com a Área de Trabalho Remota. Aqui estão as instruções sobre como usar essa abordagem:

1. Execute o seguinte comando para instalar um Agente de Autenticação: `AADConnectAuthAgentSetup.exe REGISTERCONNECTOR="false" /q`.
2. Você pode registrar o Agente de Autenticação com nosso serviço usando o Windows PowerShell. Crie um objeto de credenciais do PowerShell `$cred` que contém um nome de usuário de administrador global e uma senha para seu locatário. Execute o seguinte comando, substituindo *\<nome de usuário\>* e *\<senha\>*:

        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
3. Vá para **C:\Arquivos de Programas\Microsoft Azure AD Connect Authentication Agent** e execute o seguinte script usando o objeto `$cred` que você criou:

        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft Azure AD Connect Authentication Agent\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred -Feature PassthroughAuthentication

## <a name="next-steps"></a>Próximas etapas
- [Migrar do AD FS para Autenticação de Passagem](https://aka.ms/adfstoptadp) – um guia detalhado para migrar do AD FS (ou outras tecnologias de federação) para Autenticação de Passagem.
- [Bloqueio Inteligente](../authentication/howto-password-smart-lockout.md): saiba como configurar o recurso Bloqueio Inteligente no seu locatário para proteger as contas de usuário.
- [Limitações atuais](how-to-connect-pta-current-limitations.md): saiba quais cenários têm suporte na Autenticação de passagem e quais não têm.
- [Análise técnica aprofundada](how-to-connect-pta-how-it-works.md): entenda como funciona o recurso Autenticação de passagem.
- [Perguntas frequentes](how-to-connect-pta-faq.md): encontre respostas para as perguntas frequentes.
- [Solucionar problemas](tshoot-connect-pass-through-authentication.md): saiba como resolver problemas comuns com o recurso Autenticação de passagem.
- [Análise aprofundada sobre segurança](how-to-connect-pta-security-deep-dive.md): obtenha informações técnicas sobre o recurso Autenticação de passagem.
- [SSO contínuo do Azure AD](how-to-connect-sso.md): saiba mais sobre este recurso complementar.
- [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): use o Fórum do Azure Active Directory para gerar novas solicitações de recursos.
