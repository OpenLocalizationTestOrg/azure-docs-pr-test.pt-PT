---
title: "aaaRestore uma única tabela de cópia de segurança de SQL Database do Azure | Microsoft Docs"
description: "Saiba como toorestore uma única tabela de cópia de segurança de SQL Database do Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="f48fa-103">Como toorestore uma única tabela de uma cópia de segurança de SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="f48fa-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="f48fa-104">Poderá encontrar uma situação em que modificou acidentalmente alguns dados na base de dados SQL e agora pretende toorecover Olá única afetados tabela.</span><span class="sxs-lookup"><span data-stu-id="f48fa-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="f48fa-105">Este artigo descreve como toorestore uma única tabela numa base de dados a partir de um Olá base de dados SQL [cópias de segurança automáticas](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="f48fa-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="f48fa-106">Passos de preparação: mudar o nome da tabela de Olá e restaurar uma cópia da base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="f48fa-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="f48fa-107">Identifica a tabela de Olá na base de dados SQL do Azure que pretende que o tooreplace com cópia Olá restaurada.</span><span class="sxs-lookup"><span data-stu-id="f48fa-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="f48fa-108">Utilize a tabela do Microsoft SQL Server Management Studio toorename Olá.</span><span class="sxs-lookup"><span data-stu-id="f48fa-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="f48fa-109">Por exemplo, mudar o nome da tabela de Olá como &lt;nome da tabela&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="f48fa-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f48fa-110">tooavoid a ser bloqueado, certifique-se de que não há nenhuma atividade em execução na tabela de Olá que são mudar o nome.</span><span class="sxs-lookup"><span data-stu-id="f48fa-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="f48fa-111">Se ocorrerem problemas, certifique-se de que efetuar este procedimento durante uma janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="f48fa-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="f48fa-112">Restaurar uma cópia de segurança da sua base de dados tooa ponto no tempo que pretende que o toorecover toousing Olá [ponto-In_Time restaurar](sql-database-recovery-using-backups.md#point-in-time-restore) passos.</span><span class="sxs-lookup"><span data-stu-id="f48fa-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f48fa-113">nome de Olá da base de dados de Olá restaurada vai estar no formato de DBName + TimeStamp de Olá; Por exemplo, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="f48fa-114">Este passo não substituir o nome da base de dados existente Olá no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="f48fa-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="f48fa-115">Esta é uma medida de segurança e destina-se tooallow Olá tooverify restaurar base de dados antes de serem remover respetiva base de dados atual e mudar o nome da base de dados de Olá restaurado para utilização em produção.</span><span class="sxs-lookup"><span data-stu-id="f48fa-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="f48fa-116">Copiar Olá tabela da Olá restaurar base de dados utilizando a ferramenta de migração de base de dados do SQL Server Olá</span><span class="sxs-lookup"><span data-stu-id="f48fa-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="f48fa-117">Transfira e instale Olá [Assistente de migração de base de dados do SQL Server](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="f48fa-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="f48fa-118">Abra Olá Assistente de migração da base de dados SQL no Olá **selecione processo** página, selecione **base de dados em analisar/migrar**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Assistente de migração de base de dados do SQL Server - selecione processo](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="f48fa-120">No Olá **ligar tooServer** diálogo caixa, aplicar Olá seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="f48fa-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="f48fa-121">Nome do servidor: **do seu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="f48fa-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="f48fa-122">Autenticação: **autenticação do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="f48fa-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="f48fa-123">Início de sessão: **o início de sessão**</span><span class="sxs-lookup"><span data-stu-id="f48fa-123">Login: **Your login**</span></span>
   * <span data-ttu-id="f48fa-124">Palavra-passe: **a palavra-passe**</span><span class="sxs-lookup"><span data-stu-id="f48fa-124">Password: **Your password**</span></span>
   * <span data-ttu-id="f48fa-125">Base de dados: **Master DB (lista de todas as bases de dados)**</span><span class="sxs-lookup"><span data-stu-id="f48fa-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f48fa-126">Por predefinição, o Assistente de Olá guarda as informações de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="f48fa-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="f48fa-127">Se não pretender que ele, selecione **se esqueça de informações de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Passo de migração de base de dados SQL do assistente - selecionar origem de - 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="f48fa-129">No Olá **selecionar origem** caixa de diálogo, nome de base de dados de Olá selecione restaurada de Olá **passos de preparação** secção como a origem e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Passo de migração de base de dados SQL do assistente - selecionar origem - 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="f48fa-131">No Olá **escolha objetos** caixa de diálogo, selecione de Olá **selecionar objetos de base de dados específica** opção e, em seguida, selecione table(or tables) Olá que pretende que o servidor de destino toomigrate toohello.</span><span class="sxs-lookup"><span data-stu-id="f48fa-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="f48fa-132">![Assistente de migração de base de dados do SQL Server - escolha objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="f48fa-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="f48fa-133">No Olá **resumo do Assistente de Script** página, clique em **Sim** quando lhe for pedida sobre se estiver pronto toogenerate um script do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f48fa-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="f48fa-134">Também tem Olá opção toosave Olá TSQL Script para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="f48fa-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="f48fa-135">![Assistente de migração de base de dados do SQL Server - resumo do Assistente de Script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="f48fa-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="f48fa-136">No Olá **resumo de resultados** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="f48fa-137">![Assistente de migração de base de dados do SQL Server - resumo de resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="f48fa-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="f48fa-138">No Olá **configurar a ligação ao servidor de destino** página, clique em **ligar tooServer**e, em seguida, introduza os detalhes de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f48fa-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="f48fa-139">**Nome do servidor**: instância de servidor de destino</span><span class="sxs-lookup"><span data-stu-id="f48fa-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="f48fa-140">**Autenticação**: **autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="f48fa-141">Introduza as credenciais de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="f48fa-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="f48fa-142">**Base de dados**: **Master DB (lista de todas as bases de dados)**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="f48fa-143">Esta opção apresenta uma lista de todas as bases de dados de Olá no servidor de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="f48fa-143">This option lists all hello databases on hello target server.</span></span>
     
     ![Assistente de migração de base de dados do SQL Server - configurar a ligação ao servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="f48fa-145">Clique em **Connect**, selecione base de dados do destino Olá que pretende tabela de Olá toomove para e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="f48fa-146">Isto deve ser concluída a executar o script Olá gerado anteriormente e deverá ver Olá movido recentemente a base de dados de destino de toohello copiados de tabela.</span><span class="sxs-lookup"><span data-stu-id="f48fa-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="f48fa-147">Passo de verificação</span><span class="sxs-lookup"><span data-stu-id="f48fa-147">Verification step</span></span>

- <span data-ttu-id="f48fa-148">Consulta e teste Olá recentemente copiados toomake tabela se de que os dados de Olá estão intactos.</span><span class="sxs-lookup"><span data-stu-id="f48fa-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="f48fa-149">Após a confirmação, pode remover o formulário de tabela Olá mudado **passos de preparação** secção.</span><span class="sxs-lookup"><span data-stu-id="f48fa-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="f48fa-150">(por exemplo, &lt;nome da tabela&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="f48fa-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f48fa-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f48fa-151">Next steps</span></span>
[<span data-ttu-id="f48fa-152">Cópias de segurança automáticas de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="f48fa-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

