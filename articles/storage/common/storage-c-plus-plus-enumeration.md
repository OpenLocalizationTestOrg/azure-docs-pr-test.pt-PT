---
title: "recursos de armazenamento do Azure aaaList com Olá biblioteca de clientes do Storage para C++ | Microsoft Docs"
description: "Saiba como Olá toouse listagem APIs da biblioteca de clientes de armazenamento do Microsoft Azure para contentores de tooenumerate C++, blobs, filas, tabelas e entidades."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="31bbe-103">Lista de recursos de armazenamento do Azure em C++</span><span class="sxs-lookup"><span data-stu-id="31bbe-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="31bbe-104">As operações de listagem são cenários de desenvolvimento de toomany chave com o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="31bbe-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="31bbe-105">Este artigo descreve como toomost enumerar objetos no Storage do Azure utilizando Olá listagem APIs fornecidas Olá biblioteca de clientes de armazenamento do Microsoft Azure para C++ forma eficiente.</span><span class="sxs-lookup"><span data-stu-id="31bbe-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="31bbe-106">Este guia destina-se Olá biblioteca de clientes do Storage do Azure para a versão de C++ 2, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="31bbe-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="31bbe-107">Olá biblioteca de clientes de armazenamento fornece uma variedade de toolist métodos ou os objetos de consulta no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="31bbe-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="31bbe-108">Este artigo aborda Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="31bbe-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="31bbe-109">Lista de contentores numa conta</span><span class="sxs-lookup"><span data-stu-id="31bbe-109">List containers in an account</span></span>
* <span data-ttu-id="31bbe-110">Lista de blobs num contentor ou diretório virtual blob</span><span class="sxs-lookup"><span data-stu-id="31bbe-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="31bbe-111">Filas de lista numa conta</span><span class="sxs-lookup"><span data-stu-id="31bbe-111">List queues in an account</span></span>
* <span data-ttu-id="31bbe-112">Lista de tabelas numa conta</span><span class="sxs-lookup"><span data-stu-id="31bbe-112">List tables in an account</span></span>
* <span data-ttu-id="31bbe-113">Consulta de entidades numa tabela</span><span class="sxs-lookup"><span data-stu-id="31bbe-113">Query entities in a table</span></span>

