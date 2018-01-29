---
title: "A expressão e funções no Azure Data Factory | Microsoft Docs"
description: "Este artigo fornece informações sobre as expressões e as funções que pode utilizar na criação de entidades do data factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: shlo
ms.openlocfilehash: 78f21576bb7d839e5b5c4d8c2b721e381d663406
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="expressions-and-functions-in-azure-data-factory"></a>As expressões e funções no Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 - GA](v1/data-factory-functions-variables.md)
> * [Versão 2 - Pré-visualização](control-flow-expression-language-functions.md)

Este artigo fornece detalhes sobre expressões e funções suportadas pelo Azure Data Factory (versão 2). 

## <a name="introduction"></a>Introdução
Valores JSON na definição do podem ser literal ou expressões que são avaliadas em tempo de execução. Por exemplo:  
  
```json
"name": "value"
```

 (ou)  
  
```json
"name": "@pipeline().parameters.password"
```


> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em pré-visualização. Se estiver a utilizar a versão 1 do serviço do Data Factory, o que é geralmente disponível (DG), consulte [funções e as variáveis no Data Factory V1](v1/data-factory-functions-variables.md).


## <a name="expressions"></a>Expressões  
As expressões podem aparecer em qualquer local, um valor de cadeia JSON e sempre resultar no outro valor JSON. Se um valor JSON é uma expressão, o corpo da expressão é extraído ao remover no início de sessão (@). Se necessitar de uma cadeia literal que começa com @, tem de ser escape utilizando@. Os exemplos seguintes mostram como expressões são avaliadas.  
  
|Valor JSON|Resultado|  
|----------------|------------|  
|"parâmetros de"|Os carateres 'parameters' são devolvidos.|  
|"parâmetros de [1]"|Os carateres 'parameters [1]' são devolvidos.|  
|"@@"|Uma cadeia de 1 caráter que contém ' @' é devolvido.|  
|" @"|Uma cadeia de carateres de 2 que contém ' @' é devolvido.|  
  
 As expressões também pode aparecer dentro de cadeias, através de uma funcionalidade denominada *cadeia interpolação* onde as expressões são moldadas numa `@{ ... }`. Por exemplo: `"name" : "First Name: @{pipeline().parameters.firstName} Last Name: @{pipeline().parameters.lastName}"`  
  
 Utilizar interpolação de cadeia, o resultado é sempre uma cadeia. Diga posso definiu `myNumber` como `42` e `myString` como `foo`:  
  
|Valor JSON|Resultado|  
|----------------|------------|  
|"@pipeline(). parameters.myString"| Devolve `foo` como uma cadeia.|  
|"@{pipeline ().parameters.myString}"| Devolve `foo` como uma cadeia.|  
|"@pipeline(). parameters.myNumber"| Devolve `42` como um *número*.|  
|"@{pipeline ().parameters.myNumber}"| Devolve `42` como um *cadeia*.|  
|"Resposta é: @{pipeline ().parameters.myNumber}"| Devolve a cadeia `Answer is: 42`.|  
|"@concat(' Resposta é: ', string(pipeline().parameters.myNumber))"| Devolve a cadeia`Answer is: 42`|  
|"Resposta é: @ @ {pipeline ().parameters.myNumber}"| Devolve a cadeia `Answer is: @{pipeline().parameters.myNumber}`.|  
  
### <a name="examples"></a>Exemplos

#### <a name="a-dataset-with-a-parameter"></a>Um conjunto de dados com um parâmetro
No exemplo seguinte, o BlobDataset assume um parâmetro com o nome **caminho**. O valor é utilizado para definir um valor para o **folderPath** propriedade utilizando expressões seguintes: `@{dataset().path}`. 

```json
{
    "name": "BlobDataset",
    "properties": {
        "type": "AzureBlob",
        "typeProperties": {
            "folderPath": "@dataset().path"
        },
        "linkedServiceName": {
            "referenceName": "AzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "parameters": {
            "path": {
                "type": "String"
            }
        }
    }
}
```

#### <a name="a-pipeline-with-a-parameter"></a>Um pipeline com um parâmetro
No exemplo seguinte, o pipeline demora **inputPath** e **outputPath** parâmetros. O **caminho** para o blob parametrizado o conjunto de dados está definido utilizando os valores destes parâmetros. A sintaxe utilizada aqui é: `pipeline().parameters.parametername`. 

