---
title: Notificações por push para aplicativos Android usando Hubs de Notificação do Azure e Firebase Cloud Messaging | Microsoft Docs
description: Neste tutorial, você aprende a usar os Hubs de Notificação do Azure e o Google Firebase Cloud Messaging para enviar notificações por push a dispositivos Android.
services: notification-hubs
documentationcenter: android
keywords: notificações por push, notificação por push, notificação por push do android, fcm, firebase cloud messaging
author: jwargo
manager: patniko
editor: spelluru
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: tutorial
ms.custom: mvc
ms.date: 01/04/2019
ms.author: jowargo
ms.openlocfilehash: d758a46a19dcd109ee5786e25c886dd30b264f7e
ms.sourcegitcommit: 9b6492fdcac18aa872ed771192a420d1d9551a33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54447490"
---
# <a name="tutorial-push-notifications-to-android-devices-by-using-azure-notification-hubs-and-google-firebase-cloud-messaging"></a>Tutorial: Enviar notificações por push para dispositivos Android usando Hubs de Notificação do Azure e Google Firebase Cloud Messaging

[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

> [!IMPORTANT]
> Este artigo demonstra as notificações por push no FCM (Firebase Cloud Messaging) do Google. Se você ainda estiver usando o Google Cloud Messaging (GCM), veja [Notificações por push para dispositivos Android com Hubs de Notificação do Azure e GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).

Este tutorial mostra como usar os Hubs de Notificação do Azure e o Firebase Cloud Messaging para enviar notificações por push a um aplicativo Android. Neste tutorial, você cria um aplicativo Android em branco que recebe notificações por push usando o FCM.

O código completo para este tutorial pode ser baixado no GitHub [clicando aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).

Neste tutorial, você deve executar as seguintes etapas:

> [!div class="checklist"]
> * Criar um projeto do Android Studio.
> * Criar um projeto do Firebase que ofereça suporte ao Firebase Cloud Messaging.
> * Criar um hub de notificação.
> * Conectar seu aplicativo ao hub de notificação.
> * Testar o aplicativo.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este tutorial, você precisa ter uma conta ativa do Azure. Se não tiver uma conta, você poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).

