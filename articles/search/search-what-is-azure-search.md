---
title: "aaaWhat é da Azure Search | Microsoft Docs"
description: "A pesquisa do Azure é um serviço de pesquisa de nuvem alojado completamente gerido. Saiba mais nesta descrição geral da funcionalidade."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>O que é o Azure Search?
A pesquisa do Azure é uma solução de nuvem de pesquisa-como-um-serviço que fornece aos programadores APIs e ferramentas para adicionar uma experiência de pesquisa avançadas sobre os dados em aplicações web, móveis e enterprise.

A funcionalidade está exposta através de uma simples [REST API](/rest/api/searchservice/) ou [.NET SDK](search-howto-dotnet-sdk.md) que dissimula a complexidade inerente de Olá da tecnologia de pesquisa. Adição tooAPIs, Olá portal do Azure fornece e suporte de fazer o protótipo da administração. Infraestrutura e disponibilidade são geridos pela Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Resumo da funcionalidade

| Categoria | Funcionalidades |
|----------|----------|
|Pesquisa em texto completo e análise de texto | [**Pesquisa em texto completo** ](search-lucene-query-architecture.md) é o caso de utilização de um site primário para a maioria das aplicações baseada na procura. As consultas podem formulated utilizando uma sintaxe suportada: <br/><br/>[**Sintaxe de consulta simples**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), que oferece operadores lógicos, operadores de pesquisa de expressão, operadores de sufixo, operadores de precedência.<br/><br/>[**Sintaxe de consulta Lucene** ](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) oferece termo de consulta simples suporte plus pesquisa difusa, pesquisa de proximidade, todas as expressões de aumento e regulares.| 
| Integração de dados | Os índices de pesquisa do Azure aceitam dados a partir de qualquer origem fornecida é submetida como uma estrutura de dados JSON. <br/><br/> Opcionalmente, para origens de dados suportadas no Azure, pode utilizar [ **indexadores** ](search-indexer-overview.md) tooautomatically pesquisa [SQL Database do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [Azure Cosmos DB](search-howto-index-documentdb.md), ou [Blob storage do Azure](search-howto-indexing-azure-blob-storage.md) toosync o índice de pesquisa do conteúdo com o arquivo de dados principal. Indexadores de Blob do Azure podem efetuar *cracking documento* para [indexação formatos de ficheiro principais](search-howto-indexing-azure-blob-storage.md), incluindo o Microsoft Office, HTML e PDF, documentos. |
| Análise de pesquisa | [**Analisadores de lexical personalizados** ](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) estão disponíveis para consultas de pesquisa complexas utilizando a correspondência de fonético e expressões regulares. |
| Suporte de idiomas | [**Analisadores de idioma** ](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene, bem como Microsoft da linguagem natural processadores disponíveis no linguistics de específicas do idioma de identificador de toointelligently 56 idiomas diferentes, incluindo tenses verbo, sexo, dados plural os substantivos (por exemplo, ' rato' versus 'ratos'), word anular compounding, quebra de palavra (para idiomas sem espaços) e muito mais. |
| Georreplicação pesquisa | A pesquisa do Azure inteligentemente processa filtros e apresenta a localizações geográficas. Permite que os utilizadores tooexplore dados com base na proximidade Olá de uma localização física do resultado tooa de pesquisa. [Veja este vídeo](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) ou [rever este exemplo](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn mais. |
| Funcionalidades de experiência de utilizador | [**Sugestões de pesquisa** ](https://docs.microsoft.com/rest/api/searchservice/suggesters) pode ser ativada para consultas antecipada uma barra de pesquisa. Documentos reais no seu índice são sugeridos como os utilizadores introduzem uma pesquisa parcial de entrada. <br/><br/>[**Navegação por facetas** ](https://docs.microsoft.com/azure/search/search-faceted-navigation) é ativado através de um parâmetro de consulta simples. A pesquisa do Azure devolve uma estrutura de navegação por facetas que pode utilizar como código de Olá atrás de uma lista de categorias para filtragem de auto-direcionada (por exemplo, toofilter itens do catálogo por intervalo de preços ou marca). <br/><br/> [**Filtros** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) podem ser utilizados tooincorporate navegação por facetas na IU da aplicação, melhorar formulação de consulta e filtro com base nos critérios especificado de um utilizador ou de programador. Crie filtros utilizando a sintaxe de OData Olá.<br/><br/> [**Detetor de ocorrências** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) aplica-se de forma visual atting tooa correspondentes à palavra-chave nos resultados da pesquisa. Pode escolher os campos devolvem fragmentos realçados.<br/><br/>[**A ordenação** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) é disponibilizado para vários campos através do esquema de índice de Olá e, em seguida, tivada/desativada durante a consulta com um parâmetro de procura única.<br/><br/> [**Paginação** ](search-pagination-page-layout.md) e limitação os resultados da pesquisa é simples com controlo de Olá lhe otimizado da Azure Search oferece sobre os resultados da pesquisa.  
| Relevância | [**Classificação simples** ](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) é uma vantagem de chave de pesquisa do Azure. Perfis de classificação são relevância toomodel utilizado como uma função de valores da Olá documentos próprios. Por exemplo, poderá querer produtos mais recentes ou subvalorizado produtos tooappear superior nos resultados de pesquisa de Olá. Também pode criar perfis de classificação, utilizando etiquetas para classificação personalizada, com base nas preferências de pesquisa de cliente tiver controlada e armazenados em separado. |
| Monitorização e relatórios | [**Análise de tráfego de pesquisa** ](search-traffic-analytics.md) são toounlock recolhido e analisado conhecimentos aprofundados sobre o que os utilizadores são escrevendo na caixa de pesquisa de Olá. <br/><br/>As métricas sobre consultas por segundo, latência e limitação são capturadas e reportadas nas páginas do portal, sem qualquer configuração adicional necessária. Também pode facilmente o índice de monitor e contagem de documentos para que pode ajustar capacidade conforme necessário. Para obter mais informações, consulte [administração do serviço](search-manage.md) |
| Ferramentas para fazer o protótipo e inspeção | No portal de Olá, pode utilizar Olá [ **Assistente para importar dados** ](search-import-data-portal.md) tooconfigure indexadores, índice toostand estruturador se um índice e [ **Explorador de pesquisa** ](search-explorer.md) tootest consultas e refine os perfis de classificação. Pode também abrir qualquer tooview índice respetivo esquema. |
| Infraestrutura | Olá **plataforma elevada** garante uma experiência de serviço de pesquisa extremamente fiável. Quando ampliada corretamente, [da Azure Search oferece um SLA de 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **Completamente geridos e dimensionáveis** como uma solução ponto-a-ponto, a Azure Search não necessita absolutamente nenhuma gestão de infraestrutura. O serviço pode ser tooyour personalizáveis necessidades através da receção num duas dimensões toohandle mais armazenamento de documentos, superior cargas de consulta ou ambos.

## <a name="how-it-works"></a>Como funciona
### <a name="step-1-provision-service"></a>Passo 1: Serviço de aprovisionamento
Pode rotação um serviço da Azure Search no Olá [portal do Azure](https://portal.azure.com/) ou através de Olá [API de gestão de recursos do Azure](/rest/api/searchmanagement/). Pode escolher qualquer serviço gratuito de Olá partilhado com outros subscritores, ou um [paga camada](https://azure.microsoft.com/pricing/details/search/) que dedicates recursos utilizados apenas pelo seu serviço. Para os escalões pagos, pode dimensionar um serviço em duas dimensões: 

- Adicione toogrow réplicas que carrega a consulta de pesada toohandle capacidade.   
- Adicione armazenamento toogrow de partições para obter mais documentos. 

Ao processar o débito de armazenamento e a consulta do documento em separado, pode calibrar os resourcing com base nos requisitos de produção.

### <a name="step-2-create-index"></a>Passo 2: Criar o índice
Antes de pode carregar conteúdo pesquisável, primeiro tem de definir um índice da Azure Search. É um índice como uma tabela de base de dados que contém os dados e pode aceitar a consultas de pesquisa. É possível definir a estrutura de Olá de tooreflect esquema toomap Olá índice dos documentos Olá desejar toosearch, semelhante toofields numa base de dados.

Um esquema pode ser criado na Olá Azure portal ou através de programação utilizando Olá [.NET SDK](search-howto-dotnet-sdk.md) ou [REST API](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Passo 3: Dados de índice
Depois de definir um índice, está conteúdo tooupload pronto. Pode utilizar um modelo push ou pull.

modelo de extração Olá obtém dados a partir de origens de dados externas. É suportada através de *indexadores* que simplificar e automatizar aspetos da ingestão de dados, tais como ligar a, ler e serializar dados. [Indexadores](/rest/api/searchservice/Indexer-operations) estão disponíveis para a BD do Cosmos do Azure, SQL Database do Azure, Blob Storage do Azure e SQL Server alojado numa VM do Azure. Pode configurar um indexador para a pedido ou atualização de dados agendada.

modelo de envio de Olá é fornecido através de Olá SDK ou APIs REST, utilizada para enviar o índice de tooan documentos atualizado. Pode enviar dados a partir de praticamente qualquer conjunto de dados utilizando o formato JSON Olá. Consulte [adicionar, atualizar ou eliminar documentos](/rest/api/searchservice/addupdate-or-delete-documents) ou [como toouse Olá .NET SDK)](search-howto-dotnet-sdk.md) para obter orientações sobre a carregar os dados.

### <a name="step-4-search"></a>Passo 4: pesquisa
Depois de preencher um índice, pode [emitir consultas de pesquisa](/rest/api/searchservice/Search-Documents) pedidos de ponto final de serviço de tooyour utilizando simple HTTP com a REST API ou Olá .NET SDK.

## <a name="how-it-compares"></a>Como compara

Os clientes, muitas vezes, peça ao como [pesquisa em texto completo na Azure Search](search-lucene-query-architecture.md) compara com [pesquisa em texto completo](https://en.wikipedia.org/wiki/Full_text_search) no respetivo produto de base de dados. A nossa resposta é que as capacidades de idioma de pesquisa do Azure são mais rico e flexível e com suporte para consultas de Lucene, analisadores de idioma do Lucene e a Microsoft, analisadores personalizados para fonético ou outras entradas especializadas e Olá capacidade toomerge dados várias origens no índice de pesquisa de Olá. 

Outro ponto de inflection é que uma solução de pesquisa endereços experiência de pesquisa completa de Olá. Por exemplo, pode pretender classificação personalizada de resultados, navegação por facetas de filtragem auto-direcionada, realçando acessos e typeahead sugestões de consulta. 

Ferramentas para monitorizar e compreender a atividade de consulta podem também ter em conta numa decisão de solução de pesquisa. Por exemplo, pesquisa do Azure suporta [pesquisar a análise de tráfego](search-traffic-analytics.md) com base nas métricas taxa de clickthrough de, superior pesquisa, procura sem cliques e assim sucessivamente. Produtos onde pesquisa é um suplemento, tiver pouco provável toofind estas funcionalidades.

Utilização de recursos é outra consideração. Pesquisa de linguagem natural é frequentemente viáveis intensiva. Alguns dos nossos clientes descarregados tooAzure de operações de pesquisa procura como recursos da máquina toopreserve uma forma para o processamento de transações. Pela pesquisa externalizing, pode ajustar facilmente o volume de consulta de toomatch de escala.

Assim que tiver optado toogo Search dedicado, a sua decisão seguinte é entre um serviço em nuvem ou um servidor no local. Um serviço em nuvem é a escolha certa Olá se pretender que um [ative chave solução com overhead mínimo e a manutenção e a escala ajustável](#cloud-service-advantage).

Dentro do paradigma de nuvem Olá, vários fornecedores oferecem funcionalidades de linha de base comparável, com pesquisa de texto completo, pesquisa georreplicação e Olá capacidade toohandle um determinado nível de ambiguidade em entradas de pesquisa. Normalmente, tem um [funcionalidade especializada](#feature-drilldown), ou facilidade Olá e na simplicidade geral de APIs, ferramentas e gestão que determina Olá melhor opção.

Entre os fornecedores de nuvem, é mais fortes para cargas de trabalho de pesquisa de texto completo da Azure Search através de arquivos de conteúdo e as bases de dados no Azure, para aplicações que dependem principalmente a pesquisa para obtenção de informações e conteúda navegação. Força da codificação chave incluem:

+ Integração de dados do Azure (crawlers) na camada de indexação Olá
+ Portal do Azure para a gestão centralizada
+ Escala do Azure, fiabilidade e disponibilidade de trabalho
+ Análise de linguístico e personalizada, com analisadores de pesquisa em texto completo sólida 56 idiomas
+ [Principais funcionalidades comuns aplicações toosearch centrada](#feature-drilldown): classificação, facetamento, sugestões, sinónimos, pesquisa georreplicação e muito mais.

> [!Note]
> origens de dados e não do Azure de toobe são totalmente suportadas, mas dependem de uma metodologia de push de mais de código intensivas em vez de indexadores. Utilizar os APIs, pode encaminhar qualquer JSON documento tooan da Azure Search o índice collection.

Entre os nossos clientes, esses tooleverage capaz de Olá ser intervalo funcionalidades na Azure Search incluem catálogos online, programas de linha de negócio e aplicações de deteção do documento.

## <a name="rest-api--net-sdk"></a>REST API | .net SDK

Muitas tarefas podem ser executada no portal de Olá, Azure Search destina-se de que os programadores que pretendem toointegrate a funcionalidade de pesquisa para as aplicações existentes. Olá seguintes interfaces de programação está disponível.

|Plataforma |Descrição |
|-----|------------|
|[REST](/rest/api/searchservice/) | Comandos HTTP suportados por qualquer idioma, incluindo Xamarin, Java e JavaScript e plataforma de programação|
|[SDK do .NET](search-howto-dotnet-sdk.md) | Dispositivo de moldagem do .NET para Olá REST API oferece codificação eficiente em c# e outras linguagens de código gerido filtragem Olá .NET Framework |

## <a name="free-trial"></a>Avaliação gratuita
Os subscritores do Azure podem [aprovisionar um serviço no escalão gratuito Olá](search-create-service-portal.md).

Se não são um subscritor, pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Obter créditos para experimentar serviços pagos do Azure. Depois de que está a utilizar, pode manter a conta de Olá e utilizar [serviços gratuitos do Azure](https://azure.microsoft.com/free/). Nunca é cobrado o seu cartão de crédito, exceto se alterar as definições e peça toobe cobrado explicitamente.

Em alternativa, pode [ativar os benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): sua subscrição do MSDN dá-lhe créditos todos os meses que pode utilizar para serviços pagos do Azure. 

## <a name="how-tooget-started"></a>Como utilizar tooget

1. Criar um serviço no Olá [escalão gratuito](search-create-service-portal.md).

2. Siga os passos de uma ou mais das seguintes tutoriais de Olá. 

  + [Como toouse Olá .NET SDK](search-howto-dotnet-sdk.md) demonstra Olá principal passos no código gerido.  
  + [Introdução à REST API de Olá](https://github.com/Azure-Samples/search-rest-api-getting-started) mostra Olá mesmos passos utilizando Olá REST API.  
  + [Criar o seu primeiro índice no portal de Olá](search-get-started-portal.md) demonstra Olá do incorporada indexação e protótipo as funcionalidades do portal.   

Os motores de busca são controladores comuns de Olá de obtenção de informações em aplicações móveis, na web Olá e nos arquivos de dados da empresa. A pesquisa do Azure dá-lhe as ferramentas para criar uma experiência de pesquisa semelhante toothose em grande sites comercial.

Neste vídeo 9 minutos a partir do Gestor de programa Liam Cavanagh, saiba como integrar um motor de busca pode beneficiar da aplicação. Demonstrações curtas abrangem as principais funcionalidades na pesquisa do Azure e o aspeto de um fluxo de trabalho normal. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ 0 a 3 minutos abrange funcionalidades-chave e casos de utilização.
+ 3 a 4 minutos abrange o aprovisionamento de serviço. 
+ 4 a 6 minutos abrange toocreate do assistente utilizado de importar dados de um índice utilizando o conjunto de dados do Olá incorporada de real de propriedade.
+ 9 de 6 minutos abrange o Explorador de pesquisa e várias consultas.


