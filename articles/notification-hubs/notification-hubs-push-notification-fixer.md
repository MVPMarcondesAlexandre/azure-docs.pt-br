---
title: Diagnóstico de notificações removidas dos Hubs de Notificações do Microsoft Azure
description: Saiba como diagnosticar problemas comuns com notificações removidas nos Hubs de Notificações do Microsoft Azure.
services: notification-hubs
documentationcenter: Mobile
author: jwargo
manager: patniko
editor: spelluru
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 01/04/2019
ms.author: jowargo
ms.openlocfilehash: 9dd6a66ea416ad61682b8e33c6163db3ac345d92
ms.sourcegitcommit: 9b6492fdcac18aa872ed771192a420d1d9551a33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54447710"
---
# <a name="diagnose-dropped-notifications-in-notification-hubs"></a>Diagnosticar notificações removidas nos Hubs de Notificação

Uma das perguntas mais comuns dos clientes de Hubs de Notificação do Azure é como solucionar problemas quando as notificações enviadas de um aplicativo não aparecem no dispositivos cliente. Eles querem saber onde e por que as notificações são removidas, e como corrigir o problema. Este artigo identifica o motivo pelo qual as notificações podem ser removidas ou não recebidas pelos dispositivos. Saiba como analisar e determinar a causa raiz.

É fundamental compreender primeiro como o serviço Hubs de Notificação efetua push das notificações para um dispositivo.

![Arquitetura dos Hubs de Notificação][0]

Em um fluxo de envio de notificação típico, a mensagem é enviada do *back-end do aplicativo* para os Hubs de Notificação. Os Hubs de Notificação executam processamento em todos os registros. O processamento leva em conta as marcas configuradas e expressões de marca para determinar os “destinos”. Destinos são todos os registros que precisam receber a notificação por push. Esses registros podem ser de qualquer plataforma compatível: iOS, Google, Windows, Windows Phone, Kindle e Baidu para Android na China.

Com os destinos estabelecidos, o serviço Hubs de Notificação efetua push nas notificações para o *serviço de notificação por push* para a plataforma do dispositivo. Alguns exemplos são o serviço APNs (Apple Push Notification Service) para Apple e FCM (Firebase Cloud Messaging) para o Google. Os Hubs de Notificação efetuam push de notificações divididas em diversos lotes de registros. Hubs de Notificação são autenticados com o respectivo serviço de notificação por push com base nas credenciais que você definir no Portal do Azure, em **Configurar Hub de Notificação**. O serviço de notificação por push encaminha as notificações para os respectivos *dispositivos cliente*.

O segmento final da entrega da notificação ocorre entre o serviço de notificação por push da plataforma e o dispositivo. Qualquer um dos quatro componentes principais no processo de notificação por push (cliente, back-end do aplicativo, Hubs de Notificação e o serviço de notificação por push da plataforma) pode fazer com que as notificações sejam removidas. Para obter mais informações sobre a arquitetura dos Hubs de Notificação, consulte [Visão geral dos Hubs de Notificação].

Podem ocorrer falhas para entregar as notificações durante a fase inicial de teste/preparo. Notificações removidas neste estágio podem indicar um problema de configuração. Se ocorrer falha na entrega das notificações em produção, algumas ou todas as notificações poderão ser removidas. Nesse caso, há indicação de um problema de aplicativo ou padrão de mensagens mais profundo.

A próxima seção examina os cenários em que as notificações poderão ser removidas, variando desde casos comuns aos mais raros.

## <a name="notification-hubs-misconfiguration"></a>Configuração incorreta dos Hubs de Notificação

Para poder enviar notificações com êxito ao respectivo serviço de notificação por push, o serviço Hubs de Notificação precisa se autenticar no contexto do aplicativo do desenvolvedor. Para que isso ocorra, o desenvolvedor cria uma conta de desenvolvedor com a respectiva plataforma (Google, Apple, Windows e assim por diante). Em seguida, o desenvolvedor registra seu aplicativo com a plataforma em que ele obtém as credenciais.

