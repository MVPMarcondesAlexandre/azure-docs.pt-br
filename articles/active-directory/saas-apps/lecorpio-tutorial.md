---
title: 'Tutorial: Integração do Azure Active Directory ao Lecorpio | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Lecorpio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 2263a75ca5e3e4e0130dccd58b1fe2202f35bbd1
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55197272"
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a>Tutorial: Integração do Azure Active Directory ao Lecorpio

Neste tutorial, você aprenderá a integrar o Lecorpio ao Azure AD (Azure Active Directory).

A integração do Lecorpio ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao Lecorpio
- Você pode permitir que seus usuários façam logon automaticamente em Lecorpio (logon único) com as respectivas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Lecorpio, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Lecorpio

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Lecorpio da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-lecorpio-from-the-gallery"></a>Adicionando o Lecorpio da galeria
Para configurar a integração do Lecorpio ao Azure AD, você precisa adicionar o Lecorpio da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Lecorpio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Lecorpio**.

    ![Criação de um usuário de teste do AD do Azure](./media/lecorpio-tutorial/tutorial_lecorpio_search.png)

1. No painel de resultados, selecione **Lecorpio** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Lecorpio, com base em um usuário de teste chamado "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Lecorpio é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Lecorpio.

Essa relação de vinculação é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no Lecorpio.

Para configurar e testar o logon único do Azure AD com o Lecorpio, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do Lecorpio](#creating-a-lecorpio-test-user)** – para ter um equivalente de Brenda Fernandes no Lecorpio que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo Lecorpio.

**Para configurar o logon único do Azure AD com o Lecorpio, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **Lecorpio**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

1. Na seção **Domínio e URLs do Lecorpio**, execute as seguintes etapas:

    ![Configurar o logon único](./media/lecorpio-tutorial/tutorial_lecorpio_url.png)

     a. Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://<instance name>.lecorpio.com/<customer name>`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instance name>.lecorpio.com/<customer name>`

    > [!NOTE] 
    > Esses não são os valores reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador. Contate a [equipe de suporte do Cliente Lecorpio](mailto:info@lecorpio.com) para obter esses valores. 
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![Configurar o logon único](./media/lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/lecorpio-tutorial/tutorial_general_400.png)

1. Para configurar o logon único no lado do **Lecorpio**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Lecorpio](mailto:info@lecorpio.com).

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/lecorpio-tutorial/create_aaduser_01.png) 

1. Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/lecorpio-tutorial/create_aaduser_02.png) 

1. Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.
 
    ![Criação de um usuário de teste do AD do Azure](./media/lecorpio-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/lecorpio-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-lecorpio-test-user"></a>Criando um usuário de teste do Lecorpio

Nesta seção, você criará um usuário chamado Brenda Fernandes no Lecorpio. 

É preciso contatar a [equipe de suporte do Cliente Lecorpio](mailto:info@lecorpio.com) para adicionar os usuários no aplicativo Lecorpio.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Lecorpio.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Lecorpio, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Lecorpio**.

    ![Configurar o logon único](./media/lecorpio-tutorial/tutorial_lecorpio_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco Lecorpio no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Lecorpio.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/lecorpio-tutorial/tutorial_general_203.png

