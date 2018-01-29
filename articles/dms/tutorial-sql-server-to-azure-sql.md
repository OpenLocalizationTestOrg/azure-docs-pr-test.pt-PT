---
title: "Utilizar o serviço de migração de base de dados do Azure para migrar o SQL Server a SQL Database do Azure | Microsoft Docs"
description: "Saiba como migrar a partir do SQL Server no local para o Azure SQL, utilizando o serviço de migração de base de dados do Azure."
services: dms
author: HJToland3
ms.author: jtoland
manager: jhubbard
ms.reviewer: 
ms.service: dms
ms.workload: data-services
ms.custom: mvc, tutorial
ms.topic: article
ms.date: 01/24/2018
ms.openlocfilehash: 8dc8b4db80d5e319fad0b681924ab5a8e5642b2e
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/25/2018
---
# <a name="migrate-sql-server-to-azure-sql-database"></a>Migrar o servidor SQL para a base de dados SQL do Azure
Pode utilizar o serviço de migração de base de dados do Azure para migrar as bases de dados de uma instância do SQL Server no local para a SQL Database do Azure. Neste tutorial, migra a **Adventureworks2012** base de dados restaurada para uma instância no local do SQL Server 2016 (ou superior) para uma base de dados do SQL do Azure utilizando o serviço de migração de base de dados do Azure.

Neste tutorial, ficará a saber como:
> [!div class="checklist"]
> * Avalie a sua base de dados no local utilizando o Assistente de migração de dados.
> * Migre o esquema de exemplo, utilizando o Assistente de migração de dados.
> * Crie uma instância do serviço de migração de base de dados do Azure.
> * Crie um projeto de migração utilizando o serviço de migração de base de dados do Azure.
> * Execute a migração.
> * Monitorize a migração.

## <a name="prerequisites"></a>Pré-requisitos
Para concluir este tutorial, precisa de:

