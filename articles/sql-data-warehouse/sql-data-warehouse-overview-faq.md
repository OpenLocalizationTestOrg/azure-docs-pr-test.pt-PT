---
title: aaaAzure SQL Data Warehouse perguntas mais frequentes | Microsoft Docs
description: "Este artigo apresenta uma lista saída perguntas mais frequentes sobre o Azure SQL Data Warehouse de clientes e os programadores"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="09244-103">SQL Data Warehouse perguntas mais frequentes</span><span class="sxs-lookup"><span data-stu-id="09244-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="09244-104">Geral</span><span class="sxs-lookup"><span data-stu-id="09244-104">General</span></span>

<span data-ttu-id="09244-105">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-105">Q.</span></span> <span data-ttu-id="09244-106">O que oferecem armazém de dados do SQL Server para a segurança dos dados?</span><span class="sxs-lookup"><span data-stu-id="09244-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="09244-107">A.</span><span class="sxs-lookup"><span data-stu-id="09244-107">A.</span></span> <span data-ttu-id="09244-108">Armazém de dados do SQL Server oferece várias soluções para proteger dados, tais como o TDE e auditoria.</span><span class="sxs-lookup"><span data-stu-id="09244-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="09244-109">Para obter mais informações, consulte [segurança].</span><span class="sxs-lookup"><span data-stu-id="09244-109">For more information, see [Security].</span></span>

<span data-ttu-id="09244-110">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-110">Q.</span></span> <span data-ttu-id="09244-111">Onde posso encontrar as normas legais ou horário comercial é o armazém de dados do SQL em conformidade com?</span><span class="sxs-lookup"><span data-stu-id="09244-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="09244-112">A.</span><span class="sxs-lookup"><span data-stu-id="09244-112">A.</span></span> <span data-ttu-id="09244-113">Visite Olá [Microsoft Compliance] página para vários ofertas de compatibilidade ao produto, tais como certificados SOC e ISO.</span><span class="sxs-lookup"><span data-stu-id="09244-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="09244-114">Primeiro escolha ao título de conformidade, em seguida expanda Azure Olá no âmbito do Microsoft cloud services secção no lado direito de Olá Olá página toosee os serviços que estão a serviços do Azure está em conformidade.</span><span class="sxs-lookup"><span data-stu-id="09244-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="09244-115">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-115">Q.</span></span> <span data-ttu-id="09244-116">Posso ligar o Power BI?</span><span class="sxs-lookup"><span data-stu-id="09244-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="09244-117">A.</span><span class="sxs-lookup"><span data-stu-id="09244-117">A.</span></span> <span data-ttu-id="09244-118">Sim!</span><span class="sxs-lookup"><span data-stu-id="09244-118">Yes!</span></span> <span data-ttu-id="09244-119">Embora o Power BI suporta a consulta direta com o armazém de dados do SQL Server, não destina grande número de utilizadores ou dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="09244-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="09244-120">Para utilização em produção PowerBI, recomendamos que utilize PowerBI por cima do Azure Analysis Services ou IaaS de serviço do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="09244-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="09244-121">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-121">Q.</span></span> <span data-ttu-id="09244-122">Quais são os limites de capacidade do SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="09244-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="09244-123">A.</span><span class="sxs-lookup"><span data-stu-id="09244-123">A.</span></span> <span data-ttu-id="09244-124">Consulte o nosso atual [os limites de capacidade] página.</span><span class="sxs-lookup"><span data-stu-id="09244-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="09244-125">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-125">Q.</span></span> <span data-ttu-id="09244-126">Por que motivo o meu escala/pausa/retomar demorar tempo?</span><span class="sxs-lookup"><span data-stu-id="09244-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="09244-127">A.</span><span class="sxs-lookup"><span data-stu-id="09244-127">A.</span></span> <span data-ttu-id="09244-128">Vários fatores podem influenciar a hora de Olá para operações de gestão de computação.</span><span class="sxs-lookup"><span data-stu-id="09244-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="09244-129">Um comuns maiúsculas e minúsculas para operações de execução longa é transacional reversão.</span><span class="sxs-lookup"><span data-stu-id="09244-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="09244-130">Quando é iniciada uma operação de escala ou de pausa, todas as sessões de entrada estão bloqueadas e consultas são drained.</span><span class="sxs-lookup"><span data-stu-id="09244-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="09244-131">Em ordem tooleave Olá do sistema num estado estável, transações tem de ser revertidas novamente antes de pode começar uma operação.</span><span class="sxs-lookup"><span data-stu-id="09244-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="09244-132">Olá maior número de Olá e maior tamanho Olá do registo de transações, operação de Olá mais Olá será parada restaurar Olá tooa estável do Estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="09244-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="09244-133">Suporte de utilizador</span><span class="sxs-lookup"><span data-stu-id="09244-133">User support</span></span>

