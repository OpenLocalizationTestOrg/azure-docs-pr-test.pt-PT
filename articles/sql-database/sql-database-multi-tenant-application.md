---
title: "aplicação de SaaS multi-inquilino aaaImplement com a SQL Database do Azure | Microsoft Docs"
description: "Implemente aplicações de SaaS multi-inquilino com a SQL Database do Azure."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Implementar uma aplicação de SaaS multi-inquilino através da SQL Database do Azure

Uma aplicação de multi-inquilino é uma aplicação alojada num ambiente de nuvem e que fornece Olá mesmo conjunto de serviços toohundreds ou milhares de inquilinos que não partilhe e ver os dados entre si. Um exemplo é uma aplicação SaaS que fornece serviços tootenants num ambiente alojado na nuvem. Este modelo isola os dados de Olá para cada inquilino e otimiza a distribuição de Olá dos recursos de custo. 

Este tutorial demonstra como toocreate uma aplicação de SaaS multi-inquilino através da SQL Database do Azure.

Neste tutorial, irá aprender a:
> [!div class="checklist"]
> * Configurar um toosupport de ambiente de base de dados de uma aplicação de SaaS multi-inquilino, através do padrão de base de dados por inquilino Olá
> * Criar um inquilino de catálogo
> * Aprovisionar uma base de dados do inquilino e registá-lo no catálogo de inquilino Olá
> * Configurar um exemplo de aplicação de Java 
> * Aceder a uma aplicação de consola Java simples de bases de dados do inquilino
> * Eliminar um inquilino

Se não tiver uma subscrição do Azure, [criar uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete disponibilizar este tutorial, se tiver:

* Versão mais recente do Olá instalado do PowerShell e Olá [Azure PowerShell SDK mais recente](http://azure.microsoft.com/downloads/)

* Versão mais recente do Olá instalado do [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Instalar o SQL Server Management Studio também instala a versão mais recente do Olá do SQLPackage, um utilitário da linha de comandos que pode ser utilizado tooautomate uma variedade de tarefas de programação de base de dados.

* Olá instalado [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) e Olá [mais recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) instalado no seu computador. 

* Instalado [Apache Maven](https://maven.apache.org/download.cgi). Será utilizado maven toohelp Gerir dependências, criar, testar e executar o projeto de Java de exemplo de Olá

## <a name="set-up-data-environment"></a>Configurar o ambiente de dados

Aprovisionar uma base de dados por inquilino. modelo de base de dados por inquilino Olá fornece grau mais elevado de Olá de isolamento de inquilinos, DevOps um custo reduzido. custo de Olá toooptimize dos recursos de nuvem, será também aprovisionar Olá inquilino as bases de dados para um conjunto elástico, que permite-lhe o desempenho de preços de Olá toooptimize para um grupo de bases de dados. toolearn sobre outra base de dados de aprovisionamento modelos [apresentada aqui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Siga estes passos toocreate um SQL server e um conjunto elástico que irá alojar todas as bases de dados do inquilino. 

1. Crie variáveis toostore valores que serão utilizados no rest Olá tutorial Olá. Certifique-se de que toomodify Olá IP endereço variável tooinclude do endereço IP 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. Início de sessão tooAzure e criar um conjunto de servidor e elástico SQL 
   
   ```PowerShell
   # Login tooAzure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a>Criar o catálogo de inquilino 

Uma aplicação SaaS multi-inquilino, é importante tooknow armazenar informações para um inquilino. Isto é normalmente armazenado numa base de dados do catálogo. base de dados de catálogo de Olá é toohold utilizado um mapeamento entre um inquilino e uma base de dados na qual os dados nesse inquilino estão armazenados.  padrão de básico Olá se aplica se um multi-inquilino ou uma base de dados único inquilino é utilizado.

Siga estes passos toocreate uma base de dados do catálogo de aplicações de SaaS de exemplo de Olá.

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Aprovisionar a base de dados para 'tenant1' e registar no catálogo de inquilino 
Utilizar o Powershell tooprovision uma base de dados para um novo inquilino 'tenant1' e registe este inquilino no catálogo de Olá. 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Aprovisionar a base de dados para 'tenant2' e registar no catálogo de inquilino
Utilizar o Powershell tooprovision uma base de dados para um novo inquilino 'tenant2' e registe este inquilino no catálogo de Olá. 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a>Configurar o exemplo de aplicação de Java 

1. Crie um projeto maven. Escreva o seguinte Olá numa janela de linha de comandos:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Adicionar esta dependência, o nível de idioma e criar opção toosupport ficheiros de manifesto no ficheiro de pom.xml v7 toohello:
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
   <build>
        <plugins>
           <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-jar-plugin</artifactId>
              <version>3.0.0</version>
              <configuration>
                 <archive>
                    <manifest>
                       <mainClass>com.sqldbsamples.App</mainClass>
                    </manifest>
                 </archive>
              </configuration>
           </plugin>
        </plugins>
   </build>
   ```

3. Adicione Olá seguinte no ficheiro de App.java Olá:

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in hello system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. Guarde o ficheiro de Olá.

5. Aceda a consola de toocommand e executar

   ```bash
   mvn package
   ```

6. Quando terminar, executar Olá seguintes aplicações de Olá toorun 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
saída de Olá terá este aspeto se for executado com êxito:

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a>Eliminar primeiro inquilino 
Utilize o PowerShell toodelete Olá inquilino da base de dados e o catálogo de entrada para o inquilino primeiro Olá.

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

Tente ligar-se demasiado 'tenant1' utilizando Olá aplicação Java. Irá receber um erro a indicar que inquilino Olá não existe.

## <a name="next-steps"></a>Passos seguintes 

Neste tutorial, aprendeu a:
> [!div class="checklist"]
> * Configurar um toosupport de ambiente de base de dados de uma aplicação de SaaS multi-inquilino, através do padrão de base de dados por inquilino Olá
> * Criar um inquilino de catálogo
> * Aprovisionar uma base de dados do inquilino e registá-lo no catálogo de inquilino Olá
> * Configurar um exemplo de aplicação de Java 
> * Aceder a uma aplicação de consola Java simples de bases de dados do inquilino
> * Eliminar um inquilino

* Exemplos do PowerShell para tarefas comuns, consulte [exemplos do PowerShell de base de dados do SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Padrões para Consulte de aplicações de SaaS multi-inquilino de conceção [padrões de conceção](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Exemplos de Java para tarefas comuns do Azure, consulte [Centro para programadores do Java](https://azure.microsoft.com/develop/java/)



