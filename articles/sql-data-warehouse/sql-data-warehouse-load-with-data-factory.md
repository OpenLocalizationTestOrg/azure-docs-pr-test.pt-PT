---
title: "dados de aaaLoad no Azure SQL Data Warehouse – Data Factory | Microsoft Docs"
description: "Este tutorial carrega dados para o Azure SQL Data Warehouse, utilizando o Azure Data Factory e utiliza uma base de dados do SQL Server como origem de dados de Olá."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Carregar dados para o SQL Data Warehouse com o Data Factory

Pode utilizar os dados do Azure Data Factory tooload no Azure SQL Data Warehouse a partir de qualquer Olá [arquivos de dados de origem suportados](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Por exemplo, pode carregar dados de uma base de dados SQL do Azure ou uma base de dados Oracle para um SQL data warehouse, utilizando o Data Factory. Tutorial neste artigo mostra como dados de tooload de um servidor de SQL no local da base de dados para um SQL data warehouse.

**Estimativa de tempo**: Este tutorial guia sobre toocomplete de 10 a 15 minutos, depois de Olá pré-requisitos são cumpridos.

## <a name="prerequisites"></a>Pré-requisitos

- É necessário um **base de dados do SQL Server** com tabelas que contenham dados Olá toobe copiadas toohello do armazém de dados do SQL Server.  

- É necessário um online **SQL Data Warehouse**. Se ainda não tiver um armazém de dados, saiba como demasiado[criar um Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).

- É necessário um **conta do Storage do Azure**. Se ainda não tiver uma conta de armazenamento, saiba como demasiado[criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md). Para melhor desempenho, localize a conta de armazenamento Olá e Olá do armazém de dados no Olá mesma região do Azure.

## <a name="configure-a-data-factory"></a>Configurar uma fábrica de dados
1. Inicie sessão no toohello [portal do Azure][].
2. Localize o seu armazém de dados e clique em tooopen-lo.
3. No painel principal Olá, clique em **carga dados** > **do Azure Data Factory**.

    ![Iniciar o Assistente de dados de carga](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Se não tiver uma fábrica de dados na sua subscrição do Azure, verá um **nova fábrica de dados** caixa de diálogo no separador do browser Olá. Preencha Olá informações necessárias e clique em **criar**. Depois de criar a fábrica de dados de Olá, Olá **nova fábrica de dados** fecha a caixa de diálogo e ver Olá **selecione Data Factory** caixa de diálogo.

    Se tiver uma ou mais dos data factories já se encontra na Olá subscrição do Azure, consulte Olá **selecione Data Factory** caixa de diálogo. Na caixa de diálogo, pode selecionar uma fábrica de dados existente ou clique em **criar nova fábrica de dados** toocreate um novo.

    ![Configurar fábrica de dados](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. No Olá **selecione Data Factory** caixa de diálogo, Olá **carregar dados** opção está selecionada por predefinição. Clique em **seguinte** toostart criar uma tarefa de carregamento de dados.

## <a name="configure-hello-data-factory-properties"></a>Configurar propriedades de fábrica de dados de Olá
Agora que criou uma fábrica de dados, o passo seguinte Olá é dados de Olá de tooconfigure carregar agenda.

1. Para **nome da tarefa**, introduza **DWLoadData fromSQLServer**.
2. Utilizar predefinição de Olá **executar agora uma vez** opção, clique em **seguinte**.

    ![Configurar agenda de carga](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Configurar Olá arquivo de dados de origem e de gateway
Agora, indique ao Data Factory sobre Olá no local do SQL Server da base de dados de que pretende que os dados de tooload.

1. Escolha **do SQL Server** dos dados de origem Olá suportado armazenar catálogo e clique em **seguinte**.

    ![Selecione a origem do SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A **base de dados do especifique Olá no local do SQL Server** é apresentada a caixa de diálogo. Olá primeiro **nome da ligação** campo é automaticamente preenchido. campo segundo Olá pede-lhe nome Olá Olá **Gateway**. Se estiver a utilizar uma fábrica de dados existente que já tem um gateway, pode reutilizar o gateway de Olá, selecionando-Olá na lista pendente. Clique em Olá **criar Gateway** ligação toocreate um Data Management Gateway.  

    > [!NOTE]
    > Se o arquivo de dados de origem Olá for no local ou numa máquina virtual IaaS do Azure, é necessário um Gateway de gestão de dados. Um gateway tem uma relação de 1-1, com uma fábrica de dados. Não é possível utilizar a partir de outro fábrica de dados, mas pode ser utilizado por vários dados carregar tarefas com Olá mesma fábrica de dados. Um gateway pode ser utilizado tooconnect toomultiple os arquivos de dados quando executar tarefas de carregamento de dados.
    >
    > Para obter informações detalhadas sobre o gateway de Olá, consulte [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artigo.

3. A **criar Gateway** é apresentada a caixa de diálogo. Para nome, introduza **GatewayForDWLoading**e clique em **criar**.

4. A **configurar Gateway** é apresentada a caixa de diálogo. Clique em **lançar a configuração rápida neste computador** tooautomatically transferir, instalar e registar o Gateway de gestão de dados no seu computador atual. progresso de Olá é apresentado numa janela de pop-up. Se a máquina Olá não é possível ligar o arquivo de dados de toohello, pode manualmente [transferir e instalar o gateway de Olá](https://www.microsoft.com/download/details.aspx?id=39717) num computador que possam ligar toohello dados armazenar e, em seguida, utilize tooregister chave Olá.
    > [!NOTE]
    > configuração rápida Olá nativamente funciona com o Microsoft Edge e do Internet Explorer. Se estiver a utilizar o Google Chrome, primeiro de instalar extensão do Olá ClickOnce do arquivo de web do Chrome.

    ![Inicie a configuração rápida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Aguarde toocomplete de configuração do gateway Olá. Depois de gateway Olá for registado com êxito e estiver online, fecha a janela de pop-up Olá e o novo gateway de Olá aparece no campo gateway de Olá. Em seguida, preencha o resto Olá necessário campos da seguinte forma, em seguida, clique em **seguinte**.
    - **Nome do servidor**: nome do Olá no local do SQL Server.
    - **Nome da base de dados**: base de dados do SQL Server.
    - **Encriptação de credenciais**: utilizar a predefinição de Olá "pelo browser do web".
    - **Tipo de autenticação**: escolha Olá tipo de autenticação que está a utilizar.
    - **Nome de utilizador** e **palavra-passe**: introduza o nome de utilizador Olá e a palavra-passe para um utilizador que tem permissão toocopy Olá dados.

    ![Inicie a configuração rápida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. Olá passo seguinte consiste em tabelas de Olá toochoose que dados de Olá toocopy. Pode filtrar as tabelas de Olá através da utilização de palavras-chave. E pode pré-visualizar o esquema de dados e tabela de Olá no painel inferior de Olá. Depois de concluir a seleção, clique em **seguinte**.

    ![Selecionar tabelas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Configurar o destino de Olá, o SQL Data Warehouse

Agora, indique ao fábrica de dados sobre as informações de destino Olá.

1. As informações de ligação do SQL Data Warehouse é automaticamente preenchidas. Introduza a palavra-passe de Olá Olá nome de utilizador. e clique em **seguinte**.

    ![Configurar o destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Um mapeamento de tabela inteligente é apresentada que mapeia as tabelas de toodestination de origem com base nos nomes de tabela. Se a tabela de Olá não existe no destino Olá, por predefinição ADF irá criar uma com Olá mesmo nome (Isto aplica-se tooSQL servidor ou base de dados do Azure SQL Server como origem). Também pode escolher toomap tooan existente tabela. Reveja e clique em **seguinte**.

    ![Tabelas de mapa](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Reveja o mapeamento de esquema Olá e procurar erros ou mensagens de aviso. Mapeamento inteligente é baseado no nome da coluna. Se houver uma conversão de tipo de dados não suportados entre a coluna de origem e destino Olá, verá uma mensagem de erro em conjunto com a tabela correspondente Olá. Se escolher toolet automática de fábrica de dados criar tabelas de Olá, conversão de tipo de dados adequada pode ocorrer se for necessário incompatibilidade de Olá toofix entre os arquivos de origem e destino.

    ![Esquema de mapa](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Clique em **Seguinte**.

## <a name="configure-hello-performance-settings"></a>Configurar definições de desempenho de Olá
Configurações de desempenho de Olá, pode configura uma conta de armazenamento do Azure utilizada para dados de Olá de teste antes de que carrega para utilização do SQL Data Warehouse performantly [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Depois da conclusão da cópia de Olá, dados intermédio de Olá no armazenamento serão limpa automaticamente.

Selecione uma conta de armazenamento do Azure existente e clique em **seguinte**.

![Configurar o teste de blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Reveja as informações de resumo e implemente o pipeline de Olá

Reveja a configuração de Olá e clique em **concluir** pipeline do botão toodeploy Olá.

![Implementar a fábrica de dados](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Progresso de carregamento de dados de monitor

Pode ver o progresso da implementação Olá e resulta na Olá **implementação** página.

1. Depois de implementação de Olá é concluída, clique em ligação Olá **clique aqui o pipeline de cópia de toomonitor** dados toomonitor ao carregar o progresso.

    ![Monitorizar o pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Olá recém-criado **DWLoadData fromSQLServer** pipeline de carregamento de dados é automaticamente selecionada Olá esquerda **Explorador de recursos**.

    ![Pipeline de vista](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Clique no pipeline de Olá no meio de Olá Olá do painel toosee detalhadas de estado para cada tabela que mapeie tooan atividade.

    ![Atividade de tabela da vista](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Mais clique para uma atividade e ver dados Olá carregar os detalhes no painel à direita Olá, incluindo o tamanho dos dados, linhas, débito, etc.

    ![Ver detalhes de atividade de tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch Esta monitorização vista posterior, aceda tooyour do armazém de dados do SQL Server, clique **carga dados > Azure Data Factory**, selecione a fábrica e escolha **monitorizar existente a carregar tarefas**.

## <a name="next-steps"></a>Passos seguintes

toomigrate tooSQL a base de dados do armazém de dados, consulte [descrição geral da migração](sql-data-warehouse-overview-migrate.md).

toolearn mais informações sobre o Azure Data Factory e as respetivas capacidades do movimento de dados, consulte Olá seguintes artigos:

- [Introdução tooAzure fábrica de dados](../data-factory/data-factory-introduction.md)
- [Mover dados utilizando a atividade de cópia](../data-factory/data-factory-data-movement-activities.md)
- [Mover tooand de dados do armazém de dados SQL do Azure utilizando o Azure Data Factory](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore os dados no armazém de dados do SQL Server, consulte Olá os seguintes artigos:

- [Ligar tooSQL do armazém de dados com o Visual Studio e SSDT](sql-data-warehouse-query-visual-studio.md)
- [Dados do elemento visual com o Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).

<!-- Azure references -->
[portal do Azure]: https://portal.azure.com
