---
title: 'Tutorial: Integração do Azure Active Directory com o Picturepark | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 10ddfa2f7b2b17c23da1e67474a4b464780bc2e6
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55163638"
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Tutorial: Integração do Azure Active Directory com o Picturepark

Neste tutorial, você aprende a integrar o Picturepark ao Azure AD (Azure Active Directory).

A integração do Picturepark ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Picturepark
- É possível permitir que os usuários se conectem automaticamente ao Picturepark (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Picturepark, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Picturepark

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Picturepark por meio da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-picturepark-from-the-gallery"></a>Adicionando o Picturepark por meio da galeria
Para configurar a integração do Picturepark ao Azure AD, é necessário adicionar o Picturepark à lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Picturepark por meio da galeria, realize as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Picturepark**.

    ![Criação de um usuário de teste do AD do Azure](./media/picturepark-tutorial/tutorial_picturepark_search.png)

1. No painel de resultados, selecione **Picturepark** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Picturepark, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Picturepark é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Picturepark.

No Picturepark, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Picturepark, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criando um usuário de teste do Picturepark](#creating-a-picturepark-test-user)** – para ter um equivalente de Brenda Fernandes no Picturepark que esteja vinculado à representação de usuário do Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Picturepark.

**Para configurar o logon único do Azure AD com o Picturepark, realize as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Picturepark**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/picturepark-tutorial/tutorial_picturepark_samlbase.png)

1. Na seção **Domínio e URLs do Picturepark**, realize as seguintes etapas:

    ![Configurar o logon único](./media/picturepark-tutorial/tutorial_picturepark_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.picturepark.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte ao Cliente do Picturepark](https://picturepark.com/about/contact/) para obter esses valores. 
 
1. Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.

    ![Configurar o logon único](./media/picturepark-tutorial/tutorial_picturepark_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/picturepark-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Picturepark**, clique em **Configurar o Picturepark** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar o logon único](./media/picturepark-tutorial/tutorial_picturepark_configure.png) 

1. Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Picturepark como administrador.

1. Na barra de ferramentas na parte superior, clique em **Ferramentas administrativas** e em **Console de Gerenciamento**.
   
    ![Console de Gerenciamento](./media/picturepark-tutorial/ic795062.png "Console de Gerenciamento")

1. Clique em **Autenticação** e em **Provedores de identidade**.
   
    ![Autenticação](./media/picturepark-tutorial/ic795063.png "Autenticação")

1. Na seção **Configuração do provedor de identidade** , realize as seguintes etapas:
   
    ![Configuração do Provedor de Identidade](./media/picturepark-tutorial/ic795064.png "Configuração do Provedor de Identidade")
   
    a. Clique em **Adicionar**.
  
    b. Digite um nome para sua configuração.
   
    c. Selecione **Definir como padrão**.
   
    d. Na caixa de texto **URI do Emissor**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.
   
    e. Na caixa de texto **Impressão Digital do Emissor Confiável**, cole o valor da **Impressão Digital** copiado da seção **Certificado de Autenticação SAML**. 

1. Clique em **JoinDefaultUsersGroup**.

1. Para definir o atributo **Emailaddress** na caixa de texto **Declaração**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e clique em **Salvar**.

      ![Configuração](./media/picturepark-tutorial/ic795065.png "Configuração")

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/picturepark-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/picturepark-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/picturepark-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/picturepark-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-picturepark-test-user"></a>Criando um usuário de teste do Picturepark

Para permitir que os usuários do AD do Azure façam logon no Picturepark, eles devem ser provisionados no Picturepark. No caso do Picturepark, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon em seu locatário do **Picturepark** .

1. Na barra de ferramentas na parte superior, clique em **Ferramentas administrativas** e em **Usuários**.
   
    ![Usuários](./media/picturepark-tutorial/ic795067.png "Usuários")

1. Na guia **Visão geral de usuários**, clique em **Novo**.
   
    ![Gerenciamento de usuário](./media/picturepark-tutorial/ic795068.png "Gerenciamento de usuário")

1. Na caixa de diálogo **Criar Usuário**, realize as seguintes etapas de um Usuário válido do Azure Active Directory que você deseja provisionar:
   
    ![Criar usuário](./media/picturepark-tutorial/ic795069.png "Criar usuário")
   
    a. Na caixa de texto **Endereço de Email**, digite o **endereço de email** do usuário **BrittaSimon@contoso.com**.  
   
    b. Nas caixas de texto **Senha** e **Confirmar Senha**, digite a **senha** de BrendaFernandes. 
   
    c. Na caixa de texto **Nome**, digite o **Nome** do usuário **Brenda**. 
   
    d. Na caixa de texto **Sobrenome**, digite o **Sobrenome** do usuário **Fernandes**.
   
    e. Na caixa de texto **Empresa**, digite o **Nome da empresa** do usuário. 
   
    f. Na caixa de texto **País/Região**, selecione o **País/Região** do usuário.
  
    g. Na caixa de texto **CEP**, digite o **CEP** da cidade.
   
    h. Na caixa de texto **Cidade**, digite o **Nome da cidade** do usuário.

    i. Selecione um **Idioma**.
   
    j. Clique em **Criar**.

>[!NOTE]
>Você pode usar qualquer outra ferramenta de criação de conta de usuário do Picturepark ou as APIs fornecidas pelo Picturepark para provisionar contas de usuário do Azure AD.
> 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Picturepark.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Picturepark, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Picturepark**.

    ![Configurar o logon único](./media/picturepark-tutorial/tutorial_picturepark_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco do Picturepark no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Picturepark. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/picturepark-tutorial/tutorial_general_01.png
[2]: ./media/picturepark-tutorial/tutorial_general_02.png
[3]: ./media/picturepark-tutorial/tutorial_general_03.png
[4]: ./media/picturepark-tutorial/tutorial_general_04.png

[100]: ./media/picturepark-tutorial/tutorial_general_100.png

[200]: ./media/picturepark-tutorial/tutorial_general_200.png
[201]: ./media/picturepark-tutorial/tutorial_general_201.png
[202]: ./media/picturepark-tutorial/tutorial_general_202.png
[203]: ./media/picturepark-tutorial/tutorial_general_203.png

