---
title: 'Tutorial: Integração do Azure Active Directory ao Pingboard | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 2011458183944d9e645ec0f08327a38b545df343
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55170276"
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Tutorial: Integração do Azure Active Directory ao Pingboard

Neste tutorial, você aprende a integrar o Pingboard ao Azure AD (Azure Active Directory).

A integração do Pingboard ao Azure AD oferece os seguintes benefícios:

- No Azure AD, você pode controlar quem tem acesso ao Pingboard
- Você pode permitir que os usuários se conectem automaticamente ao SSO (logon único) do Pingboard com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Pingboard, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do Pingboard habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o Pingboard por meio da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-pingboard-from-the-gallery"></a>Adicionar o Pingboard por meio da galeria
Para configurar a integração do Pingboard ao Azure AD, você precisa adicionar o Pingboard à sua lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Pingboard por meio da galeria, realize as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos Empresariais][2]

1. Clique em **adicionar** botão na parte superior da caixa de diálogo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Pingboard**, selecione **Pingboard** do painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Pingboard na lista de resultados](./media/pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Pingboard, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Pingboard é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Pingboard.

Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Pingboard.

Para configurar e testar o logon único do Azure AD com o Pingboard, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do Pingboard](#create-a-pingboard-test-user)** – para ter um equivalente de Brenda Fernandes no Pingboard que esteja vinculado à representação do usuário do Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no seu aplicativo Pingboard.

**Para configurar o logon único do Azure AD com o Pingboard, realize as seguintes etapas:**

1. No Portal do Azure, na página de integração do aplicativo **Pingboard**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1.  Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.

    ![Caixa de diálogo Logon único](./media/pingboard-tutorial/tutorial_pingboard_samlbase.png)

1. Na seção **Domínio e URLs do Pingboard**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IdP**:

    ![IDP de informações de logon único em Domínio e URLs do Pingboard](./media/pingboard-tutorial/tutorial_pingboard_url.png)

     a. Na caixa de texto **Identificador**, digite o valor como `http://app.pingboard.com/sp`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<entity-id>.pingboard.com/auth/saml/consume`

1. Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:

    ![SP de informações de logon único em Domínio e URLs do Pingboard](./media/pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

     Na caixa de texto **URL de Entrada**, digite a URL usando o seguinte padrão: `https://<sub-domain>.pingboard.com/sign_in`

    > [!NOTE]
    > Observe que esses valores não são reais. Atualize esses valores com a URL de Resposta e a URL de Logon reais. Contate a [equipe de suporte do Pingboard](https://support.pingboard.com/) para obter esses valores.

1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.

    ![XML de metadados do Pingboard](./media/pingboard-tutorial/tutorial_pingboard_certificate.png)

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/pingboard-tutorial/tutorial_general_400.png)

1. Para configurar o SSO no lado do Pingboard, abra uma nova janela do navegador e faça logon em sua conta do Pingboard. Você deve ser administrador do Pingboard para configurar o logon único.

1. No menu superior, selecione **Aplicativos > Integrações**

    ![Configurar o logon único](./media/pingboard-tutorial/Pingboard_integration.png)

1. Na página **Integrações**, localize o bloco **"Azure Active Directory"** e clique nele.

    ![Integração de logon único do Pingboard](./media/pingboard-tutorial/Pingboard_aad.png)

1. No modal que vem a seguir, clique em **"Configurar"**

    ![Botão de configuração do Pingboard](./media/pingboard-tutorial/Pingboard_configure.png)

1. Na página seguinte, você notará que a "Integração SSO do Azure está habilitada". Abra o arquivo Metadados XML baixado em um bloco de notas e cole o conteúdo em **Metadados IDP**.

    ![Tela de configuração de SSO do Pingboard](./media/pingboard-tutorial/Pingboard_sso_configure.png)

1. O arquivo está validado, e se tudo estiver correto, o logon único será habilitado.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/pingboard-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/pingboard-tutorial/create_aaduser_02.png)

1. Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.

    ![Botão Adicionar](./media/pingboard-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/pingboard-tutorial/create_aaduser_04.png)

     a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.

### <a name="create-a-pingboard-test-user"></a>Criando um usuário de teste do Pingboard

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Pingboard. O Pingboard dá suporte ao provisionamento automático de usuário, que é habilitado por padrão. Você pode encontrar [aqui](pingboard-provisioning-tutorial.md) mais detalhes de como configurar o provisionamento automático de usuário.

**Se você precisar criar o usuário manualmente, execute as seguintes etapas:**

1. Faça logon em seu site de empresa do Pingboard como administrador.

1. Clique no botão **"Adicionar Funcionário"** na página **Diretório**.

    ![Adicionar Funcionário](./media/pingboard-tutorial/create_testuser_add.png)

1. Na página de diálogo **“Adicionar Funcionário”** execute as seguintes etapas:

    ![Convidar Pessoas](./media/pingboard-tutorial/create_testuser_name.png)

     a. Na caixa de texto **Nome Completo Name**, digite o nome completo do usuário, como **Brenda Fernandes**.

    b. Na caixa de texto **Email**, digite o endereço de email do usuário, como **brittasimon@contoso.com**.

    c. Na caixa de texto **Cargo**, digite o cargo de Brenda Fernandes.

    d. Na lista suspensa **Local**, selecione o local de Brenda Fernandes.

    e. Clique em **Adicionar**.

1. Uma tela de confirmação será exibida para confirmar a adição do usuário.

    ![confirmar](./media/pingboard-tutorial/create_testuser_confirm.png)

    > [!NOTE]
    > O titular da conta do Azure Active Directory recebe um email e segue um link para confirmar sua conta antes que ela se torne ativa.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você habilita o Brenda Fernandes para usar o logon único do Azure, concedendo acesso ao Pingboard.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Pingboard, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Pingboard**.

    ![Link do Pingboard na lista de Aplicativos](./media/pingboard-tutorial/tutorial_pingboard_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

Ao clicar no bloco Pingboard no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Pingboard.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)
* [Configurar Provisionamento de Usuário](pingboard-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/pingboard-tutorial/tutorial_general_01.png
[2]: ./media/pingboard-tutorial/tutorial_general_02.png
[3]: ./media/pingboard-tutorial/tutorial_general_03.png
[4]: ./media/pingboard-tutorial/tutorial_general_04.png

[100]: ./media/pingboard-tutorial/tutorial_general_100.png

[200]: ./media/pingboard-tutorial/tutorial_general_200.png
[201]: ./media/pingboard-tutorial/tutorial_general_201.png
[202]: ./media/pingboard-tutorial/tutorial_general_202.png
[203]: ./media/pingboard-tutorial/tutorial_general_203.png
