---
title: Configurar o ingresso no Azure Active Directory híbrido para os domínios federados | Microsoft Docs
description: Saiba como configurar o ingresso no Azure Active Directory híbrido para domínios federados.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.subservice: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/08/2019
ms.author: markvi
ms.reviewer: sandeo
ms.openlocfilehash: 760a1db68021146720e0a8e5c872d74bd2c153da
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2019
ms.locfileid: "55101509"
---
# <a name="tutorial-configure-hybrid-azure-active-directory-join-for-federated-domains"></a>Tutorial: Configurar o ingresso no Azure Active Directory híbrido para os domínios federados

De maneira semelhante a um usuário, um dispositivo está se tornando outra identidade que você deseja proteger e também usa para proteger seus recursos a qualquer hora e local. É possível atingir essa meta, colocando as identidades dos dispositivos no Azure AD usando um dos métodos a seguir:

- Ingresso no Azure AD
- Ingresso no Azure AD Híbrido
- Registro do Azure AD

Ao colocar os dispositivos no Azure AD, você maximiza a produtividade dos usuários por meio de SSO (logon único) em toda a nuvem e recursos locais. Ao mesmo tempo, é possível proteger o acesso à sua nuvem e aos recursos locais com [acesso condicional](../active-directory-conditional-access-azure-portal.md).

Neste tutorial, você aprenderá como configurar o ingresso no Azure AD híbrido para dispositivos federados usando ADFS.

> [!div class="checklist"]
> * Configurar ingresso no Azure AD híbrido
> * Habilitar dispositivos de nível inferior do Windows
> * Verificar o registro
> * Solucionar problemas


## <a name="prerequisites"></a>Pré-requisitos

Este tutorial assume que você está familiarizado com:

-  [Introdução ao gerenciamento de dispositivos no Azure Active Directory](../device-management-introduction.md)

-  [Como planejar a implementação de ingresso no Azure Active Directory híbrido](hybrid-azuread-join-plan.md)

-  [Como controlar o ingresso no Azure AD híbrido de seus dispositivos](hybrid-azuread-join-control.md)



Para configurar o cenário neste tutorial, é necessário ter:

- Windows Server 2012 R2 com AD FS

- [Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) versão 1.1.819.0 ou posterior. 
 

A partir da versão 1.1.819.0, o Azure AD Connect fornece um assistente para configurar o ingresso no Azure AD híbrido. O assistente permite simplificar significativamente o processo de configuração. O assistente relacionado:

- Configura SCP (pontos de conexão de serviço) para registro do dispositivo

- Faz backup da terceira parte confiável do Azure AD

- Atualiza as regras de declaração na confiança do Azure AD

As etapas de configuração neste artigo são baseadas nesse assistente. Se você tiver uma versão mais antiga do Azure AD Connect instalada, será necessário atualizá-la para a versão 1.1.819 ou superior. Se a instalação da última versão do Azure AD Connect não for uma opção, consulte [como configurar manualmente o registro do dispositivo](../device-management-hybrid-azuread-joined-devices-setup.md).

O ingresso no Azure AD híbrido requer que os dispositivos tenham acesso aos seguintes recursos da Microsoft dentro da rede da organização:  

- https\://enterpriseregistration.windows.net
- https\://login.microsoftonline.com
- https\://device.login.microsoftonline.com
- STS de sua organização (domínios federados)
- https\://autologon.microsoftazuread-sso.com (se estiver usando ou planejando usar o SSO contínuo)

Começando com o Windows 10 1803, se o ingresso instantâneo no Azure AD híbrido para domínio federado como AD FS falhar, dependeremos do Azure AD Connect para sincronizar o objeto de computador no Azure AD que será usado posteriormente para concluir o registro de dispositivo para ingresso no Azure AD híbrido.

