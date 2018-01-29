---
title: Utilizar o Java para consultar uma Base de Dados SQL do Azure | Microsoft Docs
description: "Este tópico mostra-lhe como utilizar o Java para criar um programa que se liga a uma base de dados SQL do Azure e a consulta com instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 07/11/2017
ms.author: andrela
ms.openlocfilehash: 994705b0a9c7ca850c357a5810f1edb1618098d6
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/29/2017
---
# <a name="use-java-to-query-an-azure-sql-database"></a>Utilizar o Java para consultar uma base de dados SQL do Azure

Este guia de introdução demonstra como utilizar o [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) para ligar a uma base de dados SQL do Azure e, em seguida, utilizar as instruções Transact-SQL para consultar dados.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este tutorial de início rápido, certifique-se de que tem os seguintes pré-requisitos:

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]

- Uma [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público do computador que utilizar para este tutorial de início rápido.

- Ter instalado o Java e software relacionado para o seu sistema operativo:

    - **MacOS**: instalar o Homebrew e o Java e, em seguida, instalar o Maven. Veja os [Passos 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: instale o Kit de desenvolvimento Java e instale o Maven. Veja os [Passos 1.2, 1.3 e 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: instale o Kit de desenvolvimento Java e o Maven. Veja os [Passos 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>Informações de ligação do servidor SQL

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]

## <a name="create-maven-project-and-dependencies"></a>**Criar projeto Maven e dependências**
1. A partir do terminal, crie um novo projeto Maven chamado **sqltest**. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. Introduza **Y** quando lhe for pedido.
3. Altere o diretório para **sqltest** e abra ***pom.xml*** com o seu editor de texto favorito.  Adicione o **Controlador Microsoft JDBC para SQL Server** às dependências do projeto, com o seguinte código:

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. Também no ***pom.xml***, adicione as propriedades seguintes ao seu projeto.  Se não tiver uma secção de propriedades, pode adicioná-la depois das dependências.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. Guarde e feche ***pom.xml***.

## <a name="insert-code-to-query-sql-database"></a>Inserir código para consultar a base de dados do SQL

1. Já deverá ter um ficheiro chamado ***App.java*** no seu projeto Maven localizado em:... \sqltest\src\main\java\com\sqlsamples\App.Java

2. Abra o ficheiro e substitua os seus conteúdos pelo código seguinte e adicione os valores corretos para o seu servidor, a sua base de dados, o seu utilizador e a sua palavra-passe.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect to database
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-the-code"></a>Executar o código

1. Na linha de comandos, execute os comandos seguintes:

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Confirme que as 20 linhas superiores são devolvidas e, em seguida, feche a janela da aplicação.


## <a name="next-steps"></a>Passos seguintes
- [Criar a sua primeira base de dados SQL do Azure](sql-database-design-first-database.md)
- [Controlador Microsoft JDBC para SQL Server](https://github.com/microsoft/mssql-jdbc)
- [Comunicar problemas/fazer perguntas](https://github.com/microsoft/mssql-jdbc/issues)

