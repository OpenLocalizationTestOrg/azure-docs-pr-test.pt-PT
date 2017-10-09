---
title: aaaFrequently mais frequentes sobre (FAQ) sobre a Azure Search | Microsoft Docs
description: "Obtenha respostas toocommon perguntas sobre o serviço de pesquisa do Microsoft Azure"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Pesquisa do Azure - perguntas mais frequentes sobre (FAQ)
 
 Encontrar respostas toocommonly perguntas mais sobre os conceitos, código e cenários relacionados com tooAzure pesquisa.

## <a name="platform"></a>Plataforma

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Como é diferente da pesquisa em texto completo na minha DBMS da Azure Search?

A pesquisa do Azure suporta várias origens de dados, [análise linguístico para vários idiomas](https://docs.microsoft.com/rest/api/searchservice/language-support), [analysis personalizado invulgares e interessantes entradas de dados](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), controlos classificação através de pesquisa [da classificação perfis](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)e funcionalidades de experiência de utilizador como typeahead, realçando acessos e navegação por facetas. Também inclui outras funcionalidades, como sinónimos e a sintaxe de consulta avançada, mas os são geralmente não differentiating funcionalidades.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>O que é a diferença de Olá entre da Azure Search e Elasticsearch?

Quando a comparação com as tecnologias de pesquisa, os clientes com frequência peça especificações na forma como a pesquisa do Azure compara com Elasticsearch. Os clientes que escolher da Azure Search através de Elasticsearch para a sua pesquisa de projetos de aplicação, normalmente, tal porque fizemos uma tarefa chave mais fácil ou precisam de integração incorporada do Olá com outras tecnologias Microsoft:

+ A pesquisa do Azure é um serviço em nuvem completamente gerido com contratos de nível de serviço (SLA) 99,9% quando aprovisionado com redundância suficiente (2 réplicas para acesso de leitura, 3 réplicas para leitura e escrita).
+ Microsoft [processadores de linguagem Natural](https://docs.microsoft.com/rest/api/searchservice/language-support) oferecem leading edge inguistic análise.  
+ [Indexadores de pesquisa do Azure](search-indexer-overview.md) pode pesquisam uma variedade de origens de dados do Azure para indexação inicial e incrementais.
+ Se precisar de resposta rápida toofluctuations na consulta ou indexação volumes, pode utilizar [controlos de deslize](search-manage.md#scale-up-or-down) no Olá Azure portal ou executar um [script do PowerShell](search-manage-powershell.md), ignorando diretamente a gestão de partições horizontais.  
+ [Classificação e funcionalidades de otimização](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) fornecer Olá significa para que influencia as pontuações de classificação de pesquisa para além de fornece o motor de busca Olá individualmente. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Pode colocar em pausa o serviço da Azure Search e parar a faturação?

Não é possível colocar em pausa o serviço de Olá. Capacidade de cálculo e recursos de armazenamento são atribuídos para utilização exclusiva quando o serviço de Olá é criado. Não é possível toorelease e recuperar esses recursos a pedido. 

## <a name="indexing-operations"></a>Operações de indexação

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Cópia de segurança e restaurem (ou transfira e moverem) índices ou instantâneos de índice?

Embora possa [obter uma definição de índice](https://docs.microsoft.com/rest/api/searchservice/get-index) em qualquer altura, não há nenhum extração de índice, um instantâneo ou um funcionalidade de restauro da cópia de segurança para a transferência um *preenchido* índice em execução no Olá nuvem tooa sistema local, ou movê-los tooanother serviço de pesquisa do Azure. 

Índices são criados e preenchidos a partir do código que escrever e executar apenas na pesquisa do Azure na nuvem de Olá. Normalmente, o que os clientes pretendem toomove um serviço de tooanother índice fazê-lo ao editar as respetivas toouse código um novo ponto final e, em seguida, execute novamente a indexação. Se pretender Olá capacidade tootake um instantâneo ou um índice de cópia de segurança, converter um voto [voz do utilizador](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>Pode indexar de réplicas de base de dados do SQL Server (aplica-se demasiado[indexadores de base de dados do Azure SQL](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Não existem sem restrições na utilização de Olá das réplicas primários ou secundários como uma origem de dados ao criar um índice a partir do zero. No entanto, atualizar um índice com atualizações incrementais (com base nos registos alterados) requer a réplica primária Olá. Este requisito provém de base de dados SQL que garantias de alterações no apenas réplicas primárias. Se tentar utilizar réplicas secundárias para uma carga de trabalho de atualização do índice, não há nenhuma garantia, obter todos os dados de Olá.

## <a name="search-operations"></a>Operações de pesquisa

### <a name="can-i-search-across-multiple-indexes"></a>Pode procurar em vários índices?

Não, esta operação não é suportada. Pesquisa é sempre índice único tooa âmbito.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Pode restringir pesquisa corpus acesso pela identidade de utilizador?

A pesquisa do Azure não tem um modelo de segurança baseada em funções para acesso a dados por utilizador. A autenticação é qualquer um dos direitos totais ou só de leitura ao nível de serviço Olá. Alguns clientes implementar soluções com base no [ `$filter` parâmetro de pesquisa](https://docs.microsoft.com/rest/api/searchservice/search-documents), mas é uma solução, melhor. Se pretender que esta funcionalidade, converter um voto [voz do utilizador](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Por que motivo existem zero corresponde à medida que poderei sabê-lo toobe válido?

caso mais comuns Olá é não saber que cada tipo de consulta suporta níveis de estatísticas linguístico e comportamentos de pesquisa diferentes. Pesquisa em texto completo, que é a carga de trabalho predominant Olá, inclui uma fase de análise de idioma de quebras de termos de licenciamento para baixo tooroot formulários. Este aspeto do consulta análise casts uma rede mais ampla através de correspondências possíveis, porque hello atomizado termo corresponde a um maior número de variantes.

Se é a invocar [outros tipos de consulta](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (universal pesquisa, pesquisa difusa, pesquisa de proximidade, sugestões, entre outras), não há nenhuma análise linguístico. Os termos são adicionados a árvore de consulta toohello como-é. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Por que motivo é classificação de pesquisa de Olá uma classificação igual ou constante de 1.0 para todos os acessos?

Por predefinição, os resultados da pesquisa são classificados com base no Olá [propriedades análises de correspondência de termos](search-lucene-query-architecture.md#stage-4-scoring)e ordenadas toolow elevada Olá conjunto de resultados. No entanto, alguns tipos (universal, prefixo, regex) de consulta contribuir sempre uma pontuação constante toohello geral pontuação de documentos. Este comportamento é propositado. A pesquisa do Azure impõe uma constante de correspondências de tooallow encontradas através da consulta expansão toobe incluída nos resultados de Olá, sem afetar a classificação de Olá de pontuação. 

Por exemplo, suponha que uma entrada de "apresentação *" numa pesquisa com carateres universais produz correspondências em "tours", "tourettes" e "tourmaline". Tendo em conta natureza Olá estes resultados, não há nenhuma forma tooreasonably inferir os termos encontram-se mais importantes do que outros. Por este motivo, estamos a ignorar frequências termo quando a classificação de resultados em consultas de caráter universal de tipos, o prefixo e o regex. Os resultados da pesquisa com base numa entrada parcial recebem uma constante tooavoid bias para correspondências potencialmente inesperadas de pontuação.

## <a name="design-patterns"></a>Padrões de conceção

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>O que é a abordagem das melhores Olá para implementar a pesquisa localizada?

Maioria dos clientes escolha campos dedicados através de uma coleção, quando se trata toosupporting diferentes regiões (idiomas) no Olá mesmo índice. Campos específico de região tornam possível tooassign um analisador adequado. Por exemplo, atribuir o campo de tooa Olá Microsoft francês Analyzer que contém as cadeias francês. Também simplifica a filtragem. Se souber que uma consulta é iniciada numa página fr-fr, pode limitar o campo de toothis de resultados de pesquisa. Ou, crie um [perfil de classificação](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive Olá campo mais peso relativo.

## <a name="next-steps"></a>Passos seguintes

É a sua pergunta sobre uma funcionalidade ou funcionalidade em falta? Pedido de funcionalidade Olá no Olá [voz do utilizador web site](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Consultar também

 [StackOverflow: A pesquisa do Azure](https://stackoverflow.com/questions/tagged/azure-search)   
 [Como completa a pesquisa em texto funciona na Azure Search](search-lucene-query-architecture.md)  
 [O que é o Azure Search?](search-what-is-azure-search.md)

 