Se a organização precisar de acesso à Internet por meio de um proxy de saída, iniciando com Windows 10 1709, será possível [definir as configurações de proxy no computador usando um GPO (Objeto de Política de Grupo)](https://blogs.technet.microsoft.com/netgeeks/2018/06/19/winhttp-proxy-settings-deployed-by-gpo/). Se o computador estiver executando uma versão mais antiga que Windows 10 1709, será necessário implementar WPAD (Descoberta Automática de Proxy da Web) para permitir que computadores com Windows 10 façam o registro do dispositivo com Azure AD. 

Se a organização exigir acesso à Internet por meio de um proxy de saída autenticado, será necessário garantir que os computadores com Windows 10 possam ser autenticados com êxito no proxy de saída. Como computadores com Windows 10 executam o registro de dispositivos usando o contexto do computador, será necessário configurar a autenticação de proxy de saída usando o contexto do computador. Acompanhe com o provedor de proxy de saída nos requisitos de configuração. 


## <a name="configure-hybrid-azure-ad-join"></a>Configurar ingresso no Azure AD híbrido

Para configurar um ingresso no Azure AD híbrido usando o Azure AD Connect, será necessário ter:

- Credenciais de um administrador global para o locatário do Azure AD.  

- As credenciais de administrador corporativo para cada uma das florestas.

- As credenciais do administrador do AD FS. 


**Para configurar um ingresso no Azure AD híbrido usando o Azure AD Connect:**

1. Inicie o Azure AD Connect e clique em **Configurar**.

    ![Bem-Vindo](./media/hybrid-azuread-join-federated-domains/11.png)

2. Na página **Tarefas adicionais**, selecione **Configurar opções de dispositivo** e, em seguida, clique em **Avançar**. 

    ![Tarefas adicionais](./media/hybrid-azuread-join-federated-domains/12.png)

3. Na página de **Visão Geral**, clique em **Avançar**. 

    ![Visão geral](./media/hybrid-azuread-join-federated-domains/13.png)

4. Na página **Conectar o Azure AD**, insira as credenciais de um administrador global para o locatário do Azure AD e clique em**Avançar**.   

    ![Conecte-se ao AD do Azure](./media/hybrid-azuread-join-federated-domains/14.png)

5. Na página **Opções do dispositivo**, selecione **Configurar ingresso no Azure AD Híbrido** e, em seguida, clique em **Avançar**. 

    ![Opções do dispositivo](./media/hybrid-azuread-join-federated-domains/15.png)

6. Na página **SCP**, execute as etapas a seguir e, em seguida, clique em **Avançar**: 

    ![SCP](./media/hybrid-azuread-join-federated-domains/16.png)

     a. Selecione a floresta.

    b. Selecione o serviço de autenticação. Você deve selecionar o servidor do AD FS, a menos que sua organização tenha exclusivamente os clientes do Windows 10 e você tiver configurado a sincronização do computador/dispositivo ou sua organização estiver usando SSO de conexão remota.

    c. Clique em **Adicionar** para inserir as credenciais do administrador corporativo.


7. Na página **Sistemas operacionais do dispositivo**, selecione os sistemas operacionais usados pelos dispositivos no ambiente do Active Directory e clique em **Avançar**. 

    ![Sistema operacional do dispositivo](./media/hybrid-azuread-join-federated-domains/17.png)

8. Na página **Configuração de federação**, insira as credenciais do administrador do AD FS e clique em **Avançar**. 

    ![Configuração de federação](./media/hybrid-azuread-join-federated-domains/18.png)

9. Na página **Pronto para configurar**, clique em **Configurar**. 

    ![Pronto para configurar](./media/hybrid-azuread-join-federated-domains/19.png)

10. Na página **Configuração completa**, clique em **Sair**. 

    ![Configuração concluída](./media/hybrid-azuread-join-federated-domains/20.png)




## <a name="enable-windows-down-level-devices"></a>Habilitar dispositivos de nível inferior do Windows

Se alguns dos seus dispositivos ingressados no domínio forem dispositivos de nível inferior do Windows, será necessário:

- Atualizar configurações do dispositivo
 
- Definir as configurações de Intranet Local para registro do dispositivo

- Controlar os dispositivos de nível inferior do Windows 


### <a name="update-device-settings"></a>Atualizar configurações do dispositivo 

Para registrar os dispositivos de nível inferior do Windows, será necessário verificar se as configurações do dispositivo para permitir que os usuários registrem dispositivos no Azure AD estão definidas. No portal do Azure, é possível localizar essas configurações em:

`Home > [Name of your tenant] > Devices - Device settings`  


    
A política a seguir deve ser definida como **Tudo**: **Os usuários podem registrar seus dispositivos com o Azure AD**

![Registrar dispositivos](./media/hybrid-azuread-join-federated-domains/23.png)


### <a name="configure-the-local-intranet-settings-for-device-registration"></a>Definir as configurações de Intranet Local para registro do dispositivo

Para concluir com êxito o ingresso no Azure AD híbrido dos dispositivos de nível inferior do Windows e evitar prompts de certificado quando os dispositivos autenticarem no Azure AD, envie uma política por push aos dispositivos ingressados no domínio para adicionar as seguintes URLs à zona da Intranet Local no Internet Explorer:

- `https://device.login.microsoftonline.com`

- Serviço de Token de Segurança da organização (STS - domínios federados)

- `https://autologon.microsoftazuread-sso.com` (para SSO Contínuo).

Além disso, é necessário habilitar **Permitir atualizações na barra de status via script** na zona da Intranet Local do usuário.



### <a name="control-windows-down-level-devices"></a>Controlar os dispositivos de nível inferior do Windows 

Para registrar os dispositivos de nível inferior do Windows, é necessário baixar e instalar um pacote do Windows Installer (.msi) do Centro de Download. Para saber mais, clique [aqui](hybrid-azuread-join-control.md#control-windows-down-level-devices). 

## <a name="verify-the-registration"></a>Verificar o registro

Para verificar o estado do registro do dispositivo no locatário do Azure, é possível usar o cmdlet **[Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)** no **[módulo do PowerShell do Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0)**.

Ao usar o cmdlet **Get-MSolDevice** para verificar os detalhes do serviço:

- Deverá existir um objeto com a **identificação do dispositivo**  correspondendo com a ID no cliente do Windows.
- O valor para **DeviceTrustType** deverá ser **Ingressado no Domínio**. Isso equivale ao estado **ingressado no Azure AD híbrido** na página Dispositivos no portal do Azure AD.
- O valor para **Habilitado** deverá ser **True** e **DeviceTrustLevel** deve ser **Gerenciado** para dispositivos usados em acesso condicional. 


**Para verificar os detalhes do serviço:**

1. Abra o **Windows PowerShell** como administrador.

2. Digite `Connect-MsolService` para conectar o locatário do Azure.  

3. Digite `get-msoldevice -deviceId <deviceId>`.

6. Verifique se **Habilitado** está definido como **Verdadeiro**.





## <a name="troubleshoot-your-implementation"></a>Solucionar problemas de implementação

Se estiver tendo problemas para concluir o ingresso do Azure AD híbrido para dispositivos Windows ingressados no domínio, consulte:

- [Solucionar problemas de ingresso no Azure AD Híbrido para dispositivos atuais do Windows](troubleshoot-hybrid-join-windows-current.md)
- [Solucionar problemas de ingresso no Azure AD Híbrido para dispositivos de nível inferior do Windows](troubleshoot-hybrid-join-windows-legacy.md)



## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Configurar ingresso no Azure Active Directory híbrido para domínios federados](hybrid-azuread-join-managed-domains.md)
> [Configurar ingresso no Azure Active Directory híbrido manualmente](hybrid-azuread-join-manual-steps.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