<span data-ttu-id="09244-134">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-134">Q.</span></span> <span data-ttu-id="09244-135">Tenho um pedido de funcionalidade, onde submetê-las?</span><span class="sxs-lookup"><span data-stu-id="09244-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="09244-136">A.</span><span class="sxs-lookup"><span data-stu-id="09244-136">A.</span></span> <span data-ttu-id="09244-137">Se tiver um pedido de funcionalidade, submetê-las no nosso [UserVoice] página</span><span class="sxs-lookup"><span data-stu-id="09244-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="09244-138">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-138">Q.</span></span> <span data-ttu-id="09244-139">Como posso fazer x?</span><span class="sxs-lookup"><span data-stu-id="09244-139">How can I do x?</span></span>

<span data-ttu-id="09244-140">A.</span><span class="sxs-lookup"><span data-stu-id="09244-140">A.</span></span> <span data-ttu-id="09244-141">Para obter ajuda na programar com o SQL Data Warehouse, pode colocar perguntas no nosso [Stack Overflow] página.</span><span class="sxs-lookup"><span data-stu-id="09244-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="09244-142">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-142">Q.</span></span> <span data-ttu-id="09244-143">Como posso submeter um pedido de suporte?</span><span class="sxs-lookup"><span data-stu-id="09244-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="09244-144">A.</span><span class="sxs-lookup"><span data-stu-id="09244-144">A.</span></span> <span data-ttu-id="09244-145">[Pedidos de suporte] pode ser registada através do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09244-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="09244-146">Suporte de idioma/funcionalidades do SQL Server</span><span class="sxs-lookup"><span data-stu-id="09244-146">SQL language/feature support</span></span> 

<span data-ttu-id="09244-147">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-147">Q.</span></span> <span data-ttu-id="09244-148">Que tipos de dados suporta o SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="09244-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="09244-149">A.</span><span class="sxs-lookup"><span data-stu-id="09244-149">A.</span></span> <span data-ttu-id="09244-150">Consulte o SQL Data Warehouse [tipos de dados].</span><span class="sxs-lookup"><span data-stu-id="09244-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="09244-151">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-151">Q.</span></span> <span data-ttu-id="09244-152">Quais as funcionalidades de tabela suportam?</span><span class="sxs-lookup"><span data-stu-id="09244-152">What table features do you support?</span></span>

<span data-ttu-id="09244-153">A.</span><span class="sxs-lookup"><span data-stu-id="09244-153">A.</span></span> <span data-ttu-id="09244-154">Enquanto o armazém de dados SQL suporta muitas funcionalidades, algumas não são suportadas e estão documentadas em [funcionalidades não suportadas de tabela].</span><span class="sxs-lookup"><span data-stu-id="09244-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="09244-155">Ferramentas e administração</span><span class="sxs-lookup"><span data-stu-id="09244-155">Tooling and administration</span></span>

