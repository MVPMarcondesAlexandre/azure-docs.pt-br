---
title: 'Tutorial: Integração do Azure Active Directory ao Riskware | Microsoft Docs'
description: Saiba como configurar logon único entre o Azure Active Directory e o Riskware.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81866167-b163-4695-8978-fd29a25dac7a
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: jeedes
ms.openlocfilehash: 3b4c979bf03b23280c9389a043375f088624efe6
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55163238"
---
# <a name="tutorial-azure-active-directory-integration-with-riskware"></a>Tutorial: Integração do Azure Active Directory ao Riskware

Neste tutorial, você aprenderá a integrar o Riskware com Azure AD (Azure Active Directory).

A integração do Riskware com Azure AD fornece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao Riskware.
- Você pode permitir que seus usuários façam logon automaticamente no Riskware (logon único) com as contas do Azure AD deles.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com Riskware, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Riskware

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adição do Riskware da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-riskware-from-the-gallery"></a>Adição do Riskware da galeria
Para configurar a integração do Riskware ao Azure AD, você precisa adicionar o Riskware da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar Riskware da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]

1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Riskware**, selecione **Riskware** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Riskware na lista de resultados](./media/riskware-tutorial/tutorial_riskware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Riskware, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Riskware é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Riskware.

Para configurar e testar o logon único do Azure AD com o Riskware, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar de um usuário de teste do Riskware](#create-a-riskware-test-user)** – para ter um equivalente de Brenda Fernandes no Riskware vinculado à representação do usuário no Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo Riskware.

**Para configurar o logon único do Azure AD com Riskware, execute as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Riskware**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.

    ![Caixa de diálogo Logon único](./media/riskware-tutorial/tutorial_riskware_samlbase.png)

1. Na seção **Domínio e URLs do Riskware**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Riskware](./media/riskware-tutorial/tutorial_riskware_url.png)

     a. Na caixa de texto **URL de Entrada**, digite uma URL usando o padrão a seguir:
    | Ambiente| Padrão de URL|
    |--|--|
    | UAT|  `https://riskcloud.net/uat?ccode=<COMPANYCODE>` |
    | PROD| `https://riskcloud.net/prod?ccode=<COMPANYCODE>` |
    | DEMO| `https://riskcloud.net/demo?ccode=<COMPANYCODE>` |
    |||

    b. Na caixa de texto **Identificador (ID da Entidade)**, digite uma URL:
    | Ambiente| Padrão de URL|
    |--|--|
    | UAT| `https://riskcloud.net/uat` |
    | PROD| `https://riskcloud.net/prod` |
    | DEMO| `https://riskcloud.net/demo` |
    |||

    > [!NOTE]
    > O valor da URL de Entrada não é real. Atualize o valor com a URL de Logon real. Contate a [equipe de suporte ao Cliente Riskware](mailto:support@pansoftware.com.au) para obter o valor.

1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/riskware-tutorial/tutorial_riskware_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/riskware-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Riskware**, clique em **Configurar o Riskware** para abrir a janela **Configurar logon**. Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**

    ![Configuração do Riskware](./media/riskware-tutorial/tutorial_riskware_configure.png)

1. Em outra janela do navegador da Web, entre em seu site empresarial do Riskware como um administrador.

1. No canto superior direito, clique em **Manutenção** para abrir a página de manutenção.

    ![Configurações de manutenção do Riskware](./media/riskware-tutorial/tutorial_riskware_maintain.png)

1. Na página de manutenção, clique em **Autenticação**.

    ![Configuração de autenticação do Riskware](./media/riskware-tutorial/tutorial_riskware_authen.png)

