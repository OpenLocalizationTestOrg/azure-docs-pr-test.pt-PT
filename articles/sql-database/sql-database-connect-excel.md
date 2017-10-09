---
title: aaaConnect Excel tooSQL da base de dados | Microsoft Docs
description: "Saiba como tooconnect Microsoft Excel tooAzure SQL da base de dados na nuvem de Olá. Importe dados para o Excel para criação de relatórios e exploração de dados."
services: sql-database
keywords: ligar toosql do excel, importe dados tooexcel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Ligar o Excel tooan SQL database do Azure e criar um relatório

Ligar a base de dados do Excel tooa SQL na nuvem de Olá e importar dados e criar tabelas e gráficos com base nos valores na base de dados de Olá. Neste tutorial, irá configurar a ligação de Olá entre o Excel e uma tabela de base de dados, guardar ficheiro Olá que armazena informações de ligação de dados e Olá para Excel e, em seguida, criar um gráfico dinâmico de Olá valores de base de dados.

Precisa de uma base de dados SQL no Azure antes de começar. Se não tiver uma, consulte o artigo [criar a sua primeira base de dados do SQL Server](sql-database-get-started-portal.md) tooget uma base de dados com dados de exemplo e funcional, em alguns minutos. Neste artigo, irá importar dados de exemplo para o Excel desse artigo, mas pode seguir passos semelhantes com os seus próprios dados.

Irá também precisar de uma cópia do Excel. Este artigo utiliza o [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Ligar a base de dados do Excel tooa SQL e criar um ficheiro odc
1. base de dados do tooSQL do Excel de tooconnect, abra o Excel e, em seguida, crie um novo livro ou abra um livro do Excel existente.
2. Na barra de menus de Olá na Olá parte superior da página Olá clique **dados**, clique em **de outras origens**e, em seguida, clique em **do SQL Server**.
   
   ![Origem de dados selecione: ligar a base de dados do Excel tooSQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   é aberto o Assistente de ligação de dados de Olá.
3. No Olá **ligar tooDatabase servidor** caixa de diálogo, Olá do tipo base de dados SQL **nome do servidor** pretende que o formulário do tooconnect tooin Olá <*servername* > **. database.windows.net**. Por exemplo, **adworkserver.database.windows.net**.
4. Em **iniciar sessão credenciais**, clique em **Olá de utilização seguintes nome de utilizador e palavra-passe**, Olá de tipo **nome de utilizador** e **palavra-passe** definido para a cópia de segurança Olá, servidor de base de dados SQL quando o criou e, em seguida, clique em **seguinte**.
   
   ![Escreva as credenciais de início de sessão e nome do servidor de Olá](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > Dependendo do ambiente de rede, pode não ser capaz de tooconnect ou poderá perder a ligação de Olá se o servidor de base de dados SQL Olá não permite tráfego a partir do seu endereço IP do cliente. Aceda toohello [portal do Azure](https://portal.azure.com/), clique em servidores SQL, clique no servidor, clique em firewall em definições e adicione o seu endereço IP do cliente. Consulte [como definições de firewall tooconfigure](sql-database-configure-firewall-settings.md) para obter mais detalhes.
   > 
   > 
5. No Olá **selecionar base de dados e tabela** caixa de diálogo, base de dados de Olá selecione pretende toowork com lista Olá e, em seguida, clique em tabelas de Olá ou vistas que pretende toowork com (Iremos escolher **vGetAllCategories**) e, em seguida, Clique em **seguinte**.
   
    ![Selecione uma base de dados e a tabela.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Olá **Guardar ficheiro de ligação de dados e termine** abre a caixa de diálogo, onde pode fornecer informações sobre Olá Office da base de dados (*.odc) ficheiro de ligação que o Excel utiliza. Pode manter Olá predefinições ou personalizar as suas seleções.
6. Pode deixar as predefinições de Olá, mas Olá nota **nome de ficheiro** em particular. A **Descrição**, um **nome amigável**, e **as palavras a procurar** ajudá-lo e outros utilizadores Lembre-se de está a ligar tooand localizar a ligação de Olá. Clique em **sempre tentativa toouse estes dados de toorefresh ficheiro** se pretender que as informações de ligação armazenadas no ficheiro odc de Olá, para que possa atualizar quando ligar tooit e, em seguida, clique em **concluir**.
   
    ![Guardar um ficheiro odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    Olá **importar dados** é apresentada a caixa de diálogo.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Importar dados de Olá para o Excel e criar um gráfico dinâmico
Agora que estabeleceu ligação Olá e ficheiro de Olá criada com as informações de ligação de dados e, está a ler dados de Olá tooimport.

1. No Olá **importar dados** caixa de diálogo, clique na opção de Olá que pretende para apresentar os dados na folha de cálculo de Olá e clique **OK**. Vamos escolher **PivotChart**. Também pode escolher toocreate um **nova folha de cálculo** ou demasiado**adicionar este tooa de dados modelo de dados**. Para mais informações sobre Modelos de Dados, consulte [Criar um modelo de dados no Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Clique em **propriedades** tooexplore informações sobre o ficheiro odc de Olá que criou no Olá passo e toochoose opções anteriores para atualizar os dados de Olá.
   
    ![Escolher o formato de Olá para os dados no Excel](./media/sql-database-connect-excel/import-data.png)
   
    folha de cálculo de Olá tem agora um gráfico e uma tabela dinâmicos em branco.
2. Em **campos PivotTable**, selecione Olá todas as caixas de verificação para Olá campos que pretende tooview.
   
    ![Configure o relatório de base de dados.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Se quiser tooconnect outro Excel livros e folhas de cálculo toohello da base de dados, clique em **dados**, clique em **ligações**, clique em **adicionar**, escolha Olá ligação que criou na lista de Olá e, em seguida, clique em **abra**.
> ![Abrir uma ligação a partir de outro livro](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[ligar tooSQL da base de dados com o SQL Server Management Studio](sql-database-connect-query-ssms.md) para consulta e análise avançadas.
* Saiba mais sobre Olá vantagens de [conjuntos elásticos](sql-database-elastic-pool.md).
* Saiba como demasiado[criar uma aplicação web que estabelece ligação tooSQL da base de dados no back-end de Olá](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

