---
title: 'Tutorial: Integração do Azure Active Directory com ThirdPartyTrust | Microsoft Docs'
description: Saiba como configurar o logon único entre o Active Directory do Azure e o ThirdPartyTrust.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3c496939-4201-4108-b0cc-d3e7c4244229
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2018
ms.author: jeedes
ms.openlocfilehash: ace619e5eba8d5f1b4f1740f2c88fbce7bc83790
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55150508"
---
# <a name="tutorial-azure-active-directory-integration-with-thirdpartytrust"></a>Tutorial: Integração do Azure Active Directory com ThirdPartyTrust

Neste tutorial, você aprenderá a integrar o ThirdPartyTrust ao Azure AD (Azure Active Directory).

A integração do ThirdPartyTrust com o AD do Azure oferece os seguintes benefícios:

- No Azure AD, você poderá controlar quem tem acesso ao ThirdPartyTrust.
- Você pode habilitar os usuários a entrar automaticamente no ThirdPartyTrust (Logon Único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao ThirdPartyTrust, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do ThirdPartyTrust

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando ThirdPartyTrust da galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-thirdpartytrust-from-the-gallery"></a>Adicionando ThirdPartyTrust da galeria
Para configurar a integração do ThirdPartyTrust ao Azure AD, você precisará adicionar o ThirdPartyTrust da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o ThirdPartyTrust por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **ThirdPartyTrust**, selecione **ThirdPartyTrust** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![ThirdPartyTrust na lista de resultados](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o ThirdPartyTrust, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do ThirdPartyTrust é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ThirdPartyTrust.

Para configurar e testar o logon único do AD do Azure com o ThirdPartyTrust, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar de um usuário de teste do ThirdPartyTrust](#create-a-thirdpartytrust-test-user)** : para ter um equivalente de Brenda Fernandes no ThirdPartyTrust que esteja vinculado à representação de usuário no Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo ThirdPartyTrust.

**Para configurar o logon único do Azure AD com o ThirdPartyTrust, realize as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **ThirdPartyTrust**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_samlbase.png)

3. Na seção **Domínio e URLs do ThirdPartyTrust**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IDP**:

    ![Informações de logon único de Domínio e URLs do ThirdPartyTrust](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_url.png)

    Na caixa de texto **Identificador**, digite uma URL: `https://api.thirdpartytrust.com/sai3/saml/metadata`

4. Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:

    ![Informações de logon único de Domínio e URLs do ThirdPartyTrust](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_url1.png)

    Na caixa de texto **URL de Logon**, digite uma URL: `https://api.thirdpartytrust.com/sai3/test`
     
5. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_certificate.png) 

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/thirdpartytrust-tutorial/tutorial_general_400.png)
    
7. Para configurar o logon único no lado do **ThirdPartyTrust**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do ThirdPartyTrust](mailto:support@thirdpartytrust.com). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/thirdpartytrust-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/thirdpartytrust-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/thirdpartytrust-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/thirdpartytrust-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-thirdpartytrust-test-user"></a>Criar um usuário de teste do ThirdPartyTrust

Nesta seção, você cria um usuário chamado Brenda Fernandes no ThirdPartyTrust. Trabalhe com a  [equipe de suporte do ThirdPartyTrust](mailto:support@thirdpartytrust.com)  para adicionar os usuários na plataforma do ThirdPartyTrust. Os usuários devem ser criados e ativados antes de usar o logon único. 


### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao ThirdPartyTrust.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao ThirdPartyTrust, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, escolha **ThirdPartyTrust**.

    ![O link do ThirdPartyTrust na lista de Aplicativos](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Na caixa de diálogo **Usuários e grupos**, selecione **Brenda Fernandes** na lista de Usuários.

6. Clique no botão **Selecionar** na caixa de diálogo **Usuários e grupos**.

7. Clique no botão **Atribuir** na caixa de diálogo **Adicionar atribuição**.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco ThirdPartyTrust no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo do ThirdPartyTrust.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/thirdpartytrust-tutorial/tutorial_general_01.png
[2]: ./media/thirdpartytrust-tutorial/tutorial_general_02.png
[3]: ./media/thirdpartytrust-tutorial/tutorial_general_03.png
[4]: ./media/thirdpartytrust-tutorial/tutorial_general_04.png

[100]: ./media/thirdpartytrust-tutorial/tutorial_general_100.png

[200]: ./media/thirdpartytrust-tutorial/tutorial_general_200.png
[201]: ./media/thirdpartytrust-tutorial/tutorial_general_201.png
[202]: ./media/thirdpartytrust-tutorial/tutorial_general_202.png
[203]: ./media/thirdpartytrust-tutorial/tutorial_general_203.png

