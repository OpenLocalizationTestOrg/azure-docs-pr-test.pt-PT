---
title: aaaConnect Excel tooSQL da base de dados | Microsoft Docs
description: "Saiba como tooconnect Microsoft Excel tooAzure SQL da base de dados na nuvem de Olá. Importe dados para o Excel para criação de relatórios e exploração de dados."
services: sql-database
keywords: ligar toosql do excel, importe dados tooexcel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="979f8-105">Ligar o Excel tooan SQL database do Azure e criar um relatório</span><span class="sxs-lookup"><span data-stu-id="979f8-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="979f8-106">Ligar a base de dados do Excel tooa SQL na nuvem de Olá e importar dados e criar tabelas e gráficos com base nos valores na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="979f8-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="979f8-107">Neste tutorial, irá configurar a ligação de Olá entre o Excel e uma tabela de base de dados, guardar ficheiro Olá que armazena informações de ligação de dados e Olá para Excel e, em seguida, criar um gráfico dinâmico de Olá valores de base de dados.</span><span class="sxs-lookup"><span data-stu-id="979f8-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="979f8-108">Precisa de uma base de dados SQL no Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="979f8-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="979f8-109">Se não tiver uma, consulte o artigo [criar a sua primeira base de dados do SQL Server](sql-database-get-started-portal.md) tooget uma base de dados com dados de exemplo e funcional, em alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="979f8-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="979f8-110">Neste artigo, irá importar dados de exemplo para o Excel desse artigo, mas pode seguir passos semelhantes com os seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="979f8-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="979f8-111">Irá também precisar de uma cópia do Excel.</span><span class="sxs-lookup"><span data-stu-id="979f8-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="979f8-112">Este artigo utiliza o [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="979f8-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="979f8-113">Ligar a base de dados do Excel tooa SQL e criar um ficheiro odc</span><span class="sxs-lookup"><span data-stu-id="979f8-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="979f8-114">base de dados do tooSQL do Excel de tooconnect, abra o Excel e, em seguida, crie um novo livro ou abra um livro do Excel existente.</span><span class="sxs-lookup"><span data-stu-id="979f8-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="979f8-115">Na barra de menus de Olá na Olá parte superior da página Olá clique **dados**, clique em **de outras origens**e, em seguida, clique em **do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="979f8-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Origem de dados selecione: ligar a base de dados do Excel tooSQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="979f8-117">é aberto o Assistente de ligação de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="979f8-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="979f8-118">No Olá **ligar tooDatabase servidor** caixa de diálogo, Olá do tipo base de dados SQL **nome do servidor** pretende que o formulário do tooconnect tooin Olá <*servername* > **. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="979f8-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="979f8-119">Por exemplo, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="979f8-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="979f8-120">Em **iniciar sessão credenciais**, clique em **Olá de utilização seguintes nome de utilizador e palavra-passe**, Olá de tipo **nome de utilizador** e **palavra-passe** definido para a cópia de segurança Olá, servidor de base de dados SQL quando o criou e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="979f8-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Escreva as credenciais de início de sessão e nome do servidor de Olá](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="979f8-122">Dependendo do ambiente de rede, pode não ser capaz de tooconnect ou poderá perder a ligação de Olá se o servidor de base de dados SQL Olá não permite tráfego a partir do seu endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="979f8-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="979f8-123">Aceda toohello [portal do Azure](https://portal.azure.com/), clique em servidores SQL, clique no servidor, clique em firewall em definições e adicione o seu endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="979f8-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="979f8-124">Consulte [como definições de firewall tooconfigure](sql-database-configure-firewall-settings.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="979f8-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="979f8-125">No Olá **selecionar base de dados e tabela** caixa de diálogo, base de dados de Olá selecione pretende toowork com lista Olá e, em seguida, clique em tabelas de Olá ou vistas que pretende toowork com (Iremos escolher **vGetAllCategories**) e, em seguida, Clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="979f8-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selecione uma base de dados e a tabela.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="979f8-127">Olá **Guardar ficheiro de ligação de dados e termine** abre a caixa de diálogo, onde pode fornecer informações sobre Olá Office da base de dados (*.odc) ficheiro de ligação que o Excel utiliza.</span><span class="sxs-lookup"><span data-stu-id="979f8-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="979f8-128">Pode manter Olá predefinições ou personalizar as suas seleções.</span><span class="sxs-lookup"><span data-stu-id="979f8-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="979f8-129">Pode deixar as predefinições de Olá, mas Olá nota **nome de ficheiro** em particular.</span><span class="sxs-lookup"><span data-stu-id="979f8-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="979f8-130">A **Descrição**, um **nome amigável**, e **as palavras a procurar** ajudá-lo e outros utilizadores Lembre-se de está a ligar tooand localizar a ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="979f8-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="979f8-131">Clique em **sempre tentativa toouse estes dados de toorefresh ficheiro** se pretender que as informações de ligação armazenadas no ficheiro odc de Olá, para que possa atualizar quando ligar tooit e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="979f8-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![Guardar um ficheiro odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="979f8-133">Olá **importar dados** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="979f8-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="979f8-134">Importar dados de Olá para o Excel e criar um gráfico dinâmico</span><span class="sxs-lookup"><span data-stu-id="979f8-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="979f8-135">Agora que estabeleceu ligação Olá e ficheiro de Olá criada com as informações de ligação de dados e, está a ler dados de Olá tooimport.</span><span class="sxs-lookup"><span data-stu-id="979f8-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="979f8-136">No Olá **importar dados** caixa de diálogo, clique na opção de Olá que pretende para apresentar os dados na folha de cálculo de Olá e clique **OK**.</span><span class="sxs-lookup"><span data-stu-id="979f8-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="979f8-137">Vamos escolher **PivotChart**.</span><span class="sxs-lookup"><span data-stu-id="979f8-137">We chose **PivotChart**.</span></span> <span data-ttu-id="979f8-138">Também pode escolher toocreate um **nova folha de cálculo** ou demasiado**adicionar este tooa de dados modelo de dados**.</span><span class="sxs-lookup"><span data-stu-id="979f8-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="979f8-139">Para mais informações sobre Modelos de Dados, consulte [Criar um modelo de dados no Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="979f8-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="979f8-140">Clique em **propriedades** tooexplore informações sobre o ficheiro odc de Olá que criou no Olá passo e toochoose opções anteriores para atualizar os dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="979f8-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Escolher o formato de Olá para os dados no Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="979f8-142">folha de cálculo de Olá tem agora um gráfico e uma tabela dinâmicos em branco.</span><span class="sxs-lookup"><span data-stu-id="979f8-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="979f8-143">Em **campos PivotTable**, selecione Olá todas as caixas de verificação para Olá campos que pretende tooview.</span><span class="sxs-lookup"><span data-stu-id="979f8-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Configure o relatório de base de dados.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="979f8-145">Se quiser tooconnect outro Excel livros e folhas de cálculo toohello da base de dados, clique em **dados**, clique em **ligações**, clique em **adicionar**, escolha Olá ligação que criou na lista de Olá e, em seguida, clique em **abra**.</span><span class="sxs-lookup"><span data-stu-id="979f8-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="979f8-146">![Abrir uma ligação a partir de outro livro](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="979f8-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="979f8-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="979f8-147">Next steps</span></span>
* <span data-ttu-id="979f8-148">Saiba como demasiado[ligar tooSQL da base de dados com o SQL Server Management Studio](sql-database-connect-query-ssms.md) para consulta e análise avançadas.</span><span class="sxs-lookup"><span data-stu-id="979f8-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="979f8-149">Saiba mais sobre Olá vantagens de [conjuntos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="979f8-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="979f8-150">Saiba como demasiado[criar uma aplicação web que estabelece ligação tooSQL da base de dados no back-end de Olá](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="979f8-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

