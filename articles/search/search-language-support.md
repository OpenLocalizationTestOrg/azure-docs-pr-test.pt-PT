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
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Criar um índice para documentos em vários idiomas na Azure Search
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing Olá potência de analisadores de idioma é tão fácil como uma propriedade de definição num campo na definição de índice de Olá pesquisável. Agora pode efetuar este passo no portal de Olá.

Seguem-se capturas de ecrã da Olá painéis do Portal do Azure para a pesquisa do Azure que permitem que os utilizadores toodefine um esquema de índice. A partir deste painel, os utilizadores podem criar todos os campos de Olá e definir a propriedade do analisador de Olá para cada um deles.

> [!IMPORTANT]
> Só é possível definir um analisador de idioma durante a definição de campo, como no quando criar um novo índice de Olá fundo cópias de segurança ou ao adicionar um novo índice de tooan do campo existente. Certifique-se de que especificar todos os atributos, incluindo analyzer Olá, ao criar o campo de Olá completamente. Não ser capaz de tooedit atributos Olá ou alterar o tipo de analisador Olá depois de guardar as alterações.
>
>

## <a name="define-a-new-field-definition"></a>Definir uma nova definição de campo
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) e abra Olá serviço painel do seu serviço de pesquisa.
2. Clique em **Adicionar índice** no comando Olá barra, Olá parte superior do toostart de dashboard de serviço Olá um novo índice ou abra um tooset índice existente um analisador de novos campos estiver a adicionar tooan de índice existente.
3. é apresentado o painel de campos de Olá, dando-lhe opções para definir o esquema de Olá do índice de Olá, incluindo o separador de analisador Olá utilizado para escolher um analisador de idioma.
4. Nos campos, inicie uma definição de campo, fornecendo um nome, escolher tipo de dados de Olá e definir o campo de Olá toomark atributos como texto completo nos resultados de pesquisa, utilizáveis em estruturas de navegação de Faceta, recuperável, pesquisável ordenável e assim forth.
5. Antes de mover num campo seguinte toohello, abra Olá **analisador** separador.

![][1]
*tooselect um analyzer, clique em separador de analisador Olá no painel de campos de Olá*

## <a name="choose-an-analyzer"></a>Escolha um analisador
1. Deslocamento toofind Olá o campo que está a definir.
2. Se ainda não marcado campo Olá como pesquisável, clique em Olá caixa de verificação agora toomark como **pesquisável**.
3. Clique Olá analisador área toodisplay Olá lista dos analisadores disponíveis.
4. Escolha o analisador de Olá pretende toouse.

![][2]
*Selecione um dos analisadores de Olá suportado para cada campo*

Por predefinição, todos os campos pesquisáveis utilizam Olá [Lucene padrão analisador](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que desconhece idioma. tooview Olá obter uma lista completa dos analisadores de suportados, consulte [suporte de idiomas da Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Assim que o analisador de idioma Olá está selecionado para um campo, será utilizado com cada pedido de indexação e de pesquisa para esse campo. Quando uma consulta é emitida contra vários campos utilizando analisadores de diferentes, consulta Olá será processada independentemente pelo analisadores de direito de Olá para cada campo.

Muitas aplicações móveis e web servem os utilizadores à volta de globo Olá utilizando vários idiomas. É possível toodefine um índice para um cenário assim através da criação de um campo para cada idioma suportado.

![][3]
*Definição de índice com um campo de descrição para cada idioma suportado*

Se o idioma de Olá do agente de Olá emitir uma consulta é conhecido, um pedido de pesquisa pode ser confinada tooa campo específico utilizando Olá **searchFields** parâmetro de consulta. Olá seguinte consulta será emitida apenas em relação a descrição de Olá na Polaco:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Pode consultar o índice do portal de Olá, utilizando **Explorador de pesquisa** toopaste num toohello semelhante de consulta mostrado acima. Explorador de pesquisa está disponível a partir da barra de comando Olá no painel de serviço Olá. Consulte [consultar o índice da Azure Search no portal de Olá](search-explorer.md) para obter mais detalhes.

Por vezes, hello idioma do agente de Olá emitir uma consulta não é conhecido, na qual Olá maiúsculas consulta pode ser emitida contra todos os campos em simultâneo. Se for necessário, preferência resulta num determinado idioma pode ser definida utilizando [classificação perfis](https://msdn.microsoft.com/library/azure/dn798928.aspx). Exemplo de Olá abaixo, correspondências encontradas na descrição Olá em inglês serão classificar superior toomatches relativo no polaco e francês:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Se tiver um programador de .NET, tenha em atenção que pode configurar analisadores de idiomas utilizando Olá [SDK .NET da Azure Search](http://www.nuget.org/packages/Microsoft.Azure.Search). versão mais recente Olá inclui suporte para Olá Microsoft dos analisadores de idiomas bem.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
