---
title: "conector de base de dados Oracle Olá aaaAdd nas suas Logic Apps do Azure | Microsoft Docs"
description: "Utilizar o conector de base de dados Oracle Olá numa aplicação lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="da23e-103">Começar a utilizar o conector de base de dados Oracle Olá</span><span class="sxs-lookup"><span data-stu-id="da23e-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="da23e-104">Utilizar o conector de base de dados Oracle Olá, criar organizacionais fluxos de trabalho que utilizam dados na base de dados existente.</span><span class="sxs-lookup"><span data-stu-id="da23e-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="da23e-105">Este conector pode ligar tooan base de dados no local Oracle ou uma máquina virtual do Azure com a base de dados Oracle instalado.</span><span class="sxs-lookup"><span data-stu-id="da23e-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="da23e-106">Com este conector, pode:</span><span class="sxs-lookup"><span data-stu-id="da23e-106">With this connector, you can:</span></span>

* <span data-ttu-id="da23e-107">Crie o fluxo de trabalho ao adicionar uma base de dados de clientes de tooa de cliente novo ou atualizar uma ordem numa base de dados ordens.</span><span class="sxs-lookup"><span data-stu-id="da23e-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="da23e-108">Utilize ações tooget uma linha de dados, insira uma nova linha e mesmo eliminar.</span><span class="sxs-lookup"><span data-stu-id="da23e-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="da23e-109">Por exemplo, quando é criado um registo no Dynamics CRM Online (um acionador), em seguida, inserir uma linha numa base de dados Oracle (uma ação).</span><span class="sxs-lookup"><span data-stu-id="da23e-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="da23e-110">Este tópico mostra como toouse Olá conector de base de dados Oracle numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="da23e-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da23e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da23e-111">Prerequisites</span></span>

