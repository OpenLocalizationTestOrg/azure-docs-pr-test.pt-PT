---
Título: aaa "lesson de suplementar tutorial Azure Analysis Services: segurança dinâmica | Descrição da Microsoft Docs": descreve como toouse segurança dinâmico utilizando a linha filtra tutorial do Olá Azure Analysis Services.
serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '

MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 05/26/2017 Author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Lição suplementar - Segurança dinâmica

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição suplementar, vai criar uma função adicional que implementa a segurança dinâmica. Segurança dinâmica fornece segurança ao nível da linha com base no Olá nome ou o início de sessão id de utilizador do utilizador Olá atualmente com sessão iniciada. 
  
segurança dinâmico de tooimplement, adicione um modelo de tooyour de tabela que contém nomes de utilizador de Olá dos utilizadores que podem ligar toohello modelo e procurar dados e objetos de modelo. modelo de Olá que criar a utilizar neste tutorial está no contexto de Olá do Adventure Works; No entanto, toocomplete isto lesson, tem de adicionar uma tabela que contém os utilizadores do seu próprio domínio. Não precisa de palavras-passe de Olá para nomes de utilizador de Olá que são adicionados. toocreate uma tabela de EmployeeSecurity, com um exemplo pequeno de utilizadores do seu próprio domínio, utilizar Olá colar funcionalidade, colagem de dados de empregado da folha de cálculo do Excel. Um cenário do mundo real, que contém nomes de utilizador de tabela de Olá, normalmente, seria uma tabela a partir de uma base de dados real como uma origem de dados; Por exemplo, uma tabela de DimEmployee real.  
  
