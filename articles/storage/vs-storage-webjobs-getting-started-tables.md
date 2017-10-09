---
title: "aaaGetting iniciado com o storage do Azure e os serviços do Visual Studio ligado (projetos de trabalho Web)"
description: "Como tooget iniciado utilizando o Table storage do Azure num projeto WebJobs do Azure no Visual Studio depois de ligar tooa conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Introdução ao Azure Storage (projetos de trabalho Web do Azure)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Descrição geral
Este artigo fornece c# exemplos de código que mostram mostram como toouse Olá versão do SDK de WebJobs do Azure 1. x com Olá serviço de armazenamento de tabela do Azure. Exemplos de código Olá utilizam Olá [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x.

Olá serviço de armazenamento de tabelas do Azure permite-lhe toostore grandes quantidades de dados estruturados. o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.  Consulte [introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md#create-a-table) para obter mais informações.

Alguns fragmentos de código Olá mostram Olá **tabela** atributo utilizado nas funções que são denominadas manualmente, ou seja, não utilizando um dos atributos de Acionador de Olá.

## <a name="how-tooadd-entities-tooa-table"></a>Como tabela de tooa tooadd entidades
tabela de tooa de entidades tooadd, utilize Olá **tabela** atributo com um **ICollector<T>**  ou **IAsyncCollector<T>**  parâmetro onde **T** Especifica o esquema de Olá de entidades de Olá pretende tooadd. Construtor de atributos de Olá assume um parâmetro de cadeia que especifica o nome de Olá da tabela de Olá.

Olá seguinte exemplo de código adiciona **pessoa** entidades tooa tabela *entrada*.

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

Olá, normalmente, o tipo que utiliza com o **ICollector** deriva de **TableEntity** ou implementa **ITableEntity**, mas não tem. Olá seguinte **pessoa** classes de trabalho com o código de Olá mostrado na Olá anterior **entrada** método.

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

Se quiser toowork diretamente com Olá API do armazenamento do Azure, pode adicionar um **CloudStorageAccount** a assinatura do método toohello parâmetro.

## <a name="real-time-monitoring"></a>A monitorização em tempo real
Porque as funções do dados entrada frequentemente processam grandes volumes de dados, Olá dashboard do SDK de WebJobs fornece dados de monitorização em tempo real. Olá **invocação registo** secção indica se a função Olá ainda está em execução.

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Olá **detalhes de invocação** página Relatórios Olá progresso da função (número de entidades escritos) enquanto está em execução e dá-lhe uma oportunidade tooabort-lo.

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Quando a função Olá estiver concluído, hello **detalhes de invocação** página reporta o número de Olá de linhas escrito.

![Função de entrada concluída](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Como tooread várias entidades de uma tabela
tooread uma tabela, utilize Olá **tabela** atributo com um **IQueryable<T>**  parâmetro onde escreva **T** deriva de **TableEntity**ou implementa **ITableEntity**.

Olá seguinte exemplo de código lê e regista todas as linhas de Olá **entrada** tabela:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Como tooread uma única entidade a partir de uma tabela
Não existe um **tabela** construtor de atributos com dois parâmetros adicionais que permitem-lhe especificar a chave da fila e a chave de partição Olá quando pretender que a entidade do toobind tooa única tabela.

Olá seguinte exemplo de código lê uma linha de tabela para um **pessoa** entidade com base na partição chave e a linha de valores de chave recebidos uma mensagem de fila:  

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


Olá **pessoa** classe neste exemplo não tem tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Como toouse Olá API .NET do armazenamento diretamente toowork com uma tabela
Também pode utilizar Olá **tabela** atributo com um **CloudTable** objeto para uma maior flexibilidade na trabalhar com uma tabela.

seguinte de Olá código de exemplo utiliza um **CloudTable** objeto tooadd toohello uma única entidade *entrada* tabela.

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

Para obter mais informações sobre como toouse Olá **CloudTable** objeto, consulte [introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Tópicos relacionados abrangidos por Olá filas como-tooarticle
Para obter informações sobre como processamento de tabela toohandle acionado por uma mensagem de fila ou para WebJobs cenários do SDK não processar, consulte específicos tootable [introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (projetos de trabalho Web) ](vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Passos seguintes
Este artigo foi fornecido o código de exemplo que mostram como toohandle cenários comuns para trabalhar com as tabelas do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).

