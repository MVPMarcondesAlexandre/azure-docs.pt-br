---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 01/07/2019
ms.author: alkohli
ms.openlocfilehash: c7e5231650ec1afb97a72ec0cf26cb8f80088b63
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54440466"
---
Etapa final é preparar o dispositivo para o envio. Nesta etapa, todos os compartilhamentos do dispositivo são colocados offline. As ações não poderão ser acessadas depois que você iniciar esse processo.

> [!IMPORTANT]
> A preparação para o envio é obrigatória, pois sinaliza os dados que não estão em conformidade com as convenções de nomenclatura do Azure. Ignorar essa etapa pode causar eventuais falhas no upload dos dados devido a dados fora de conformidade.

1. Vá para **Preparar para enviar** e clique em **Iniciar preparação**. Por padrão, as somas de verificação são computadas embutidas ao preparar para o envio. O cálculo da soma de verificação pode levar de horas a dias dependendo do tamanho dos seus dados. 
   
    ![Preparar para o envio 1](media/data-box-prepare-to-ship/prepare-to-ship1.png)

    Se, por algum motivo, você desejar interromper a preparação do dispositivo, clique em **Parar a preparação**. É possível retomar a preparação para o envio mais tarde.
        
    ![Preparar para o envio 2](media/data-box-prepare-to-ship/prepare-to-ship2.png)
    
2. A preparação para o envio é iniciada e os compartilhamentos do dispositivo ficam offline. Você verá um lembrete para baixar a etiqueta de remessa depois que o dispositivo estiver pronto.

    ![Baixar o lembrete da etiqueta de remessa](media/data-box-prepare-to-ship/download-shipping-label-reminder.png)

3. O status do dispositivo é atualizado para *Pronto para envio* e o dispositivo será bloqueado depois que sua preparação for concluída.
        
    ![Preparar para o envio 3](media/data-box-prepare-to-ship/prepare-to-ship3.png)

    Se desejar copiar mais dados para o dispositivo, será possível desbloqueá-lo, copiar mais dados e executar a preparação para o envio novamente.

    Se houver erros nesta etapa, será necessário baixar o log de erros e resolvê-los. Depois de resolver os erros, execute **Preparar para o envio**.

4. Depois que a preparação para o envio for concluída com êxito (sem erros), baixe a lista de arquivos (também conhecida como o manifesto) copiada neste processo. Posteriormente, você poderá usar essa lista para verificar os arquivos carregados no Azure.
        
    ![Preparar para o envio 1](media/data-box-prepare-to-ship/prepare-to-ship4.png)

5. Desligar o dispositivo. Vá para **desligar ou reiniciar** da página e clique em **desligar**. Quando solicitado a confirmação, clique em **OK** para continuar.

6. Remova os cabos. A próxima etapa é enviar o dispositivo à Microsoft.
