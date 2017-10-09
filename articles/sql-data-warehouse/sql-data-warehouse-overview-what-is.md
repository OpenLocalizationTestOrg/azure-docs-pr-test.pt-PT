---
title: "aaaWhat é o Azure SQL Data Warehouse? | Microsoft Docs"
description: "Base de dados distribuída de nível empresarial capaz de processar volumes de petabytes de dados relacionais e não relacionais. É primeiro nuvem armazém de dados da indústria Olá que pode aumentar, diminuir e colocar em pausa em segundos."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>O que é o Azure SQL Data Warehouse?
O Azure SQL Data Warehouse é uma base de dados para processamento paralelo em massa (MPP), baseada na cloud, de escalabilidade horizontal e relacional, capaz de processar grandes volumes de dados. 

SQL Data Warehouse:

* Combina a base de dados relacional do SQL Server Olá com capacidades de escalamento horizontal em nuvem do Azure. 
* Dissocia o armazenamento da computação.
* Ativa o aumento, diminuição, colocação em pausa e retoma da computação. 
* Integra-se em Olá plataforma Azure.
* Utiliza o Transact-SQL (T-SQL) e ferramentas do SQL Server.
* Está em conformidade com diversos requisitos de segurança legais e empresariais, como SOC e ISO.

Este artigo descreve as principais funcionalidades Olá do SQL Data Warehouse.

## <a name="massively-parallel-processing-architecture"></a>Arquitetura de processamento paralelo em massa
O SQL Data Warehouse é um sistema de base de dados distribuído de processamento paralelo em massa (MPP). Em segundo plano do Olá, o SQL Data Warehouse propaga os dados em muitas unidades de processamento e armazenamento. dados de Olá são armazenados numa camada de armazenamento localmente redundante Premium sobre quais nós de computação ligados dinamicamente executar consultas. Guia de armazém de dados do SQL Server que carrega um toorunning abordagem de "dividir e conquistar" e consultas complexas. Os pedidos são recebidos pelo nó de controlo, otimizados para distribuição e, em seguida, transmitidos tooCompute nós toodo trabalhar em paralelo.

Com armazenamento e computação desacoplados, o SQL Data Warehouse pode:

* Aumentar ou diminuir o tamanho do armazenamento, independentemente da computação.
* Aumentar ou diminuir o poder de computação sem mover dados.
* Colocar a capacidade de computação em pausa mantendo os dados intactos, pagando apenas pelo armazenamento.
* Retomar a capacidade de computação durante as horas de funcionamento.

Olá diagrama seguinte mostra a arquitetura de Olá mais detalhadamente.

![Arquitetura do SQL Data Warehouse][1]

**Nó de controlo:** o nó de controlo de Olá gere e otimiza consultas. É front-end do Olá que interage com todas as ligações e aplicações. No SQL Data Warehouse, utiliza a tecnologia de base de dados do SQL Server, o nó de controlo de Olá e ligar tooit procura e um aspeto semelhante Olá mesmo. Sob a superfície de Olá, nó de controlo de Olá coordena movimento de dados de Olá e a computação necessária toorun consultas paralelas nos seus dados distribuídos. Quando submete uma tooSQL de consulta de T-SQL do armazém de dados, o nó de controlo de Olá transforma-a em consultas separadas que são executadas em cada nó de computação em paralelo.

**Nós de computação:** nós de computação Olá servirem como poder de Olá por trás do SQL Data Warehouse. São Bases de Dados SQL que armazenam os dados e processam a consulta. Quando adiciona dados, o SQL Data Warehouse distribui nós de computação do Olá linhas tooyour. nós de computação Olá são trabalhadores de Olá que executam consultas paralelas Olá nos seus dados. Após o processamento, passam do nó de controlo do Olá resultados toohello anterior. consulta de Olá toofinish, o nó de controlo de Olá agrega os resultados de Olá e devolve Olá resultado final.

**Armazenamento:** os dados são armazenados no Armazenamento de Blobs do Azure. Quando os nós de computação interagem com os seus dados, escrevem e leem diretamente tooand do armazenamento de Blobs. Uma vez que o armazenamento do Azure expande de forma transparente e muito, o SQL Data Warehouse pode fazer Olá mesmo. Como a computação e o armazenamento são independentes, o SQL Data Warehouse pode, de forma independente, dimensionar o armazenamento e a computação e vice-versa. Blob storage do Azure é também totalmente tolerante a falhas e simplifica Olá cópia de segurança e restaurar o processo.

**Serviço de movimento de dados:** serviço de movimento de dados (DMS) move dados entre os nós de Olá. O DMS dá Olá computação nós acesso toodata que necessitam para associações e agregações. O DMS não é um serviço do Azure. É um serviço do Windows que é executado em conjunto com a base de dados SQL em todos os nós de Olá. O DMS é um processo em segundo plano com o qual não é possível interagir diretamente. No entanto, pode examinar consulta planos toosee quando ocorrem operações do DMS, uma vez que o movimento de dados é necessário toorun cada consulta em paralelo.

