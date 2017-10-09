---
title: "aaaCreate e gerir as tarefas elásticas com o PowerShell | Microsoft Docs"
description: PowerShell utilizado toomanage conjuntos de SQL Database do Azure
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="1b4f0-103">Criar e gerir tarefas elásticas da base de dados do SQL Server através do PowerShell (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="1b4f0-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="1b4f0-104">Olá das APIs do PowerShell para **tarefas de bases de dados elásticas** (em pré-visualização), permitem-lhe definir um grupo de bases de dados relativamente ao qual vai executar scripts.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="1b4f0-105">Este artigo mostra como toocreate e gerir **tarefas de bases de dados elásticas** utilizando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="1b4f0-106">Consulte [descrição geral das tarefas elásticas](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1b4f0-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b4f0-107">Prerequisites</span></span>
* <span data-ttu-id="1b4f0-108">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-108">An Azure subscription.</span></span> <span data-ttu-id="1b4f0-109">Para uma versão de avaliação gratuita, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1b4f0-110">Um conjunto de bases de dados criadas com ferramentas de base de dados elástica Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="1b4f0-111">Consulte [começar a utilizar as ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="1b4f0-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-112">Azure PowerShell.</span></span> <span data-ttu-id="1b4f0-113">Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="1b4f0-114">**As tarefas de base de dados elásticas** PowerShell pacote: consulte [tarefas de instalação de base de dados elástica](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="1b4f0-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="1b4f0-115">Selecione a sua subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="1b4f0-115">Select your Azure subscription</span></span>
<span data-ttu-id="1b4f0-116">subscrição de Olá tooselect tem o Id de subscrição (**- SubscriptionId**) ou o nome da subscrição (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="1b4f0-117">Se tiver várias subscrições podem executar Olá **Get-AzureRmSubscription** assim o desejar Olá cmdlet e copie as informações de subscrição do conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="1b4f0-118">Assim que tiver informações da sua subscrição, run Olá seguir commandlet tooset esta subscrição predefinida Olá, nomeadamente Olá destino para criar e gerir tarefas:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="1b4f0-119">Olá [ISE do PowerShell](https://technet.microsoft.com/library/dd315244.aspx) é recomendado para utilização toodevelop e executar scripts do PowerShell contra as tarefas de bases de dados elásticas Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="1b4f0-120">Objetos de tarefas de base de dados elásticos</span><span class="sxs-lookup"><span data-stu-id="1b4f0-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="1b4f0-121">Olá seguintes listas de tabela enviados todos os tipos de objeto de Olá de **tarefas de bases de dados elásticas** juntamente com a descrição e APIs relevantes do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="1b4f0-122">Tipo de objeto</span><span class="sxs-lookup"><span data-stu-id="1b4f0-122">Object Type</span></span></th>
    <th><span data-ttu-id="1b4f0-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="1b4f0-123">Description</span></span></th>
    <th><span data-ttu-id="1b4f0-124">APIs de PowerShell relacionados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="1b4f0-125">Credencial</span><span class="sxs-lookup"><span data-stu-id="1b4f0-125">Credential</span></span></td>
    <td><span data-ttu-id="1b4f0-126">Toouse de nome de utilizador e palavra-passe quando ligar toodatabases para aplicação de DACPACs ou execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="1b4f0-127">palavra-passe de Olá é encriptado antes de enviar tooand armazenar na base de dados do Olá as tarefas de base de dados elásticas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="1b4f0-128">palavra-passe de Olá é desencriptado pelo Olá serviço as tarefas de base de dados elásticas através de credencial de Olá criado e carregado a partir de script de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="1b4f0-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="1b4f0-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="1b4f0-130">Novo AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="1b4f0-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="1b4f0-131">Conjunto AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="1b4f0-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="1b4f0-132">Script</span><span class="sxs-lookup"><span data-stu-id="1b4f0-132">Script</span></span></td>
    <td><span data-ttu-id="1b4f0-133">Toobe de script de Transact-SQL utilizada para execução em bases de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="1b4f0-134">script de Olá deve ser idempotent toobe criados uma vez que o serviço de Olá irá repetir a execução do script Olá após falhas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="1b4f0-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="1b4f0-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="1b4f0-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="1b4f0-137">Novo AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="1b4f0-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="1b4f0-138">Conjunto AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="1b4f0-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="1b4f0-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="1b4f0-139">DACPAC</span></span></td>
    <td><span data-ttu-id="1b4f0-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplicação de camada de dados </a> toobe aplicada em bases de dados do pacote.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="1b4f0-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="1b4f0-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="1b4f0-142">Novo AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="1b4f0-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="1b4f0-143">Conjunto AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="1b4f0-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="1b4f0-144">Destino de base de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-144">Database Target</span></span></td>
    <td><span data-ttu-id="1b4f0-145">Base de dados e o servidor de nome indo tooan SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="1b4f0-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="1b4f0-147">Novo AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="1b4f0-148">Destino de mapa de partições horizontais</span><span class="sxs-lookup"><span data-stu-id="1b4f0-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="1b4f0-149">Combinação de um destino de base de dados e uma credencial toobe utilizar informações de toodetermine armazenadas dentro de um mapa de partições horizontais bases de dados elásticas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="1b4f0-151">Novo AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="1b4f0-152">Conjunto AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="1b4f0-153">Destino de recolha personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="1b4f0-154">Utilize definido grupo de bases de dados toocollectively para execução.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="1b4f0-156">Novo AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="1b4f0-157">Destino de subordinados de recolha personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="1b4f0-158">Destino de base de dados que é referenciado a partir de uma coleção personalizada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-159">AzureSqlJobChildTarget adicionar</span><span class="sxs-lookup"><span data-stu-id="1b4f0-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="1b4f0-160">Remover AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="1b4f0-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="1b4f0-161">Tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-162">Definição de parâmetros para uma tarefa que pode ser utilizado tootrigger execução ou toofulfill uma agenda.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="1b4f0-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="1b4f0-164">Novo AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="1b4f0-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="1b4f0-165">Conjunto AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="1b4f0-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="1b4f0-166">Execução da tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-167">Política de execução de tooan accordance processados contentor das tarefas toofulfill necessário executar um script ou aplicar um destino de tooa DACPAC utilizando as credenciais para ligações de base de dados com falhas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="1b4f0-169">Início AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="1b4f0-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="1b4f0-171">Espera-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="1b4f0-172">Tarefa a execução da tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-173">Única unidade de trabalho toofulfill uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="1b4f0-174">Se uma tarefa não for capaz de toosuccessfully executar, é registada a mensagem de exceção resultante Olá e uma nova tarefa correspondente será criada e executada na toohello accordance especificado política de execução.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="1b4f0-176">Início AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="1b4f0-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="1b4f0-178">Espera-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="1b4f0-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="1b4f0-179">Política de execução da tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-180">Controlos da tarefa tempos limite de execução, os limites de repetição e os intervalos entre tentativas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="1b4f0-181">As tarefas de base de dados elásticas inclui uma política de execução da tarefa ao predefinido que provocar essencialmente infinita tentativas de falhas de tarefas de tarefas com um término exponencial de intervalos entre cada tentativa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="1b4f0-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="1b4f0-183">Novo AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="1b4f0-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="1b4f0-184">Conjunto AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="1b4f0-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="1b4f0-185">Agenda</span><span class="sxs-lookup"><span data-stu-id="1b4f0-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-186">Hora baseada especificação para execução tootake local ou num intervalo reoccurring de uma única vez.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="1b4f0-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="1b4f0-188">Novo AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="1b4f0-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="1b4f0-189">Conjunto AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="1b4f0-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="1b4f0-190">Aciona a tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="1b4f0-191">Um mapeamento entre uma tarefa e uma execução da tarefa agenda tootrigger toohello agenda de acordo com.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="1b4f0-192">Novo AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="1b4f0-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="1b4f0-193">Remover AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="1b4f0-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="1b4f0-194">Tipos de grupo de tarefas de bases de dados elásticas suportadas</span><span class="sxs-lookup"><span data-stu-id="1b4f0-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="1b4f0-195">tarefa de Olá executa os scripts de Transact-SQL (T-SQL) ou a aplicação de DACPACs entre um grupo de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="1b4f0-196">Quando um trabalho é submetido toobe executado através de um grupo de bases de dados, a tarefa de Olá "expande" Olá para tarefas subordinadas em que cada uma desempenha Olá pediu para execução em relação a uma base de dados no grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="1b4f0-197">Existem dois tipos de grupos que pode criar:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="1b4f0-198">[Mapa de partições horizontais](sql-database-elastic-scale-shard-map-management.md) grupo: quando um trabalho for submetido tootarget um mapa de partições horizontais, tarefa Olá consulta toodetermine de mapa de partições horizontais Olá o conjunto atual de shards e, em seguida, cria subordinado tarefas para cada partição horizontal no mapa de partições horizontais Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="1b4f0-199">Grupo de recolha personalizado: personalizadas um conjunto de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="1b4f0-200">Quando uma tarefa está direcionada para uma coleção personalizada, cria subordinado tarefas para cada base de dados atualmente numa coleção personalizada Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="1b4f0-201">Olá tooset ligação de tarefas da base de dados elástica</span><span class="sxs-lookup"><span data-stu-id="1b4f0-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="1b4f0-202">Necessita de uma ligação toobe conjunto toohello tarefas *base de dados de controlo* toousing anterior Olá tarefas APIs.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="1b4f0-203">Executar este cmdlet aciona uma toopop de janela de credencial segurança pedir o nome de utilizador de Olá e a palavra-passe criado ao instalar as tarefas de bases de dados elásticas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="1b4f0-204">Todos os exemplos fornecidos neste tópico partem do princípio de que já foram realizado neste primeiro passo.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="1b4f0-205">Abra um tarefas de bases de dados elásticas toohello ligação:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="1b4f0-206">Credenciais encriptado dentro de tarefas de bases de dados elásticas Olá</span><span class="sxs-lookup"><span data-stu-id="1b4f0-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="1b4f0-207">As credenciais da base de dados podem ser inseridas no tarefas Olá *base de dados de controlo* com a respetiva palavra-passe encriptada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="1b4f0-208">É necessário toostore credenciais tooenable tarefas toobe executado num momento posterior, (utilizando as agendas de tarefas).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="1b4f0-209">Encriptação funciona através de um certificado que criou como parte do script de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="1b4f0-210">script de instalação de Olá cria e carregamentos Olá certificado para Olá o serviço em nuvem do Azure para a desencriptação de Olá armazenados encriptadas palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="1b4f0-211">Olá posteriormente para serviço de nuvem do Azure armazena a chave pública do Olá dentro tarefas Olá *base de dados de controlo* que lhe permite Olá de API do PowerShell ou o Portal clássico do Azure de tooencrypt de interface uma palavra-passe fornecida sem necessidade de certificado Olá toobe instalada localmente.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="1b4f0-212">as palavras-passe de credencial de Olá são encriptados e seguros a partir de utilizadores com objetos de tarefas da base de dados de tooElastic de acesso só de leitura.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="1b4f0-213">Mas é possível que um utilizador mal intencionado com acesso de leitura e escrita tooElastic tarefas de base de dados objetos tooextract uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="1b4f0-214">As credenciais são toobe concebida reutilizada em execuções de tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="1b4f0-215">As credenciais são transmitidas tootarget bases de dados quando estabelecer ligações.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="1b4f0-216">Não existem atualmente sem restrições nas bases de dados do destino de Olá utilizados para cada credencial, o utilizador mal intencionado pode adicionar um destino de base de dados para uma base de dados sob o controlo do utilizador mal intencionado Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="1b4f0-217">utilizador Olá, subsequentemente, foi possível iniciar uma tarefa direcionada para a palavra-passe do base de dados toogain Olá credenciais.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="1b4f0-218">Melhores práticas de segurança para tarefas de bases de dados elásticas incluem:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="1b4f0-219">Limitar a utilização de indivíduos de tootrusted Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="1b4f0-220">As credenciais devem ter Olá menos privilégios necessário tooperform Olá tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="1b4f0-221">Obter mais informações podem ser vistas nisto [autorização e permissões](https://msdn.microsoft.com/library/bb669084.aspx) artigo do MSDN do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="1b4f0-222">toocreate uma credencial encriptada para execução da tarefa em bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="1b4f0-223">toocreate encriptada de uma nova credencial, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) pede-lhe um nome de utilizador e palavra-passe que pode ser transmitido toohello [ **AzureSqlJobCredential novo cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="1b4f0-224">tooupdate credenciais</span><span class="sxs-lookup"><span data-stu-id="1b4f0-224">tooupdate credentials</span></span>
<span data-ttu-id="1b4f0-225">Quando alterar as palavras-passe, utilize Olá [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e conjunto Olá **CredentialName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="1b4f0-226">toodefine um destino de mapa de partições horizontais de base de dados elástica</span><span class="sxs-lookup"><span data-stu-id="1b4f0-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="1b4f0-227">tooexecute uma tarefa em todas as bases de dados de um conjunto de partições horizontais (criado utilizando [biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md)), utilize um mapa de partições horizontais como destino de base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="1b4f0-228">Este exemplo requer uma aplicação em partição horizontal criada utilizando a biblioteca de clientes de base de dados elástica Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="1b4f0-229">Consulte [introdução com exemplo de ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="1b4f0-230">base de dados do Olá partições horizontais mapa manager tem de ser definido como um destino de base de dados e, em seguida, o mapa de partições horizontais específico Olá deve ser especificado como um destino.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="1b4f0-231">Criar um Script T-SQL para execução em bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="1b4f0-232">Ao criar scripts T-SQL para execução, recomenda-se vivamente toobuild-los toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) e resilientes contra falhas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="1b4f0-233">As tarefas de base de dados elásticas irão repetir a execução de um script sempre que a execução detetar uma falha, independentemente da classificação de Olá de falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="1b4f0-234">Olá utilize [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate e guardar um script para execução e defina Olá **- ContentName** e **- CommandText**parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="1b4f0-235">Criar um script novo a partir de um ficheiro</span><span class="sxs-lookup"><span data-stu-id="1b4f0-235">Create a new script from a file</span></span>
<span data-ttu-id="1b4f0-236">Se Olá script T-SQL está definido no âmbito de um ficheiro, utilize este script de Olá tooimport:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="1b4f0-237">script de tooupdate T-SQL para execução em bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="1b4f0-238">Este atualizações de script de PowerShell Olá texto de comando T-SQL para um script existente.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="1b4f0-239">Olá de conjunto de variáveis tooreflect Olá pretendido script definição toobe conjunto os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="1b4f0-240">script existente do tooupdate Olá definição tooan</span><span class="sxs-lookup"><span data-stu-id="1b4f0-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="1b4f0-241">toocreate tooexecute uma tarefa um script através de um mapa de partições horizontais</span><span class="sxs-lookup"><span data-stu-id="1b4f0-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="1b4f0-242">Este script do PowerShell inicia uma tarefa para execução de um script em cada partição horizontal um mapa de partições horizontais horizontal elástico.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="1b4f0-243">Olá de set seguintes Olá de tooreflect variáveis pretendido script e de destino:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="1b4f0-244">tooexecute uma tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-244">tooexecute a job</span></span>
<span data-ttu-id="1b4f0-245">Este script do PowerShell executa uma tarefa existente:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="1b4f0-246">Atualize Olá tooreflect variável Olá pretendido tarefa nome toohave executada os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="1b4f0-247">Estado de Olá tooretrieve da execução de uma única tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="1b4f0-248">Olá utilize [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e conjunto Olá **JobExecutionId** parâmetro tooview Olá Estado execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="1b4f0-249">Utilize Olá mesmo **Get-AzureSqlJobExecution** cmdlet com Olá **includechildren exige** parâmetro tooview Olá Estado execuções de tarefa subordinada, nomeadamente Olá estado específico de cada execução da tarefa em relação a cada a base de dados visada pela tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="1b4f0-250">Estado de Olá tooview em várias execuções de tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="1b4f0-251">Olá [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) tem vários parâmetros opcionais que podem ser utilizado toodisplay várias execuções de tarefa, filtradas através de parâmetros de Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="1b4f0-252">seguinte Olá demonstra Algumas das várias formas de Olá toouse Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="1b4f0-253">Obter todas as execuções de tarefas ativas de nível superior:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="1b4f0-254">Obter todas as execuções de tarefa de nível superior, incluindo as execuções de tarefa inativo:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="1b4f0-255">Obter todas as execuções de tarefa de subordinados de um ID de execução da tarefa fornecida, incluindo execuções de tarefa inativo:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="1b4f0-256">Obter todas as execuções de tarefa criadas com base numa agenda / combinação, incluindo tarefas Inativas da tarefa:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="1b4f0-257">Obter todas as tarefas direcionada para um mapa de partições horizontais especificado, incluindo tarefas Inativas:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="1b4f0-258">Obter todas as tarefas direcionada para uma coleção personalizada especificada, incluindo tarefas Inativas:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="1b4f0-259">Obter a lista de Olá de execuções de tarefas da tarefa em execução uma tarefa específica:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="1b4f0-260">Obter os detalhes de tarefa de execução da tarefa:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="1b4f0-261">Olá seguinte script do PowerShell pode ser utilizados tooview Olá detalhes sobre uma execução de tarefas da tarefa, que é particularmente útil quando a depuração de falhas de execução.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="1b4f0-262">execuções de tarefas de falhas de tooretrieve dentro da tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="1b4f0-263">Olá **JobTaskExecution objeto** inclui uma propriedade para Olá ciclo de vida da tarefa de Olá juntamente com uma propriedade de mensagem.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="1b4f0-264">Se uma execução de tarefas da tarefa falhou, Olá ciclo de vida será possível definir a propriedade demasiado*falha* e será possível definir a propriedade de mensagem de Olá toohello resultante mensagem de exceção e a pilha.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="1b4f0-265">Se uma tarefa não foi concluída com êxito, é importante tooview Olá detalhes sobre as tarefas que não foram concluída com êxito para uma determinada tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="1b4f0-266">toowait para um toocomplete de execução da tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="1b4f0-267">Olá seguinte script do PowerShell pode ser utilizado toowait para um toocomplete de tarefas da tarefa:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="1b4f0-268">Criar uma política de execução personalizado</span><span class="sxs-lookup"><span data-stu-id="1b4f0-268">Create a custom execution policy</span></span>
<span data-ttu-id="1b4f0-269">As tarefas de base de dados elásticas suporta a criação de políticas de execução personalizadas que podem ser aplicadas ao iniciar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="1b4f0-270">Atualmente permitem definir políticas de execução:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="1b4f0-271">Nome: Identificador para a política de execução de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="1b4f0-272">Tempo limite de tarefa: Total de tempo antes de uma tarefa será cancelada pelo tarefas de base de dados elásticas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="1b4f0-273">Intervalo de repetição inicial: Intervalo toowait antes da repetição primeiro.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="1b4f0-274">Intervalo máximo de tentativas: Limite de toouse de intervalos de repetição.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="1b4f0-275">Coeficiente de término de intervalo de repetição: Coeficiente utilizado toocalculate Olá próximo intervalo entre tentativas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="1b4f0-276">Olá seguinte fórmula utilizada: (intervalo de Repita inicial) * Math.pow ((coeficiente de término de intervalo), (número de tentativas) - 2).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="1b4f0-277">Número máximo de tentativas: Olá número máximo de tentativas de repetição tooperform dentro de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="1b4f0-278">política de execução de predefinida Olá utiliza Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="1b4f0-279">Nome: Política de execução de predefinida</span><span class="sxs-lookup"><span data-stu-id="1b4f0-279">Name: Default execution policy</span></span>
* <span data-ttu-id="1b4f0-280">Tempo limite de tarefa: 1 semana</span><span class="sxs-lookup"><span data-stu-id="1b4f0-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="1b4f0-281">Intervalo de repetição inicial: 100 milissegundos</span><span class="sxs-lookup"><span data-stu-id="1b4f0-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="1b4f0-282">Intervalo máximo de tentativas: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="1b4f0-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="1b4f0-283">Repita o coeficiente de intervalo: 2</span><span class="sxs-lookup"><span data-stu-id="1b4f0-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="1b4f0-284">Número máximo de tentativas: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="1b4f0-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="1b4f0-285">Crie política de execução de Olá pretendido:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="1b4f0-286">Atualizar uma política de execução personalizado</span><span class="sxs-lookup"><span data-stu-id="1b4f0-286">Update a custom execution policy</span></span>
<span data-ttu-id="1b4f0-287">Atualize tooupdate de política de execução de Olá pretendido:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="1b4f0-288">Cancelar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-288">Cancel a job</span></span>
<span data-ttu-id="1b4f0-289">As tarefas de base de dados elásticas suporta pedidos de cancelamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="1b4f0-290">Se as tarefas de base de dados elásticas Deteta um pedido de cancelamento de uma tarefa atualmente a ser executado, tentará a tarefa de Olá toostop.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="1b4f0-291">Existem duas formas diferentes, que as tarefas de base de dados elásticas podem executar um cancelamento:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="1b4f0-292">Cancelar tarefas a executar atualmente: se for detetado um cancelamento enquanto uma tarefa está atualmente em execução, será tentado a um cancelamento dentro Olá atualmente em execução aspeto de tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="1b4f0-293">Por exemplo: se houver uma consulta de execução longa atualmente a ser efetuada quando é tentado um cancelamento, existirá uma consulta de Olá toocancel tentativa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="1b4f0-294">As repetições de tarefas a cancelar: se um cancelamento for detetado por thread de controlo de Olá antes de uma tarefa é iniciada para execução, thread de controlo de Olá irá evitar iniciar tarefa Olá e declarar pedido Olá como cancelada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="1b4f0-295">Se for pedido um cancelamento de tarefas para uma tarefa principal, o pedido de cancelamento Olá será cumprido para a tarefa principal de Olá e para todos os respetivos tarefas subordinadas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="1b4f0-296">toosubmit um pedido de cancelamento, utilize Olá [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e conjunto Olá **JobExecutionId** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="1b4f0-297">toodelete uma tarefa e histórico da tarefa assíncrona</span><span class="sxs-lookup"><span data-stu-id="1b4f0-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="1b4f0-298">As tarefas de base de dados elásticas suporta eliminação assíncrona de tarefas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="1b4f0-299">Uma tarefa pode ser marcada para eliminação e sistema Olá irá eliminar a tarefa de Olá e todos os respetivo histórico de tarefas após conclusão da tarefa de Olá todas as execuções de tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="1b4f0-300">sistema de Olá não cancelará automaticamente execuções de tarefas ativas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="1b4f0-301">Invocar [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel execuções de tarefas ativas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="1b4f0-302">eliminação de tarefa tootrigger, utilize Olá [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e conjunto Olá **JobName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="1b4f0-303">toocreate um destino de base de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-303">toocreate a custom database target</span></span>
<span data-ttu-id="1b4f0-304">Pode definir os destinos de base de dados personalizada para execução direta ou para inclusão dentro de um grupo de base de dados personalizada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="1b4f0-305">Por exemplo, porque **conjuntos elásticos** são ainda não diretamente suportada através das APIs do PowerShell, pode criar um destino de coleção da base de dados personalizada que abrange todas as bases de dados de Olá no agrupamento de Olá e de destino de base de dados personalizada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="1b4f0-306">Definir Olá seguindo as informações de base de dados do variáveis tooreflect Olá pretendido:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="1b4f0-307">toocreate um destino de coleção da base de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="1b4f0-308">Olá utilize [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine uma execução de base de dados personalizada do tooenable ao destino coleção entre vários destinos de base de dados definido.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="1b4f0-309">Depois de criar um grupo de base de dados, as bases de dados podem ser associados com o destino de coleção personalizada Olá.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="1b4f0-310">Definir Olá a seguinte configuração de destino do variáveis tooreflect Olá pretendido coleção personalizada:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="1b4f0-311">destino de coleção do tooadd bases de dados tooa base de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="1b4f0-312">base de dados tooa personalizado coleção específica de tooadd utilizar Olá [ **adicionar AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="1b4f0-313">Reveja as bases de dados de Olá dentro de um destino de coleção da base de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="1b4f0-314">Olá utilize [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve Olá subordinado bases de dados dentro de uma base de dados personalizada recolha de destino.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="1b4f0-315">Criar um script de uma tarefa tooexecute através de um destino de coleção da base de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="1b4f0-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="1b4f0-316">Olá utilize [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate uma tarefa de um grupo de bases de dados definidas por um destino de coleção da base de dados personalizada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="1b4f0-317">As tarefas de base de dados elásticas irão expandir tarefa Olá para várias tarefas de subordinados cada base de dados correspondente tooa associados com o destino de coleção de base de dados personalizada Olá e certifique-se de que o script de Olá é executado em relação a cada base de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="1b4f0-318">Novamente, é importante que os scripts estão idempotent toobe resiliente tooretries.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="1b4f0-319">Recolha de dados entre bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-319">Data collection across databases</span></span>
<span data-ttu-id="1b4f0-320">Pode utilizar um tooexecute tarefa consulta entre um grupo de bases de dados e enviar tabela do Olá resultados tooa específica.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="1b4f0-321">tabela de Olá pode ser consultada após Olá facto toosee Olá resultados da consulta de cada base de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="1b4f0-322">Esta opção fornece um método assíncrono tooexecute uma consulta em muitas bases de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="1b4f0-323">Tentativas falhadas são processadas automaticamente através de tentativas.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="1b4f0-324">tabela de destino especificado Olá será criada automaticamente se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="1b4f0-325">nova tabela de Olá corresponde ao esquema Olá Olá devolvida um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="1b4f0-326">Se um script devolver vários conjuntos de resultados, tarefas de bases de dados elásticas só irão enviar Olá primeira toohello destino tabela.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="1b4f0-327">Olá seguinte script do PowerShell executa um script e recolhe os respetivos resultados numa tabela especificada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="1b4f0-328">Este script parte do princípio de que foi criado um script T-SQL que produz um conjunto de resultados único e que foi criado uma base de dados personalizada recolha de destino.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="1b4f0-329">Este script utiliza Olá [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="1b4f0-330">Definir os parâmetros de Olá de script, as credenciais e o destino de execução:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="1b4f0-331">toocreate e iniciar uma tarefa para cenários de recolha de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="1b4f0-332">Este script utiliza Olá [ **início AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="1b4f0-333">tooschedule um acionador de execução da tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="1b4f0-334">Olá seguinte script do PowerShell pode ser utilizado toocreate numa agenda periódica.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="1b4f0-335">Este script utiliza um intervalo em minuto, mas [ **New-AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) também suporta os parâmetros - DayInterval, - HourInterval, - MonthInterval e - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="1b4f0-336">As agendas que executar apenas uma vez que podem ser criadas por transmitir - OneTime.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="1b4f0-337">Crie uma nova agenda:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="1b4f0-338">tootrigger uma tarefa executada num horário</span><span class="sxs-lookup"><span data-stu-id="1b4f0-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="1b4f0-339">Um acionador da tarefa pode ser definido toohave um tarefa executada according tooa horário.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="1b4f0-340">Olá seguinte script do PowerShell pode ser utilizado toocreate um acionador da tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="1b4f0-341">Utilize [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e conjunto Olá seguindo tarefa pretendida do variáveis toocorrespond toohello e agenda:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="1b4f0-342">tooremove uma tarefa de toostop associação agendada execução numa agenda</span><span class="sxs-lookup"><span data-stu-id="1b4f0-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="1b4f0-343">toodiscontinue ocorrer a execução da tarefa através de um acionador da tarefa, acionador da tarefa de Olá pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="1b4f0-344">Remover a um toostop de acionamento de tarefa uma tarefa a ser executado de acordo com tooa agenda utilizando Olá [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="1b4f0-345">Obter tarefa acionadores tooa vinculada horário</span><span class="sxs-lookup"><span data-stu-id="1b4f0-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="1b4f0-346">Olá seguinte script do PowerShell pode ser utilizado tooobtain e apresentar Olá tarefa acionadores tooa registado específico horário.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="1b4f0-347">acionadores de tarefa tooretrieve vinculado tooa tarefa</span><span class="sxs-lookup"><span data-stu-id="1b4f0-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="1b4f0-348">Utilize [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain e apresentar agendas que contém uma tarefa registada.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="1b4f0-349">toocreate uma aplicação de camada de dados (DACPAC) para execução em bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="1b4f0-350">Consulte toocreate um DACPAC [aplicações de camada de dados](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="1b4f0-351">toodeploy um DACPAC, utilize Olá [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="1b4f0-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="1b4f0-352">Olá DACPAC tem de ser acessível toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="1b4f0-353">É recomendado tooupload um tooAzure DACPAC criado armazenamento e criar um [assinatura de acesso partilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para Olá DACPAC.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="1b4f0-354">tooupdate uma aplicação de camada de dados (DACPAC) para execução em bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="1b4f0-355">DACPACs existentes registados dentro de tarefas de base de dados elásticas podem ser atualizada toopoint toonew URIs.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="1b4f0-356">Olá utilize [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate Olá DACPAC URI no existente registado DACPAC:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="1b4f0-357">toocreate tooapply uma tarefa uma aplicação de camada de dados (DACPAC) em bases de dados</span><span class="sxs-lookup"><span data-stu-id="1b4f0-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="1b4f0-358">Depois de ter sido criado um DACPAC dentro de tarefas de base de dados elásticas, uma tarefa pode ser criada tooapply Olá DACPAC entre um grupo de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="1b4f0-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="1b4f0-359">Olá seguinte script do PowerShell pode ser utilizado toocreate uma tarefa DACPAC através de uma coleção personalizada das bases de dados:</span><span class="sxs-lookup"><span data-stu-id="1b4f0-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
