---
title: "aaaHow toomanage simultânea escreve tooresources na Azure Search"
description: "Utilize colisões de ar intermédio simultaneidade otimista tooavoid actualizações ou eliminações tooAzure os índices de pesquisa, indexadores, origens de dados."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a>Como toomanage simultaneidade na Azure Search

Ao gerir os recursos de pesquisa do Azure, como índices e origens de dados, é importante tooupdate recursos de forma segura, especialmente se aceder aos recursos em simultâneo por vários componentes da aplicação. Quando dois clientes em simultâneo atualizar um recurso sem coordenação, condições race são possíveis. tooprevent, ofertas de Azure Search um *modelo de simultaneidade otimista*. Existem não existem bloqueios num recurso. Em vez disso, não há uma ETag para cada recurso que identifica a versão de recurso Olá, de modo a que pode craft pedidos evitar acidental substitui.

> [!Tip]
> Código conceptual um [c# solução de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explica como funciona o controlo de simultaneidade na Azure Search. código de Olá cria condições que invocam o controlo de simultaneidade. Olá leitura [fragmento de código abaixo](#samplecode) é provavelmente suficiente para a maior parte dos programadores, mas se pretender toorun-lo, edite o nome do serviço appsettings.json tooadd Olá e uma chave de api de administração. -Lhe fornecido um URL de serviço de `http://myservice.search.windows.net`, é o nome do serviço Olá `myservice`.

## <a name="how-it-works"></a>Como funciona

É implementada simultaneidade otimista através do acesso condição verifica nas chamadas API escrever tooindexes, indexadores, origens de dados e recursos de synonymMap. 

Todos os recursos de ter um [ *tag de entidade (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) que fornece informações de versão do objeto. Verificando Olá ETag pela primeira vez, pode evitar atualizações em simultâneo num fluxo de trabalho normal (obter, modificar localmente, atualizar), assegurando que corresponde à ETag do recurso Olá sua cópia local. 

+ Olá REST API utiliza um [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no cabeçalho de pedido de Olá.
+ Olá .NET SDK define Olá ETag através de um objeto de accessCondition, definição Olá [If-Match | O cabeçalho If-Match-nenhuma](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no recurso de Olá. Qualquer objeto herdar [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) tem um objeto de accessCondition.

Sempre que atualizar um recurso, a ETag alterado automaticamente. Quando implementar a gestão de simultaneidade, tudo o que estiver a fazer é colocar pré-condição no pedido de actualização de Olá que requer o recurso remoto Olá toohave Olá ETag mesmo como cópia Olá do recurso de Olá que modificada no cliente Olá. Se um processo em simultâneo tiver sido alterada recurso remoto Olá já Olá ETag não irá corresponder à pré-condição Olá e pedido Olá irá falhar com HTTP 412. Se estiver a utilizar o .NET SDK de Olá, isto manifestos como um `CloudException` onde Olá `IsAccessConditionFailed()` método de extensão devolve true.

> [!Note]
> Não há apenas um mecanismo de concorrência. É sempre utilizado, independentemente da que API é utilizada para atualizações de recursos. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Casos de utilização e o código de exemplo

Olá seguinte código demonstra accessCondition verifica a existência de operações de atualização de chave:

+ Efetuar uma atualização se recursos Olá já não existe
+ Efetuar uma atualização se mudar de versão do recurso Olá

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Código de exemplo [DotNetETagsExplainer programa](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a>Padrão de conceção

Um padrão de conceção para implementar a simultaneidade otimista deve incluir um ciclo que repete a verificação de condição de acesso Olá, um teste para a condição de acesso de Olá e, opcionalmente, obtém um recurso atualizado antes de tentar toore-aplicar alterações de Olá. 

Este fragmento de código ilustra a adição de Olá de um índice de tooan synonymMap que já existe. Este código é de Olá [sinónimo (pré-visualização) c# tutorial de Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

obtém o índice Olá "Hotéis" de fragmento Olá, verifica a versão do objeto de Olá de uma operação de atualização, emite uma exceção se a condição de Olá falha e, em seguida, as repetições Olá operação (cópia de segurança vezes toothree), começando pelo índice obtenção do tooget hello do Olá servidor mais recente versão.

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a>Passos seguintes

Olá revisão [exemplo sinónimos c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) mais contexto no como toosafely atualizar um índice existente.

Tente modificar qualquer uma das seguintes Olá amostras tooinclude ETags ou AccessCondition objetos.

+ [Exemplo de REST API no Github](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [Exemplo de SDK do .NET no Github](https://github.com/Azure-Samples/search-dotnet-getting-started). Esta solução inclui o projeto de "DotNetEtagsExplainer" Olá que contém o código de Olá apresentado neste artigo.

## <a name="see-also"></a>Consultar também

  [Pedido e resposta cabeçalhos de HTTP comuns](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)    
  [Códigos de estado HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [índice operações (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)