---
title: Coletar dados sobre as Máquinas Virtuais do Azure | Microsoft Docs
description: Saiba como habilitar a Extensão de VM do agente do Log Analytics e como habilitar a coleta de dados das VMs do Azure com o Log Analytics.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: quickstart
ms.date: 11/13/2018
ms.author: magoedte
ms.custom: mvc
ms.openlocfilehash: 2c756e9e2944895cc493aa56d1dd20254e5d8ea0
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53188481"
---
# <a name="collect-data-about-azure-virtual-machines"></a>Coletar dados sobre as Máquinas Virtuais do Azure
O [Azure Log Analytics](../../azure-monitor/log-query/log-query-overview.md) pode coletar dados diretamente das máquinas virtuais do Azure e de outros recursos do ambiente em um único repositório para correlação e análise detalhada.  Este guia de início rápido mostra como configurar e coletar dados de VMs Linux ou Windows do Azure com algumas etapas simples.  
 
Este guia de início rápido pressupõe que você tenha uma máquina virtual do Azure existente. Se não puder [criar uma VM Windows](../../virtual-machines/windows/quick-create-portal.md) nem [criar uma VM Linux](../../virtual-machines/linux/quick-create-cli.md), siga nossos guias de início rápido de VM.

## <a name="log-in-to-azure-portal"></a>Fazer logon no portal do Azure
Faça logon no Portal do Azure em [https://portal.azure.com](https://portal.azure.com). 

## <a name="create-a-workspace"></a>Criar um workspace
1. No portal do Azure, clique em **Todos os serviços**. Na lista de recursos, digite **Log Analytics**. Quando você começa a digitar, a lista é filtrada com base em sua entrada. Selecione **Log Analytics**.

    ![Portal do Azure](media/quick-collect-azurevm/azure-portal-01.png)<br>  

2. Clique em **Criar** e, em seguida, selecione opções para os seguintes itens:

  * Forneça um nome para o novo **Workspace do Log Analytics**, como *DefaultLAWorkspace*. Os workspaces do OMS agora são chamados de workspaces do Log Analytics.  
  * Selecione uma **Assinatura** a vincular escolhendo uma na lista suspensa, se a selecionada por padrão não é adequada.
  * Para **Grupo de Recursos**, selecione um grupo de recursos existente que contém uma ou mais máquinas virtuais do Azure.  
  * Selecione o **Local** no qual as VMs serão implantadas.  Para obter mais informações, consulte em quais [regiões o Log Analytics está disponível](https://azure.microsoft.com/regions/services/).
  * Se você estiver criando um workspace em uma nova assinatura feita depois de 2 de abril de 2018, ele usará o plano de preços *por GB* e a opção de selecionar um tipo de preço não estará disponível.  Se você estiver criando um workspace para uma assinatura existente feita antes de 2 de abril ou uma assinatura associada a uma inscrição de EA existente, selecione seu tipo de preço preferido.  Para obter mais informações sobre os tipos específicos, consulte [Detalhes de preço do Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).
  
        ![Create Log Analytics resource blade](media/quick-collect-azurevm/create-loganalytics-workspace-02.png) 

3. Depois de fornecer as informações necessárias no painel **Workspace do Log Analytics**, clique em **OK**.  

Enquanto as informações são verificadas e o workspace é criado, você pode acompanhar seu progresso no menu **Notificações**. 

## <a name="enable-the-log-analytics-vm-extension"></a>Habilitar a Extensão de VM do Log Analytics

[!INCLUDE [log-analytics-agent-note](../../../includes/log-analytics-agent-note.md)] 

Para máquinas virtuais Windows e Linux já implantadas no Azure, instale o agente do Log Analytics com a Extensão de VM do Log Analytics. Usar a extensão simplifica o processo de instalação e configura automaticamente o agente para enviar dados para o workspace do Log Analytics que você especificar. O agente também será automaticamente atualizado, garantindo que você disponha dos recursos e correções mais recentes. Antes de prosseguir, verifique se a VM está em execução, caso contrário, a conclusão do processo com êxito falhará.  

>[!NOTE]
>O agente do Log Analytics para Linux não pode ser configurado para se reportar a mais de um workspace do Log Analytics. 

1. No Portal do Azure, clique em **Todos os serviços**, localizado no canto superior esquerdo. Na lista de recursos, digite **Log Analytics**. Quando você começa a digitar, a lista é filtrada com base em sua entrada. Selecione **Log Analytics**.
2. Na lista de workspaces do Log Analytics, selecione *DefaultLAWorkspace* criado anteriormente.
3. No menu à esquerda, em Fontes de Dados do Workspace, clique em **Máquinas virtuais**.  
4. Na lista de **Máquinas virtuais**, selecione uma máquina virtual em que deseja instalar o agente. Observe que o **status de conexão do Log Analytics** da VM indica que ele **Não está conectado**.
5. Nos detalhes de sua máquina virtual, selecione **Conectar**. O agente é automaticamente instalado e configurado para o seu workspace do Log Analytics. Esse processo leva alguns minutos, período durante o qual o **Status** é **Conectando**.
6. Depois de instalar e conectar o agente, o **status da conexão do Log Analytics** será atualizado com **Este workspace**.

## <a name="collect-event-and-performance-data"></a>Coletar dados de desempenho e eventos
O Log Analytics pode coletar eventos dos logs de eventos do Windows ou do Syslog do Linux e de contadores de desempenho especificados para relatórios e análise de prazo mais longo e tomar uma ação quando determinada condição for detectada.  Siga estas etapas para configurar a coleta de eventos do log do sistema do Windows e do Syslog do Linux e de vários contadores de desempenho comuns para começar.  

### <a name="data-collection-from-windows-vm"></a>Coleta de dados de VM Windows
1. Selecione **Configurações avançadas**.

    ![Configurações avançadas do Log Analytics](media/quick-collect-azurevm/log-analytics-advanced-settings-01.png)

3. Selecione **Dados** e, em seguida, **Logs de Eventos do Windows**.  
4. Adicione um novo log de eventos digitando o nome do log.  Digite **Sistema** e, em seguida, clique no sinal de adição **+**.  
5. Na tabela, verifique as severidades **Erro** e **Aviso**.   
6. Clique em **Salvar** na parte superior da página para salvar a configuração.
7. Selecione **Dados de Desempenho do Windows** para habilitar a coleta de contadores de desempenho em um computador Windows. 
8. Quando você configura os contadores de desempenho do Windows para um novo workspace do Log Analytics pela primeira vez, você tem a opção de criar rapidamente vários contadores comuns. Eles são listados com uma caixa de seleção ao lado de cada um.

    ![Contadores de desempenho padrão do Windows selecionados](media/quick-collect-azurevm/windows-perfcounters-default.png)

    Clique em **Adicionar os contadores de desempenho selecionados**.  Eles são adicionados e predefinidos com um intervalo de amostragem de coleta de dez segundos.
  
9. Clique em **Salvar** na parte superior da página para salvar a configuração.

### <a name="data-collection-from-linux-vm"></a>Coleta de dados de VM Linux

1. Selecione **Syslog**.  
2. Adicione um novo log de eventos digitando o nome do log.  Digite **Syslog** e, em seguida, clique no sinal de adição **+**.  
3. Na tabela, desmarque as severidades **Informações**, **Aviso** e **Depuração**. 
4. Clique em **Salvar** na parte superior da página para salvar a configuração.
5. Selecione **Dados de Desempenho do Linux** para habilitar a coleta de contadores de desempenho em um computador Linux. 
6. Quando você configura os contadores de desempenho do Linux para um novo workspace do Log Analytics pela primeira vez, você tem a opção de criar rapidamente vários contadores comuns. Eles são listados com uma caixa de seleção ao lado de cada um.

    ![Contadores de desempenho padrão do Windows selecionados](media/quick-collect-azurevm/linux-perfcounters-default.png)

    Clique em **Adicionar os contadores de desempenho selecionados**.  Eles são adicionados e predefinidos com um intervalo de amostragem de coleta de dez segundos.  

7. Clique em **Salvar** na parte superior da página para salvar a configuração.

## <a name="view-data-collected"></a>Exibir os dados coletados
Agora que você habilitou a coleta de dados, vamos executar um exemplo simples de pesquisa de logs para ver alguns dados das VMs de destino.  

1. No portal do Azure, navegue para Log Analytics e selecione o workspace criado anteriormente.
2. Clique no bloco **Pesquisa de Logs** e, no painel da Pesquisa de Logs, no campo de consulta, digite `Perf` e, em seguida, pressione Enter ou clique no botão de pesquisa à direita do campo de consulta.

    ![Exemplo de consulta da pesquisa de logs do Log Analytics](./media/quick-collect-azurevm/log-analytics-portal-perf-query.png) 

Por exemplo, a consulta na imagem a seguir retornou 735 registros de desempenho.  Os resultados serão significativamente menores. 

![Resultado da pesquisa de logs do Log Analytics](media/quick-collect-azurevm/log-analytics-search-perf.png)

## <a name="clean-up-resources"></a>Limpar recursos
Quando não for mais necessário, exclua o workspace do Log Analytics. Para fazer isso, selecione o workspace do Log Analytics criado anteriormente e, na página de recursos, clique em **Excluir**.


![Excluir um recurso do Log Analytics](media/quick-collect-azurevm/log-analytics-portal-delete-resource.png)

## <a name="next-steps"></a>Próximas etapas
Agora que você está coletando dados operacionais e de desempenho das máquinas virtuais Windows ou Linux, comece a explorar, analisar e tomar ações com facilidade em relação aos dados coletados *gratuitamente*.  

Para saber como exibir e analisar os dados, continue lendo o tutorial.   

> [!div class="nextstepaction"]
> [Exibir ou analisar dados no Log Analytics](../../azure-monitor/learn/tutorial-viewdata.md)
