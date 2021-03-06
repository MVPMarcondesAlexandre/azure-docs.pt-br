---
title: 'Tutorial: Integração do Azure Active Directory ao SpaceIQ | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o SpaceIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: 5b55ae29-491f-401f-9299-d3a6b64a1b99
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2017
ms.author: jeedes
ms.openlocfilehash: e0f52a33f0213af7d361af77f4b2dcd1ab0fcd3c
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55154194"
---
# <a name="tutorial-azure-active-directory-integration-with-spaceiq"></a>Tutorial: Integração do Azure Active Directory ao SpaceIQ

Neste tutorial, você aprenderá a integrar o SpaceIQ ao Azure AD (Azure Active Directory).

A integração do SpaceIQ ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao SpaceIQ.
- Você pode permitir que seus usuários façam logon automaticamente no SpaceIQ (logon único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao SpaceIQ, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SpaceIQ

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o SpaceIQ da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-spaceiq-from-the-gallery"></a>Adicionando o SpaceIQ da galeria
Para configurar a integração do SpaceIQ ao Azure AD, você precisará adicionar o SpaceIQ da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o SpaceIQ da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **SpaceIQ**, selecione **SpaceIQ** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![SpaceIQ na lista de resultados](./media/spaceiq-tutorial/tutorial_spaceiq_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o SpaceIQ, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do SpaceIQ é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no SpaceIQ.

No SpaceIQ, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o SpaceIQ, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do SpaceIQ](#create-a-spaceiq-test-user)** – para ter um equivalente de Brenda Fernandes no SpaceIQ que esteja vinculado à representação de usuário no Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SpaceIQ.

**Para configurar o logon único do Azure AD com o SpaceIQ, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **SpaceIQ**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/spaceiq-tutorial/tutorial_spaceiq_samlbase.png)

1. Na seção **URLs e Domínio do SpaceIQ**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do SpaceIQ](./media/spaceiq-tutorial/tutorial_spaceiq_url.png)

     a. Na caixa de texto **Identificador**, digite a URL: `https://api.spaceiq.com`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://api.spaceiq.com/saml/<instanceid>/callback`

    > [!NOTE] 
    > Atualize esses valores com a URL de Resposta e o Identificador reais, que são explicados adiante no tutorial.
 
1. Na seção **Certificado de Autenticação SAML**, clique em **(Certificado Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/spaceiq-tutorial/tutorial_spaceiq_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/spaceiq-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do SpaceIQ**, clique em **Configurar o SpaceIQ** para abrir a janela **Configurar logon**. Copie a **ID da Entidade SAML** da **seção Referência Rápida.**

    ![Configuração do SpaceIQ](./media/spaceiq-tutorial/tutorial_spaceiq_configure.png) 

1.  Abra uma nova janela do navegador e conecte-se ao ambiente do SpaceIQ como administrador.

1. Depois que estiver conectado, clique no sinal de quebra-cabeça no canto superior direito e clique em **"Integrações"**

    ![Configurações da conta](./media/spaceiq-tutorial/setting1.png) 

1. Em **TODOS OS PROVISIONAMENTOS E SSO**, clique no bloco **Azure** para adicionar uma instância do Azure como IDP.

    ![Ícone SAML](./media/spaceiq-tutorial/setting2.png)

1. Na caixa de diálogo **SSO**, execute as seguintes etapas:

    ![Configurações de Autenticação SAML](./media/spaceiq-tutorial/setting3.png)

     a. Na caixa **URL do Emissor SAML**, cole o valor da **ID de Entidade SAML** na janela de configuração de aplicativos do Azure AD.
    
    b. Copie o valor da **URL de Ponto de Extremidade de Retorno de Chamada SAML (somente leitura)** e cole o valor na caixa **URL de Resposta** no portal do Azure, na seção **Domínio e URLs** do SpaceIQ.
    
    c. Copie o valor da **URI de Audiência SAML (somente leitura)** e cole o valor na caixa **Identificador** no portal do Azure, na seção **Domínio e URLs** do SpaceIQ.

    d. Abra o arquivo de certificados baixado no bloco de notas, copie o conteúdo e cole-o na caixa **Certificado X.509**.
    
    e. Clique em **Salvar**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/spaceiq-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/spaceiq-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/spaceiq-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/spaceiq-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
  
### <a name="create-a-spaceiq-test-user"></a>Criar um usuário de teste do SpaceIQ

Nesta seção, você criará uma usuária chamada Brenda Fernandes no SpaceIQ. Trabalhe com a [equipe de suporte do SpaceIQ](mailto:eng@spaceiq.com) para adicionar os usuários à plataforma do SpaceIQ. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao SpaceIQ.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao SpaceIQ, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, escolha **SpaceIQ**.

    ![O link do SpaceIQ na lista Aplicativos](./media/spaceiq-tutorial/tutorial_spaceiq_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco SpaceIQ no Painel de Acesso, deve ser conectado automaticamente ao seu aplicativo SpaceIQ.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/spaceiq-tutorial/tutorial_general_01.png
[2]: ./media/spaceiq-tutorial/tutorial_general_02.png
[3]: ./media/spaceiq-tutorial/tutorial_general_03.png
[4]: ./media/spaceiq-tutorial/tutorial_general_04.png

[100]: ./media/spaceiq-tutorial/tutorial_general_100.png

[200]: ./media/spaceiq-tutorial/tutorial_general_200.png
[201]: ./media/spaceiq-tutorial/tutorial_general_201.png
[202]: ./media/spaceiq-tutorial/tutorial_general_202.png
[203]: ./media/spaceiq-tutorial/tutorial_general_203.png

