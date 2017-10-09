---
title: "referência do motor de regras de aaaAzure CDN | Microsoft Docs"
description: "Documentação de referência para a CDN do Azure regras de funcionalidades e as condições de correspondência do motor."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Motor de regras CDN do Azure
Este tópico lista as descrições detalhadas das condições de correspondência disponíveis Olá e funcionalidades de rede de entrega de conteúdos (CDN) do Azure [motor de regras](cdn-rules-engine.md).

Olá motor de regras de HTTP é concebida toobe Olá final autoridade em específicos como tipos de pedidos processados pelo Olá CDN.

**Utilizações comuns**:

- Substituição ou definir uma política de cache personalizada.
- Proteger ou negar pedidos para conteúdo confidencial.
- Redirecionar pedidos.
- Armazenar dados de registo personalizado.

## <a name="terminology"></a>Terminologia
Uma regra está definida através da utilização de Olá de [ **expressões condicionais**](cdn-rules-engine-reference-conditional-expressions.md), [ **corresponde**](cdn-rules-engine-reference-match-conditions.md), e [  **funcionalidades**](cdn-rules-engine-reference-features.md). Estes elementos são realçados na Olá seguinte ilustração.

 ![Condição de correspondência CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Sintaxe

forma Olá no qual serão tratados carateres especiais varia de acordo com toohow uma condição de correspondência ou valores de texto de identificadores de funcionalidade. Uma condição de correspondência ou a funcionalidade pode interpretar texto dos Olá seguintes formas:

1. [**Valores literais**](#literal-values) 
2. [**Valores de caráter universal**](#wildcard-values)
3. [**Expressões regulares**](#regular-expressions)

### <a name="literal-values"></a>Valores literais
Texto que é interpretado como um valor literal irão tratar todos os carateres especiais, com exceção de Olá do símbolo de % Olá, como parte do valor Olá deve corresponder. Por outras palavras, um literal corresponde à condição definida demasiado`\'*'\` só pode ser satisfeita quando exacta que o valor (ou seja, `\'*'\`) foi encontrado.
 
Um símbolo de percentagem é utilizado tooindicate URL codificação (por exemplo, `%20`).

### <a name="wildcard-values"></a>Valores de caráter universal
Texto que é interpretado como um valor de caráter universal atribuirá carateres de toospecial significado adicionais. Olá, a tabela seguinte descreve como Olá seguinte conjunto de carateres será devem ser interpretada.

Caráter | Descrição
----------|------------
\ | Uma barra invertida é tooescape utilizado, nenhum dos carateres Olá especificado nesta tabela. É necessário especificar uma barra invertida diretamente antes de caráter especial Olá que deve ser caráter de escape correto.<br/>Por exemplo, Olá sintaxe escapes um asterisco:`\*`
% | Um símbolo de percentagem é utilizado tooindicate URL codificação (por exemplo, `%20`).
* | Um asterisco é um caráter universal que representa um ou mais carateres.
Espaço | Um caráter de espaço indica que uma condição de correspondência pode ser satisfeita por qualquer um dos Olá especificado valores ou padrões.
'value' | Uma aspa simples não têm um significado especial. No entanto, é utilizado um conjunto de plicas tooindicate que um valor deve ser tratado como um valor literal. Podem ser utilizado em Olá seguintes formas:<br><br/>-Permite que um toobe de condição de correspondência satisfeitos sempre que Olá especificado correspondências de valor de qualquer parte do valor de comparação de Olá.  Por exemplo, `'ma'` seria corresponde a nenhum dos Olá cadeias os seguintes: <br/><br/>/Business/**ma**rathon/asset.htm<br/>**Ma**p.gif<br/>empresas/modelo. **ma**p<br /><br />-Permite toobe um caráter especial especificado como um caráter literal. Por exemplo, pode especificar um caráter de espaço literal por envolvente um caráter de espaço dentro de um conjunto de plicas (ou seja, `' '` ou `'sample value'`).<br/>-Permite toobe um valor em branco especificado. Especifique um valor em branco, especificando um conjunto de plicas (ou seja, ').<br /><br/>**Importante:**<br/>-Se Olá especificado o valor não contém um caráter universal, em seguida, este será automaticamente ser considerada um valor literal. Isto significa que não é necessário toospecify um conjunto de plicas.<br/>-Se uma barra invertida não outro como carácter de escape nesta tabela, em seguida, este será ignorado quando especificado dentro de um conjunto de plicas.<br/>-Outra forma toospecify um caráter especial como um caráter literal é tooescape-la utilizando uma barra invertida (ou seja, `\`).

### <a name="regular-expressions"></a>Expressões regulares

As expressões regulares definem um padrão que será procurado dentro de um valor de texto. A notação de expressão regular define significados específico tooa diversas símbolos. Olá seguinte tabela indica os carateres especiais como são tratadas pelo correspondência condições e funcionalidades que suportam expressões regulares.

Caráter especial | Descrição
------------------|------------
\ | Uma barra invertida escapes Olá caráter Olá seguinte. Isto faz com que esse toobe caráter tratado como um valor literal em vez de demorar no significado da expressão regular. Por exemplo, Olá sintaxe escapes um asterisco:`\*`
% | significado Olá de um símbolo de percentagem depende da sua utilização.<br/><br/> `%{HTTPVariable}`: Este sintaxe identifica uma variável HTTP.<br/>`%{HTTPVariable%Pattern}`: Este sintaxe utiliza um tooidentify de símbolo de percentagem um HTTP variável e como um delimitador.<br />`\%`: Escape um símbolo de percentagem permite toobe utilizado como um valor literal ou a codificação do URL tooindicate (por exemplo, `\%20`).
* | Um asterisco permite Olá precedente toobe caráter correspondida zero ou mais vezes. 
Espaço | Um caráter de espaço, normalmente, é tratado como um caráter literal. 
'value' | Plicas são tratadas como literais carateres. Um conjunto de plicas não têm um significado especial.


## <a name="next-steps"></a>Passos seguintes
* [Condições de correspondência do motor de regras](cdn-rules-engine-reference-match-conditions.md)
* [Expressões condicionais de motor de regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Funcionalidades do motor de regras](cdn-rules-engine-reference-features.md)
* [Substituir o comportamento HTTP predefinido utilizando o motor de regras de Olá](cdn-rules-engine.md)
* [Descrição geral da CDN do Azure](cdn-overview.md)
