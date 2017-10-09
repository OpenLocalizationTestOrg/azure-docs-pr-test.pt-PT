---
title: "aaaIntroduction toohello Azure Redis escalão Premium da Cache | Microsoft Docs"
description: "Saiba como toocreate e gerir a persistência de Redis, de clustering de Redis e suporte VNET para as instâncias de Cache de Redis do Azure do escalão Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Introdução toohello Azure Redis escalão Premium da Cache
Cache de Redis do Azure é uma cache distribuída, gerida que o ajuda a criar aplicações de elevada disponibilidade escaláveis e responsivas fornecendo dados tooyour de acesso rápido Super-obrigatórios. 

Olá que nova camada Premium é uma camada pronta empresarial, que inclui todas as funcionalidades do escalão Standard Olá e obter mais informações, tais como um melhor desempenho, as cargas de trabalho maiores, recuperação após desastre, importação/exportação e a segurança avançada. Continue toolearn ler mais sobre as funcionalidades adicionais do Olá da camada de cache Olá Premium.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Em comparação com um melhor desempenho tooStandard ou o escalão básico
**Melhor desempenho através do padrão ou básico camada.** Caches no escalão Premium de Olá são implementadas no hardware que tem processadores mais rápidos e fornece um melhor desempenho em comparação comparado toohello, Basic ou escalão Standard. Caches de escalão Premium têm um maior débito e latências inferiores. 

**Débito para Olá mesmo Cache tamanho está superior nas Premium em comparação com tooStandard camada.** Por exemplo, o débito de Olá de um 53 GB P4 cache (Premium) é 250 mil pedidos por segundo como em comparação com too150K para C6 (Standard).