<span data-ttu-id="09244-156">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-156">Q.</span></span> <span data-ttu-id="09244-157">Suporta projetos de base de dados no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09244-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="09244-158">A.</span><span class="sxs-lookup"><span data-stu-id="09244-158">A.</span></span> <span data-ttu-id="09244-159">Atualmente não suportamos projetos de base de dados no Visual Studio para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09244-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="09244-160">Se quiser toocast tooget um voto esta funcionalidade, visite a nossa voz do utilizador [projetos de base de dados de funcionalidade pedido].</span><span class="sxs-lookup"><span data-stu-id="09244-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="09244-161">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-161">Q.</span></span> <span data-ttu-id="09244-162">Armazém de dados SQL suporta REST APIs?</span><span class="sxs-lookup"><span data-stu-id="09244-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="09244-163">A.</span><span class="sxs-lookup"><span data-stu-id="09244-163">A.</span></span> <span data-ttu-id="09244-164">Sim.</span><span class="sxs-lookup"><span data-stu-id="09244-164">Yes.</span></span> <span data-ttu-id="09244-165">A maioria das funcionalidades REST que podem ser utilizada com a base de dados do SQL Server também estão disponível no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09244-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="09244-166">Pode encontrar informações de API dentro páginas da documentação de REST ou [MSDN].</span><span class="sxs-lookup"><span data-stu-id="09244-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="09244-167">A carregar</span><span class="sxs-lookup"><span data-stu-id="09244-167">Loading</span></span>

<span data-ttu-id="09244-168">Q.</span><span class="sxs-lookup"><span data-stu-id="09244-168">Q.</span></span> <span data-ttu-id="09244-169">Os controladores cliente que suportam?</span><span class="sxs-lookup"><span data-stu-id="09244-169">What client drivers do you support?</span></span>

<span data-ttu-id="09244-170">A.</span><span class="sxs-lookup"><span data-stu-id="09244-170">A.</span></span> <span data-ttu-id="09244-171">Suporte de controladores para o armazém de dados pode ser encontrado no Olá [cadeias de ligação] página</span><span class="sxs-lookup"><span data-stu-id="09244-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="09244-172">P: quais formatos de ficheiro são suportados pelo PolyBase com o SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="09244-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="09244-173">R: Orc, RC, Parquet e simples texto delimitado</span><span class="sxs-lookup"><span data-stu-id="09244-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="09244-174">P: o que pode ligar armazém de dados do SQL Server toofrom utilizando o PolyBase?</span><span class="sxs-lookup"><span data-stu-id="09244-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="09244-175">R: [do Azure Data Lake Store] e [Blobs de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="09244-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="09244-176">P: é possível pushdown de cálculo ao ligar tooAzure Blobs de armazenamento ou ADLS?</span><span class="sxs-lookup"><span data-stu-id="09244-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="09244-177">R: não, o PolyBase de armazém de dados do SQL Server interage apenas componentes de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="09244-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="09244-178">P: posso ligar tooHDI?</span><span class="sxs-lookup"><span data-stu-id="09244-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="09244-179">R: HDI pode utilizar ADLS ou WASB como camada HDFS Olá.</span><span class="sxs-lookup"><span data-stu-id="09244-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="09244-180">Se tiver como a camada HDFS, pode carregar os dados no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="09244-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="09244-181">No entanto, não é possível gerar instância do pushdown cálculo toohello HDI.</span><span class="sxs-lookup"><span data-stu-id="09244-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="09244-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="09244-182">Next steps</span></span>
<span data-ttu-id="09244-183">Para obter mais informações no armazém de dados do SQL Server como um todo, consulte a nossa [descrição geral] página.</span><span class="sxs-lookup"><span data-stu-id="09244-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[cadeias de ligação]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Pedidos de suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md
[segurança]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[os limites de capacidade]: ./sql-data-warehouse-service-capacity-limits.md
[tipos de dados]: ./sql-data-warehouse-tables-data-types.md
[funcionalidades não suportadas de tabela]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[do Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Blobs de armazenamento do Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[projetos de base de dados de funcionalidade pedido]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[descrição geral]: ./sql-data-warehouse-overview-faq.md