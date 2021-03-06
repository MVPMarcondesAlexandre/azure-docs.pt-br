---
title: 'Tutorial: Integração do Microsoft Azure Active com o Suporte Remoto Bomgar | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Suporte Remoto Bomgar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 193b163f-bdee-4974-b16d-777c51b991df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2018
ms.author: jeedes
ms.openlocfilehash: c59f4291726b24b7c96bb60d0497c1578a3e4b0f
ms.sourcegitcommit: 7208bfe8878f83d5ec92e54e2f1222ffd41bf931
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2018
ms.locfileid: "39048174"
---
# <a name="tutorial-azure-active-directory-integration-with-bomgar-remote-support"></a>Tutorial: Integração do Microsoft Azure Active Directory do Azure com o suporte remoto Bomgar

Neste tutorial, você aprenderá como integrar o suporte de Bomgar remoto com o Microsoft Azure Active Directory (Azure AD).

A integração do suporte de Bomgar remoto com o Microsoft Azure Active Directory oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso Suporte Remoto Bomgar.
- Você pode permitir que seus usuários façam logon automaticamente no Suporte Remoto Bomgar (logon único) com suas contas do Microsoft Azure Active Directory.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Microsoft Azure Active Directory ao Suporte Remoto Bomgar você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Suporte Remoto Bomgar

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o suporte remoto Bomgar da Galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-bomgar-remote-support-from-the-gallery"></a>Adicionando o suporte remoto Bomgar da Galeria
Para configurar a integração do suporte remoto Bomgar ao Microsoft Azure Active Directory, você precisa adicionar o suporte remoto Bomgar por meio da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o suporte remoto Bomgar da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **suporte remoto Bomgar**, selecione **suporte remoto Bomgar** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Suporte remoto Bomgarna na lista de resultados](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Microsoft Azure Active Directory com o suporte remoto Bomgar, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Microsoft Azure Active Directory precisa saber qual usuário do suporte remoto Bomgar é equivalente a um usuário do Microsoft Azure Active Directory. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Microsoft Azure Active Directory e o usuário relacionado do suporte remoto Bomgar.

Para configurar e testar o logon único do Microsoft Azure Active Directory com o suporte remoto Bomgar, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do suporte remoto Bomgar](#create-a-bomgar-remote-support-test-user)** – para ter um equivalente de Brenda Fernandes no suporte remoto Bomgar que esteja vinculado à representação do usuário no Microsoft Azure Active Directory.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Microsoft Azure Active Directory no portal do Azure e configura o logon único no aplicativo suporte remoto Bomgar.

**Para configurar o logon único do Microsoft Azure Active Directory com o suporte remoto Bomgar, realize as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo do **suporte remoto Bomgar**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_samlbase.png)

3. Na seção **Domínio e URLs do suporte remoto Bomgar**, realize as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do suporte remoto Bomgar](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<SUBDOMAIN>.trafficmanager.net/saml`

    b. Na caixa de texto **Identificador (ID da Entidade)**, digite uma URL usando o seguinte padrão: `https://<SUBDOMAIN>.trafficmanager.net`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais (ID de entidade). Contate a [equipe do suporte remoto Bomgar](https://www.bomgar.com/docs/index.htm#support) para obter esses valores. 
 
4. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/bomgarremotesupport-tutorial/tutorial_general_400.png)

6. Para configurar o logon único no lado do **suporte remoto Bomgar**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte remoto Bomgar](https://www.bomgar.com/docs/index.htm#support). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/bomgarremotesupport-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/bomgarremotesupport-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/bomgarremotesupport-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/bomgarremotesupport-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-bomgar-remote-support-test-user"></a>Criar um usuário de teste suporte remoto Bomgar

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no suporte remoto Bomgar. O suporte remoto Bomgar dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão. Não há itens de ação para você nesta seção. Um novo usuário será criado durante uma tentativa de acessar o suporte remoto Bomgar, caso ele ainda não exista.
>[!Note]
>Se você precisar criar um usuário manualmente, contate a [equipe de suporte remoto Bomgar](https://www.bomgar.com/docs/index.htm#support).

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao suporte remoto Bomgar.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao suporte remoto Bomgar, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, escolha **suporte remoto Bomgar**.

    ![O link de suporte remoto Bomgar na lista de aplicativos](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica na peça suporte remoto Bomgar no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo do suporte remoto Bomgar.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bomgarremotesupport-tutorial/tutorial_general_01.png
[2]: ./media/bomgarremotesupport-tutorial/tutorial_general_02.png
[3]: ./media/bomgarremotesupport-tutorial/tutorial_general_03.png
[4]: ./media/bomgarremotesupport-tutorial/tutorial_general_04.png

[100]: ./media/bomgarremotesupport-tutorial/tutorial_general_100.png

[200]: ./media/bomgarremotesupport-tutorial/tutorial_general_200.png
[201]: ./media/bomgarremotesupport-tutorial/tutorial_general_201.png
[202]: ./media/bomgarremotesupport-tutorial/tutorial_general_202.png
[203]: ./media/bomgarremotesupport-tutorial/tutorial_general_203.png

