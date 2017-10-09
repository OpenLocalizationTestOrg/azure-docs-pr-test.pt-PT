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
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="0cf5d-103">Sintaxe de SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="0cf5d-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="0cf5d-104">A *SqlRuleAction* é uma instância de Olá [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe e representa conjunto de ações escritas em linguagem SQL baseiam sintaxe que é executada em relação a um [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="0cf5d-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="0cf5d-105">Este tópico lista os detalhes sobre Olá gramática de ação de regra SQL.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="0cf5d-106">Argumentos</span><span class="sxs-lookup"><span data-stu-id="0cf5d-106">Arguments</span></span>  
  
-   <span data-ttu-id="0cf5d-107">`<scope>`é uma cadeia opcional que indica o âmbito Olá Olá `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="0cf5d-108">Os valores válidos são `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="0cf5d-109">Olá `sys` valor indica o âmbito do sistema onde `<property_name>` é um nome de propriedade pública de Olá [BrokeredMessage classe](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="0cf5d-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="0cf5d-110">`user`indica o âmbito de utilizador onde `<property_name>` é uma chave de Olá [BrokeredMessage classe](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dicionário.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="0cf5d-111">`user`o âmbito é o âmbito de predefinição Olá se `<scope>` não está especificado.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="0cf5d-112">Observações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-112">Remarks</span></span>  

<span data-ttu-id="0cf5d-113">Uma tentativa de tooaccess uma propriedade inexistente sistema é um erro enquanto uma propriedade de utilizador de tooaccess um inexistente tentativa não é um erro.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="0cf5d-114">Em vez disso, uma propriedade inexistente utilizador internamente é avaliada como um valor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="0cf5d-115">Um valor desconhecido é tratado especial durante a avaliação de operador.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="0cf5d-116">property_name</span><span class="sxs-lookup"><span data-stu-id="0cf5d-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="0cf5d-117">Argumentos</span><span class="sxs-lookup"><span data-stu-id="0cf5d-117">Arguments</span></span>  
 <span data-ttu-id="0cf5d-118">`<regular_identifier>`é uma cadeia representada pelo Olá seguintes expressão regular:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="0cf5d-119">Isto significa que qualquer cadeia que começa com uma letra e é seguida de um ou mais um caráter de sublinhado/letra/dígitos.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="0cf5d-120">`[:IsLetter:]`significa que qualquer caráter Unicode, que está categorizado como uma letra de Unicode.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="0cf5d-121">`System.Char.IsLetter(c)`Devolve `true` se `c` uma letra de Unicode.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="0cf5d-122">`[:IsDigit:]`significa que qualquer caráter Unicode, que está categorizado como um dígito decimal.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="0cf5d-123">`System.Char.IsDigit(c)`Devolve `true` se `c` é um dígito de Unicode.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="0cf5d-124">A `<regular_identifier>` não pode ser uma palavra-chave reservada.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="0cf5d-125">`<delimited_identifier>`é qualquer cadeia que está incluída com esquerda/direita Parênteses Retos ([]).</span><span class="sxs-lookup"><span data-stu-id="0cf5d-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="0cf5d-126">Um parêntesis Reto direito é representado como dois direita entre parênteses Retos.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="0cf5d-127">Olá seguem-se exemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="0cf5d-128">`<quoted_identifier>`é qualquer cadeia que é colocada entre aspas.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="0cf5d-129">Uma dupla aspas no identificador é representada como dois aspas.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="0cf5d-130">Não é recomendado toouse entre aspas identificadores porque podem facilmente ser confundido com uma constante de cadeia.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="0cf5d-131">Utilize um identificador delimitado se possível.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="0cf5d-132">Olá segue-se um exemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="0cf5d-133">Padrão</span><span class="sxs-lookup"><span data-stu-id="0cf5d-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="0cf5d-134">Observações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-134">Remarks</span></span>
  
 <span data-ttu-id="0cf5d-135">`<pattern>`tem de ser uma expressão que é avaliada como uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="0cf5d-136">É utilizado como um padrão para Olá como operador.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="0cf5d-137">Pode conter os seguintes carateres universais de Olá:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="0cf5d-138">`%`: Qualquer cadeia de carateres de zero ou mais.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="0cf5d-139">`_`: Um único caráter.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="0cf5d-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="0cf5d-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="0cf5d-141">Observações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-141">Remarks</span></span>
  
 <span data-ttu-id="0cf5d-142">`<escape_char>`tem de ser uma expressão que é avaliada como uma cadeia de comprimento 1.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="0cf5d-143">É utilizado como um caráter de escape para Olá como operador.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="0cf5d-144">Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde `ABC%` em vez de uma cadeia que começa com `ABC`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="0cf5d-145">constante</span><span class="sxs-lookup"><span data-stu-id="0cf5d-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="0cf5d-146">Argumentos</span><span class="sxs-lookup"><span data-stu-id="0cf5d-146">Arguments</span></span>  
  
-   <span data-ttu-id="0cf5d-147">`<integer_constant>`é uma cadeia de números que não são entre aspas e não contêm decimais.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="0cf5d-148">valores de Olá são armazenados como `System.Int64` internamente, e siga Olá mesmo intervalo.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="0cf5d-149">Olá, são exemplos de constantes de tempo:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="0cf5d-150">`<decimal_constant>`é uma cadeia de números que não são entre aspas e contenham um ponto decimal.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="0cf5d-151">valores de Olá são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="0cf5d-152">Numa versão futura, este número poderá ser armazenado numa dados diferentes tipo toosupport exato número semântica de, pelo que não deverá confiar na Olá facto Olá subjacente o tipo de dados é `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="0cf5d-153">Olá, são exemplos de constantes decimais:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="0cf5d-154">`<approximate_number_constant>`é uma número escrita na notação de científica.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="0cf5d-155">valores de Olá são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="0cf5d-156">Olá, são exemplos de constantes de número aproximados:</span><span class="sxs-lookup"><span data-stu-id="0cf5d-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="0cf5d-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="0cf5d-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="0cf5d-158">Observações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-158">Remarks</span></span>
  
<span data-ttu-id="0cf5d-159">As constantes booleanos são representadas por palavras-chave de Olá `TRUE` ou `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="0cf5d-160">valores de Olá são armazenados como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="0cf5d-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="0cf5d-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="0cf5d-162">Observações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-162">Remarks</span></span>
  
<span data-ttu-id="0cf5d-163">As constantes String estão incluídas entre plicas e incluam quaisquer carateres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="0cf5d-164">Uma plica incorporada numa constante de cadeia é representada como dois único entre aspas.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="0cf5d-165">Função</span><span class="sxs-lookup"><span data-stu-id="0cf5d-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="0cf5d-166">Observações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-166">Remarks</span></span>  

<span data-ttu-id="0cf5d-167">Olá `newid()` função devolve um **GUID** gerados pelo Olá `System.Guid.NewGuid()` método.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="0cf5d-168">Olá `property(name)` função devolve Olá valor da propriedade Olá referenciada pelo `name`.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="0cf5d-169">Olá `name` valor pode ser uma expressão válida que devolva um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="0cf5d-170">Considerações</span><span class="sxs-lookup"><span data-stu-id="0cf5d-170">Considerations</span></span>

- <span data-ttu-id="0cf5d-171">CONJUNTO é utilizado toocreate um novo valor de Olá de propriedade ou atualização de uma propriedade existente.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="0cf5d-172">REMOVER é utilizado tooremove uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="0cf5d-173">CONJUNTO efetua a conversão implícita de se for possível quando o tipo de expressão Olá e tipo de propriedade Olá existente são diferentes.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="0cf5d-174">Ação falha se as propriedades do sistema não existente foram referenciadas.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="0cf5d-175">Ação não falhar se as propriedades do utilizador inexistente foram referenciadas.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="0cf5d-176">Uma propriedade inexistente utilizador é avaliada como "Desconhecido" internamente, seguinte Olá mesmo semântica como [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) ao avaliar operadores.</span><span class="sxs-lookup"><span data-stu-id="0cf5d-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cf5d-177">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0cf5d-177">Next steps</span></span>

- [<span data-ttu-id="0cf5d-178">Classe de SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="0cf5d-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="0cf5d-179">Classe de SQLFilter</span><span class="sxs-lookup"><span data-stu-id="0cf5d-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
