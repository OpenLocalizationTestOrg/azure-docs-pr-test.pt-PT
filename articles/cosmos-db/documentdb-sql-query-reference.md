---
<span data-ttu-id="ac22e-101">Título: aaa "API de DocumentDB do Azure Cosmos DB: Sintaxe SQL | Descrição da Microsoft Docs": referência de documentação para Olá linguagem de consulta de SQL de API do DocumentDB do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ac22e-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="ac22e-102">serviços: cosmos-db autor: Gestor mimig1: jhubbard editor: mimig documentationcenter: '</span><span class="sxs-lookup"><span data-stu-id="ac22e-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="ac22e-103">MS. AssetID: MS. Service: cosmos-db workload: MS. tgt_pltfrm de serviços de dados: na devlang: MS. topic de na: referência MS. Date: 13/06/2017 Author: mimig</span><span class="sxs-lookup"><span data-stu-id="ac22e-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="ac22e-104">DocumentDB do Azure do Cosmos DB API: Referência de sintaxe SQL</span><span class="sxs-lookup"><span data-stu-id="ac22e-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="ac22e-105">Olá API de DocumentDB do Azure Cosmos DB suporta consulta de documentos através de um familiar SQL (Structured Query Language) como gramática através de documentos JSON hierárquicos sem necessidade de um esquema explícito ou criação de índices secundários.</span><span class="sxs-lookup"><span data-stu-id="ac22e-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="ac22e-106">Este tópico fornece documentação de referência para Olá linguagem de consulta de SQL de API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ac22e-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="ac22e-107">Para obter instruções sobre Olá linguagem de consulta de SQL de API do DocumentDB, consulte [as consultas SQL para a API de DocumentDB do Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="ac22e-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="ac22e-108">Também Convidamo-lo toovisit Olá [Query Playground](http://www.documentdb.com/sql/demo) onde pode tentar BD do Cosmos do Azure e executar consultas SQL no nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ac22e-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="ac22e-109">Consulta SELECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-109">SELECT query</span></span>  
<span data-ttu-id="ac22e-110">Obtém os documentos JSON da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="ac22e-111">Suporta a avaliação da expressão, projeções, filtragem e associa.</span><span class="sxs-lookup"><span data-stu-id="ac22e-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="ac22e-112">convenções de Olá utilizadas para descrever instruções SELECT Olá são apresentadas na secção de convenções de sintaxe de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="ac22e-113">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="ac22e-114">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-114">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-115">Consulte as seguintes secções para obter detalhes sobre cada cláusula:</span><span class="sxs-lookup"><span data-stu-id="ac22e-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="ac22e-116">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="ac22e-117">A cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="ac22e-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="ac22e-118">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="ac22e-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="ac22e-119">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="ac22e-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="ac22e-120">cláusulas Olá na instrução SELECT Olá têm de ser ordenadas conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="ac22e-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="ac22e-121">Qualquer uma das cláusulas opcional Olá pode ser omitida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="ac22e-122">Mas, quando são utilizadas cláusulas opcionais, deve aparecer na ordem correta Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="ac22e-123">**Ordem de processamento de mensagens em fila lógico de instrução SELECT Olá**</span><span class="sxs-lookup"><span data-stu-id="ac22e-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="ac22e-124">ordem de Olá na qual são processadas cláusulas é:</span><span class="sxs-lookup"><span data-stu-id="ac22e-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="ac22e-125">A cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="ac22e-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="ac22e-126">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="ac22e-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="ac22e-127">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="ac22e-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="ac22e-128">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="ac22e-129">Tenha em atenção que isto é diferente da ordem de Olá em que aparecem na sintaxe Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="ac22e-130">Olá ordenação é que todos os símbolos novo introduzidos por uma cláusula processada estão visíveis e podem ser utilizados nas cláusulas processadas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ac22e-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="ac22e-131">Por exemplo, aliases declarados numa cláusula FROM estão acessíveis no onde e cláusulas SELECT.</span><span class="sxs-lookup"><span data-stu-id="ac22e-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="ac22e-132">**Os carateres de espaço em branco e comentários**</span><span class="sxs-lookup"><span data-stu-id="ac22e-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="ac22e-133">Todos os carateres de espaço em branco que não façam parte de uma cadeia delimitada por aspas ou entre aspas identificador não fazem parte de gramática de idioma Olá e serão ignorados durante a análise.</span><span class="sxs-lookup"><span data-stu-id="ac22e-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="ac22e-134">suporta o idioma de consulta Olá comentários de estilo de T-SQL, como</span><span class="sxs-lookup"><span data-stu-id="ac22e-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="ac22e-135">Instrução de SQL`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="ac22e-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="ac22e-136">Enquanto carateres de espaço em branco e comentários não têm qualquer significância na gramática Olá, têm de ser utilizados tooseparate tokens.</span><span class="sxs-lookup"><span data-stu-id="ac22e-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="ac22e-137">Por exemplo: `-1e5` é o único tempo token, número`: – 1 e5` é um token minus seguido pelo número de 1 e e5 identificador.</span><span class="sxs-lookup"><span data-stu-id="ac22e-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="ac22e-138"><a name="bk_select_query"></a>Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="ac22e-139">cláusulas Olá na instrução SELECT Olá têm de ser ordenadas conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="ac22e-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="ac22e-140">Qualquer uma das cláusulas opcional Olá pode ser omitida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="ac22e-141">Mas, quando são utilizadas cláusulas opcionais, deve aparecer na ordem correta Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="ac22e-142">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="ac22e-143">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="ac22e-144">Definir propriedades ou valor toobe selecionado para o resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="ac22e-145">Especifica que o valor de Olá deve ser obtido sem efetuar alterações.</span><span class="sxs-lookup"><span data-stu-id="ac22e-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="ac22e-146">Especificamente se valor de Olá processado um objeto, serão possível obter todas as propriedades.</span><span class="sxs-lookup"><span data-stu-id="ac22e-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="ac22e-147">Especifica a lista de Olá de toobe propriedades obtido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="ac22e-148">Cada valor devolvido será um objeto com Olá foram especificadas propriedades.</span><span class="sxs-lookup"><span data-stu-id="ac22e-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="ac22e-149">Especifica que o valor JSON Olá deve ser obtido em vez de um objeto JSON Olá concluído.</span><span class="sxs-lookup"><span data-stu-id="ac22e-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="ac22e-150">Isto, ao contrário `<property_list>` moldam Olá projetado valor um objeto.</span><span class="sxs-lookup"><span data-stu-id="ac22e-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="ac22e-151">Expressão que representa Olá valor toobe calculada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="ac22e-152">Consulte [expressões escalares](#bk_scalar_expressions) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="ac22e-153">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-153">**Remarks**</span></span>  
  
<span data-ttu-id="ac22e-154">Olá `SELECT *` sintaxe só é válida se a cláusula FROM tem declaradas exatamente um alias.</span><span class="sxs-lookup"><span data-stu-id="ac22e-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="ac22e-155">`SELECT *`Fornece uma projeção de identidade, o que pode ser útil se não for necessária nenhuma projecção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="ac22e-156">SELECIONE * só é válido se a cláusula FROM for especificado e apresentados apenas uma única origem de entrada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="ac22e-157">Tenha em atenção que `SELECT <select_list>` e `SELECT *` são "sugar diferenças sintáticas" e podem ser expressas em alternativa, utilizando instruções SELECT simples, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="ac22e-158">é equivalente ao:</span><span class="sxs-lookup"><span data-stu-id="ac22e-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="ac22e-159">é equivalente ao:</span><span class="sxs-lookup"><span data-stu-id="ac22e-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="ac22e-160">**Consulte também**</span><span class="sxs-lookup"><span data-stu-id="ac22e-160">**See Also**</span></span>  
  
[<span data-ttu-id="ac22e-161">Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="ac22e-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="ac22e-162">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="ac22e-163"><a name="bk_from_clause"></a>A cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="ac22e-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="ac22e-164">Especifica a origem Olá ou origens associadas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="ac22e-165">cláusula FROM de Olá é opcional.</span><span class="sxs-lookup"><span data-stu-id="ac22e-165">hello FROM clause is optional.</span></span> <span data-ttu-id="ac22e-166">Se não for especificadas, outras cláusulas ainda serão executadas como se a cláusula FROM fornecido um único documento.</span><span class="sxs-lookup"><span data-stu-id="ac22e-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="ac22e-167">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-167">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="ac22e-168">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="ac22e-169">Especifica uma origem de dados, com ou sem um alias.</span><span class="sxs-lookup"><span data-stu-id="ac22e-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="ac22e-170">Se não for especificado o alias, irá ser inferido a partir Olá `<collection_expression>` utilizando os seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="ac22e-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="ac22e-171">Se a expressão de Olá é um collection_name, collection_name será utilizado como um alias.</span><span class="sxs-lookup"><span data-stu-id="ac22e-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="ac22e-172">Se estiver a expressão de Olá `<collection_expression>`, property_name, em seguida, property_name será utilizado como um alias.</span><span class="sxs-lookup"><span data-stu-id="ac22e-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="ac22e-173">Se a expressão de Olá é um collection_name, collection_name será utilizado como um alias.</span><span class="sxs-lookup"><span data-stu-id="ac22e-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="ac22e-174">TAL COMO`input_alias`</span><span class="sxs-lookup"><span data-stu-id="ac22e-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="ac22e-175">Especifica que Olá `input_alias` é um conjunto de valores obtidos pelo Olá subjacente expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="ac22e-176">`input_alias`EM</span><span class="sxs-lookup"><span data-stu-id="ac22e-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="ac22e-177">Especifica que Olá `input_alias` deve representam o conjunto de Olá de valores obtidos pelo iterating através de todos os elementos de matriz de cada matriz devolvida pelo Olá subjacente expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="ac22e-178">Qualquer valor devolvido pela expressão de coleção subjacente que não é uma matriz é ignorada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="ac22e-179">Especifica Olá coleção expressão toobe utilizada documentos de Olá tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="ac22e-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="ac22e-180">Especifica que esse documento deve ser obtido a partir da predefinição de Olá, coleção atualmente ligada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="ac22e-181">Especifica que esse documento deve ser obtido da coleção de Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="ac22e-182">nome de Olá da coleção de Olá deve corresponder ao nome de Olá da coleção de Olá atualmente ligada ao.</span><span class="sxs-lookup"><span data-stu-id="ac22e-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="ac22e-183">Especifica esse documento deve ser obtido a partir de Olá outra origem definida pelo alias Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="ac22e-184">Especifica esse documento deve ser obtido acedendo Olá `property_name` elemento de matriz de propriedade ou array_index para todos os documentos obtidos pelo especificada a expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="ac22e-185">Especifica esse documento deve ser obtido acedendo Olá `property_name` elemento de matriz de propriedade ou array_index para todos os documentos obtidos pelo especificada a expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="ac22e-186">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-186">**Remarks**</span></span>  
  
<span data-ttu-id="ac22e-187">Todos os aliases fornecido ou inferir na Olá `<from_source>(`s) têm de ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="ac22e-188">Olá sintaxe `<collection_expression>.`property_name é Olá igual `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="ac22e-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="ac22e-189">No entanto, a sintaxe de última Olá pode ser utilizado se um nome de propriedade contém um identificador não carateres.</span><span class="sxs-lookup"><span data-stu-id="ac22e-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="ac22e-190">**Falta de propriedades em falta elementos de matriz não definida valores processamento**</span><span class="sxs-lookup"><span data-stu-id="ac22e-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="ac22e-191">Se uma expressão de coleção acede propriedades ou elementos de matriz e que não existe valor, esse valor será ignorado e não continuar a processar.</span><span class="sxs-lookup"><span data-stu-id="ac22e-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="ac22e-192">**Âmbito de contexto de expressão de coleção**</span><span class="sxs-lookup"><span data-stu-id="ac22e-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="ac22e-193">Uma expressão de coleção pode ser confinados por coleção ou no âmbito do documento:</span><span class="sxs-lookup"><span data-stu-id="ac22e-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="ac22e-194">Uma expressão de âmbito de coleção, se hello origem subjacente da expressão de coleção de Olá é a raiz ou `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="ac22e-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="ac22e-195">Este tipo uma expressão representa um conjunto de documentos obtidos da coleção de Olá diretamente e não está dependente de processamento de Olá de outras expressões de coleção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="ac22e-196">Uma expressão no âmbito do documento, se hello origem subjacente da expressão de coleção de Olá é `input_alias` introduzidas anteriormente na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="ac22e-197">Este tipo uma expressão representa um conjunto de documentos obtido através da avaliação de expressão de coleção de Olá no âmbito de Olá de cada documento que pertence o conjunto de toohello associado à coleção de um alias de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="ac22e-198">conjunto resultante Olá será uma União de conjuntos obtido através da avaliação de coleção de Olá expressão para cada um dos documentos Olá Olá subjacente conjunto.</span><span class="sxs-lookup"><span data-stu-id="ac22e-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="ac22e-199">**Associações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-199">**Joins**</span></span>  
  
<span data-ttu-id="ac22e-200">Na versão atual do Olá, Azure Cosmos DB suporta associações internas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="ac22e-201">Capacidades de associação adicionais são lançamento.</span><span class="sxs-lookup"><span data-stu-id="ac22e-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="ac22e-202">Resultado de associações internas num produto cruzado completado de Olá define participar na União Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="ac22e-203">resultado Olá uma associação de forma de N é um conjunto de cadeias de identificação de elemento N, onde cada valor na cadeia de identificação de Olá está associado a alias de Olá definir participar na União Olá e pode ser acedido por referenciar esse alias nas outras cláusulas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="ac22e-204">avaliação Olá de associação de Olá depende do âmbito do contexto Olá de Olá define a participar:</span><span class="sxs-lookup"><span data-stu-id="ac22e-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="ac22e-205">Uma associação entre um conjunto de coleções e âmbito de coleção de conjunto B, os resultados num produto cruzado de todos os elementos em conjuntos de A e B.</span><span class="sxs-lookup"><span data-stu-id="ac22e-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="ac22e-206">Uma associação entre o conjunto A e conjunto no âmbito do documento B, resulta numa união de todos os conjuntos de obtido através da avaliação no âmbito do documento conjunto B para cada documento de definir A.</span><span class="sxs-lookup"><span data-stu-id="ac22e-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="ac22e-207">Na versão atual do Olá, um máximo de uma expressão de âmbito de coleção é suportado pelo processador de consultas Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="ac22e-208">**Exemplos de associações:**</span><span class="sxs-lookup"><span data-stu-id="ac22e-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="ac22e-209">Vamos ver Olá a cláusula FROM a seguir:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="ac22e-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="ac22e-210">Permitir que cada origem definir `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="ac22e-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="ac22e-211">Esta cláusula FROM devolve um conjunto de cadeias de identificação de N (cadeia de identificação com valores N).</span><span class="sxs-lookup"><span data-stu-id="ac22e-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="ac22e-212">Cada cadeia de identificação tem valores produzidos pelo iterating todos os aliases de coleção ao longo do respetivos respetivos conjuntos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="ac22e-213">*Exemplo 1, com 2 origens de associação:*</span><span class="sxs-lookup"><span data-stu-id="ac22e-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="ac22e-214">Permitir que `<from_source1>` ser coleção no âmbito e representam conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="ac22e-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ac22e-215">Permitir que `<from_source2>` ser confinada documento referenciar input_alias1 e conjuntos de representar:</span><span class="sxs-lookup"><span data-stu-id="ac22e-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="ac22e-216">{1, 2} para`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="ac22e-217">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="ac22e-218">{4, 5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="ac22e-219">Olá a cláusula FROM `<from_source1> JOIN <from_source2>` resultará na Olá seguinte identificação:</span><span class="sxs-lookup"><span data-stu-id="ac22e-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="ac22e-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="ac22e-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="ac22e-221">*Exemplo 2, com 3 origens de associação:*</span><span class="sxs-lookup"><span data-stu-id="ac22e-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="ac22e-222">Permitir que `<from_source1>` ser coleção no âmbito e representam conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="ac22e-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ac22e-223">Permitir que `<from_source2>` estar no âmbito do documento referenciar `input_alias1` e conjuntos de representar:</span><span class="sxs-lookup"><span data-stu-id="ac22e-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="ac22e-224">{1, 2} para`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="ac22e-225">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="ac22e-226">{4, 5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="ac22e-227">Permitir que `<from_source3>` estar no âmbito do documento referenciar `input_alias2` e conjuntos de representar:</span><span class="sxs-lookup"><span data-stu-id="ac22e-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="ac22e-228">{100, 200} para`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="ac22e-229">{300} para`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="ac22e-230">Olá a cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará na Olá seguinte identificação:</span><span class="sxs-lookup"><span data-stu-id="ac22e-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="ac22e-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="ac22e-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="ac22e-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="ac22e-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ac22e-233">Falta de cadeias de identificação para outros valores de `input_alias1`, `input_alias2`, para que Olá `<from_source3>` não devolveu quaisquer valores.</span><span class="sxs-lookup"><span data-stu-id="ac22e-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="ac22e-234">*ASSOCIE exemplo 3, com 3 origens:*</span><span class="sxs-lookup"><span data-stu-id="ac22e-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="ac22e-235">Permita < from_source1 > ser confinada de coleção e representam conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="ac22e-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ac22e-236">Permitir que `<from_source1>` ser coleção no âmbito e representam conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="ac22e-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ac22e-237">Permitem < from_source2 > ser input_alias1 de referência no âmbito do documento e conjuntos de representar:</span><span class="sxs-lookup"><span data-stu-id="ac22e-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="ac22e-238">{1, 2} para`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="ac22e-239">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="ac22e-240">{4, 5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="ac22e-241">Permitir que `<from_source3>` ser confinada demasiado`input_alias1` e conjuntos de representar:</span><span class="sxs-lookup"><span data-stu-id="ac22e-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="ac22e-242">{100, 200} para`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="ac22e-243">{300} para`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="ac22e-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="ac22e-244">Olá a cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará na Olá seguinte identificação:</span><span class="sxs-lookup"><span data-stu-id="ac22e-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="ac22e-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="ac22e-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="ac22e-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="ac22e-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ac22e-247">Isto resultou num produto cruzado entre `<from_source2>` e `<from_source3>` porque ambos estão confinada toohello mesmo `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="ac22e-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="ac22e-248">Isto resultou numa 4 (2 x 2) cadeias de identificação que tenham o valor A, cadeias de identificação 0 ter o valor B (1, 0) e (2 x 1) de 2 cadeias de identificação ter valor C.</span><span class="sxs-lookup"><span data-stu-id="ac22e-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="ac22e-249">**Consulte também**</span><span class="sxs-lookup"><span data-stu-id="ac22e-249">**See also**</span></span>  
  
 [<span data-ttu-id="ac22e-250">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="ac22e-251"><a name="bk_where_clause"></a>Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="ac22e-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="ac22e-252">Especifica a condição de pesquisa de Olá para documentos Olá devolvidos pela consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="ac22e-253">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="ac22e-254">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="ac22e-255">Especifica Olá condição toobe cumprido Olá documentos toobe devolvido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="ac22e-256">Expressão que representa Olá valor toobe calculada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="ac22e-257">Consulte Olá [expressões escalares](#bk_scalar_expressions) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="ac22e-258">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-258">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-259">Para que Olá documento toobe devolveu uma expressão especificada como condição de filtro tem de avaliar tootrue.</span><span class="sxs-lookup"><span data-stu-id="ac22e-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="ac22e-260">Apenas true valor booleano satisfaçam a condição de Olá, qualquer outro valor: indefinido, null, false, número, matriz nem um objeto não satisfaçam a condição de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="ac22e-261"><a name="bk_orderby_clause"></a>Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="ac22e-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="ac22e-262">Especifica Olá para que os resultados devolvidos pela consulta Olá a ordenação.</span><span class="sxs-lookup"><span data-stu-id="ac22e-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="ac22e-263">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="ac22e-264">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="ac22e-265">Especifica uma propriedade ou expressão em que o resultado da consulta toosort Olá definido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="ac22e-266">Uma coluna de ordenação pode ser especificada como um alias de nome ou coluna.</span><span class="sxs-lookup"><span data-stu-id="ac22e-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="ac22e-267">Podem ser especificadas várias colunas de ordenação.</span><span class="sxs-lookup"><span data-stu-id="ac22e-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="ac22e-268">Os nomes de coluna tem de ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-268">Column names must be unique.</span></span> <span data-ttu-id="ac22e-269">sequência de Olá de colunas de ordenação Olá na cláusula ORDER BY Olá define organização Olá do conjunto de resultados de Olá ordenado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="ac22e-270">Ou seja, o conjunto de resultados de Olá está ordenado por propriedade primeiro Olá e, em seguida, essa lista ordenada está ordenada por propriedade segundo Olá e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="ac22e-271">os nomes de coluna de Olá referenciados na cláusula ORDER BY Olá têm de corresponder tooeither uma coluna na Olá selecionar a coluna de lista ou tooa definida numa tabela especificada na cláusula FROM de Olá sem qualquer ambiguities.</span><span class="sxs-lookup"><span data-stu-id="ac22e-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="ac22e-272">Especifica uma propriedade de único ou uma expressão que conjunto de resultados de consulta de Olá toosort.</span><span class="sxs-lookup"><span data-stu-id="ac22e-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="ac22e-273">Consulte Olá [expressões escalares](#bk_scalar_expressions) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="ac22e-274">Especifica que devem ser ordenados Olá valores existentes na coluna especificada Olá na ordem ascendente ou descendente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="ac22e-275">Ordena ASC de Olá menor valor toohighest valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="ac22e-276">Ordena DESC do valor de toolowest do valor mais alto.</span><span class="sxs-lookup"><span data-stu-id="ac22e-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="ac22e-277">ASC é uma sequência de ordenação Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-277">ASC is hello default sort order.</span></span> <span data-ttu-id="ac22e-278">Valores nulos são tratados como Olá mais baixos possíveis valores.</span><span class="sxs-lookup"><span data-stu-id="ac22e-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="ac22e-279">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-279">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-280">Enquanto a gramática de consulta Olá suporta vários ordem pelas propriedades, o tempo de execução de consulta de base de dados do Azure Cosmos de Olá suporta a ordenação apenas em relação a uma única propriedade e apenas com os nomes de propriedades, ou seja, não contra propriedades calculadas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="ac22e-281">A ordenação também requer que Olá política de indexação inclui um índice de intervalo para a propriedade de Olá e Olá especificado tipo, com precisão máxima Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="ac22e-282">Consulte a documentação para obter mais detalhes da política de indexação de toohello.</span><span class="sxs-lookup"><span data-stu-id="ac22e-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="ac22e-283"><a name="bk_scalar_expressions"></a>Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="ac22e-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="ac22e-284">Uma expressão escalar é uma combinação de símbolos e operadores que podem ser avaliadas tooobtain um valor único.</span><span class="sxs-lookup"><span data-stu-id="ac22e-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="ac22e-285">Expressões simples podem ser constantes, referências de propriedade, referências de elemento de matriz, referências de alias ou chamadas de função.</span><span class="sxs-lookup"><span data-stu-id="ac22e-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="ac22e-286">As expressões simples podem ser combinadas nas expressões complexas utilizando operadores.</span><span class="sxs-lookup"><span data-stu-id="ac22e-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="ac22e-287">Para obter detalhes sobre qual expressão escalar poderá ter de valores, consulte [constantes](#bk_constants) secção.</span><span class="sxs-lookup"><span data-stu-id="ac22e-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="ac22e-288">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-288">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="ac22e-289">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="ac22e-290">Representa um valor constante.</span><span class="sxs-lookup"><span data-stu-id="ac22e-290">Represents a constant value.</span></span> <span data-ttu-id="ac22e-291">Consulte [constantes](#bk_constants) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="ac22e-292">Representa um valor definido pelo Olá `input_alias` introduzida no Olá `FROM` cláusula.</span><span class="sxs-lookup"><span data-stu-id="ac22e-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="ac22e-293">Este valor é garantido toonot ser **indefinido** –**indefinido** valores de entrada Olá são ignorados.</span><span class="sxs-lookup"><span data-stu-id="ac22e-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="ac22e-294">Representa um valor da propriedade Olá um objeto.</span><span class="sxs-lookup"><span data-stu-id="ac22e-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="ac22e-295">Se não existe propriedade Olá ou propriedade é referenciada num valor que não é um objeto, em seguida, expressão Olá avalia demasiado**indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="ac22e-296">Representa um valor de propriedade de Olá com o nome `property_name` ou elemento com índice de matriz `array_index` de uma objeto/matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="ac22e-297">Se o índice de matriz/propriedade Olá não existe ou o índice de matriz/propriedade Olá é referenciado num valor que não é uma objeto/matriz, em seguida, Olá expressão é avaliada tooundefined valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="ac22e-298">Representa um operador que é aplicado tooa único valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="ac22e-299">Consulte [operadores](#bk_operators) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="ac22e-300">Representa um operador que é aplicado tootwo valores.</span><span class="sxs-lookup"><span data-stu-id="ac22e-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="ac22e-301">Consulte [operadores](#bk_operators) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="ac22e-302">Representa um valor definido por um resultado de uma chamada de função.</span><span class="sxs-lookup"><span data-stu-id="ac22e-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="ac22e-303">Nome de utilizador de Olá definido função escalar.</span><span class="sxs-lookup"><span data-stu-id="ac22e-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="ac22e-304">Nome da função de escalar incorporada Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="ac22e-305">Representa um valor obtido através da criação de um novo objeto com propriedades especificadas e os respetivos valores.</span><span class="sxs-lookup"><span data-stu-id="ac22e-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="ac22e-306">Representa um valor obtido através da criação de uma matriz de novo com valores especificados como elementos</span><span class="sxs-lookup"><span data-stu-id="ac22e-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="ac22e-307">Representa um valor de nome de parâmetro especificado do Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="ac22e-308">Os nomes dos parâmetros têm de ter um único @ como caráter de primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="ac22e-309">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-309">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-310">Quando chamar um utilizador ou incorporados definida uma função escalar todos os argumentos tem de ser definidos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="ac22e-311">Se qualquer um dos argumentos de Olá não for definido, não será possível chamar a função de Olá e resultado Olá serão indefinido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="ac22e-312">Ao criar um objeto, qualquer propriedade que é atribuída o valor indefinido será ignorada e não incluída no Olá criada objeto.</span><span class="sxs-lookup"><span data-stu-id="ac22e-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="ac22e-313">Quando a criação de uma matriz, qualquer valor de elemento que é atribuído **indefinido** valor será ignorado e não incluído no objeto de Olá criado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="ac22e-314">Isto fará com que Olá definido seguinte elemento tootake seu lugar de forma a que matriz Olá criado será não ter foi ignorada índices.</span><span class="sxs-lookup"><span data-stu-id="ac22e-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="ac22e-315"><a name="bk_operators"></a>Operadores</span><span class="sxs-lookup"><span data-stu-id="ac22e-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="ac22e-316">Esta secção descreve os operadores de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-316">This section describes hello supported operators.</span></span> <span data-ttu-id="ac22e-317">Cada operador pode ser atribuído tooexactly uma categoria.</span><span class="sxs-lookup"><span data-stu-id="ac22e-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="ac22e-318">Consulte **categorias de operador** tabela abaixo, para obter detalhes sobre o processamento de **indefinido** valores, requisitos de tipo para os valores de entrada e de processamento de valores com os tipos não correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="ac22e-319">**Categorias de operador:**</span><span class="sxs-lookup"><span data-stu-id="ac22e-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="ac22e-320">**Categoria**</span><span class="sxs-lookup"><span data-stu-id="ac22e-320">**Category**</span></span>|<span data-ttu-id="ac22e-321">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="ac22e-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="ac22e-322">**aritmética**</span><span class="sxs-lookup"><span data-stu-id="ac22e-322">**arithmetic**</span></span>|<span data-ttu-id="ac22e-323">Operador espera input(s) toobe Number(s).</span><span class="sxs-lookup"><span data-stu-id="ac22e-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="ac22e-324">Saída também é um número.</span><span class="sxs-lookup"><span data-stu-id="ac22e-324">Output is also a Number.</span></span> <span data-ttu-id="ac22e-325">Se qualquer uma das entradas de Olá **indefinido** ou um tipo diferente de resultado de número, em seguida, Olá **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="ac22e-326">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="ac22e-326">**bitwise**</span></span>|<span data-ttu-id="ac22e-327">Operador espera input(s) inteiro com sinal de 32 bits toobe Number(s).</span><span class="sxs-lookup"><span data-stu-id="ac22e-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="ac22e-328">O resultado é também o número inteiro com sinal de 32 bits número.</span><span class="sxs-lookup"><span data-stu-id="ac22e-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="ac22e-329">Qualquer valor de não-inteiros será arredondado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="ac22e-330">Um valor positivo será arredondado para baixo, negativa valores arredondar por excesso.</span><span class="sxs-lookup"><span data-stu-id="ac22e-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="ac22e-331">Qualquer valor que está fora do intervalo de número inteiro de 32 bits Olá será convertido, efetuando os últimos 32 bits da respetivo dois notação complemento.</span><span class="sxs-lookup"><span data-stu-id="ac22e-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="ac22e-332">Se qualquer uma das entradas de Olá **indefinido** ou escreva outro número, em seguida, o resultado de Olá é **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="ac22e-333">**Nota:** Olá acima comportamento é compatível com o comportamento de operador bit a bit JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ac22e-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="ac22e-334">**lógica**</span><span class="sxs-lookup"><span data-stu-id="ac22e-334">**logical**</span></span>|<span data-ttu-id="ac22e-335">Operador espera input(s) toobe Boolean(s).</span><span class="sxs-lookup"><span data-stu-id="ac22e-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="ac22e-336">Saída também é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="ac22e-337">Se qualquer uma das entradas de Olá **indefinido** ou escreva exceto Boolean, em seguida, o resultado de Olá será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="ac22e-338">**comparação**</span><span class="sxs-lookup"><span data-stu-id="ac22e-338">**comparison**</span></span>|<span data-ttu-id="ac22e-339">Operador espera input(s) toohave Olá mesmo tipo e não pode ser definido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="ac22e-340">O resultado é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="ac22e-341">Se qualquer uma das entradas de Olá **indefinido** ou entradas de Olá têm tipos diferentes, em seguida, resultado Olá é **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="ac22e-342">Consulte **ordenação dos valores de comparação** tabela para o valor de ordenação detalhes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="ac22e-343">**cadeia**</span><span class="sxs-lookup"><span data-stu-id="ac22e-343">**string**</span></span>|<span data-ttu-id="ac22e-344">Operador espera input(s) toobe cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="ac22e-345">Saída também é uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-345">Output is also a String.</span></span><br /><span data-ttu-id="ac22e-346">Se qualquer uma das entradas de Olá **indefinido** ou um tipo diferente de resultado de cadeia, em seguida, Olá **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="ac22e-347">**Operadores unários:**</span><span class="sxs-lookup"><span data-stu-id="ac22e-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="ac22e-348">**Nome**</span><span class="sxs-lookup"><span data-stu-id="ac22e-348">**Name**</span></span>|<span data-ttu-id="ac22e-349">**Operador**</span><span class="sxs-lookup"><span data-stu-id="ac22e-349">**Operator**</span></span>|<span data-ttu-id="ac22e-350">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="ac22e-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="ac22e-351">**aritmética**</span><span class="sxs-lookup"><span data-stu-id="ac22e-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="ac22e-352">Devolve Olá valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="ac22e-353">Negação bit a bit.</span><span class="sxs-lookup"><span data-stu-id="ac22e-353">Bitwise negation.</span></span> <span data-ttu-id="ac22e-354">Devolve negated valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="ac22e-355">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="ac22e-355">**bitwise**</span></span>|~|<span data-ttu-id="ac22e-356">Daqueles complemento.</span><span class="sxs-lookup"><span data-stu-id="ac22e-356">Ones' complement.</span></span> <span data-ttu-id="ac22e-357">Devolve um conjunto de um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="ac22e-358">**Lógica**</span><span class="sxs-lookup"><span data-stu-id="ac22e-358">**Logical**</span></span>|<span data-ttu-id="ac22e-359">**NÃO**</span><span class="sxs-lookup"><span data-stu-id="ac22e-359">**NOT**</span></span>|<span data-ttu-id="ac22e-360">Negação.</span><span class="sxs-lookup"><span data-stu-id="ac22e-360">Negation.</span></span> <span data-ttu-id="ac22e-361">Devolve negated valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="ac22e-362">**Operadores binários:**</span><span class="sxs-lookup"><span data-stu-id="ac22e-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="ac22e-363">**Nome**</span><span class="sxs-lookup"><span data-stu-id="ac22e-363">**Name**</span></span>|<span data-ttu-id="ac22e-364">**Operador**</span><span class="sxs-lookup"><span data-stu-id="ac22e-364">**Operator**</span></span>|<span data-ttu-id="ac22e-365">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="ac22e-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="ac22e-366">**aritmética**</span><span class="sxs-lookup"><span data-stu-id="ac22e-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="ac22e-367">Adição.</span><span class="sxs-lookup"><span data-stu-id="ac22e-367">Addition.</span></span><br /><br /> <span data-ttu-id="ac22e-368">Subtração.</span><span class="sxs-lookup"><span data-stu-id="ac22e-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="ac22e-369">Multiplicação.</span><span class="sxs-lookup"><span data-stu-id="ac22e-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="ac22e-370">Divisão.</span><span class="sxs-lookup"><span data-stu-id="ac22e-370">Division.</span></span><br /><br /> <span data-ttu-id="ac22e-371">Reforçada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-371">Modulation.</span></span>|  
|<span data-ttu-id="ac22e-372">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="ac22e-372">**bitwise**</span></span>|<span data-ttu-id="ac22e-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="ac22e-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="ac22e-374">Bit a bit OR.</span><span class="sxs-lookup"><span data-stu-id="ac22e-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="ac22e-375">Bit a bit AND.</span><span class="sxs-lookup"><span data-stu-id="ac22e-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="ac22e-376">Operação XOR.</span><span class="sxs-lookup"><span data-stu-id="ac22e-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="ac22e-377">Shift esquerdo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="ac22e-378">Shift à direita.</span><span class="sxs-lookup"><span data-stu-id="ac22e-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="ac22e-379">Shift à direita do preenchimento de zero.</span><span class="sxs-lookup"><span data-stu-id="ac22e-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="ac22e-380">**lógica**</span><span class="sxs-lookup"><span data-stu-id="ac22e-380">**logical**</span></span>|<span data-ttu-id="ac22e-381">**E**</span><span class="sxs-lookup"><span data-stu-id="ac22e-381">**AND**</span></span><br /><br /> <span data-ttu-id="ac22e-382">**OU**</span><span class="sxs-lookup"><span data-stu-id="ac22e-382">**OR**</span></span>|<span data-ttu-id="ac22e-383">Conjunção lógica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-383">Logical conjunction.</span></span> <span data-ttu-id="ac22e-384">Devolve **verdadeiro** se ambos os argumentos forem **verdadeiro**, devolve **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-385">Conjunção lógica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-385">Logical conjunction.</span></span> <span data-ttu-id="ac22e-386">Devolve **verdadeiro** se ambos os argumentos forem **verdadeiro**, devolve **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="ac22e-387">**comparação**</span><span class="sxs-lookup"><span data-stu-id="ac22e-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="ac22e-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="ac22e-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="ac22e-389">**??**</span><span class="sxs-lookup"><span data-stu-id="ac22e-389">**??**</span></span>|<span data-ttu-id="ac22e-390">Igual a.</span><span class="sxs-lookup"><span data-stu-id="ac22e-390">Equals.</span></span> <span data-ttu-id="ac22e-391">Devolve **verdadeiro** se argumentos são iguais, devolve **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-392">Não é igual a.</span><span class="sxs-lookup"><span data-stu-id="ac22e-392">Not equal to.</span></span> <span data-ttu-id="ac22e-393">Devolve **verdadeiro** se argumentos não são iguais, devolve **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-394">Maior.</span><span class="sxs-lookup"><span data-stu-id="ac22e-394">Greater Than.</span></span> <span data-ttu-id="ac22e-395">Devolve **verdadeiro** se o primeiro argumento é maior do que o Olá segunda, devolver **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-396">Maior ou igual a.</span><span class="sxs-lookup"><span data-stu-id="ac22e-396">Greater Than or Equal To.</span></span> <span data-ttu-id="ac22e-397">Devolve **verdadeiro** se o primeiro argumento for maior ou igual a segunda toohello, devolver **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-398">Menor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-398">Less Than.</span></span> <span data-ttu-id="ac22e-399">Devolve **verdadeiro** se o primeiro argumento é inferior ao hello segunda, devolver **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-400">Menor ou igual a.</span><span class="sxs-lookup"><span data-stu-id="ac22e-400">Less Than or Equal To.</span></span> <span data-ttu-id="ac22e-401">Devolve **verdadeiro** se o primeiro argumento é menor ou igual toohello segundo um, retorno **falso** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ac22e-402">Unir.</span><span class="sxs-lookup"><span data-stu-id="ac22e-402">Coalesce.</span></span> <span data-ttu-id="ac22e-403">Devolve Olá segundo argumento se Olá primeiro argumento é uma **indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="ac22e-404">**Cadeia**</span><span class="sxs-lookup"><span data-stu-id="ac22e-404">**String**</span></span>|<span data-ttu-id="ac22e-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="ac22e-405">**&#124;&#124;**</span></span>|<span data-ttu-id="ac22e-406">Concatenação.</span><span class="sxs-lookup"><span data-stu-id="ac22e-406">Concatenation.</span></span> <span data-ttu-id="ac22e-407">Devolve uma concatenação de ambos os argumentos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="ac22e-408">**Operadores ternary:**</span><span class="sxs-lookup"><span data-stu-id="ac22e-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="ac22e-409">Operador ternary</span><span class="sxs-lookup"><span data-stu-id="ac22e-409">Ternary operator</span></span>|<span data-ttu-id="ac22e-410">?</span><span class="sxs-lookup"><span data-stu-id="ac22e-410">?</span></span>|<span data-ttu-id="ac22e-411">Devolve Olá segundo argumento, se o primeiro argumento de Olá avalia demasiado**verdadeiro**; devolver o argumento da terceira Olá caso contrário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="ac22e-412">**Ordenação de valores de comparação**</span><span class="sxs-lookup"><span data-stu-id="ac22e-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="ac22e-413">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="ac22e-413">**Type**</span></span>|<span data-ttu-id="ac22e-414">**Ordem de valores**</span><span class="sxs-lookup"><span data-stu-id="ac22e-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="ac22e-415">**Indefinido**</span><span class="sxs-lookup"><span data-stu-id="ac22e-415">**Undefined**</span></span>|<span data-ttu-id="ac22e-416">Não é comparável.</span><span class="sxs-lookup"><span data-stu-id="ac22e-416">Not comparable.</span></span>|  
|<span data-ttu-id="ac22e-417">**Valor nulo**</span><span class="sxs-lookup"><span data-stu-id="ac22e-417">**Null**</span></span>|<span data-ttu-id="ac22e-418">Único valor: **nulo**</span><span class="sxs-lookup"><span data-stu-id="ac22e-418">Single value: **null**</span></span>|  
|<span data-ttu-id="ac22e-419">**Número**</span><span class="sxs-lookup"><span data-stu-id="ac22e-419">**Number**</span></span>|<span data-ttu-id="ac22e-420">Número de real natural.</span><span class="sxs-lookup"><span data-stu-id="ac22e-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="ac22e-421">Valor de infinito negativo é menor do que qualquer outro valor de número.</span><span class="sxs-lookup"><span data-stu-id="ac22e-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="ac22e-422">Valor de infinito positivo é maior do que qualquer outro valor de número. **NaN** valor não é comparável.</span><span class="sxs-lookup"><span data-stu-id="ac22e-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="ac22e-423">Comparar com **NaN** resultará na **indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="ac22e-424">**Cadeia**</span><span class="sxs-lookup"><span data-stu-id="ac22e-424">**String**</span></span>|<span data-ttu-id="ac22e-425">Lexicographical ordem.</span><span class="sxs-lookup"><span data-stu-id="ac22e-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="ac22e-426">**Matriz**</span><span class="sxs-lookup"><span data-stu-id="ac22e-426">**Array**</span></span>|<span data-ttu-id="ac22e-427">Não existem ordenação, mas equitable.</span><span class="sxs-lookup"><span data-stu-id="ac22e-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="ac22e-428">**Objeto**</span><span class="sxs-lookup"><span data-stu-id="ac22e-428">**Object**</span></span>|<span data-ttu-id="ac22e-429">Não existem ordenação, mas equitable.</span><span class="sxs-lookup"><span data-stu-id="ac22e-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="ac22e-430">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-430">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-431">Na base de dados do Azure Cosmos, tipos de Olá de valores, muitas vezes, não são conhecidos até que, na verdade, são obtidos a partir da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="ac22e-432">Na ordem toosupport eficiente a execução do consultas, a maioria operadores Olá tem requisitos do tipo restrito.</span><span class="sxs-lookup"><span data-stu-id="ac22e-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="ac22e-433">Também operadores por si mesmos não efetuar conversões implícitas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="ac22e-434">Isto significa que, como uma consulta: SELECIONAR * da raiz r onde r.Age = 21 só irá devolver documentos com o número de toohello igual de idade 21 de propriedade.</span><span class="sxs-lookup"><span data-stu-id="ac22e-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="ac22e-435">Documentos com a cadeia de toohello igual de antiguidade de propriedade "21" ou uma cadeia de Olá "0021" não irão corresponder à, como expressão Olá "21" = 21 avalia tooundefined.</span><span class="sxs-lookup"><span data-stu-id="ac22e-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="ac22e-436">Isto permite uma melhor utilização dos índices, porque pesquisa Olá de um valor específico (ou seja, número de 21) é mais rápida do que procurar um número indefinido de potenciais correspondências (ou seja, o número 21 ou cadeias "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="ac22e-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="ac22e-437">Isto é diferente do modo como o JavaScript avalia operadores nos valores de diferentes tipos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="ac22e-438">**Comparação de igualdade de objetos e as matrizes e**</span><span class="sxs-lookup"><span data-stu-id="ac22e-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="ac22e-439">Comparação dos valores de matriz nem um objeto utilizando operadores de intervalo (>, > =, <, < =) irá resultar no não definida como há não definida no objeto ou a matriz de valores de ordem.</span><span class="sxs-lookup"><span data-stu-id="ac22e-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="ac22e-440">No entanto, utilizar os operadores de igualdade/inequality (=,! = <>) é suportada e valores serão comparados estruturalmente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="ac22e-441">As matrizes são iguais se ambas as matrizes têm o mesmo número de elementos e os elementos das posições de correspondência também são iguais.</span><span class="sxs-lookup"><span data-stu-id="ac22e-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="ac22e-442">Se comparar qualquer par de elementos resulta em indefinido, Olá resultado de comparação de matriz não está definida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="ac22e-443">Os objetos são iguais se ambos os objetos têm propriedades mesmas definidas e valores de propriedades de correspondência também são iguais.</span><span class="sxs-lookup"><span data-stu-id="ac22e-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="ac22e-444">Se comparar qualquer par de valores de propriedade resulta em indefinido, Olá resultado de comparação de objeto não está definida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="ac22e-445"><a name="bk_constants"></a>Constantes</span><span class="sxs-lookup"><span data-stu-id="ac22e-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="ac22e-446">Uma constante, também conhecido como um literal ou um valor escalar, é um símbolo que representa um valor de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="ac22e-447">formato de Olá de uma constante depende do tipo de dados de Olá do valor de Olá representa.</span><span class="sxs-lookup"><span data-stu-id="ac22e-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="ac22e-448">**Tipos de dados escalar suportados:**</span><span class="sxs-lookup"><span data-stu-id="ac22e-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="ac22e-449">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="ac22e-449">**Type**</span></span>|<span data-ttu-id="ac22e-450">**Ordem de valores**</span><span class="sxs-lookup"><span data-stu-id="ac22e-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="ac22e-451">**Indefinido**</span><span class="sxs-lookup"><span data-stu-id="ac22e-451">**Undefined**</span></span>|<span data-ttu-id="ac22e-452">Único valor: **indefinido**</span><span class="sxs-lookup"><span data-stu-id="ac22e-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="ac22e-453">**Valor nulo**</span><span class="sxs-lookup"><span data-stu-id="ac22e-453">**Null**</span></span>|<span data-ttu-id="ac22e-454">Único valor: **nulo**</span><span class="sxs-lookup"><span data-stu-id="ac22e-454">Single value: **null**</span></span>|  
|<span data-ttu-id="ac22e-455">**Valor booleano**</span><span class="sxs-lookup"><span data-stu-id="ac22e-455">**Boolean**</span></span>|<span data-ttu-id="ac22e-456">Valores: **falso**, **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="ac22e-457">**Número**</span><span class="sxs-lookup"><span data-stu-id="ac22e-457">**Number**</span></span>|<span data-ttu-id="ac22e-458">Um dupla precisão número de vírgula flutuante, IEEE 754 padrão.</span><span class="sxs-lookup"><span data-stu-id="ac22e-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="ac22e-459">**Cadeia**</span><span class="sxs-lookup"><span data-stu-id="ac22e-459">**String**</span></span>|<span data-ttu-id="ac22e-460">Uma sequência de zero ou mais carateres Unicode.</span><span class="sxs-lookup"><span data-stu-id="ac22e-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="ac22e-461">Cadeias de têm de estar entre aspas único ou duplo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="ac22e-462">**Matriz**</span><span class="sxs-lookup"><span data-stu-id="ac22e-462">**Array**</span></span>|<span data-ttu-id="ac22e-463">Uma sequência de zero ou mais elementos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="ac22e-464">Cada elemento pode ser um valor de qualquer tipo de dados escalar, exceto Undefined.</span><span class="sxs-lookup"><span data-stu-id="ac22e-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="ac22e-465">**Objeto**</span><span class="sxs-lookup"><span data-stu-id="ac22e-465">**Object**</span></span>|<span data-ttu-id="ac22e-466">Um conjunto não ordenado de zero ou mais pares nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ac22e-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="ac22e-467">O nome é uma cadeia Unicode, o valor pode ser de qualquer tipo de dados escalar, exceto **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="ac22e-468">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-468">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="ac22e-469">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="ac22e-470">Valor de representa não definida do tipo Undefined.</span><span class="sxs-lookup"><span data-stu-id="ac22e-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="ac22e-471">Representa **nulo** valor do tipo **nulo**.</span><span class="sxs-lookup"><span data-stu-id="ac22e-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="ac22e-472">Representa a constante de tipo Booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="ac22e-473">Representa **falso** valor do tipo Booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="ac22e-474">Representa **verdadeiro** valor do tipo Booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="ac22e-475">Representa uma constante.</span><span class="sxs-lookup"><span data-stu-id="ac22e-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="ac22e-476">As literais decimais são os números de representado utilizando notação decimal ou notação científica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="ac22e-477">As literais hexadecimal são os números de representado utilizando o prefixo '0x' seguido de um ou mais dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="ac22e-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="ac22e-478">Representa uma constante de tipo cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="ac22e-479">As literais de cadeia são cadeias Unicode representadas por uma sequência de zero ou mais carateres Unicode ou sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="ac22e-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="ac22e-480">As literais de cadeia estão incluídas no plicas (apóstrofo: ') ou de aspas (aspas: ").</span><span class="sxs-lookup"><span data-stu-id="ac22e-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="ac22e-481">São permitidas seguintes sequências de escape:</span><span class="sxs-lookup"><span data-stu-id="ac22e-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="ac22e-482">**Sequência de escape**</span><span class="sxs-lookup"><span data-stu-id="ac22e-482">**Escape sequence**</span></span>|<span data-ttu-id="ac22e-483">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="ac22e-483">**Description**</span></span>|<span data-ttu-id="ac22e-484">**Carácter Unicode**</span><span class="sxs-lookup"><span data-stu-id="ac22e-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="ac22e-485">\\'</span><span class="sxs-lookup"><span data-stu-id="ac22e-485">\\'</span></span>|<span data-ttu-id="ac22e-486">apóstrofo (')</span><span class="sxs-lookup"><span data-stu-id="ac22e-486">apostrophe (')</span></span>|<span data-ttu-id="ac22e-487">U + 0027</span><span class="sxs-lookup"><span data-stu-id="ac22e-487">U+0027</span></span>|  
|<span data-ttu-id="ac22e-488">\\"</span><span class="sxs-lookup"><span data-stu-id="ac22e-488">\\"</span></span>|<span data-ttu-id="ac22e-489">aspas (")</span><span class="sxs-lookup"><span data-stu-id="ac22e-489">quotation mark (")</span></span>|<span data-ttu-id="ac22e-490">U + 0022</span><span class="sxs-lookup"><span data-stu-id="ac22e-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="ac22e-491">solidus inversa (\\)</span><span class="sxs-lookup"><span data-stu-id="ac22e-491">reverse solidus (\\)</span></span>|<span data-ttu-id="ac22e-492">U + 005C</span><span class="sxs-lookup"><span data-stu-id="ac22e-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="ac22e-493">solidus (/)</span><span class="sxs-lookup"><span data-stu-id="ac22e-493">solidus (/)</span></span>|<span data-ttu-id="ac22e-494">U + 002F</span><span class="sxs-lookup"><span data-stu-id="ac22e-494">U+002F</span></span>|  
|<span data-ttu-id="ac22e-495">\b</span><span class="sxs-lookup"><span data-stu-id="ac22e-495">\b</span></span>|<span data-ttu-id="ac22e-496">RETROCESSO</span><span class="sxs-lookup"><span data-stu-id="ac22e-496">backspace</span></span>|<span data-ttu-id="ac22e-497">U + 0008</span><span class="sxs-lookup"><span data-stu-id="ac22e-497">U+0008</span></span>|  
|<span data-ttu-id="ac22e-498">\f</span><span class="sxs-lookup"><span data-stu-id="ac22e-498">\f</span></span>|<span data-ttu-id="ac22e-499">feed do formulário</span><span class="sxs-lookup"><span data-stu-id="ac22e-499">form feed</span></span>|<span data-ttu-id="ac22e-500">U + 000C</span><span class="sxs-lookup"><span data-stu-id="ac22e-500">U+000C</span></span>|  
|\n|<span data-ttu-id="ac22e-501">linha</span><span class="sxs-lookup"><span data-stu-id="ac22e-501">line feed</span></span>|<span data-ttu-id="ac22e-502">U + 000A</span><span class="sxs-lookup"><span data-stu-id="ac22e-502">U+000A</span></span>|  
|<span data-ttu-id="ac22e-503">\r</span><span class="sxs-lookup"><span data-stu-id="ac22e-503">\r</span></span>|<span data-ttu-id="ac22e-504">avanço retorno</span><span class="sxs-lookup"><span data-stu-id="ac22e-504">carriage return</span></span>|<span data-ttu-id="ac22e-505">U + 000D</span><span class="sxs-lookup"><span data-stu-id="ac22e-505">U+000D</span></span>|  
|<span data-ttu-id="ac22e-506">\t</span><span class="sxs-lookup"><span data-stu-id="ac22e-506">\t</span></span>|<span data-ttu-id="ac22e-507">Separador</span><span class="sxs-lookup"><span data-stu-id="ac22e-507">tab</span></span>|<span data-ttu-id="ac22e-508">U + 0009</span><span class="sxs-lookup"><span data-stu-id="ac22e-508">U+0009</span></span>|  
|<span data-ttu-id="ac22e-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="ac22e-509">\uXXXX</span></span>|<span data-ttu-id="ac22e-510">Um carácter Unicode definido pelo 4 dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="ac22e-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="ac22e-511">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="ac22e-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="ac22e-512"><a name="bk_query_perf_guidelines"></a>Diretrizes de desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="ac22e-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="ac22e-513">Ordem de para um toobe consulta executada de forma eficiente para uma coleção grande, deverá utilizar os filtros que podem ser servidos através de um ou mais índices.</span><span class="sxs-lookup"><span data-stu-id="ac22e-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="ac22e-514">Olá seguintes filtros será considerado para a pesquisa do índice:</span><span class="sxs-lookup"><span data-stu-id="ac22e-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="ac22e-515">Utilize o operador de igualdade (=) com uma expressão de caminho do documento e uma constante.</span><span class="sxs-lookup"><span data-stu-id="ac22e-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="ac22e-516">Utilizar os operadores de intervalo (<, \<=, >, > =) com uma expressão de caminho do documento e constantes de números.</span><span class="sxs-lookup"><span data-stu-id="ac22e-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="ac22e-517">Expressão de caminho do documento representa uma expressão que identifica um caminho de constante em documentos de Olá da coleção da base de dados de Olá referenciado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="ac22e-518">**Expressão de caminho do documento**</span><span class="sxs-lookup"><span data-stu-id="ac22e-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="ac22e-519">Expressões de caminho do documento são expressões que um caminho de propriedade ou matriz assessors indexador através de um documento proveniente de documentos de coleção da base de dados.</span><span class="sxs-lookup"><span data-stu-id="ac22e-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="ac22e-520">Este caminho pode ser utilizado tooidentify Olá localização dos valores referenciada num filtro diretamente no documentos Olá na coleção da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="ac22e-521">Para um toobe expressão considerada uma expressão de caminho do documento, deve:</span><span class="sxs-lookup"><span data-stu-id="ac22e-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="ac22e-522">Referência Olá coleção raiz diretamente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="ac22e-523">Indexador de matriz de propriedade ou constante referência de algumas expressão de caminho do documento</span><span class="sxs-lookup"><span data-stu-id="ac22e-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="ac22e-524">Um alias, que representa alguns expressão de caminho do documento de referência.</span><span class="sxs-lookup"><span data-stu-id="ac22e-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="ac22e-525">**Convenções de sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="ac22e-526">Olá, a tabela seguinte descreve Olá convenções utilizadas toodescribe sintaxe numa referência de linguagem de consulta do DocumentDB API Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="ac22e-527">**Convenção**</span><span class="sxs-lookup"><span data-stu-id="ac22e-527">**Convention**</span></span>|<span data-ttu-id="ac22e-528">**Utilizado para**</span><span class="sxs-lookup"><span data-stu-id="ac22e-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="ac22e-529">EM MAIÚSCULAS</span><span class="sxs-lookup"><span data-stu-id="ac22e-529">UPPERCASE</span></span>|<span data-ttu-id="ac22e-530">Palavras-chave sensível.</span><span class="sxs-lookup"><span data-stu-id="ac22e-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="ac22e-531">minúsculas</span><span class="sxs-lookup"><span data-stu-id="ac22e-531">lowercase</span></span>|<span data-ttu-id="ac22e-532">Palavras-chave de maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="ac22e-533">\<nonterminal ></span><span class="sxs-lookup"><span data-stu-id="ac22e-533">\<nonterminal></span></span>|<span data-ttu-id="ac22e-534">Nonterminal, definidas separadamente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="ac22e-535">\<nonterminal >:: =</span><span class="sxs-lookup"><span data-stu-id="ac22e-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="ac22e-536">Definição de sintaxe de nonterminal Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="ac22e-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="ac22e-537">other_terminal</span></span>|<span data-ttu-id="ac22e-538">Terminal (token), descrito detalhadamente nas palavras.</span><span class="sxs-lookup"><span data-stu-id="ac22e-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="ac22e-539">Identificador</span><span class="sxs-lookup"><span data-stu-id="ac22e-539">identifier</span></span>|<span data-ttu-id="ac22e-540">Identificador.</span><span class="sxs-lookup"><span data-stu-id="ac22e-540">Identifier.</span></span> <span data-ttu-id="ac22e-541">Permite que os seguintes carateres: caráter de _First. a-z A-Z 0-9 não pode ser um dígito.</span><span class="sxs-lookup"><span data-stu-id="ac22e-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="ac22e-542">"cadeia"</span><span class="sxs-lookup"><span data-stu-id="ac22e-542">"string"</span></span>|<span data-ttu-id="ac22e-543">Cadeia delimitada por aspas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-543">Quoted string.</span></span> <span data-ttu-id="ac22e-544">Permite que qualquer cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-544">Allows any valid string.</span></span> <span data-ttu-id="ac22e-545">Ver descrição de um string_literal.</span><span class="sxs-lookup"><span data-stu-id="ac22e-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="ac22e-546">'símbolo'</span><span class="sxs-lookup"><span data-stu-id="ac22e-546">'symbol'</span></span>|<span data-ttu-id="ac22e-547">Símbolo literal que faz parte da sintaxe de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="ac22e-548">&#124; (barra vertical)</span><span class="sxs-lookup"><span data-stu-id="ac22e-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="ac22e-549">Alternativas para itens de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="ac22e-549">Alternatives for syntax items.</span></span> <span data-ttu-id="ac22e-550">Pode utilizar apenas um dos itens de Olá especificados.</span><span class="sxs-lookup"><span data-stu-id="ac22e-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="ac22e-551">[] /(brackets)</span><span class="sxs-lookup"><span data-stu-id="ac22e-551">[ ] /(brackets)</span></span>|<span data-ttu-id="ac22e-552">Retos coloque um ou mais itens opcionais.</span><span class="sxs-lookup"><span data-stu-id="ac22e-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="ac22e-553">[,.. n]</span><span class="sxs-lookup"><span data-stu-id="ac22e-553">[ ,...n ]</span></span>|<span data-ttu-id="ac22e-554">Indica a Olá precedente item pode ser n repetida diversas vezes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="ac22e-555">as ocorrências de Olá são separadas por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="ac22e-556">[.. n]</span><span class="sxs-lookup"><span data-stu-id="ac22e-556">[ ...n ]</span></span>|<span data-ttu-id="ac22e-557">Indica a Olá precedente item pode ser n repetida diversas vezes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="ac22e-558">as ocorrências de Olá são separadas por espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="ac22e-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="ac22e-559"><a name="bk_built_in_functions"></a>Funções incorporadas</span><span class="sxs-lookup"><span data-stu-id="ac22e-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="ac22e-560">BD do Cosmos do Azure fornece várias funções incorporadas do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ac22e-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="ac22e-561">categorias de Olá das funções incorporadas são listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="ac22e-562">Função</span><span class="sxs-lookup"><span data-stu-id="ac22e-562">Function</span></span>|<span data-ttu-id="ac22e-563">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac22e-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="ac22e-564">Funções matemática</span><span class="sxs-lookup"><span data-stu-id="ac22e-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="ac22e-565">Olá matemática funções cada efetuar um cálculo, normalmente, com base nos valores de entrada que são fornecidos como argumentos e devolvem um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="ac22e-566">A verificar as funções de tipo</span><span class="sxs-lookup"><span data-stu-id="ac22e-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="ac22e-567">funções de verificação de tipo de Olá permitem-lhe tipo de Olá toocheck de uma expressão dentro de consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="ac22e-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="ac22e-568">Funções de cadeia</span><span class="sxs-lookup"><span data-stu-id="ac22e-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="ac22e-569">as funções de cadeia Olá efetuar uma operação num valor de cadeia de entrada e devolvem uma cadeia, o valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="ac22e-570">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="ac22e-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="ac22e-571">as funções de matriz Olá efetuar uma operação num valor de entrada da matriz e devolver um valor numérico, o valor de cadeia Boolean ou matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="ac22e-572">Funções geográficos</span><span class="sxs-lookup"><span data-stu-id="ac22e-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="ac22e-573">funções geográficos Olá efetuar uma operação num valor de entrada do objeto espacial e devolvem um valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="ac22e-574"><a name="bk_mathematical_functions"></a>Funções matemática</span><span class="sxs-lookup"><span data-stu-id="ac22e-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="ac22e-575">Olá seguintes funções de efetuar um cálculo, normalmente, com base nos valores de entrada que são fornecidos como argumentos e devolvem um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ac22e-576">ABS</span><span class="sxs-lookup"><span data-stu-id="ac22e-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="ac22e-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="ac22e-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="ac22e-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="ac22e-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="ac22e-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="ac22e-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="ac22e-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="ac22e-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="ac22e-581">LIMITE</span><span class="sxs-lookup"><span data-stu-id="ac22e-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="ac22e-582">COS</span><span class="sxs-lookup"><span data-stu-id="ac22e-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="ac22e-583">COT</span><span class="sxs-lookup"><span data-stu-id="ac22e-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="ac22e-584">GRAUS</span><span class="sxs-lookup"><span data-stu-id="ac22e-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="ac22e-585">EXP</span><span class="sxs-lookup"><span data-stu-id="ac22e-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="ac22e-586">PISO</span><span class="sxs-lookup"><span data-stu-id="ac22e-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="ac22e-587">REGISTO</span><span class="sxs-lookup"><span data-stu-id="ac22e-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="ac22e-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="ac22e-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="ac22e-589">INSTALADOR DE PLATAFORMA</span><span class="sxs-lookup"><span data-stu-id="ac22e-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="ac22e-590">ENERGIA</span><span class="sxs-lookup"><span data-stu-id="ac22e-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="ac22e-591">RADIANOS</span><span class="sxs-lookup"><span data-stu-id="ac22e-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="ac22e-592">ARREDONDAR</span><span class="sxs-lookup"><span data-stu-id="ac22e-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="ac22e-593">ÚNICO</span><span class="sxs-lookup"><span data-stu-id="ac22e-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="ac22e-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="ac22e-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="ac22e-595">PARÊNTESES</span><span class="sxs-lookup"><span data-stu-id="ac22e-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="ac22e-596">INÍCIO DE SESSÃO</span><span class="sxs-lookup"><span data-stu-id="ac22e-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="ac22e-597">TAN</span><span class="sxs-lookup"><span data-stu-id="ac22e-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="ac22e-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="ac22e-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="ac22e-599"><a name="bk_abs"></a>ABS</span><span class="sxs-lookup"><span data-stu-id="ac22e-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="ac22e-600">Devolve Olá absoluto () especificado um valor positivo de Olá expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-601">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-602">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-603">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-604">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-604">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-605">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-606">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-606">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-607">Olá exemplo seguinte mostra os resultados de Olá de utilização da função de Olá ABS em três números diferentes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="ac22e-608">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="ac22e-609"><a name="bk_acos"></a>ACOS</span><span class="sxs-lookup"><span data-stu-id="ac22e-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="ac22e-610">Ângulo do devolve Olá, em radianos, cujo co-seno é o Olá especificada uma expressão numérica; Também denominado o arco de co-seno.</span><span class="sxs-lookup"><span data-stu-id="ac22e-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="ac22e-611">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-612">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-613">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-614">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-614">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-615">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-616">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-616">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-617">Olá exemplo seguinte devolve Olá ACOS de -1.</span><span class="sxs-lookup"><span data-stu-id="ac22e-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="ac22e-618">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="ac22e-619"><a name="bk_asin"></a>ASIN</span><span class="sxs-lookup"><span data-stu-id="ac22e-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="ac22e-620">Ângulo do devolve Olá, em radianos, cujo seno é o Olá especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="ac22e-621">Isto também é denominado o arco de seno.</span><span class="sxs-lookup"><span data-stu-id="ac22e-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="ac22e-622">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-623">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-624">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-625">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-625">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-626">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-627">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-627">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-628">Olá exemplo seguinte devolve Olá ASIN de -1.</span><span class="sxs-lookup"><span data-stu-id="ac22e-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="ac22e-629">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="ac22e-630"><a name="bk_atan"></a>ATAN</span><span class="sxs-lookup"><span data-stu-id="ac22e-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="ac22e-631">Ângulo do devolve Olá, em radianos, cuja tangente é o Olá especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="ac22e-632">Isto também é denominado o arco de tangente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="ac22e-633">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-634">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-635">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-636">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-636">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-637">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-638">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-638">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-639">Olá seguinte o exemplo Olá ATAN de Olá, devolve o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="ac22e-640">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="ac22e-641"><a name="bk_atn2"></a>ATN2</span><span class="sxs-lookup"><span data-stu-id="ac22e-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="ac22e-642">Devolve o valor principal do Olá do Olá arco tangente de y / x, expressado em radianos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="ac22e-643">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-644">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-645">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-646">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-646">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-647">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-648">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-648">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-649">Olá exemplo seguinte calcula Olá ATN2 para Olá especificado x e y componentes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="ac22e-650">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="ac22e-651"><a name="bk_ceiling"></a>LIMITE</span><span class="sxs-lookup"><span data-stu-id="ac22e-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="ac22e-652">Devolve Olá menor número inteiro maior que ou igual ao hello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-653">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-654">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-655">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-656">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-656">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-657">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-658">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-658">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-659">Olá seguinte exemplo mostra numérico positivo, negativo, e zero valores com Olá função de limite.</span><span class="sxs-lookup"><span data-stu-id="ac22e-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="ac22e-660">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="ac22e-661"><a name="bk_cos"></a>COS</span><span class="sxs-lookup"><span data-stu-id="ac22e-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="ac22e-662">Devolve Olá trigonometric co-seno de Olá especificado ângulo, em radianos, nas Olá especificada a expressão.</span><span class="sxs-lookup"><span data-stu-id="ac22e-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="ac22e-663">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-664">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-665">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-666">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-666">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-667">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-668">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-668">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-669">Olá seguinte o exemplo calcula Olá COS de Olá de ângulo especificado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="ac22e-670">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="ac22e-671"><a name="bk_cot"></a>COT</span><span class="sxs-lookup"><span data-stu-id="ac22e-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="ac22e-672">Co-tangente de trigonometric Olá devolve de Olá especificado ângulo, em radianos, nas Olá especificada a expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-673">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-674">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-675">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-676">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-676">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-677">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-678">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-678">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-679">calcula o seguinte exemplo de Olá Olá COT do ângulo especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="ac22e-680">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="ac22e-681"><a name="bk_degrees"></a>GRAUS</span><span class="sxs-lookup"><span data-stu-id="ac22e-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="ac22e-682">Devolve Olá correspondente ângulo em graus para um ângulo especificado em radianos.</span><span class="sxs-lookup"><span data-stu-id="ac22e-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="ac22e-683">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-684">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-685">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-686">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-686">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-687">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-688">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-688">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-689">Olá exemplo seguinte devolve Olá número de graus um ângulo de radianos PI/2.</span><span class="sxs-lookup"><span data-stu-id="ac22e-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="ac22e-690">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="ac22e-691"><a name="bk_floor"></a>PISO</span><span class="sxs-lookup"><span data-stu-id="ac22e-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="ac22e-692">Devolve um número inteiro maior de Olá inferior ou igual toohello especificada a expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-693">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-694">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-695">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-696">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-696">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-697">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-698">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-698">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-699">Olá seguinte exemplo mostra numérico positivo, negativo, e zero valores com Olá função piso.</span><span class="sxs-lookup"><span data-stu-id="ac22e-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="ac22e-700">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="ac22e-701"><a name="bk_exp"></a>EXP</span><span class="sxs-lookup"><span data-stu-id="ac22e-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="ac22e-702">Devolve Olá valor exponencial Olá especificada a expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-703">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-704">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-705">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-706">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-706">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-707">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-708">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-708">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-709">constante de Olá **i** (2.718281...), é Olá base do natural logarithms.</span><span class="sxs-lookup"><span data-stu-id="ac22e-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="ac22e-710">Olá expoente de um número é Olá constante **i** gerado toohello energia número Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="ac22e-711">Por exemplo EXP(1.0) = i ^ 1.0 = 2.71828182845905 e EXP(10) = i ^ 10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="ac22e-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="ac22e-712">Olá exponencial do logaritmo natural de Olá de um número é o número de Olá próprio: EXP (registo (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ac22e-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="ac22e-713">E o logaritmo natural de Olá de Olá exponencial de um número é o número de Olá próprio: registo (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ac22e-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="ac22e-714">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-714">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-715">Olá exemplo seguinte declara uma variável e devolve Olá exponencial valor de variável especificado de Olá (10).</span><span class="sxs-lookup"><span data-stu-id="ac22e-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="ac22e-716">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="ac22e-717">Olá exemplo seguinte devolve Olá exponencial valor logaritmo natural de Olá de 20 e o logaritmo natural de Olá de Olá exponencial de 20.</span><span class="sxs-lookup"><span data-stu-id="ac22e-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="ac22e-718">Uma vez que estas funções são funções de inverso um do outro, valor de retorno de Olá com arredondamento de vírgula flutuante bibliotecas em ambos os casos é 20.</span><span class="sxs-lookup"><span data-stu-id="ac22e-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="ac22e-719">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="ac22e-720"><a name="bk_log"></a>REGISTO</span><span class="sxs-lookup"><span data-stu-id="ac22e-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="ac22e-721">Devolve Olá natural logaritmo de Olá especificada a expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-722">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="ac22e-723">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-724">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="ac22e-725">Argumento numérico opcional que define Olá base para logaritmo Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="ac22e-726">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-726">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-727">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-728">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-728">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-729">Por predefinição, LOG() devolve o logaritmo natural de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="ac22e-730">Pode alterar a base de Olá do valor de tooanother Olá logaritmo utilizando Olá base é o parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="ac22e-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="ac22e-731">logaritmo natural de Olá é Olá logaritmo toohello base **i**, onde **i** é uma constante too2.718281828 de aproximadamente igual irrational.</span><span class="sxs-lookup"><span data-stu-id="ac22e-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="ac22e-732">logaritmo natural de Olá de Olá exponencial de um número é o número de Olá próprio: registo (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ac22e-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="ac22e-733">E Olá exponencial do logaritmo natural de Olá de um número é o número de Olá próprio: EXP (registo (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ac22e-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="ac22e-734">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-734">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-735">Olá exemplo seguinte declara uma variável e devolve Olá logaritmo valor de variável especificado de Olá (10).</span><span class="sxs-lookup"><span data-stu-id="ac22e-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="ac22e-736">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="ac22e-737">Olá exemplo seguinte calcula Olá registo para expoente Olá de um número.</span><span class="sxs-lookup"><span data-stu-id="ac22e-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="ac22e-738">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="ac22e-739"><a name="bk_log10"></a>LOG10</span><span class="sxs-lookup"><span data-stu-id="ac22e-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="ac22e-740">Logaritmo base 10 de Olá de devolve de Olá especificada a expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-741">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-742">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-743">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-744">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-744">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-745">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-746">**Observações**</span><span class="sxs-lookup"><span data-stu-id="ac22e-746">**Remarks**</span></span>  
  
 <span data-ttu-id="ac22e-747">Olá LOG10 e funções de energia são tooone inversely relacionado outro.</span><span class="sxs-lookup"><span data-stu-id="ac22e-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="ac22e-748">Por exemplo, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="ac22e-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="ac22e-749">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-749">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-750">Olá exemplo seguinte declara uma variável e devolve Olá LOG10 valor de variável especificado de Olá (100).</span><span class="sxs-lookup"><span data-stu-id="ac22e-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="ac22e-751">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="ac22e-752"><a name="bk_pi"></a>INSTALADOR DE PLATAFORMA</span><span class="sxs-lookup"><span data-stu-id="ac22e-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="ac22e-753">Devolve Olá constante valor de PI.</span><span class="sxs-lookup"><span data-stu-id="ac22e-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="ac22e-754">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="ac22e-755">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-756">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-757">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-757">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-758">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-759">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-759">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-760">Olá exemplo seguinte devolve Olá valor de PI.</span><span class="sxs-lookup"><span data-stu-id="ac22e-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="ac22e-761">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="ac22e-762"><a name="bk_power"></a>ENERGIA</span><span class="sxs-lookup"><span data-stu-id="ac22e-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="ac22e-763">Devolve o valor de Olá especificado de Olá toohello de expressão especificado energia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="ac22e-764">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="ac22e-765">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-766">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="ac22e-767">É Olá energia toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="ac22e-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="ac22e-768">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-768">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-769">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-770">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-770">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-771">Olá seguinte o exemplo demonstra que gera uma potência de toohello número de 3 (cubo Olá número Olá).</span><span class="sxs-lookup"><span data-stu-id="ac22e-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="ac22e-772">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="ac22e-773"><a name="bk_radians"></a>RADIANOS</span><span class="sxs-lookup"><span data-stu-id="ac22e-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="ac22e-774">Devolve radianos quando uma expressão numérica, em graus, é introduzida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="ac22e-775">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-776">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-777">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-778">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-778">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-779">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-780">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-780">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-781">Olá exemplo seguinte utiliza os ângulos de alguns como entrada e devolve os valores de radian correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ac22e-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="ac22e-782">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="ac22e-783"><a name="bk_round"></a>ARREDONDAR</span><span class="sxs-lookup"><span data-stu-id="ac22e-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="ac22e-784">Devolve um valor numérico, o valor de número inteiro mais próximo toohello arredondado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="ac22e-785">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-786">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-787">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-788">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-788">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-789">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-790">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-790">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-791">Olá exemplo seguinte Arredonda por excesso Olá seguintes números positivos e negativos toohello mais próximo número inteiro.</span><span class="sxs-lookup"><span data-stu-id="ac22e-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="ac22e-792">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="ac22e-793"><a name="bk_sign"></a>INÍCIO DE SESSÃO</span><span class="sxs-lookup"><span data-stu-id="ac22e-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="ac22e-794">Devolve Olá positivo (+ 1), zero (0), negativo (-1) sinal de Olá foi especificado ou expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-795">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-796">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-797">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-798">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-798">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-799">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-800">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-800">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-801">Olá exemplo seguinte devolve os valores de início de sessão de Olá de números de too2-2.</span><span class="sxs-lookup"><span data-stu-id="ac22e-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="ac22e-802">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="ac22e-803"><a name="bk_sin"></a>ÚNICO</span><span class="sxs-lookup"><span data-stu-id="ac22e-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="ac22e-804">Devolve Olá trigonometric seno Olá especificado ângulo, em radianos, nas Olá especificada a expressão.</span><span class="sxs-lookup"><span data-stu-id="ac22e-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="ac22e-805">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-806">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-807">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-808">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-808">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-809">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-810">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-810">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-811">calcula o seguinte exemplo de Olá Olá único do ângulo especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="ac22e-812">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="ac22e-813"><a name="bk_sqrt"></a>SQRT</span><span class="sxs-lookup"><span data-stu-id="ac22e-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="ac22e-814">Devolve Olá cuja raiz quadrada de Olá especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="ac22e-815">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-816">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-817">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-818">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-818">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-819">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-820">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-820">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-821">Olá exemplo seguinte devolve Olá raízes de quadrada dos números 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="ac22e-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="ac22e-822">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="ac22e-823"><a name="bk_square"></a>PARÊNTESES</span><span class="sxs-lookup"><span data-stu-id="ac22e-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="ac22e-824">Olá devolve quadrado de Olá especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="ac22e-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="ac22e-825">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-826">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-827">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-828">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-828">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-829">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-830">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-830">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-831">Olá exemplo seguinte devolve quadrados Olá dos números 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="ac22e-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="ac22e-832">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="ac22e-833"><a name="bk_tan"></a>TAN</span><span class="sxs-lookup"><span data-stu-id="ac22e-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="ac22e-834">Tangente Olá devolve Olá especificado ângulo, em radianos, nas Olá especificada a expressão.</span><span class="sxs-lookup"><span data-stu-id="ac22e-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="ac22e-835">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-836">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-837">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-838">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-838">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-839">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-840">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-840">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-841">Olá exemplo seguinte calcula tangente Olá (de) PI / 2.</span><span class="sxs-lookup"><span data-stu-id="ac22e-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="ac22e-842">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="ac22e-843"><a name="bk_trunc"></a>TRUNC</span><span class="sxs-lookup"><span data-stu-id="ac22e-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="ac22e-844">Devolve um valor numérico, o valor de número inteiro mais próximo toohello truncada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="ac22e-845">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="ac22e-846">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ac22e-847">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-848">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-848">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-849">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-850">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-850">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-851">Olá seguinte o exemplo trunca Olá seguintes números positivos e negativos toohello. o valor de número inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="ac22e-852">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="ac22e-853"><a name="bk_type_checking_functions"></a>A verificar as funções de tipo</span><span class="sxs-lookup"><span data-stu-id="ac22e-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="ac22e-854">Olá funções seguintes suportam o tipo de verificação contra os valores de entrada e cada devolver um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ac22e-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="ac22e-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="ac22e-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="ac22e-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="ac22e-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="ac22e-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="ac22e-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="ac22e-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="ac22e-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="ac22e-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="ac22e-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="ac22e-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="ac22e-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="ac22e-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="ac22e-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="ac22e-863"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="ac22e-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="ac22e-864">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="ac22e-865">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="ac22e-866">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-867">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-868">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-868">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-869">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-870">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-870">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-871">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="ac22e-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-872">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="ac22e-873"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="ac22e-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="ac22e-874">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="ac22e-875">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="ac22e-876">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-877">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-878">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-878">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-879">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-880">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-880">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-881">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="ac22e-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-882">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="ac22e-883"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="ac22e-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="ac22e-884">Devolve um valor boleano que indica se foi atribuída um valor de propriedade de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="ac22e-885">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="ac22e-886">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-887">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-888">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-888">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-889">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-890">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-890">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-891">Olá seguintes verificações de exemplo para a presença de Olá de uma propriedade no Olá especificado documento JSON.</span><span class="sxs-lookup"><span data-stu-id="ac22e-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="ac22e-892">Olá primeiro devolve true, uma vez que "a" está presente, mas Olá segundo devolve false, uma vez que "b" está ausente.</span><span class="sxs-lookup"><span data-stu-id="ac22e-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="ac22e-893">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="ac22e-894"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="ac22e-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="ac22e-895">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é nulo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="ac22e-896">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="ac22e-897">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-898">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-899">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-899">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-900">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-901">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-901">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-902">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="ac22e-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-903">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="ac22e-904"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="ac22e-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="ac22e-905">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão for um número.</span><span class="sxs-lookup"><span data-stu-id="ac22e-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="ac22e-906">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="ac22e-907">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-908">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-909">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-909">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-910">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-911">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-911">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-912">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="ac22e-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-913">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="ac22e-914"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ac22e-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="ac22e-915">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="ac22e-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="ac22e-916">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="ac22e-917">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-918">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-919">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-919">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-920">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-921">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-921">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-922">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="ac22e-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-923">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="ac22e-924"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="ac22e-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="ac22e-925">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma primitiva (string, Boolean, numérico ou null).</span><span class="sxs-lookup"><span data-stu-id="ac22e-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="ac22e-926">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="ac22e-927">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-928">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-929">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-929">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-930">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-931">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-931">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-932">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="ac22e-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-933">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="ac22e-934"><a name="bk_is_string"></a>IS_STRING</span><span class="sxs-lookup"><span data-stu-id="ac22e-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="ac22e-935">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="ac22e-936">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="ac22e-937">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ac22e-938">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-939">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-939">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-940">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-941">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-941">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-942">Olá exemplo seguinte verifica objetos de JSON booleano número, cadeia, null, objeto, matriz e tipos indefinidos utilizando Olá função IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="ac22e-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ac22e-943">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="ac22e-944"><a name="bk_string_functions"></a>Funções de cadeia</span><span class="sxs-lookup"><span data-stu-id="ac22e-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="ac22e-945">Olá seguintes funções escalares efetuar uma operação num valor de cadeia de entrada e devolvem uma cadeia, o valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ac22e-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="ac22e-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="ac22e-947">CONTÉM</span><span class="sxs-lookup"><span data-stu-id="ac22e-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="ac22e-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="ac22e-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="ac22e-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="ac22e-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="ac22e-950">À ESQUERDA</span><span class="sxs-lookup"><span data-stu-id="ac22e-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="ac22e-951">COMPRIMENTO</span><span class="sxs-lookup"><span data-stu-id="ac22e-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="ac22e-952">INFERIOR</span><span class="sxs-lookup"><span data-stu-id="ac22e-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="ac22e-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="ac22e-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="ac22e-954">SUBSTITUIR</span><span class="sxs-lookup"><span data-stu-id="ac22e-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="ac22e-955">REPLICAR</span><span class="sxs-lookup"><span data-stu-id="ac22e-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="ac22e-956">INVERSA</span><span class="sxs-lookup"><span data-stu-id="ac22e-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="ac22e-957">À DIREITA</span><span class="sxs-lookup"><span data-stu-id="ac22e-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="ac22e-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="ac22e-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="ac22e-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="ac22e-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="ac22e-960">SUBCADEIA</span><span class="sxs-lookup"><span data-stu-id="ac22e-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="ac22e-961">SUPERIOR</span><span class="sxs-lookup"><span data-stu-id="ac22e-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="ac22e-962"><a name="bk_concat"></a>CONCAT</span><span class="sxs-lookup"><span data-stu-id="ac22e-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="ac22e-963">Devolve uma cadeia que é o resultado Olá concatenar duas ou mais valores de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="ac22e-964">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="ac22e-965">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-966">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-967">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-967">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-968">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-969">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-969">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-970">Olá exemplo devolve Olá concatenado cadeia de Olá os seguintes valores especificados.</span><span class="sxs-lookup"><span data-stu-id="ac22e-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="ac22e-971">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="ac22e-972"><a name="bk_contains"></a>CONTÉM</span><span class="sxs-lookup"><span data-stu-id="ac22e-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="ac22e-973">Devolve um valor boleano que indica se primeira expressão de cadeia Olá contém Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="ac22e-974">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ac22e-975">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-976">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-977">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-977">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-978">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-979">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-979">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-980">Olá exemplo seguinte verifica se o "abc" contém "ab" e contém "d".</span><span class="sxs-lookup"><span data-stu-id="ac22e-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="ac22e-981">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="ac22e-982"><a name="bk_endswith"></a>ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="ac22e-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="ac22e-983">Devolve um valor boleano que indica se primeira expressão de cadeia Olá termina com Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="ac22e-984">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ac22e-985">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-986">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-987">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-987">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-988">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-989">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-989">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-990">Olá exemplo seguinte devolve Olá "abc" termina com "b" e "bc".</span><span class="sxs-lookup"><span data-stu-id="ac22e-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="ac22e-991">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="ac22e-992"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="ac22e-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="ac22e-993">Devolve Olá iniciar a posição da primeira ocorrência de Olá de Olá segunda cadeia expressão numa expressão de cadeia especificada primeiro Olá ou -1 se não é possível encontrar a cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="ac22e-994">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ac22e-995">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-996">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-997">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-997">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-998">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-999">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-999">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1000">Olá exemplo seguinte devolve Olá índice de subcadeias vários dentro "abc".</span><span class="sxs-lookup"><span data-stu-id="ac22e-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="ac22e-1001">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="ac22e-1002"><a name="bk_left"></a>À ESQUERDA</span><span class="sxs-lookup"><span data-stu-id="ac22e-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="ac22e-1003">Devolve Olá parte esquerda de uma cadeia com Olá especificado número de carateres.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="ac22e-1004">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="ac22e-1005">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1006">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ac22e-1007">Se qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-1008">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1009">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1010">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1010">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1011">Olá exemplo seguinte devolve Olá deixado parte "abc" para vários valores de comprimento.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="ac22e-1012">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="ac22e-1013"><a name="bk_length"></a>COMPRIMENTO</span><span class="sxs-lookup"><span data-stu-id="ac22e-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="ac22e-1014">Devolve Olá número de carateres de Olá especificada a expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1015">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1016">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1017">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1018">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1019">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1020">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1020">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1021">Olá exemplo seguinte devolve Olá comprimento de uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="ac22e-1022">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="ac22e-1023"><a name="bk_lower"></a>INFERIOR</span><span class="sxs-lookup"><span data-stu-id="ac22e-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="ac22e-1024">Devolve uma expressão de cadeia após a conversão toolowercase de dados do caráter em maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="ac22e-1025">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1026">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1027">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1028">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1029">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1030">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1030">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1031">Olá seguinte exemplo mostra como toouse inferior numa consulta.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="ac22e-1032">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="ac22e-1033"><a name="bk_ltrim"></a>LTRIM</span><span class="sxs-lookup"><span data-stu-id="ac22e-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="ac22e-1034">Devolve uma expressão de cadeia após remove espaços em branco à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="ac22e-1035">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1036">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1037">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1038">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1039">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1040">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1040">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1041">Olá seguinte exemplo mostra como toouse LTRIM dentro de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="ac22e-1042">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="ac22e-1043"><a name="bk_replace"></a>SUBSTITUIR</span><span class="sxs-lookup"><span data-stu-id="ac22e-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="ac22e-1044">Substitui todas as ocorrências de um valor de cadeia especificada com outro valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="ac22e-1045">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1046">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1047">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1048">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1049">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1050">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1050">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1051">Olá seguinte exemplo mostra como toouse substituir numa consulta.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="ac22e-1052">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="ac22e-1053"><a name="bk_replicate"></a>REPLICAR</span><span class="sxs-lookup"><span data-stu-id="ac22e-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="ac22e-1054">Repete-se um valor de cadeia um número de vezes especificado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="ac22e-1055">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="ac22e-1056">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1057">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ac22e-1058">Se qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-1059">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1060">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1061">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1061">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1062">Olá seguinte exemplo mostra como toouse REPLICAR numa consulta.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="ac22e-1063">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="ac22e-1064"><a name="bk_reverse"></a>INVERSA</span><span class="sxs-lookup"><span data-stu-id="ac22e-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="ac22e-1065">Devolve a ordem inversa de Olá de um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="ac22e-1066">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1067">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1068">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1069">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1070">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1071">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1071">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1072">Olá seguinte exemplo mostra como toouse INVERSO numa consulta.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="ac22e-1073">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="ac22e-1074"><a name="bk_right"></a>À DIREITA</span><span class="sxs-lookup"><span data-stu-id="ac22e-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="ac22e-1075">Olá devolve direito fazem parte de uma cadeia com Olá especificar o número de carateres.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="ac22e-1076">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="ac22e-1077">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1078">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ac22e-1079">Se qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-1080">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1081">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1082">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1082">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1083">Olá exemplo seguinte devolve Olá parte direita de "abc" para vários valores de comprimento.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="ac22e-1084">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="ac22e-1085"><a name="bk_rtrim"></a>RTRIM</span><span class="sxs-lookup"><span data-stu-id="ac22e-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="ac22e-1086">Devolve uma expressão de cadeia após remove espaços em branco à direita.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="ac22e-1087">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1088">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1089">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1090">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1091">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1092">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1092">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1093">Olá seguinte exemplo mostra como toouse RTRIM dentro de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="ac22e-1094">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="ac22e-1095"><a name="bk_startswith"></a>STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="ac22e-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="ac22e-1096">Devolve um valor boleano que indica se primeira expressão de cadeia Olá começa com Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="ac22e-1097">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1098">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1099">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1100">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1101">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-1102">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1102">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1103">Olá exemplo seguinte, verifica se a hello cadeia "abc" começa com "b" e "a".</span><span class="sxs-lookup"><span data-stu-id="ac22e-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="ac22e-1104">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="ac22e-1105"><a name="bk_substring"></a>SUBCADEIA</span><span class="sxs-lookup"><span data-stu-id="ac22e-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="ac22e-1106">Devolve parte de uma expressão de cadeia começando Olá especificado posição de caráter baseado em zero e continua a toohello especificado comprimento ou toohello fim da cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="ac22e-1107">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="ac22e-1108">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1109">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ac22e-1110">Se qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-1111">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1112">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1113">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1113">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1114">Olá exemplo seguinte devolve Olá subcadeia de "abc" começando em 1 e durante um período de 1 caráter.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="ac22e-1115">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="ac22e-1116"><a name="bk_upper"></a>SUPERIOR</span><span class="sxs-lookup"><span data-stu-id="ac22e-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="ac22e-1117">Devolve uma expressão de cadeia após a conversão toouppercase de dados do caráter em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="ac22e-1118">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="ac22e-1119">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ac22e-1120">É uma expressão de cadeia válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1121">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1122">Devolve uma expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ac22e-1123">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1123">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1124">Olá seguinte exemplo mostra como toouse superior numa consulta</span><span class="sxs-lookup"><span data-stu-id="ac22e-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="ac22e-1125">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="ac22e-1126"><a name="bk_array_functions"></a>Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="ac22e-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="ac22e-1127">Olá seguintes funções escalares efetuar uma operação num valor de entrada da matriz e devolver um valor numérico, valor de cadeia Boolean ou matriz</span><span class="sxs-lookup"><span data-stu-id="ac22e-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ac22e-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="ac22e-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="ac22e-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="ac22e-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="ac22e-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="ac22e-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="ac22e-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="ac22e-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="ac22e-1132"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="ac22e-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="ac22e-1133">Devolve uma matriz que é o resultado Olá concatenar duas ou mais valores de matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="ac22e-1134">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="ac22e-1135">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ac22e-1136">É uma expressão de matriz válido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="ac22e-1137">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1138">Devolve uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="ac22e-1139">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1139">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1140">Olá seguintes como tooconcatenate duas matrizes de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="ac22e-1141">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="ac22e-1142"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="ac22e-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="ac22e-1143">Devolve um valor boleano que indica se a matriz de Olá contém Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="ac22e-1144">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="ac22e-1145">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ac22e-1146">É uma expressão de matriz válido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="ac22e-1147">Se qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ac22e-1148">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1149">Devolve um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ac22e-1150">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1150">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1151">Olá seguinte o exemplo de como toocheck para associação a uma matriz ARRAY_CONTAINS a utilizar.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="ac22e-1152">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="ac22e-1153"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="ac22e-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="ac22e-1154">Devolve o número de Olá de elementos de Olá especificada a expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="ac22e-1155">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="ac22e-1156">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ac22e-1157">É uma expressão de matriz válido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="ac22e-1158">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1159">Devolve uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-1160">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1160">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1161">Olá seguintes exemplo como tooget Olá comprimento de uma matriz ARRAY_LENGTH a utilizar.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="ac22e-1162">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="ac22e-1163"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="ac22e-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="ac22e-1164">Devolve a parte de uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="ac22e-1165">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="ac22e-1166">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ac22e-1167">É uma expressão de matriz válido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ac22e-1168">Se qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ac22e-1169">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1170">Devolve um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ac22e-1171">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1171">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1172">Olá seguinte o exemplo de como tooget uma parte de uma matriz ARRAY_SLICE a utilizar.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="ac22e-1173">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="ac22e-1174"><a name="bk_spatial_functions"></a>Funções geográficos</span><span class="sxs-lookup"><span data-stu-id="ac22e-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="ac22e-1175">Olá seguintes funções escalares efetuar uma operação num valor de entrada do objeto espacial e devolvem um valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ac22e-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="ac22e-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="ac22e-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="ac22e-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="ac22e-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="ac22e-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="ac22e-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ac22e-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="ac22e-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ac22e-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="ac22e-1181"><a name="bk_st_distance"></a>ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="ac22e-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="ac22e-1182">Devolve a distância Olá entre Olá dois GeoJSON ponto, Polygon ou LineString expressões.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="ac22e-1183">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="ac22e-1184">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1185">Se qualquer expressão de objeto GeoJSON ponto, polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="ac22e-1186">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1187">Devolve uma expressão numérica, que contém a distância Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="ac22e-1188">Este valor é expresso em medidores Olá predefinição sistema de referência.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="ac22e-1189">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1189">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1190">Olá seguinte exemplo mostra como tooreturn todos os documentos famílias que estejam dentro de 30 km de Olá especificado localização utilizando a função incorporada do Olá ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="ac22e-1191">.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="ac22e-1192">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="ac22e-1193"><a name="bk_st_within"></a>ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="ac22e-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="ac22e-1194">Devolve uma expressão booleana a indicar se Olá GeoJSON objeto (ponto, polígono ou LineString) especificado no primeiro argumento de Olá está dentro do Olá GeoJSON (ponto, polígono ou LineString) no argumento da segunda Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="ac22e-1195">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="ac22e-1196">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1197">Se qualquer expressão de objeto GeoJSON ponto, polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1198">Se qualquer expressão de objeto GeoJSON ponto, polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="ac22e-1199">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1200">Devolve um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ac22e-1201">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1201">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1202">Olá seguinte exemplo mostra como toofind família todos os documentos dentro de um polígono com ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="ac22e-1203">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="ac22e-1204"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="ac22e-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="ac22e-1205">Devolve uma expressão de booleana indicando se Olá GeoJSON objeto (ponto, polígono ou LineString) especificado no primeiro argumento de Olá intersetar Olá GeoJSON (ponto, polígono ou LineString) no argumento da segunda Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="ac22e-1206">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="ac22e-1207">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1208">Se qualquer expressão de objeto GeoJSON ponto, polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1209">Se qualquer expressão de objeto GeoJSON ponto, polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="ac22e-1210">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1211">Devolve um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ac22e-1212">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1212">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1213">Olá seguinte exemplo mostra como toofind todas as áreas intersetar com Olá fornecido polígono.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="ac22e-1214">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="ac22e-1215"><a name="bk_st_isvalid"></a>ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ac22e-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="ac22e-1216">Devolve um valor de Booleano indicando se Olá especificada a expressão de ponto de GeoJSON, polígono ou LineString é válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="ac22e-1217">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="ac22e-1218">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1219">Se qualquer expressão GeoJSON ponto, polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="ac22e-1220">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1221">Devolve uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ac22e-1222">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1222">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1223">Olá seguinte exemplo mostra como toocheck se existir um ponto utilizando ST_VALID válido.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="ac22e-1224">Por exemplo, este ponto tem um valor de latitude que não se encontra no intervalo de valores [-90, 90] válido Olá, por isso, Olá consulta devolve false.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="ac22e-1225">Para multilinestrings, Olá GeoJSON especificação requer que Olá último coordenada par de fornecidas deve ser Olá mesmo como toocreate primeiro, Olá uma forma fechada.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="ac22e-1226">Pontos de dentro de um polígono tem de ser especificados por ordem counter-no sentido horário.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="ac22e-1227">Um polígono especificado na ordem no sentido horário representa inverso Olá da região de Olá dentro da mesma.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="ac22e-1228">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="ac22e-1229"><a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ac22e-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="ac22e-1230">Devolve um valor JSON que contém um valor booleano se Olá especificado GeoJSON ponto, polígono ou LineString expressão é válido e se inválido, Olá, além disso, razão como um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="ac22e-1231">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="ac22e-1232">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ac22e-1233">Se qualquer expressão de ponto ou polígono GeoJSON válida.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="ac22e-1234">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="ac22e-1235">Devolve um valor JSON que contém um valor booleano se Olá especificado GeoJSON ponto ou expressão de polígono é válido e se inválido, Olá, além disso, razão como um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="ac22e-1236">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="ac22e-1236">**Examples**</span></span>  
  
 <span data-ttu-id="ac22e-1237">Olá seguinte como exemplo de validade da toocheck (com detalhes) utilizando ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="ac22e-1238">Eis o conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac22e-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="ac22e-1239">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ac22e-1239">Next steps</span></span>  
 <span data-ttu-id="ac22e-1240">[Sintaxe SQL e consulta SQL para a base de dados do Azure Cosmos](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="ac22e-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="ac22e-1241">Documentação do Cosmos BD do Azure</span><span class="sxs-lookup"><span data-stu-id="ac22e-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
