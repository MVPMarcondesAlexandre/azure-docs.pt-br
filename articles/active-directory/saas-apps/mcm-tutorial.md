---
title: 'Tutorial: Integração do Azure Active Directory com o MCM | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o MCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: b00d71cd326be850096e814c759949204040c3b5
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55152596"
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a>Tutorial: Integração do Azure Active Directory ao MCM

Neste tutorial, você aprenderá a integrar o MCM ao Azure AD (Azure Active Directory).

A integração do MCM ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao MCM
- Você pode permitir que seus usuários faça logon automaticamente no MCM (logon único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o MCM, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do MCM

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar MCM da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-mcm-from-the-gallery"></a>Adicionar MCM da galeria
Para configurar a integração do MCM com o Azure AD, você precisará adicionar o MCM à sua lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o MCM por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **MCM**.

    ![Criação de um usuário de teste do AD do Azure](./media/mcm-tutorial/tutorial_mcm_search.png)

1. No painel de resultados, selecione **MCM** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o MCM, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do MCM é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do MCM.

No MCM, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o MCM, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criar um usuário de teste do MCM](#creating-a-mcm-test-user)**: para ter um equivalente de Brenda Fernandes no MCM que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo MCM.

**Para configurar o logon único do Azure AD com o MCM, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **MCM**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/mcm-tutorial/tutorial_mcm_samlbase.png)

1. Na seção **URLs e Domínio do MCM**, execute as seguintes etapas:

    ![Configurar o logon único](./media/mcm-tutorial/tutorial_mcm_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://myaba.co.uk/client-access/<companyname>/saml.php`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://myaba.co.uk/<companyname>`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte do Cliente MCM](https://mcmtechnology.com/support/) para obter esses valores. 
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![Configurar o logon único](./media/mcm-tutorial/tutorial_mcm_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/mcm-tutorial/tutorial_general_400.png) 

1. Para configurar o logon único no lado do **MCM**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte MCM](https://mcmtechnology.com/support/). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/mcm-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/mcm-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/mcm-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/mcm-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-mcm-test-user"></a>Criar um usuário de teste do MCM

Nesta seção, você criará uma usuária chamada Brenda Fernandes no MCM. Trabalhe com a [equipe de suporte MCM](https://mcmtechnology.com/support/) para adicionar os usuários na plataforma MCM.

> [!NOTE]
> É possível usar qualquer outra ferramenta de criação da conta de usuário do MCM ou APIs fornecidas pelo MCM para provisionar as contas de usuário do AAD.


### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao MCM.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao MCM, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **MCM**.

    ![Configurar o logon único](./media/mcm-tutorial/tutorial_mcm_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do MCM no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo do MCM.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/mcm-tutorial/tutorial_general_01.png
[2]: ./media/mcm-tutorial/tutorial_general_02.png
[3]: ./media/mcm-tutorial/tutorial_general_03.png
[4]: ./media/mcm-tutorial/tutorial_general_04.png

[100]: ./media/mcm-tutorial/tutorial_general_100.png

[200]: ./media/mcm-tutorial/tutorial_general_200.png
[201]: ./media/mcm-tutorial/tutorial_general_201.png
[202]: ./media/mcm-tutorial/tutorial_general_202.png
[203]: ./media/mcm-tutorial/tutorial_general_203.png

