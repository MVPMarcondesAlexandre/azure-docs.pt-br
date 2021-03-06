---
title: Disponibilidade de serviços do Service Fabric | Microsoft Docs
description: Descreve a detecção de falhas, o failover e a recuperação dos serviços
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0794c0e190ecbc4cce808e94f98bb0ac63d1075a
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2018
ms.locfileid: "34206242"
---
# <a name="availability-of-service-fabric-services"></a>Disponibilidade dos serviços de malha do serviço
Este artigo apresenta uma visão geral de como o Azure Service Fabric mantém a disponibilidade de um serviço.

## <a name="availability-of-service-fabric-stateless-services"></a>Disponibilidade dos serviços de malha do serviço sem monitoração do estado
Os serviços do Service Fabric podem ser com ou sem monitoração de estado. Um serviço sem estado é um serviço de aplicativo que não tem um [estado local](service-fabric-concepts-state.md) que precise estar altamente disponível nem ser altamente confiável.

Criar um serviço sem estado requer a definição de uma `InstanceCount`. A contagem de instâncias define o número de instâncias da lógica de aplicativo do serviço sem estado que deve ser executado no cluster. Aumentar o número de instâncias é a maneira recomendada de escalar horizontalmente um serviço sem estado.

Quando uma instância de um serviço chamado sem monitoração de estado falha, uma nova instância é criada em um nó qualificado no cluster. Por exemplo, uma instância de serviço sem estado pode falhar no Node1 e ser recriada no Node5.

## <a name="availability-of-service-fabric-stateful-services"></a>Disponibilidade dos serviços de malha do serviço com monitoração do estado
Um serviço com estado tem um estado associado a ele. Na malha de serviço, um serviço com monitoração de estado é modelado como um conjunto de réplicas. Cada réplica é uma instância em execução do código do serviço. A réplica também tem uma cópia do estado para o serviço. As operações de leitura e gravação são realizadas em uma réplica chamada de *Primária*. As alterações ao estado das operações de gravação são *replicadas* para outras réplicas no conjunto de réplicas, chamadas de *Secundárias Ativas* e aplicadas. 

Pode haver apenas uma réplica Primária, mas pode haver várias réplicas Secundárias Ativas. O número de réplicas Secundárias ativas é configurável e um número maior de réplicas pode tolerar um número maior de falhas simultâneas de hardware e de software.

Se uma réplica Primária falhar, o Service Fabric torna uma das réplicas Secundárias Ativas a nova réplica Primária. Essa réplica Secundária Ativa já tem a versão atualizada do estado, via *replicação*, e pode continuar processando mais operações de leitura/gravação. Esse processo é conhecido como *reconfiguração* e é descrito mais detalhadamente no artigo [Reconfiguração](service-fabric-concepts-reconfiguration.md).

O conceito de uma réplica ser Primária ou Secundária Ativa é conhecido como *função de réplica*. Essas réplicas são descritas mais detalhadamente no artigo [Réplicas e instâncias](service-fabric-concepts-replica-lifecycle.md). 

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre os conceitos do Service Fabric, confira os seguintes artigos:

- [Dimensionando serviços do Service Fabric](service-fabric-concepts-scalability.md)
- [Particionando serviços da Malha do Serviço](service-fabric-concepts-partitioning.md)
- [Definindo e gerenciando o estado](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)

