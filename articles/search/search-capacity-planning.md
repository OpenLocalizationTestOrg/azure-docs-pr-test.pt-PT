---
title: aaaCapacity planeamento de Azure Search | Microsoft Docs
description: "Ajuste a partição e réplica recursos de computador na Azure Search, onde cada recurso tem um preço em unidades de pesquisa sujeito a faturação."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Níveis de recursos de escala de consulta e indexação cargas de trabalho na Azure Search
Depois de [escolha um escalão de preço](search-sku-tier.md) e [aprovisionar um serviço de pesquisa](search-create-service-portal.md), Olá passo seguinte consiste em toooptionally aumento Olá número as réplicas ou partições utilizadas pelo seu serviço. Cada camada oferece um número fixo de unidades de faturação. Este artigo explica como tooallocate tooachieve essas unidades uma configuração ideal equilibrar os requisitos para a execução da consulta, indexação e armazenamento.

Configuração do recurso está disponível quando configurar um serviço em Olá [escalão básico](http://aka.ms/azuresearchbasic) ou um dos Olá [camadas Standard](search-limits-quotas-capacity.md). Para serviços facturável estas camadas, a capacidade é adquirida em incrementos de *unidades de pesquisa* (SUs) onde cada partição e réplica contagem como um SU. 

Utilizar menos SUs resultados numa fatura proporcionalmente inferior. Faturação destina-se em vigor, desde que o serviço de Olá está configurado. Se temporariamente não estiver a utilizar um serviço, a única forma de Olá tooavoid faturação é por eliminar o serviço de Olá e, em seguida, voltar a criá-lo quando precisar dele.

> [!Note]
> Eliminar um serviço elimina tudo no mesmo. Não existe nenhuma das instalações dentro da Azure Search para cópias de segurança e restaurar dados de pesquisa persistentes. tooredeploy um índice existente num novo serviço, deve executar Olá programa utilizado toocreate e carregá-lo originalmente. 

## <a name="terminology-partitions-and-replicas"></a>Terminologia: as partições e réplicas
As partições e réplicas são recursos de principal de Olá que fazer uma cópia de um serviço de pesquisa.

| Recurso | Definição |
|----------|------------|
|*Partições* | Fornece armazenamento de índice e e/s para operações de leitura/escrita (por exemplo, quando reconstruir ou atualizar um índice).|
|*Réplicas* | As instâncias do serviço de pesquisa de Olá, utilizada principalmente tooload saldo operações de consulta. Cada réplica aloja sempre uma cópia de um índice. Se tiver 12 réplicas, terá de 12 cópias de cada índice carregado no serviço de Olá.|

> [!NOTE]
> Não é possível toodirectly manipular ou gerir os índices executam numa réplica. Uma cópia de cada índice cada réplica faz parte da arquitetura do serviço de Olá.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Como tooallocate partições e réplicas
Na Azure Search, um serviço inicialmente é atribuído um nível mínimo de recursos constituída por uma partição e uma réplica. Para as camadas de que o suportem, pode ajustar incrementalmente recursos informáticos aumento partições se precisar de mais armazenamento e e/s ou adicionar mais réplicas de volumes maiores de consulta ou um melhor desempenho. Um único serviço tem de ter toohandle de recursos suficientes todas as cargas de trabalho (indexação e consultas). Não é possível subdividir cargas de trabalho entre vários serviços.

Alocação Olá tooincrease ou alteração das réplicas e partições, recomendamos que utilize Olá portal do Azure. portal de Olá impõe limites permitidos combinações que permanecem abaixo os limites máximos:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/) e selecione o serviço de pesquisa de Olá.
2. No **definições**, abra Olá **escala** painel e utilize Olá tooincrease de controlos de deslize ou reduzir o número de Olá de partições e réplicas.