<span data-ttu-id="31bbe-114">Cada um destes métodos é apresentada com sobrecargas diferentes para diferentes cenários.</span><span class="sxs-lookup"><span data-stu-id="31bbe-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="31bbe-115">Assíncrona versus síncrona</span><span class="sxs-lookup"><span data-stu-id="31bbe-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="31bbe-116">Porque Olá biblioteca de clientes do Storage para C++ é desenvolvida com Olá [biblioteca C++ REST](https://github.com/Microsoft/cpprestsdk), suportamos inerentemente operações assíncronas utilizando [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="31bbe-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="31bbe-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="31bbe-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="31bbe-118">Operações síncronas moldam operações assíncronas correspondente de Olá:</span><span class="sxs-lookup"><span data-stu-id="31bbe-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="31bbe-119">Se estiver a trabalhar com várias aplicações ou serviços thread, recomendamos que utilize Olá async APIs diretamente em vez de criar uma sincronização de Olá toocall thread APIs, que afeta significativamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="31bbe-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="31bbe-120">Listagem segmentada</span><span class="sxs-lookup"><span data-stu-id="31bbe-120">Segmented listing</span></span>
<span data-ttu-id="31bbe-121">escala de Olá de armazenamento na nuvem necessita de listagem segmentada.</span><span class="sxs-lookup"><span data-stu-id="31bbe-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="31bbe-122">Por exemplo, pode ter um milhões BLOBs no contentor de Blobs do Azure ou através de mil milhões de entidades numa tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="31bbe-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="31bbe-123">Não são números teórico, mas casos de utilização de clientes reais.</span><span class="sxs-lookup"><span data-stu-id="31bbe-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="31bbe-124">Consequentemente, é toolist impractical todos os objetos numa única resposta.</span><span class="sxs-lookup"><span data-stu-id="31bbe-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="31bbe-125">Em vez disso, pode listar objetos utilizando a paginação.</span><span class="sxs-lookup"><span data-stu-id="31bbe-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="31bbe-126">Cada um dos Olá listagem APIs tem um *segmentado* de sobrecarga.</span><span class="sxs-lookup"><span data-stu-id="31bbe-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="31bbe-127">resposta de Olá para uma operação de listagem segmentados inclui:</span><span class="sxs-lookup"><span data-stu-id="31bbe-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="31bbe-128"><i>_segment</i>, que contém o conjunto de Olá de resultados devolvido para toohello uma única chamada de API de listagem.</span><span class="sxs-lookup"><span data-stu-id="31bbe-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="31bbe-129">*continuation_token*, que é transferido toohello próxima chamada na página seguinte do ordem tooget Olá de resultados.</span><span class="sxs-lookup"><span data-stu-id="31bbe-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="31bbe-130">Quando não existem nenhum mais tooreturn de resultados, o token de continuação Olá é nulo.</span><span class="sxs-lookup"><span data-stu-id="31bbe-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="31bbe-131">Por exemplo, uma chamada típico toolist todos os blobs num contentor poderão aparentar ser Olá seguinte fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="31bbe-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="31bbe-132">código de Olá está disponível no nosso [amostras](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="31bbe-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="31bbe-133">Tenha em atenção que o número de Olá de resultados devolvido numa página pode ser controlado pelo parâmetro Olá *max_results* em sobrecarga Olá de cada API, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="31bbe-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="31bbe-134">Se não especificar Olá *max_results* parâmetro, a predefinição de Olá valor máximo de resultados de too5000 é devolvido numa única página.</span><span class="sxs-lookup"><span data-stu-id="31bbe-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="31bbe-135">Tenha também em atenção que uma consulta ao Table storage do Azure pode devolver não registos ou menos registos ao valor de Olá de Olá *max_results* parâmetros que especificou, mesmo que o token de continuação Olá não está vazio.</span><span class="sxs-lookup"><span data-stu-id="31bbe-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="31bbe-136">Uma razão poderá ser que essa consulta Olá não conseguiu concluir a cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="31bbe-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="31bbe-137">Desde que o token de continuação Olá não estiver vazia, consulta Olá deve continuar e o código não deve partem do princípio de tamanho de Olá dos resultados de segmento.</span><span class="sxs-lookup"><span data-stu-id="31bbe-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="31bbe-138">Olá recomendado programação padrão para a maioria dos cenários é segmentado listagem, que fornece o progresso explícito de listagem ou consultar e como o serviço de Olá responde tooeach pedido.</span><span class="sxs-lookup"><span data-stu-id="31bbe-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="31bbe-139">Particularmente serviços ou aplicações de C++, controlo de nível inferior de Olá listagem progresso pode ajudar a memória de controlo e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="31bbe-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="31bbe-140">Listagem abrangente</span><span class="sxs-lookup"><span data-stu-id="31bbe-140">Greedy listing</span></span>
<span data-ttu-id="31bbe-141">Versões anteriores do Olá biblioteca de clientes do Storage para C++ (0.5.0 de versões de pré-visualização e versões anteriores) incluído não-segmentado listagem de APIs para as tabelas e filas, como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="31bbe-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="31bbe-142">Estes métodos foram implementados como wrappers de APIs segmentadas.</span><span class="sxs-lookup"><span data-stu-id="31bbe-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="31bbe-143">Para cada resposta de listagem segmentada, código de Olá anexado vetor de tooa Olá resultados e devolvidos todos os resultados depois de contentores completa Olá foram analisados.</span><span class="sxs-lookup"><span data-stu-id="31bbe-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="31bbe-144">Esta abordagem poderá funcionar quando a conta de armazenamento de Olá ou tabela contém um pequeno número de objetos.</span><span class="sxs-lookup"><span data-stu-id="31bbe-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="31bbe-145">No entanto, com um aumento no número de Olá de objetos, memória Olá necessária pode aumentar, sem limite, porque todos os resultados permanecer na memória.</span><span class="sxs-lookup"><span data-stu-id="31bbe-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="31bbe-146">Uma operação de listagem pode demorar muito tempo, durante o qual Olá autor da chamada não tinha informação sobre o progresso da mesma.</span><span class="sxs-lookup"><span data-stu-id="31bbe-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="31bbe-147">Estes abrangente listagem APIs no Olá SDK não existe em c#, Java, ou Olá ambiente JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="31bbe-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="31bbe-148">tooavoid Olá potenciais problemas de utilizar estas APIs abrangente, removemos-los na versão 0.6.0 pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="31bbe-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="31bbe-149">Se o seu código está a chamar estas APIs abrangente:</span><span class="sxs-lookup"><span data-stu-id="31bbe-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="31bbe-150">Em seguida, deve modificar o seu código toouse Olá segmentado listagem APIs:</span><span class="sxs-lookup"><span data-stu-id="31bbe-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="31bbe-151">Ao especificar Olá *max_results* parâmetro segmento Olá, pode equilibrar entre os números de Olá de pedidos e memória utilização toomeet considerações sobre o desempenho para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="31bbe-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="31bbe-152">Além disso, se estiver a utilizar listagem segmentada APIs, mas armazenar dados de Olá numa coleção local num style "abrangente", também recomendamos vivamente que refatorar a toohandle código armazenar dados numa coleção local cuidadosamente à escala.</span><span class="sxs-lookup"><span data-stu-id="31bbe-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="31bbe-153">Listagem lento</span><span class="sxs-lookup"><span data-stu-id="31bbe-153">Lazy listing</span></span>
<span data-ttu-id="31bbe-154">Embora a listagem abrangente gerado potenciais problemas, é conveniente se não existirem demasiados objetos num contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="31bbe-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="31bbe-155">Se também estiver a utilizar c# ou Oracle Java SDKs, deve estar familiarizado com Olá enumeráveis modelo de programação, que oferece um lento-estilo de listagem, onde hello dados de um determinado desvio é apenas obtidos se for necessário.</span><span class="sxs-lookup"><span data-stu-id="31bbe-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="31bbe-156">No C++, o modelo de com base em iterator Olá também fornece uma abordagem semelhante.</span><span class="sxs-lookup"><span data-stu-id="31bbe-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="31bbe-157">Uma listagem lento típica API, utilizando **list_blobs** como exemplo, se parece com isto:</span><span class="sxs-lookup"><span data-stu-id="31bbe-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="31bbe-158">Um fragmento de código típicas que utiliza o padrão de listagem lento Olá poderá ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="31bbe-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="31bbe-159">Tenha em atenção que a listagem lento só está disponível no modo síncrono.</span><span class="sxs-lookup"><span data-stu-id="31bbe-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="31bbe-160">Em comparação com listagem abrangente, listagem lento obtém dados apenas quando necessário.</span><span class="sxs-lookup"><span data-stu-id="31bbe-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="31bbe-161">Em bastidores Olá, este obtém dados do armazenamento do Azure apenas quando iterator seguinte Olá desloca para segmento seguinte.</span><span class="sxs-lookup"><span data-stu-id="31bbe-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="31bbe-162">Por conseguinte, a utilização de memória é controlada com um tamanho vinculado e operação Olá é rápida.</span><span class="sxs-lookup"><span data-stu-id="31bbe-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="31bbe-163">Listagem lento APIs estão incluídos no Olá biblioteca de clientes do Storage para C++ versão 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="31bbe-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="31bbe-164">Conclusão</span><span class="sxs-lookup"><span data-stu-id="31bbe-164">Conclusion</span></span>
<span data-ttu-id="31bbe-165">Neste artigo, discutimos sobrecargas diferentes para listar as APIs para vários objetos Olá biblioteca de clientes do Storage para C++.</span><span class="sxs-lookup"><span data-stu-id="31bbe-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="31bbe-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="31bbe-166">toosummarize:</span></span>

* <span data-ttu-id="31bbe-167">APIs de Async são vivamente recomendados em vários cenários de thread.</span><span class="sxs-lookup"><span data-stu-id="31bbe-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="31bbe-168">Para a maioria dos cenários, recomenda-se listagem segmentada.</span><span class="sxs-lookup"><span data-stu-id="31bbe-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="31bbe-169">Listagem lento é fornecida na biblioteca de Olá como um wrapper em cenários síncronos conveniente.</span><span class="sxs-lookup"><span data-stu-id="31bbe-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="31bbe-170">Listagem abrangente não é recomendada e foi removida da biblioteca de Olá.</span><span class="sxs-lookup"><span data-stu-id="31bbe-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31bbe-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="31bbe-171">Next steps</span></span>
<span data-ttu-id="31bbe-172">Para obter mais informações sobre o Storage do Azure e a biblioteca de clientes para C++, consulte Olá os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="31bbe-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="31bbe-173">Como toouse Blob Storage do C++</span><span class="sxs-lookup"><span data-stu-id="31bbe-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="31bbe-174">Como toouse Table Storage do C++</span><span class="sxs-lookup"><span data-stu-id="31bbe-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="31bbe-175">Como toouse armazenamento de filas do C++</span><span class="sxs-lookup"><span data-stu-id="31bbe-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="31bbe-176">Biblioteca de clientes de armazenamento do Azure para documentação da API de C++.</span><span class="sxs-lookup"><span data-stu-id="31bbe-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="31bbe-177">Blogue da Equipa de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="31bbe-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="31bbe-178">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="31bbe-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