## <a name="optimized-for-data-warehouse-workloads"></a>Otimizado para cargas de trabalho do armazém de dados
Olá abordagem MPP é auxiliada algumas por vários otimizações de desempenho específica, incluindo de armazém de dados:

* Um otimizador de consultas distribuídas e um conjunto de estatísticas complexas em todos os dados. Utilizando informações sobre o tamanho dos dados e a distribuição, o serviço de Olá é capaz de toooptimize consultas ao avaliar o custo de Olá das operações de consulta distribuída específicas.
* Técnicas e algoritmos avançados integrados no dados Olá movimento processar tooefficiently mover dados entre os recursos informáticos como consulta de Olá tooperform necessário. Estas operações de movimento de dados estão incorporadas no e todas as otimizações toohello serviço de movimento de dados ocorrem automaticamente.
* Índices **columnstore** em cluster por predefinição. Utilizando o armazenamento baseado em colunas, o SQL Data Warehouse obtém em média 5 ganhos de compressão x ao armazenamento orientado por linhas tradicional e cópia de segurança too10x ou mais ganhos de desempenho de consulta. As consultas de análises que precisam de tooscan um grande número de linhas são funcionar melhor com índices columnstore.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Desempenho previsível e dimensionável com Unidades do Data Warehouse
O SQL Data Warehouse está incorporado com tecnologias semelhantes às da Base de Dados SQL, o que significa que os utilizadores podem contar com desempenho consistente e previsível em consultas de análise. Os utilizadores devem esperar escala de desempenho toosee forma linear dado que o se adicionam ou subtrair nós de computação. Alocação de recursos tooyour SQL Data Warehouse é medida em unidades do Data Warehouse (DWUs). As DWUs são uma medida dos recursos subjacentes como CPU, memória e IOPS, que estão alocados tooyour SQL Data Warehouse. Aumento Olá número de DWUs aumenta os recursos e o desempenho. Especificamente, as DWUs ajudam a garantir o seguinte:

* É capaz de tooscale do armazém de dados sem ter de se preocupar sobre o hardware subjacente Olá ou software.
* Pode prever uma melhoria de desempenho para um nível DWU antes de alterar o cálculo de Olá do seu armazém de dados.
* Olá subjacente hardware e software da sua instância podem ser alterados ou movidos sem afetar o desempenho da carga de trabalho.
* Pode melhorar o Microsoft hello subjacente arquitetura do serviço de Olá sem afetar o desempenho de Olá da sua carga de trabalho.
* Microsoft pode melhorar rapidamente o desempenho do armazém de dados do SQL Server, de forma a que seja escalável e uniformemente efeitos Olá sistema.

As Unidades do Data Warehouse proporcionam uma medida de três métricas, que estão altamente correlacionadas com o desempenho da carga de trabalho do armazém de dados. seguinte Olá chave escala de métricas de carga de trabalho forma linear com Olá DWUs.

**Análise/Agregação:** uma consulta de armazém de dados padrão, que analisa um grande número de linhas e, em seguida, efetua uma agregação complexa. Esta operação é exigente em termos de E/S e CPU.

**Carga:** Olá dados tooingest de capacidade para o serviço de Olá. As cargas são melhor efetuadas com o PolyBase a partir dos Blobs do Armazenamento do Azure ou do Azure Data Lake. Esta métrica é concebida toostress rede e aspetos de CPU do serviço de Olá.

**Create Table As Select (CTAS):** CTAS mede Olá capacidade toocopy uma tabela. Isto envolve a leitura de dados do armazenamento, a distribuição dos mesmos por nós de Olá da aplicação Olá e escrever toostorage novamente. É uma operação exigente em termos de CPU, de E/S e da rede.

## <a name="built-on-sql-server"></a>Incorporado no SQL Server
O SQL Data Warehouse baseia-se no motor de base de dados relacional do SQL Server Olá e inclui muitas das funcionalidades de Olá que se espera de um armazém de dados empresarial. Se já conhece o T-SQL, é fácil tootransfer tooSQL o conhecimento do armazém de dados. Se um utilizador avançado ou esteja apenas a começar, exemplos de Olá em toda a documentação de Olá irão ajudar a começar. Em geral, pode pensar sobre a forma de Olá construímos elementos de linguagem Olá do SQL Data Warehouse da seguinte forma:

* O SQL Data Warehouse utiliza sintaxe de T-SQL para muitas operações. Suporta também um conjunto amplo de construções tradicionais de SQL, tais como procedimentos armazenados, funções definidas pelo utilizador, criação de partições de tabela, índices e agrupamentos.
* O SQL Data Warehouse contém também várias funcionalidades mais recentes do SQL Server, incluindo índices **columnstore** em cluster, integração do PolyBase e auditoria de dados (completa com avaliação de ameaças).
* Determinados elementos de linguagem T-SQL que são menos comuns para cargas de trabalho do armazém de dados, ou que são tooSQL mais recente do servidor, poderão não estar disponíveis atualmente. Para obter mais informações, consulte Olá [documentação de migração][Migration documentation].

