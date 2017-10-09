---
title: Guia de estrutura da tabela de armazenamento de aaaAzure | Microsoft Docs
description: "Design dimensionável e tabelas de Performant no Table Storage do Azure"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Guia de Design da tabela de armazenamento do Azure: Estruturar dimensionável e tabelas Performant
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign dimensionável e tabelas de performant tem de considerar um número de fatores, tais como o desempenho, escalabilidade e o custo. Se anteriormente tiver concebido esquemas para bases de dados relacionais, estas considerações será familiar tooyou, mas enquanto existirem alguns semelhanças entre o modelo de armazenamento de serviço de Azure Table Olá e modelos relacionais, também existem muitas importantes diferenças. Estas diferenças normalmente levar toovery diferentes estruturas que poderá ser counter-intuitive ou errada toosomeone familiarizado com bases de dados relacionais, mas o que sentido boa se está a conceber um arquivo de chave/valor NoSQL, tais como Olá serviço de Azure Table. Muitos dos seus diferenças de estrutura irão refletir o facto de Olá que o serviço de tabela de Olá está concebida toosupport aplicações de escala da nuvem que podem conter billions das entidades (linhas na terminologia de base de dados relacional) de dados ou para conjuntos de dados tem de suportar muito elevado volumes de transação: por conseguinte, tem de toothink diferente sobre como armazena os dados e compreender como funciona o Olá serviço tabela. Um arquivo de dados NoSQL bem estruturado pode ativar a sua solução tooscale muito mais (e um custo mais baixo) que uma solução que utiliza uma base de dados relacional. Este guia ajuda-o com estes tópicos.  

## <a name="about-hello-azure-table-service"></a>Sobre Olá serviço tabela do Azure
Esta secção realça algumas das Olá as principais funcionalidades do serviço de tabela Olá que são especialmente relevante toodesigning para o desempenho e escalabilidade. Se for tooAzure novo armazenamento e Olá serviço tabela, leia primeiro [introdução tooMicrosoft Storage do Azure](storage-introduction.md) e [introdução ao armazenamento de tabelas do Azure através do .NET](storage-dotnet-how-to-use-tables.md) antes de ler este resto Olá artigo. Embora o foco Olá neste guia é Olá serviço tabela, incluirá algumas debate Olá filas do Azure e serviços de Blob, e como pode utilizá-los, juntamente com Olá serviço tabela numa solução.  

O que é o serviço de tabela Olá? Como seria de esperar do nome de Olá, Olá serviço tabela utiliza um toostore de dados de formato tabular. Na terminologia de padrão Olá, cada linha da tabela de Olá represente uma entidade e arquivo de colunas de Olá Olá várias propriedades dessa entidade. Cada entidade tem um par de chaves toouniquely identificá-lo e uma coluna de carimbo Olá serviço tabela utiliza tootrack quando entidade Olá foi atualizada pela última vez (isto ocorre automaticamente e não é possível substituir manualmente Olá timestamp com um valor arbitrário). Olá serviço tabela utiliza este simultaneidade otimista de toomanage last-modified timestamp (LMT).  

> [!NOTE]
> operações de REST API do serviço de tabela Olá também devolvem uma **ETag** valor que deriva de Olá last-modified timestamp (LMT). Neste documento utilizaremos Olá termos ETag e LMT-no alternadamente porque consultarem toohello mesmo subjacente dados.  
> 
> 

Olá exemplo seguinte mostra um toostore de estrutura da tabela simples entidades do empregado e departamento. Muitos dos exemplos de Olá mostrados posteriormente neste guia são baseados nesta estrutura simple.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td>Jun</td>
<td>CaO</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Departamento</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Vendas</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td>Manuel</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Até ao momento, este analisa muito semelhantes tooa tabela na base de dados relacional com principais diferenças de Olá que está a ser Olá colunas obrigatórias, e hello capacidade toostore entidade vários tipos de Olá mesma tabela. Além disso, cada um dos Olá propriedades definidas pelo utilizador, tais como **FirstName** ou **idade** tem um tipo de dados, tais como número inteiro ou uma cadeia, apenas como uma coluna na base de dados relacional. Embora ao contrário numa base de dados relacional, natureza sem esquema Olá Olá significa de serviço de tabela que não precisa de ter uma propriedade Olá mesmo tipo de dados em cada entidade. tipos de dados complexos toostore numa única propriedade, tem de utilizar um formato serializado como JSON ou XML. Para obter mais informações sobre tipos de dados de serviço suportado, tais como de tabela Olá, intervalos de data suportados, regras de nomenclatura e restrições de tamanho, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Como verá, à sua escolha de **PartitionKey** e **RowKey** é fundamental toogood tabela estrutura. Cada entidade armazenada numa tabela tem de ter uma combinação única de **PartitionKey** e **RowKey**. Tal como acontece com as chaves de uma tabela de base de dados relacional, Olá **PartitionKey** e **RowKey** os valores são toocreate indexada um índice em cluster que permite a rápida look-ups; no entanto, Olá serviço tabela não criar qualquer índices secundários, pelo que estes são Olá apenas dois indexado propriedades (alguns dos padrões de Olá descritos mais à frente mostram como pode contornar esta limitação aparente).  

Uma tabela é constituída por uma ou mais partições e como verá, muitas das Olá design decisões que tomar irá ser à volta de escolher um adequado **PartitionKey** e **RowKey** toooptimize sua solução. Uma solução pode consistir apenas uma única tabela que contém todas as entidades organizadas em partições, mas normalmente uma solução irá ter várias tabelas. As tabelas ajudá-lo toologically organizar as entidades, ajudam a gerir o acesso toohello dados através de listas de controlo de acesso e pode colocar uma tabela inteira utilizando uma operação de armazenamento única.  