Você precisa adicionar as credenciais da plataforma para o Portal do Azure. Se nenhuma notificação está acessando o dispositivo, a primeira etapa deve ser garantir que as credenciais corretas sejam configuradas nos Hubs de Notificação. As credenciais precisam corresponder ao aplicativo que é criado em uma conta de desenvolvedor específica da plataforma.

Para ver instruções passo a passo para concluir esse processo, consulte [Introdução aos Hubs de Notificações do Microsoft Azure].

Aqui estão algumas configurações incorretas comuns para observar:

**Geral:**

    * Verifique se o nome do seu hub de notificação (sem erros de grafia) é o mesmo em todos esses locais:
        * Onde você registra do cliente.
        * Para onde enviar notificações do back-end.
        * Onde você configurou as credenciais do serviço de notificação por push.
    * Verifique se você usou as cadeias de caracteres de configuração de assinatura de acesso compartilhado corretas no cliente e no back-end do aplicativo. Geralmente, é necessário usar **DefaultListenSharedAccessSignature** no cliente e **DefaultFullSharedAccessSignature** no back-end do aplicativo (que concede permissão para enviar notificações para os Hubs de Notificação).

**Configuração de APNs:**

    You must maintain two different hubs: one hub for production, and another hub for testing. This means that you must upload the certificate that you use in a sandbox environment to a separate hub than the certificate and hub that you are going to use in production. Don't try to upload different types of certificates to the same hub. This might cause notification failures.

    If you inadvertently upload different types of certificates to the same hub, we recommend that you delete the hub and start fresh with a new hub. If for some reason you can't delete the hub, at a minimum, you must delete all the existing registrations from the hub.

**Configuração de FCM:**

    1. Verifique se a *chave do servidor* obtida do Firebase corresponde à chave de servidor que você registrou no Portal do Azure.

    ![Chave do servidor Firebase][3]

    2. Verifique se você configurou a **ID do projeto** no cliente. Você pode obter o valor da **ID do projeto** do painel do Firebase.

    ![ID do projeto Firebase][1]

## <a name="application-issues"></a>Problemas de aplicativos

**Marcas e expressões de marca:**

    If you use tags or tag expressions to segment your audience, it's possible that when you send the notification, no target is found based on the tags or tag expressions that you specify in your send call.

    Review your registrations to ensure that there are matching tags when you send a notification. Then, verify the notification receipt only from the clients that have those registrations.

    As an example, if all your registrations with Notification Hubs were made by using the tag "Politics" and you send a notification with the tag "Sports," the notification isn't sent to any device. A complex case might involve tag expressions in which you registered by using "Tag A" OR "Tag B," but while sending notifications, you target "Tag A && Tag B." In the self-diagnosis tips section later in the article, we show you how to review your registrations and their tags.

**Problemas do modelo:**

    If you use templates, ensure that you follow the guidelines described in [Templates].

