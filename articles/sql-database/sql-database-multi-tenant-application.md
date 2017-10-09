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
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="c737f-103">Implementar uma aplicação de SaaS multi-inquilino através da SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="c737f-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="c737f-104">Uma aplicação de multi-inquilino é uma aplicação alojada num ambiente de nuvem e que fornece Olá mesmo conjunto de serviços toohundreds ou milhares de inquilinos que não partilhe e ver os dados entre si.</span><span class="sxs-lookup"><span data-stu-id="c737f-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="c737f-105">Um exemplo é uma aplicação SaaS que fornece serviços tootenants num ambiente alojado na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c737f-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="c737f-106">Este modelo isola os dados de Olá para cada inquilino e otimiza a distribuição de Olá dos recursos de custo.</span><span class="sxs-lookup"><span data-stu-id="c737f-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="c737f-107">Este tutorial demonstra como toocreate uma aplicação de SaaS multi-inquilino através da SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="c737f-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="c737f-108">Neste tutorial, irá aprender a:</span><span class="sxs-lookup"><span data-stu-id="c737f-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="c737f-109">Configurar um toosupport de ambiente de base de dados de uma aplicação de SaaS multi-inquilino, através do padrão de base de dados por inquilino Olá</span><span class="sxs-lookup"><span data-stu-id="c737f-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="c737f-110">Criar um inquilino de catálogo</span><span class="sxs-lookup"><span data-stu-id="c737f-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="c737f-111">Aprovisionar uma base de dados do inquilino e registá-lo no catálogo de inquilino Olá</span><span class="sxs-lookup"><span data-stu-id="c737f-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="c737f-112">Configurar um exemplo de aplicação de Java</span><span class="sxs-lookup"><span data-stu-id="c737f-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="c737f-113">Aceder a uma aplicação de consola Java simples de bases de dados do inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="c737f-114">Eliminar um inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-114">Delete a tenant</span></span>

