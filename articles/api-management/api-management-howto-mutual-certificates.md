---
title: Proteger serviços de back-end usando autenticação de certificado do cliente - Gerenciamento de API do Azure | Microsoft Docs
description: Saiba como garantir serviços de back-end usando autenticação de certificado do cliente no Gerenciamento de API do Azure.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: apimpm
ms.openlocfilehash: b76b64ddf854b32c51b8b319479a35331e0f72f3
ms.sourcegitcommit: 5d837a7557363424e0183d5f04dcb23a8ff966bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52957419"
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Como garantir serviços de back-end usando autenticação de certificado do cliente no Gerenciamento de API do Azure

O Gerenciamento de API permite proteger o acesso ao serviço back-end de uma API usando certificados do cliente. Este guia mostra como gerenciar certificados na instância do serviço Gerenciamento de API do Azure no portal do Azure. Também explica como configurar uma API para usar um certificado para acessar um serviço back-end.

Para obter mais informações sobre gerenciamento de certificados usando a API REST de gerenciamento de API, consulte <a href="https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-certificate-entity">Entidade de certificado da API REST de Gerenciamento de API do Azure</a>.

## <a name="prerequisites"> </a>Pré-requisitos

Este guia mostra como configurar sua instância de serviço de Gerenciamento de API para usar a autenticação de certificado do cliente para acessar o serviço back-end para uma API. Antes de executar as etapas deste artigo, será necessário ter o serviço back-end configurado para a autenticação de certificado do cliente ([para configurar a autenticação de certificado nos sites do Azure, consulte este artigo][to configure certificate authentication in Azure WebSites refer to this article]). É necessário acessar o certificado e a senha para enviar ao serviço de Gerenciamento de API.

## <a name="step1"> </a>Carregar um certificado do cliente

![Adicionar certificados do cliente](media/api-management-howto-mutual-certificates/apim-client-cert.png)

Siga as etapas abaixo para fazer upload de um novo certificado do cliente. Se você ainda não criou uma instância de serviço de Gerenciamento de API, consulte o tutorial [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance].

1. Navegue até a instância de serviço do Gerenciamento de API do Azure no portal do Azure.
2. Selecione **Certificados do Cliente** do menu.
3. Clique no botão **+ Adicionar**.  
    ![Adicionar certificados do cliente](media/api-management-howto-mutual-certificates/apim-client-cert-add.png)  
4. Procure o certificado, forneça a ID e senha.  
5. Clique em **Criar**.

> [!NOTE]
> O certificado deve estar no formato **.pfx** . Os certificados autoassinados são permitidos.

Depois que o certificado for carregado, ele será exibido nos **Certificados do cliente**.  Se você tiver muitos certificados, anote a impressão digital do certificado desejado para poder [Configurar uma API para usar um certificado do cliente para a autenticação de gateway][Configure an API to use a client certificate for gateway authentication].

> [!NOTE]
> Para desabilitar a validação da cadeia de certificados ao usar, por exemplo, um certificado autoassinado, siga as etapas descritas neste [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) das Perguntas frequentes.

## <a name="step1a"> </a>Excluir um certificado do cliente

Para excluir um certificado, clique no menu de contexto **...** e selecione **Excluir** ao lado do certificado.

![Excluir certificados do cliente](media/api-management-howto-mutual-certificates/apim-client-cert-delete.png)

Se o certificado está em uso por uma API, então uma tela de aviso é exibida. Para excluir o certificado, você primeiro deve remover o certificado de quaisquer APIs que são configuradas para usá-la.

![Excluir falha nos certificados do cliente](media/api-management-howto-mutual-certificates/apim-client-cert-delete-failure.png)

## <a name="step2"> </a>Configurar uma API para usar um certificado do cliente para a autenticação de gateway

1. Clique em **APIs** do menu **Gerenciamento de API**  à esquerda e navegue até a API.  
    ![Habilitar certificados do cliente](media/api-management-howto-mutual-certificates/apim-client-cert-enable.png)

2. Na guia **Design**, clique em um ícone de lápis da seção **Back-end**. 
3. Altere as **Credenciais do Gateway** para **Client cert** e selecione o certificado na lista suspensa.  
    ![Habilitar certificados do cliente](media/api-management-howto-mutual-certificates/apim-client-cert-enable-select.png)

4. Clique em **Salvar**. 

> [!WARNING]
> Essa alteração tem efeito imediato e chama para operações desta API, que usará o certificado para autenticar no servidor back-end.


> [!TIP]
> Quando um certificado é especificado para a autenticação de gateway para o serviço back-end de uma API, ele se torna parte da política dessa API e pode ser exibido no editor da política.

## <a name="self-signed-certificates"></a>Certificados autoassinados

Se você estiver usando certificados autoassinados, será necessário desabilitar a validação da cadeia de certificados para que o Gerenciamento de API comunique-se com o sistema back-end. Caso contrário, retornará um código de erro 500. Para configurar isso, você pode usar cmdlets [`New-AzureRmApiManagementBackend`](https://docs.microsoft.com/powershell/module/azurerm.apimanagement/new-azurermapimanagementbackend) (para novo back-end) ou [`Set-AzureRmApiManagementBackend`](https://docs.microsoft.com/powershell/module/azurerm.apimanagement/set-azurermapimanagementbackend) (para back-end existente) do PowerShell e definir o parâmetro `-SkipCertificateChainValidation` como `True`.

```
$context = New-AzureRmApiManagementContext -resourcegroup 'ContosoResourceGroup' -servicename 'ContosoAPIMService'
New-AzureRmApiManagementBackend -Context  $context -Url 'https://contoso.com/myapi' -Protocol http -SkipCertificateChainValidation $true
```

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: get-started-create-service-instance.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: get-started-create-service-instance.md

[Azure API Management REST API Certificate entity]: https://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: ../app-service/app-service-web-configure-tls-mutual-auth.md

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps
