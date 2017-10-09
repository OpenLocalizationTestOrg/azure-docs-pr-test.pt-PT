---
title: "aaaAzure idioma de várias pesquisa | Microsoft Docs"
description: A pesquisa do Azure suporta 56 idiomas, tirar partido dos analisadores de idiomas da tecnologia de Lucene e processamento de linguagem Natural da Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="6fd6c-103">Criar um índice para documentos em vários idiomas na Azure Search</span><span class="sxs-lookup"><span data-stu-id="6fd6c-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="6fd6c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6fd6c-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="6fd6c-105">REST</span><span class="sxs-lookup"><span data-stu-id="6fd6c-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="6fd6c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="6fd6c-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="6fd6c-107">Unleashing Olá potência de analisadores de idioma é tão fácil como uma propriedade de definição num campo na definição de índice de Olá pesquisável.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="6fd6c-108">Agora pode efetuar este passo no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="6fd6c-109">Seguem-se capturas de ecrã da Olá painéis do Portal do Azure para a pesquisa do Azure que permitem que os utilizadores toodefine um esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="6fd6c-110">A partir deste painel, os utilizadores podem criar todos os campos de Olá e definir a propriedade do analisador de Olá para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fd6c-111">Só é possível definir um analisador de idioma durante a definição de campo, como no quando criar um novo índice de Olá fundo cópias de segurança ou ao adicionar um novo índice de tooan do campo existente.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="6fd6c-112">Certifique-se de que especificar todos os atributos, incluindo analyzer Olá, ao criar o campo de Olá completamente.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="6fd6c-113">Não ser capaz de tooedit atributos Olá ou alterar o tipo de analisador Olá depois de guardar as alterações.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="6fd6c-114">Definir uma nova definição de campo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-114">Define a new field definition</span></span>
1. <span data-ttu-id="6fd6c-115">Inicie sessão no toohello [portal do Azure](https://portal.azure.com) e abra Olá serviço painel do seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="6fd6c-116">Clique em **Adicionar índice** no comando Olá barra, Olá parte superior do toostart de dashboard de serviço Olá um novo índice ou abra um tooset índice existente um analisador de novos campos estiver a adicionar tooan de índice existente.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="6fd6c-117">é apresentado o painel de campos de Olá, dando-lhe opções para definir o esquema de Olá do índice de Olá, incluindo o separador de analisador Olá utilizado para escolher um analisador de idioma.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="6fd6c-118">Nos campos, inicie uma definição de campo, fornecendo um nome, escolher tipo de dados de Olá e definir o campo de Olá toomark atributos como texto completo nos resultados de pesquisa, utilizáveis em estruturas de navegação de Faceta, recuperável, pesquisável ordenável e assim forth.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="6fd6c-119">Antes de mover num campo seguinte toohello, abra Olá **analisador** separador.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="6fd6c-120">![][1]
*tooselect um analyzer, clique em separador de analisador Olá no painel de campos de Olá*</span><span class="sxs-lookup"><span data-stu-id="6fd6c-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="6fd6c-121">Escolha um analisador</span><span class="sxs-lookup"><span data-stu-id="6fd6c-121">Choose an analyzer</span></span>
1. <span data-ttu-id="6fd6c-122">Deslocamento toofind Olá o campo que está a definir.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="6fd6c-123">Se ainda não marcado campo Olá como pesquisável, clique em Olá caixa de verificação agora toomark como **pesquisável**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="6fd6c-124">Clique Olá analisador área toodisplay Olá lista dos analisadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="6fd6c-125">Escolha o analisador de Olá pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="6fd6c-126">![][2]
*Selecione um dos analisadores de Olá suportado para cada campo*</span><span class="sxs-lookup"><span data-stu-id="6fd6c-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="6fd6c-127">Por predefinição, todos os campos pesquisáveis utilizam Olá [Lucene padrão analisador](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que desconhece idioma.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="6fd6c-128">tooview Olá obter uma lista completa dos analisadores de suportados, consulte [suporte de idiomas da Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="6fd6c-129">Assim que o analisador de idioma Olá está selecionado para um campo, será utilizado com cada pedido de indexação e de pesquisa para esse campo.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="6fd6c-130">Quando uma consulta é emitida contra vários campos utilizando analisadores de diferentes, consulta Olá será processada independentemente pelo analisadores de direito de Olá para cada campo.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="6fd6c-131">Muitas aplicações móveis e web servem os utilizadores à volta de globo Olá utilizando vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="6fd6c-132">É possível toodefine um índice para um cenário assim através da criação de um campo para cada idioma suportado.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="6fd6c-133">![][3]
*Definição de índice com um campo de descrição para cada idioma suportado*</span><span class="sxs-lookup"><span data-stu-id="6fd6c-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="6fd6c-134">Se o idioma de Olá do agente de Olá emitir uma consulta é conhecido, um pedido de pesquisa pode ser confinada tooa campo específico utilizando Olá **searchFields** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="6fd6c-135">Olá seguinte consulta será emitida apenas em relação a descrição de Olá na Polaco:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="6fd6c-136">Pode consultar o índice do portal de Olá, utilizando **Explorador de pesquisa** toopaste num toohello semelhante de consulta mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="6fd6c-137">Explorador de pesquisa está disponível a partir da barra de comando Olá no painel de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="6fd6c-138">Consulte [consultar o índice da Azure Search no portal de Olá](search-explorer.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="6fd6c-139">Por vezes, hello idioma do agente de Olá emitir uma consulta não é conhecido, na qual Olá maiúsculas consulta pode ser emitida contra todos os campos em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="6fd6c-140">Se for necessário, preferência resulta num determinado idioma pode ser definida utilizando [classificação perfis](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="6fd6c-141">Exemplo de Olá abaixo, correspondências encontradas na descrição Olá em inglês serão classificar superior toomatches relativo no polaco e francês:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="6fd6c-142">Se tiver um programador de .NET, tenha em atenção que pode configurar analisadores de idiomas utilizando Olá [SDK .NET da Azure Search](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="6fd6c-143">versão mais recente Olá inclui suporte para Olá Microsoft dos analisadores de idiomas bem.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