```json
{
    "name": "Adfv2QuickStartPipeline",
    "properties": {
        "activities": [
            {
                "name": "CopyFromBlobToBlob",
                "type": "Copy",
                "inputs": [
                    {
                        "referenceName": "BlobDataset",
                        "parameters": {
                            "path": "@pipeline().parameters.inputPath"
                        },
                        "type": "DatasetReference"
                    }
                ],
                "outputs": [
                    {
                        "referenceName": "BlobDataset",
                        "parameters": {
                            "path": "@pipeline().parameters.outputPath"
                        },
                        "type": "DatasetReference"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                }
            }
        ],
        "parameters": {
            "inputPath": {
                "type": "String"
            },
            "outputPath": {
                "type": "String"
            }
        }
    }
}
```
  
## <a name="functions"></a>Funções  
 Pode chamar funções dentro de expressões. As secções seguintes fornecem informações sobre as funções que pode ser utilizado numa expressão.  

## <a name="string-functions"></a>Funções de cadeia  
 As seguintes funções só se aplicam a cadeias. Também pode utilizar um número de funções de coleção em cadeias.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|concat|Combina qualquer número de cadeias em conjunto. Por exemplo, se for parameter1 `foo,` a seguinte expressão devolvam `somevalue-foo-somevalue`:`concat('somevalue-',pipeline().parameters.parameter1,'-somevalue')`<br /><br /> **Número de parâmetro**: 1...*n*<br /><br /> **Nome**: cadeia*n*<br /><br /> **Descrição**: necessário. As cadeias de combinar numa cadeia única.|  
|subcadeia|Devolve um subconjunto de carateres a partir de uma cadeia. Por exemplo, a seguinte expressão:<br /><br /> `substring('somevalue-foo-somevalue',10,3)`<br /><br /> Devolve:<br /><br /> `foo`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia a partir da qual foi efetuada a subcadeia.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: índice inicial<br /><br /> **Descrição**: necessário. O índice de onde a subcadeia começa no parâmetro 1.<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: comprimento<br /><br /> **Descrição**: necessário. O comprimento da subcadeia.|  
|Substituir|Substitui uma cadeia com uma determinada cadeia. Por exemplo, a expressão:<br /><br /> `replace('the old string', 'old', 'new')`<br /><br /> Devolve:<br /><br /> `the new string`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário.  Se não for encontrado 2 de parâmetro no parâmetro 1, a cadeia é procurado para o parâmetro 2 e atualizado com o parâmetro 3.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: cadeia antiga<br /><br /> **Descrição**: necessário. A cadeia de substituir pelo parâmetro 3 quando é encontrada uma correspondência no parâmetro 1<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: nova cadeia<br /><br /> **Descrição**: necessário. A cadeia é utilizada para substituir a cadeia no parâmetro 2 quando é encontrada uma correspondência no parâmetro 1.|  
|GUID| Gera uma cadeia exclusiva global (também conhecido como. GUID). Por exemplo, foi possível gerar o seguinte resultado `c2ecc88d-88c8-4096-912c-d6f2e2b138ce`:<br /><br /> `guid()`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. Um especificador de formato único indica [como formatar o valor deste Guid](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). O parâmetro de formato pode ser "N", "D", "B", "P" ou "X". Se o formato não for fornecido, "D" é utilizada.|  
|toLower|Converte uma cadeia em minúsculas. Por exemplo, o seguinte devolve `two by two is four`:`toLower('Two by Two is Four')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia a converter para maiúsculas e minúsculas inferior. Se um carácter na cadeia de não tiver um equivalente em minúsculas, é incluída inalterados na cadeia devolvida.|  
|toUpper|Converte uma cadeia em maiúsculas. Por exemplo, a seguinte expressão devolve `TWO BY TWO IS FOUR`:`toUpper('Two by Two is Four')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia a converter para maiúsculas e minúsculas superior. Se um carácter na cadeia de não tiver um equivalente em maiúsculas, é incluída inalterados na cadeia devolvida.|  
|indexOf|Localize o índice de um valor dentro de um caso de cadeia insensitively. Por exemplo, a seguinte expressão devolve `7`:`indexof('hello, world.', 'world')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia que pode conter o valor.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. O valor a pesquisar o índice da.|  
|lastindexof|Localize o índice de um valor dentro de um caso de cadeia último insensitively. Por exemplo, a seguinte expressão devolve `3`:`lastindexof('foofoo', 'foo')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia que pode conter o valor.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. O valor a pesquisar o índice da.|  
|startswith|Verifica se a cadeia começa com um caso de valor insensitively. Por exemplo, a seguinte expressão devolve `true`:`lastindexof('hello, world', 'hello')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia que pode conter o valor.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. O valor de cadeia pode começar a utilizar.|  
|endswith|Verifica se a cadeia termina com um caso de valor insensitively. Por exemplo, a seguinte expressão devolve `true`:`lastindexof('hello, world', 'world')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia que pode conter o valor.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. O valor de cadeia pode terminar com.|  
|dividir|Divide a cadeia com um separador. Por exemplo, a seguinte expressão devolve `["a", "b", "c"]`:`split('a;b;c',';')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia que é dividida.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. O separador.|  
  
  
## <a name="collection-functions"></a>Funções de coleção  
 Estas funções funcionam sobre as coleções como matrizes, cadeias e, por vezes, dicionários.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|contém|Devolve VERDADEIRO se o dicionário contém uma lista de chaves, contém um valor ou a cadeia contém subcadeia. Por exemplo, a seguinte expressão devolve`true:``contains('abacaba','aca')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: dentro da coleção<br /><br /> **Descrição**: necessário. A coleção para pesquisar no.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: encontrar o objeto<br /><br /> **Descrição**: necessário. O objeto localizar dentro de **dentro da coleção**.|  
