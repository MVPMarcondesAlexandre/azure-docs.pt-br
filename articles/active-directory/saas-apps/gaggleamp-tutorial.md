---
title: 'Tutorial: Integração do Azure Active Directory com o GaggleAMP | Microsoft Docs'
description: Saiba como configurar o logon único entre o Active Directory do Azure e o GaggleAMP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2018
ms.author: jeedes
ms.openlocfilehash: ccb2e6be481c27661543ff0dc19e5b60b2aa8d8a
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55178249"
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a>Tutorial: Integração do Azure Active Directory com o GaggleAMP

Neste tutorial, você aprende a integrar o GaggleAMP ao Azure AD (Azure Active Directory).

A integração do GaggleAMP ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao GaggleAMP
- Você pode permitir seus usuários façam logon automaticamente no GaggleAMP (logon único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao GaggleAMP, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do GaggleAMP com logon único habilitado

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adição do GaggleAMP da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-gaggleamp-from-the-gallery"></a>Adição do GaggleAMP da galeria
Para configurar a integração do GaggleAMP com o Azure AD, você precisa adicionar o GaggleAMP à sua lista de aplicativos SaaS gerenciados a partir da galeria.

**Para adicionar o GaggleAMP a partir da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **GaggleAMP**.

    ![Criação de um usuário de teste do AD do Azure](./media/gaggleamp-tutorial/tutorial_gaggleamp_search.png)

1. No painel de resultados, selecione **GaggleAMP** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o GaggleAMP com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do GaggleAMP é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no GaggleAMP.

No GaggleAMP, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o GaggleAMP, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do GaggleAMP](#creating-a-gaggleamp-test-user)** – para ter um equivalente de Brenda Fernandes no GaggleAMP que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo GaggleAMP.

**Para configurar o logon único do Azure AD com o GaggleAMP, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **GaggleAMP**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

1. Na seção **Domínio e URLs do GaggleAMP**, execute as etapas a seguir se você quiser configurar o aplicativo no modo iniciado pelo **IDP**:

    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     Na caixa de texto **Identificador**, digite a URL: `https://accounts.gaggleamp.com/auth/saml/callback`

1. Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:

    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_gaggleamp_url1.png)

     Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://gaggleamp.com/i/<customerid>`

    > [!NOTE]
    > O valor da URL de logon não é real. Atualize esse valor com a URL de Entrada real. Contate a [equipe de suporte ao Cliente do GaggleAMP](mailto:sales@gaggleamp.com) para obter esse valor.
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do GaggleAMP**, clique em **Configurar GaggleAMP** para abrir a janela **Configurar logon**. Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

1. Em outra instância do navegador, navegue até a página de SSO de SAML criada para você pela equipe de suporte do Gaggle (por exemplo: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).

1. Na página **SSO de SAML** , execute as seguintes etapas:  
   
    ![Logon único do GaggleAMP](./media/gaggleamp-tutorial/tutorial_gaggleamp_06.png)

     a. Selecione **Outro** formulário no menu suspenso do **Provedor de identidade**.
    
    b. Na caixa de texto **Emissor do Provedor de Identidade**, cole o valor da **URL do Emissor do Certificado** que você copiou do Portal do Azure.
    
    c. Na caixa de texto **URL de Logon Único do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único** que você copiou do Portal do Azure.
    
    d. Abra o arquivo de **Certificado (Base64)** baixado no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado X.509**.
    
    e. Clique em **Salvar**.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/gaggleamp-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/gaggleamp-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/gaggleamp-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/gaggleamp-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-gaggleamp-test-user"></a>Criação de um usuário de teste do GaggleAMP

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no GaggleAMP. O GaggleAMP dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Um novo usuário é criado durante uma tentativa de acessar o GaggleAMP, caso ainda não exista. 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao GaggleAMP.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao GaggleAMP, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **GaggleAMP**.

    ![Configurar o logon único](./media/gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.

Ao clicar no bloco GaggleAMP no Painel de Acesso, você deve ser automaticamente conectado a seu aplicativo GaggleAMP.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/gaggleamp-tutorial/tutorial_general_203.png