segurança de dinâmica tooimplement, utilizar duas funções DAX: [função de nome de utilizador (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) e [função LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Estas funções, aplicadas a uma fórmula de filtro de linha, são definidas numa função nova. Ao utilizar a função LOOKUPVALUE Olá, a fórmula Olá Especifica um valor de tabela de EmployeeSecurity Olá. a fórmula Olá, em seguida, passa a que a função de nome de utilizador do valor toohello, que especifica o nome de utilizador de Olá do utilizador Olá iniciada pertence toothis função. utilizador Olá, em seguida, pode procurar apenas os dados especificados pelos filtros de linha da função de Olá. Neste cenário, pode especificar que os funcionários vendas só podem procurar dados de vendas da Internet para zonas de vendas Olá nos quais forem um membro.  
  
As tarefas necessárias que são exclusivos toothis cenário de modelo em tabela do Adventure Works, mas seriam não se aplicam necessariamente cenário do mundo real de tooa são identificadas como tal. Cada tarefa inclui informações adicionais que descreve a finalidade Olá tarefas Olá.  
  
Estimado tempo toocomplete este lesson: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico de lição suplementar faz parte de um tutorial de modelação em tabela, que deve ser concluído por ordem. Antes de executar tarefas de Olá neste lesson suplementar, deve concluir todas as lições anteriores.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Adicionar Olá DimSalesTerritory tabela toohello AW Internet vendas tabela modelo de projeto  
tooimplement segurança dinâmico para este cenário Adventure Works, tem de adicionar o modelo de tooyour duas tabelas adicionais. tabela primeiro Olá adicionar é DimSalesTerritory (como vendas Oceano Índico) de Olá mesma base de dados AdventureWorksDW. Mais tarde aplicam-se uma tabela de SalesTerritory de toohello de filtro de linha que define os dados de específica de Olá Olá utilizador com sessão iniciada pode navegar.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tabela de DimSalesTerritory tooadd Olá  
  
1.  No Explorador de Modelos em Tabela > **Origens de Dados**, clique com o botão direito do rato na sua ligação e clique em **Importar Tabelas Novas**.  

    Se for apresentada a caixa de diálogo de credenciais de representação de Olá, escreva as credenciais de representação de Olá utilizou Lesson 2: adicionar dados.
  
2.  No navegador, selecione Olá **DimSalesTerritory** tabela e, em seguida, clique em **OK**.    
  
3.  No Editor de consultas, clique em Olá **DimSalesTerritory** consultar e, em seguida, remova **SalesTerritoryAlternateKey** coluna.  
  
7.  Clique em **importar**.  
  
    nova tabela de Olá é adicionada a área de trabalho do toohello modelo. Objetos e dados da tabela de DimSalesTerritory Olá origem, em seguida, são importados para o modelo de tabela de vendas do AW Internet.  
  
9. Depois de tabela Olá foi importada com êxito, clique em **fechar**.  

## <a name="add-a-table-with-user-name-data"></a>Adicionar tabela com dados de nome de utilizador  
tabela de DimEmployee Olá na base de dados de exemplo Olá AdventureWorksDW contém os utilizadores do domínio de AdventureWorks Olá. Estes nomes de utilizador não existem no seu ambiente. Tem de criar uma tabela no seu ambiente que contenha uma pequena amostra (pelo menos, três) de utilizadores reais da sua organização. Em seguida, adicione esses utilizadores como nova função de membros toohello. Não precisa de palavras-passe de Olá para nomes de utilizador de exemplo de Olá, mas tem nomes de utilizador reais do Windows do seu próprio domínio.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd uma tabela de EmployeeSecurity  
  
1.  Abra o Microsoft Excel e crie uma folha de cálculo.  
  
2.  Copie Olá seguinte tabela, incluindo a linha de cabeçalho de Olá e, em seguida, cole-o folha de cálculo de Olá.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Substitua o nome do próprio Olá, o apelido e o domínio ome de utilizador com nomes de Olá e ids de início de sessão de três utilizadores na sua organização. Colocar Olá mesmo utilizador no Olá primeiras duas linhas, para o campo IDdeEmpregado 1, que mostra este utilizador pertence toomore que um território de venda. Deixe Olá campos campo IDdeEmpregado e SalesTerritoryId como estão.  
  
4.  Guardar a folha de cálculo de Olá como **SampleEmployee**.  
  
5.  Na folha de cálculo de Olá, selecione todas as células de Olá com dados de empregado, incluindo os cabeçalhos de Olá, em seguida, faça duplo clique dados Olá selecionado e, em seguida, clique em **cópia**.  
  
6.  No SSDT, clique em Olá **editar** e, em seguida, clique em **colar**.  
  
    Se colar fica a cinzento, clique em qualquer coluna no qualquer tabela na janela estruturador do Olá modelo e tente novamente.  
  
7.  No Olá **pré-visualização de colar** caixa de diálogo **nome da tabela**, tipo **EmployeeSecurity**.  
  
8.  No **toobe dados colado**, certifique-se de que os dados de Olá incluem todos os dados de utilizador de Olá e cabeçalhos da folha de cálculo do Olá SampleEmployee.  
  
9. Verifique se **Utilizar primeira linha como cabeçalhos de coluna** está marcado e clique em **OK**.  
  
    É criada uma nova tabela com o nome EmployeeSecurity com dados de empregado copiados da folha de cálculo do Olá SampleEmployee.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Criar relações entre as tabelas FactInternetSales, DimGeography e DimSalesTerritory  
Olá FactInternetSales, DimGeography e DimSalesTerritory tabela todos os conter uma coluna comuns, SalesTerritoryId. coluna de SalesTerritoryId Olá na tabela de DimSalesTerritory Olá contém valores com um Id diferente para cada território de venda.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>toocreate relações entre Olá FactInternetSales DimGeography, tabela e Olá DimSalesTerritory  
  
1.  Na vista de diagrama, no Olá **DimGeography** tabela, clique e espere Olá **SalesTerritoryId** coluna, em seguida, arraste Olá cursor toohello **SalesTerritoryId** coluna na Olá **DimSalesTerritory** tabela e, em seguida, da versão.  
  
2.  No Olá **FactInternetSales** tabela, clique e espere Olá **SalesTerritoryId** coluna, em seguida, arraste Olá cursor toohello **SalesTerritoryId** coluna na Olá  **DimSalesTerritory** tabela e, em seguida, da versão.  
  
    Olá aviso propriedade ativa para esta relação é False, o que significa que está inativo. tabela FactInternetSales de Olá já tem outra relação de Active Directory.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Ocultar Olá EmployeeSecurity tabela a partir de aplicações de cliente  
Nesta tarefa, ocultar Olá EmployeeSecurity tabela, o mantê-la a apresentação na lista de campos de uma aplicação de cliente. Tenha em conta que a ocultação de tabelas não as protege. Os utilizadores continuam a poder consultar os dados da tabela EmployeeSecurity, se souberem como fazê-lo. toosecure Olá EmployeeSecurity os dados da tabela, impedindo que os utilizadores sejam capaz tooquery qualquer um dos respetivos dados, aplicar um filtro numa tarefa posterior.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>tabela de EmployeeSecurity Olá toohide de aplicações de cliente  
  
-   No estruturador de modelo de Olá, na vista de diagrama, faça duplo clique Olá **empregado** no cabeçalho de tabela e, em seguida, clique em **ocultar ferramentas de cliente**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Criar uma função de utilizador Colaboradores de Vendas por Região  
Nesta tarefa, vai criar uma função de utilizador. Esta função inclui um filtro de linha definir que linhas da tabela de DimSalesTerritory Olá são toousers visível. Olá filtro é então aplicado numa relação um-para-muitos de Olá direção tooall outras tabelas tooDimSalesTerritory relacionado. Também se aplicam um filtro que protege tabela EmployeeSecurity completa Olá sejam consultável por qualquer utilizador que seja membro da função de Olá.  
  
> [!NOTE]  
> Olá funcionários de vendas por função território que criar este lesson restringe membros toobrowse (ou consulta) apenas dados de vendas para Olá território vendas toowhich pertencem. Se adicionar um utilizador como um toohello membro funcionários de vendas por função de território que também existe como um membro numa função criados no [Lesson 11: criar funções](../tutorials/aas-lesson-11-create-roles.md), obtenha uma combinação de permissões. Quando um utilizador é um membro de várias funções, permissões de Olá e definidos para cada função de filtros de linha são cumulativos. Ou seja, o utilizador de Olá tem permissões de maiores Olá determinadas pela combinação de Olá de funções.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate um funcionários de vendas por função de utilizador do Oceano Índico  
  
1.  No SSDT, clique em Olá **modelo** e, em seguida, clique em **funções**.  
  
2.  No **Gestor de Funções**, clique em **Nova**.  
  
    Uma nova função com Olá nenhum permissão é adicionado toohello lista.  
  
3.  Clique em nova função de Olá e, em seguida, no Olá **nome** coluna, mude o nome de função de Olá demasiado**funcionários de vendas por território**.  
  
4.  No Olá **permissões** coluna, clique na lista pendente Olá e, em seguida, selecione Olá **leitura** permissão.  
  
5.  Clique em Olá **membros** separador e, em seguida, clique em **adicionar**.  
  
6.  No Olá **selecionar utilizador ou grupo** caixa de diálogo **objeto de Olá Enter denominado tooselect**, tipo Olá primeiro exemplo nome de utilizador que utilizou quando criar Olá EmployeeSecurity tabela. Clique em **verificar nomes** nome de utilizador de Olá tooverify é válido e, em seguida, clique em **Ok**.  
  
    Repita este passo, adicionar Olá outros exemplos de nomes de utilizador que utilizou quando criar Olá EmployeeSecurity tabela.  
  
7.  Clique em Olá **filtros de linha** separador.  
  
8.  Para Olá **EmployeeSecurity** tabela, Olá **DAX filtro** coluna, Olá tipo seguinte fórmula:  
  
    ```
      =FALSE()  
    ```
  
    Esta fórmula Especifica que todas as colunas resolver toohello de condição booleana FALSO. Não existem colunas da tabela de EmployeeSecurity Olá podem ser consultadas por um membro do Olá funcionários de vendas por função de utilizador do Oceano Índico.  
  
9. Para Olá **DimSalesTerritory** tabela, Olá tipo seguinte fórmula:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    Esta fórmula Olá a função LOOKUPVALUE devolve todos os valores de coluna de Olá DimEmployeeSecurity [SalesTerritoryId] onde hello EmployeeSecurity [LoginId] é Olá mesmo como Olá atual com sessão iniciada num nome de utilizador do Windows e EmployeeSecurity [ SalesTerritoryId] é Olá igual Olá DimSalesTerritory [SalesTerritoryId].  
  
    Olá conjunto de IDs de vendas Oceano Índico devolvido pelo LOOKUPVALUE é, em seguida, utilizado toorestrict Olá linhas apresentadas no Olá DimSalesTerritory tabela. Apenas as linhas onde hello SalesTerritoryID para linha Olá está no conjunto de Olá de IDs devolvido pela função LOOKUPVALUE Olá são apresentadas.  
  
10. No Gestor de Funções, clique em **Ok**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Testar Olá funcionários de vendas por função de utilizador do Oceano Índico  
Nesta tarefa, utilize Olá analisar na funcionalidade de Excel efficacy de Olá tootest SSDT de Olá funcionários de vendas por função de utilizador do Oceano Índico. Especifique um dos nomes de utilizador Olá adicionou toohello EmployeeSecurity tabela e como um membro da função de Olá. Este nome de utilizador, em seguida, é utilizado como nome de utilizador Efetivo Olá na ligação de Olá criada entre o Excel e Olá modelo.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>tootest Olá funcionários de vendas por função de utilizador do Oceano Índico  
  
1.  No SSDT, clique em Olá **modelo** e, em seguida, clique em **analisar no Excel**.  
  
2.  No Olá **analisar no Excel** caixa de diálogo **especifique Olá utilizador nome ou função toouse tooconnect toohello modelo**, selecione **outro utilizador do Windows**e, em seguida, clique em **Procurar**.  
  
3.  No Olá **selecionar utilizador ou grupo** caixa de diálogo **introduza tooselect de nome de objeto Olá**, escreva um nome de utilizador incluído na tabela de EmployeeSecurity Olá e, em seguida, clique em **verificar nomes**.  
  
4.  Clique em **Ok** tooclose Olá **selecionar utilizador ou grupo** caixa de diálogo e, em seguida, clique em **Ok** tooclose Olá **analisar no Excel** caixa de diálogo.  
  
    O Excel abre-se com um livro novo. É criada automaticamente uma Tabela Dinâmica. Olá lista de campos PivotTable inclui a maioria dos campos de dados de Olá disponíveis no seu modelo de novo.  
  
    Tabela de EmployeeSecurity Olá de aviso não é visível no Olá lista de campos da tabela dinâmica. Tal deve-se a tê-la ocultado das ferramentas de cliente numa tarefa anterior.  
  
5.  No Olá **campos** , na área **∑ Internet vendas** (medidas), selecione Olá **InternetTotalSales** medidas. medida de Olá introduzida na Olá **valores** campos.  
  
6.  Selecione Olá **SalesTerritoryId** coluna Olá **DimSalesTerritory** tabela. coluna Olá introduzida na Olá **etiquetas de linha** campos.  
  
    Internet de aviso do volume de vendas são apresentadas apenas para Olá uma região toowhich Olá nome de utilizador Efetivo utilizou pertence. Se selecionar outra coluna, como a cidade da tabela de DimGeography Olá como o campo de etiqueta de linha, cidades apenas num utilizador Efetivo do Olá território vendas toowhich Olá pertence são apresentados.  
  
    Este utilizador não é possível procurar ou consultar quaisquer dados de vendas da Internet para zonas que não sejam Olá um pertencem a. Esta restrição é porque hello filtro da linha definido para a tabela de DimSalesTerritory Olá, no Olá funcionários de vendas por função de utilizador do Oceano Índico, protege os dados para todos os dados relacionados com tooother zonas de vendas.  
  
## <a name="see-also"></a>Veja Também  
[Função USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Função LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Função CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  