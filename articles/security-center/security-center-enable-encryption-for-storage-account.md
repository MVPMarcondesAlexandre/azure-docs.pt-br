---
title: Habilitar criptografia para conta de armazenamento na Central de Segurança do Azure | Microsoft Docs
description: Este documento mostra como implementar as recomendações da Central de Segurança do Azure **Habilitar criptografia para Conta de Armazenamento do Azure**.
services: security-center
documentationcenter: na
author: rkarlin
manager: MBaldwin
editor: ''
ms.assetid: ''
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/28/2018
ms.author: rkarlin
ms.openlocfilehash: 727e0cc7f0dac18a6ac9e97b3c6edae3ba8f62d6
ms.sourcegitcommit: edacc2024b78d9c7450aaf7c50095807acf25fb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53338015"
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Habilitar criptografia para conta de armazenamento do Azure na Central de Segurança do Azure
A Central de Segurança do Azure pode aconselhar você a habilitar a Criptografia do Serviço de Armazenamento do Azure para dados em repouso.

A SSE (Criptografia do Serviço de Armazenamento) funciona criptografando os dados quando eles são gravados no armazenamento do Azure e descriptografando-os antes da recuperação.  Atualmente, a SSE está disponível somente para o serviço Blob do Azure e pode ser usada para blobs de blocos, blobs de páginas e blobs de acréscimo.  Para saber mais, confira [Criptografia do Serviço de Armazenamento para dados em repouso](../storage/common/storage-service-encryption.md).


> [!Note]
> Depois de habilitar a criptografia, somente dados novos serão criptografados. Todos os blobs existentes em sua conta de armazenamento permanecem descriptografados. Para criptografar os blobs existentes, confira as [perguntas frequentes sobre a Criptografia do Serviço de Armazenamento](../storage/common/storage-service-encryption.md#faq-for-storage-service-encryption).
>
>

A Criptografia do Serviço de Armazenamento é compatível apenas com contas de armazenamento do Resource Manager. Atualmente, não há suporte para contas de armazenamento clássicas. Para entender os modelos de implantação clássicos e do Resource Manager, confira [Modelos de implantação do Azure](../azure-classic-rm.md).

> [!NOTE]
> Este documento apresenta o serviço usando uma implantação de exemplo.  Este documento não é um guia passo a passo.
>
>

## <a name="implement-the-recommendation"></a>Implementar a recomendação
1. Na folha **Recomendações**, escolha **Habilitar criptografia para Conta de Armazenamento do Azure**.
   ![Habilitar a criptografia para a conta de armazenamento][1]
2. A folha **Habilitar criptografia de armazenamento** é aberta. Essa folha lista as contas de armazenamento do Azure em que a criptografia de armazenamento está desabilitada. Neste exemplo, vamos selecionar **storageacct1**.
   ![Habilitar criptografia de armazenamento][2]
3. A folha **Criptografia** de **storageacct1** é aberta. Selecione **Habilitado**.
   ![Folha Criptografia][3]
4. Clique em **Salvar**.

Agora, você habilitou a criptografia de armazenamento para **storageacct1**.


## <a name="see-also"></a>Consulte também
Este documento mostrou como implementar a recomendação da Central de Segurança do Azure "Habilitar criptografia para Conta de Armazenamento do Azure". Para saber mais sobre a Criptografia do Serviço de Armazenamento do Azure, confira:

* [Criptografia do Serviço de Armazenamento do Azure para dados em repouso](../storage/common/storage-service-encryption.md)

Para saber mais sobre a Central de Segurança, confira o seguinte:

* [Configurando políticas de segurança na Central de Segurança do Azure](tutorial-security-policy.md): saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.
* [Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md): saiba como monitorar a integridade dos recursos do Azure.
* [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md): encontre as perguntas frequentes sobre como usar o serviço.
* [Blog de Segurança do Azure](https://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