<span data-ttu-id="c737f-115">Se não tiver uma subscrição do Azure, [criar uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="c737f-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c737f-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c737f-116">Prerequisites</span></span>

<span data-ttu-id="c737f-117">toocomplete disponibilizar este tutorial, se tiver:</span><span class="sxs-lookup"><span data-stu-id="c737f-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="c737f-118">Versão mais recente do Olá instalado do PowerShell e Olá [Azure PowerShell SDK mais recente](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="c737f-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="c737f-119">Versão mais recente do Olá instalado do [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="c737f-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="c737f-120">Instalar o SQL Server Management Studio também instala a versão mais recente do Olá do SQLPackage, um utilitário da linha de comandos que pode ser utilizado tooautomate uma variedade de tarefas de programação de base de dados.</span><span class="sxs-lookup"><span data-stu-id="c737f-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="c737f-121">Olá instalado [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) e Olá [mais recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) instalado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="c737f-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="c737f-122">Instalado [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="c737f-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="c737f-123">Será utilizado maven toohelp Gerir dependências, criar, testar e executar o projeto de Java de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="c737f-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="c737f-124">Configurar o ambiente de dados</span><span class="sxs-lookup"><span data-stu-id="c737f-124">Set up data environment</span></span>

<span data-ttu-id="c737f-125">Aprovisionar uma base de dados por inquilino.</span><span class="sxs-lookup"><span data-stu-id="c737f-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="c737f-126">modelo de base de dados por inquilino Olá fornece grau mais elevado de Olá de isolamento de inquilinos, DevOps um custo reduzido.</span><span class="sxs-lookup"><span data-stu-id="c737f-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="c737f-127">custo de Olá toooptimize dos recursos de nuvem, será também aprovisionar Olá inquilino as bases de dados para um conjunto elástico, que permite-lhe o desempenho de preços de Olá toooptimize para um grupo de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="c737f-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="c737f-128">toolearn sobre outra base de dados de aprovisionamento modelos [apresentada aqui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="c737f-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="c737f-129">Siga estes passos toocreate um SQL server e um conjunto elástico que irá alojar todas as bases de dados do inquilino.</span><span class="sxs-lookup"><span data-stu-id="c737f-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="c737f-130">Crie variáveis toostore valores que serão utilizados no rest Olá tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="c737f-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="c737f-131">Certifique-se de que toomodify Olá IP endereço variável tooinclude do endereço IP</span><span class="sxs-lookup"><span data-stu-id="c737f-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
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
   
2. <span data-ttu-id="c737f-132">Início de sessão tooAzure e criar um conjunto de servidor e elástico SQL</span><span class="sxs-lookup"><span data-stu-id="c737f-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="c737f-133">Criar o catálogo de inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-133">Create tenant catalog</span></span> 

<span data-ttu-id="c737f-134">Uma aplicação SaaS multi-inquilino, é importante tooknow armazenar informações para um inquilino.</span><span class="sxs-lookup"><span data-stu-id="c737f-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="c737f-135">Isto é normalmente armazenado numa base de dados do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c737f-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="c737f-136">base de dados de catálogo de Olá é toohold utilizado um mapeamento entre um inquilino e uma base de dados na qual os dados nesse inquilino estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="c737f-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="c737f-137">padrão de básico Olá se aplica se um multi-inquilino ou uma base de dados único inquilino é utilizado.</span><span class="sxs-lookup"><span data-stu-id="c737f-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="c737f-138">Siga estes passos toocreate uma base de dados do catálogo de aplicações de SaaS de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c737f-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="c737f-139">Aprovisionar a base de dados para 'tenant1' e registar no catálogo de inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="c737f-140">Utilizar o Powershell tooprovision uma base de dados para um novo inquilino 'tenant1' e registe este inquilino no catálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c737f-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="c737f-141">Aprovisionar a base de dados para 'tenant2' e registar no catálogo de inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="c737f-142">Utilizar o Powershell tooprovision uma base de dados para um novo inquilino 'tenant2' e registe este inquilino no catálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c737f-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="c737f-143">Configurar o exemplo de aplicação de Java</span><span class="sxs-lookup"><span data-stu-id="c737f-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="c737f-144">Crie um projeto maven.</span><span class="sxs-lookup"><span data-stu-id="c737f-144">Create a maven project.</span></span> <span data-ttu-id="c737f-145">Escreva o seguinte Olá numa janela de linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="c737f-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="c737f-146">Adicionar esta dependência, o nível de idioma e criar opção toosupport ficheiros de manifesto no ficheiro de pom.xml v7 toohello:</span><span class="sxs-lookup"><span data-stu-id="c737f-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="c737f-147">Adicione Olá seguinte no ficheiro de App.java Olá:</span><span class="sxs-lookup"><span data-stu-id="c737f-147">Add hello following into hello App.java file:</span></span>

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

4. <span data-ttu-id="c737f-148">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="c737f-148">Save hello file.</span></span>

5. <span data-ttu-id="c737f-149">Aceda a consola de toocommand e executar</span><span class="sxs-lookup"><span data-stu-id="c737f-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="c737f-150">Quando terminar, executar Olá seguintes aplicações de Olá toorun</span><span class="sxs-lookup"><span data-stu-id="c737f-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="c737f-151">saída de Olá terá este aspeto se for executado com êxito:</span><span class="sxs-lookup"><span data-stu-id="c737f-151">hello output will look like this if it runs successfully:</span></span>

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

## <a name="delete-first-tenant"></a><span data-ttu-id="c737f-152">Eliminar primeiro inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-152">Delete first tenant</span></span> 
<span data-ttu-id="c737f-153">Utilize o PowerShell toodelete Olá inquilino da base de dados e o catálogo de entrada para o inquilino primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="c737f-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="c737f-154">Tente ligar-se demasiado 'tenant1' utilizando Olá aplicação Java.</span><span class="sxs-lookup"><span data-stu-id="c737f-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="c737f-155">Irá receber um erro a indicar que inquilino Olá não existe.</span><span class="sxs-lookup"><span data-stu-id="c737f-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c737f-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c737f-156">Next steps</span></span> 

<span data-ttu-id="c737f-157">Neste tutorial, aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="c737f-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="c737f-158">Configurar um toosupport de ambiente de base de dados de uma aplicação de SaaS multi-inquilino, através do padrão de base de dados por inquilino Olá</span><span class="sxs-lookup"><span data-stu-id="c737f-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="c737f-159">Criar um inquilino de catálogo</span><span class="sxs-lookup"><span data-stu-id="c737f-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="c737f-160">Aprovisionar uma base de dados do inquilino e registá-lo no catálogo de inquilino Olá</span><span class="sxs-lookup"><span data-stu-id="c737f-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="c737f-161">Configurar um exemplo de aplicação de Java</span><span class="sxs-lookup"><span data-stu-id="c737f-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="c737f-162">Aceder a uma aplicação de consola Java simples de bases de dados do inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="c737f-163">Eliminar um inquilino</span><span class="sxs-lookup"><span data-stu-id="c737f-163">Delete a tenant</span></span>

* <span data-ttu-id="c737f-164">Exemplos do PowerShell para tarefas comuns, consulte [exemplos do PowerShell de base de dados do SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="c737f-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="c737f-165">Padrões para Consulte de aplicações de SaaS multi-inquilino de conceção [padrões de conceção](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="c737f-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="c737f-166">Exemplos de Java para tarefas comuns do Azure, consulte [Centro para programadores do Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="c737f-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



