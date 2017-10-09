---
title: "referência de sintaxe aaaSQLRuleAction no Azure | Microsoft Docs"
description: "Detalhes sobre SQLRuleAction gramática."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a>Sintaxe de SQLRuleAction

A *SqlRuleAction* é uma instância de Olá [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe e representa conjunto de ações escritas em linguagem SQL baseiam sintaxe que é executada em relação a um [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
Este tópico lista os detalhes sobre Olá gramática de ação de regra SQL.  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
```

```
<expression> ::=
    <constant>
    | <function>
    | <property>
    | <expression> { + | - | * | / | % } <expression>
    | { + | - } <expression>
    | ( <expression> )
``` 

```
<property> := 
    [<scope> .] <property_name>
``` 
  
## <a name="arguments"></a>Argumentos  
  
-   `<scope>`é uma cadeia opcional que indica o âmbito Olá Olá `<property_name>`. Os valores válidos são `sys` ou `user`. Olá `sys` valor indica o âmbito do sistema onde `<property_name>` é um nome de propriedade pública de Olá [BrokeredMessage classe](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`indica o âmbito de utilizador onde `<property_name>` é uma chave de Olá [BrokeredMessage classe](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dicionário. `user`o âmbito é o âmbito de predefinição Olá se `<scope>` não está especificado.  
  
### <a name="remarks"></a>Observações  

Uma tentativa de tooaccess uma propriedade inexistente sistema é um erro enquanto uma propriedade de utilizador de tooaccess um inexistente tentativa não é um erro. Em vez disso, uma propriedade inexistente utilizador internamente é avaliada como um valor desconhecido. Um valor desconhecido é tratado especial durante a avaliação de operador.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argumentos  
 `<regular_identifier>`é uma cadeia representada pelo Olá seguintes expressão regular:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 Isto significa que qualquer cadeia que começa com uma letra e é seguida de um ou mais um caráter de sublinhado/letra/dígitos.  
  
 `[:IsLetter:]`significa que qualquer caráter Unicode, que está categorizado como uma letra de Unicode. `System.Char.IsLetter(c)`Devolve `true` se `c` uma letra de Unicode.  
  
 `[:IsDigit:]`significa que qualquer caráter Unicode, que está categorizado como um dígito decimal. `System.Char.IsDigit(c)`Devolve `true` se `c` é um dígito de Unicode.  
  
 A `<regular_identifier>` não pode ser uma palavra-chave reservada.  
  
 `<delimited_identifier>`é qualquer cadeia que está incluída com esquerda/direita Parênteses Retos ([]). Um parêntesis Reto direito é representado como dois direita entre parênteses Retos. Olá seguem-se exemplos de `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 `<quoted_identifier>`é qualquer cadeia que é colocada entre aspas. Uma dupla aspas no identificador é representada como dois aspas. Não é recomendado toouse entre aspas identificadores porque podem facilmente ser confundido com uma constante de cadeia. Utilize um identificador delimitado se possível. Olá segue-se um exemplo de `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>Padrão  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Observações
  
 `<pattern>`tem de ser uma expressão que é avaliada como uma cadeia. É utilizado como um padrão para Olá como operador.      Pode conter os seguintes carateres universais de Olá:  
  
-   `%`: Qualquer cadeia de carateres de zero ou mais.  
  
-   `_`: Um único caráter.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Observações
  
 `<escape_char>`tem de ser uma expressão que é avaliada como uma cadeia de comprimento 1. É utilizado como um caráter de escape para Olá como operador.  
  
 Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde `ABC%` em vez de uma cadeia que começa com `ABC`.  
  
## <a name="constant"></a>constante  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argumentos  
  
-   `<integer_constant>`é uma cadeia de números que não são entre aspas e não contêm decimais. valores de Olá são armazenados como `System.Int64` internamente, e siga Olá mesmo intervalo.  
  
     Olá, são exemplos de constantes de tempo:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>`é uma cadeia de números que não são entre aspas e contenham um ponto decimal. valores de Olá são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.  
  
     Numa versão futura, este número poderá ser armazenado numa dados diferentes tipo toosupport exato número semântica de, pelo que não deverá confiar na Olá facto Olá subjacente o tipo de dados é `System.Double` para `<decimal_constant>`.  
  
     Olá, são exemplos de constantes decimais:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>`é uma número escrita na notação de científica. valores de Olá são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão. Olá, são exemplos de constantes de número aproximados:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Observações
  
As constantes booleanos são representadas por palavras-chave de Olá `TRUE` ou `FALSE`. valores de Olá são armazenados como `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Observações
  
As constantes String estão incluídas entre plicas e incluam quaisquer carateres Unicode válidos. Uma plica incorporada numa constante de cadeia é representada como dois único entre aspas.  
  
## <a name="function"></a>Função  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Observações  

Olá `newid()` função devolve um **GUID** gerados pelo Olá `System.Guid.NewGuid()` método.  
  
Olá `property(name)` função devolve Olá valor da propriedade Olá referenciada pelo `name`. Olá `name` valor pode ser uma expressão válida que devolva um valor de cadeia.  
  
## <a name="considerations"></a>Considerações

- CONJUNTO é utilizado toocreate um novo valor de Olá de propriedade ou atualização de uma propriedade existente.
- REMOVER é utilizado tooremove uma propriedade.
- CONJUNTO efetua a conversão implícita de se for possível quando o tipo de expressão Olá e tipo de propriedade Olá existente são diferentes.
- Ação falha se as propriedades do sistema não existente foram referenciadas.
- Ação não falhar se as propriedades do utilizador inexistente foram referenciadas.
- Uma propriedade inexistente utilizador é avaliada como "Desconhecido" internamente, seguinte Olá mesmo semântica como [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) ao avaliar operadores.

## <a name="next-steps"></a>Passos seguintes

- [Classe de SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [Classe de SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