* <span data-ttu-id="da23e-112">Versões suportadas do Oracle:</span><span class="sxs-lookup"><span data-stu-id="da23e-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="da23e-113">Oracle 9 e posterior</span><span class="sxs-lookup"><span data-stu-id="da23e-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="da23e-114">Software de cliente Oracle 8.1.7 e posterior</span><span class="sxs-lookup"><span data-stu-id="da23e-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="da23e-115">Instale o gateway de dados do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="da23e-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="da23e-116">[Ligar dados tooon local a partir das logic apps](../logic-apps/logic-apps-gateway-connection.md) listas Olá passos.</span><span class="sxs-lookup"><span data-stu-id="da23e-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="da23e-117">gateway de Olá é necessário tooconnect tooan base de dados no local Oracle ou VM do Azure com o Oracle DB instalado.</span><span class="sxs-lookup"><span data-stu-id="da23e-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="da23e-118">gateway de dados no local Olá atua como uma ponte e fornece uma transferência de dados seguros entre os dados no local (dados que não se encontra numa nuvem Olá) e as logic apps.</span><span class="sxs-lookup"><span data-stu-id="da23e-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="da23e-119">Olá mesmo gateway pode ser utilizado com vários serviços e várias origens de dados.</span><span class="sxs-lookup"><span data-stu-id="da23e-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="da23e-120">Por isso, poderá apenas terá de gateway de Olá tooinstall uma vez.</span><span class="sxs-lookup"><span data-stu-id="da23e-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="da23e-121">Instale Olá cliente Oracle no computador de olá onde instalou o gateway de dados do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="da23e-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="da23e-122">Não se esqueça de tooinstall hello 64-bit Oracle Data Provider para .NET do Oracle:</span><span class="sxs-lookup"><span data-stu-id="da23e-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="da23e-123">64-bit ODAC 12c versão 4 (12.1.0.2.4) para Windows x64</span><span class="sxs-lookup"><span data-stu-id="da23e-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="da23e-124">Se não estiver instalado o cliente de Oracle Olá, ocorre um erro ao tentar toocreate ou utilizar Olá ligação.</span><span class="sxs-lookup"><span data-stu-id="da23e-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="da23e-125">Consulte os erros comuns de Olá neste tópico.</span><span class="sxs-lookup"><span data-stu-id="da23e-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="da23e-126">Adicione o conector de Olá</span><span class="sxs-lookup"><span data-stu-id="da23e-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da23e-127">Este conector não ter acionadores.</span><span class="sxs-lookup"><span data-stu-id="da23e-127">This connector does not have any triggers.</span></span> <span data-ttu-id="da23e-128">Tem apenas ações.</span><span class="sxs-lookup"><span data-stu-id="da23e-128">It has only actions.</span></span> <span data-ttu-id="da23e-129">Por isso, ao criar a sua aplicação lógica, adicionar outro toostart de Acionador a aplicação lógica, tais como **agenda - periodicidade**, ou **pedido / resposta - resposta**.</span><span class="sxs-lookup"><span data-stu-id="da23e-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="da23e-130">No Olá [portal do Azure](https://portal.azure.com), criar uma aplicação lógica em branco.</span><span class="sxs-lookup"><span data-stu-id="da23e-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="da23e-131">Início Olá da sua aplicação lógica, selecione Olá **pedido / resposta - pedido** acionador:</span><span class="sxs-lookup"><span data-stu-id="da23e-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="da23e-132">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="da23e-132">Select **Save**.</span></span> <span data-ttu-id="da23e-133">Quando guardar, o URL do pedido é gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="da23e-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="da23e-134">Selecione **novo passo**e selecione **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="da23e-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="da23e-135">Escreva `oracle` toosee Olá ações disponíveis:</span><span class="sxs-lookup"><span data-stu-id="da23e-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="da23e-136">Este é também toosee de forma mais rápida Olá Olá acionadores e ações disponíveis para os conectores.</span><span class="sxs-lookup"><span data-stu-id="da23e-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="da23e-137">Escreva a parte do nome de conector Olá, tal como `oracle`.</span><span class="sxs-lookup"><span data-stu-id="da23e-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="da23e-138">designer de Olá apresenta uma lista de acionadores e ações.</span><span class="sxs-lookup"><span data-stu-id="da23e-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="da23e-139">Selecione uma das ações de Olá, tais como **base de dados Oracle - Get linha**.</span><span class="sxs-lookup"><span data-stu-id="da23e-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="da23e-140">Selecione **ligar através do gateway de dados no local**.</span><span class="sxs-lookup"><span data-stu-id="da23e-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="da23e-141">Introduza o nome de servidor Oracle Olá, método de autenticação, nome de utilizador, palavra-passe e selecione Olá gateway:</span><span class="sxs-lookup"><span data-stu-id="da23e-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="da23e-142">Assim que estiver ligado, selecione uma tabela na lista de Olá e introduza a tabela de tooyour Olá linha ID.</span><span class="sxs-lookup"><span data-stu-id="da23e-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="da23e-143">Terá de tabela de toohello tooknow Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="da23e-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="da23e-144">Se não souber, contacte o administrador de Oracle DB e obter um resultado de Olá `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="da23e-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="da23e-145">Este oferece Olá terá tooproceed de informações de identificação.</span><span class="sxs-lookup"><span data-stu-id="da23e-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="da23e-146">No seguinte exemplo de Olá, os dados da tarefa estão a ser devolvidos de uma base de dados de recursos humanos:</span><span class="sxs-lookup"><span data-stu-id="da23e-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="da23e-147">Neste passo seguinte, pode utilizar qualquer um dos Olá toobuild outros conectores o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="da23e-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="da23e-148">Se pretender tootest dados ao obter do Oracle, em seguida, enviar uma mensagem de e-mail por si com Olá Oracle dados, utilizando um dos Olá envie correio eletrónico conectores, do Office 365 ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="da23e-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="da23e-149">Utilize Olá tokens dinâmico de Olá do Olá Oracle tabela toobuild `Subject` e `Body` do seu correio eletrónico:</span><span class="sxs-lookup"><span data-stu-id="da23e-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="da23e-150">**Guardar** sua aplicação lógica e, em seguida, selecione **executar**.</span><span class="sxs-lookup"><span data-stu-id="da23e-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="da23e-151">Fechar o designer de Olá e observe o histórico de execuções de Olá para o estado de Olá.</span><span class="sxs-lookup"><span data-stu-id="da23e-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="da23e-152">Se falhar, selecione a linha de mensagem de falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="da23e-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="da23e-153">designer de Olá abre e mostra que o passo houve e também mostra Olá informações de erro.</span><span class="sxs-lookup"><span data-stu-id="da23e-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="da23e-154">Se tiver êxito, deverá receber um e-mail com as informações de Olá adicionou.</span><span class="sxs-lookup"><span data-stu-id="da23e-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="da23e-155">Ideias de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="da23e-155">Workflow ideas</span></span>

* <span data-ttu-id="da23e-156">Pretende toomonitor Olá #oracle hashtag e colocar Olá tweets numa base de dados para que possa ser consultadas e utilizados dentro de outras aplicações.</span><span class="sxs-lookup"><span data-stu-id="da23e-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="da23e-157">Numa aplicação lógica, adicionar Olá `Twitter - When a new tweet is posted` acionar e introduza Olá **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="da23e-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="da23e-158">Em seguida, adicionar Olá `Oracle Database - Insert row` ação e selecione a tabela:</span><span class="sxs-lookup"><span data-stu-id="da23e-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="da23e-159">São enviadas mensagens de fila do Service Bus tooa.</span><span class="sxs-lookup"><span data-stu-id="da23e-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="da23e-160">Pretende tooget estas mensagens e colocá-los numa base de dados.</span><span class="sxs-lookup"><span data-stu-id="da23e-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="da23e-161">Numa aplicação lógica, adicionar Olá `Service Bus - when a message is received in a queue` acionador e selecione Olá fila.</span><span class="sxs-lookup"><span data-stu-id="da23e-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="da23e-162">Em seguida, adicionar Olá `Oracle Database - Insert row` ação e selecione a tabela:</span><span class="sxs-lookup"><span data-stu-id="da23e-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="da23e-163">Erros comuns</span><span class="sxs-lookup"><span data-stu-id="da23e-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="da23e-164">**Erro**: não é possível alcançar Olá Gateway</span><span class="sxs-lookup"><span data-stu-id="da23e-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="da23e-165">**Causa**: gateway de dados no local Olá não é possível tooconnect toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="da23e-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="da23e-166">**Mitigação**: Certifique-se de que o gateway está em execução na máquina no local de olá onde a instalou e que as TI podem ser ligados toohello internet.</span><span class="sxs-lookup"><span data-stu-id="da23e-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="da23e-167">Recomendamos que não instale o gateway de Olá num computador que pode ser desativada ou em suspensão.</span><span class="sxs-lookup"><span data-stu-id="da23e-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="da23e-168">Também pode reiniciar o serviço de gateway de dados do Olá no local (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="da23e-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="da23e-169">**Erro**: Olá o fornecedor utilizado foi preterido: ' System.Data.OracleClient requer Oracle versão do software de cliente 8.1.7 ou superior.'.</span><span class="sxs-lookup"><span data-stu-id="da23e-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="da23e-170">Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) fornecedor oficial do tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="da23e-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="da23e-171">**Causa**: cliente Oracle de Olá SDK não está instalado na máquina de olá onde hello no local o gateway de dados está em execução.</span><span class="sxs-lookup"><span data-stu-id="da23e-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="da23e-172">**Resolução**: transferir e instalar o SDK do cliente de Oracle Olá Olá mesmo computador como gateway de dados do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="da23e-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="da23e-173">**Erro**: tabela '[Tablename]' não define quaisquer colunas de chaves</span><span class="sxs-lookup"><span data-stu-id="da23e-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="da23e-174">**Causa**: Olá tabela não tem nenhuma chave primária.</span><span class="sxs-lookup"><span data-stu-id="da23e-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="da23e-175">**Resolução**: conector de base de dados Oracle Olá necessita que uma tabela com uma coluna de chave primária utilizada.</span><span class="sxs-lookup"><span data-stu-id="da23e-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="da23e-176">Atualmente não suportado</span><span class="sxs-lookup"><span data-stu-id="da23e-176">Currently not supported</span></span>

* <span data-ttu-id="da23e-177">As vistas e procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="da23e-177">Views and stored procedures</span></span> 
* <span data-ttu-id="da23e-178">Nenhuma tabela com as chaves compostas</span><span class="sxs-lookup"><span data-stu-id="da23e-178">Any table with composite keys</span></span>
* <span data-ttu-id="da23e-179">Tipos de objeto aninhado nas tabelas</span><span class="sxs-lookup"><span data-stu-id="da23e-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="da23e-180">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="da23e-180">Connector-specific details</span></span>

<span data-ttu-id="da23e-181">Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="da23e-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="da23e-182">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="da23e-182">Get some help</span></span>

<span data-ttu-id="da23e-183">Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) é ótimo colocar perguntas tooask, responda às perguntas e ver que outros utilizadores Logic Apps estão a fazer.</span><span class="sxs-lookup"><span data-stu-id="da23e-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="da23e-184">Pode ajudar a melhorar as Logic Apps e conectores ao voto e submeter as suas ideias em [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="da23e-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="da23e-185">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="da23e-185">Next steps</span></span>
<span data-ttu-id="da23e-186">[Criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md)e explore os conectores disponíveis de Olá em Logic Apps no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="da23e-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
