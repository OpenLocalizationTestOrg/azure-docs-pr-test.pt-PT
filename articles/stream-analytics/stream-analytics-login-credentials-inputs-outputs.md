---
title: "Análise de fluxo: Rodar credenciais de início de sessão de entradas e saídas | Microsoft Docs"
description: "Saiba como tooupdate Olá credenciais para o Stream Analytics entradas e saídas."
keywords: "credenciais de início de sessão"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="a94fc-104">Roda credenciais de início de sessão de entradas e saídas nas tarefas do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="a94fc-105">Abstrato</span><span class="sxs-lookup"><span data-stu-id="a94fc-105">Abstract</span></span>
<span data-ttu-id="a94fc-106">O Azure Stream Analytics atualmente não permite substituir Olá as credenciais numa entrada/saída ao hello tarefa está em execução.</span><span class="sxs-lookup"><span data-stu-id="a94fc-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="a94fc-107">Enquanto o Azure Stream Analytics suporta retomar uma tarefa a partir do último saída, queremos processo completo de Olá tooshare para minimizar o desfasamento de Olá entre Olá parar e iniciar a tarefa de Olá e rodar as credenciais de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="a94fc-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="a94fc-108">Parte 1 – preparar o novo conjunto de Olá de credenciais:</span><span class="sxs-lookup"><span data-stu-id="a94fc-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="a94fc-109">Esta peça é aplicável toohello entradas/saídas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a94fc-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="a94fc-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a94fc-110">Blob Storage</span></span>
* <span data-ttu-id="a94fc-111">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a94fc-111">Event Hubs</span></span>
* <span data-ttu-id="a94fc-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a94fc-112">SQL Database</span></span>
* <span data-ttu-id="a94fc-113">Armazenamento de Tabelas</span><span class="sxs-lookup"><span data-stu-id="a94fc-113">Table Storage</span></span>

