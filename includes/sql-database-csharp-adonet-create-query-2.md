
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="fe8f3-101">Exemplo de programa c#</span><span class="sxs-lookup"><span data-stu-id="fe8f3-101">C# program example</span></span>

<span data-ttu-id="fe8f3-102">Olá secções seguintes deste artigo apresentam um programa c# que utiliza ADO.NET toosend Transact-SQL instruções toohello base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="fe8f3-103">programa de Olá c# efetua Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="fe8f3-104">[Estabelece ligação a base de dados do SQL Server de tooour utilizando ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="fe8f3-105">[Cria tabelas](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="fe8f3-106">[Preenche tabelas Olá com dados, através da emissão de instruções INSERT T-SQL](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="fe8f3-107">[Atualizações de dados através de uma associação](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="fe8f3-108">[Elimina os dados através de uma associação](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="fe8f3-109">[Seleciona as linhas de dados através de uma associação](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="fe8f3-110">Fecha a ligação de Olá (que ignora quaisquer tabelas temporárias de tempdb).</span><span class="sxs-lookup"><span data-stu-id="fe8f3-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="fe8f3-111">contém programa Olá c#:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-111">hello C# program contains:</span></span>

- <span data-ttu-id="fe8f3-112">C# código tooconnect toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="fe8f3-113">Métodos Olá T-SQL origem código de retorno.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="fe8f3-114">Dois métodos que submetem Olá base de dados de toohello de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="fe8f3-115">toocompile e executar</span><span class="sxs-lookup"><span data-stu-id="fe8f3-115">toocompile and run</span></span>

<span data-ttu-id="fe8f3-116">Este programa c# está logicamente um ficheiro de CS.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="fe8f3-117">Mas aqui programa Olá fisicamente está dividido em vários blocos de código, toomake cada bloquear toosee mais fácil e compreender.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="fe8f3-118">toocompile e executar este programa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="fe8f3-119">Crie um projeto c# no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="fe8f3-120">tipo de projeto Olá deve ser um *consola* aplicação, de algo semelhante Olá hierarquia os seguintes: **modelos** > **Visual c#** > **Ambiente de trabalho clássico do Windows** > **(.NET Framework) de aplicação de consola**.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="fe8f3-121">No ficheiro de Olá **Program.cs**, apagar linhas de arranque pequeno Olá de código.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="fe8f3-122">Em Program.cs, copiar e colar de Olá blocos, os seguintes na Olá mesma sequência que são apresentados aqui.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="fe8f3-123">Em Program.cs, seguinte de Olá editar valores na Olá **Main** método:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="fe8f3-124">**CB. Origem de dados**</span><span class="sxs-lookup"><span data-stu-id="fe8f3-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="fe8f3-125">**CD. ID de utilizador**</span><span class="sxs-lookup"><span data-stu-id="fe8f3-125">**cd.UserID**</span></span>
   - <span data-ttu-id="fe8f3-126">**CB. Palavra-passe**</span><span class="sxs-lookup"><span data-stu-id="fe8f3-126">**cb.Password**</span></span>
   - <span data-ttu-id="fe8f3-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="fe8f3-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="fe8f3-128">Certifique-se de que assemblagem Olá **System.Data.dll** é referenciado.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="fe8f3-129">tooverify, expanda Olá **referências** nó Olá **Explorador de soluções** painel.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="fe8f3-130">programa de Olá toobuild no Visual Studio, clique em Olá **criar** menu.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="fe8f3-131">programa de Olá toorun do Visual Studio, clique em Olá **iniciar** botão.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="fe8f3-132">resultado do relatório de Olá é apresentado numa janela cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="fe8f3-133">Tem Olá opção de editar Olá T-SQL tooadd à esquerda  **#**  toohello os nomes das tabelas, que cria tabelas temporárias como no **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="fe8f3-134">Isto pode ser útil para fins de demonstração, se não estiver disponível nenhuma base de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="fe8f3-135">Tabelas temporárias são eliminadas automaticamente quando fecha a ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="fe8f3-136">Quaisquer referências para as chaves externas não são impostas para tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="fe8f3-137">C# bloco 1: ligar utilizando ADO.NET</span><span class="sxs-lookup"><span data-stu-id="fe8f3-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="fe8f3-138">Seguinte</span><span class="sxs-lookup"><span data-stu-id="fe8f3-138">Next</span></span>](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="fe8f3-139">C# bloco 2: as tabelas de toocreate T-SQL</span><span class="sxs-lookup"><span data-stu-id="fe8f3-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="fe8f3-140">[Anterior](#cs_1_connect) &nbsp;  /  &nbsp; [seguinte](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="fe8f3-141">Diagrama de relação de entidade (ERD)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="fe8f3-142">Olá anteriores instruções CREATE TABLE envolvem Olá **referências** palavra-chave toocreate um *chave externa* relação (FK) entre duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="fe8f3-143">Se estiver a utilizar tempdb, comente Olá `--REFERENCES` palavra-chave através de um par de traços à esquerda.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="fe8f3-144">Em seguida, é um ERD que mostra a relação de Olá entre duas tabelas de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="fe8f3-145">Olá valores Olá #tabEmployee.DepartmentCode *subordinado* coluna são valores de toohello limitado presentes no Olá #tabDepartment.Department *principal* coluna.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![Chave externa da apresentação ERD](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="fe8f3-147">C# bloco 3: dados de tooinsert T-SQL</span><span class="sxs-lookup"><span data-stu-id="fe8f3-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="fe8f3-148">[Anterior](#cs_2_createtables) &nbsp;  /  &nbsp; [seguinte](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="fe8f3-149">C# bloco 4: associação tooupdate T-SQL</span><span class="sxs-lookup"><span data-stu-id="fe8f3-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="fe8f3-150">[Anterior](#cs_3_insert) &nbsp;  /  &nbsp; [seguinte](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="fe8f3-151">C# bloco 5: associação toodelete T-SQL</span><span class="sxs-lookup"><span data-stu-id="fe8f3-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="fe8f3-152">[Anterior](#cs_4_updatejoin) &nbsp;  /  &nbsp; [seguinte](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="fe8f3-153">C# bloco 6: linhas tooselect de T-SQL</span><span class="sxs-lookup"><span data-stu-id="fe8f3-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="fe8f3-154">[Anterior](#cs_5_deletejoin) &nbsp;  /  &nbsp; [seguinte](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a><span data-ttu-id="fe8f3-155">C# bloco 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="fe8f3-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="fe8f3-156">[Anterior](#cs_6_selectrows) &nbsp;  /  &nbsp; [seguinte](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="fe8f3-157">Este método é concebida toorun Olá T-SQL instrução SELECT que é composta por Olá **Build_6_Tsql_SelectEmployees** método.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="fe8f3-158">C# bloco 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="fe8f3-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="fe8f3-159">[Anterior](#cs_6b_datareader) &nbsp;  /  &nbsp; [seguinte](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="fe8f3-160">Este método é denominado para operações de modificar o conteúdo de dados de Olá de tabelas sem devolver quaisquer linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="fe8f3-161">C# bloco 8: consola de toohello de resultado do teste real</span><span class="sxs-lookup"><span data-stu-id="fe8f3-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="fe8f3-162">Anterior</span><span class="sxs-lookup"><span data-stu-id="fe8f3-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="fe8f3-163">Esta secção captura saída Olá que Olá programa enviado toohello consola.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="fe8f3-164">Apenas os valores de guid do Olá variam entre execuções do teste.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-164">Only hello guid values vary between test runs.</span></span>


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
