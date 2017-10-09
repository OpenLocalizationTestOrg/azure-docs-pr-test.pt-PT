---
title: "dados de aaaLoad do SQL Server do armazém de dados de SQL do Azure (SSIS) | Microsoft Docs"
description: "Mostra como toocreate um SQL Server Integration Services (SSIS) pacote toomove de dados de uma ampla variedade de dados origens tooSQL do armazém de dados."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Carregar dados do SQL Server do armazém de dados de SQL do Azure (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Crie um SQL Server Integration Services (SSIS) pacote tooload de dados do SQL Server para o Azure SQL Data Warehouse. Pode, opcionalmente, reestruturar, transformar e limpar os dados de Olá, estes passam por fluxo de dados SSIS Olá.

Neste tutorial, irá:

* Crie um novo projeto de serviços de integração no Visual Studio.
* Ligar a origens de toodata, incluindo o SQL Server (como uma origem) e o SQL Data Warehouse (como um destino).
* Conceber um pacote SSIS carrega dados a partir da origem de Olá para destino Olá.
* Execute Olá SSIS pacote tooload Olá de dados.

Este tutorial utiliza o SQL Server como origem de dados de Olá. SQL Server pode estar em execução no local ou numa máquina virtual do Azure.

## <a name="basic-concepts"></a>Conceitos básicos
pacote de Olá é Olá uma unidade de trabalho no SSIS. Pacotes relacionados são agrupadas numa projetos. Crie projetos e pacotes de estrutura no Visual Studio com SQL Server Data Tools. estrutura de Olá processo é um processo visual na qual a arrastar e largar os componentes da superfície de desenho de toohello de caixa de ferramentas de Olá, ligue-os e definir as respetivas propriedades. Depois de concluir o pacote, pode, opcionalmente, implementar, tooSQL servidor de Gestão abrangente, monitorização e segurança.

## <a name="options-for-loading-data-with-ssis"></a>Opções para carregar dados com SSIS
SQL Server Integration Services (SSIS) é um conjunto flexível de ferramentas que fornece uma variedade de opções para ligar a e carregar dados para o SQL Data Warehouse.

1. Utilize um tooSQL de tooconnect ADO NET destino do armazém de dados. Este tutorial utiliza um destino de NET ADO porque tem Olá menos opções de configuração.
2. Utilize um tooSQL tooconnect de destino OLE DB do armazém de dados. Esta opção pode fornecer ligeiramente melhor desempenho do que Olá ADO rede de destino.
3. Utilize dados de Olá de toostage do Olá a tarefa de carregar Blob do Azure no Blob Storage do Azure. Em seguida, utilize toolaunch de tarefas de SSIS executar SQL Olá um script do Polybase que carrega dados Olá para o SQL Data Warehouse. Esta opção fornece o melhor desempenho Olá de Olá três opções listadas aqui. Olá tooget tarefa carregar de Blob do Azure, transferir Olá [Microsoft SQL Server 2016 integração serviços Feature Pack para o Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn mais informações sobre o Polybase, consulte [Guia do PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Antes de começar
toostep com este tutorial, precisa de:

1. **SQL Server Integration Services (SSIS)**. SSIS é um componente do SQL Server e necessita de uma versão de avaliação ou uma versão licenciada do SQL Server. Consulte tooget uma versão de avaliação do SQL Server 2016 Preview [avaliações do SQL Server][SQL Server Evaluations].
2. **Visual Studio**. tooget Olá livre Visual Studio Community Edition, consulte [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools para Visual Studio (SSDT)**. tooget SQL Server Data Tools para Visual Studio, consulte [transferir SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Dados de exemplo**. Este tutorial utiliza dados de exemplo armazenados no SQL Server na base de dados de exemplo Olá AdventureWorks como Olá toobe de dados de origem carregado para o SQL Data Warehouse. Olá tooget base de dados de exemplo AdventureWorks, consulte [bases de dados de exemplo AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **Uma base de dados do SQL Data Warehouse e as permissões**. Este tutorial liga-se a instância do SQL Data Warehouse tooa e carrega dados para a mesma. Ter toohave permissões toocreate uma tabela e tooload de dados.
6. **Uma regra de firewall**. Tem toocreate uma regra de firewall no SQL Data Warehouse com o endereço IP Olá do computador local antes de pode carregar toohello de dados do armazém de dados do SQL Server.

## <a name="step-1-create-a-new-integration-services-project"></a>Passo 1: Criar um novo projeto de serviços de integração
1. Inicie o Visual Studio.
2. No Olá **ficheiro** menu, selecione **novo | Projeto**.
3. Navegue toohello **instalada | Modelos | Business Intelligence | Serviços de integração** tipos de projetos.
4. Selecione **projeto dos serviços de integração**. Fornecer valores para **nome** e **localização**e, em seguida, selecione **OK**.

Visual Studio abre e cria um novo projeto do Integration Services (SSIS). Em seguida, o Visual Studio abre designer Olá para o pacote SSIS Olá único novo (Package.dtsx) no projeto Olá. Consulte Olá áreas de ecrã a seguir:

* No lado esquerdo de Olá, Olá **Toolbox** dos componentes SSIS.
* No meio de Olá, Olá superfície de desenho, com vários separadores. Normalmente utiliza, pelo menos, Olá **fluxo de controlo** e Olá **do fluxo de dados** separadores.
* No Olá à direita, Olá **Explorador de soluções** e Olá **propriedades** painéis.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Passo 2: Criar o fluxo de dados básico Olá
1. Arraste uma tarefa de fluxo de dados a partir do Centro de toohello Olá caixa de ferramentas da superfície de desenho de Olá (no Olá **fluxo de controlo** separador).
   
    ![][02]
2. Faça duplo clique separador de fluxo de dados de toohello tooswitch de tarefa de fluxo de dados do Olá.
3. Na lista de outras origens de Olá na caixa de ferramentas de Olá, arraste uma superfície de desenho de toohello de origem do ADO.NET. Com o adaptador de origem Olá ainda selecionada, alterar o respetivo nome demasiado**origem do SQL Server** no Olá **propriedades** painel.
4. Na lista de destinos outras Olá na caixa de ferramentas de Olá, arraste uma superfície de desenho do destino do ADO.NET toohello em Olá ADO.NET origem. Com o adaptador de destino de Olá ainda selecionada, alterar o respetivo nome demasiado**destino do armazém de dados do SQL Server** no Olá **propriedades** painel.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Passo 3: Configurar a placa de origem Olá
1. Faça duplo clique em Olá do Olá origem adaptador tooopen **Editor de origem do ADO.NET**.
   
    ![][03]
2. No Olá **Gestor de ligações** separador de Olá **Editor de origem do ADO.NET**, clique em Olá **novo** toohello seguinte botão **Gestor de ligações do ADO.NET**Olá de tooopen lista **configurar Gestor de ligação do ADO.NET** diálogo caixa e criar definições de ligação de base de dados do SQL Server Olá partir do qual este tutorial carrega dados.
   
    ![][04]
3. No Olá **configurar Gestor de ligação do ADO.NET** caixa de diálogo, clique em Olá **novo** Olá do botão tooopen **Gestor de ligações** diálogo caixa e criar uma nova ligação de dados.
   
    ![][05]
4. No Olá **Gestor de ligações** diálogo caixa, Olá seguintes coisas.
   
   1. Para **fornecedor**, selecione Olá SqlClient Data Provider.
   2. Para **nome do servidor**, introduza o nome do Olá do SQL Server.
   3. No Olá **inicie sessão no servidor de toohello** secção, selecione ou introduza as informações de autenticação.
   4. No Olá **base de dados do Connect tooa** secção, selecione a base de dados de exemplo Olá AdventureWorks.
   5. Clique em **Testar ligação**.
      
       ![][06]
   6. Na caixa de diálogo de Olá que reporta Olá resultados do teste de ligação de Olá, clique em **OK** tooreturn toohello **Gestor de ligações** caixa de diálogo.
   7. No Olá **Gestor de ligações** caixa de diálogo, clique em **OK** tooreturn toohello **configurar Gestor de ligação do ADO.NET** caixa de diálogo.
5. No Olá **configurar Gestor de ligação do ADO.NET** caixa de diálogo, clique em **OK** tooreturn toohello **Editor de origem do ADO.NET**.
6. No Olá **Editor de origem do ADO.NET**, no Olá **nome de tabela de Olá ou vista Olá** lista, selecione de Olá **Sales.SalesOrderDetail** tabela.
   
    ![][07]
7. Clique em **pré-visualização** toosee Olá primeiros 200 linhas de dados na tabela de origem Olá no Olá **pré-visualizar resultados de consulta** caixa de diálogo.
   
    ![][08]
8. No Olá **pré-visualizar resultados de consulta** caixa de diálogo, clique em **fechar** tooreturn toohello **Editor de origem do ADO.NET**.
9. No Olá **Editor de origem do ADO.NET**, clique em **OK** toofinish ao configurar a origem de dados de Olá.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Passo 4: Ligar o adaptador de destino do Olá origem adaptador toohello
1. Selecione o adaptador de origem de Olá na superfície de desenho de Olá.
2. Selecione a seta azul Olá que alarga a partir do adaptador de origem Olá e arraste-o editor de destino toohello até ajusta a no local.
   
    ![][10]
   
    Num pacote de SSIS típico, pode utiliza um número de outros componentes de Olá SSIS Toolbox entre a origem de Olá e Olá destino toorestructure, transformação e limpar os seus dados, estes passam por fluxo de dados SSIS Olá. tookeep neste exemplo tão simple quanto possível, está a ligar Olá diretamente origem toohello destino.

## <a name="step-5-configure-hello-destination-adapter"></a>Passo 5: Configurar o adaptador de destino Olá
1. Faça duplo clique em Olá do Olá destino placa tooopen **ADO.NET destino Editor**.
   
    ![][11]
2. No Olá **Gestor de ligações** separador de Olá **ADO.NET destino Editor**, clique em Olá **novo** toohello seguinte botão **Gestor de ligações**Olá de tooopen lista **configurar Gestor de ligação do ADO.NET** diálogo caixa e criar definições de ligação de base de dados do Azure SQL Data Warehouse Olá na qual este tutorial carrega dados.
3. No Olá **configurar Gestor de ligação do ADO.NET** caixa de diálogo, clique em Olá **novo** Olá do botão tooopen **Gestor de ligações** diálogo caixa e criar uma nova ligação de dados.
4. No Olá **Gestor de ligações** diálogo caixa, Olá seguintes coisas.
   1. Para **fornecedor**, selecione Olá SqlClient Data Provider.
   2. Para **nome do servidor**, introduza o nome do SQL Data Warehouse Olá.
   3. No Olá **inicie sessão no servidor de toohello** secção, selecione **autenticação do SQL Server de utilização** e introduza as informações de autenticação.
   4. No Olá **base de dados do Connect tooa** secção, selecione uma base de dados existente do SQL Data Warehouse.
   5. Clique em **Testar ligação**.
   6. Na caixa de diálogo de Olá que reporta Olá resultados do teste de ligação de Olá, clique em **OK** tooreturn toohello **Gestor de ligações** caixa de diálogo.
   7. No Olá **Gestor de ligações** caixa de diálogo, clique em **OK** tooreturn toohello **configurar Gestor de ligação do ADO.NET** caixa de diálogo.
5. No Olá **configurar Gestor de ligação do ADO.NET** caixa de diálogo, clique em **OK** tooreturn toohello **ADO.NET destino Editor**.
6. No Olá **ADO.NET destino Editor**, clique em **novo** toohello seguinte **utilizar uma tabela ou vista** Olá de tooopen lista **Create Table** caixa de diálogo uma nova tabela de destino com uma lista de colunas que corresponde à tabela de origem Olá toocreate.
   
    ![][12a]
7. No Olá **Create Table** diálogo caixa, Olá seguintes coisas.
   
   1. Alterar o nome de Olá da tabela de destino Olá demasiado**SalesOrderDetail**.
   2. Remover Olá **rowguid** coluna. Olá **uniqueidentifier** tipo de dados não é suportado no SQL Data Warehouse.
   3. Alterar tipo de dados de Olá de Olá **LineTotal** coluna demasiado**dinheiro**. Olá **decimal** tipo de dados não é suportado no SQL Data Warehouse. Para informações sobre os tipos de dados suportadas, consulte [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Clique em **OK** toocreate Olá toohello tabela e retorno **ADO.NET destino Editor**.
8. No Olá **ADO.NET destino Editor**, selecione Olá **mapeamentos** separador toosee como colunas na origem de Olá mapeados toocolumns no destino Olá.
   
    ![][13]
9. Clique em **OK** toofinish ao configurar a origem de dados de Olá.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Passo 6: Executar Olá pacote tooload Olá de dados
Pacote de execução Olá clicando Olá **iniciar** botão na barra de ferramentas Olá ou selecionando uma das Olá **executar** opções Olá **depurar** menu.

À medida que o pacote de Olá, começa a toorun vê amarelo girar rodas tooindicate atividade, bem como o número de Olá de linhas processadas até ao momento.

![][14]

Quando o pacote de Olá concluiu a execução, consulte marca de verificação verde tooindicate êxito, bem como Olá número total de linhas de dados carregados a partir do destino de toohello Olá origem.

![][15]

Parabéns! Utilizou com êxito dados do SQL Server Integration Services tooload no Azure SQL Data Warehouse.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre o fluxo de dados SSIS Olá. Comece por aqui: [do fluxo de dados][Data Flow].
* Saiba como toodebug e o direito de pacotes no ambiente de estrutura de Olá de resolução de problemas. Comece por aqui: [ferramentas de resolução de problemas de mensagens em fila para o desenvolvimento de pacote][Troubleshooting Tools for Package Development].
* Saiba como toodeploy sua SSIS projetos e pacotes tooIntegration localização de armazenamento do servidor de serviços ou tooanother. Comece por aqui: [de projetos de implementação do e pacotes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
