---
title: 'Tutorial: Integração do Azure Active Directory ao ICIMS | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o ICIMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 2db359f6aba800e3fb6ea0826ae0e49c43dd4a88
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55167726"
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a>Tutorial: Integração do Azure Active Directory ao ICIMS

Neste tutorial, você aprenderá a integrar o ICIMS ao Azure AD (Azure Active Directory).

A integração do ICIMS ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao ICIMS
- Você pode permitir que seus usuários entrem automaticamente no ICIMS (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao ICIMS, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do ICIMS habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Como adicionar o ICIMS da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-icims-from-the-gallery"></a>Como adicionar o ICIMS da galeria
Para configurar a integração do ICIMS ao Azure AD, você precisará adicionar o ICIMS da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o ICIMS da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **ICIMS**, selecione **ICIMS** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![ICIMS na lista de resultados](./media/icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o ICIMS, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do ICIMS é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ICIMS.

No ICIMS, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o ICIMS, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do ICIMS](#create-an-icims-test-user)** – para ter um equivalente de Brenda Fernandes no ICIMS vinculado à representação do usuário no Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo ICIMS.

**Para configurar o logon único do Azure AD com o ICIMS, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **ICIMS**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/icims-tutorial/tutorial_icims_samlbase.png)

1. Na seção **Domínio e URLs do ICIMS**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do ICIMS](./media/icims-tutorial/tutorial_icims_url.png)

     a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant name>.icims.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenant name>.icims.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte ao cliente do ICIMS](https://www.icims.com/contact-us) para obter esses valores. 
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/icims-tutorial/tutorial_icims_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/icims-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do ICIMS**, clique em **Configurar o ICIMS** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configuração ICIMS](./media/icims-tutorial/tutorial_icims_configure.png) 

1. Para configurar o logon único no lado do **ICIMS**, é necessário enviar o **XML de metadados**, a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** baixados para a [equipe de suporte do ICIMS](https://www.icims.com/contact-us). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/icims-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/icims-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![O botão Adicionar](./media/icims-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![A caixa de diálogo Usuário](./media/icims-tutorial/create_aaduser_04.png) 

     a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="create-an-icims-test-user"></a>Criar um usuário de teste do ICIMS

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no ICIMS. Trabalhe com a [equipe de suporte do ICIMS](https://www.icims.com/contact-us) para adicionar os usuários à conta do ICIMS. 

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao ICIMS.

![Atribuir a função de usuário][200]

**Para atribuir Brenda Fernandes ao ICIMS, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, escolha **ICIMS**.

    ![O link do ICIMS na lista de Aplicativos](./media/icims-tutorial/tutorial_icims_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.  

Ao clicar no bloco ICIMS no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo ICIMS.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/icims-tutorial/tutorial_general_01.png
[2]: ./media/icims-tutorial/tutorial_general_02.png
[3]: ./media/icims-tutorial/tutorial_general_03.png
[4]: ./media/icims-tutorial/tutorial_general_04.png

[100]: ./media/icims-tutorial/tutorial_general_100.png

[200]: ./media/icims-tutorial/tutorial_general_200.png
[201]: ./media/icims-tutorial/tutorial_general_201.png
[202]: ./media/icims-tutorial/tutorial_general_202.png
[203]: ./media/icims-tutorial/tutorial_general_203.png

