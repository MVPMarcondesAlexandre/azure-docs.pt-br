---
title: 'Tutorial: Integração do Azure Active Directory ao Coupa | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Coupa.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2018
ms.author: jeedes
ms.openlocfilehash: 50d2e6a7ae1f34232a20e244ac65c2d3678f4f97
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55153923"
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Tutorial: Integração do Azure Active Directory ao Coupa

Neste tutorial, você aprende a integrar o Coupa ao Azure AD (Azure Active Directory).

A integração do Coupa ao Microsoft Azure AD oferece os seguintes benefícios:

- Você pode controlar no Microsoft Azure AD quem tem acesso ao Coupa.
- Você pode permitir que seus usuários entrem automaticamente no Coupa (Logon Único) com suas contas do Microsoft Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Microsoft Azure AD ao Coupa, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Coupa

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adição do Coupa a partir da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-coupa-from-the-gallery"></a>Adição do Coupa a partir da galeria
Para configurar a integração do Coupa ao Microsoft Azure AD, você precisa adicionar o Coupa à sua lista de aplicativos SaaS gerenciados a partir da galeria.

**Para adicionar o Coupa por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]

1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Coupa**, selecione **Coupa** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Coupa na lista de resultados](./media/coupa-tutorial/tutorial_coupa_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Microsoft Azure AD com o Coupa, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Microsoft Azure AD precisa saber qual usuário do Coupa é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Microsoft Azure AD e o usuário relacionado em Coupa.

No Coupa, atribua o valor do **nome de usuário** no Microsoft Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Microsoft Azure AD com o Coupa, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do Coupa](#create-a-coupa-test-user)** – para ter um equivalente de Brenda Fernandes no Coupa vinculado à representação do usuário no Microsoft Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Microsoft Azure AD no Portal do Azure e configurará o logon único no aplicativo Coupa.

**Para configurar o logon único do Microsoft Azure AD com o Coupa, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **Coupa**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.

    ![Caixa de diálogo Logon único](./media/coupa-tutorial/tutorial_coupa_samlbase.png)

1. Na seção **URLs e Domínio do Coupa**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Coupa](./media/coupa-tutorial/tutorial_coupa_url.png)

     a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.coupahost.com`

    > [!NOTE]
    > O valor da URL de logon não é real. Atualize esse valor com a URL de Logon real. Contate a [equipe de suporte ao Cliente do Coupa](https://success.coupa.com/Support/Contact_Us?) para obter esses valores.

    b. Na caixa de texto **Identificador**, digite a URL:

    | Ambiente  | URL |
    |:-------------|----|
    | Área restrita | `devsso35.coupahost.com`|
    | Produção | `prdsso40.coupahost.com`|
    | | |

    c. Na caixa de texto **URL de resposta**, digite a URL:

    | Ambiente | URL |
    |------------- |----|
    | Área restrita | `https://devsso35.coupahost.com/sp/ACS.saml2`|
    | Produção | `https://prdsso40.coupahost.com/sp/ACS.saml2`|
    | | |

1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/coupa-tutorial/tutorial_coupa_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/coupa-tutorial/tutorial_general_400.png)

1. Faça logon em seu site de empresa do Coupa como administrador.

1. Vá para **Configuração \> Controle de Segurança**.

   ![Controles de Segurança](./media/coupa-tutorial/ic791900.png "Controles de Segurança")

1. Na seção **Fazer Logon usando as credenciais do Coupa** , realize as seguintes etapas:

    ![Metadados SP do Coupa](./media/coupa-tutorial/ic791901.png "Metadados SP do Coupa")

     a. Selecione **Fazer logon usando o SAML**.

    b. Clique em **Procurar** para carregar os metadados baixados a partir do portal do Azure.

    c. Clique em **Salvar**.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/coupa-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/coupa-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/coupa-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/coupa-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.

### <a name="create-a-coupa-test-user"></a>Criar um usuário de teste do Coupa

Para permitir que os usuários do Azure AD façam logon no Coupa, eles devem ser provisionados no Coupa.  

* No caso do Coupa, o provisionamento é uma tarefa manual.

**Para configurar o provisionamento de usuários, execute as seguintes etapas:**

1. Faça logon em seu site de empresa do **Coupa** como administrador.

1. No menu na parte superior, clique em **Configuração** e em **Usuários**.

   ![Usuários](./media/coupa-tutorial/ic791908.png "Usuários")

1. Clique em **Criar**.

   ![Criar Usuários](./media/coupa-tutorial/ic791909.png "Criar Usuários")

1. Na seção **Criação de Usuário** , realize as seguintes etapas:

   ![Detalhes do Usuário](./media/coupa-tutorial/ic791910.png "Detalhes do Usuário")

    a. Digite os atributos **Logon**, **Nome**, **Sobrenome**, **ID de Logon Único** e **Email** de uma conta válida do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.

   b. Clique em **Criar**.

   >[!NOTE]
   >O titular da conta do Active Directory do Azure receberá um email com um link para confirmar a conta antes que ela se torne ativa.
   >

>[!NOTE]
>É possível usar qualquer outra ferramenta de criação da conta de usuário do Coupa ou as APIs fornecidas pelo Coupa para provisionar as contas de usuário do AAD.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Coupa.

![Atribuir a função de usuário][200]

**Para atribuir Brenda Fernandes ao Coupa, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201]

1. Na lista de aplicativos, escolha **Coupa**.

    ![O link do Coupa na lista de Aplicativos](./media/coupa-tutorial/tutorial_coupa_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Coupa no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo do Coupa.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/coupa-tutorial/tutorial_general_01.png
[2]: ./media/coupa-tutorial/tutorial_general_02.png
[3]: ./media/coupa-tutorial/tutorial_general_03.png
[4]: ./media/coupa-tutorial/tutorial_general_04.png

[100]: ./media/coupa-tutorial/tutorial_general_100.png

[200]: ./media/coupa-tutorial/tutorial_general_200.png
[201]: ./media/coupa-tutorial/tutorial_general_201.png
[202]: ./media/coupa-tutorial/tutorial_general_202.png
[203]: ./media/coupa-tutorial/tutorial_general_203.png