|comprimento|Devolve o número de elementos de uma cadeia ou matriz. Por exemplo, a seguinte expressão devolve `3`:`length('abc')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: coleção<br /><br /> **Descrição**: necessário. A coleção para obter o comprimento do.|  
|Vazio|Devolve true se o objeto, cadeia ou matriz está vazia. Por exemplo, a seguinte expressão devolve `true`:<br /><br /> `empty('')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: coleção<br /><br /> **Descrição**: necessário. A coleção para verificar se está vazia.|  
|intersecção|Devolve uma matriz única ou o objeto com os elementos comuns entre as matrizes ou objetos transmitidos ao mesmo. Por exemplo, esta função devolve `[1, 2]`:<br /><br /> `intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])`<br /><br /> Os parâmetros para a função podem ser um conjunto de objetos ou um conjunto de matrizes (não uma mistura de ambos). Se existirem dois objetos com o mesmo nome, o objeto de última com esse nome é apresentado no objeto final.<br /><br /> **Número de parâmetro**: 1...*n*<br /><br /> **Nome**: coleção*n*<br /><br /> **Descrição**: necessário. As coleções a avaliar. Um objeto tem de ser transmitidas nas aparecer nos resultados de todas as coleções.|  
|União|Devolve uma matriz única ou o objeto com todos os elementos que estão na matriz ou objeto transmitidos ao mesmo. Por exemplo, esta função devolve`[1, 2, 3, 10, 101]:`<br /><br /> :`union([1, 2, 3], [101, 2, 1, 10])`<br /><br /> Os parâmetros para a função podem ser um conjunto de objetos ou um conjunto de matrizes (não uma mistura de ambos). Se existirem dois objetos com o mesmo nome no resultado final, o objeto de última com esse nome é apresentado no objeto final.<br /><br /> **Número de parâmetro**: 1...*n*<br /><br /> **Nome**: coleção*n*<br /><br /> **Descrição**: necessário. As coleções a avaliar. Um objeto que é apresentado em qualquer uma das coleções é apresentado nos resultados.|  
|primeiro|Devolve o primeiro elemento da matriz ou a cadeia transmitida. Por exemplo, esta função devolve `0`:<br /><br /> `first([0,2,3])`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: coleção<br /><br /> **Descrição**: necessário. A coleção para tirar o objeto do primeiro.|  
|última|Devolve o último elemento na matriz ou cadeia transmitida. Por exemplo, esta função devolve `3`:<br /><br /> `last('0123')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: coleção<br /><br /> **Descrição**: necessário. A coleção para tirar o objeto de última.|  
|tirar|Devolve o primeiro **contagem** transmitido elementos da matriz ou de cadeia, por exemplo esta função devolve `[1, 2]`:`take([1, 2, 3, 4], 2)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: coleção<br /><br /> **Descrição**: necessário. A coleção para tirar o primeiro **contagem** objetos de.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: contagem<br /><br /> **Descrição**: necessário. O número de objetos a demorar entre o **coleção**. Tem de ser um número inteiro positivo.|  
|Ignorar|Devolve os elementos na matriz que começa no índice **contagem**, por exemplo esta função devolve `[3, 4]`:<br /><br /> `skip([1, 2 ,3 ,4], 2)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: coleção<br /><br /> **Descrição**: necessário. A coleção para ignorar a primeira **contagem** objetos de.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: contagem<br /><br /> **Descrição**: necessário. O número de objetos para remover o início de **coleção**. Tem de ser um número inteiro positivo.|  
  
## <a name="logical-functions"></a>Funções lógicas  
 Estas funções são úteis no interior de condições, pode ser utilizados para avaliar a qualquer tipo de lógica.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|é igual a|Devolve true se dois valores são iguais. Por exemplo, se parameter1 foo, a seguinte expressão devolvam `true`:`equals(pipeline().parameters.parameter1), 'foo')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 de objeto<br /><br /> **Descrição**: necessário. O objeto comparar para **objeto 2**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: objeto 2<br /><br /> **Descrição**: necessário. O objeto comparar para **objeto 1**.|  
