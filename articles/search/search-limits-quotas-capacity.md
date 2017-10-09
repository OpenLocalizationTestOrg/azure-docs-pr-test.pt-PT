---
title: os limites de aaaService na Azure Search | Microsoft Docs
description: "Limites de serviço utilizados para o planeamento de capacidade e os limites máximos nos pedidos e respostas de pesquisa do Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Limites de serviço da Azure Search
Máximo limita-se no armazenamento, as cargas de trabalho e quantidades de índices, documentos, e outros objetos dependem se [aprovisionar da Azure Search](search-create-service-portal.md) num **livres**, **básico**, ou **padrão** escalão de preço.

* **Livre** é um serviço partilhado do multi-inquilino que vem com a sua subscrição do Azure. É uma opção de não custos adicionais para subscritores existentes que permite-lhe tooexperiment com o serviço de Olá antes de inscrever-se recursos dedicados.
* **Básico** fornece recursos de informática dedicados para cargas de trabalho de produção em escala mais pequena.
* **Standard** é executado em máquinas dedicadas, com mais capacidade de armazenamento e processamento em cada nível. Standard, é apresentada no quatro níveis: S1, S2, S3 e S3 alta densidade (S3 HD).

> [!NOTE]
> Um serviço é aprovisionado em nenhum escalão específico. Se precisar de toojump camadas tooget mais capacidade, terá de aprovisionar um novo serviço (não há nenhuma atualização no local). Para obter mais informações, consulte [escolha um SKU ou camada](search-sku-tier.md). toolearn mais sobre o ajuste da capacidade dentro de um serviço já tenha sido já aprovisionada, consulte [Dimensionar níveis de recursos de consulta e cargas de trabalho de indexação](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Por limites de subscrição
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Por limites de serviço
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Por limites de índice
Há uma correspondência de e-mail de um para um entre limites em índices e limites de indexadores. Tendo em conta um limite de 200 índices, Olá limite máximo de indexadores é também 200 para Olá mesmo serviço.

| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| O índice: campos máximos por índice |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Índice: máximo perfis por índice de classificação |100 |100 |100 |100 |100 |100 |
| O índice: funções máximas por perfil |8 |8 |8 |8 |8 |8 |
| Indexadores: máxima carga indexação por invocação |10 000 documentos |Limitado apenas por documentos máximos |Limitado apenas por documentos máximos |Limitado apenas por documentos máximos |Limitado apenas por documentos máximos |N/D <sup>2</sup> |
| Indexadores: tempo de execução máximo | 1 a 3 minutos <sup>3</sup> |24 horas |24 horas |24 horas |24 horas |N/D <sup>2</sup> |
| Indexador de blob: o tamanho máximo de blob, MB |16 |16 |128 |256 |256 |N/D <sup>2</sup> |
| Indexador de blob: número máximo de conteúdo extraídos de um blob caracteres |32,000 |64,000 |milhões de 4 |milhões de 4 |milhões de 4 |N/D <sup>2</sup> |

<sup>1</sup> escalão básico é Olá apenas SKU com um limite inferior de 100 campos por índice.

<sup>2</sup> S3 HD atualmente não suporta indexadores. Contacte o suporte do Azure se tiver uma necessidade urgente para esta capacidade.

<sup>3</sup> indexador tempo de execução máximo para o escalão gratuito Olá é 3 minutos para as origens de blob e 1 minuto para todas as outras origens de dados.

## <a name="document-size-limits"></a>Limites de tamanho do documento
| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Tamanho de documentos individuais por API de índice |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |

Quando chamar uma API de índice, refere-se toohello o tamanho máximo do documento. O tamanho do documento é, na verdade, de um limite no tamanho Olá de Olá corpo do pedido de API do índice. Uma vez que pode passar um lote de vários documentos toohello API de índice de uma só vez, o limite de tamanho de Olá depende, na verdade, são o número de documentos no lote de Olá. Para um lote com um único documento, o tamanho máximo do documento de Olá é 16 MB de JSON.

tamanho do documento tookeep descendente, lembre-se os dados não consultável tooexclude pedido Olá. Imagens e outros dados binários não são diretamente consultável e não devem ser armazenados no índice Olá. dados de não consultável toointegrate para os resultados da pesquisa, defina um campo não pesquisáveis que armazena um recurso de toohello de referência de URL.

## <a name="workload-limits-queries-per-second"></a>Limites de carga de trabalho (consultas por segundo)
| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |N/D |~3 por réplica |~15 por réplica |~60 por réplica |>60 por réplica |>60 por réplica |

As consultas por segundo (QPS) é uma aproximação do seu com base no heurística, utilizando os valores de tooderive estimada de cargas de trabalho do cliente simulada e real. Débito exato de QPS varia dependendo da natureza Olá e dados da consulta de Olá.

Embora estimativas aproximadas são fornecidas acima, uma taxa real é difícil toodetermine, especialmente em Olá que livres partilhado serviço onde débito baseia-se na largura de banda disponível e disputa pelos recursos do sistema. No escalão gratuito Olá, recursos de armazenamento e computação são partilhados por vários subscritores, pelo que QPS para a sua solução sempre irá variar, dependendo de como muitas outras cargas de trabalho são executadas em Olá mesmo tempo.

Nível Olá padrão, pode fazer a estimativa QPS mais detalhadamente porque tem controlo sobre mais dos parâmetros de Olá. Consulte a secção de melhores práticas Olá no [gerir a sua solução de pesquisa](search-manage.md) para obter orientações sobre como toocalculate QPS para as cargas de trabalho.

## <a name="api-request-limits"></a>Limites de pedido de API
* Máximo de 16 MB por pedido <sup>1</sup>
* Comprimento máximo do URL de 8 KB
* Documentos máximo de 1000 por lote de índice carrega, intercala ou elimina
* Campos máximos de 32 na cláusula $orderby
* Tamanho do termo de pesquisa máximo é 32,766 bytes (32 KB menos de 2 bytes) de texto codificado UTF-8

<sup>1</sup> na Azure Search, o corpo de Olá de um pedido é o limite superior de tooan assunto de 16 MB, impor um limite prático nos conteúdos Olá de campos individuais ou de coleções que caso contrário, não estão restritos pelo teórico limites (consulte [suportados tipos de dados](https://msdn.microsoft.com/library/azure/dn798938.aspx) para obter mais informações sobre restrições de composição de campo e).

## <a name="api-response-limits"></a>Limites de resposta de API
* Máximos 1000 documentos devolvidos por página de resultados de pesquisa
* Sugestões de 100 máximos devolvidos por pedido de API Sugerir

## <a name="api-key-limits"></a>Limites de chave de API
Chaves de API são utilizadas para autenticação do serviço. Existem dois tipos. Chaves de administração são especificadas no cabeçalho de pedido de Olá e conceder o serviço de acesso de leitura e escrita completa a toohello. As chaves de consulta são só de leitura, especificado no URL Olá e aplicações tooclient normalmente distribuída.

* Máximo de 2 chaves de administração por serviço
* Máximo de 50 chaves de consulta por serviço
