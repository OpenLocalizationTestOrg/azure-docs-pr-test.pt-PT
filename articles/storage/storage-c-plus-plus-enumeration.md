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
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Lista de recursos de armazenamento do Azure em C++
As operações de listagem são cenários de desenvolvimento de toomany chave com o Storage do Azure. Este artigo descreve como toomost enumerar objetos no Storage do Azure utilizando Olá listagem APIs fornecidas Olá biblioteca de clientes de armazenamento do Microsoft Azure para C++ forma eficiente.

> [!NOTE]
> Este guia destina-se Olá biblioteca de clientes do Storage do Azure para a versão de C++ 2, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Olá biblioteca de clientes de armazenamento fornece uma variedade de toolist métodos ou os objetos de consulta no armazenamento do Azure. Este artigo aborda Olá os seguintes cenários:

* Lista de contentores numa conta
* Lista de blobs num contentor ou diretório virtual blob
* Filas de lista numa conta
* Lista de tabelas numa conta
* Consulta de entidades numa tabela

Cada um destes métodos é apresentada com sobrecargas diferentes para diferentes cenários.

## <a name="asynchronous-versus-synchronous"></a>Assíncrona versus síncrona
Porque Olá biblioteca de clientes do Storage para C++ é desenvolvida com Olá [biblioteca C++ REST](https://github.com/Microsoft/cpprestsdk), suportamos inerentemente operações assíncronas utilizando [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Por exemplo:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Operações síncronas moldam operações assíncronas correspondente de Olá:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Se estiver a trabalhar com várias aplicações ou serviços thread, recomendamos que utilize Olá async APIs diretamente em vez de criar uma sincronização de Olá toocall thread APIs, que afeta significativamente o desempenho.

## <a name="segmented-listing"></a>Listagem segmentada
escala de Olá de armazenamento na nuvem necessita de listagem segmentada. Por exemplo, pode ter um milhões BLOBs no contentor de Blobs do Azure ou através de mil milhões de entidades numa tabela do Azure. Não são números teórico, mas casos de utilização de clientes reais.

Consequentemente, é toolist impractical todos os objetos numa única resposta. Em vez disso, pode listar objetos utilizando a paginação. Cada um dos Olá listagem APIs tem um *segmentado* de sobrecarga.

resposta de Olá para uma operação de listagem segmentados inclui:

* <i>_segment</i>, que contém o conjunto de Olá de resultados devolvido para toohello uma única chamada de API de listagem.
* *continuation_token*, que é transferido toohello próxima chamada na página seguinte do ordem tooget Olá de resultados. Quando não existem nenhum mais tooreturn de resultados, o token de continuação Olá é nulo.

Por exemplo, uma chamada típico toolist todos os blobs num contentor poderão aparentar ser Olá seguinte fragmento de código. código de Olá está disponível no nosso [amostras](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

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

Tenha em atenção que o número de Olá de resultados devolvido numa página pode ser controlado pelo parâmetro Olá *max_results* em sobrecarga Olá de cada API, por exemplo:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Se não especificar Olá *max_results* parâmetro, a predefinição de Olá valor máximo de resultados de too5000 é devolvido numa única página.

Tenha também em atenção que uma consulta ao Table storage do Azure pode devolver não registos ou menos registos ao valor de Olá de Olá *max_results* parâmetros que especificou, mesmo que o token de continuação Olá não está vazio. Uma razão poderá ser que essa consulta Olá não conseguiu concluir a cinco segundos. Desde que o token de continuação Olá não estiver vazia, consulta Olá deve continuar e o código não deve partem do princípio de tamanho de Olá dos resultados de segmento.

Olá recomendado programação padrão para a maioria dos cenários é segmentado listagem, que fornece o progresso explícito de listagem ou consultar e como o serviço de Olá responde tooeach pedido. Particularmente serviços ou aplicações de C++, controlo de nível inferior de Olá listagem progresso pode ajudar a memória de controlo e o desempenho.

## <a name="greedy-listing"></a>Listagem abrangente
Versões anteriores do Olá biblioteca de clientes do Storage para C++ (0.5.0 de versões de pré-visualização e versões anteriores) incluído não-segmentado listagem de APIs para as tabelas e filas, como no seguinte exemplo de Olá:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Estes métodos foram implementados como wrappers de APIs segmentadas. Para cada resposta de listagem segmentada, código de Olá anexado vetor de tooa Olá resultados e devolvidos todos os resultados depois de contentores completa Olá foram analisados.

Esta abordagem poderá funcionar quando a conta de armazenamento de Olá ou tabela contém um pequeno número de objetos. No entanto, com um aumento no número de Olá de objetos, memória Olá necessária pode aumentar, sem limite, porque todos os resultados permanecer na memória. Uma operação de listagem pode demorar muito tempo, durante o qual Olá autor da chamada não tinha informação sobre o progresso da mesma.

Estes abrangente listagem APIs no Olá SDK não existe em c#, Java, ou Olá ambiente JavaScript Node.js. tooavoid Olá potenciais problemas de utilizar estas APIs abrangente, removemos-los na versão 0.6.0 pré-visualização.

Se o seu código está a chamar estas APIs abrangente:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Em seguida, deve modificar o seu código toouse Olá segmentado listagem APIs:

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

Ao especificar Olá *max_results* parâmetro segmento Olá, pode equilibrar entre os números de Olá de pedidos e memória utilização toomeet considerações sobre o desempenho para a sua aplicação.

Além disso, se estiver a utilizar listagem segmentada APIs, mas armazenar dados de Olá numa coleção local num style "abrangente", também recomendamos vivamente que refatorar a toohandle código armazenar dados numa coleção local cuidadosamente à escala.

## <a name="lazy-listing"></a>Listagem lento
Embora a listagem abrangente gerado potenciais problemas, é conveniente se não existirem demasiados objetos num contentor de Olá.

Se também estiver a utilizar c# ou Oracle Java SDKs, deve estar familiarizado com Olá enumeráveis modelo de programação, que oferece um lento-estilo de listagem, onde hello dados de um determinado desvio é apenas obtidos se for necessário. No C++, o modelo de com base em iterator Olá também fornece uma abordagem semelhante.

Uma listagem lento típica API, utilizando **list_blobs** como exemplo, se parece com isto:

```cpp
list_blob_item_iterator list_blobs() const;
```

Um fragmento de código típicas que utiliza o padrão de listagem lento Olá poderá ter o seguinte aspeto:

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

Tenha em atenção que a listagem lento só está disponível no modo síncrono.

Em comparação com listagem abrangente, listagem lento obtém dados apenas quando necessário. Em bastidores Olá, este obtém dados do armazenamento do Azure apenas quando iterator seguinte Olá desloca para segmento seguinte. Por conseguinte, a utilização de memória é controlada com um tamanho vinculado e operação Olá é rápida.

Listagem lento APIs estão incluídos no Olá biblioteca de clientes do Storage para C++ versão 2.2.0.

## <a name="conclusion"></a>Conclusão
Neste artigo, discutimos sobrecargas diferentes para listar as APIs para vários objetos Olá biblioteca de clientes do Storage para C++. toosummarize:

* APIs de Async são vivamente recomendados em vários cenários de thread.
* Para a maioria dos cenários, recomenda-se listagem segmentada.
* Listagem lento é fornecida na biblioteca de Olá como um wrapper em cenários síncronos conveniente.
* Listagem abrangente não é recomendada e foi removida da biblioteca de Olá.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre o Storage do Azure e a biblioteca de clientes para C++, consulte Olá os seguintes recursos.

* [Como toouse Blob Storage do C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse Table Storage do C++](storage-c-plus-plus-how-to-use-tables.md)
* [Como toouse armazenamento de filas do C++](storage-c-plus-plus-how-to-use-queues.md)
* [Biblioteca de clientes de armazenamento do Azure para documentação da API de C++.](http://azure.github.io/azure-storage-cpp/)
* [Blogue da Equipa de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)