### <a name="table-partitions"></a>Partições da tabela
nome da conta Olá, nome da tabela e **PartitionKey** em conjunto identificar partição Olá no âmbito do serviço de armazenamento de olá onde o serviço de tabela Olá armazena entidade Olá. Bem como a ser parte do esquema para entidades de endereçamento de Olá, partições definem um âmbito para transações (consulte [entidade grupo transações](#entity-group-transactions) abaixo) e a base de Olá do formulário da forma como o serviço de tabela Olá dimensiona. Para obter mais informações sobre as partições Consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md).  

No serviço tabela Olá, um nó individual dos serviços de um ou mais partições de conclusão e Olá escalas de serviço por dinamicamente o balanceamento de carga partições entre nós. Se um nó estiver sob carga, o serviço de tabela Olá pode *dividir* intervalo Olá de partições servidos esse nó em nós diferentes; quando o tráfego subsides, o serviço de Olá pode *intercalação* partição Olá varia de fazer uma cópia de nós silenciosos para um único nó.  

Para obter mais informações sobre Olá detalhes internos de Olá serviço tabela e, em particular como serviço Olá gere partições, consulte o documento de Olá [armazenamento do Microsoft Azure: A nuvem armazenamento serviço de elevada disponibilidade com consistência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Transações de grupo de entidade
No serviço tabela Olá, transações de grupo de entidade (EGTs) são o mecanismo de apenas incorporada de Olá para executar atualizações atómicas entre várias entidades. EGTs também são referidos tooas *lote de transações* em alguma documentação. EGTs só pode operar em entidades armazenadas no Olá mesma partição (partilha Olá mesma chave de partição numa tabela fornecida), por isso sempre que necessitar de comportamento transacional atómico entre várias entidades terá tooensure dessas entidades estão a ser Olá mesma partição. Isto é frequentemente um motivo para manter os vários tipos de entidade no Olá mesmo tabela (e partição) e não a utilizar várias tabelas para tipos de entidade diferente. Um único EGT pode operar no máximo de 100 entidades.  Se submeter vários EGTs simultâneas para o processamento é importante tooensure esses EGTs não operar em entidades que são comuns entre EGTs como processar caso contrário, pode sofrer um atraso.

EGTs também introduzir um compromisso potencial para tooevaluate na sua estrutura: utilizar mais partições irá aumentar a escalabilidade de Olá da sua aplicação porque o Azure tem mais de oportunidades de balanceamento de carga pedidos entre nós, mas isto pode limitar Olá capacidade das suas aplicações tooperform atómico transações e manter a consistência forte para os seus dados. Além disso, existem metas de escalabilidade específico ao nível de Olá da partição que pode limitar o débito de Olá de transações que pode esperar para um único nó: Para mais informações sobre metas de escalabilidade Olá para contas do storage do Azure e a tabela de Olá Service, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md). As secções deste guia abordam vários design estratégias que o ajudam a gerir compromissos, tais como este e discutem melhor toochoose a chave de partição com base nos requisitos específicos de Olá da sua aplicação de cliente.  

### <a name="capacity-considerations"></a>Considerações sobre a capacidade
Olá tabela que se segue inclui algumas das Olá valores de chave toobe em consideração quando está a conceber uma solução de serviço tabela:  

| Capacidade total de uma conta de armazenamento do Azure | 500 TB |
| --- | --- |
| Número de tabelas de uma conta de armazenamento do Azure |Limitado apenas pela capacidade de Olá Olá da conta de armazenamento |
| Número de partições numa tabela |Limitado apenas pela capacidade de Olá Olá da conta de armazenamento |
| Número de entidades numa partição |Limitado apenas pela capacidade de Olá Olá da conta de armazenamento |
| Tamanho de uma entidade individuais |Configurar too1 MB com um máximo de 255 propriedades (incluindo Olá **PartitionKey**, **RowKey**, e **Timestamp**) |
| Tamanho de Olá **PartitionKey** |Uma cadeia de cópia de segurança too1 KB de tamanho |
| Tamanho de Olá **RowKey** |Uma cadeia de cópia de segurança too1 KB de tamanho |
| Tamanho de uma transação de grupo de entidade |Uma transação pode incluir um máximo de 100 entidades e payload Olá tem de ser inferior a 4 MB de tamanho. Uma vez, uma EGT só pode atualizar uma entidade. |

Para obter mais informações, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Considerações sobre o custo
O Table storage é relativamente barato, mas deve incluir estimativas de custos para ambos os quantidade de utilização e Olá de capacidade de transações como parte da sua avaliação de qualquer solução que utiliza o serviço de tabela Olá. No entanto, muitos cenários de armazenamento de dados duplicados ou denormalized no Olá tooimprove de ordem de desempenho ou escalabilidade da sua solução é tootake uma abordagem válido. Para obter mais informações sobre preços, consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Diretrizes para estruturar tabela
Estas listas resumem algumas diretrizes chave Olá que deve ter em consideração quando conceber a sua tabelas e este guia irá resolvê-los todos em mais detalhe posteriormente. Estas diretrizes são muito diferentes das diretrizes Olá que normalmente seriam siga para o design da base de dados relacional.  

Conceber a sua toobe de solução do serviço tabela *ler* eficiente:

* ***Estrutura de consulta em aplicações pesado de leitura.*** Ao conceber a sua tabelas, tenha em consideração consultas de Olá (especialmente Olá latência aqueles confidenciais) que será executado antes de pensar sobre como atualizar as entidades. Normalmente, isto resulta numa solução eficiente e performant.  
* ***Especifique PartitionKey e RowKey nas suas consultas.*** *Ponto de consultas* como estas são consultas de serviço de tabela Olá mais eficientes.  
* ***Considere armazenar cópias duplicadas de entidades.*** O Table storage é cheap, por isso, considere armazenar Olá a mesma entidade várias vezes (com chaves diferentes) tooenable consultas mais eficientes.  
* ***Considere denormalizing os seus dados.*** O Table storage é cheap por isso considere denormalizing os seus dados. Por exemplo, armazene entidades de resumidas para que as consultas para agregadas dados basta tooaccess uma única entidade.  
* ***Utilize os valores da chave compostos.*** Olá apenas chaves tiver são **PartitionKey** e **RowKey**. Por exemplo, utilize os valores da chave composta tooenable acesso codificada alternativo caminhos tooentities.  
* ***Utilize projeção da consulta.*** Pode reduzir a quantidade de Olá de dados que são transferidos através de rede de Olá através de consultas que selecionar apenas os campos de Olá que precisa.  

Conceber a sua toobe de solução do serviço tabela *escrever* eficiente:  

* ***Não crie partições frequente.*** Escolha chaves que lhe permitem toospread os pedidos entre várias partições em qualquer ponto de tempo.  
* ***Evite picos de tráfego.*** Uniforme tráfego Olá durante um período de tempo razoável e evitar picos de tráfego.
* ***Necessariamente não crie uma tabela separada para cada tipo de entidade.*** Quando necessitar de transações atómicas em tipos de entidade, pode armazenar estes vários tipos de entidade no Olá mesma partição no Olá mesma tabela.
* ***Considere tem alcançar o débito máximo Olá.*** Tem de ter em consideração os objetivos de escalabilidade Olá para Olá serviço tabela e certifique-se de que a estrutura não fará com que tooexceed-los.  

Como ler este guia, irá ver exemplos que colocar todos estes princípios em prática.  

## <a name="design-for-querying"></a>Conceção para consultas
Soluções de serviço tabela podem ser lidos intensiva, intensiva de escrita ou uma combinação de Olá dois. Esta secção centra-se no Olá coisas toobear em consideração quando conceber a sua toosupport de serviço tabela operações de leitura de forma eficiente. Normalmente, também é eficiente para operações de escrita de uma estrutura que suporta operações de leitura de forma eficiente. No entanto, existem considerações adicionais toobear em consideração quando conceber toosupport escrever operações, abordadas na secção seguinte Olá, [Design de modificação de dados](#design-for-data-modification).

Um ponto de partida para estruturar a sua tooenable de solução do serviço tabela tooread dados eficiente são tooask "que consultas serão a minha aplicação necessidade tooexecute tooretrieve Olá dados de que necessita de Olá serviço tabela?"  

> [!NOTE]
> Com o serviço tabela Olá, é importante tooget Olá design correto adiantado porque é difícil e dispendiosa toochange-lo mais tarde. Por exemplo, numa base de dados relacional é, muitas vezes, tooaddress possíveis problemas de desempenho adicionando simplesmente índices da base de dados existente tooan: não é uma opção com Olá serviço tabela.  
> 
> 

Esta secção centra-se nos problemas-chave Olá que devem ser abordadas ao conceber as tabelas para consultas. tópicos de Olá abrangidos nesta secção incluem:

* [Como à sua escolha de PartitionKey e RowKey tem impacto no desempenho das consultas](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Escolher um PartitionKey adequado](#choosing-an-appropriate-partitionkey)
* [Otimizar as consultas para Olá serviço tabela](#optimizing-queries-for-the-table-service)
* [Ordenação de dados no Olá serviço tabela](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Como à sua escolha de PartitionKey e RowKey tem impacto no desempenho das consultas
Olá exemplos seguintes partem do princípio de serviço de tabela Olá é o armazenamento de entidades de empregado com Olá seguir a estrutura (maioria dos exemplos de Olá omitir Olá **Timestamp** propriedade para efeitos de clareza):  

| *Nome da coluna* | *Tipo de dados* |
| --- | --- |
| **PartitionKey** (nome do departamento de) |Cadeia |
| **RowKey** (Id de empregado) |Cadeia |
| **Nome próprio** |Cadeia |
| **Apelido** |Cadeia |
| **Idade** |Número inteiro |
| **Endereço de correio eletrónico** |Cadeia |

Olá secção anterior [descrição geral do serviço de Azure Table](#overview) descreve algumas das Olá as principais funcionalidades de Olá serviço tabela do Azure que tenham uma influência direta na conceção para a consulta. Estes resultam em Olá seguintes diretrizes gerais para conceber consultas do serviço de tabela. Tenha em atenção que a sintaxe de filtro de Olá utilizado nos exemplos de Olá abaixo é de Olá tabela REST API do serviço, para obter mais informações, consulte [entidades de consulta](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* A ***ponto consulta*** é Olá toouse de pesquisa mais eficiente e é recomendada toobe utilizado para pesquisas de elevado volume ou pesquisas que necessitam de latência mais baixa. Este tipo uma consulta pode utilizar Olá índices toolocate uma entidade individuais forma muito eficiente, especificando ambos Olá **PartitionKey** e **RowKey** valores. Por exemplo: $filter = (PartitionKey eq 'Vendas') e (RowKey eq '2')  
* Segundo melhor é um ***intervalo de consulta*** que utiliza Olá **PartitionKey** e os filtros num intervalo de **RowKey** valores tooreturn mais de uma entidade. Olá **PartitionKey** valor identifica uma partição específica e Olá **RowKey** valores identificam um subconjunto de Olá as entidades dessa partição. Por exemplo: $filter = PartitionKey eq 'Dos vendas e do RowKey ge' e RowKey lt possível '  
* É melhor terceiro um ***partição analisar*** que utiliza Olá **PartitionKey** e filtros e que a outra propriedade de chave não podem devolver mais de uma entidade. Olá **PartitionKey** valor identifica uma partição específica, e selecione para um subconjunto de entidades de Olá na partição de que os valores de propriedade de Olá. Por exemplo: $filter = PartitionKey eq 'Vendas' e LastName eq 'Santos'  
* A ***tabela analisar*** não inclui Olá **PartitionKey** e é muito ineficaz porque este procura todas as partições de Olá que compõem a sua tabela por sua vez para qualquer entidades correspondentes. A operação executará uma análise da tabela, independentemente se o filtro utiliza Olá **RowKey**. Por exemplo: $filter = LastName eq 'Jones'  
* As consultas que devolvem várias entidades devolvem-las ordenados **PartitionKey** e **RowKey** ordem. entidades Olá resorting tooavoid no cliente Olá, escolha um **RowKey** que define a sequência de ordenação Olá mais comuns.  

Tenha em atenção que utilizar um "**ou**" toospecify um filtro com base no **RowKey** valores resultados de uma análise de partição e não é tratado como uma consulta de intervalo. Por conseguinte, deve evitar consultas que utilizam os filtros, tais como: $filter = PartitionKey eq 'Vendas' e (RowKey eq '121' ou RowKey eq '322')  

Para obter exemplos de código do lado do cliente que utilizam Olá biblioteca de clientes de armazenamento tooexecute eficiente consultas, consulte:  

* [Executar uma consulta de ponto utilizando Olá biblioteca de clientes de armazenamento](#executing-a-point-query-using-the-storage-client-library)
* [A obter várias entidades com LINQ](#retrieving-multiple-entities-using-linq)
* [Projecção do lado do servidor](#server-side-projection)  

Para obter exemplos de código do lado do cliente que pode processar vários entidade tipos armazenados no Olá mesma tabela, consulte:  

* [Trabalhar com tipos de entidade heterogénea](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Escolher um PartitionKey adequado
À sua escolha de **PartitionKey** deve balancear Olá necessidade tooenables Olá utilização EGTs (consistência do tooensure) contra Olá requisito toodistribute as entidades de várias partições (tooensure uma solução dimensionável).  

Num Alpine, pode armazenar todas as entidades numa partição única, mas isto pode limitar a escalabilidade de Olá da sua solução e seria impedem serviço de tabela Olá balancear tooload capaz de pedidos. Em Olá outro Alpine, pode armazenar uma entidade por partição, que seria altamente dimensionável e que lhe permite pedidos de tooload saldo de serviços de tabela Olá, mas que iria impedi-lo da utilização de transações do grupo de entidade.  

Um ideal **PartitionKey** é aquele que lhe permite consultas eficiente toouse e que tem suficiente partições tooensure sua solução é dimensionável. Normalmente, irá encontrar que as entidades terão uma propriedade adequada que distribui as entidades partições suficientes.

> [!NOTE]
> Por exemplo, um sistema que armazena informações sobre os utilizadores ou os funcionários, UserID pode ser uma boa PartitionKey. Pode ter várias entidades que utilizam um ID de utilizador especificado como chave de partição Olá. Cada entidade que armazena dados sobre um utilizador se encontra agrupada para uma única partição e, por isso, estas entidades estão acessíveis através de transações do grupo de entidade, enquanto altamente dimensionável.
> 
> 

Existem considerações adicionais na sua escolha de **PartitionKey** relacionadas com toohow irá inserir, atualizar e eliminar entidades: consulte a secção de Olá [Design de modificação de dados](#design-for-data-modification) abaixo.  

### <a name="optimizing-queries-for-hello-table-service"></a>Otimizar as consultas para Olá serviço tabela
Olá serviço tabela indexa automaticamente os seus entidades utilizando Olá **PartitionKey** e **RowKey** valores de um índice em cluster único, por conseguinte, Olá razão que o ponto consultas são Olá toouse mais eficiente . No entanto, não existem nenhum índices diferente que no índice em cluster do Olá na Olá **PartitionKey** e **RowKey**.

Muitas estruturas têm de cumprir pesquisa de tooenable requisitos de entidades com base em vários critérios. Por exemplo, localizar entidades de empregado com base no correio eletrónico, id de empregado ou apelido. Olá seguintes padrões na secção de Olá [padrões de conceção de tabela](#table-design-patterns) endereço estes tipos de requisito e descrevem formas de trabalhar em torno do facto de Olá que o serviço de tabela Olá fornecem índices secundários:  

* [Padrão de índice secundário intra partição](#intra-partition-secondary-index-pattern) -armazenar várias cópias de cada entidade utilizando diferentes **RowKey** valores (no Olá mesma partição) tooenable rápidos e eficientes pesquisas e ordenação alternada ordena utilizando diferentes **RowKey** valores.  
* [Padrão de índice secundário partição entre](#inter-partition-secondary-index-pattern) - armazenar várias cópias de cada entidade com diferentes valores de RowKey em partições separadas ou em tabelas separadas tooenable rápido e eficiente pesquisas e ordenação alternada ordena utilizando diferentes**RowKey** valores.  
* [Padrão de entidades do índice](#index-entities-pattern) -manter índice entidades tooenable eficiente pesquisas que devolvem apresenta uma lista de entidades.  

### <a name="sorting-data-in-hello-table-service"></a>Ordenação de dados no Olá serviço tabela
Olá serviço tabela devolve entidades ordenadas por ordem, com base no ascendente **PartitionKey** e, em seguida, **RowKey**. Estas chaves são valores de cadeia e tooensure valores numéricos ordenar corretamente, deverá convertê-los comprimento tooa fixo e preenche-as com zeros. Por exemplo, se hello valor de id de empregado utilizar como Olá **RowKey** é um valor de número inteiro, deve converter id de empregado **123** demasiado**00000123**.  

Muitas aplicações têm requisitos toouse dados ordenados as ordens de diferentes: por exemplo, ordenação dos empregados pelo nome ou ao associar data. Olá seguintes padrões na secção de Olá [padrões de conceção de tabela](#table-design-patterns) como tooalternate ordenação ordena para as entidades de endereços:  

* [Padrão de índice secundário intra partição](#intra-partition-secondary-index-pattern) -armazenar várias cópias de cada entidade com diferentes valores de RowKey (no Olá mesma partição) tooenable rápidos e eficientes pesquisas e ordenação alternada ordena utilizando valores RowKey diferentes.  
* [Padrão de índice secundário partição entre](#inter-partition-secondary-index-pattern) - armazenar várias cópias de cada entidade com diferentes valores de RowKey em separado partições em tabelas separadas tooenable rápido e eficiente pesquisas e ordenação alternada ordena utilizando RowKey diferentes valores.
* [Padrão de seguimento de registo](#log-tail-pattern) -obter Olá  *n*  entidades recentemente adicionado tooa partição utilizando um **RowKey** valor ordena na data inversa e ordem de tempo.  

## <a name="design-for-data-modification"></a>Estrutura de modificação de dados
Esta secção centra-se em considerações de design Olá para otimizar as introduções, atualizações e elimina. Em alguns casos, terá de compromisso de Olá tooevaluate entre estruturas otimizar para consulta contra estruturas otimizar a modificação de dados tal como o que fazer em estruturas de bases de dados relacionais (embora técnicas Olá para gerir Olá design compromissos são diferentes numa base de dados relacional). Olá secção [padrões de conceção de tabela](#table-design-patterns) descreve alguns padrões de conceção de detalhado para Olá serviço tabela e realça algumas destas compromissos. Na prática, irá encontrar que muitas estruturas otimizadas para consultar entidades também funcionam bem para modificar as entidades.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Otimizar o desempenho de Olá de inserção, atualização e eliminação de operações
tooupdate ou eliminar uma entidade, tem de ser capaz de tooidentify-lo utilizando Olá **PartitionKey** e **RowKey** valores. No que esta respeita, à sua escolha de **PartitionKey** e **RowKey** para modificar as entidades deve seguir semelhante toosupport de escolha de tooyour critérios ponto consultas porque pretende tooidentify entidades como eficientemente possível. Não pretende toouse um ineficaz partição ou tabela análise toolocate uma entidade em Olá toodiscover de ordem **PartitionKey** e **RowKey** valores necessário tooupdate ou eliminá-lo.  

Olá seguintes padrões na secção de Olá [padrões de conceção de tabela](#table-design-patterns) endereços otimizar o desempenho de Olá ou a inserção, atualização e operações de eliminação:  

* [Um volume elevado eliminar padrão](#high-volume-delete-pattern) -ativar a eliminação de Olá de um grande volume de entidades armazenando todas as entidades de Olá para eliminação em simultâneo na sua própria tabela separada; eliminar entidades Olá, eliminando tabela Olá.  
* [Padrão de séries de dados](#data-series-pattern) -série de dados completa de loja uma única entidade toominimize Olá diversas pedidos que efetuar.  
* [Padrão de entidades Wide](#wide-entities-pattern) -utilizar várias entidades lógico de toostore entidades físicas com mais do que 252 propriedades.  
* [Padrão de entidades grandes](#large-entities-pattern) -valores de propriedade grande de toostore de armazenamento de BLOBs de utilização.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Garantir a consistência no seu entidades armazenadas
Olá outro fator chave que influencia à sua escolha de chaves para otimizar as modificações de dados é como tooensure consistência utilizando transações atomic. Só pode utilizar um toooperate EGT no entidades armazenadas no Olá mesma partição.  

Olá seguintes padrões na secção de Olá [padrões de conceção de tabela](#table-design-patterns) endereço gerir consistência:  

* [Padrão de índice secundário intra partição](#intra-partition-secondary-index-pattern) -armazenar várias cópias de cada entidade utilizando diferentes **RowKey** valores (no Olá mesma partição) tooenable rápidos e eficientes pesquisas e ordenação alternada ordena utilizando diferentes **RowKey** valores.  
* [Padrão de índice secundário partição entre](#inter-partition-secondary-index-pattern) - armazenar várias cópias de cada entidade com diferentes valores de RowKey em partições separadas ou em tabelas separadas tooenable rápido e eficiente pesquisas e ordenação alternada ordena utilizando diferentes**RowKey** valores.  
* [Padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern) -ativar o comportamento eventualmente consistente em limites de partição ou limites de sistema de armazenamento ao utilizar as filas do Azure.
* [Padrão de entidades do índice](#index-entities-pattern) -manter índice entidades tooenable eficiente pesquisas que devolvem apresenta uma lista de entidades.  
* [Padrão de denormalization](#denormalization-pattern) -combinar dados relacionados com o em conjunto na tooenable única entidade tooretrieve Olá todos os dados que precisa com uma ponto único de consulta.  
* [Padrão de séries de dados](#data-series-pattern) -série de dados completa de loja uma única entidade toominimize Olá diversas pedidos que efetuar.  

Para obter informações sobre transações do grupo de entidade, consulte a secção de Olá [entidade grupo transações](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Garantir a estrutura para que as modificações eficiente facilita eficiente consultas
Em muitos casos, uma estrutura eficaz resulta consultas em modificações eficiente, mas deve sempre avaliar se este for o caso de Olá para o seu cenário específico. Alguns dos padrões de Olá na secção de Olá [padrões de conceção de tabela](#table-design-patterns) explicitamente avaliar compromissos entre consultas e modificar as entidades e, sempre deve ter em conta Olá diversas cada tipo de operação.  

Olá seguintes padrões na secção de Olá [padrões de conceção de tabela](#table-design-patterns) compromissos entre conceber consultas eficiente e estruturar para modificação de dados eficiente de endereços:  

* [Padrão de chave composta](#compound-key-pattern) -utilização composta **RowKey** valores tooenable toolookup um cliente relacionadas com a dados com um ponto único de consulta.  
* [Padrão de seguimento de registo](#log-tail-pattern) -obter Olá  *n*  entidades recentemente adicionado tooa partição utilizando um **RowKey** valor ordena na data inversa e ordem de tempo.  

## <a name="encrypting-table-data"></a>Encriptar dados da tabela
Olá biblioteca de clientes de armazenamento de Azure .NET suporta a encriptação de propriedades de entidade para inserção da cadeia e substitua operações. cadeias de Olá encriptado são armazenadas no serviço de Olá como propriedades binárias e estes são convertidos toostrings anterior depois de desencriptação.    

Para as tabelas, além disso toohello política de encriptação, os utilizadores tem de especificar Olá propriedades toobe encriptado. Pode fazê-lo especificando a um atributo [EncryptProperty] (para entidades POCO que derivem de TableEntity) ou um resolvedor de encriptação nas opções de pedido. Um resolvedor de encriptação é um delegado que utiliza uma chave de partição, chave de linha e nome de propriedade e devolve um valor boleano que indica se essa propriedade deve ser encriptada. Durante a encriptação, a biblioteca de clientes do Olá irá utilizar este toodecide informações se uma propriedade deve ser encriptada durante a escrita toohello durante a transmissão. Também fornece delegado Olá para a possibilidade de Olá da lógica em torno da forma como as propriedades são encriptadas. (Por exemplo, se X, então encriptar propriedade um; caso contrário, encriptar propriedades A e B.) Tenha em atenção que é necessário não tooprovide estas informações ao ler ou consultar entidades.

Tenha em atenção que merge não é atualmente suportado. Uma vez que um subconjunto de propriedades poderá ter sido encriptado anteriormente com uma chave diferente, basta intercalação novas propriedades de Olá e atualizar os metadados de Olá resultará na perda de dados. A intercalação um requer efetuar serviço adicional chama entidade pré-existente de Olá tooread do serviço de Olá ou utilizar uma nova chave por propriedade, que não são adequadas por motivos de desempenho.     

Para obter informações sobre a encriptação de dados da tabela, consulte [encriptação do lado do cliente e o Cofre de chaves do Azure para armazenamento do Microsoft Azure](storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Modelling relações
Criação de modelos de domínio é um passo chave na estrutura de Olá dos sistemas complexos. Normalmente, utilizar Olá modelling processo tooidentify entidades e Olá as relações entre-los como uma forma toounderstand Olá domínio de empresa e informam o design de Olá do seu sistema. Esta secção centra-se na forma como pode traduzir alguns dos tipos Olá comuns relação encontrados no domínio modelos toodesigns para Olá serviço tabela. processo de Olá de mapeamento de um tooa lógicas do modelo de dados físico NoSQL com base-modelo de dados é muito diferente da utilizada ao conceber a base de dados relacional. Estrutura de bases de dados relacionais, normalmente, assume um processo de normalização de dados otimizado para minimizando a redundância – e uma capacidade de consulta declarativa que abstracts Olá como implementação como funciona a base de dados de Olá.  

### <a name="one-to-many-relationships"></a>Relações um-para-muitos
Relações um-para-muitos entre objetos de domínio do negócio ocorrerem com muita frequência: por exemplo, um departamento tem muitos colaboradores. Existem várias relações de um-para-muitos de tooimplement formas Olá serviço tabela cada com os profissionais de TI e contras que podem ser relevantes toohello cenário em particular.  

Tenha em conta o exemplo de Olá de uma grande empresa múltiplos national com dezenas de milhares de departamentos e entidades de empregado onde cada departamento tem muitos colaboradores e cada empregado como associados com um departamento específico. Uma abordagem é departamento separado toostore e entidades de empregado como estas:  

![][1]

Este exemplo mostra uma relação um-para-muitos implícita entre tipos de Olá com base no Olá **PartitionKey** valor. Cada departamento pode ter muitos colaboradores.  

Este exemplo mostra também uma entidade de departamento e respetivos entidades de empregado relacionados no Olá mesma partição. Poderia escolher toouse de partições diferente, tabelas ou contas do storage, mesmo para tipos de entidade diferentes Olá.  

Uma abordagem alternativa é toodenormalize as entidades de empregado apenas e arquivo de dados com dados de departamento denormalized conforme mostrado no seguinte exemplo de Olá. Neste cenário específico, esta abordagem denormalized não pode ser Olá melhor se tiver um requisito toobe toochange capaz de Olá os detalhes de um Gestor de departamento porque toodo isto é necessário tooupdate todos os funcionários do departamento de Olá.  

![][2]

Para obter mais informações, consulte Olá [padrão Denormalization](#denormalization-pattern) mais à frente neste guia.  

Olá tabela seguinte resume os profissionais de Olá e contras de cada uma das abordagens Olá descritas acima para armazenar o empregado e entidades de departamento que tenham uma relação um-para-muitos. Deve também considerar a frequência esperada tooperform várias operações: pode ser toohave aceitável uma estrutura que inclui uma operação dispendiosa, se essa operação só acontece com pouca frequência.  

<table>
<tr>
<th>Abordagem</th>
<th>Profissionais de TI</th>
<th>Contras</th>
</tr>
<tr>
<td>Separe os tipos de entidade, a mesma partição, a mesma tabela</td>
<td>
<ul>
<li>Pode atualizar uma entidade de departamento com uma única operação.</li>
<li>Pode utilizar uma consistência de toomaintain EGT se tiver um requisito toomodify uma entidade de departamento sempre que atualizar/insert/eliminar uma entidade do empregado. Por exemplo, se mantém uma contagem de empregado departamentais para cada departamento.</li>
</ul>
</td>
<td>
<ul>
<li>Poderá ser necessário tooretrieve um empregado e uma entidade de departamento para algumas atividades de cliente.</li>
<li>Operações de armazenamento acontecer na Olá mesma partição. Em volumes de transação elevada, isto pode resultar num hotspot.</li>
<li>Não é possível mover um departamento novo de empregado tooa utilizando um EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Tipos de entidade separado, partições diferentes ou tabelas ou contas de armazenamento</td>
<td>
<ul>
<li>Pode atualizar uma entidade do departamento ou uma entidade de empregado com uma única operação.</li>
<li>Em volumes de transação elevada, isto pode ajudar a propagação Olá carga entre mais partições.</li>
</ul>
</td>
<td>
<ul>
<li>Poderá ser necessário tooretrieve um empregado e uma entidade de departamento para algumas atividades de cliente.</li>
<li>Não é possível utilizar EGTs toomaintain consistência quando a atualização/insert/eliminar um empregado e a atualização de um departamento. Por exemplo, ao atualizar uma contagem do empregado na entidade de um departamento.</li>
<li>Não é possível mover um departamento novo de empregado tooa utilizando um EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Denormalize para o tipo de entidade única</td>
<td>
<ul>
<li>Pode obter todas as informações de Olá que terá com um único pedido.</li>
</ul>
</td>
<td>
<ul>
<li>Poderá ser toomaintain dispendiosas consistência se precisar de informações de departamento tooupdate (isto precisaria tooupdate todos os funcionários de Olá de um departamento).</li>
</ul>
</td>
</tr>
</table>

Como optar entre estas opções e em que os profissionais de Olá e contras são mais importantes, depende os cenários de aplicação específica. Por exemplo, com que frequência modificar entidades departamento; todas as consultas de empregado precisa Olá departamentais obter informações adicionais; como fechar tem a limites de escalabilidade toohello no seu partições ou a sua conta de armazenamento?  

### <a name="one-to-one-relationships"></a>Relações um para um
Modelos de domínio podem incluir um para um relações entre entidades. Se precisar de tooimplement uma relação unívoca no Olá serviço tabela, também tem de escolher como toolink Olá duas entidades relacionadas quando precisar de tooretrieve-los ambas. Esta ligação pode ser implícita, com base na Convenção de valores de chave Olá ou explícito armazenando uma ligação na forma de Olá de **PartitionKey** e **RowKey** valores em cada tooits entidade relacionada com entidade. Para ver um debate do se deve armazenar Olá relacionadas com entidades na mesma partição de Olá, consulte a secção Olá [um-para-muitos relações](#one-to-many-relationships).  

Tenha em atenção que também existem considerações de implementação que podem tomar relações um para um tooimplement no serviço de tabela Olá:  

* Processamento de entidades grandes (para obter mais informações, consulte [padrão de entidades grandes](#large-entities-pattern)).  
* Implementar controlos de acesso (para obter mais informações, consulte [controlar o acesso com assinaturas de acesso partilhado](#controlling-access-with-shared-access-signatures)).  

### <a name="join-in-hello-client"></a>Associação no cliente Olá
Embora não existam relações de toomodel formas no Olá serviço tabela, deve não se esqueça que Olá dois prime algumas das razões para utilizar o serviço de tabela Olá são escalabilidade e desempenho. Se encontrar que são modelling muitas relações comprometer desempenho Olá e de escalabilidade da sua solução, deverá solicitar a si que se for necessário toobuild Olá todas as relações de dados para a estrutura da tabela. Pode ser toosimplify capaz de estrutura de Olá e melhorar a escalabilidade de Olá e o desempenho da sua solução se permitir que a aplicação de cliente, efetuar quaisquer associações necessárias.  

Por exemplo, se tiver pequenas tabelas que contêm dados que não se altera com muita frequência, em seguida, pode obter estes dados uma vez e cache-la no cliente Olá. Isto pode evitar e voltas repetidas tooretrieve Olá mesmos dados. Nos exemplos de Olá que iremos consultou neste guia, hello conjunto de departamentos numa organização pequeno é provavelmente toobe pequeno e altere raramente tornando um bom candidato para dados que a aplicação cliente pode transferir uma vez e cache como aspeto dos dados.  

### <a name="inheritance-relationships"></a>Relações de herança
Se a aplicação de cliente utiliza um conjunto de classes que fazem parte de um entidades de negócio de toorepresent de relação de herança, facilmente, pode manter as entidades numa Olá serviço tabela. Por exemplo, poderá ter Olá seguinte conjunto de classes definidas na sua aplicação de cliente onde **pessoa** é uma classe abstracta.

![][3]

Pode manter as instâncias de duas classes concretas Olá no Olá serviço tabela utilizando uma única tabela de pessoa utilizar entidades em que aspeto este:  

![][4]

Para obter mais informações sobre como trabalhar com vários tipos de entidade Olá mesmo tabela no código de cliente, consulte a secção de Olá [trabalhar com tipos de entidade heterogéneos](#working-with-heterogeneous-entity-types) mais à frente neste guia. Esta opção fornece exemplos de como toorecognize Olá o tipo de entidade no código de cliente.  

## <a name="table-design-patterns"></a>Padrões de conceção da tabela
Nas secções anteriores, constatou algumas debates detalhadas sobre como toooptimize a tabela de design para ambos os dados de entidade obter utilizando consultas e para inserir, atualizar e eliminar dados de entidade. Esta secção descreve alguns padrões adequados para utilização com soluções de serviço tabela. Além disso, verá como pode praticamente abordar alguns dos problemas de Olá e compromissos gerados anteriormente neste guia. Olá diagrama a seguir resume as relações de Olá entre padrões diferentes de Olá:  

![][5]

mapa de padrão de Olá acima destaca algumas relações entre padrões (azul) e padrões anti (cor de laranja) que estão documentados neste guia. Obviamente, não existem muitos padrões merecem considerar. Por exemplo, é um dos cenários-chave para o serviço tabela Olá toouse Olá [padrão de vista materializada](https://msdn.microsoft.com/library/azure/dn589782.aspx) de Olá [segregação de responsabilidade de consulta de comando (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) padrão.  

### <a name="intra-partition-secondary-index-pattern"></a>Padrão de índice secundário intra partição
Armazenar várias cópias de cada entidade utilizando diferentes **RowKey** valores (no Olá mesma partição) tooenable rápidos e eficientes pesquisas e ordenação alternada ordena utilizando diferentes **RowKey** valores. Atualizações entre cópias podem ser mantidas consistentes através do EGT.  

#### <a name="context-and-problem"></a>Contexto e do problema
Olá serviço tabela indexa automaticamente entidades utilizando Olá **PartitionKey** e **RowKey** valores. Isto permite que um tooretrieve de aplicação de cliente uma entidade eficiente, utilizando estes valores. Por exemplo, utilizando a estrutura da tabela Olá mostrada abaixo, uma aplicação cliente pode utilizar um tooretrieve de consulta do ponto de uma entidade de empregado individuais utilizando o nome do departamento de Olá e id de empregado Olá (Olá **PartitionKey** e  **RowKey** valores). Um cliente também pode obter entidades ordenadas por id de empregado dentro de cada departamento.

![][6]

Se também pretender toobe capaz de toofind uma entidade de empregado com base no valor de Olá de outra propriedade, tal como endereço de e-mail, tem de utilizar um menos eficiente toofind de análise de partição uma correspondência. Isto acontece porque o serviço de tabela Olá não fornece índices secundários. Além disso, não há toorequest nenhuma opção uma lista dos funcionários ordenados por uma ordem diferente que **RowKey** ordem.  

#### <a name="solution"></a>Solução
toowork à volta de falta de Olá de índices secundários, pode armazenar várias cópias de cada entidade com cada cópia utilizando outro **RowKey** valor. Se armazenar uma entidade com estruturas de Olá mostradas abaixo, pode obter eficientemente entidades de empregado com base no id de endereço ou empregado de correio eletrónico. Olá valores de prefixo para Olá **RowKey**, "empid_" e "email_" permitem-lhe tooquery para um empregado único ou um intervalo de funcionários através da utilização de um intervalo de endereços de e-mail ou os ids de funcionário.  

![][7]

Olá seguir dois critérios de filtro (uma pesquisa por id de empregado e uma pesquisa por endereço de e-mail) ambos especificar ponto consultas:  

* $filter = (PartitionKey eq 'Vendas') e (RowKey eq 'empid_000223')  
* $filter = (PartitionKey eq 'Vendas') e (RowKey eq 'email_jonesj@contoso.com')  

Se a consulta para um intervalo de entidades de empregado, pode especificar um intervalo ordenados por ordem de id de empregado ou um intervalo ordenados por ordem de endereço de e-mail através da consulta para entidades com o prefixo adequado do Olá no Olá **RowKey**.  

* utilizarem de todos os funcionários de Olá no departamento de vendas Olá com um id de empregado Olá intervalo 000100 too000199 toofind: $filter = (PartitionKey eq 'Vendas') e (RowKey ge 'empid_000100') e (RowKey le 'empid_000199')  
* toofind Olá todos os funcionários do departamento de vendas Olá, com um endereço de e-mail a partir Olá letra "a" utilização: $filter = (PartitionKey eq 'Vendas') e (RowKey ge 'email_a') e (RowKey lt 'email_b')  
  
  Tenha em atenção que a sintaxe de filtro de Olá utilizado nos exemplos de Olá acima é de Olá tabela REST API do serviço, para obter mais informações, consulte [entidades de consulta](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* O Table storage é relativamente cheap toouse pelo Olá custo do armazenamento de dados duplicados a sobrecarga não deve ser uma preocupação principal. No entanto, deve sempre avaliar o custo de Olá da estrutura com base nos seus requisitos de armazenamento previsto e adicione apenas consultas de Olá entidades duplicado toosupport que irá executar a aplicação cliente.  
* Porque as entidades de índice secundário Olá são armazenadas no Olá mesma partição como entidades original Olá, deve certificar-se de que não exceda os objetivos de escalabilidade Olá para uma partição individual.  
* Pode manter as entidades duplicadas consistentes entre si utilizando EGTs tooupdate Olá duas cópias da entidade de Olá atomically. Isto implica que deve armazenar todas as cópias de uma entidade no Olá mesma partição. Para obter mais informações, consulte a secção de Olá [utilizando transações de grupo de entidade](#entity-group-transactions).  
* Olá valor utilizado para Olá **RowKey** tem de ser exclusivo para cada entidade. Considere utilizar os valores da chave compostos.  
* Preenchimento valores numéricos na Olá **RowKey** (por exemplo, id de empregado Olá 000223), permite corrigir ordenar e filtrar com base nas maiúscula e limites inferiores.  
* Não é necessariamente necessário tooduplicate todas as propriedades de Olá de entidade. Por exemplo, se hello consultas que o e-mail de entidades de Olá pesquisa utilizando Olá endereços no Olá **RowKey** nunca precisam de idade do empregado Olá, estas entidades podem ter Olá seguir a estrutura:

![][8]

* É melhores normalmente dados duplicados do toostore e certifique-se de que pode obter todos os dados de Olá terá com uma única consulta, que toouse uma consulta toolocate uma entidade outro toolookup Olá necessários e dados.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando a aplicação de cliente precisa de entidades tooretrieve utilizando uma variedade de diferentes chaves, quando o cliente tem de entidades tooretrieve as ordens de ordenação diferente e, em que possa identificar cada entidade utilizando uma variedade de valores exclusivos. No entanto, deve ser se de que não excede os limites de escalabilidade de partição Olá quando estiver a efetuar pesquisas de entidades com diferentes Olá **RowKey** valores.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de índice secundário entre partição](#inter-partition-secondary-index-pattern)
* [Padrão de chave composta](#compound-key-pattern)
* [Transações de grupo de entidade](#entity-group-transactions)
* [Trabalhar com tipos de entidade heterogénea](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Padrão de índice secundário entre partição
Armazenar várias cópias de cada entidade utilizando diferentes **RowKey** valores em partições separadas ou em tabelas separadas tooenable rápidos e eficientes pesquisas êxito e as ordens de ordenação alternada utilizando diferentes **RowKey**valores.  

#### <a name="context-and-problem"></a>Contexto e do problema
Olá serviço tabela indexa automaticamente entidades utilizando Olá **PartitionKey** e **RowKey** valores. Isto permite que um tooretrieve de aplicação de cliente uma entidade eficiente, utilizando estes valores. Por exemplo, utilizando a estrutura da tabela Olá mostrada abaixo, uma aplicação cliente pode utilizar um tooretrieve de consulta do ponto de uma entidade de empregado individuais utilizando o nome do departamento de Olá e id de empregado Olá (Olá **PartitionKey** e  **RowKey** valores). Um cliente também pode obter entidades ordenadas por id de empregado dentro de cada departamento.  

![][9]

Se também pretender toobe capaz de toofind uma entidade de empregado com base no valor de Olá de outra propriedade, tal como endereço de e-mail, tem de utilizar um menos eficiente toofind de análise de partição uma correspondência. Isto acontece porque o serviço de tabela Olá não fornece índices secundários. Além disso, não há toorequest nenhuma opção uma lista dos funcionários ordenados por uma ordem diferente que **RowKey** ordem.  

São prevendo um volume muito elevado de transações em relação a estas entidades e pretende risco de Olá toominimize de Olá serviço tabela, o cliente de limitação.  

#### <a name="solution"></a>Solução
toowork à volta de falta de Olá de índices secundários, pode armazenar várias cópias de cada entidade com cada cópia utilizando diferentes **PartitionKey** e **RowKey** valores. Se armazenar uma entidade com estruturas de Olá mostradas abaixo, pode obter eficientemente entidades de empregado com base no id de endereço ou empregado de correio eletrónico. Olá valores de prefixo para Olá **PartitionKey**, "empid_" e "email_" permitem-lhe tooidentify que índice pretende toouse para uma consulta.  

![][10]

Olá seguir dois critérios de filtro (uma pesquisa por id de empregado e uma pesquisa por endereço de e-mail) ambos especificar ponto consultas:  

* $filter = (PartitionKey eq ' empid_Sales') e (RowKey eq '000223')
* $filter = (PartitionKey eq ' email_Sales') e (RowKey eq 'jonesj@contoso.com')  

Se a consulta para um intervalo de entidades de empregado, pode especificar um intervalo ordenados por ordem de id de empregado ou um intervalo ordenados por ordem de endereço de e-mail através da consulta para entidades com o prefixo adequado do Olá no Olá **RowKey**.  

* toofind Olá todos os empregados na Olá departamento de vendas com um id de empregado no intervalo de Olá **000100** demasiado**000199** ordenado na utilização de ordem de id de empregado: $filter = (PartitionKey eq ' empid_Sales') e (RowKey ge ' 000100') e (RowKey le '000199')  
* toofind todos os funcionários de Olá no departamento de vendas Olá com um endereço de e-mail que começa com "a" ordenado na utilização de ordem de endereço de e-mail: $filter = (PartitionKey eq ' email_Sales') e (RowKey ge "a") e (RowKey lt 'b')  

Tenha em atenção que a sintaxe de filtro de Olá utilizado nos exemplos de Olá acima é de Olá tabela REST API do serviço, para obter mais informações, consulte [entidades de consulta](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Pode manter as entidades duplicadas eventualmente consistente entre si utilizando Olá [padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern) entidades do toomaintain Olá índice principal e secundário.  
* O Table storage é relativamente cheap toouse pelo Olá custo do armazenamento de dados duplicados a sobrecarga não deve ser uma preocupação principal. No entanto, deve sempre avaliar o custo de Olá da estrutura com base nos seus requisitos de armazenamento previsto e adicione apenas consultas de Olá entidades duplicado toosupport que irá executar a aplicação cliente.  
* Olá valor utilizado para Olá **RowKey** tem de ser exclusivo para cada entidade. Considere utilizar os valores da chave compostos.  
* Preenchimento valores numéricos na Olá **RowKey** (por exemplo, id de empregado Olá 000223), permite corrigir ordenar e filtrar com base nas maiúscula e limites inferiores.  
* Não é necessariamente necessário tooduplicate todas as propriedades de Olá de entidade. Por exemplo, se hello consultas que o e-mail de entidades de Olá pesquisa utilizando Olá endereços no Olá **RowKey** nunca precisam de idade do empregado Olá, estas entidades podem ter Olá seguir a estrutura:
  
  ![][11]
* É normalmente uma melhor toostore de dados duplicados e certifique-se de que pode obter todos os dados de Olá que terá com uma única consulta que toouse toolocate de uma consulta para uma entidade utilizando Olá índice secundário e outro toolookup Olá dados necessários no índice principal Olá.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando a aplicação de cliente precisa de entidades tooretrieve utilizando uma variedade de diferentes chaves, quando o cliente tem de entidades tooretrieve as ordens de ordenação diferente e, em que possa identificar cada entidade utilizando uma variedade de valores exclusivos. Utilize este padrão quando pretender que tooavoid exceder os limites de escalabilidade da partição Olá quando estiver a efetuar pesquisas de entidades com diferentes Olá **RowKey** valores.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern)  
* [Padrão de índice secundário intra partição](#intra-partition-secondary-index-pattern)  
* [Padrão de chave composta](#compound-key-pattern)  
* [Transações de grupo de entidade](#entity-group-transactions)  
* [Trabalhar com tipos de entidade heterogénea](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Padrão de transações eventualmente consistente
Ative o comportamento eventualmente consistente em limites de partição ou limites de sistema de armazenamento ao utilizar as filas do Azure.  

#### <a name="context-and-problem"></a>Contexto e do problema
EGTs ativar transações atómicas entre várias entidades que partilham Olá mesma chave de partição. Para o desempenho e as razões de escalabilidade, poderá decidir toostore entidades que têm requisitos de consistência em partições separadas ou num sistema de armazenamento separada: neste cenário, não é possível utilizar EGTs toomaintain consistência. Por exemplo, poderá ter uma consistência eventual do toomaintain requisito entre:  

* Entidades armazenadas no duas partições diferentes na Olá mesmo tabela em tabelas diferentes, em contas de armazenamento diferente.  
* Uma entidade armazenados no Olá serviço tabela e um blob armazenados no Olá serviço Blob.  
* Uma entidade armazenada no serviço de tabela Olá e um ficheiro num sistema de ficheiros.  
* Uma entidade armazenar no Olá serviço tabela ainda indexado com o serviço de pesquisa do Azure Olá.  

#### <a name="solution"></a>Solução
Ao utilizar as filas do Azure, pode implementar uma solução que fornece a consistência eventual entre dois ou mais partições ou sistemas de armazenamento.
tooillustrate esta abordagem, suponha que tem um requisito toobe tooarchive capaz de antigo empregado as entidades. Entidades de empregado antigo raramente são consultadas e devem ser excluídas da todas as atividades que lidam com os empregados atuais. tooimplement este requisito armazenar funcionários ativos no Olá **atual** tabela e funcionários antigos Olá **arquivo** tabela. Arquivar um empregado requer entidade de Olá toodelete do Olá **atual** uma tabela e adicionar Olá entidade toohello **arquivo** tabela, mas não é possível utilizar um tooperform EGT estas duas operações. risco de Olá tooavoid que uma falha faz com que um tooappear de entidade em ambas ou nenhuma das tabelas, a operação de arquivo de Olá tem de ser eventualmente consistente. Olá diagrama sequência seguinte descreve os passos de Olá nesta operação. É fornecido mais detalhadamente para caminhos de exceção na seguinte de texto Olá.  

![][12]

Um cliente inicia uma operação do arquivo de Olá colocando a uma mensagem sobre uma fila do Azure, este empregado tooarchive de exemplo #456. Uma função de trabalho consulta fila Olá para novas mensagens; Quando encontrar um, lê a mensagem de saudação e mantém uma cópia oculta na fila de Olá. função de trabalho de Olá seguinte obtém uma cópia da entidade de Olá de Olá **atual** tabela, insere uma cópia no Olá **arquivo** de tabela e, em seguida, elimina Olá original de Olá **atual**tabela. Por fim, se não existirem erros de nenhum dos passos anteriores Olá, função de trabalho de Olá elimina mensagem de saudação oculto da fila de Olá.  

Neste exemplo, o passo 4 insere empregado Olá na Olá **arquivo** tabela. Foi possível adicionar Olá empregado tooa um blob no Olá serviço Blob ou um ficheiro num sistema de ficheiros.  

#### <a name="recovering-from-failures"></a>Recuperar de falhas
É importante que Olá operações nos passos **4** e **5** tem de ser *idempotent* no caso de função de trabalho de Olá tem de operação de arquivo de Olá toorestart. Se estiver a utilizar o serviço de tabela Olá, para o passo **4** deve utilizar uma operação "Inserir ou substituir"; para o passo **5** deve utilizar um "eliminar se existe" operação na biblioteca de clientes de Olá estiver a utilizar. Se estiver a utilizar outro sistema de armazenamento, tem de utilizar uma operação idempotent adequado.  

Se a função de trabalho de Olá nunca conclui passo **6**, em seguida, depois de uma mensagem de saudação do tempo limite reappears na fila de Olá prontos a Olá trabalho função tootry tooreprocess-lo. função de trabalho de Olá pode verificar o número de vezes uma mensagem na fila de Olá foram lidos e, se necessário, o sinalizador é uma mensagem de "nocivas" para investigação enviando-tooa separar fila. Para obter mais informações sobre a leitura de mensagens de fila e a verificação de Olá anular contagem, consulte [obter mensagens](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Alguns erros dos serviços de tabela e fila Olá erros transitórios e a aplicação cliente deve incluem toohandle de lógica de repetição adequado-los.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Esta solução fornece para isolamento da transação. Por exemplo, um cliente pode ler Olá **atual** e **arquivo** tabelas quando a função de trabalho de Olá foi entre passos **4** e **5**e ver um inconsistente vista dos dados de Olá. Tenha em atenção que os dados de Olá serão consistentes eventualmente.  
* Tem de ser se de que os passos 4 e 5 idempotent na consistência eventual de tooensure de ordem.  
* Pode dimensionar solução Olá utilizando várias filas e instâncias de função de trabalho.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando quiser tooguarantee a consistência eventual entre entidades que existe nas tabelas ou partições diferentes. Pode expandir este consistência eventual do tooensure padrão para operações em serviço de tabela Olá e serviço de Blob Olá e outras origens de dados de armazenamento não do Azure, tais como o sistema de ficheiros de base de dados ou Olá.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Transações de grupo de entidade](#entity-group-transactions)  
* [Intercalação ou substituir](#merge-or-replace)  

> [!NOTE]
> Se o isolamento da transação é importante tooyour solução, deve considerar ao reestruturar o tooenable de tabelas que toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Padrão de entidades de índice
Manter o índice entidades tooenable eficiente pesquisas que devolvem apresenta uma lista de entidades.  

#### <a name="context-and-problem"></a>Contexto e do problema
Olá serviço tabela indexa automaticamente entidades utilizando Olá **PartitionKey** e **RowKey** valores. Isto permite que um tooretrieve de aplicação de cliente uma entidade eficiente, utilizando uma consulta de ponto. Por exemplo, utilizando a estrutura da tabela Olá mostrada abaixo, uma aplicação cliente pode eficientemente obter uma entidade de empregado individuais utilizando o nome do departamento de Olá e id de empregado Olá (Olá **PartitionKey** e **RowKey** ).  

![][13]

Se também pretender tooretrieve capaz de toobe uma lista de entidades de empregado com base no valor de Olá de outra propriedade exclusivos, como o seu apelido, tem de utilizar uma partição menos eficiente toofind correspondências de análise, em vez de utilizar um índice toolook-los diretamente de segurança. Isto acontece porque o serviço de tabela Olá não fornece índices secundários.  

#### <a name="solution"></a>Solução
pesquisa de tooenable por apelido com uma estrutura de entidade Olá mostrado acima, tem de manter as listas de ids de funcionário. Se pretender que as entidades do empregado de Olá tooretrieve com um nome de último específico, como Jones, tem de primeiro localizar lista Olá de ids de empregado para os funcionários com Jones como o seu apelido e, em seguida, obter as entidades de empregado. Existem três opções principais para armazenar as listas de Olá de ids de empregado:  

* Utilize o blob storage.  
* Crie entidades de índice no Olá mesma partição como entidades de empregado Olá.  
* Crie entidades de índice numa partição separada ou tabela.  

<u>Opção #1: Armazenamento de BLOBs de utilização</u>  

Para a primeira opção Olá, pode criar um blob para cada apelido exclusivo e, no arquivo de cada blob uma lista de Olá **PartitionKey** (departamento) e **RowKey** (id de empregado) os valores para os empregados que têm ou pela última vez nome. Quando adicionar ou eliminar um empregado deve certificar-se de que o conteúdo de Olá do blob relevantes Olá é eventualmente consistente com as entidades de empregado Olá.  

<u>Opção #2:</u> Olá, criar entidades de índice na mesma partição  

Para a segunda opção Olá, utilizam as entidades de índice que armazenam Olá dados os seguintes:  

![][14]

Olá **EmployeeIDs** propriedade contém uma lista de ids de empregado para os funcionários com apelido Olá armazenado no Olá **RowKey**.  

Olá passos seguintes descrevem o processo de Olá que deve seguir quando estiver a adicionar um empregado a nova se estiver a utilizar a segunda opção de Olá. Neste exemplo, que estamos a adicionar um empregado com Id 000152 e um apelido Jones no departamento de vendas Olá:  

1. Obter o índice de Olá entidade com uma **PartitionKey** valor "Vendas" e Olá **RowKey** valor "Jones." Guarde Olá ETag de toouse esta entidade no passo 2.  
2. Criar uma transação de grupo de entidade (ou seja, uma operação em lote) insere a entidade de empregado novo Olá (**PartitionKey** valor "Vendas" e **RowKey** valor "000152"), e atualizações Olá entidade índice ( **PartitionKey** valor "Vendas" e **RowKey** valor "Jones") ao adicionar Olá nova empregado id toohello lista no campo de EmployeeIDs Olá. Para mais informações sobre transações do grupo de entidade, consulte [entidade grupo transações](#entity-group-transactions).  
3. Se a transação de grupo de entidade Olá falhar devido a um erro de simultaneidade otimista (alguém tem apenas modificou Olá índice entidade), em seguida, terá de toostart através no passo 1 novamente.  

Pode utilizar um toodeleting abordagem semelhante um empregado se estiver a utilizar a segunda opção de Olá. A alteração do apelido um empregado é ligeiramente mais complexa pois precisará tooexecute uma transação de grupo de entidade que atualiza três entidades: Olá entidade empregado, a entidade de índice de Olá para Apelido antigo Olá e a entidade de índice de Olá para novo nome do último Olá. Tem de obter cada entidade antes de efetuar quaisquer alterações por ordem de valores de ETag tooretrieve Olá que, em seguida, pode utilizar atualizações de Olá tooperform utilizar simultaneidade otimista.  

Olá passos seguintes descrevem o processo de Olá que deve seguir quando for necessário toolook segurança todos os funcionários de Olá com um determinado apelido, um departamento, se estiver a utilizar a segunda opção de Olá. Neste exemplo, vamos são procurar todos os funcionários de Olá com apelido Jones no departamento de vendas Olá:  

1. Obter o índice de Olá entidade com uma **PartitionKey** valor "Vendas" e Olá **RowKey** valor "Jones."  
2. Analisar a lista de Olá de empregado Ids no campo de EmployeeIDs Olá.  
3. Se precisar de informações adicionais sobre cada um destes funcionários (por exemplo, os respetivos endereços de e-mail), cada uma das entidades de empregado Olá utilizando obter **PartitionKey** valor "Vendas" e **RowKey** valores do lista de Olá de funcionários que obteve no passo 2.  

<u>Opção #3:</u> criar entidades de índice numa partição separada ou tabela  

Opção de terceiro Olá, utilizam as entidades de índice que armazenam Olá dados os seguintes:  

![][15]

Olá **EmployeeIDs** propriedade contém uma lista de ids de empregado para os funcionários com apelido Olá armazenado no Olá **RowKey**.  

Com a opção de terceira Olá, não é possível utilizar EGTs toomaintain consistência porque são entidades de índice de Olá numa partição separada da entidades de empregado Olá. Deve certificar-se de que as entidades de índice de Olá são eventualmente consistentes com as entidades de empregado Olá.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Esta solução requer tooretrieve, pelo menos, duas consultas entidades de correspondência: um tooquery Olá índice entidades tooobtain Olá lista de **RowKey** os valores e, em seguida, consulta tooretrieve cada entidade na lista de Olá.  
* Uma vez que uma entidade individuais tem um tamanho máximo de 1 MB, opção #2 e a opção #3 na solução de Olá partem do princípio que lista Olá de ids de empregado para qualquer apelido determinado nunca é maior que 1 MB. Se Olá a lista de ids de empregado está provavelmente toobe superior a 1 MB de tamanho, utilize a opção #1 e armazenar dados do índice Olá no blob storage.  
* Se utilizar a opção #2 (utilizando EGTs toohandle adicionar e eliminar os funcionários e a alteração do apelido um empregado), tem de avaliar se o volume Olá de transações irão abordar os limites de escalabilidade Olá numa determinada partição. Se for este caso de Olá, deve considerar uma solução eventualmente consistente (opção #1 ou opção #3) que utiliza filas toohandle Olá update pedidos e permite-lhe toostore as entidades de índice numa partição separada da entidades de empregado Olá.  
* Opção #2 nesta solução parte do princípio de que pretende que toolook cópias de segurança por apelido dentro de um departamento: por exemplo, pretende tooretrieve uma lista dos empregados com um apelido Jones no departamento de vendas Olá. Se quiser toobe toolook capaz de segurança de todos os funcionários de Olá com um apelido Jones em toda a organização Olá, utilize a opção #1 ou a opção #3.
* Pode implementar uma solução baseada em fila que fornece a consistência eventual (consulte Olá [padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern) para obter mais detalhes).  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando quiser toolookup um conjunto de entidades que todos os partilham um valor de propriedade comuns, como todos os funcionários com apelido Olá Jones.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de chave composta](#compound-key-pattern)  
* [Padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern)  
* [Transações de grupo de entidade](#entity-group-transactions)  
* [Trabalhar com tipos de entidade heterogénea](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Padrão de denormalization
Combinar os dados relacionados num tooenable única entidade tooretrieve Olá todos os dados que precisa com uma ponto único de consulta.  

#### <a name="context-and-problem"></a>Contexto e do problema
Numa base de dados relacional, normalmente normalizar dados tooremove duplicados, resultando em consultas que obtêm dados de várias tabelas. Se normalizar os dados nas tabelas do Azure, tem de se vários ida e volta de Olá cliente toohello servidor tooretrieve os dados relacionados. Por exemplo, com a estrutura da tabela Olá mostrada abaixo, precisam de dois arredondar detalhes de Olá tooretrieve viagens para um departamento: um toofetch Olá departamento entidade que inclui o id do Gestor de Olá e os detalhes, em seguida, outro pedido toofetch Olá do Gestor num empregado entidade.  

![][16]

#### <a name="solution"></a>Solução
Em vez de armazenar dados de Olá em duas entidades separadas, denormalize dados Olá e manter uma cópia dos detalhes do Gestor de Olá na entidade de departamento Olá. Por exemplo:  

![][17]

Com entidades de departamento armazenadas com estas propriedades, agora pode obter todos os detalhes de Olá que terá sobre um departamento utilizando uma consulta de ponto.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Há alguns custos de sobrecarga associados ao armazenamento alguns dados duas vezes. Olá desempenho benefício (resultante do serviço de armazenamento de toohello pedidos menos), normalmente, prevalece sobre aumento marginal Olá os custos de armazenamento (e este custo é parcialmente deslocamento por uma redução do número de Olá de transações requerem os detalhes de Olá toofetch de um departamento).  
* Tem de manter consistência Olá de entidades de dois Olá que armazenam informações sobre os gestores. Pode processar problema de consistência Olá utilizando EGTs tooupdate várias entidades numa única transação atómica: neste caso, Olá departamento entidade e entidade de empregado Olá para Gestor de departamento Olá são armazenados no Olá mesma partição.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando precisar de toolook das informações relacionadas com frequência. Este padrão reduz o número de Olá das consultas, que o cliente tem de se dados de Olá tooretrieve requer.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de chave composta](#compound-key-pattern)  
* [Transações de grupo de entidade](#entity-group-transactions)  
* [Trabalhar com tipos de entidade heterogénea](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Padrão de chave composta
Utilize composta **RowKey** valores tooenable toolookup um cliente relacionadas com a dados com um ponto único de consulta.  

#### <a name="context-and-problem"></a>Contexto e do problema
Base de dados relacional, é bastante natural toouse associações em consultas tooreturn relacionadas com partes do cliente de toohello dados numa única consulta. Por exemplo, poderá utilizar toolook de id de empregado Olá uma lista de entidades relacionadas que contenham o desempenho e reveja os dados para esse empregado.  

Suponha que estão a armazenar as entidades de empregado no serviço de tabela Olá utilizando Olá seguir a estrutura:  

![][18]

Também precisa de dados históricos toostore referentes tooreviews e desempenho para cada empregado de Olá ano trabalhou para a sua organização e precisa tooaccess capaz de toobe estas informações por ano. Uma opção é toocreate outra tabela que armazena as entidades com Olá seguir a estrutura:  

![][19]

Tenha em atenção que, com esta abordagem, pode decidir tooduplicate algumas informações (por exemplo, o nome próprio e apelido) no Olá nova entidade tooenable tooretrieve os dados com um único pedido. No entanto, não é possível manter a consistência forte porque não é possível utilizar um EGT tooupdate Olá duas entidades atomically.  

#### <a name="solution"></a>Solução
Armazene um novo tipo de entidade na tabela original com entidades Olá seguir a estrutura:  

![][20]

Repare como Olá **RowKey** é agora uma chave composta constituída por id de empregado Olá e ano de Olá Olá revisão de dados de que permite-lhe tooretrieve Olá desempenho do empregado e analisar dados com um único pedido de uma única entidade.  

Olá exemplo a seguir descreve como pode obter todos os dados de revisão Olá para um funcionário específico (por exemplo, um empregado 000123 no departamento de vendas Olá):  

$filter = (PartitionKey eq 'Vendas') e (RowKey ge 'empid_000123') e (RowKey lt 'empid_000124') & $select = RowKey, Gestor de classificação, ponto a ponto de classificação, comentários  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Deve utilizar um caráter de separação adequado que torna mais fácil tooparse Olá **RowKey** valor: por exemplo, **000123_2012**.  
* Também estão a armazenar esta entidade no Olá mesma partição como outras entidades que contêm dados relacionados de Olá empregado mesmo, o que significa que pode utilizar EGTs toomaintain a consistência forte.
* Deve considerar a frequência irá consultar Olá dados toodetermine se este padrão é adequado.  Por exemplo, se forem aceder ao hello com pouca frequência a data de revisão e Olá dados empregado principal, muitas vezes, que deve mantê-las como entidades separadas.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando precisar de toostore um ou mais relacionadas com entidades essa consulta frequentemente.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Transações de grupo de entidade](#entity-group-transactions)  
* [Trabalhar com tipos de entidade heterogénea](#working-with-heterogeneous-entity-types)  
* [Padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Padrão de seguimento de registo
Obter Olá  *n*  entidades recentemente adicionado tooa partição utilizando um **RowKey** valor ordena na data inversa e ordem de tempo.  

#### <a name="context-and-problem"></a>Contexto e do problema
Um requisito comum é tooretrieve capaz de ser entidades Olá criado mais recentemente, por exemplo Olá dez mais recentes despesa afirmações submetidas por um funcionário. Suporte de consulta de tabela um **$top** Olá tooreturn de operação de consulta primeiro  *n*  entidades de um conjunto: não há nenhuma consulta equivalente operação tooreturn Olá últimas n entidades com um conjunto.  

#### <a name="solution"></a>Solução
Arquivo Olá entidades utilizando uma **RowKey** que naturalmente ordena no inversa data/hora ordem utilizando, para a entrada mais recente Olá é sempre Olá um primeiro na tabela de Olá.  

Por exemplo, tooretrieve capaz de toobe Olá dez afirmações despesa mais recentes submetidas por um empregado, pode utilizar um valor de escala inversa derivado Olá data/hora atual. Olá c# código exemplo seguinte mostra uma forma toocreate um valor de "inverted ticks" adequado para uma **RowKey** que ordena de Olá toohello mais recente mais antigo:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Pode voltar valor de tempo de data toohello utilizando Olá seguinte código:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

consulta de tabela Olá tem o seguinte aspeto:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Deve preencher o valor de escala inversa Olá com líderes zeros valor de cadeia de Olá tooensure ordena conforme esperado.  
* Tem de ser em consideração os objetivos de escalabilidade Olá ao nível de Olá de uma partição. Seja cuidadoso não criar partições do ponto ativo.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando precisar de entidades tooaccess por ordem inversa de data/hora ou quando for necessário tooaccess Olá mais recentemente adicionado entidades.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Preceder / acrescentar anti padrão](#prepend-append-anti-pattern)  
* [Obter entidades](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Padrão de eliminação de um volume elevado
Ativar a eliminação de um grande volume de entidades Olá armazenando todas as entidades de Olá para eliminação em simultâneo na sua própria tabela separada; eliminar entidades Olá, eliminando tabela Olá.  

#### <a name="context-and-problem"></a>Contexto e do problema
Muitas aplicações eliminar dados antigos que já não necessita de aplicação de cliente disponíveis tooa toobe ou essa aplicação Olá tem arquivados tooanother média de armazenamento. Normalmente, identificar esses dados por uma data: por exemplo, tiver registos toodelete requisito de todos os pedidos de início de sessão que são mais de 60 dias.  

Um design de possíveis é toouse Olá data e hora pedido de início de sessão de Olá no Olá **RowKey**:  

![][21]

Esta abordagem evita a hotspots de partição porque a aplicação Olá pode inserir e eliminar entidades de início de sessão para cada utilizador numa partição separada. No entanto, esta abordagem poderá ser dispendiosa e demorada se tiver um grande número de entidades porque tem primeiro tooperform uma tabela de análise na ordem tooidentify toodelete de entidades de Olá todas as e, em seguida, tem de eliminar cada entidade antiga. Tenha em atenção que pode reduzir o número Olá de ida e volta toohello servidor necessário toodelete Olá antigo entidades por vários pedidos de eliminação de criação de batches para EGTs.  

#### <a name="solution"></a>Solução
Utilize uma tabela em separado para cada dia de início de sessão falhadas. Pode utilizar o design de entidade Olá acima tooavoid hotspots quando são inserir entidades e eliminar entidades antigas agora é simplesmente uma pergunta de eliminação de uma tabela de todos os dias (uma operação de armazenamento única) em vez de localizar e eliminar centenas e milhares de entidades de início de sessão individuais todos os dias.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* A estrutura suporta outras formas a aplicação utilizará dados Olá como procurar entidades específicas, com outros dados ou gerar agregam informações de ligação?  
* O design evitar frequente oportunidades quando são inserir novas entidades?  
* Esperar um atraso se quiser tooreuse Olá mesmo depois de eliminar o nome da tabela. É melhor tooalways utilize tabela exclusivo nomes.  
* Espere alguns limitação ao primeiro utilizar uma nova tabela enquanto Olá serviço tabela aprende padrões de acesso de Olá e distribui as partições de Olá nós. Deve considerar a frequência tem de toocreate novas tabelas.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão se tiver um grande volume de entidades que tem de eliminar em Olá mesmo tempo.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Transações de grupo de entidade](#entity-group-transactions)
* [A modificação de entidades](#modifying-entities)  

### <a name="data-series-pattern"></a>Padrão de séries de dados
Série de dados completa de loja uma única entidade toominimize Olá diversas pedidos que efetuar.  

#### <a name="context-and-problem"></a>Contexto e do problema
Um cenário comum é para uma aplicação toostore uma série de dados que, normalmente, necessita de tooretrieve ao mesmo tempo. Por exemplo, a aplicação poderá registar como muitas mensagens de MI cada empregado envia a cada hora e, em seguida, utilize este tooplot informações quantidade de mensagens enviada a cada utilizador Olá 24 horas anteriores. Uma estrutura poderá ser toostore 24 entidades para cada empregado:  

![][22]

Com esta conceção, pode localizar e atualizar Olá tooupdate de entidade para cada empregado sempre que a aplicação de Olá tem o valor de contagem de mensagens de Olá tooupdate facilmente. No entanto, tooretrieve Olá informações tooplot um gráfico de atividade de Olá para Olá anterior a 24 horas, tem de obter 24 entidades.  

#### <a name="solution"></a>Solução
Utilize Olá seguir a estrutura com uma contagem de mensagens de Olá de toostore propriedade separado para cada hora:  

![][23]

Com esta conceção, pode utilizar uma contagem de mensagens hello de tooupdate de operação de intercalação do empregado para uma hora específica. Agora, pode obter todas as informações de Olá precisa de gráfico de Olá tooplot utilizando um pedido para uma única entidade.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Se a série de dados completo não se ajusta uma única entidade (uma entidade pode ter propriedades de too252), utilize um arquivo de dados alternativos, tais como um blob.  
* Se tiver vários clientes em simultâneo a atualizar uma entidade, terá de toouse Olá **ETag** simultaneidade otimista tooimplement. Se tiver muitos clientes, pode deparar-se elevada contenção.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando precisar tooupdate e obter uma série de dados associada a uma entidade individuais.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de entidades grandes](#large-entities-pattern)  
* [Intercalação ou substituir](#merge-or-replace)  
* [Padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern) (se estiver a armazenar série de dados de Olá num blob)  

### <a name="wide-entities-pattern"></a>Padrão de entidades Wide
Utilize várias entidades lógico de toostore entidades físicas com mais do que 252 propriedades.  

#### <a name="context-and-problem"></a>Contexto e do problema
Uma entidade individual pode ter mais do que 252 propriedades (excluindo as propriedades de sistema obrigatório Olá) e não é possível armazenar mais de 1 MB de dados no total. Numa base de dados relacional, normalmente, obterá arredondar os limites de tamanho de Olá de uma linha ao adicionar uma nova tabela e impor uma relação de 1 para 1 entre eles.  

#### <a name="solution"></a>Solução
Utilizar o serviço de tabela Olá, pode armazenar várias entidades toorepresent um objeto de empresas de grandes dimensões única com mais do que 252 propriedades. Por exemplo, se quiser toostore uma contagem do número de Olá de mensagens de MI enviadas por cada funcionário para Olá últimos 365 dias, pode utilizar Olá estrutura que utiliza duas entidades com diferentes esquemas os seguintes:  

![][24]

Se precisar de toomake uma alteração que requer a atualização de ambos os tookeep entidades-los sincronizados entre si pode utilizar um EGT. Caso contrário, pode utilizar uma contagem de mensagens do intercalação única operação tooupdate Olá num dia específico. tooretrieve todas hello dados para um empregado individuais, tem de obter as entidades, o que pode fazer com dois pedidos eficiente que utilizam ambos um **PartitionKey** e um **RowKey** valor.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Obter uma entidade lógica completa envolve transações de armazenamento, pelo menos, duas: entidade física um tooretrieve.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando necessidade toostore entidades cujo tamanho ou o número de propriedades excede os limites de Olá para uma entidade individuais em Olá serviço tabela.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Transações de grupo de entidade](#entity-group-transactions)
* [Intercalação ou substituir](#merge-or-replace)

### <a name="large-entities-pattern"></a>Padrão de entidades grandes
Utilize os valores de propriedade grande de toostore de armazenamento de Blobs.  

#### <a name="context-and-problem"></a>Contexto e do problema
Uma entidade individuais não é possível armazenar mais de 1 MB de dados no total. Se uma ou várias das suas propriedades armazenarem valores causam este valor de tamanho total do Olá dos seus tooexceed de entidade, não é possível armazenar a entidade todo Olá no Olá serviço tabela.  

#### <a name="solution"></a>Solução
Se a entidade exceder 1 MB de tamanho, porque uma ou mais propriedades contém uma grande quantidade de dados, pode armazenar dados numa Olá serviço Blob e, em seguida, armazenar endereço Olá do blob Olá numa propriedade na entidade de Olá. Por exemplo, pode armazenar fotografia de Olá de um empregado no blob storage e armazenar uma fotografia de toohello de ligação no Olá **fotografia** propriedade de entidade empregado:  

![][25]

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* toomaintain a consistência eventual entre entidade Olá no Olá serviço tabela e dados Olá Olá serviço Blob, utilize Olá [padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern) toomaintain as entidades.
* Obter uma entidade completa envolve a, pelo menos, dois transações de armazenamento: uma entidade de Olá tooretrieve e Olá um tooretrieve blob de dados.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Utilize este padrão quando necessita de entidades toostore cujo tamanho excede os limites de Olá para uma entidade no serviço de tabela Olá individuais.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de transações eventualmente consistente](#eventually-consistent-transactions-pattern)  
* [Padrão de entidades Wide](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Preceder/acrescentar anti padrão
Aumentar a escalabilidade quando tiver um grande volume de inserções pelo Olá inserções entre várias partições.  

#### <a name="context-and-problem"></a>Contexto e do problema
Prefixação ou acrescentando entidades de tooyour armazenado entidades normalmente resulta numa aplicação Olá adicionar novas entidades toohello primeiro ou último partição de uma sequência de partições. Neste caso, todos Olá inserções em qualquer momento são executadas no Olá insere mesma partição, criar um hotspot que impede que o serviço de tabela Olá balanceamento de carga entre múltiplos nós e, possivelmente, fazendo com que a escalabilidade de Olá toohit aplicação destinos para a partição. Por exemplo, se tiver uma aplicação que aceder a recursos de rede de registos e pelos funcionários, em seguida, uma estrutura de entidade, conforme mostrado abaixo pode resultar na partição de hora atual se tornar um hotspot se volume Olá de transações atingir o destino de escalabilidade Olá para Olá uma partição individual:  

![][26]

#### <a name="solution"></a>Solução
Olá seguinte estrutura de entidade alternativa evita um hotspot em qualquer partição específica como eventos de registos de aplicação Olá:  

![][27]

Tenha em atenção com este exemplo como ambos Olá **PartitionKey** e **RowKey** são chaves compostas. Olá **PartitionKey** utiliza o departamento de Olá e o registo de Olá de toodistribute de id de empregado em várias partições.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá seguintes pontos ao decidir como tooimplement este padrão:  

* Does Olá alternativa estrutura chave que evita a criar partições frequente no inserções de forma eficiente suporte Olá consultas torna a sua aplicação cliente?  
* O volume previsto de transações significa que são tooreach provável metas de escalabilidade Olá para uma partição individual e limitadas pelo serviço de armazenamento Olá?  

#### <a name="when-toouse-this-pattern"></a>Quando toouse este padrão
Evite padrão anti de preceder/acrescentar Olá quando o volume de transações é provavelmente tooresult na limitação pelo serviço de armazenamento Olá ao aceder a uma partição de acesso frequente.  

#### <a name="related-patterns-and-guidance"></a>Padrões relacionados e as orientações
Olá padrões e orientações seguintes também podem ser relevantes ao implementar este padrão:  

* [Padrão de chave composta](#compound-key-pattern)  
* [Padrão de seguimento de registo](#log-tail-pattern)  
* [A modificação de entidades](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Padrão de anti de dados do registo
Normalmente, deve utilizar Olá serviço Blob em vez de Olá dados de registo do serviço toostore da tabela.  

#### <a name="context-and-problem"></a>Contexto e do problema
Caso de utilização de um comuns para dados de registo são tooretrieve uma seleção de entradas de registo de um intervalo de data/hora específico: por exemplo, pretende toofind Olá, todas as mensagens de erro e críticas que a aplicação, registada entre 15:04 e 15:06 numa data específica. Não pretende toouse Olá data e hora as partições de Olá mensagem de registo do Olá toodetermine Guardar entidades de registo para: que resultados numa partição frequente porque em qualquer momento, todas as entidades de registo de Olá irão partilhar Olá mesmo **PartitionKey** valor (consulte a secção de Olá [Prepend/acrescentar anti padrão](#prepend-append-anti-pattern)). Por exemplo, Olá seguir o esquema de entidade de uma mensagem de registo resulta numa partição frequente porque a aplicação Olá escreve todas as mensagens de registo toohello partição para Olá atual data e hora:  

![][28]

Neste exemplo, Olá **RowKey** inclui Olá data e hora tooensure de mensagem de registo de Olá que as mensagens do registo são armazenadas ordenados por ordem de data/hora e inclui um id de mensagem no caso de várias mensagens de registo partilham Olá mesmo data e hora.  

Outra abordagem é toouse um **PartitionKey** que garante que a aplicação Olá escreve mensagens através de um intervalo de partições. Por exemplo, se a origem Olá Olá da mensagem do registo fornece uma forma toodistribute mensagens através de várias partições, pode utilizar Olá esquema de entidade a seguir:  

![][29]

No entanto, o problema de Olá com este esquema é essa tooretrieve Olá todas as mensagens do registo para um intervalo de tempo específico tem de procurar cada partição na tabela de Olá.

#### <a name="solution"></a>Solução
Olá anterior secção Olá realçado problema de tentar toouse Olá entradas de registo de toostore de serviço tabela e sugerida dois, unsatisfactory, designs. Uma solução guiada tooa frequente a partição com o risco de Olá de fraco desempenho ao escrever as mensagens do registo; Olá outra solução resultou no desempenho das consultas fraco devido a Olá requisito tooscan cada partição num Olá tabela tooretrieve as mensagens do registo para um intervalo de tempo específico. O blob storage oferece a melhor solução para este tipo de cenário e este é o Azure como armazenamento arquivos Olá registo dados de análise recolhe.  

Esta secção descreve como o análise de armazenamento armazena dados de registo no armazenamento de BLOBs, como uma ilustração destas abordagem toostoring de dados de que consulta normalmente por intervalo.  

Análise de armazenamento armazena as mensagens do registo num formato delimitado em vários blobs. formato delimitado Olá torna mais fácil para um cliente dados da aplicação tooparse Olá na mensagem do registo de saudação.  

Análise de armazenamento utiliza uma convenção de nomenclatura de blobs que lhe permite toolocate Olá blob (ou blobs) que contém mensagens hello do registo para o qual esteja a pesquisar. Por exemplo, um blob com o nome "queue/2014/07/31/1800/000001.log" contém mensagens de registo relacionados com o serviço de fila toohello para hora Olá começando 18:00 em 31 de Julho de 2014. Olá "000001" indica que é Olá primeiro ficheiro de registo para este período. Análise de armazenamento também regista Olá carimbos de Olá primeiro e último registar mensagens armazenadas no ficheiro de Olá como parte dos metadados do blob Olá. Olá API para ativa de armazenamento de BLOBs localizar os blobs num contentor com base no prefixo de nome: toolocate todos os blobs Olá que contêm a fila de registo de dados para a hora de Olá começando 18:00, pode utilizar Olá prefixo "fila/2014/07/31/1800."  

Análise de armazenamento coloca internamente mensagens de registo e, em seguida, atualiza periodicamente blob adequado Olá ou cria uma nova com o batch mais recente do Olá de entradas de registo. Isto reduz o número de Olá de gravações tem de efetuar toohello serviço de blob.  

Se estiver a implementar uma solução semelhante na sua própria aplicação, tem de considerar como toomanage Olá compromisso entre fiabilidade (escrever cada armazenamento de tooblob de entrada de registo como ocorre) e o custo e escalabilidade (colocação em memória intermédia atualizações na sua aplicação e escrever tooblob armazenamento em lotes).  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá ao decidir como toostore registar dados os seguintes pontos:  

* Se criar um design de tabela que evita partições frequente potenciais, pode constatar que não é possível aceder os dados de registo de forma eficiente.  
* tooprocess registar dados, um cliente precisar frequentemente tooload vários registos.  
* Apesar dos dados de registo, muitas vezes, estão estruturados, armazenamento de blob pode ser a melhor solução.  

### <a name="implementation-considerations"></a>Considerações de implementação
Esta secção descreve algumas das considerações de Olá toobear em consideração quando implementar padrões Olá descritos nas secções anteriores Olá. Na maioria desta secção utiliza exemplos escritos em c# que utilizam Olá biblioteca de clientes de armazenamento (versão 4.3.0 momento Olá da escrita).  

### <a name="retrieving-entities"></a>Obter entidades
Tal como explicado na secção de Olá [estrutura para consultar](#design-for-querying), consulta mais eficiente Olá é uma consulta de ponto. No entanto, em alguns cenários poderá ser necessário tooretrieve várias entidades. Esta secção descreve algumas entidades de tooretrieving abordagens comuns utilizando Olá biblioteca de clientes de armazenamento.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Executar uma consulta de ponto utilizando Olá biblioteca de clientes de armazenamento
Olá tooexecute da forma mais fácil uma consulta de ponto é toouse Olá **obter** operação de tabela, conforme mostrado no Olá seguinte fragmento de código c# que obtém uma entidade com uma **PartitionKey** de valor "vendas" e um  **RowKey** do valor "212":  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Repare como neste exemplo espera entidade Olá obtém toobe do tipo **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>A obter várias entidades com LINQ
Pode obter várias entidades utilizando LINQ com bibliotecas de cliente de armazenamento e especificar uma consulta com um **onde** cláusula. tooavoid uma análise da tabela, sempre deve incluir Olá **PartitionKey** valor olá onde cláusula e se for possível Olá **RowKey** valor tooavoid análises de tabela e partição. Olá serviço tabela suporta um conjunto limitado de comparação operadores (maior, maior ou igual, menos a, menor que ou igual, igual e não igual) toouse olá onde cláusula. Olá seguinte fragmento de código da c# localiza todos os funcionários de Olá cuja última começa de nome com "B" (partindo do princípio que Olá **RowKey** arquivos Olá apelido) no departamento de vendas Olá (partindo do princípio de Olá **PartitionKey** armazena o nome do departamento de Olá):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Repare como a consulta de Olá especifica ambos um **RowKey** e um **PartitionKey** tooensure um melhor desempenho.  

Olá exemplo de código seguinte mostra a funcionalidade equivalente com a API fluent Olá (para obter mais informações sobre as APIs fluent em geral, consulte o artigo [melhores práticas para criar uma API Fluent](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> Olá exemplo nests vários **CombineFilters** métodos tooinclude Olá três condições de filtro.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>A obter grande número de entidades de uma consulta
Uma consulta ideal devolve uma entidade individuais com base num **PartitionKey** valor e um **RowKey** valor. No entanto, em alguns cenários pode ter um requisito tooreturn muitas entidades de Olá mesma partição ou mesmo a partir de várias partições.  

Sempre totalmente deve testar o desempenho de Olá da sua aplicação no tais cenários.  

Uma consulta ao serviço de tabela Olá pode devolver um máximo de 1000 entidades em simultâneo e poderá ser executada para um máximo de cinco segundos. Se hello conjunto de resultados contém mais de 1000 entidades, se a consulta de Olá não foi concluído dentro de cinco segundos, ou se a consulta de Olá atravesse limites de partição Olá, Olá serviço tabela devolve um tooenable de token de continuação Olá hello do cliente aplicação toorequest seguinte conjunto de entidades. Para obter mais informações sobre como continuação tokens trabalho, consulte [tempo limite de consulta e paginação](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Se estiver a utilizar Olá biblioteca de clientes de armazenamento, pode processar de automaticamente tokens de continuação para si como devolve entidades de Olá serviço tabela. Olá seguinte c# exemplo de código utilizando automaticamente Olá biblioteca de clientes de armazenamento processa tokens de continuação se o serviço de tabela Olá devolve-os numa resposta:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

Olá seguinte código c# processa tokens de continuação explicitamente:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Utilizando os tokens de continuação explicitamente, pode controlar quando a aplicação obtém segmento seguinte do Olá de dados. Por exemplo, se a aplicação de cliente permite que os utilizadores toopage através de entidades de Olá armazenados numa tabela, um utilizador pode decidir não toopage através de todas as entidades de Olá obtidos pela consulta Olá para a aplicação apenas utilizará um Olá token tooretrieve de continuação seguinte segmento quando o utilizador Olá tinha concluído paginação através de todas as entidades de Olá no segmento atual Olá. Esta abordagem tem várias vantagens:  

* Permite-lhe quantidade de Olá toolimit de tooretrieve de dados do serviço tabela de Olá e mover rede Olá.  
* Permite-lhe tooperform assíncrono e/s no .NET.  
* Permite-lhe armazenamento de token toopersistent de continuação de Olá tooserialize para poder continuar no evento Olá de uma falha de aplicação.  

> [!NOTE]
> Um token de continuação normalmente devolve um segmento de 1.000 entidades, embora possam ser menos. Este é também caso Olá se limite Olá número de entradas de uma consulta devolve utilizando **demorar** tooreturn Olá primeiro n entidades que correspondam aos critérios de pesquisa: serviço de tabela Olá pode devolver um segmento que contenham menos de entidades n ao longo com um tooenable de token de continuação tooretrieve Olá entidades restantes.  
> 
> 

Olá c# código seguinte mostra como foi devolvido um número de entidades toomodify Olá dentro de um segmento de:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Projecção do lado do servidor
Uma única entidade pode ter propriedades de too255 e ser segurança too1 MB de tamanho. Quando consultar a tabela de Olá e obter entidades, pode não necessitar de todas as propriedades de Olá e pode evitar desnecessariamente a transferência de dados (toohelp reduzir a latência e o custo). Pode utilizar propriedades de Olá apenas de tootransfer de projeção do lado do servidor que é necessário. Olá exemplo seguinte é obtém apenas Olá **E-Mail** propriedade (juntamente com **PartitionKey**, **RowKey**, **Timestamp**e  **ETag**) de entidades de Olá selecionadas por consulta Olá.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Repare como Olá **RowKey** valor está disponível, apesar de não estava incluído na lista de Olá de tooretrieve de propriedades.  

### <a name="modifying-entities"></a>A modificação de entidades
Olá biblioteca de clientes de armazenamento permite toomodify as entidades armazenadas no serviço de tabela de Olá por inserir, eliminar e entidades de atualização. Pode utilizar EGTs toobatch vários insert, update e as operações delete em conjunto tooreduce Olá diversas ida e volta necessário e melhorar o desempenho de Olá da sua solução.  

Tenha em atenção de que exceções acionadas quando Olá biblioteca de clientes de armazenamento executa um EGT normalmente incluem o índice de Olá da entidade de Olá que causou Olá batch toofail. Isto é útil quando está a depurar código que utiliza EGTs.  

Deve também considerar como a estrutura afeta a forma como a aplicação cliente processa as operações de simultaneidade e atualização.  

#### <a name="managing-concurrency"></a>Gerir a simultaneidade
Por predefinição, o serviço de tabela Olá implementa otimista simultaneidade verifica ao nível de Olá de entidades individuais para **inserir**, **intercalar**, e **eliminar** operações, Embora seja possível para um hello do cliente tooforce tabela serviço toobypass estas verificações. Para obter mais informações sobre como o serviço de tabela Olá gere a simultaneidade, consulte [gerir simultaneidade no armazenamento do Microsoft Azure](storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Intercalação ou substituir
Olá **substituir** método de Olá **TableOperation** classe substitui sempre entidade completa de Olá no Olá serviço tabela. Se não incluir uma propriedade no pedido de Olá quando essa propriedade existe na entidade de Olá armazenado, o pedido Olá remove a que a propriedade de Olá armazenados entidade. A menos que queira tooremove uma propriedade explicitamente a partir de uma entidade armazenada, tem de incluir cada propriedade no pedido de Olá.  

Pode utilizar Olá **intercalar** método de Olá **TableOperation** quantidade de Olá tooreduce classe de dados a enviar serviço de tabela toohello quando quiser tooupdate uma entidade. Olá **intercalar** método substitui quaisquer propriedades de entidade Olá armazenado com valores de propriedade de entidade Olá incluídas no pedido de Olá, mas mantém intactos quaisquer propriedades no Olá armazenados entidade que não estão incluídos no pedido de Olá. Isto é útil se tiver entidades grandes e só precisa de tooupdate um pequeno número de propriedades de um pedido.  

> [!NOTE]
> Olá **substituir** e **intercalar** métodos falharem se Olá entidade não existe. Como alternativa, pode utilizar Olá **InsertOrReplace** e **InsertOrMerge** métodos que se não existir, crie uma nova entidade.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Trabalhar com tipos de entidade heterogénea
Olá serviço tabela é um *sem esquema* arquivo de tabela, que significa que uma única tabela pode armazenar as entidades de vários tipos de fornecer uma grande flexibilidade na sua estrutura. Olá exemplo a seguir ilustra uma armazenar empregado e entidades do departamento de tabela:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Tenha em atenção que cada entidade ainda tem de ter **PartitionKey**, **RowKey**, e **Timestamp** valores, mas pode ter qualquer conjunto de propriedades. Além disso, não há nada tooindicate Olá tipo de entidade, exceto se optar por toostore algures essas informações. Existem duas opções para identificar o tipo de entidade Olá:  

* Preceder toohello de tipo de entidade Olá **RowKey** (ou possivelmente Olá **PartitionKey**). Por exemplo, **EMPLOYEE_000123** ou **DEPARTMENT_SALES** como **RowKey** valores.  
* Utilize um propriedade de diferentes toorecord Olá tipo de entidade conforme mostrado na tabela de Olá abaixo.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td>Empregado</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td>Empregado</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Departamento</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nome próprio</th>
<th>Apelido</th>
<th>Idade</th>
<th>E-mail</th>
</tr>
<tr>
<td>Empregado</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Olá primeira opção, prefixação toohello de tipo de entidade Olá **RowKey**, é útil se existir a possibilidade de que duas entidades de diferentes tipos de poderão ter Olá mesmo valor de chave. -Grupos de entidades de Olá mesmo tipo em conjunto na partição de Olá também.  

Olá técnicas abordadas nesta secção são especialmente relevantes toohello debate [relações de herança](#inheritance-relationships) anteriormente neste guia na secção de Olá [Modelling relações](#modelling-relationships).  

> [!NOTE]
> Deve incluir um número de versão no Olá tipo valor tooenable cliente aplicações tooevolve POCO objetos de entidade e trabalhar com versões diferentes.  
> 
> 

Olá resto esta secção descreve algumas das funcionalidades de Olá no Olá biblioteca de clientes de armazenamento que o facilitam a trabalhar com vários tipos de entidade Olá mesma tabela.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Obter os tipos de entidade heterogénea
Se estiver a utilizar Olá biblioteca de clientes de armazenamento, tem três opções para trabalhar com diversos tipos de entidade.  

Se sabe que o tipo de Olá da entidade de Olá armazenado com específico **RowKey** e **PartitionKey** valores, em seguida, pode especificar o tipo de entidade Olá ao obter a entidade de Olá, conforme ilustrado nos exemplos de Olá dois anterior que obter entidades de tipo **EmployeeEntity**: [executar uma consulta de ponto utilizando Olá biblioteca de clientes de armazenamento](#executing-a-point-query-using-the-storage-client-library) e [obter várias entidades com LINQ](#retrieving-multiple-entities-using-linq).  

segunda opção de Olá é toouse Olá **DynamicTableEntity** tipo (uma matriz de propriedades) em vez de um tipo de entidade POCO concreto (esta opção pode também melhorar o desempenho porque não há nenhum tooserialize necessidade e anular a serialização da entidade de Olá demasiado. Tipos de redes). Olá seguinte código c# potencialmente obtém várias entidades de diferentes tipos de tabela de Olá, mas devolve todas as entidades como **DynamicTableEntity** instâncias. Em seguida, utiliza Olá **EntityType** toodetermine Olá o tipo de propriedade de cada entidade:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Tenha em atenção que tooretrieve outras propriedades tem de utilizar Olá **TryGetValue** método no Olá **propriedades** propriedade Olá **DynamicTableEntity** classe.  

Uma terceira opção está toocombine utilizando Olá **DynamicTableEntity** tipo e um **EntityResolver** instância. Isto permite que tooresolve toomultiple POCO tipos Olá mesma consulta. Neste exemplo, Olá **EntityResolver** delegado está a utilizar Olá **EntityType** propriedade toodistinguish entre Olá dois os tipos de entidade que Olá consulta devolve. Olá **resolver** método utiliza Olá **resolução** delegar tooresolve **DynamicTableEntity** instâncias demasiado**TableEntity** instâncias.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Modificar os tipos de entidade heterogénea
Não é necessário o tipo de Olá tooknow de uma entidade toodelete e que saiba sempre tipo Olá de uma entidade ao inseri-lo. No entanto, pode utilizar **DynamicTableEntity** tooupdate uma entidade de tipo sem saberem o respetivo tipo e sem utilizar uma classe de entidade POCO. Olá exemplo de código seguinte obtém uma única entidade e verifica Olá **EmployeeCount** existe uma propriedade antes de atualizá-la.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Controlar o acesso com assinaturas de acesso partilhado
Pode utilizar a assinatura de acesso partilhado (SAS) tokens tooenable cliente aplicações toomodify (e consultar) diretamente, sem necessidade de Olá tooauthenticate diretamente com o serviço de tabela Olá as entidades da tabela. Normalmente, existem três toousing vantagens principais SAS na sua aplicação:  

* Não é necessário toodistribute seu armazenamento conta tooan chave plataforma inseguras (por exemplo, um dispositivo móvel) na ordem tooallow tooaccess desse dispositivo e modificar as entidades de Olá serviço tabela.  
* Pode descarregar algum do trabalho Olá nesse web e funções de trabalho executar gerir os dispositivos de tooclient entidades, tais como computadores do utilizador final e de dispositivos móveis.  
* Pode atribuir um restrita e tempo conjunto limitado de cliente de tooa de permissões (por exemplo, permitir o acesso só de leitura toospecific recursos).  

Para obter mais informações sobre como utilizar os tokens SAS com Olá serviço tabela, consulte [através de acesso partilhado assinaturas (SAS)](storage-dotnet-shared-access-signature-part-1.md).  

No entanto, tem ainda de gerar tokens SAS Olá que um cliente de conceder as entidades da aplicação toohello no serviço de tabela Olá: deve fazê-lo num ambiente que tem acesso seguro tooyour chaves de conta de armazenamento. Normalmente, utilizar um web ou de trabalho função toogenerate Olá SAS tokens e entregá-los toohello aplicações de cliente que precisam de aceder tooyour entidades. Porque não existe ainda um overhead inerente ao gerar e entrega tooclients de tokens SAS, deve considerar como melhor tooreduce esta sobrecarga, especialmente em cenários de elevado volume.  

É possível toogenerate um token SAS, que concede acesso tooa subconjunto de entidades de Olá numa tabela. Por predefinição, cria um token SAS para uma tabela inteira, mas também é possível toospecify que tooeither do acesso de concessão de token SAS Olá um intervalo de **PartitionKey** valores ou um intervalo de **PartitionKey** e  **RowKey** valores. Poderá escolher toogenerate tokens SAS para utilizadores individuais do seu sistema, de modo a que o token SAS de cada utilizador só permite-lhes acesso tootheir entidades própria Olá serviço tabela.  

### <a name="asynchronous-and-parallel-operations"></a>Operações assíncronas e paralelas
Fornecidas são propagando-se os pedidos entre várias partições, pode melhorar a capacidade de resposta de débito e o cliente utilizando as consultas paralelas ou assíncronas.
Por exemplo, pode ter duas ou mais trabalho instâncias de função de aceder as tabelas em paralelo. Foi tem funções de trabalho individuais responsáveis por conjuntos de específicos de partições ou simplesmente tem várias instâncias de função de trabalho, cada tooaccess capaz de Olá todas as partições numa tabela.  

Dentro de uma instância de cliente, pode melhorar o débito ao executar operações de armazenamento de forma assíncrona. Olá biblioteca de clientes de armazenamento permite consultas assíncrona toowrite fácil e modificações. Por exemplo, poderá começar com o método síncrono Olá que obtém todas as entidades de Olá numa partição, conforme mostrado no Olá código c# os seguintes:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Pode facilmente modificar este código para que essa consulta Olá seja executada de forma assíncrona, da seguinte forma:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

Neste exemplo assíncrona, pode ver a seguinte Olá é alterado de versão síncrona Olá:  

* a assinatura do método Olá inclui agora Olá **async** modificador e devolve um **tarefas** instância.  
* Em vez de chamar Olá **ExecuteSegmented** resultados do método tooretrieve, Olá método agora chamadas Olá **ExecuteSegmentedAsync** Olá método e utiliza **await** modificador tooretrieve resulta no modo assíncrono.  

aplicação de cliente Olá pode chamar este método várias vezes (com valores diferentes para Olá **departamento** parâmetro), e cada consulta será executado num thread separado.  

Tenha em atenção que não há nenhuma versão assíncrona de Olá **executar** método Olá **TableQuery** classe porque Olá **IEnumerable** interface não suporta assíncrona enumeração.  

Também pode inserir, atualizar e eliminar entidades no modo assíncrono. Olá c# exemplo a seguir mostra um método simples, síncrona tooinsert ou substituir uma entidade de empregado:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Pode facilmente modificar este código, para que a atualização de Olá funciona de forma assíncrona, da seguinte forma:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Neste exemplo assíncrona, pode ver a seguinte Olá é alterado de versão síncrona Olá:  

* a assinatura do método Olá inclui agora Olá **async** modificador e devolve um **tarefas** instância.  
* Em vez de chamar Olá **executar** entidade do método tooupdate Olá, Olá método agora chamadas Olá **ExecuteAsync** Olá método e utiliza **await** tooretrieve modificador resulta no modo assíncrono.  

aplicação de cliente Olá pode chamar vários métodos assíncronos como este, e cada invocação do método será executado num thread separado.  

### <a name="credits"></a>Créditos
Gostaríamos Olá toothank seguintes membros Olá equipa do Azure para as respetivas contribuições: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Irwin Jorge, Vamshidhar Kommineni, Vinay Shah e Serdar Ozler, bem como Hollander personalizada da Microsoft DX. 

Também Gostaríamos Olá toothank seguir da Microsoft MVP para os seus comentários importantes ciclos de revisão: Igor Papirov e Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