Se necessitar de uma abordagem de aprovisionamento baseado em script ou código, Olá [API de REST de gestão](https://msdn.microsoft.com/library/azure/dn832687.aspx) é um portal toohello alternativo.

Geralmente, pesquisa necessário as aplicações mais réplicas de partições, especialmente quando as operações de serviço Olá são totalmente direcionadas para cargas de trabalho de consulta. Olá secção no [elevada disponibilidade](#HA) explica o motivo.

> [!NOTE]
> Depois de um serviço é aprovisionado, não pode ser atualizado tooa SKU superior. Irá precisar toocreate um serviço de pesquisa na camada de nova Olá e recarregar os índices. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda com o aprovisionamento de serviço.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Elevada disponibilidade
Porque é fácil e rápido relativamente tooscale cópias de segurança, recomendamos, geralmente, que começa com uma partição e um ou criar duas réplicas e, em seguida, dimensionamento, segurança, como volumes de consulta. Para vários serviços em camadas de Basic ou S1 Olá, uma partição disponibiliza e e/s de armazenamento suficiente (milhões de 15 de documentos por partição).

Executam cargas de trabalho de consulta principalmente nas réplicas. Se precisar de mais débito ou elevada disponibilidade, provavelmente venha a necessitar réplicas adicionais.

Recomendações gerais para elevada disponibilidade são:

* Duas réplicas para elevada disponibilidade de só de leitura cargas de trabalho (consultas)
* Três ou mais réplicas para elevada disponibilidade de cargas de trabalho de leitura/escrita (consultas mais indexação como documentos individuais são adicionados, atualizados ou eliminados)

Contratos de nível de serviço (SLA) de pesquisa do Azure são direcionados para operações de consulta e em atualizações de índice que consiste em Adicionar, atualizar ou eliminar documentos.

### <a name="index-availability-during-a-rebuild"></a>Índice de disponibilidade durante uma reconstrução

Elevada disponibilidade para a Azure Search diz respeito tooqueries e índice de atualizações que não envolvem a reconstruir um índice. Se eliminar um campo, alterar um tipo de dados ou mudar o nome de um campo, terá de índice de Olá toorebuild. índice de Olá toorebuild, tem de eliminar Olá de índice, recrie o índice de Olá e recarregar os dados de Olá.

> [!NOTE]
> Pode adicionar o novo índice de pesquisa do Azure de campos tooan sem reconstrua o índice de Olá. valor de Olá do campo novo Olá será nulo para todos os documentos já se encontra num índice de Olá.

disponibilidade de índice de toomaintain durante uma reconstrução, tem de ter uma cópia do índice de Olá com um nome diferente no Olá mesmo serviço, ou uma cópia de Olá índice com Olá mesmo nome num serviço diferente e, em seguida, fornecer a lógica de redirecionamento ou de ativação pós-falha no seu código.

## <a name="disaster-recovery"></a>Recuperação após desastre
Atualmente, não há nenhum mecanismo incorporado para recuperação após desastre. Adicionar partições ou réplicas seria estratégia de errado Olá para cumprir os objetivos de recuperação após desastre. abordagem mais comuns Olá é tooadd redundância ao nível de serviço Olá ao configurar um serviço de pesquisa segundo noutra região. Tal como acontece com disponibilidade durante uma reconstrução do índice, redirecionamento de Olá lógica de ativação pós-falha tem uma combinação ou a partir do código.

## <a name="increase-query-performance-with-replicas"></a>Aumentar o desempenho de consulta com réplicas
A latência de consulta é um indicador de que as réplicas adicionais são necessárias. Geralmente, o primeiro passo para melhorar o desempenho da consulta é tooadd mais deste recurso. À medida que adiciona réplicas, cópias adicionais do índice de Olá são colocadas online toosupport maiores consulta as cargas de trabalho e Olá de saldo tooload pede ao longo de Olá várias réplicas.

Não é possível fornecemos estimativas de disco rígidas em consultas por segundo (QPS): consulta desempenho depende de complexidade de Olá de Olá consulta e cargas de trabalho concorrentes. Em média, uma réplica em básicas ou os SKUs de S1 pode servir QPS cerca de 15, mas o débito poderão ser superior ou inferior, consoante a complexidade de consulta (consultas por facetas são mais complexas) e a latência de rede. Além disso, é importante toorecognize embora adicionar réplicas adicionará sem dúvida dimensionamento e desempenho, Olá resultado não seja estritamente linear: adicionar três réplicas garante triplo débito.

toolearn sobre QPS, incluindo as abordagens para estimar QPS para cargas de trabalho, consulte [gerir o serviço de pesquisa](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Aumentar o desempenho de indexação com partições
Procurar aplicações que necessitam de perto a atualização de dados em tempo real serão necessário proporcionalmente mais partições que as réplicas. Adicionar partições propaga operações de leitura/escrita num grande número de recursos de computação. Também proporciona mais espaço em disco para armazenar adicionais índices e documentos.

Índices maiores demorar mais longo tooquery. Como tal, poderá achar que cada aumento incremental em partições requer um aumento de menor mas proporcional réplicas. complexidade Olá das suas consultas e o volume de consulta irá ter em conta no rapidez a execução de consultas está ativada em torno.

## <a name="basic-tier-partition-and-replica-combinations"></a>O escalão básico: combinações de partição e réplica
Um serviço básico pode ter exatamente uma partição e até as réplicas de toothree, para um limite máximo de três SUs. recursos apenas ajustável Olá é réplicas. É necessário um mínimo de duas réplicas para elevada disponibilidade em consultas.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Os escalões Standard: combinações de partição e réplica
Esta tabela mostra Olá SUs toosupport necessário combinações de réplicas e partições, limite de 36 SU toohello do requerente, para todos os escalões Standard.

|   | **1 partição** | **2 partições** | **3 partições** | **4 partições** | **6 partições** | **12 partições** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 réplica** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **2 réplicas** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **3 réplicas** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **4 réplicas** |4 SU |8 SU |12 SU |16 SU |24 SU |N/D |
| **5 réplicas** |5 SU |10 SU |15 DE SU |20 SU |30 SU |N/D |
| **6 réplicas** |6 SU |12 SU |18 SU |24 SU |36 SU |N/D |
| **12 réplicas** |12 SU |24 SU |36 SU |N/D |N/D |N/D |

SUs, o preço e a capacidade são explicados em detalhe no Olá Web site Azure. Para obter mais informações, consulte [detalhes dos preços](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> número de Olá das réplicas e de partições uniformemente divide em 12 (especificamente, 1, 2, 3, 4, 6, 12). Isto acontece porque a Azure Search divide previamente cada índice em 12 shards para que podem ser distribuído em partes iguais em todas as partições. Por exemplo, se o serviço tem três partições e criar um índice, cada partição irá conter quatro shards do índice de Olá. Como shards da Azure Search um índice é um detalhe de implementação, assunto toochange em versões futuras. Apesar do número de Olá 12 hoje em dia, não deve esperar que número tooalways constar 12 Olá futuras.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Fórmula de faturação para recursos de partição e réplica
fórmula Olá para calcular o SUs quantos são utilizados para combinações específicas é produto Olá das réplicas e partições, ou (P X de R = SU). Por exemplo, três réplicas multiplicadas pelo três partições é faturada como nove SUs.

Custo por SU é determinado pelo escalão de Olá, com uma velocidade de faturação por unidade inferior para básico que para Standard. Classifica para cada camada pode ser encontrada no [detalhes dos preços](https://azure.microsoft.com/pricing/details/search/).