|menos|Devolve VERDADEIRO se o primeiro argumento for menor do que o segundo. Tenha em atenção de que os valores só podem ser do tipo número inteiro, flutuante ou uma cadeia. Por exemplo, a seguinte expressão devolve `true`:`less(10,100)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 de objeto<br /><br /> **Descrição**: necessário. O objeto para verificar se é inferior a **objeto 2**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: objeto 2<br /><br /> **Descrição**: necessário. O objeto para verificar se é superior ao **objeto 1**.|  
|lessOrEquals|Devolve true se o primeiro argumento é menor ou igual ao segundo. Tenha em atenção de que os valores só podem ser do tipo número inteiro, flutuante ou uma cadeia. Por exemplo, a seguinte expressão devolve `true`:`lessOrEquals(10,10)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 de objeto<br /><br /> **Descrição**: necessário. O objeto para verificar se é menor ou igual a **objeto 2**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: objeto 2<br /><br /> **Descrição**: necessário. O objeto para verificar se é maior que ou igual a **objeto 1**.|  
|maior|Devolve true se o primeiro argumento é maior do que o segundo. Tenha em atenção de que os valores só podem ser do tipo número inteiro, flutuante ou uma cadeia. Por exemplo, a seguinte expressão devolve `false`:`greater(10,10)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 de objeto<br /><br /> **Descrição**: necessário. O objeto para verificar se é superior ao **objeto 2**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: objeto 2<br /><br /> **Descrição**: necessário. O objeto para verificar se é inferior a **objeto 1**.|  
|greaterOrEquals|Devolve true se o primeiro argumento é igual ou superior para o segundo. Tenha em atenção de que os valores só podem ser do tipo número inteiro, flutuante ou uma cadeia. Por exemplo, a seguinte expressão devolve `false`:`greaterOrEquals(10,100)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 de objeto<br /><br /> **Descrição**: necessário. O objeto para verificar se é maior que ou igual a **objeto 2**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: objeto 2<br /><br /> **Descrição**: necessário. O objeto para verificar se é menor ou igual a **objeto 1**.|  
|e|Devolve true se ambos os parâmetros são verdadeiras. Ambos os argumentos tem de ser em booleanos. A seguinte devolve `false`:`and(greater(1,10),equals(0,0))`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 booleano<br /><br /> **Descrição**: necessário. O primeiro argumento tem de ser `true`.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: 2 booleano<br /><br /> **Descrição**: necessário. O segundo argumento tem de ser `true`.|  
|ou|Devolve true se qualquer um dos parâmetros são VERDADEIRO. Ambos os argumentos tem de ser em booleanos. A seguinte devolve `true`:`or(greater(1,10),equals(0,0))`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 booleano<br /><br /> **Descrição**: necessário. O primeiro argumento que pode ser `true`.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: 2 booleano<br /><br /> **Descrição**: necessário. O segundo argumento pode ser `true`.|  
|não|Devolve VERDADEIRO se o parâmetro for `false`. Ambos os argumentos tem de ser em booleanos. A seguinte devolve `true`:`not(contains('200 Success','Fail'))`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: booleano<br /><br /> **Descrição**: devolve true se o parâmetro é `false`. Ambos os argumentos tem de ser em booleanos. A seguinte devolve `true`:`not(contains('200 Success','Fail'))`|  
|Se|Devolve um valor especificado com base em se os resultados de expressão fornecido no `true` ou `false`.  Por exemplo, o seguinte devolve `"yes"`:`if(equals(1, 1), 'yes', 'no')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: expressão<br /><br /> **Descrição**: necessário. Um valor booleano que determina qual o valor é devolvido pela expressão.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: VERDADEIRO<br /><br /> **Descrição**: necessário. O valor a devolver se a expressão é `true`.<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: False<br /><br /> **Descrição**: necessário. O valor a devolver se a expressão é `false`.|  
  
## <a name="conversion-functions"></a>Funções de conversão  
 Estas funções são utilizadas para a conversão entre cada um dos tipos nativos no idioma:  
  
-   cadeia  
  
-   inteiro  
  
-   flutuante  
  
-   boolean  
  
-   Matrizes  
  
-   dicionários  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|Int|Converta o parâmetro para um número inteiro. Por exemplo, a seguinte expressão devolve 100 como um número, em vez de uma cadeia:`int('100')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: valor<br /><br /> **Descrição**: necessário. O valor que é convertido para um número inteiro.|  
|cadeia|Converta o parâmetro numa cadeia. Por exemplo, a seguinte expressão devolve `'10'`: `string(10)` também pode converter um objeto de uma cadeia, por exemplo, se o **foo** parâmetro é um objeto com uma propriedade `bar : baz`, em seguida, teria o seguinte devolver `{"bar" : "baz"}``string(pipeline().parameters.foo)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: valor<br /><br /> **Descrição**: necessário. O valor que é convertido numa cadeia.|  
|json|Converta o parâmetro para um valor de tipo JSON. É o oposto da string(). Por exemplo, a seguinte expressão devolve `[1,2,3]` como uma matriz, em vez de uma cadeia:<br /><br /> `parse('[1,2,3]')`<br /><br /> Da mesma forma, pode converter uma cadeia para um objeto. Por exemplo, `json('{"bar" : "baz"}')` devolve:<br /><br /> `{ "bar" : "baz" }`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia que é convertida para um valor de tipo nativo.<br /><br /> A função de json suporta também a entrada de xml. Por exemplo, o valor do parâmetro:<br /><br /> `<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>`<br /><br /> é convertido para o seguinte json:<br /><br /> `{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|flutuante|Converta o argumento de parâmetro para um número de vírgula flutuante. Por exemplo, a seguinte expressão devolve `10.333`:`float('10.333')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: valor<br /><br /> **Descrição**: necessário. O valor que é convertido para um número de vírgula flutuante.|  
|bool|Converta o parâmetro booleano. Por exemplo, a seguinte expressão devolve `false`:`bool(0)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: valor<br /><br /> **Descrição**: necessário. O valor que é convertido para um valor booleano.|  
|Unir|Devolve o objeto não nulo primeiro os argumentos transmitidos. Nota: uma cadeia vazia não é nula. Por exemplo, se não for definidos um parâmetros 1 e 2, esta ação devolve `fallback`:`coalesce(pipeline().parameters.parameter1', pipeline().parameters.parameter2 ,'fallback')`<br /><br /> **Número de parâmetro**: 1...*n*<br /><br /> **Nome**: objeto*n*<br /><br /> **Descrição**: necessário. Os objetos para procurar `null`.|  
|Base64|Devolve a representação de base64 de cadeia de entrada. Por exemplo, a seguinte expressão devolve `c29tZSBzdHJpbmc=`:`base64('some string')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: 1 de cadeia<br /><br /> **Descrição**: necessário. A cadeia de codificar para base64 representação.|  
|base64ToBinary|Devolve uma representação binária de uma cadeia codificada em base64. Por exemplo, a seguinte expressão devolve a representação binária de algumas cadeia: `base64ToBinary('c29tZSBzdHJpbmc=')`.<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia codificada em base64.|  
|base64ToString|Devolve uma representação de cadeia de uma cadeia de based64 codificado. Por exemplo, a seguinte expressão devolve algumas cadeia: `base64ToString('c29tZSBzdHJpbmc=')`.<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia codificada em base64.|  
|Binário|Devolve uma representação de um valor binária.  Por exemplo, a seguinte expressão devolve uma representação binária de algumas cadeia:`binary(‘some string’).`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: valor<br /><br /> **Descrição**: necessário. O valor que é convertido em binário.|  
|dataUriToBinary|Devolve uma representação binária de um URI de dados. Por exemplo, a seguinte expressão devolve a representação binária de algumas cadeia:`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. O URI para converter para representação binária de dados.|  
|dataUriToString|Devolve uma representação de cadeia de um URI de dados. Por exemplo, a seguinte expressão devolve algumas cadeia:`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br />**Descrição**: necessário. O URI para converter para representação de cadeia de dados.|  
|dataUri|Devolve um URI de um valor de dados. Por exemplo, a seguinte expressão devolve dados:`text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=: dataUri('some string')`<br /><br /> **Número de parâmetro**: 1<br /><br />**Nome**: valor<br /><br />**Descrição**: necessário. O valor para converter para o URI de dados.|  
|decodeBase64|Devolve uma representação de cadeia de uma cadeia de entrada based64. Por exemplo, a seguinte expressão devolve `some string`:`decodeBase64('c29tZSBzdHJpbmc=')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: devolve uma representação de cadeia de uma cadeia de entrada based64.|  
|encodeUriComponent|URL escapes a cadeia que é transmitida no. Por exemplo, a seguinte expressão devolve `You+Are%3ACool%2FAwesome`:`encodeUriComponent('You Are:Cool/Awesome')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia para o escape carateres não seguro URL do.|  
|decodeUriComponent|Anular-URL-escapes a cadeia que é transmitida no. Por exemplo, a seguinte expressão devolve `You Are:Cool/Awesome`:`encodeUriComponent('You+Are%3ACool%2FAwesome')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. A cadeia de descodificar os carateres não seguro URL do.|  
|decodeDataUri|Devolve uma representação binária de dados de entrada, cadeia URI. Por exemplo, a seguinte expressão devolve a representação binária do `some string`:`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br /> **Descrição**: necessário. DataURI descodificar para uma representação binária.|  
|uriComponent|Devolve um URI codificado representação de um valor. Por exemplo, a seguinte expressão devolve`You+Are%3ACool%2FAwesome: uriComponent('You Are:Cool/Awesome ')`<br /><br /> Detalhes de parâmetro: Número: 1, nome: cadeia, Descrição: necessário. A cadeia a ser URI codificado.|  
|uriComponentToBinary|Devolve que uma representação binária de um URI cadeia codificada. Por exemplo, a seguinte expressão devolve uma representação binária do `You Are:Cool/Awesome`:`uriComponentToBinary('You+Are%3ACool%2FAwesome')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: cadeia<br /><br />**Descrição**: necessário. A cadeia URI codificado.|  
|uriComponentToString|Devolve que uma representação de cadeia de um URI cadeia codificada. Por exemplo, a seguinte expressão devolve `You Are:Cool/Awesome`:`uriComponentToBinary('You+Are%3ACool%2FAwesome')`<br /><br /> **Número de parâmetro**: 1<br /><br />**Nome**: cadeia<br /><br />**Descrição**: necessário. A cadeia URI codificado.|  
|xml|Devolve uma representação xml do valor. Por exemplo, a seguinte expressão devolve um conteúdo xml representado pelo `'\<name>Alan\</name>'`: `xml('\<name>Alan\</name>')`. A função de xml suporta, bem como entrada de objeto em JSON. Por exemplo, o parâmetro `{ "abc": "xyz" }` é convertido para um conteúdo de xml`\<abc>xyz\</abc>`<br /><br /> **Número de parâmetro**: 1<br /><br />**Nome**: valor<br /><br />**Descrição**: necessário. O valor a converter XML.|  
|XPath|Devolva uma matriz de correspondência de expressão de xpath de um valor que avalia a expressão de xpath para nós de xml.<br /><br />  **Exemplo 1**<br /><br /> Assuma que o valor do parâmetro 'p1' é uma representação de cadeia do XML seguinte:<br /><br /> `<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>`<br /><br /> 1. Este código:`xpath(xml(pipeline().parameters.p1), '/lab/robot/name')`<br /><br /> devolvam<br /><br /> `[ <name>R1</name>, <name>R2</name> ]`<br /><br /> enquanto<br /><br /> 2. Este código:`xpath(xml(pipeline().parameters.p1, ' sum(/lab/robot/parts)')`<br /><br /> devolvam<br /><br /> `13`<br /><br /> <br /><br /> **Exemplo 2**<br /><br /> Dado o seguinte conteúdo XML:<br /><br /> `<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>`<br /><br /> 1.  Este código:`@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')`<br /><br /> ou<br /><br /> 2. Este código:`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')`<br /><br /> Devolve<br /><br /> `<Location xmlns="http://foo.com">bar</Location>`<br /><br /> e<br /><br /> 3. Este código:`@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')`<br /><br /> Devolve<br /><br /> ``bar``<br /><br /> **Número de parâmetro**: 1<br /><br />**Nome**: Xml<br /><br />**Descrição**: necessário. O XML no qual se avalia a expressão XPath.<br /><br /> **Número de parâmetro**: 2<br /><br />**Nome**: XPath<br /><br />**Descrição**: necessário. A expressão de XPath para avaliar.|  
|array|Converta o parâmetro de uma matriz.  Por exemplo, a seguinte expressão devolve `["abc"]`:`array('abc')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: valor<br /><br /> **Descrição**: necessário. O valor que é convertido numa matriz.|
|createArray|Cria uma matriz de parâmetros.  Por exemplo, a seguinte expressão devolve `["a", "c"]`:`createArray('a', 'c')`<br /><br /> **Número de parâmetro**: 1... n<br /><br /> **Nome**: quaisquer n<br /><br /> **Descrição**: necessário. Os valores para combinar numa matriz.|

## <a name="math-functions"></a>Funções matemáticas  
 Estas funções podem ser utilizadas para qualquer um dos tipos de números: **números inteiros** e **floats**.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|adicionar|Devolve o resultado da adição de dois números. Por exemplo, esta função devolve `20.333`:`add(10,10.333)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Summand 1<br /><br /> **Descrição**: necessário. O número para adicionar a **Summand 2**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: Summand 2<br /><br /> **Descrição**: necessário. O número para adicionar a **Summand 1**.|  
|sub|Devolve o resultado da subtração dos dois números. Por exemplo, esta função devolve: `-0.333`:<br /><br /> `sub(10,10.333)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Minuend<br /><br /> **Descrição**: necessário. O número que **Subtrahend** é removido.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: Subtrahend<br /><br /> **Descrição**: necessário. O número para remover o **Minuend**.|  
|MUL|Devolve o resultado da multiplicação de dois números. Por exemplo, o seguinte devolve `103.33`:<br /><br /> `mul(10,10.333)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Multiplicand 1<br /><br /> **Descrição**: necessário. O número a multiplicar **Multiplicand 2** com.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: Multiplicand 2<br /><br /> **Descrição**: necessário. O número a multiplicar **Multiplicand 1** com.|  
|Div|Devolve o resultado da divisão dos dois números. Por exemplo, o seguinte devolve `1.0333`:<br /><br /> `div(10.333,10)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: dividendo<br /><br /> **Descrição**: necessário. O número dividir pelo **Divisor**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: Divisor<br /><br /> **Descrição**: necessário. O número dividir o **dividendo** pelo.|  
|MOD|Devolve o resultado do resto após a divisão dos dois números (módulo). Por exemplo, a seguinte expressão devolve `2`:<br /><br /> `mod(10,4)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: dividendo<br /><br /> **Descrição**: necessário. O número dividir pelo **Divisor**.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: Divisor<br /><br /> **Descrição**: necessário. O número dividir o **dividendo** pelo. Após a divisão, os restantes foi atribuído.|  
|min.|Existem dois padrões diferentes para chamar esta função: `min([0,1,2])` aqui min assume uma matriz. Esta expressão devolve `0`. Em alternativa, esta função pode demorar uma lista separada por vírgulas de valores: `min(0,1,2)` esta função devolve também 0. Tenha em atenção de que todos os valores têm de ser números, pelo que o se o parâmetro é uma matriz tem de conter apenas números na mesma.<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: ou valor de coleção<br /><br /> **Descrição**: necessário. Este pode ser uma matriz de valores para localizar o valor mínimo ou o primeiro valor de um conjunto.<br /><br /> **Número de parâmetro**: 2...*n*<br /><br /> **Nome**: valor*n*<br /><br /> **Descrição**: opcional. Se o primeiro parâmetro é um valor, em seguida, pode passar valores adicionais e o mínimo de todos os valores transmitidos são devolvidos.|  
|máx.|Existem dois padrões diferentes para chamar esta função:`max([0,1,2])`<br /><br /> Aqui máx. assume uma matriz. Esta expressão devolve `2`. Em alternativa, esta função pode demorar uma lista separada por vírgulas de valores: `max(0,1,2)` esta função devolve 2. Tenha em atenção de que todos os valores têm de ser números, pelo que o se o parâmetro é uma matriz tem de conter apenas números na mesma.<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: ou valor de coleção<br /><br /> **Descrição**: necessário. Este pode ser uma matriz de valores para localizar o valor máximo ou o primeiro valor de um conjunto.<br /><br /> **Número de parâmetro**: 2...*n*<br /><br /> **Nome**: valor*n*<br /><br /> **Descrição**: opcional. Se o primeiro parâmetro é um valor, em seguida, pode passar valores adicionais e o número máximo de todos os valores transmitidos são devolvidos.|  
|intervalo| Gera uma matriz de números inteiros a partir de um determinado número, e definir o comprimento da matriz devolvido. Por exemplo, esta função devolve `[3,4,5,6]`:<br /><br /> `range(3,4)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: índice inicial<br /><br /> **Descrição**: necessário. É o número inteiro primeiro na matriz.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: contagem<br /><br /> **Descrição**: necessário. Número de números inteiros que estão na matriz.|  
|rand| Gera um número inteiro aleatório dentro do intervalo especificado (inclusive em ambas as extremidades. Por exemplo, isto pode devolver `42`:<br /><br /> `rand(-1000,1000)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: mínimo<br /><br /> **Descrição**: necessário. O número inteiro menor que pode ser devolvido.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: máximo<br /><br /> **Descrição**: necessário. O maior número inteiro que pode ser devolvido.|  
  
## <a name="date-functions"></a>Funções de data  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|utcnow|Devolve o timestamp atual como uma cadeia. Por exemplo `2015-03-15T13:27:36Z`:<br /><br /> `utcnow()`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. É um [único caráter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrão de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como formatar o valor deste carimbo. Se o formato não for fornecido, é utilizado o formato ISO 8601 ("o").|  
|addseconds|Adiciona um número inteiro de segundos para um carimbo de cadeia transmitido. O número de segundos pode ser positivo ou negativo. O resultado é uma cadeia no formato ISO 8601 ("o") por predefinição, a menos que é fornecido um especificador de formato. Por exemplo `2015-03-15T13:27:00Z`:<br /><br /> `addseconds('2015-03-15T13:27:36Z', -36)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrição**: necessário. Uma cadeia que contém a hora.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: segundos<br /><br /> **Descrição**: necessário. O número de segundos a adicionar. Pode ser negativo subtrair segundos.<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. É um [único caráter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrão de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como formatar o valor deste carimbo. Se o formato não for fornecido, é utilizado o formato ISO 8601 ("o").|  
|addminutes|Adiciona um número inteiro de minutos para um carimbo de cadeia transmitido. O número de minutos pode ser positivo ou negativo. O resultado é uma cadeia no formato ISO 8601 ("o") por predefinição, a menos que é fornecido um especificador de formato. Por exemplo, `2015-03-15T14:00:36Z`:<br /><br /> `addminutes('2015-03-15T13:27:36Z', 33)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrição**: necessário. Uma cadeia que contém a hora.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: minutos<br /><br /> **Descrição**: necessário. O número de minutos para adicionar. Pode ser negativo subtrair minutos.<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. É um [único caráter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrão de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como formatar o valor deste carimbo. Se o formato não for fornecido, é utilizado o formato ISO 8601 ("o").|  
|addhours|Adiciona um número inteiro de horas para um carimbo de cadeia transmitido. O número de horas pode ser positivo ou negativo. O resultado é uma cadeia no formato ISO 8601 ("o") por predefinição, a menos que é fornecido um especificador de formato. Por exemplo `2015-03-16T01:27:36Z`:<br /><br /> `addhours('2015-03-15T13:27:36Z', 12)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrição**: necessário. Uma cadeia que contém a hora.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: horas<br /><br /> **Descrição**: necessário. O número de horas para adicionar. Pode ser negativo subtrair horas.<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. É um [único caráter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrão de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como formatar o valor deste carimbo. Se o formato não for fornecido, é utilizado o formato ISO 8601 ("o").|  
|adddays|Adiciona um número inteiro de dias para um carimbo de cadeia transmitido. O número de dias pode ser positivo ou negativo. O resultado é uma cadeia no formato ISO 8601 ("o") por predefinição, a menos que é fornecido um especificador de formato. Por exemplo `2015-02-23T13:27:36Z`:<br /><br /> `addseconds('2015-03-15T13:27:36Z', -20)`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrição**: necessário. Uma cadeia que contém a hora.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: dias<br /><br /> **Descrição**: necessário. O número de dias a adicionar. Pode ser negativo subtrair dias.<br /><br /> **Número de parâmetro**: 3<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. É um [único caráter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrão de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como formatar o valor deste carimbo. Se o formato não for fornecido, é utilizado o formato ISO 8601 ("o").|  
|FormatDateTime|Devolve uma cadeia no formato de data. O resultado é uma cadeia no formato ISO 8601 ("o") por predefinição, a menos que é fornecido um especificador de formato. Por exemplo `2015-02-23T13:27:36Z`:<br /><br /> `formatDateTime('2015-03-15T13:27:36Z', 'o')`<br /><br /> **Número de parâmetro**: 1<br /><br /> **Nome**: data<br /><br /> **Descrição**: necessário. Uma cadeia que contém a data.<br /><br /> **Número de parâmetro**: 2<br /><br /> **Nome**: formato<br /><br /> **Descrição**: opcional. É um [único caráter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrão de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como formatar o valor deste carimbo. Se o formato não for fornecido, é utilizado o formato ISO 8601 ("o").|  

## <a name="next-steps"></a>Passos Seguintes
Para obter uma lista de variáveis de sistema pode utilizar expressões, consulte [variáveis do sistema](control-flow-system-variables.md).