* Além de uma conta ativa do Azure mencionada acima, este tutorial requer a última versão do [Android Studio](https://go.microsoft.com/fwlink/?LinkId=389797).
* Android 2.3 ou superior para Firebase Cloud Messaging.
* A revisão 27 ou superior do Repositório do Google é necessária para o Firebase Cloud Messaging.
* Google Play Services 9.0.2 ou superior para Firebase Cloud Messaging.
* A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Android.

## <a name="create-an-android-studio-project"></a>Criar um projeto do Android Studio

1. No Android Studio, inicie um novo projeto Android Studio.

    ![Android Studio - novo projeto](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. Escolha o fator forma **Telefone e Tablet** e o **SDK Mínimo** ao qual você deseja oferecer suporte. Em seguida, clique em **Próximo**.

    ![Android Studio - fluxo de trabalho de criação de projeto](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. Escolha **Atividade Vazia** para a atividade principal, clique em **Avançar** e em **Concluir**.

## <a name="create-a-firebase-project-that-supports-fcm"></a>Crie um projeto do Firebase que ofereça suporte ao FCM

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Configurar um hub de notificação

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

### <a name="configure-firebase-cloud-messaging-settings-for-the-hub"></a>Definir as configurações do Firebase Cloud Messaging para o hub

1. Selecione **Google (GCM)** na categoria **CONFIGURAÇÕES DE NOTIFICAÇÃO**.
2. Insira a chave de API (chave do servidor FCM) copiada anteriormente do [Console Firebase](https://firebase.google.com/console/).
3. Selecione **Salvar** na barra de ferramentas.

    ![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

Agora, o hub de notificação está configurado para funcionar com o Firebase Cloud Messaging, e você tem as cadeias de conexão para registrar o aplicativo para receber e enviar notificações por push.

## <a id="connecting-app"></a>Conectar seu aplicativo ao hub de notificação

### <a name="add-google-play-services-to-the-project"></a>Adicionar serviços do Google Play ao projeto

[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Como adicionar bibliotecas dos Hubs de Notificação do Azure

1. No arquivo `Build.Gradle` para o **aplicativo**, adicione as linhas a seguir à seção **dependencies**.

    ```text
    compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
    ```

2. Adicione o seguinte repositório após a seção **dependências** .

    ```text
    repositories {
        maven {
            url "http://dl.bintray.com/microsoftazuremobile/SDK"
        }
    }
    ```

### <a name="add-google-firebase-support"></a>Adicionar suporte ao Google Firebase

1. No arquivo `Build.Gradle` para o **aplicativo**, adicione as linhas a seguir à seção **dependencies**.

    ```text
    compile 'com.google.firebase:firebase-core:12.0.0'
    ```

2. Adicione o seguinte plug-in ao final do arquivo.

    ```text
    apply plugin: 'com.google.gms.google-services'
    ```

### <a name="updating-the-androidmanifestxml"></a>Atualização do arquivo AndroidManifest.xml

1. Para dar suporte ao FCM, implemente um serviço de escuta de ID da Instância em seu código, que será usado para [obter tokens do registro](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) usando a [API FirebaseInstanceId do Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId). Neste tutorial, o nome da classe é `MyInstanceIDService`.

    Adicione a seguinte definição de serviço ao arquivo Androidmanifest.xml, dentro da marcação `<application>` .

    ```xml
    <service android:name=".MyInstanceIDService">
        <intent-filter>
            <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
        </intent-filter>
    </service>
    ```

2. Depois de receber seu token de registro FCM da API FirebaseInstanceId, use-o para [registrar com o Hub de Notificação do Azure](notification-hubs-push-notification-registration-management.md). Você oferecerá suporte a esse registro em segundo plano usando um `IntentService` chamado `RegistrationIntentService`. Esse serviço também é responsável por atualizar o token de registro do FCM.

    Adicione a seguinte definição de serviço ao arquivo Androidmanifest.xml, dentro da marcação `<application>` .

    ```xml
    <service
        android:name=".RegistrationIntentService"
        android:exported="false">
    </service>
    ```

3. Defina também um receptor para receber notificações. Adicione a seguinte definição do receptor ao arquivo AndroidManifest.xml, dentro da marcação `<application>` . Substitua o espaço reservado `<your package>` pelo nome do pacote real mostrado na parte superior do arquivo `AndroidManifest.xml`.

    ```xml
    <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
        android:permission="com.google.android.c2dm.permission.SEND">
        <intent-filter>
            <action android:name="com.google.android.c2dm.intent.RECEIVE" />
            <category android:name="<your package name>" />
        </intent-filter>
    </receiver>
    ```

4. Adicione as seguintes permissões necessárias relacionadas ao FCM abaixo da marca `</application>`.

    Para saber mais sobre essas permissões, confira [Configurar um aplicativo de Cliente GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest) e [Migrar um aplicativo de Cliente GCM para Android para o Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).

    ```xml
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    ```

### <a name="adding-code"></a>Como adicionar um código

1. Na Exibição de Projeto, expanda **app** > **src** > **main** > **java**. Clique na pasta do seu pacote em **java**, clique em **Novo** e então clique em **Classe Java**. Adicione uma nova classe denominada `NotificationSettings`.

    ![Android Studio - nova classe de Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)

    Atualize esses três espaços reservados no código a seguir para a classe `NotificationSettings`:

   * **SenderId**: a ID de Remetente obtida anteriormente na guia **Cloud Messaging** de configurações do projeto no [console Firebase](https://firebase.google.com/console/).
   * **HubListenConnectionString**: a cadeia de conexão **DefaultListenAccessSignature** do hub. Copie essa cadeia de conexão clicando em **Políticas de Acesso** no hub no [portal do Azure].
   * **HubName**: use o nome do hub de notificação que aparece na página do hub no [Portal do Azure].

     `NotificationSettings` :

    ```java
    public class NotificationSettings {
        public static String SenderId = "<Your project number>";
        public static String HubName = "<Your HubName>";
        public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
    }
    ```

2. Usando as etapas precedentes, adicione outra classe nova denominada `MyInstanceIDService`. Essa classe é sua implementação do serviço de escuta de ID da Instância.

    O código para essa classe chama `IntentService` para [atualizar o token FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) em segundo plano.

    ```java
    import android.content.Intent;
    import android.util.Log;
    import com.google.firebase.iid.FirebaseInstanceIdService;

    public class MyInstanceIDService extends FirebaseInstanceIdService {

        private static final String TAG = "MyInstanceIDService";

        @Override
        public void onTokenRefresh() {

            Log.d(TAG, "Refreshing GCM Registration Token");

            Intent intent = new Intent(this, RegistrationIntentService.class);
            startService(intent);
        }
    };
    ```

3. Adicione outra classe nova ao projeto denominada `RegistrationIntentService`. Essa classe implementa a interface `IntentService` e processa a [atualização do token FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e o [registro no hub de notificação](notification-hubs-push-notification-registration-management.md).

    Use o código a seguir para essa classe.

    ```java
    import android.app.IntentService;
    import android.content.Intent;
    import android.content.SharedPreferences;
    import android.preference.PreferenceManager;
    import android.util.Log;
    import com.google.firebase.iid.FirebaseInstanceId;
    import com.microsoft.windowsazure.messaging.NotificationHub;

    public class RegistrationIntentService extends IntentService {

        private static final String TAG = "RegIntentService";

        private NotificationHub hub;

        public RegistrationIntentService() {
            super(TAG);
        }

        @Override
        protected void onHandleIntent(Intent intent) {

            SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
            String resultString = null;
            String regID = null;
            String storedToken = null;

            try {
                String FCM_token = FirebaseInstanceId.getInstance().getToken();
                Log.d(TAG, "FCM Registration Token: " + FCM_token);

                // Storing the registration ID that indicates whether the generated token has been
                // sent to your server. If it is not stored, send the token to your server,
                // otherwise your server should have already received the token.
                if (((regID=sharedPreferences.getString("registrationID", null)) == null)){

                    NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                            NotificationSettings.HubListenConnectionString, this);
                    Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                    regID = hub.register(FCM_token).getRegistrationId();

                    // If you want to use tags...
                    // Refer to : https://azure.microsoft.com/documentation/articles/notification-hubs-routing-tag-expressions/
                    // regID = hub.register(token, "tag1,tag2").getRegistrationId();

                    resultString = "New NH Registration Successfully - RegId : " + regID;
                    Log.d(TAG, resultString);

                    sharedPreferences.edit().putString("registrationID", regID ).apply();
                    sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                }

                // Check if the token may have been compromised and needs refreshing.
                else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {

                    NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                            NotificationSettings.HubListenConnectionString, this);
                    Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                    regID = hub.register(FCM_token).getRegistrationId();

                    // If you want to use tags...
                    // Refer to : https://azure.microsoft.com/documentation/articles/notification-hubs-routing-tag-expressions/
                    // regID = hub.register(token, "tag1,tag2").getRegistrationId();

                    resultString = "New NH Registration Successfully - RegId : " + regID;
                    Log.d(TAG, resultString);

                    sharedPreferences.edit().putString("registrationID", regID ).apply();
                    sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                }

                else {
                    resultString = "Previously Registered Successfully - RegId : " + regID;
                }
            } catch (Exception e) {
                Log.e(TAG, resultString="Failed to complete registration", e);
                // If an exception happens while fetching the new token or updating our registration data
                // on a third-party server, this ensures that we'll attempt the update at a later time.
            }

            // Notify UI that registration has completed.
            if (MainActivity.isVisible) {
                MainActivity.mainActivity.ToastNotify(resultString);
            }
        }
    }
    ```

4. Em sua classe `MainActivity`, adicione as seguintes instruções `import` acima da declaração da classe.

    ```java
    import com.google.android.gms.common.ConnectionResult;
    import com.google.android.gms.common.GoogleApiAvailability;
    import com.microsoft.windowsazure.notifications.NotificationsManager;
    import android.content.Intent;
    import android.util.Log;
    import android.widget.TextView;
    import android.widget.Toast;
    ```

5. Adicione os seguintes membros privados na parte superior da classe. Use esses campos para [verificar a disponibilidade do Google Play Services, conforme recomendado pelo Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).

    ```java
    public static MainActivity mainActivity;
    public static Boolean isVisible = false;
    private static final String TAG = "MainActivity";
    private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
    ```

6. Em sua classe `MainActivity` , adicione o seguinte método à disponibilidade dos Serviços do Google Play.

    ```java
    /**
    * Check the device to make sure it has the Google Play Services APK. If
    * it doesn't, display a dialog that allows users to download the APK from
    * the Google Play Store or enable it in the device's system settings.
    */

    private boolean checkPlayServices() {
        GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
        int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
        if (resultCode != ConnectionResult.SUCCESS) {
            if (apiAvailability.isUserResolvableError(resultCode)) {
                apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                        .show();
            } else {
                Log.i(TAG, "This device is not supported by Google Play Services.");
                ToastNotify("This device is not supported by Google Play Services.");
                finish();
            }
            return false;
        }
        return true;
    }
    ```

7. Na classe `MainActivity`, adicione o seguinte código que verifica o Google Play Services antes de chamar o `IntentService` para obter seu token de registro do FCM e registrá-lo com o hub de notificação.

    ```java
    public void registerWithNotificationHubs()
    {
        if (checkPlayServices()) {
            // Start IntentService to register this application with FCM.
            Intent intent = new Intent(this, RegistrationIntentService.class);
            startService(intent);
        }
    }
    ```

8. No método `OnCreate` da classe `MainActivity`, adicione o código a seguir para começar o processo de registro quando a atividade for criada.

    ```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mainActivity = this;
        NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
        registerWithNotificationHubs();
    }
    ```

9. Para verificar o estado do aplicativo e informar o status em seu aplicativo, adicione esses métodos adicionais a `MainActivity`.

    ```java
    @Override
    protected void onStart() {
        super.onStart();
        isVisible = true;
    }

    @Override
    protected void onPause() {
        super.onPause();
        isVisible = false;
    }

    @Override
    protected void onResume() {
        super.onResume();
        isVisible = true;
    }

    @Override
    protected void onStop() {
        super.onStop();
        isVisible = false;
    }

    public void ToastNotify(final String notificationMessage) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                TextView helloText = (TextView) findViewById(R.id.text_hello);
                helloText.setText(notificationMessage);
            }
        });
    }
    ```

10. O método `ToastNotify` usa o controle *"Hello World"* `TextView` para informar de forma persistente o status e as notificações no aplicativo. No layout activity_main.xml, adicione a seguinte ID para esse controle.

    ```java
    android:id="@+id/text_hello"
    ```

11. Em seguida, adicione uma subclasse para o receptor que você definiu no AndroidManifest.xml. Adicione outra classe nova ao projeto denominada `MyHandler`.

12. Adicione as seguintes instruções de importação na parte superior de `MyHandler.java`:

    ```java
    import android.app.NotificationManager;
    import android.app.PendingIntent;
    import android.content.Context;
    import android.content.Intent;
    import android.media.RingtoneManager;
    import android.net.Uri;
    import android.os.Bundle;
    import android.support.v4.app.NotificationCompat;
    import com.microsoft.windowsazure.notifications.NotificationsHandler;
    ```

13. Adicione o código a seguir à classe `MyHandler`, tornando-a uma subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.

    Esse código substitui o método `OnReceive` para que o manipulador informe as notificações recebidas. O manipulador também envia a notificação por push ao gerenciador de notificações do Android usando o método `sendNotification()` . O método `sendNotification()` deve ser executado quando o aplicativo não está em execução e uma notificação é recebida.

    ```java
    public class MyHandler extends NotificationsHandler {
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
        Context ctx;

        @Override
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String nhMessage = bundle.getString("message");
            sendNotification(nhMessage);
            if (MainActivity.isVisible) {
                MainActivity.mainActivity.ToastNotify(nhMessage);
            }
        }

        private void sendNotification(String msg) {

            Intent intent = new Intent(ctx, MainActivity.class);
            intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);

            mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);

            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                    intent, PendingIntent.FLAG_ONE_SHOT);

            Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
            NotificationCompat.Builder mBuilder =
                    new NotificationCompat.Builder(ctx)
                            .setSmallIcon(R.mipmap.ic_launcher)
                            .setContentTitle("Notification Hub Demo")
                            .setStyle(new NotificationCompat.BigTextStyle()
                                    .bigText(msg))
                            .setSound(defaultSoundUri)
                            .setContentText(msg);

            mBuilder.setContentIntent(contentIntent);
            mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
    }
    ```

14. No Android Studio, na barra de menus, clique em **Compilar** > **Recompilar Projeto** para garantir que não haja erros presentes no código.

15. Execute o aplicativo em seu dispositivo e verifique se ele se registra com êxito no hub de notificação.

    > [!NOTE]
    > O registro poderá falhar na primeira inicialização até que o método `onTokenRefresh()` do serviço de ID da instância seja chamado. A atualização deve iniciar um registro bem-sucedido com o hub de notificação.

## <a name="test-the-app"></a>Testar o aplicativo

### <a name="test-send-notification-from-the-notification-hub"></a>Teste enviar notificação pelo hub de notificação

Você pode enviar notificações por push pelo [Portal do Azure] da seguinte maneira:

1. Selecione **Envio de Teste** na seção **Solução de Problemas**.
2. Em **Plataformas**, selecione **Android**.
3. Selecione **Enviar**.  Você ainda não vê uma notificação no dispositivo Android porque não executou o aplicativo móvel nele. Depois de executar o aplicativo móvel, selecione **Enviar** novamente para ver a mensagem de notificação.
4. Consulte o **resultado** da operação na lista na parte inferior.

    ![Hubs de notificação do Azure - Testar Enviar](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

### <a name="run-the-mobile-app"></a>Executar o aplicativo móvel

Para testar notificações por push em um emulador, verifique se a imagem de emulador dá suporte ao nível de API do Google que você escolheu para o aplicativo. Se sua imagem não for compatível com as APIs nativas do Google, você verá a exceção **SERVICE\_NOT\_AVAILABLE**.

Além disso, verifique se você adicionou a conta do Google ao emulador em execução em **Configurações** > **Contas**. Caso contrário, suas tentativas de se registrar no GCM podem resultar na exceção **AUTHENTICATION\_FAILED**.

1. Execute o aplicativo e observe que a ID de registro é relatada para um registro bem-sucedido.

    ![Como testar no Android - registro de canal](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. Insira uma mensagem de notificação a ser enviada para todos os dispositivos Android registrados no hub.

    ![Como testar no Android - envio de uma mensagem](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. Pressione **Enviar Notificação**. Qualquer dispositivo com o aplicativo em execução mostrará uma instância de `AlertDialog` com a mensagem de notificação por push. Dispositivos que não tiverem o aplicativo em execução, mas foram registrados anteriormente para notificações por push, receberão uma notificação no Gerenciador de Notificações do Android. As notificação podem ser exibidas passando o dedo do canto superior esquerdo para baixo.

    ![Como testar no Android - notificações](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você usou Firebase Cloud Messaging para enviar notificações por push a dispositivos Android. Para saber como enviar notificações por push usando o Google Cloud Messaging, avance ao seguinte tutorial:

> [!div class="nextstepaction"]
>[Notificações por push para dispositivos Android usando o Google Cloud Messaging](notification-hubs-android-push-notification-google-gcm-get-started.md)

<!-- Images. -->

<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md
[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Portal do Azure]: https://portal.azure.com
