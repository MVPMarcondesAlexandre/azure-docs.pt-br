---
title: 'Tutorial: Integração do Azure Active Directory ao Nexonia | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Nexonia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2018
ms.author: jeedes
ms.openlocfilehash: a2ddeee181962a4e11633705fbe657596478870e
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55165551"
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a>Tutorial: Integração do Azure Active Directory ao Nexonia

Neste tutorial, você aprenderá a integrar o Nexonia ao Azure AD (Azure Active Directory).

A integração do Nexonia ao Azure AD oferece os seguintes benefícios:

- No Azure AD, você pode controlar quem tem acesso ao Nexonia.
- Você pode permitir que seus usuários faça logon automaticamente no Nexonia (logon único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Nexonia, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do Nexonia habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar Nexonia da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-nexonia-from-the-gallery"></a>Adicionar Nexonia da galeria
Para configurar a integração do Nexonia ao Azure AD, você precisará adicionar o Nexonia da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Nexonia da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Nexonia**, selecione **Nexonia** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Nexonia na lista de resultados](./media/nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Nexonia, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Nexonia é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Nexonia.

No Nexonia, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Nexonia, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do Nexonia](#create-a-nexonia-test-user)** – para ter um equivalente de Brenda Fernandes no Nexonia que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Nexonia.

  > [!Note]
   > Se você tiver problemas na integração, consulte este [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery) para um guia de solução de problemas. Se você ainda não encontrou a solução, acione a solicitação de suporte do Portal do Azure.

**Para configurar o logon único do Azure AD com o Nexonia, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **Nexonia**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/nexonia-tutorial/tutorial_nexonia_samlbase.png)

1. Na seção **URLs e Domínio do Nexonia**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Nexonia](./media/nexonia-tutorial/tutorial_nexonia_url.png)

     a. Na caixa de texto **Identificador**, digite um valor: `Nexonia`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`

    > [!NOTE] 
    > O valor de URL de Resposta não é real. Atualize o valor com a URL de Resposta real. Para obter o valor, entre em contato com a [equipe de suporte do Nexonia](https://nexonia.zendesk.com/hc/requests/new).
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/nexonia-tutorial/tutorial_nexonia_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/nexonia-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Nexonia**, clique em **Configurar o Nexonia** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configuração do Nexonia](./media/nexonia-tutorial/tutorial_nexonia_configure.png) 

1. Para configurar o logon único no lado do **Nexonia**, é necessário enviar o **Certificado (Base64) baixado, a URL de Saída, a ID da Entidade SAML, e a URL do Serviço de Logon Único do SAML** e a **ID da Entidade SAML** para a [equipe de suporte do Nexonia](https://nexonia.zendesk.com/hc/requests/new). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/nexonia-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/nexonia-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/nexonia-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/nexonia-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
  
### <a name="create-a-nexonia-test-user"></a>Criar um usuário de teste do Nexonia

Nesta seção, você criará um usuário chamado Brenda Fernandes no Nexonia. Trabalhe com a [equipe de suporte do Nexonia](https://nexonia.zendesk.com/hc/requests/new) para adicionar os usuários na plataforma do Nexonia. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, ao conceder acesso ao Nexonia a Brenda Fernandes, você permitirá que ela use o logon único do Azure.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Nexonia, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Nexonia**.

    ![O link do Nexonia na lista de Aplicativos](./media/nexonia-tutorial/tutorial_nexonia_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco Nexonia no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Nexonia.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/nexonia-tutorial/tutorial_general_01.png
[2]: ./media/nexonia-tutorial/tutorial_general_02.png
[3]: ./media/nexonia-tutorial/tutorial_general_03.png
[4]: ./media/nexonia-tutorial/tutorial_general_04.png

[100]: ./media/nexonia-tutorial/tutorial_general_100.png

[200]: ./media/nexonia-tutorial/tutorial_general_200.png
[201]: ./media/nexonia-tutorial/tutorial_general_201.png
[202]: ./media/nexonia-tutorial/tutorial_general_202.png
[203]: ./media/nexonia-tutorial/tutorial_general_203.png