Para obter mais informações sobre o tamanho, débito e largura de banda com premium caches, consulte [FAQ de Cache de Redis do Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>A persistência de dados de redis
camada de Premium Olá permite-lhe dados em cache toopersist Olá numa conta do Storage do Azure. Cache Basic/padrão são armazenados todos os dados de Olá apenas na memória. Em caso de infraestrutura subjacente existir problemas podem ser potencial perda de dados. Recomendamos que utilize a funcionalidade de persistência de dados de Redis Olá no resiliência do Olá Premium camada tooincrease contra a perda de dados. Cache de Redis do Azure oferece RDB e AOF (brevemente) opções no [persistência de Redis](http://redis.io/topics/persistence). 

Para obter instruções sobre como configurar a persistência, consulte [como tooconfigure persistência para uma Cache de Redis do Azure Premium](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Cluster de redis
Se pretender toocreate caches superiores a 53 GB ou quiser tooshard dados em vários nós de Redis, pode utilizar o clustering que está disponível na camada de Premium Olá de Redis. Cada nó é composta por um par de cache primário/réplica gerido pelo Azure para elevada disponibilidade. 

**Clustering de redis-dimensionamento máximo e débito.** Débito de forma linear aumenta como aumentar o número de Olá de partições horizontais (nós) no cluster de Olá. Ex. Se criar um cluster de P4 de 10 shards, em seguida, débito disponíveis Olá é 250 mil * 10 = 2,5 milhões de pedidos por segundo. Consulte Olá [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obter mais detalhes sobre o tamanho, débito e largura de banda com premium caches.

tooget começar a utilizar clustering, consulte [como tooconfigure clustering para uma Cache de Redis do Azure Premium](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Segurança e isolamento otimizados
Caches criados no escalão básicas ou Standard de Olá estão acessíveis no Olá internet pública. Cache é restrita com base na chave de acesso de Olá toohello de acesso. Com o escalão de Premium Olá que pode ainda Certifique-se de que apenas os clientes dentro de uma rede especificado podem aceder Olá Cache. Pode implementar a Cache de Redis num [rede Virtual do Azure (VNet)](https://azure.microsoft.com/services/virtual-network/). Pode utilizar todas as funcionalidades de Olá da VNet, tais como sub-redes, políticas de controlo de acesso e outra funcionalidades toofurther restringir acesso tooRedis.

Para obter mais informações, consulte [como suportam o tooconfigure rede Virtual para uma Cache de Redis do Azure Premium](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Importação/Exportação
Importar/exportar é uma operação de gestão de dados de Cache de Redis do Azure que permite-lhe tooimport dados para a Cache de Redis do Azure ou a exportação de dados da Cache de Redis do Azure por importar e exportar um instantâneo de base de dados de Cache de Redis (RDB) de um blob de página do premium cache tooa num Azure Conta de armazenamento. Isto permite-lhe toomigrate entre instâncias diferentes de Cache de Redis do Azure ou povoar a cache de Olá com dados antes de utilização.

Importação pode ser utilizado toobring Redis compatíveis RDB ficheiros de qualquer servidor Redis em execução em qualquer nuvem ou o ambiente, incluindo Redis em execução no Linux, Windows ou qualquer fornecedor de nuvem como Amazon Web Services e outras pessoas. Importação de dados é uma forma fácil de toocreate uma cache com dados pré-preenchidos. Durante o processo de importação de Olá, a Cache de Redis do Azure carrega os ficheiros RDB Olá storage do Azure para a memória e, em seguida, insere chaves Olá na cache de Olá.

Exportação permite-lhe dados de Olá tooexport armazenados na Cache de Redis do Azure tooRedis compatíveis RDB ficheiros. Pode utilizar estas funcionalidade toomove dados um tooanother de instância da Cache de Redis do Azure ou servidor de Redis tooanother. Durante o processo de exportação de Olá, é criado um ficheiro temporário no Olá VM que anfitriões Olá instância de servidor de Cache de Redis do Azure, não sendo ficheiro Olá toohello carregado designada de conta de armazenamento. Quando concluir a operação de exportação Olá com o estado de sucesso ou falha, o ficheiro temporário Olá é eliminado.

Para obter mais informações, consulte [como tooimport dados para e exportar dados a partir da Cache de Redis do Azure](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Reiniciar
camada de premium Olá permite-lhe tooreboot um ou mais nós da sua cache a pedido. Isto permite que tootest a aplicação para resiliência no evento Olá de uma falha. Pode reiniciar o computador Olá seguintes nós.

* Nó principal da cache
* Nó subordinado da cache
* Nós secundários e mestre da cache
* Ao utilizar uma cache premium com clustering, pode reiniciar o mestre de Olá, multisservidor ou ambos os nós para shards individuais na cache de Olá

Para obter mais informações, consulte [reiniciar](cache-administration.md#reboot) e [reiniciar FAQ](cache-administration.md#reboot-faq).

>[!NOTE]
>Reinicie a funcionalidade está agora ativada para todos os escalões de Cache de Redis do Azure.
>
>

## <a name="schedule-updates"></a>Atualizações agendadas
funcionalidade de atualizações agendadas Olá permite-lhe toodesignate uma janela de manutenção para a sua cache. Quando a janela de manutenção de Olá for especificada, quaisquer atualizações do servidor de Redis são efetuadas durante este período. toodesignate uma janela de manutenção, selecione os dias de Olá pretendida e especifique a hora do início de janela de manutenção do Olá para cada dia. Tenha em atenção que o tempo de janela de manutenção de Olá está em UTC. 

Para obter mais informações, consulte [agendar atualizações](cache-administration.md#schedule-updates) e [agendar atualizações FAQ](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Apenas as atualizações são efetuadas durante a janela de manutenção agendada hello do servidor de Redis. janela de manutenção de Olá não se aplica atualizações tooAzure ou atualizações do sistema de operativo toohello VM.
> 
> 

## <a name="geo-replication"></a>Georreplicação

**Replicação geográfica** fornece um mecanismo para ligar duas instâncias de Cache de Redis do Azure do escalão Premium. Uma cache está designado como Olá primário ligado e a cache de Olá como cache de ligado secundário Olá. cache de ligado secundário Olá torna-se só de leitura e os dados escritos toohello de cache primárias replicados toohello secundária, cache ligado. Esta funcionalidade pode ser utilizado tooreplicate uma cache em regiões do Azure.

Para obter mais informações, consulte [como tooconfigure georreplicação para a Cache de Redis do Azure](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>escalão do tooscale toohello premium
escalão do tooscale toohello premium, basta escolher um dos escalões de premium Olá Olá **alteração de escalão de preço** painel. Também pode dimensionar o escalão premium do toohello de cache com o PowerShell e a CLI. Para obter instruções passo a passo, consulte [como tooScale do Azure da Cache de Redis](cache-how-to-scale.md) e [como tooautomate uma operação de dimensionamento](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Passos seguintes
Criar uma cache e explorar as funcionalidades do escalão premium novo Olá.

* [Como tooconfigure persistência para uma Cache de Redis do Azure Premium](cache-how-to-premium-persistence.md)
* [Como suportam o tooconfigure rede Virtual para uma Cache de Redis do Azure Premium](cache-how-to-premium-vnet.md)
* [Como tooconfigure clustering para uma Cache de Redis do Azure Premium](cache-how-to-premium-clustering.md)
* [Como tooimport dados para e exportar dados a partir da Cache de Redis do Azure](cache-how-to-import-export-data.md)
* [Como tooadminister do Azure da Cache de Redis](cache-administration.md)