- Transfira e instale [SQL Server 2016 ou posterior](https://www.microsoft.com/sql-server/sql-server-downloads) (qualquer edição).
- Ative o protocolo TCP/IP, que está desativado por predefinição durante a instalação do SQL Server Express, ao seguir as instruções no artigo [ativar ou desativar um protocolo de rede do servidor](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).
- Criar uma instância de instância de SQL Database do Azure, o que fazer, seguindo o detalhe no artigo [criar uma base de dados SQL do Azure no portal do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).
- Transfira e instale o [Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 ou posterior.
- Criar uma VNET para o serviço de migração de base de dados do Azure utilizando o modelo de implementação Azure Resource Manager, que fornece a conectividade de site a site para os seus servidores de origem no local através de um [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) ou [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).
- Certifique-se de que a sua escolha de regras do Azure (VNET) rede segurança grupo de rede Virtual bloquear a comunicação seguinte portas 443, 53, 9354, 445, 12000. Para mais detalhes sobre a filtragem de tráfego do Azure VNET NSG, consulte o artigo [filtrar o tráfego de rede com grupos de segurança de rede](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-nsg).
- Configurar o seu [Firewall do Windows para acesso ao motor de base de dados](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).
- Abra a firewall do Windows para permitir que o serviço de migração de base de dados do Azure para aceder à origem de SQL Server.
- Quando utilizar uma aplicação de firewall à frente da sua bases de dados de origem, poderá ter de adicionar regras de firewall para permitir que o serviço de migração de base de dados do Azure para aceder a bases de dados de origem para migração.
- Criar um nível de servidor [regra de firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) para o servidor da SQL Database do Azure permitir o acesso de serviço de migração de base de dados do Azure para as bases de dados de destino. Forneça o intervalo de sub-rede da VNET utilizado para o serviço de migração de base de dados do Azure.
- Certifique-se de que as credenciais utilizadas para ligar à instância do SQL Server de origem têm [controlo servidor](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permissões.
- Certifique-se de que as credenciais utilizadas para ligar à instância de SQL Database do Azure de destino tem a permissão controlar base de dados nas bases de dados de SQL do Azure de destino.

## <a name="assess-your-on-premises-database"></a>Avaliar a sua base de dados no local
Antes de poder migrar dados a partir de uma instância do SQL Server no local para a SQL Database do Azure, terá de avaliar a base de dados do SQL Server para quaisquer problemas de bloqueio que possam impedir a migração. O Assistente de migração de dados v3.3 ou posterior, siga os passos descritos no artigo [efetuar uma avaliação de migração do SQL Server](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem) para concluir no local da base de dados avaliação. Segue um resumo dos passos necessários:
1.  No Assistente de migração de dados, selecione o ícone de novo (+) e, em seguida, selecione o **avaliação** o tipo de projeto.
2.  Especifique um nome de projeto, no **tipo de servidor de origem** caixa de texto, selecione **do SQL Server**e, em seguida, no **tipo de servidor de destino** caixa de texto, selecione **SQL do Azure Base de dados**.
3.  Selecione **criar** para criar o projeto.

    Quando estiver a avaliar a origem do SQL Server da base de dados a migrar para a SQL Database do Azure, pode escolher um ou ambos dos seguintes tipos de relatório de avaliação:
    - Verificar a compatibilidade da base de dados
    - Paridade da funcionalidade de verificação

    Ambos os tipos de relatório estão selecionados por predefinição.
4.  No Assistente de migração de dados, no **opções** ecrã, selecione **seguinte**.
5.  No **selecione origens** no ecrã o **ligar a um servidor** , forneça os detalhes de ligação ao SQL Server e, em seguida, selecione **Connect**.
6.  No **adicionar origens** caixa de diálogo, selecione **AdventureWorks2012**, selecione **adicionar**e, em seguida, selecione **iniciar avaliação**.

    Quando estiver concluída a avaliação, apresentam os resultados conforme mostrado no seguinte gráfico:

    ![Avaliar a migração de dados](media\tutorial-sql-server-to-azure-sql\dma-assessments.png)

    Para a base de dados SQL do Azure, as avaliações de identificam problemas de bloqueio de migração e problemas de paridade da funcionalidade.

7.  Reveja os resultados da avaliação para problemas de bloqueio de migração e problemas de paridade da funcionalidade selecionando as opções específicas.
    - O **paridade de funcionalidades do SQL Server** categoria fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure, e mitigar os passos para o ajudar a planear o esforço do utilizador para os projetos de migração.
    - O **problemas de compatibilidade** categoria identifica parcialmente suportada ou funcionalidades não suportadas que refletem a problemas de compatibilidade, que poderão bloquear Migrar bases de SQL Server no local dados para a SQL Database do Azure. Recomendações também são fornecidas para o ajudar a resolver esses problemas.


## <a name="migrate-the-sample-schema"></a>Migrar o esquema de exemplo
Depois de estiver familiarizado com a avaliação e estiver satisfeito que a base de dados selecionada é um bom candidato para a migração para a SQL Database do Azure, utilize o Assistente de migração de dados para migrar o esquema para a SQL Database do Azure.

> [!NOTE]
> Antes de criar um projeto de migração no Assistente de migração de dados, lembre-se de que já aprovisionou uma base de dados SQL do Azure tal como mencionado nos pré-requisitos. Para efeitos deste tutorial, o nome da base de dados do SQL do Azure é prestado **AdventureWorksAzure**, mas pode atribuir o nome forma diferente se desejar.

Para migrar o **AdventureWorks2012** esquema para a base de dados SQL do Azure, execute os seguintes passos:

1.  No Assistente de migração de dados, selecione o ícone de novo (+) e, em **o tipo de projeto**, selecione **migração**.
3.  Especifique um nome de projeto, no **tipo de servidor de origem** caixa de texto, selecione **do SQL Server**e, em seguida, no **tipo de servidor de destino** caixa de texto, selecione **SQL do Azure Base de dados**.
4.  Em **migração âmbito**, selecione **apenas o esquema**.

    Depois de efetuar os passos anteriores, a interface de Assistente de migração de dados deve aparecer conforme mostrado no seguinte gráfico:
    
    ![Criar projeto através do Assistente de migração de dados](media\tutorial-sql-server-to-azure-sql\dma-create-project.png)

5.  Selecione **criar** para criar o projeto.
6.  No Assistente de migração de dados, especifique os detalhes de ligação de origem para o SQL Server, selecione **Connect**e, em seguida, selecione o **AdventureWorks2012** base de dados.

    ![Detalhes de ligação de origem através do Assistente de migração de dados](media\tutorial-sql-server-to-azure-sql\dma-source-connect.png)
7.  Selecione **seguinte**, em **ligar ao servidor de destino**, especifique os detalhes de ligação de destino para a base de dados SQL do Azure, selecione **Connect**e, em seguida, selecione o **AdventureWorksAzure** base de dados previamente tinha sido aprovisionadas na base de dados SQL do Azure.

    ![Detalhes de ligação de destino através do Assistente de migração de dados](media\tutorial-sql-server-to-azure-sql\dma-target-connect.png)
8.  Selecione **seguinte** para avançar para o **selecionar objetos** ecrã, onde pode especificar os objetos de esquema no **AdventureWorks2012** base de dados que têm de ser implementada no Azure Base de dados do SQL Server.

    Por predefinição, são selecionados todos os objetos.

    ![Gerar Scripts SQL](media\tutorial-sql-server-to-azure-sql\dma-assessment-source.png)
9.  Selecione **script SQL gerar** para criar os scripts de SQL e, em seguida, reveja os scripts de eventuais erros.

    ![Script de esquema](media\tutorial-sql-server-to-azure-sql\dma-schema-script.png)
10. Selecione **implementar esquema** para implementar o esquema SQL Database do Azure e, em seguida, depois de implementar o esquema, verifique o servidor de destino para qualquer anomalias.

    ![Implementar o esquema](media\tutorial-sql-server-to-azure-sql\dma-schema-deploy.png)

## <a name="register-the-microsoftdatamigration-resource-provider"></a>Registar o fornecedor de recursos Microsoft.DataMigration
1. Inicie sessão no portal do Azure, selecione **todos os serviços**e, em seguida, selecione **subscrições**.
 
   ![Mostrar subscrições portais](media\tutorial-sql-server-to-azure-sql\portal-select-subscription.png)
       
2. Selecione a subscrição na qual pretende criar a instância do Database Migration Service do Azure e, em seguida, selecione **Fornecedores de recursos**.
 
    ![Mostrar os fornecedores de recursos](media\tutorial-sql-server-to-azure-sql\portal-select-resource-provider.png)    
3.  Pesquisa para a migração e, em seguida, à direita do **Microsoft.DataMigration**, selecione **registar**.
 
    ![Registar o fornecedor de recursos](media\tutorial-sql-server-to-azure-sql\portal-register-resource-provider.png)    


## <a name="create-an-instance"></a>Criar uma instância
1.  No portal do Azure, selecione **+ criar um recurso**, procure o serviço de migração de base de dados do Azure e, em seguida, selecione **serviço de migração de base de dados do Azure** na lista pendente.

    ![Azure Marketplace](media\tutorial-sql-server-to-azure-sql\portal-marketplace.png)
2.  No **serviço de migração de base de dados do Azure (pré-visualização)** ecrã, selecione **criar**.
 
    ![Criar uma instância de serviço de migração de base de dados do Azure](media\tutorial-sql-server-to-azure-sql\dms-create.png)
  
3.  No **serviço de migração de base de dados** ecrã, especifique um nome para o serviço, a subscrição, uma rede virtual e o escalão de preço.

    Para obter mais informações sobre os custos e escalões de preços, consulte o [página de preços](https://aka.ms/dms-pricing).

     ![Configurar as definições de instância de serviço de migração de base de dados do Azure](media\tutorial-sql-server-to-azure-sql\dms-settings.png)

4.  Selecione **criar** ao criar o serviço.

## <a name="create-a-migration-project"></a>Criar um projeto de migração
Depois de criar o serviço, localizá-la no portal do Azure e, em seguida, criar um projeto de migração.
1. No portal do Azure, selecione **todos os serviços**, procure o serviço de migração de base de dados do Azure e, em seguida, selecione **serviços de migração de base de dados do Azure**.
 
      ![Localizar todas as instâncias do serviço de migração de base de dados do Azure](media\tutorial-sql-server-to-azure-sql\dms-search.png)
2. No **serviços de migração de base de dados do Azure** ecrã, procure o nome do DMS Azure instância que criou e, em seguida, selecione a instância.
 
     ![Localizar a instância do serviço de migração de base de dados do Azure](media\tutorial-sql-server-to-azure-sql\dms-instance-search.png)
 
3. Selecione **+ novo projeto de migração**.
4. No **novo projeto de migração** ecrã, especifique um nome para o projeto no **tipo de servidor de origem** caixa de texto, selecione **do SQL Server**e, em seguida, no **destino tipo de servidor** caixa de texto, selecione **SQL Database do Azure**.

    ![Criar projeto do serviço de migração de base de dados](media\tutorial-sql-server-to-azure-sql\dms-create-project.png)

5.  Selecione **criar** para criar o projeto.


## <a name="specify-source-details"></a>Especifique os detalhes de origem
1. No **origem detalhes** ecrã, especifique os detalhes de ligação para a origem de SQL Server.

    ![Selecione a origem](media\tutorial-sql-server-to-azure-sql\dms-select-source.png)

2. Selecione **guardar**e, em seguida, selecione o **AdventureWorks2012** base de dados para migração.

    ![Selecione a base de dados de origem](media\tutorial-sql-server-to-azure-sql\dms-select-source-db.png)

## <a name="specify-target-details"></a>Especifique os detalhes de destino
1. Selecione **guardar**e, em seguida, no **detalhes de destino** ecrã, especifique os detalhes de ligação para o destino, o que é pré-aprovisionada SQL Database do Azure para o qual o **AdventureWorks2012**  esquema foi implementado utilizando o Assistente de migração de dados.

    ![Selecione o destino](media\tutorial-sql-server-to-azure-sql\dms-select-target.png)

2. Selecione **guardar** para guardar o projeto.
3. No **resumo de migração** ecrã, reveja e verifique os detalhes associados ao projeto de migração.

    ![O DMS resumo](media\tutorial-sql-server-to-azure-sql\dms-summary.png)

4. Selecione **Guardar**.

## <a name="run-the-migration"></a>Executar a migração
1.  Selecione o projeto guardado recentemente, selecione **+ nova atividade**e, em seguida, selecione **executar a migração de dados**.

    ![Nova atividade](media\tutorial-sql-server-to-azure-sql\dms-new-activity.png)

2.  Quando lhe for pedido, introduza as credenciais para a origem e os servidores de destino e, em seguida, selecione **guardar**.
3.  No **mapa para bases de dados de destino** ecrã, mapear a origem e a base de dados de destino para migração.

    Se a base de dados de destino contém o mesmo nome de base de dados que a base de dados de origem, o Azure DMS seleciona a base de dados de destino por predefinição.

    ![Mapear para bases de dados de destino](media\tutorial-sql-server-to-azure-sql\dms-map-targets-activity.png)

4. Selecione **guardar**, no **selecionar tabelas** ecrã, expanda a lista de tabela e reveja a lista de campos afetados.

    ![Selecionar tabelas](media\tutorial-sql-server-to-azure-sql\dms-configure-setting-activity.png)

5.  Selecione **guardar**, no **resumo de migração** no ecrã o **nome da atividade** texto caixa, especifique um nome para a atividade de migração.

    Neste ecrã, também pode expandir o **escolher a opção de validação** ecrã, que pode utilizar para especificar a validar a base de dados migrado para:
    - Esquema
    - Consistência dos dados
    - Correção de consulta e de desempenho

    ![Escolha a opção de validação](media\tutorial-sql-server-to-azure-sql\dms-configuration.png)

6.  Selecione **guardar**, reveja o resumo para se certificar de que os detalhes de origem e de destino corresponde ao que é especificado.

    ![Resumo de migração](media\tutorial-sql-server-to-azure-sql\dms-run-migration.png)

7.  Selecione **executar migração** para iniciar a atividade de migração e, em seguida, selecione **atualizar** para rever o estado atual.

    ![Estado da Atividade](media\tutorial-sql-server-to-azure-sql\dms-activity-status.png)

## <a name="monitor-the-migration"></a>Monitorizar a migração
1. Selecione a atividade de migração para rever o estado da atividade.
2. Certifique-se a base de dados do SQL do Azure de destino após a migração estar concluída.

    ![Concluída](media\tutorial-sql-server-to-azure-sql\dms-completed-activity.png)
