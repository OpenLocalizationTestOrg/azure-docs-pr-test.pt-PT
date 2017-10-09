---
title: "aaaGetting iniciado com o storage do Azure e os serviços do Visual Studio ligado (projetos de trabalho Web)"
description: "Como tooget iniciado utilizando o Table storage do Azure num projeto WebJobs do Azure no Visual Studio depois de ligar tooa conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="daf8f-103">Introdução ao Azure Storage (projetos de trabalho Web do Azure)</span><span class="sxs-lookup"><span data-stu-id="daf8f-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="daf8f-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="daf8f-104">Overview</span></span>
<span data-ttu-id="daf8f-105">Este artigo fornece c# exemplos de código que mostram mostram como toouse Olá versão do SDK de WebJobs do Azure 1. x com Olá serviço de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf8f-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="daf8f-106">Exemplos de código Olá utilizam Olá [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="daf8f-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="daf8f-107">Olá serviço de armazenamento de tabelas do Azure permite-lhe toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="daf8f-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="daf8f-108">o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf8f-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="daf8f-109">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="daf8f-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="daf8f-110">Consulte [introdução ao Table storage do Azure através do .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="daf8f-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="daf8f-111">Alguns fragmentos de código Olá mostram Olá **tabela** atributo utilizado nas funções que são denominadas manualmente, ou seja, não utilizando um dos atributos de Acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="daf8f-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="daf8f-112">Como tabela de tooa tooadd entidades</span><span class="sxs-lookup"><span data-stu-id="daf8f-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="daf8f-113">tabela de tooa de entidades tooadd, utilize Olá **tabela** atributo com um **ICollector<T>**  ou **IAsyncCollector<T>**  parâmetro onde **T** Especifica o esquema de Olá de entidades de Olá pretende tooadd.</span><span class="sxs-lookup"><span data-stu-id="daf8f-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="daf8f-114">Construtor de atributos de Olá assume um parâmetro de cadeia que especifica o nome de Olá da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="daf8f-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="daf8f-115">Olá seguinte exemplo de código adiciona **pessoa** entidades tooa tabela *entrada*.</span><span class="sxs-lookup"><span data-stu-id="daf8f-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() {
                        PartitionKey = "Test",
                        RowKey = i.ToString(),
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="daf8f-116">Olá, normalmente, o tipo que utiliza com o **ICollector** deriva de **TableEntity** ou implementa **ITableEntity**, mas não tem.</span><span class="sxs-lookup"><span data-stu-id="daf8f-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="daf8f-117">Olá seguinte **pessoa** classes de trabalho com o código de Olá mostrado na Olá anterior **entrada** método.</span><span class="sxs-lookup"><span data-stu-id="daf8f-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="daf8f-118">Se quiser toowork diretamente com Olá API do armazenamento do Azure, pode adicionar um **CloudStorageAccount** a assinatura do método toohello parâmetro.</span><span class="sxs-lookup"><span data-stu-id="daf8f-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="daf8f-119">A monitorização em tempo real</span><span class="sxs-lookup"><span data-stu-id="daf8f-119">Real-time monitoring</span></span>
<span data-ttu-id="daf8f-120">Porque as funções do dados entrada frequentemente processam grandes volumes de dados, Olá dashboard do SDK de WebJobs fornece dados de monitorização em tempo real.</span><span class="sxs-lookup"><span data-stu-id="daf8f-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="daf8f-121">Olá **invocação registo** secção indica se a função Olá ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="daf8f-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="daf8f-123">Olá **detalhes de invocação** página Relatórios Olá progresso da função (número de entidades escritos) enquanto está em execução e dá-lhe uma oportunidade tooabort-lo.</span><span class="sxs-lookup"><span data-stu-id="daf8f-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="daf8f-125">Quando a função Olá estiver concluído, hello **detalhes de invocação** página reporta o número de Olá de linhas escrito.</span><span class="sxs-lookup"><span data-stu-id="daf8f-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Função de entrada concluída](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="daf8f-127">Como tooread várias entidades de uma tabela</span><span class="sxs-lookup"><span data-stu-id="daf8f-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="daf8f-128">tooread uma tabela, utilize Olá **tabela** atributo com um **IQueryable<T>**  parâmetro onde escreva **T** deriva de **TableEntity**ou implementa **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="daf8f-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="daf8f-129">Olá seguinte exemplo de código lê e regista todas as linhas de Olá **entrada** tabela:</span><span class="sxs-lookup"><span data-stu-id="daf8f-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}",
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="daf8f-130">Como tooread uma única entidade a partir de uma tabela</span><span class="sxs-lookup"><span data-stu-id="daf8f-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="daf8f-131">Não existe um **tabela** construtor de atributos com dois parâmetros adicionais que permitem-lhe especificar a chave da fila e a chave de partição Olá quando pretender que a entidade do toobind tooa única tabela.</span><span class="sxs-lookup"><span data-stu-id="daf8f-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="daf8f-132">Olá seguinte exemplo de código lê uma linha de tabela para um **pessoa** entidade com base na partição chave e a linha de valores de chave recebidos uma mensagem de fila:</span><span class="sxs-lookup"><span data-stu-id="daf8f-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="daf8f-133">Olá **pessoa** classe neste exemplo não tem tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="daf8f-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="daf8f-134">Como toouse Olá API .NET do armazenamento diretamente toowork com uma tabela</span><span class="sxs-lookup"><span data-stu-id="daf8f-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="daf8f-135">Também pode utilizar Olá **tabela** atributo com um **CloudTable** objeto para uma maior flexibilidade na trabalhar com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="daf8f-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="daf8f-136">seguinte de Olá código de exemplo utiliza um **CloudTable** objeto tooadd toohello uma única entidade *entrada* tabela.</span><span class="sxs-lookup"><span data-stu-id="daf8f-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="daf8f-137">Para obter mais informações sobre como toouse Olá **CloudTable** objeto, consulte [introdução ao Table storage do Azure através do .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="daf8f-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="daf8f-138">Tópicos relacionados abrangidos por Olá filas como-tooarticle</span><span class="sxs-lookup"><span data-stu-id="daf8f-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="daf8f-139">Para obter informações sobre como processamento de tabela toohandle acionado por uma mensagem de fila ou para WebJobs cenários do SDK não processar, consulte específicos tootable [introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (projetos de trabalho Web) ](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="daf8f-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="daf8f-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="daf8f-140">Next steps</span></span>
<span data-ttu-id="daf8f-141">Este artigo foi fornecido o código de exemplo que mostram como toohandle cenários comuns para trabalhar com as tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf8f-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="daf8f-142">Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="daf8f-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

