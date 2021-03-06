---
title: 'Tutorial: Integração do Azure Active Directory com o Flatter Files | Microsoft Docs'
description: Saiba como configurar o logon único entre o Active Directory do Azure e o Flatter Files.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: fe15a1aa0d284913c77d62e254b8827d9d60c850
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55188228"
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a>Tutorial: Integração do Azure Active Directory com o Flatter Files

Neste tutorial, você aprenderá a integrar o Flatter Files ao Azure AD (Azure Active Directory).

A integração do Flatter Files ao Azure AD oferece os seguintes benefícios:

- No AD do Azure, você pode controlar quem tem acesso ao Flatter Files
- Você pode permitir que seus usuários façam logon automaticamente no Flatter Files (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do AD do Azure ao Flatter Files, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do Flatter Files com logon único habilitado

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando Flatter Files da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-flatter-files-from-the-gallery"></a>Adicionando Flatter Files da galeria
Para configurar a integração do Flatter Files ao AD do Azure, você precisará adicionar o Flatter Files da galeria à sua lista de aplicativos de SaaS gerenciados.

**Para adicionar o Flatter Files da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Flatter Files**.

    ![Criação de um usuário de teste do AD do Azure](./media/flatter-files-tutorial/tutorial_flatterfiles_search.png)

1. No painel de resultados, selecione **Flatter Files** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Flatter Files com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Flatter Files é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Flatter Files.

No Flatter Files, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do AD do Azure com o Flatter Files, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do Flatter Files](#creating-a-flatter-files-test-user)** – para ter um equivalente de Brenda Fernandes no Flatter Files que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Flatter Files.

**Para configurar o logon único do AD do Azure com o Flatter Files, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Flatter Files**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

1. Na seção **URLs e Domínio do Flatter Files**, o usuário não precisa executar nenhuma etapa, já que o aplicativo já está integrado ao Azure.

    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
1. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Flatter Files**, clique em **Configurar Flatter Files** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

1. Faça logon no aplicativo Flatter Files como administrador.

1. Clique em **PAINEL**. 
   
    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatter_files_05.png)  

1. Clique em **Configurações** e execute as etapas a seguir na guia **Empresa**: 
   
    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
     a. Selecione **Usar SAML 2.0 para Autenticação**.
    
    b. Clique em **Configurar SAML**.

1. No diálogo **Configuração de SAML** , execute as seguintes etapas: 
   
    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
     a. Na caixa de texto **Domínio**, digite seu domínio registrado.
   
    >[!NOTE]
    >Se não tiver um domínio registrado, entre em contato com a equipe de suporte do Flatter Files pelo email [support@flatterfiles.com](mailto:support@flatterfiles.com). 
    
    b. Na caixa de texto **URL do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** copiado do portal do Azure.
   
    c.  Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado do Provedor de Identidade**.

    d. Clique em **Atualizar**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/flatter-files-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/flatter-files-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/flatter-files-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/flatter-files-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-flatter-files-test-user"></a>Criação de um usuário de teste do Flatter Files

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Flatter Files.

**Para criar um usuário chamado Brenda Fernandes no Flatter Files, execute as seguintes etapas:**

1. Faça logon no site da empresa **Flatter Files** como administrador.

1. No painel de navegação à esquerda, clique em **Configurações** e, em seguida, clique na guia **Usuários**.
   
    ![Criar um usuário do Flatter Files](./media/flatter-files-tutorial/tutorial_flatter_files_09.png)

1. Clique em **Adicionar Usuário**. 

1. No diálogo **Adicionar Usuário** , realize as seguintes etapas:
   
    ![Criar um usuário do Flatter Files](./media/flatter-files-tutorial/tutorial_flatter_files_10.png)

     a. Na caixa de texto **Nome**, digite **Brenda**.
   
    b. Na caixa de texto **Sobrenome**, digite **Fernandes**. 
   
    c. Na caixa de texto **Endereço de Email**, digite o endereço de email de Brenda no portal do Azure.
   
    d. Clique em **Enviar**.   


### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Flatter Files.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Flatter Files, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, escolha **Flatter Files**.

    ![Configurar o logon único](./media/flatter-files-tutorial/tutorial_flatterfiles_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Flatter Files no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Flatter Files.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/flatter-files-tutorial/tutorial_general_203.png

