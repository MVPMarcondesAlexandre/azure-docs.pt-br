---
title: Configurar ferramentas do Azure Stream Analytics para Visual Studio
description: Este artigo descreve os requisitos de instalação e como instalar as ferramentas do Azyre Stream Analytics para Visual Studio.
services: stream-analytics
author: su-jie
ms.author: sujie
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 05/22/2018
ms.openlocfilehash: 47bdbc2297fb1e1ef24f13710391b4e9d154d37c
ms.sourcegitcommit: c2c279cb2cbc0bc268b38fbd900f1bac2fd0e88f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2018
ms.locfileid: "49983815"
---
# <a name="install-azure-stream-analytics-tools-for-visual-studio"></a>Instalar o Azure Stream Analytics Tools para Visual Studio
As ferramentas do Azure Stream Analytics são compatíveis com o Visual Studio 2017, 2015 e 2013. Este artigo descreve como instalar e desinstalar as ferramentas.

Para obter mais informações sobre como usar as ferramentas, veja [Ferramentas do Stream Analytics para Visual Studio](stream-analytics-quick-create-vs.md).

## <a name="install"></a>Instalar
### <a name="visual-studio-2017"></a>Visual Studio 2017
* Baixe o [Visual Studio 2017 (15.3 ou acima)](https://www.visualstudio.com/). As edições Enterprise (Ultimate/Premium), Professional, Community têm suporte. Não há suporte para a Edição Express. 
* As ferramentas do Stream Analytics são parte das cargas de trabalho de **Desenvolvimento do Azure** e de **Armazenamento e processamento de dados** no Visual Studio 2017. Habilite qualquer uma dessas duas cargas de trabalho como parte da instalação do Visual Studio.

Habilite a carga de trabalho de **Armazenamento e processamento de dados** conforme mostrado:

![A carga de trabalho de armazenamento e processamento de dados é selecionada](./media/stream-analytics-tools-for-visual-studio-install/stream-analytics-tools-for-vs-2017-install-01.png)

Habilite a carga de trabalho de **Desenvolvimento do Azure** conforme mostrado:

![A carga de trabalho de desenvolvimento do Azure é selecionada](./media/stream-analytics-tools-for-visual-studio-install/stream-analytics-tools-for-vs-2017-install-02.png)

* No menu Ferramentas, clique em **Extensões e Atualizações**. Encontre as ferramentas do Azure Data Lake e do Stream Analytics nas extensões instaladas e clique em **Atualizar** para instalar a extensão mais recente. 

![Extensões e atualizações do Visual Studio](./media/stream-analytics-tools-for-visual-studio-install/stream-analytics-tools-for-vs-extensions-updates.png)

### <a name="visual-studio-2013-2015"></a>Visual Studio 2013, 2015
* Instale o Visual Studio 2015 ou o Visual Studio 2013 Atualização 4. As edições Enterprise (Ultimate/Premium), Professional, Community têm suporte. Não há suporte para a Edição Express. 
* Instale o SDK do Microsoft Azure para .NET versão 2.7.1 ou posterior usando o [Web platform installer](https://www.microsoft.com/web/downloads/platform.aspx).
* Instalar o [Azure Stream Analytics Tools para Visual Studio](https://www.microsoft.com/en-us/download/details.aspx?id=49504).

## <a name="update"></a>Atualizar

### <a name="visual-studio-2017"></a>Visual Studio 2017
O novo lembrete de versão aparece na notificação do Visual Studio.

![Lembrete de nova versão do Visual Studio](./media/stream-analytics-tools-for-visual-studio-install/stream-analytics-new-version-reminder-vs-tools.png)

### <a name="visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 e Visual Studio 2015
As ferramentas do Stream Analytics instaladas para o Visual Studio verificam automaticamente em busca de novas versões. Siga as instruções na janela pop-up para instalar a versão mais recente. 


## <a name="uninstall"></a>Desinstalar

### <a name="visual-studio-2017"></a>Visual Studio 2017
Clique duas vezes no instalador do Visual Studio e selecione **Modificar**. Desmarque a caixa de seleção **Azure Data Lake e Stream Analytics Tools** da carga de trabalho de **Armazenamento de dados e processamento** ou da carga de trabalho do **Desenvolvimento do Azure**.

### <a name="visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 e Visual Studio 2015
Vá para o Painel de Controle e desinstale o **Microsoft Azure Data Lake e Ferramentas do Stream Analytics para Visual Studio**.





