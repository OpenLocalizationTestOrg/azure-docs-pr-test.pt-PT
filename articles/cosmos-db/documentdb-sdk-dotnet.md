---
title: aaaAzure SDK .NET da BD do Cosmos & recursos | Microsoft Docs
description: "Saiba tudo sobre Olá SDK, incluindo as datas de versão, as datas de extinção e as alterações efetuadas entre cada versão do SDK .NET da Azure Cosmos DB de Olá e .NET API."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Cosmos do Azure SDK .NET da base de dados: Transferir e notas de versão
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Feed de alteração de .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Fornecedor de Recursos REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Transferência do SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência da API de .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Amostras**</td><td>[Exemplos de código do .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao hello SDK .NET da Azure Cosmos DB](documentdb-get-started.md)</td></tr>

<tr><td>**Tutorial de aplicação Web**</td><td>[Desenvolvimento da aplicação Web com base de dados do Azure Cosmos](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Arquitetura suportada atual**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Suporte adicionado para PartitionKeyRangeId como um FeedOption para controlo de âmbito do valor de intervalo de chaves de partição específica de tooa de resultados de consulta. 
* Suporte adicionado para StartTime como um toostart ChangeFeedOption procurando alterações Olá após esse tempo.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Foi corrigido um problema no Olá JsonSerializable classe que pode causar uma exceção de capacidade excedida da pilha.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Foi corrigido um problema que é necessário recompilar da aplicação Olá devido a introdução de toohello de JsonSerializerSettings como um parâmetro opcional no construtor do Olá DocumentClient.
* Olá marcado DocumentClient construtor obsoleto que necessárias JsonSerializerSettings como Olá o último parâmetro tooallow para valores predefinidos dos parâmetros ConnectionPolicy e ConsistencyLevel ao transmitir parâmetro JsonSerializerSettings.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Foi adicionado suporte para especificar JsonSerializerSettings personalizadas ao instanciar [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Foi corrigido um problema que afetados x64 máquinas que não suportam instruções SSE4 e gerar um SEHException quando executar consultas de API de DocumentDB do Azure Cosmos DB.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Suporte adicionado para um novo nível de consistência chamado ConsistentPrefix.
*   Adicionado suporte para as métricas de consulta para partições individuais.
*   Suporte adicionado para limitar o tamanho de Olá do token de continuação Olá para consultas.
*   Suporte adicionado para o rastreio mais detalhado para pedidos falhados.
*   Feitos alguns melhoramentos de desempenho nos Olá SDK.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Funcionalmente igual 1.13.3. Efetuou algumas alterações internas.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Funcionalmente igual 1.13.2. Efetuou algumas alterações internas.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Foi corrigido um problema que ignorado o valor de PartitionKey Olá fornecido FeedOptions para consultas de agregação.
* Foi corrigido um problema no processamento transparente de gestão de partição durante o voo intermédio partição cruzada Order By a execução da consulta.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Foi corrigido um problema que causou a impasses em algumas das Olá async APIs quando utilizada dentro do contexto do ASP.NET.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Correções toomake SDK mais ativação pós-falha de tooautomatic resiliente em determinadas condições.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Corrigir um problema que ocasionalmente faz com que um WebException: não foi possível resolver o nome remoto Olá.
* Olá adicionado suporte para diretamente ao ler um documento com tipo ao adicionar a nova API de tooReadDocumentAsync sobrecargas.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Adicionado suporte LINQ para consultas de agregação (CONTAGEM, MIN, MAX, soma e média).
* Corrigir para um problema de fuga de memória para o objeto de ConnectionPolicy Olá causado pela utilização de Olá de processador de eventos.
* Corrigir um problema wherein UpsertAttachmentAsync foi não está a funcionar quando ETag foi utilizada.
* Corrigir um problema wherein continuação de partição cruzada por ordem consulta foi não funcionar ao ordenar no campo de cadeia.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Suporte adicionado para consultas de agregação (CONTAGEM, MIN, MAX, soma e média). Consulte [suporte de agregação](documentdb-sql-query.md#Aggregates).
* Lowered débito mínimo em coleções particionadas de 10,100 RU/s too2500 RU/s.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Corrigir um problema wherein algumas das consultas de partição cruzada Olá foram falha no processo de anfitrião de 32 bits Olá.
* Corrigir um problema wherein contentor de sessão de Olá não estava a ser atualizada com token Olá para pedidos falhados no modo de Gateway.
* Corrigir um problema wherein uma consulta com as chamadas UDF na projeção falhasse em alguns casos.
* Correções de desempenho de lado de cliente para aumentar Olá ler e escrever o débito de pedidos de Olá.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Corrigir um problema wherein contentor de sessão de Olá não estava a ser atualizada com token Olá para pedidos falhados.
* Suporte adicionado para Olá SDK toowork num processo anfitrião de 32 bits. Tenha em atenção que, se utilizar consultas de partição cruzada, anfitrião de 64 bits de processamento é recomendada para um melhor desempenho.
* Melhoria do desempenho para cenários que envolvem consultas com um grande número de valores de chave de partição numa expressão IN.
* Preenchido diversas estatísticas de quota de recursos no Olá ResourceResponse para pedidos de leitura de coleção de documentos quando a opção de pedido de PopulateQuotaInfo está definida.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Correção de desempenho secundárias para Olá API CreateDocumentCollectionIfNotExistsAsync introduzida no 1.11.0.
* Correção de desempenho no Olá SDK para cenários que envolvem elevado grau de pedidos em simultâneo.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Suporte para nova classes e métodos Olá de tooprocess [alterar feed](change-feed.md) de documentos numa coleção.
* Suporte para a consulta da partição cruzada continuação e alguns melhoramentos de desempenho para consultas de partição cruzada.
* Adição de métodos CreateDatabaseIfNotExistsAsync e CreateDocumentCollectionIfNotExistsAsync.
* Suporta LINQ para funções de sistema: IsDefined, IsNull e IsPrimitive.
* Corrija binplacing automática da pasta de reciclagem do Microsoft.Azure.Documents.ServiceInterop.dll e DocumentDB.Spatial.Sql.dll assemblagens tooapplication, ao utilizar o pacote Nuget de Olá com projetos que tenham project.json ferramentas.
* Suporte para emitir os rastreios ETW do lado do cliente que pode ser útil em cenários de depuração.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Ligação direta adicionado suporte para coleções particionadas.
* Desempenho melhorado de nível de consistência vinculada tem um vínculo de Olá.
* Foram adicionadas polígono e tipos de dados de LineString ao especificar a coleção de indexação de política para consultas geográficos barreiras geográficas.
* LINQ suporte adicionado para StringEnumConverter, IsoDateTimeConverter e UnixDateTimeConverter ao traduzir a predicados.
* Várias correções de erros SDK.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Foi corrigido um problema que Olá caused seguir NotFoundException: Olá sessão não está disponível para o token de sessão de entrada de Olá de leitura. Esta exceção ocorreu em alguns casos, quando consultar Olá leitura-região de uma conta geo-distribuição.
* Expostos a propriedade de ResponseStream Olá no Olá ResourceResponse classe, que permite acesso direto toohello subjacente em fluxo a partir uma resposta.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Olá modificado ResourceResponse, FeedResponse, StoredProcedureResponse e MediaResponse classes tooimplement Olá correspondente interface pública para que pode ser mocked para teste orientadas por implementação (TDD).
* Foi corrigido um problema que causou a geração de um cabeçalho de chave de partição com formato incorreto ao utilizar um objeto de JsonSerializerSettings personalizado para serializar dados.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Foi corrigido um problema que causou a geração de execução longa consultas toofail com o erro: token de autorização não é válido na Olá a hora atual.
* Um problema que removidos Olá SqlParameterCollection original de cruzada partição parte superior/ordem-por consultas fixo.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Suporte adicionado para consultas paralelas para coleções particionadas.
* Suporte adicionado para entre consultas de ORDER BY e parte superior de partição para coleções particionadas.
* Olá fixo em falta referências tooDocumentDB.Spatial.Sql.dll e Microsoft.Azure.Documents.ServiceInterop.dll que são necessárias quando referenciar um projeto de base de dados do Azure Cosmos com um pacote de Azure Cosmos DB Nuget toohello referência.
* Olá fixo capacidade toouse os parâmetros de tipos diferentes ao utilizar as funções definidas pelo utilizador no LINQ. 
* Corrigido um erro para contas global replicadas onde Upsert chamadas foram que está a ser tooread direcionados localizações em vez de localizações de escrita.
* Foram adicionadas métodos toohello IDocumentClient interface que estavam em falta: 
  * Método de UpsertAttachmentAsync que assume mediaStream e opções como parâmetros
  * Método de CreateAttachmentAsync que aceita opções como parâmetro
  * Método de CreateOfferQuery que assume querySpec como parâmetro.
* Classes públicas não seladas que são expostas na interface de IDocumentClient Olá.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Suporte adicionado Olá para contas de multirregião base de dados.
* Suporte adicionado para repetição nos pedidos otimizadas.  Utilizador pode personalizar o número de Olá de repetições e tempo de espera máximo de Olá através da configuração de propriedade de ConnectionPolicy.RetryOptions Olá.
* Adicionar uma nova interface de IDocumentClient define assinaturas hello de todas as propriedades de DocumenClient e métodos.  Como parte desta alteração, alterar também os métodos de extensão que criar toomethods IQueryable e IOrderedQueryable Olá própria classe de DocumentClient.
* Adicionar configuração opção tooset Olá ServicePoint.ConnectionLimit para um ponto de final de base de dados do Azure Cosmos especificado Uri.  Utilize o valor predefinido do ConnectionPolicy.MaxConnectionLimit toochange Olá, que está definido too50.
* IPartitionResolver preterida e a implementação.  Suporte para IPartitionResolver está obsoleto. É recomendado que utilize coleções Particionadas de armazenamento superior e débito.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Adicionar uma sobrecarga tooUri com base em método ExecuteStoredProcedureAsync que demora RequestOptions como parâmetro.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Tempo toolive (TTL) suporte adicionado para documentos.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Corrigido um erro em empacotamento Nuget do .NET SDK de empacotamento como parte de uma solução de serviço de nuvem do Azure.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Implementado [particionada coleções](partition-data.md) e [níveis de desempenho definido pelo utilizador](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Fixo]**  Emite de ponto final de consultar a base de dados de Cosmos do Azure: ' System.Net.Http.HttpRequestException: erro ao copiar o fluxo de conteúdo tooa'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* LINQ expandido, incluindo operadores novo para paginação, condicionais expressões de suporte e intervalo de comparação.
  * Tirar operador tooenable comportamento SELECIONAR parte superior do LINQ
  * Comparações de intervalo de cadeias de tooenable operador CompareTo
  * Condicional (?) e unir operadores (?)
* **[Fixo]**  ArgumentOutOfRangeException ao combinar a projecção de modelo com Where-numa consulta LINQ. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Fixo]**  Se selecionar não Olá de expressão último Olá fornecedor LINQ assumido não projeção e produzidos SELECIONE * incorretamente.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Upsert implementado, métodos de UpsertXXXAsync adicionado
* Melhorias de desempenho para todos os pedidos
* Suporte de fornecedor LINQ para condicional, unir e os métodos de CompareTo para cadeias
* **[Fixo]**  Fornecedor LINQ--> Implementar contém método na lista toogenerate Olá SQL mesmo que em IEnumerable e a matriz
* **[Fixo]**  BackoffRetryUtility utiliza Olá HttpRequestMessage mesmo novamente em vez de criar um novo, tente novamente
* **[Obsoleto]**  UriFactory.CreateCollection--> agora deve utilizar UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Fixo]**  Localização problemas ao utilizar as informações de cultura de não en, como nl-NL, etc. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Adicionado com base no ID de encaminhamento
  * Novo auxiliar UriFactory tooassist com construir ligações com base no ID de recurso
  * Novo sobrecargas no DocumentClient tootake no URI
* Foram adicionadas IsValid() e IsValidDetailed() no LINQ para geoespacial
* Suporte de fornecedor LINQ avançado:
  * **Bibliotecas** -Abs, Acos, Asin, Atan, limite, Cos, Exp, piso, registo, Log10, Pow, Round, início de sessão único, Sqrt, Tan, truncar
  * **Cadeia** -Concat, contém, EndsWith IndexOf, Count, ToLower, TrimStart, substituir, inverso, TrimEnd, StartsWith, subcadeia, ToUpper
  * **Matriz** -Concat, contém, contagem
  * **EM** operador

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Suporte adicionado para modificar as políticas de indexação.
  * Novo método de ReplaceDocumentCollectionAsync DocumentClient
  * Nova propriedade IndexTransformationProgress no ResourceResponse<T> para controlar o progresso da percentagem de alterações de política de índice
  * Está agora mutável DocumentCollection.IndexingPolicy
* Suporte adicionado para indexação geográficos e a consulta.
  * Novo Microsoft.Azure.Documents.Spatial espaço de nomes para serialização/anulação da serialização de tipos geográficos como ponto e polígono
  * Nova classe de SpatialIndex para indexação de dados de GeoJSON armazenados na base de dados do Cosmos
* **[Fixo]**  Consulta de SQL incorreto gerada a partir de uma expressão LINQ [#38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Adicionar uma dependência no v5.0.7 newtonsoft.
* As alterações efetuadas toosupport Order By:
  
  * Suporte de fornecedor LINQ para OrderBy() ou OrderByDescending()
  * IndexingPolicy toosupport Order By 
    
    **Alteração inovadora possíveis** 
    
    Se tiver código existente coleções que Aprovisiona com uma política de indexação personalizada, a necessidades toobe existente do código atualizado nova IndexingPolicy classe toosupport Olá. Não se tiver nenhuma política de indexação personalizada, em seguida, esta alteração não afeta a.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Suporte adicionado para criação de partições de dados utilizando Olá novas HashPartitionResolver e RangePartitionResolver classes e Olá IPartitionResolver.
* Serialização de DataContract adicionada.
* GUID adicionado suporte no fornecedor LINQ.
* Foram adicionada UDF suporta LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>Versão & extinção datas
A Microsoft disponibiliza notificação, pelo menos, **12 meses** previamente extinguir um SDK na ordem toosmooth Olá transição tooa/suportada mais recente versão.

Apenas são adicionadas novas funcionalidades e a funcionalidade e otimizações o atual toohello SDK, como tal, é recomendado que lhe toohello sempre atualização mais recente versão do SDK antecipadamente quanto possível. 

Qualquer base de dados do Cosmos utilizando um SDK extinto é rejeitado pelo serviço de Olá tooAzure de pedidos.

<br/>

| Versão | Data da versão | Data de retirada |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 de Agosto de 2017 |--- |
| [1.16.1](#1.16.1) |07 de Agosto de 2017 |--- |
| [1.16.0](#1.16.0) |02 de Agosto de 2017 |--- |
| [1.15.0](#1.15.0) |30 de Junho de 2017 |--- |
| [1.14.1](#1.14.1) |23 de Maio de 2017 |--- |
| [1.14.0](#1.14.0) |10 de maio de 2017 |--- |
| [1.13.4](#1.13.4) |09 de Maio de 2017 |--- |
| [1.13.3](#1.13.3) |06 de Maio de 2017 |--- |
| [1.13.2](#1.13.2) |19 de Abril de 2017 |--- |
| [1.13.1](#1.13.1) |29 de Março de 2017 |--- |
| [1.13.0](#1.13.0) |24 de Março de 2017 |--- |
| [1.12.2](#1.12.2) |20 de março de 2017 |--- |
| [1.12.1](#1.12.1) |14 de março de 2017 |--- |
| [1.12.0](#1.12.0) |15 de Fevereiro de 2017 |--- |
| [1.11.4](#1.11.4) |06 de Fevereiro de 2017 |--- |
| [1.11.3](#1.11.3) |26 de Janeiro de 2017 |--- |
| [1.11.1](#1.11.1) |21 de Dezembro de 2016 |--- |
| [1.11.0](#1.11.0) |08 de Dezembro de 2016 |--- |
| [1.10.0](#1.10.0) |27 de Setembro de 2016 |--- |
| [1.9.5](#1.9.5) |01 de Setembro de 2016 |--- |
| [1.9.4](#1.9.4) |24 de Agosto de 2016 |--- |
| [1.9.3](#1.9.3) |15 de Agosto de 2016 |--- |
| [1.9.2](#1.9.2) |23 de Julho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de Junho de 2016 |--- |
| [1.7.1](#1.7.1) |06 de Maio de 2016 |--- |
| [1.7.0](#1.7.0) |26 de Abril de 2016 |--- |
| [1.6.3](#1.6.3) |08 de Abril de 2016 |--- |
| [1.6.2](#1.6.2) |29 de Março de 2016 |--- |
| [1.5.3](#1.5.3) |19 de Fevereiro de 2016 |--- |
| [1.5.2](#1.5.2) |14 de Dezembro de 2015 |--- |
| [1.5.1](#1.5.1) |23 de Novembro de 2015 |--- |
| [1.5.0](#1.5.0) |05 de Outubro de 2015 |--- |
| [1.4.1](#1.4.1) |25 de Agosto de 2015 |--- |
| [1.4.0](#1.4.0) |13 de Agosto de 2015 |--- |
| [1.3.0](#1.3.0) |05 de Agosto de 2015 |--- |
| [1.2.0](#1.2.0) |06 de Julho de 2015 |--- |
| [1.1.0](#1.1.0) |30 de Abril de 2015 |--- |
| [1.0.0](#1.0.0) |08 de Abril de 2015 |--- |


## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consultar também
toolearn mais informações sobre a base de dados do Cosmos, consulte [base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página do serviço. 