<span data-ttu-id="a94fc-114">Para outras entradas/saídas, prossiga com a parte 2.</span><span class="sxs-lookup"><span data-stu-id="a94fc-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="a94fc-115">Armazenamento de/tabela de armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="a94fc-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="a94fc-116">Aceda a extensão de armazenamento toohello no portal de gestão do Azure Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="a94fc-118">Localize o armazenamento de Olá utilizado pelo seu trabalho e vá para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="a94fc-120">Clique no comando de gerir chaves de acesso de Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="a94fc-122">Entre Olá chave de acesso primária e chave de acesso secundária, de Olá **escolha Olá não utilizada pela sua tarefa**.</span><span class="sxs-lookup"><span data-stu-id="a94fc-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="a94fc-123">Voltar a gerar acessos:</span><span class="sxs-lookup"><span data-stu-id="a94fc-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="a94fc-125">Copie a chave de Olá gerado recentemente:</span><span class="sxs-lookup"><span data-stu-id="a94fc-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="a94fc-127">Continue tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="a94fc-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="a94fc-128">Event hubs</span><span class="sxs-lookup"><span data-stu-id="a94fc-128">Event hubs</span></span>
1. <span data-ttu-id="a94fc-129">Aceda a extensão de Service Bus toohello no portal de gestão do Azure Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="a94fc-131">Localize Olá espaço de nomes do barramento de serviço utilizada pelo seu trabalho e vá para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="a94fc-133">Se a sua tarefa utilizar uma política de acesso partilhado no Olá espaço de nomes do Service Bus, avance toostep 6</span><span class="sxs-lookup"><span data-stu-id="a94fc-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="a94fc-134">Visite o separador de Event Hubs toohello:</span><span class="sxs-lookup"><span data-stu-id="a94fc-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="a94fc-136">Localize Olá utilizado pela sua tarefa de Hub de eventos e vá para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="a94fc-138">Aceda toohello separador Configurar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="a94fc-140">No Olá pendente do nome da política, localize a política de acesso de Olá partilhado utilizada pela sua tarefa:</span><span class="sxs-lookup"><span data-stu-id="a94fc-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="a94fc-142">Entre Olá chave primária e chave secundária, de Olá **escolha Olá não utilizada pela sua tarefa**.</span><span class="sxs-lookup"><span data-stu-id="a94fc-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="a94fc-143">Voltar a gerar acessos:</span><span class="sxs-lookup"><span data-stu-id="a94fc-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="a94fc-145">Copie a chave de Olá gerado recentemente:</span><span class="sxs-lookup"><span data-stu-id="a94fc-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="a94fc-147">Continue tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="a94fc-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="a94fc-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a94fc-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="a94fc-149">Nota: precisa tooconnect toohello serviço de base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a94fc-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="a94fc-150">Vamos tooshow como toodo esta utilizando Olá experiência de gestão no portal de gestão do Azure Olá, mas pode escolher toouse algumas ferramenta do lado do cliente, tais como o SQL Server Management Studio bem.</span><span class="sxs-lookup"><span data-stu-id="a94fc-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="a94fc-151">Aceda a extensão de bases de dados SQL toohello no portal de gestão do Azure Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="a94fc-153">Localizar Olá base de dados do SQL Server utilizada pela sua tarefa e **clique no servidor de Olá** ligar sobre Olá mesmo linha:</span><span class="sxs-lookup"><span data-stu-id="a94fc-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="a94fc-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="a94fc-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="a94fc-155">Clique no comando de gerir Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="a94fc-157">Tipo de base de dados mestra:</span><span class="sxs-lookup"><span data-stu-id="a94fc-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="a94fc-159">Digite o nome de utilizador, palavra-passe e clique em registo em:</span><span class="sxs-lookup"><span data-stu-id="a94fc-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="a94fc-161">Clique em nova consulta:</span><span class="sxs-lookup"><span data-stu-id="a94fc-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="a94fc-163">Tipo de Olá seguinte consulta substituindo < login_name > com o nome de utilizador e de substituir <enterStrongPasswordHere> com a sua nova palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="a94fc-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="a94fc-164">Clique em executar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="a94fc-166">Voltar atrás toostep 2 e desta vez clique base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="a94fc-168">Clique no comando de gerir Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="a94fc-170">Digite o nome de utilizador, palavra-passe e clique em início de sessão:</span><span class="sxs-lookup"><span data-stu-id="a94fc-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="a94fc-172">Clique em nova consulta:</span><span class="sxs-lookup"><span data-stu-id="a94fc-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="a94fc-174">Escreva Olá seguinte consulta substituindo < user_name > com um nome pelo qual pretende tooidentify este início de sessão no contexto de Olá desta base de dados (pode fornecer Olá mesmo valor que forneceu para < login_name >, por exemplo) e de substituir < login_name > com o o novo nome de utilizador:</span><span class="sxs-lookup"><span data-stu-id="a94fc-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="a94fc-175">Clique em executar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="a94fc-177">Agora deve fornecer o seu novo utilizador com Olá mesmas funções e privilégios tinha o utilizador original.</span><span class="sxs-lookup"><span data-stu-id="a94fc-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="a94fc-178">Continue tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="a94fc-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="a94fc-179">Parte 2: A parar Olá tarefa do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="a94fc-180">Aceda a extensão de Stream Analytics toohello no portal de gestão do Azure Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="a94fc-182">Localize a tarefa e vá para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="a94fc-184">Visite o separador de entradas de toohello ou separador saídas de Olá com base em se estão rodar credenciais Olá numa entrada ou um resultado.</span><span class="sxs-lookup"><span data-stu-id="a94fc-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="a94fc-186">Clique em comando de paragem Olá e confirme a tarefa de Olá parou:</span><span class="sxs-lookup"><span data-stu-id="a94fc-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="a94fc-187">![graphic29][graphic29] aguardar Olá tarefa toostop.</span><span class="sxs-lookup"><span data-stu-id="a94fc-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="a94fc-188">Localizar Olá entrada/saída pretender toorotate credenciais no e vá para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="a94fc-190">Continuar tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="a94fc-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="a94fc-191">Parte 3: Editar Olá as credenciais no Olá tarefa do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="a94fc-192">Armazenamento de/tabela de armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="a94fc-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="a94fc-193">Localizar o campo de chave de conta de armazenamento de Olá e cole a chave recentemente criada para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="a94fc-195">Clique em comandos de guardar Olá e confirmar as alterações a guardar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="a94fc-197">Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de que é passou com êxito.</span><span class="sxs-lookup"><span data-stu-id="a94fc-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="a94fc-198">Continuar tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="a94fc-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="a94fc-199">Event hubs</span><span class="sxs-lookup"><span data-stu-id="a94fc-199">Event hubs</span></span>
1. <span data-ttu-id="a94fc-200">Localizar o campo de chave de política de Hub de eventos de Olá e cole a chave recentemente criada para a mesma:</span><span class="sxs-lookup"><span data-stu-id="a94fc-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="a94fc-202">Clique em comandos de guardar Olá e confirmar as alterações a guardar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="a94fc-204">Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de que tem passou com êxito.</span><span class="sxs-lookup"><span data-stu-id="a94fc-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="a94fc-205">Continuar tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="a94fc-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="a94fc-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="a94fc-206">Power BI</span></span>
1. <span data-ttu-id="a94fc-207">Clique em autorização de renovação de Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="a94fc-209">Irá obter Olá confirmação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a94fc-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="a94fc-211">Clique em comandos de guardar Olá e confirmar as alterações a guardar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="a94fc-213">Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de passou com êxito.</span><span class="sxs-lookup"><span data-stu-id="a94fc-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="a94fc-214">Continuar tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="a94fc-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="a94fc-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a94fc-215">SQL Database</span></span>
1. <span data-ttu-id="a94fc-216">Localizar Olá campos de nome de utilizador e palavra-passe e cole-os do conjunto de credenciais criado recentemente:</span><span class="sxs-lookup"><span data-stu-id="a94fc-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="a94fc-218">Clique em comandos de guardar Olá e confirmar as alterações a guardar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="a94fc-220">Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de que tem passou com êxito.</span><span class="sxs-lookup"><span data-stu-id="a94fc-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="a94fc-221">Continuar tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="a94fc-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="a94fc-222">Parte 4: A iniciar a tarefa de hora da última paragem</span><span class="sxs-lookup"><span data-stu-id="a94fc-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="a94fc-223">Saia Olá entrada/saída:</span><span class="sxs-lookup"><span data-stu-id="a94fc-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="a94fc-225">Clique no comando de início de Olá:</span><span class="sxs-lookup"><span data-stu-id="a94fc-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="a94fc-227">Escolha Olá hora da última paragem e clique em OK:</span><span class="sxs-lookup"><span data-stu-id="a94fc-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="a94fc-229">Continuar tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="a94fc-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="a94fc-230">Parte 5: Remover Olá antigo conjunto de credenciais</span><span class="sxs-lookup"><span data-stu-id="a94fc-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="a94fc-231">Esta peça é aplicável toohello entradas/saídas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a94fc-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="a94fc-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a94fc-232">Blob Storage</span></span>
* <span data-ttu-id="a94fc-233">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a94fc-233">Event Hubs</span></span>
* <span data-ttu-id="a94fc-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a94fc-234">SQL Database</span></span>
* <span data-ttu-id="a94fc-235">Armazenamento de Tabelas</span><span class="sxs-lookup"><span data-stu-id="a94fc-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="a94fc-236">Armazenamento de/tabela de armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="a94fc-236">Blob storage/Table storage</span></span>
<span data-ttu-id="a94fc-237">Repita parte 1 para Olá chave de acesso que foi utilizado anteriormente pelo seu trabalho toorenew Olá agora não utilizados chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="a94fc-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="a94fc-238">Event hubs</span><span class="sxs-lookup"><span data-stu-id="a94fc-238">Event hubs</span></span>
<span data-ttu-id="a94fc-239">Repita parte 1 para Olá chave que foi utilizado anteriormente pelo seu trabalho toorenew Olá chave agora não utilizado.</span><span class="sxs-lookup"><span data-stu-id="a94fc-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="a94fc-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a94fc-240">SQL Database</span></span>
1. <span data-ttu-id="a94fc-241">Volte atrás toohello janela de consulta do tipo no Olá consulta a seguir, substituindo < previous_login_name > com Olá nome de utilizador que foi utilizado anteriormente pelo seu trabalho e parte 1 passo 7:</span><span class="sxs-lookup"><span data-stu-id="a94fc-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="a94fc-242">Clique em executar:</span><span class="sxs-lookup"><span data-stu-id="a94fc-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="a94fc-244">Pode ser obtido Olá confirmação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a94fc-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="a94fc-245">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="a94fc-245">Get help</span></span>
<span data-ttu-id="a94fc-246">Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a94fc-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a94fc-247">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a94fc-247">Next steps</span></span>
* [<span data-ttu-id="a94fc-248">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a94fc-249">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a94fc-250">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a94fc-251">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a94fc-252">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a94fc-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