**Registros inválidos:**

    If the notification hub was configured correctly, and if any tags or tag expressions were used correctly, valid targets are found. Notifications should be sent to these targets. The Notification Hubs service then fires off several processing batches in parallel. Each batch sends messages to a set of registrations.

    > [!NOTE]
    > Because processing is performed in parallel, the order in which the notifications are delivered is not guaranteed.

    Notification Hubs is optimized for an "at-most once" message delivery model. We attempt deduplication, so that no notifications are delivered more than once to a device. To ensure this, we check registrations and ensure that only one message is sent per device identifier before the message is sent to the push notification service.

    As each batch is sent to the push notification service, which in turn is accepting and validating the registrations, it's possible that the push notification service will detect an error with one or more of the registrations in a batch. In this case, the push notification service returns an error to Notification Hubs, and the process stops. The push notification service drops that batch completely. This is especially true with APNS, which uses a TCP stream protocol.

    We are optimized for at-most once delivery. But in this case, the faulting registration is removed from the database. Then, we retry notification delivery for the rest of the devices in that batch.

    To get more error information about the failed delivery attempt against a registration, you can use the Notification Hubs REST APIs [Per Message Telemetry: Get Notification Message Telemetry](https://msdn.microsoft.com/library/azure/mt608135.aspx) and [PNS feedback](https://msdn.microsoft.com/library/azure/mt705560.aspx). For sample code, see the [Send REST example](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample).

## <a name="push-notification-service-issues"></a>Problemas do serviço de notificação por push

Depois que a mensagem de notificação foi recebida pelo serviço de notificação por push da plataforma, é responsabilidade do serviço de notificação por push entregar a notificação para o dispositivo. Nesse ponto, o serviço Hubs de Notificação do Azure fica de fora e não tem controle sobre quando, ou se, a notificação é entregue para o dispositivo.

Como os serviços de notificação de plataforma são robustos, as notificações tendem a acessar os dispositivos com o serviço de notificação por push dentro de alguns segundos. Se o serviço de notificação por push realiza limitação, os Hubs de Notificação aplicam uma estratégia de retirada exponencial. Se o serviço de notificação por push permanece inacessível por 30 minutos, temos uma política em vigor para expirar e remover essas mensagens permanentemente.

Se um serviço de notificação por push tenta entregar uma notificação, mas o dispositivo está offline, a notificação é armazenada pelo serviço por um período limitado. A notificação é entregue ao dispositivo quando ele estiver disponível.

Para cada aplicativo, apenas uma notificação recente é armazenada. Se várias notificações forem enviadas quando o dispositivo estiver offline, cada nova notificação fará com que a notificação anterior seja descartada. Manter somente a notificação mais recente é chamado de *união de notificações* no APNs e *recolhimento* no FCM (que usa uma chave de recolhimento). Se o dispositivo permanecer offline por um longo tempo, as notificações que estavam sendo armazenadas para ele serão descartadas. Para obter mais informações, consulte [Visão geral de APNs] e [Sobre mensagens de FCM].

Com os Hubs de Notificações do Microsoft Azure, você pode passar uma chave de união por meio de um cabeçalho HTTP usando a API SendNotification genérica. Por exemplo, para o SDK do .NET, você usaria `SendNotificationAsync`. A API SendNotification também usa cabeçalhos HTTP que são passados no estado em que se encontram para o respectivo serviço de notificação por push.

## <a name="self-diagnosis-tips"></a>Dicas de autodiagnóstico

Estes são os caminhos para diagnosticar a causa raiz da remoção de notificações em Hubs de Notificação:

### <a name="verify-credentials"></a>Verifique as credenciais

**Portal do desenvolvedor do serviço de notificação por push:**

Verifique as credenciais no respectivo portal do desenvolvedor do serviço de notificação por push (APNs, FCM, Serviço de Notificação do Windows e assim por diante). Para saber mais, veja [Introdução aos Hubs de Notificações do Microsoft Azure].

**Portal do Azure:**

Para examinar e corresponder as credenciais àquelas obtidas do portal do desenvolvedor do serviço de notificação por push, no Portal do Azure, acesse a guia **Políticas de Acesso**.

![Políticas de acesso do Portal do Azure][4]

### <a name="verify-registrations"></a>Verificar registros

**Visual Studio:**

Se você usar o Visual Studio para desenvolvimento, poderá se conectar ao Azure e por meio do Gerenciador de Servidores para exibir e gerenciar vários serviços do Azure, incluindo os Hubs de Notificação. Isso é útil principalmente para seu ambiente de desenvolvimento e teste.

![Gerenciador de Servidores do Visual Studio][9]

Você pode exibir e gerenciar todos os registros no seu hub categorizados por plataforma, registro nativo ou de modelo, marcas, identificador do serviço de notificação por push, ID de registro e data de validade. Também é possível editar um registro nesta página. Isso é especialmente útil para editar marcas.

![Registros de dispositivos do Visual Studio][8]

> [!NOTE]
> Use o Visual Studio para editar os registros somente durante o desenvolvimento e teste e com um número limitado de registros. Se for necessário editar seus registros em massa, considere usar a funcionalidade de exportar e importar registros descrita em [Exportar e modificar registros em massa](https://msdn.microsoft.com/library/dn790624.aspx).

**Gerenciador de Barramento de Serviço:**

Muitos clientes usam o [Explorer do Barramento de Serviço] para exibir e gerenciar o hub de notificação. O Gerenciador de Barramento de Serviço é um projeto de software livre. Para ver exemplos, consulte [código do Gerenciador de Barramento de Serviço].

### <a name="verify-message-notifications"></a>Verificar as notificações de mensagem

 **Portal do Azure:**

Para enviar uma notificação de teste para seus clientes sem precisar de um serviço de back-end em funcionamento, em **SUPORTE + SOLUÇÃO DE PROBLEMAS**, selecione **Envio de Teste**.

![Funcionalidade de Envio de Teste no Azure][7]

**Visual Studio:**

Você também pode enviar notificações de teste do Visual Studio.

![Funcionalidade de Envio de Teste no Visual Studio][10]

Para obter mais informações sobre como usar os Hubs de Notificação com o Gerenciador de Servidores do Visual Studio, consulte estes artigos:

* [Exibir registros de dispositivo para os hubs de notificação]
* [Aprofundamento: Visual Studio 2013 Update 2 RC e SDK 2.3 do Azure]
* [Anunciando o lançamento do Visual Studio 2013 Atualização 3 e SDK do Azure 2.4]

### <a name="debug-failed-notifications-and-review-notification-outcome"></a>Depurar notificações com falha e examinar o resultado da notificação

**Propriedade `EnableTestSend`:**

Quando você enviar uma notificação por meio dos Hubs de Notificação, inicialmente, a notificação é enfileirada para processamento nos Hubs de Notificação. Os Hubs de Notificação determinam os destinos corretos e, em seguida, enviam a notificação para o serviço de notificação por push. Se você estiver usando a API REST ou qualquer SDK cliente, o retorno bem-sucedido da sua chamada de envio significará apenas que a mensagem foi enfileirada com êxito com os Hubs de Notificação. Você não tem nenhuma informação sobre o que aconteceu quando os Hubs de Notificação eventualmente enviaram a mensagem para o serviço de notificação por push.

Caso a notificação não chegue ao dispositivo cliente, é possível que tenha ocorrido um erro quando os Hubs de Notificação tentaram entregar a mensagem para o serviço de notificação por push. Por exemplo, o tamanho do conteúdo poderá exceder o máximo permitido pelo serviço de notificação por push, ou as credenciais configuradas em Hubs de Notificação podem ser inválidas.

Para obter informações sobre erros do serviço de notificação por push, você pode usar a propriedade [EnableTestSend]. Essa propriedade é habilitada automaticamente quando você envia mensagens de teste do portal ou do cliente do Visual Studio. Você pode usar essa propriedade para ver informações detalhadas de depuração. Você também pode usar a propriedade por meio de APIs. No momento, é possível usá-la no SDK do .NET. Eventualmente, ela será adicionada a todos os SDKs de cliente.

Para usar a propriedade `EnableTestSend` com a chamada REST, acrescente um parâmetro de cadeia de consulta chamado *test* ao final da sua chamada de envio. Por exemplo: 

```text
https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test
```

**Exemplo (SDK do .NET):**

Veja este exemplo de como usar o SDK do .NET para enviar uma notificação de pop-up nativo (notificação do sistema):

```csharp
NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
var result = await hub.SendWindowsNativeNotificationAsync(toast);
Console.WriteLine(result.State);
```

No final da execução, `result.State` simplesmente declara `Enqueued`. Os resultados não fornecem nenhuma informação sobre o que aconteceu com a notificação por push.

Em seguida, você pode usar a propriedade booliana `EnableTestSend`. Use a propriedade `EnableTestSend` ao iniciar `NotificationHubClient` para obter um status detalhado sobre os erros do serviço de notificação por push que ocorrem quando a notificação é enviada. A chamada de envio leva tempo adicional para retornar porque ela é retornada somente depois que os Hubs de Notificação entregaram a notificação para o serviço de notificação por push para determinar o resultado.

```csharp
    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }
```

**Saída de exemplo:**

```text
DetailedStateAvailable
windows
7619785862101227384-7840974832647865618-3
The Token obtained from the Token Provider is wrong
```

Esta mensagem indica que credenciais inválidas são configuradas nos Hubs de Notificação ou que há um problema com os registros no hub. É recomendável excluir esse registro e permitir que o cliente recrie o registro antes de enviar a mensagem.

> [!NOTE]
> O uso da propriedade `EnableTestSend` é extremamente limitado. Use esta opção somente em um ambiente de desenvolvimento e teste e com um conjunto limitado de registros. Enviamos notificações de depuração para somente 10 dispositivos. Também há um limite de processamento de envios de depuração de 10 por minuto.

### <a name="review-telemetry"></a>Telemetria de revisão

**Usar o portal do Azure:**

No portal, é possível obter uma visão geral rápida de todas as atividades no seu hub de notificação.

1. Na guia **Visão geral**, é possível ver uma exibição agregada de registros, notificações e erros por plataforma.

    ![Painel Visão geral dos Hubs de Notificação][5]

2. Na guia **Monitor**, você pode adicionar várias outras métricas específicas da plataforma para uma análise mais profunda. Você pode examinar especificamente qualquer erro relacionado ao serviço de notificação por push que retornado quando o serviço Hubs de Notificação tenta enviar a notificação para o serviço de notificação por push.

    ![Log de atividades do Portal do Azure][6]

3. Comece revisando as **Mensagens de entrada**, **Operações de registro** e **Notificações com êxito**. Em seguida, acesse a guia por plataforma para examinar os erros que são específicos para o serviço de notificação por push.

4. Se as configurações de autenticação para o hub de notificação estiverem incorretas, a mensagem **Erro de autenticação do PNS** será exibida. Essa é uma boa indicação para verificar as credenciais do serviço de notificação por push.

* **Acesso programático**

Para obter mais informações sobre acesso programático, consulte esses artigos:

* [Acesso programático à telemetria]  
* [Acesso de telemetria por meio do exemplo de APIs]

> [!NOTE]
> Vários recursos relacionados à telemetria, como exportar e importar os registros e acesso à telemetria por meio de APIs, estão disponíveis apenas na camada de serviço Standard. Se tentar usar esses recursos na camada de serviço Gratuita ou Básica, você receberá uma mensagem de exceção se usar o SDK e um erro de HTTP 403 (Proibido) se usar os recursos diretamente das APIs REST.
>
> Para usar os recursos relacionados à telemetria, verifique primeiro no Portal do Azure se você está usando a camada de serviço Standard.  

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/FCMConfigure.png
[3]: ./media/notification-hubs-diagnosing/FCMServerKey.png
[4]: ../../includes/media/notification-hubs-portal-create-new-hub/notification-hubs-connection-strings-portal.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalAnalytics.png
[7]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Visão geral dos Hubs de Notificação]: notification-hubs-push-notification-overview.md
[Introdução aos Hubs de Notificações do Microsoft Azure]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Templates]: https://msdn.microsoft.com/library/dn530748.aspx
[Visão geral de APNs]: https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html
[Sobre mensagens de FCM]: https://firebase.google.com/docs/cloud-messaging/concept-options
[Export and modify registrations in bulk]: http://msdn.microsoft.com/library/dn790624.aspx
[Explorer do Barramento de Serviço]: https://msdn.microsoft.com/library/dn530751.aspx#sb_explorer
[Código do Gerenciador de Barramento de Serviço]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Exibir registros de dispositivo para os hubs de notificação]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx
[Aprofundamento: Visual Studio 2013 Update 2 RC e SDK 2.3 do Azure]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs
[Anunciando o lançamento do Visual Studio 2013 Atualização 3 e SDK do Azure 2.4]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/
[EnableTestSend]: https://docs.microsoft.com/dotnet/api/microsoft.azure.notificationhubs.notificationhubclient.enabletestsend?view=azure-dotnet
[Acesso programático à telemetria]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Acesso de telemetria por meio do exemplo de APIs]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
