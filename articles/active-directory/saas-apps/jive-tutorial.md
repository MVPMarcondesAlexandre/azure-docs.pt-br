---
title: 'Tutorial: Integração do Azure Active Directory com o Jive | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: jeedes
ms.openlocfilehash: 1f2b9d59e85593047feb8d243c7c874786864b4d
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55191628"
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a>Tutorial: Integração do Azure Active Directory com o Jive

Neste tutorial, você aprenderá a integrar o Jive ao Azure AD (Azure Active Directory).

A integração do Jive ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Jive
- Você pode permitir que seus usuários faça logon automaticamente no Jive (logon único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Caso deseje obter mais informações sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Jive, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Jive

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.
 O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar Fuse da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-jive-from-the-gallery"></a>Adicionar Fuse da galeria
Para configurar a integração do Jive com o Azure AD, você precisará adicionar o Jive à sua lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Jive por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]

1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Jive**.

    ![Criação de um usuário de teste do AD do Azure](./media/jive-tutorial/tutorial_jive_search.png)

1. No painel de resultados, selecione **Jive** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Jive, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Jive é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Jive.

Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Jive.

Para configurar e testar o logon único do Azure AD com o Jive, você precisa concluir os seguintes blocos de construção:

1. **[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do Jive](#creating-a-jive-test-user)** – para ter um equivalente de Brenda Fernandes no Jive que esteja vinculado à representação de usuário do Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Jive.

**Para configurar o logon único do Azure AD com o Jive, execute as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Jive**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.

    ![Configurar o logon único](./media/jive-tutorial/tutorial_jive_samlbase.png)

1. Na seção **Domínio e URLs do Jive**, realize as seguintes etapas:

    ![Configurar o logon único](./media/jive-tutorial/tutorial_jive_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<instance name>.jivecustom.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instance name>.jiveon.com`

    > [!NOTE]
    > Esses não são os valores reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte ao Cliente do Jive](https://www.jivesoftware.com/services-support/) para obter esses valores.

1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.

    ![Configurar o logon único](./media/jive-tutorial/tutorial_jive_certificate.png)

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/jive-tutorial/tutorial_general_400.png)

1. Para configurar o logon único no lado do **Jive**, faça logon em seu locatário do Jive como administrador.

1. No menu na parte superior, clique em “**SAML**”.

    ![Configurar o logon único no lado do aplicativo](./media/jive-tutorial/tutorial_jive_002.png)

     a. Selecione **Habilitado** na guia **Geral**. b. Clique no botão "**Salvar todas as configurações de saml**".

1. Navegue até a guia "**Metadados Idp**".

    ![Configurar o logon único no lado do aplicativo](./media/jive-tutorial/tutorial_jive_003.png)

     a. Copie o conteúdo do arquivo XML de metadados baixado e cole-o na caixa de texto **Metadados do IDP (Provedor de Identidade)** .

    b. Clique no botão "**Salvar todas as configurações de saml**".

1. Vá até a guia "**Mapeamento de Atributo de Usuário**".

    ![Configurar o logon único no lado do aplicativo](./media/jive-tutorial/tutorial_jive_004.png)

     a. Na caixa de texto **Email**, copie e cole o nome de atributo do valor **email**.

    b. Na caixa de texto **Nome**, copie e cole o nome do atributo do valor **nome**.

    c. Na caixa de texto **Sobrenome**, copie e cole o nome do atributo do valor **sobrenome**.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/jive-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.

    ![Criação de um usuário de teste do AD do Azure](./media/jive-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.

    ![Criação de um usuário de teste do AD do Azure](./media/jive-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:

    ![Criação de um usuário de teste do AD do Azure](./media/jive-tutorial/create_aaduser_04.png)

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.

### <a name="creating-a-jive-test-user"></a>Criar um usuário de teste Jive

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Jive. O Jive dá suporte ao provisionamento automático do usuário, que está habilitado por padrão. Você pode encontrar [aqui](jive-provisioning-tutorial.md) mais detalhes de como configurar o provisionamento automático de usuário.

Se precisar criar um usuário manualmente, trabalhe com a [Equipe de suporte ao cliente do Jive](https://www.jivesoftware.com/services-support/) para adicionar os usuários à plataforma Jive.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Jive.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Jive, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, escolha **Jive**.

    ![Configurar o logon único](./media/jive-tutorial/tutorial_jive_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Jive no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo do Jive.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)
* [Configurar Provisionamento de Usuário](jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/jive-tutorial/tutorial_general_01.png
[2]: ./media/jive-tutorial/tutorial_general_02.png
[3]: ./media/jive-tutorial/tutorial_general_03.png
[4]: ./media/jive-tutorial/tutorial_general_04.png

[100]: ./media/jive-tutorial/tutorial_general_100.png

[200]: ./media/jive-tutorial/tutorial_general_200.png
[201]: ./media/jive-tutorial/tutorial_general_201.png
[202]: ./media/jive-tutorial/tutorial_general_202.png
[203]: ./media/jive-tutorial/tutorial_general_203.png