1. Na página **Configuração de Autenticação**, execute as seguintes etapas:

    ![Configuração authenconfig do Riskware](./media/riskware-tutorial/tutorial_riskware_config.png)

     a. Selecione **Digite** como **SAML** para autenticação.

    b. In the **Code** textbox, type your code like AZURE_UAT.

    c. Na caixa de texto **Descrição**, digite sua descrição como AZURE Configuration for SSO.

    d. Na caixa de texto **Página de Logon Único**, cole a **URL do Serviço de Logon Único do SAML** copiado do portal do Azure.

    e. Na caixa de texto **Página de Saída**, cole o a **URL de Saída** copiado do portal do Azure.

    f. Na caixa de texto **Campo Postagem do Formulário**, digite o nome do campo presente em Postar Resposta que contém SAML, como SAMLResponse

    g. Na caixa de texto **Nome da Marca de Identidade XML**, digite o atributo que contém o identificador exclusivo na resposta SAML, como NameID.

    h. Abra o **XML de Metadados** baixado do portal do Azure no Bloco de notas, copie o certificado do arquivo de Metadados e cole-o na caixa de texto **Certificado**

    i. Na caixa de texto **URL do Consumidor**, cole o valor da **URL de Resposta**, que você recebe da equipe de suporte.

    j. Na caixa de texto **Emissor**, cole o valor do **Identificador**, que você recebe da equipe de suporte.

    > [!Note]
    > Contate a [equipe de suporte ao Cliente Riskware](mailto:support@pansoftware.com.au) para obter esses valores

    k. Selecione a caixa de seleção **Usar POST**.

    l. Selecione a caixa de seleção **Usar solicitação de SAML**.

    m. Clique em **Salvar**.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/riskware-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/riskware-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/riskware-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/riskware-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.

### <a name="create-a-riskware-test-user"></a>Criar um usuário de teste Riskware

Para permitir que os usuários do Microsoft Azure Active Directory entre no Riskware, eles devem ser provisionados no Riskware. No Riskware, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Entre no Riskware como Administrador de Segurança.

1. No canto superior direito, clique em **Manutenção** para abrir a página de manutenção. 

    ![Configuração de manutenções do Riskware](./media/riskware-tutorial/tutorial_riskware_maintain.png)

1. Na página de manutenção, clique em **Pessoas**.

    ![Configuração Pessoas do Riskware](./media/riskware-tutorial/tutorial_riskware_people.png)

1. Na guia **Detalhes**, execute as seguintes etapas:

    ![Detalhes da configuração do Riskware](./media/riskware-tutorial/tutorial_riskware_details.png)

     a. Selecione **Tipo de Pessoa**, como Funcionário.

    b. Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.

    c. Na caixa de texto **Sobrenome**, digite o sobrenome do usuário, como **Brenda**.

1. Na guia **Segurança** , realize as seguintes etapas:

    ![Configuração de segurança do Riskware](./media/riskware-tutorial/tutorial_riskware_security.png)

     a. Na seção **Autenticação**, selecione o modo **Autenticação**, que você configurou como Configuração do AZURE para SSO.

    b. Na seção **Detalhes do Logon**, na caixa de texto **ID de Usuário**, insira o email do usuário como **brittasimon@contoso.com**.

    c. Na caixa de texto **Senha**, insira a senha do usuário.

1. Na guia **Organização**, execute as seguintes etapas:

    ![Configuração da Organização do Riskware](./media/riskware-tutorial/tutorial_riskware_org.png)

     a. Selecione a opção como organização **Level1**.

    b. Na seção **Local de Trabalho Principal da Pessoa**, na caixa de texto **Local**, digite o local.

    c. Na seção **Funcionário**, selecione **Status do Funcionário** como Casual.

1. Clique em **Salvar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure, concedendo acesso ao Riskware.

![Atribuir a função de usuário][200]

**Para atribuir Brenda Fernandes ao Riskware, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, escolha **Riskware**.

    ![O link do Riskware na lista de Aplicativos](./media/riskware-tutorial/tutorial_riskware_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Riskware no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Riskware.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/riskware-tutorial/tutorial_general_01.png
[2]: ./media/riskware-tutorial/tutorial_general_02.png
[3]: ./media/riskware-tutorial/tutorial_general_03.png
[4]: ./media/riskware-tutorial/tutorial_general_04.png

[100]: ./media/riskware-tutorial/tutorial_general_100.png

[200]: ./media/riskware-tutorial/tutorial_general_200.png
[201]: ./media/riskware-tutorial/tutorial_general_201.png
[202]: ./media/riskware-tutorial/tutorial_general_202.png
[203]: ./media/riskware-tutorial/tutorial_general_203.png