Com Olá Transact-SQL e a convergência de funcionalidades de funcionalidade entre SQL Server, o SQL Data Warehouse, base de dados SQL e Analytics Platform System, pode desenvolver uma solução que se adeque às suas necessidades de dados. Pode decidir onde tookeep os dados, com base nos dados de desempenho, segurança e os requisitos de escala e, em seguida, transferência conforme necessário entre sistemas diferentes.

## <a name="data-protection"></a>Proteção de dados
O SQL Data Warehouse armazena todos os dados no armazenamento localmente redundante Premium do Azure. Várias cópias síncronas dos dados de Olá são mantidas na proteção transparente de dados tooguarantee de centro de dados local de Olá contra falhas localizadas. Além disso, o SQL Data Warehouse efetua automaticamente cópias de segurança das bases de dados ativas (que não estão em pausa) a intervalos regulares através de Instantâneos de Armazenamento do Azure. toolearn mais informações sobre como criar cópias de segurança e restaurar funciona, consulte Olá [descrição geral da cópia de segurança e restauro][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Integrado com ferramentas da Microsoft
O SQL Data Warehouse também integra muitas das ferramentas de Olá que os utilizadores podem estar familiarizados com o SQL Server. Estas ferramentas incluem:

**Ferramentas tradicionais do SQL Server:** o SQL Data Warehouse, está totalmente integrado com o SQL Server Analysis Services, o Integration Services e o Reporting Services.

**Ferramentas baseadas na cloud:** o SQL Data Warehouse pode ser integrado em vários serviços do Azure, incluindo o Data Factory, o Stream Analytics, o Machine Learning e o Power BI. Para obter uma lista mais completa, veja [Integrated tools overview (Descrição geral de ferramentas integradas)][Integrated tools overview].

**Ferramentas de terceiros:** muitos fornecedores terceiros de ferramentas certificaram a integração das respetivas ferramentas com o SQL Data Warehouse. Para obter uma lista completa, veja [SQL Data Warehouse solution partners (Parceiros de soluções do SQL Data Warehouse)][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Cenários híbridos de origens de dados
O Polybase permite-lhe tooleverage os dados de diferentes origens através da utilização de comandos familiares do T-SQL. O Polybase permite fazer tooquery dados não relacionais mantidos no armazenamento de Blobs do Azure como se se tratasse de uma tabela normal. Utilize o Polybase tooquery dados não relacionais ou tooimport dados não relacionais para o SQL Data Warehouse.

* O PolyBase utiliza dados não relacionais do tooaccess tabelas externas. definições de tabela Olá são armazenadas no armazém de dados do SQL Server e pode aceder às mesmas através de SQL e ferramentas, tal como acederia a dados relacionais normais.
* O Polybase é agnóstico em termos de integração. Expõe Olá mesmas funcionalidades e a funcionalidade tooall Olá origens que suporta. dados de Olá lidos pelo Polybase podem ter vários formatos, incluindo ficheiros delimitados ou ficheiros ORC.
* O PolyBase pode ser utilizado tooaccess armazenamento de BLOBs que também está a ser utilizado como armazenamento para um cluster do HDInsight. Este fornecem acesso toohello mesmos dados com ferramentas relacionais e não relacionais.

## <a name="sla"></a>SLA
O SQL Data Warehouse oferece um contrato de nível de serviço (SLA) de nível de produto como parte do SLA do Microsoft Online Services. Para obter mais informações, visite [SLA para o SQL Data Warehouse][SLA for SQL Data Warehouse]. Para informações de SLA sobre todos os outros produtos visitando Olá [contratos de nível de serviço] Azure página ou transferi-los no Olá [licenciamento em Volume] [ Volume Licensing] página. 

## <a name="next-steps"></a>Passos seguintes
Agora que já sabe um pouco sobre o SQL Data Warehouse, saiba como tooquickly [criar um SQL Data Warehouse] [ create a SQL Data Warehouse] e [carregar dados de exemplo][load sample data]. Se forem tooAzure novo, pode encontrar Olá [Glossário do Azure] [ Azure glossary] úteis como que encontra terminologia nova. Em alternativa, veja alguns destes outros Recursos do SQL Data Warehouse.  

* [Histórias de sucesso de clientes]
* [Blogues]
* [Pedidos de funcionalidades]
* [Vídeos]
* [Blogues da Equipa Customer Advisory]
* [Criar pedido de suporte]
* [Fórum do MSDN]
* [Fórum do Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Criar pedido de suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Histórias de sucesso de clientes]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogues]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogues da Equipa Customer Advisory]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Pedidos de funcionalidades]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Fórum do MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Fórum do Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vídeos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[contratos de nível de serviço]: https://azure.microsoft.com/en-us/support/legal/sla/
