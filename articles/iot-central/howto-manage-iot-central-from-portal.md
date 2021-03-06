---
title: Gerenciar IoT Central do portal do Azure | Microsoft Docs
description: Gerenciar IoT Central do portal do Azure.
services: iot-central
ms.service: iot-central
author: dominicbetts
ms.author: dobett
ms.date: 01/14/2019
ms.topic: conceptual
manager: philmea
ms.openlocfilehash: 89109dec83342a8f4b5962778b1803eb36656e42
ms.sourcegitcommit: a1cf88246e230c1888b197fdb4514aec6f1a8de2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54352199"
---
# <a name="manage-iot-central-from-the-azure-portal"></a>Gerenciar IoT Central do portal do Azure

Em vez de criar e gerenciar aplicativos do IoT Central da página [Gerenciador de Aplicativos](https://aka.ms/iotcentral) do IoT Central, você pode usar o [portal do Azure](https://portal.azure.com) para gerenciá-los.

## <a name="create-iot-central-applications"></a>Criar aplicativos do IoT Central

Para criar um aplicativo, navegue até o [portal do Azure](https://ms.portal.azure.com) e clique em **Criar um recurso** no menu de navegação principal à esquerda.

![Portal de gerenciamento: menu de navegação](media/howto-manage-iot-central-from-portal/image0.png)

Na barra de pesquisa, digite **IoT Central**.

![Portal de gerenciamento: pesquisar](media/howto-manage-iot-central-from-portal/image0a.png)

Clique no item de linha **Aplicativo do IoT Central** nos resultados da pesquisa.

![Portal de gerenciamento: resultados da pesquisa](media/howto-manage-iot-central-from-portal/image0b.png)

Agora, clique no botão **Criar**.

![Portal de gerenciamento: Recursos de IoT Central](media/howto-manage-iot-central-from-portal/image0c.png)

Preencha todos os campos no formulário. Este formulário é semelhante ao formulário que você preenche para criar aplicativos na página do [Gerenciador de Aplicativos](https://aka.ms/iotcentral) do IoT Central. Para obter mais informações, confira o guias de início rápido [Criar um aplicativo do IoT Central](quick-deploy-iot-central.md).

![Portal de gerenciamento: criar recurso do IoT Central](media/howto-manage-iot-central-from-portal/image1.png)  

Após preencher todos os campos, clique no botão **Criar**.

## <a name="manage-existing-iot-central-applications"></a>Gerenciar aplicativos do IoT Central existentes

Se você já tiver um aplicativo do Azure IoT Central, poderá excluí-lo ou movê-lo para uma assinatura ou grupo de recursos diferente no portal do Azure.

> [!NOTE]
> Você não pode ver aplicativos de avaliação no portal do Azure porque eles não estão associados com sua assinatura.

Para começar, clique em **Todos os recursos** no menu de navegação principal à esquerda. Use a caixa de pesquisa para digitar o nome do aplicativo para localizá-lo na lista de recursos. Em seguida, clique no aplicativo do IoT Central que você quer gerenciar.

![Portal de gerenciamento: gerenciamento de recursos](media/howto-manage-iot-central-from-portal/image2.png)

Para navegar até o aplicativo, clique na URL do aplicativo do IoT Central.

![Portal de gerenciamento: gerenciamento de recursos](media/howto-manage-iot-central-from-portal/image3.png)

Para mover o aplicativo para um grupo de recursos diferente, clique em **alterar** ao lado do grupo de recursos. Na página **Mover recursos**, escolha o grupo de recursos para o qual você deseja migrar esse aplicativo.

![Portal de gerenciamento: gerenciamento de recursos](media/howto-manage-iot-central-from-portal/image4.png)

Para mover o aplicativo para uma assinatura diferente, clique no link **alterar** ao lado da assinatura. Escolha a assinatura para a qual você deseja migrar esse aplicativo na caixa de diálogo exibida.

![Portal de gerenciamento: gerenciamento de recursos](media/howto-manage-iot-central-from-portal/image5.png)

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu a gerenciar os aplicativos do Azure IoT Central no portal do Azure, aqui está a próxima etapa sugerida:

> [!div class="nextstepaction"]
> [Administrar o aplicativo](howto-administer.md)