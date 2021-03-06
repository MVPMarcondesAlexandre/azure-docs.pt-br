---
title: Pontos de extremidade de streaming nos Serviços de Mídia do Azure | Microsoft Docs
description: Este artigo fornece uma explicação sobre o que são os pontos de extremidade de streaming e como são usados pelos Serviços de Mídia do Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 01/16/2019
ms.author: juliako
ms.openlocfilehash: 18c5e48b5f7dbf664b607b8b83473a914256590b
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2019
ms.locfileid: "55104535"
---
# <a name="streaming-endpoints"></a>Ponto de extremidade de streaming

No AMS (Serviços de Mídia do Microsoft Azure), a entidade [Ponto de Extremidade de Streaming](https://docs.microsoft.com/rest/api/media/streamingendpoints) representa um serviço de streaming que pode fornecer conteúdo diretamente a um aplicativo de player cliente ou a uma CDN (Rede de Distribuição de Conteúdo) para distribuição adicional. O fluxo de saída de um serviço de **Ponto de Extremidade de Streaming** pode ser uma transmissão ao vivo ou um Ativo de vídeo sob demanda em sua conta dos Serviços de Mídia. Quando você cria uma conta de Serviços de Mídia, um Ponto de Extremidade de Streaming **padrão** é criado em um estado parado. Não é possível excluir o Ponto de Extremidade de Streaming **padrão**. Ponto de Extremidade de Streaming adicionais podem ser criados na conta. 

> [!NOTE]
> Para começar a transmitir vídeos, é necessário iniciar o **Ponto de extremidade de streaming** do qual deseja transmitir o vídeo. 

## <a name="naming-convention"></a>Convenção de nomenclatura

Para o ponto de extremidade padrão: `{AccountName}-{DatacenterAbbreviation}.streaming.media.azure.net`

Para pontos de extremidade adicionais: `{EndpointName}-{AccountName}-{DatacenterAbbreviation}.streaming.media.azure.net`

## <a name="types"></a>Tipos  

Há dois tipos de **Ponto de Extremidade de Streaming**: **Standard** e **Premium**. O tipo é definido pelo número de unidades de escala (`scaleUnits`) alocadas para o ponto de extremidade de streaming. 

A tabela descreve os tipos:  

|Type|Unidades de escala|DESCRIÇÃO|
|--------|--------|--------|  
|**Ponto de Extremidade de Streaming Standard** (recomendado)|0|O tipo **Standard** é a opção recomendada para praticamente todos os cenários de streaming e tamanhos de público-alvo. O tipo **Standard** dimensiona automaticamente a largura de banda de saída. <br/>Para clientes com requisitos extremamente exigentes, os Serviços de Mídia oferecem pontos de extremidade de streaming **Premium**, que podem ser usados para dimensionar a capacidade dos maiores públicos-alvos da Internet. Se você espera grandes públicos-alvos e visualizadores simultâneos, contate-nos pelo telefone amsstreaming@microsoft.com para saber se será necessário mudar para o tipo **Premium**. |
|**Ponto de Extremidade de Streaming Premium**|>0|Os pontos de extremidade do streaming **Premium** são adequados para as cargas de trabalho avançadas, fornecendo uma capacidade de largura de banda dimensionável e dedicada. É possível mudar para um tipo **Premium**, ajustando `scaleUnits`. `scaleUnits` fornece capacidade de saída dedicada que pode ser comprada em incrementos de 200 Mbps. Ao usar o tipo **Premium**, cada unidade habilitada fornece capacidade adicional de largura de banda ao aplicativo. |

## <a name="working-with-cdn"></a>Trabalhando com CDN

Na maioria dos casos, é necessário ter a CDN habilitada. No entanto, se você estiver antecipando uma simultaneidade máxima menor que 500 visualizadores, então, é recomendável desabilitar a CDN, já que a CDN dimensiona melhor com simultaneidade.

> [!NOTE]
> O ponto de extremidade de streaming `hostname` e a URL de streaming permanecem os mesmos, independentemente de você habilitar a CDN ou não.

### <a name="detailed-explanation-of-how-caching-works"></a>Explicação detalhada de como o armazenamento em cache funciona

Não há nenhum valor de largura de banda específico ao adicionar a CDN porque a quantidade de largura de banda necessária para um ponto de extremidade de streaming habilitado para CDN varia. Depende muito do tipo de conteúdo, da popularidade, das taxas de bits e dos protocolos. A CDN está apenas armazenando em cache o que está sendo solicitado. Isso significa que o conteúdo popular será atendido diretamente pela CDN – contanto que o fragmento de vídeo seja armazenado em cache. É provável que o conteúdo ao vivo seja armazenado em cache, porque normalmente há muitas pessoas assistindo exatamente o mesmo conteúdo. O conteúdo sob demanda pode ser um pouco mais complicado porque você pode ter algum conteúdo que seja popular e outro que não seja. Se você tem milhões de ativos de vídeo em que nenhum deles é popular (apenas 1 ou 2 visualizadores por semana), mas tem milhares de pessoas assistindo a todos os diferentes vídeos, a CDN torna-se muito menos eficaz. Com essa perda no cache, você aumenta a carga no ponto de extremidade de streaming.
 
Também é necessário considerar como o streaming adaptável funciona. Cada fragmento de vídeo individual é armazenado em cache como sua própria entidade. Por exemplo, se a primeira vez que um determinado vídeo é assistido e a pessoa ignora assistindo apenas alguns segundos de trechos aleatórios, apenas os fragmentos de vídeo associados ao que a pessoa assistiu são armazenados em cache no CDN. Com o streaming adaptável, você normalmente tem de 5 a 7 taxas de bits diferentes de vídeo. Se uma pessoa estiver assistindo a uma taxa de bits e outra pessoa estiver assistindo a uma taxa de bits diferente, cada uma delas será armazenada separadamente na CDN. Mesmo que duas pessoas estejam assistindo a mesma taxa de bits, é possível que estejam transmitindo por stream em diferentes protocolos. Cada protocolo (HLS, MPEG-DASH, Smooth Streaming) é armazenado em cache separadamente. Portanto, cada taxa de bits e protocolo são armazenados em cache separadamente e apenas os fragmentos de vídeo que foram solicitados são armazenados em cache.
 
## <a name="properties"></a>propriedades 

Esta seção fornece detalhes sobre algumas das propriedades do StreamingEndpoint. Para exemplos de como criar um novo ponto de extremidade de streaming e descrições de todas as propriedades, consulte [Ponto de Extremidade de Streaming](https://docs.microsoft.com/rest/api/media/streamingendpoints/create). 

|Propriedade|DESCRIÇÃO|  
|--------------|----------|
|`accessControl`|Usado para definir as seguintes configurações de segurança para esse ponto de extremidade de streaming: Chaves de autenticação de cabeçalho de assinatura do Akamai e endereços IP que têm permissão para se conectar a esse ponto de extremidade.<br />Esta propriedade poderá ser definida quando `cdnEnabled`"` estiver definido como false.|  
|`cdnEnabled`|Indica se a integração de CDN do Azure para este ponto de extremidade de streaming está habilitada ou não (desabilitada por padrão.)<br /><br /> Se você definir `cdnEnabled` como verdadeiro, as seguintes configurações serão desabilitadas: `customHostNames` e `accessControl`.<br /><br />Nem todos os data centers dão suporte para integração da CDN do Azure. Para verificar se o data center tem ou não a integração da CDN do Azure disponível, execute o seguinte:<br /><br /> - Experimente definir `cdnEnabled` como verdadeiro.<br /><br /> - Verifique o resultado retornado de `HTTP Error Code 412` (PreconditionFailed) com uma mensagem de "A propriedade CdnEnabled do ponto de extremidade de streaming não pode ser configurada como verdadeira, pois o recurso de CDN não está disponível na região atual."<br /><br /> Se você receber esse erro, o data center não dará suporte. Você deve experimentar outro data center.|  
|`cdnProfile`|Quando `cdnEnabled` é definido como verdadeiro, você também pode passar valores `cdnProfile`. `cdnProfile` é o nome do perfil CDN no qual o ponto de extremidade CDN será criado. Você pode fornecer um cdnProfile existente ou usar um novo. Se o valor for NULL e `cdnEnabled` for verdadeiro, o valor padrão "AzureMediaStreamingPlatformCdnProfile" será usado. Se o perfil `cdnProfile` fornecido já existir, um ponto de extremidade será criado sob ele. Se o perfil não existir, um novo perfil será criado automaticamente.|
|`cdnProvider`|Quando a CDN for habilitada, você também poderá passar valores `cdnProvider`. `cdnProvider` controla qual provedor será usado. Atualmente, três valores são suportados: "StandardVerizon", "PremiumVerizon" e "StandardAkamai". Se nenhum valor for fornecido e `cdnEnabled` for verdadeiro, será usado StandardVerizon" (esse é o valor padrão.)|
|`crossSiteAccessPolicies`|Usado para especificar políticas de acesso entre sites para vários clientes. Para obter mais informações, consulte [Especificação de arquivo de política entre domínios](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html) e [Disponibilizando um serviço entre limites de domínios](https://msdn.microsoft.com/library/cc197955\(v=vs.95\).aspx).|  
|`customHostNames`|Usado para configurar um ponto de extremidade de streaming para aceitar tráfego direcionado para um nome do host personalizado. Isso permite uma configuração de gerenciamento de tráfego mais fácil por meio de um GTM (Gerenciador de Tráfego Global) e também para nomes de domínio de marca a serem usados como o nome do ponto de extremidade de streaming.<br /><br /> A propriedade do nome de domínio deve ser confirmada pelos Serviços de Mídia do Azure. Os Serviços de Mídia do Azure verificam a propriedade do nome de domínio, exigindo que um registro `CName` contendo a ID da conta de Serviços de Mídia do Azure como um componente seja adicionado ao domínio em uso. Por exemplo, para "sports.contoso.com" ser usado como um nome do host personalizado para o ponto de extremidade de streaming, um registro para `<accountId>.contoso.com` deve ser configurado para apontar para um dos nomes do host de verificação dos Serviços de Mídia. O nome do host de verificação é composto por verifydns.\<mediaservices-dns-zone>. A tabela a seguir contém as zonas DNS esperadas a serem usadas no registro de verificação para diferentes regiões do Azure.<br /><br /> América do Norte, Europa, Singapura, Hong Kong, Japão:<br /><br /> - mediaservices.windows.net<br /><br /> - verifydns.mediaservices.windows.net<br /><br /> China:<br /><br /> - mediaservices.chinacloudapi.cn<br /><br /> - verifydns.mediaservices.chinacloudapi.cn<br /><br /> Por exemplo, um registro `CName` que mapeia "945a4c4e-28ea-45cd-8ccb-a519f6b700ad.contoso.com" para "verifydns.mediaservices.windows.net" prova que a ID dos Serviços de Mídia do Azure 945a4c4e-28ea-45cd-8ccb-a519f6b700ad tem a propriedade do domínio contoso.com, permitindo que qualquer nome sob contoso.com seja usado como um nome do host personalizado para um ponto de extremidade de streaming sob essa conta.<br /><br /> Para localizar o valor da ID do Serviço de Mídia, acesse o [portal do Azure](https://portal.azure.com/) e selecione a conta de Serviço de Mídia. A ID do SERVIÇO DE MÍDIA aparece à direita da página de PAINEL.<br /><br /> **Aviso**: Se houver uma tentativa de definir um nome do host personalizado sem uma verificação adequada do registro `CName`, a resposta DNS falhará e, em seguida, será armazenada em cache por algum tempo. Depois que um registro adequado estiver em vigor, poderá demorar um pouco até que a resposta armazenada em cache seja revalidada. Dependendo do provedor DNS do domínio personalizado, pode levar de alguns minutos a uma hora para revalidar o registro.<br /><br /> Além de `CName` que mapeia `<accountId>.<parent domain>` para `verifydns.<mediaservices-dns-zone>`, você deve criar outro `CName` que mapeie o nome do host personalizado (por exemplo, `sports.contoso.com`) para o nome do host do StreamingEndpont dos Serviços de Mídia (por exemplo, `amstest.streaming.mediaservices.windows.net`).<br /><br /> **Observação**: Pontos de extremidade de streaming localizados no mesmo data center, não podem compartilhar o mesmo nome do host personalizado.<br /> Essa propriedade é válida para pontos de extremidade de streaming Standard e Premium e poderá ser definida quando "cdnEnabled": false<br/><br/> Atualmente, o AMS não dá suporte ao SSL com domínios personalizados.  |  
|`maxCacheAge`|Substitui o cabeçalho de controle de cache HTTP max-age padrão definido pelo ponto de extremidade de streaming em fragmentos de mídia e manifestos sob demanda. O valor é definido em segundos.|
|`resourceState`|Valores para a propriedade incluem:<br /><br /> - Parado. O estado inicial de um ponto de extremidade de streaming após a criação.<br /><br /> - Iniciando. O ponto de extremidade de streaming está em transição para o estado de execução.<br /><br /> - Executando. O ponto de extremidade de streaming é capaz de transmitir conteúdo para os clientes.<br /><br /> - Dimensionando. As unidades de escala estão sendo aumentadas ou diminuídas.<br /><br /> - Parando. O ponto de extremidade de streaming está fazendo transição para o estado parado.<br/><br/> - Excluindo. O ponto de extremidade de streaming está sendo excluído.|
|`scaleUnits `|scaleUnits fornecem capacidade de saída dedicada que pode ser comprada em incrementos de 200 Mbps. Se você precisar mudar para um tipo **Premium**, ajuste `scaleUnits`. |

## <a name="next-steps"></a>Próximas etapas

O exemplo [neste repositório](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs) mostra como iniciar o ponto de extremidade de streaming padrão com .NET.

