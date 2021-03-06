---
title: Remover dados pessoais – Proxy de Aplicativo do Azure Active Directory | Microsoft Docs
description: Remova dados pessoais de conectores instalados em dispositivos para o Proxy de Aplicativo do Azure Active Directory.
documentationcenter: ''
author: barbkess
manager: daveba
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b17d3b339bf2c873e8e4c02586e814febfefaec
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55177331"
---
# <a name="remove-personal-data-for-azure-active-directory-application-proxy"></a>Remover dados pessoais para o Proxy de Aplicativo do Azure Active Directory  

O Proxy de Aplicativo do Azure Active Directory exige que você instale conectores em seus dispositivos, o que significa que pode haver dados pessoais em seus dispositivos. Este artigo fornece as etapas para excluir esses dados pessoais para melhorar a privacidade. 


## <a name="where-is-the-personal-data"></a>Onde estão os dados pessoais?
O Proxy de Aplicativo pode gravar dados pessoais para os seguintes tipos de log:

- Logs de eventos do conector
- Logs de eventos do Windows

## <a name="remove-personal-data-from-windows-event-logs"></a>Remover dados pessoais dos logs de eventos do Windows

Para obter informações sobre como configurar a retenção de dados para os logs de eventos do Windows, confira [Configurações dos logs de eventos](https://technet.microsoft.com/library/cc952132.aspx). Para saber mais sobre os logs de eventos do Windows, confira [Usando o log de eventos do Windows](https://msdn.microsoft.com/library/windows/desktop/aa385772.aspx).

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-hybrid-note.md)]

## <a name="remove-personal-data-from-connector-event-logs"></a>Remover dados pessoais dos logs de eventos do conector

Para garantir que os logs de Proxy do Aplicativo não têm dados pessoais, você pode:

- Excluir ou exibir dados quando necessário ou
- Desativar registro em log

Use as seções a seguir para remover dados pessoais dos logs de eventos do conector. Você deve concluir o processo de remoção de todos os dispositivos em que o conector está instalado.

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

### <a name="view-or-export-specific-data"></a>Exibir ou exportar dados específicos

Para exibir ou exportar dados específicos, procure entradas relacionadas em cada um dos logs de eventos do conector. Os logs estão localizados em `C:\ProgramData\Microsoft\Microsoft AAD Application Proxy Connector\Trace`. 

Como os logs são arquivos de texto, você pode usar [findstr](https://docs.microsoft.com/windows-server/administration/windows-commands/findstr) para pesquisar entradas de texto relacionadas a um usuário.  

Para localizar dados pessoais, pesquise os arquivos de log por UserID. 

Para localizar dados pessoais registrados por um aplicativo que usa a delegação restrita de Kerberos, pesquise esses componentes do tipo de nome de usuário:

- UPN local
- Nome de usuário que faz parte do UPN
- Nome de usuário que faz parte do UPN local
- Nome de conta de SAM (gerenciador de contas de segurança) local 


### <a name="delete-specific-data"></a>Excluir dados específicos

Para excluir dados específicos:

1. Reinicie o serviço do Conector do Proxy de Aplicativo do Microsoft Azure AD para gerar um novo arquivo de log. O novo arquivo de log permite excluir ou modificar os arquivos de log antigos. 
2. Siga o processo de [Exibir ou exportar dados específicos](#view-or-export-specific-data) descrito anteriormente para encontrar as informações que precisam ser excluídas. Pesquise todos os logs de conector.
3. Exclua os arquivos de log relevantes ou exclua seletivamente os campos que contêm dados pessoais. Também é possível excluir todos os arquivos de log antigos, caso não sejam mais necessários.

### <a name="turn-off-connector-logs"></a>Desativar os logs do conector

Uma opção para garantir que os logs do conector não contenham dados pessoais é desativar a geração de logs. Para interromper a geração de logs do conector, remova a seguinte linha realçada de `C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config`. 

![Configuração](./media/application-proxy-remove-personal-data/01.png)


## <a name="next-steps"></a>Próximas etapas

Para obter uma visão geral do Proxy de Aplicativo, confira [Como fornecer acesso remoto seguro a aplicativos locais](application-proxy.md).

