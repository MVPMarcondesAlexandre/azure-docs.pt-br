---
title: 'Tutorial: Integração do Azure Active Directory com o Intralinks | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Intralinks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: aaa3b7d0ac80fbe2bca937a2826c1c26e6718ea4
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55168559"
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Tutorial: Integração do Azure Active Directory com o Intralinks

Neste tutorial, você aprenderá como integrar o Intralinks ao Azure AD (Azure Active Directory).

A integração do Intralinks ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao Intralinks
- Você pode permitir que seus usuários façam logon automaticamente no Intralinks (logon único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Intralinks, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Intralinks

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Intralinks da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-intralinks-from-the-gallery"></a>Adicionando o Intralinks da galeria
Para configurar a integração do Intralinks ao Azure AD, você precisará adicionar o Intralinks da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Intralinks da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Intralinks**.

    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/tutorial_intralinks_search.png)

1. No painel de resultados, selecione **Intralinks** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Intralinks, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Intralinks é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Intralinks.

No Intralinks, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Intralinks, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criando um usuário de teste do Intralinks](#creating-an-intralinks-test-user)** – para ter um equivalente de Brenda Fernandes no Intralinks que esteja vinculado à representação de usuário do Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Intralinks.

**Para configurar o logon único do Azure AD com o Intralinks, execute as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Intralinks**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_intralinks_samlbase.png)

1. Na seção **Domínio e URLs do Intralinks**, realize as seguintes etapas:

    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_intralinks_url.png)

    Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com a URL de Logon real. Contate a [equipe de suporte ao Cliente do Intralinks](https://www.intralinks.com/contact) para obter esse valor. 
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_intralinks_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_general_400.png)

1. Para configurar o logon único no lado do **Intralinks**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Intralinks](https://www.intralinks.com/contact). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-intralinks-test-user"></a>Criação de um usuário de teste do Intralinks

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Intralinks. Trabalhe com a [equipe de suporte do Intralinks](https://www.intralinks.com/contact) para adicionar os usuários à plataforma Intralinks.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Intralinks.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Intralinks, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Intralinks**.

    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_intralinks_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

### <a name="add-intralinks-via-or-elite-application"></a>Adicionar o aplicativo Intralinks VIA ou Elite

O Intralinks usa a mesma plataforma de Identidade de SSO para todos os outros aplicativos Intralinks excluindo o aplicativo Deal Nexus. Portanto, se você planeja usar qualquer outro aplicativo Intralinks, primeiro você precisa configurar o SSO para um aplicativo Intralinks primário usando o procedimento descrito acima.

Depois disso, você pode seguir o procedimento abaixo para adicionar outro aplicativo Intralinks em seu locatário, que pode aproveitar esse aplicativo principal para o SSO. 

>[!NOTE]
>Esse recurso está disponível somente para clientes de SKU do Azure AD Premium e não está disponível para clientes de SKU Gratuito ou Básico.

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]


1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Intralinks**.

    ![Criação de um usuário de teste do AD do Azure](./media/intralinks-tutorial/tutorial_intralinks_search.png)

1. No **aplicativo Intralinks Add**, realize as seguintes etapas:

    ![Adicionar o aplicativo Intralinks VIA ou Elite](./media/intralinks-tutorial/tutorial_intralinks_addapp.png)

     a. Na caixa de texto **Nome**, insira o nome apropriado do aplicativo, por exemplo, **Intralinks Elite**.

    b. Clique no botão **Adicionar**.

1.  No portal do Azure, na página de integração do aplicativo **Intralinks**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon vinculado**.
 
    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

1. Obtenha a URL de SSO Iniciada por SP com a [equipe do Intralinks](https://www.intralinks.com/contact) para o outro aplicativo Intralinks e insira-a em **Configurar URL de Logon**, conforme é mostrado abaixo. 
    
     ![Configurar o logon único](./media/intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     Na caixa de texto URL de Logon, digite a URL usada pelos usuários para fazer logon no aplicativo Intralinks usando o seguinte padrão:
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/intralinks-tutorial/tutorial_general_400.png)

1. Atribua o aplicativo para usuários ou grupos, como mostrado na seção **[Atribuição do usuário de teste do Azure AD](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco Intralinks no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Intralinks.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/intralinks-tutorial/tutorial_general_01.png
[2]: ./media/intralinks-tutorial/tutorial_general_02.png
[3]: ./media/intralinks-tutorial/tutorial_general_03.png
[4]: ./media/intralinks-tutorial/tutorial_general_04.png

[100]: ./media/intralinks-tutorial/tutorial_general_100.png

[200]: ./media/intralinks-tutorial/tutorial_general_200.png
[201]: ./media/intralinks-tutorial/tutorial_general_201.png
[202]: ./media/intralinks-tutorial/tutorial_general_202.png
[203]: ./media/intralinks-tutorial/tutorial_general_203.png

