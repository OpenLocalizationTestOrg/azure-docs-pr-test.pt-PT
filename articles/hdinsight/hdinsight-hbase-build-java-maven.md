---
title: "Criar uma aplicação de Java HBase para baseado no Windows Azure HDInsight | Microsoft Docs"
description: "Saiba como utilizar o Apache Maven para criar uma aplicação baseada em Java Apache HBase, em seguida, implementá-la para um cluster baseado no Windows Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 59c9af5a91b107e68a676f02fe5a936f955b22fa
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Utilizar Maven para criar aplicações de Java que utilizam o HBase com o HDInsight (Hadoop) baseado em Windows
Saiba como criar e criar um [Apache HBase](http://hbase.apache.org/) aplicação em Java utilizando o Apache Maven. Em seguida, utilize a aplicação com o Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) é uma ferramenta de gestão e a compreensão de projeto de software que lhe permite criar software, documentação e relatórios para projetos de Java. Neste artigo, irá aprender a utilizá-la para criar uma aplicação básica de Java que cria, consultas, e elimina uma tabela de HBase num cluster do Azure HDInsight.

> [!IMPORTANT]
> Os passos neste documento exigem um cluster do HDInsight que utiliza o Windows. O Linux é o único sistema operativo utilizado na versão 3.4 ou superior do HDInsight. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a name="requirements"></a>Requisitos
* [Plataforma de Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 ou posterior
* [Maven](http://maven.apache.org/)
* Um cluster do HDInsight baseados em Windows com o HBase

    > [!NOTE]
    > Os passos neste documento foi testados com as versões de cluster do HDInsight 3.2 e 3.3. Os valores predefinidos fornecidos nos exemplos são para um cluster de HDInsight 3.3.

## <a name="create-the-project"></a>Criar o projeto
1. Na linha de comandos no seu ambiente de desenvolvimento, altere os diretórios para a localização onde pretende criar o projeto, por exemplo, `cd code\hdinsight`.
2. Utilize o **mvn** comando, que é instalado com o Maven, para gerar o andaime para o projeto.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Este comando cria um diretório na localização atual, com o nome especificado pelo **artifactID** parâmetro (**hbaseapp** neste exemplo.) Este diretório contém os seguintes itens:

   * **pom.XML**: O modelo de objeto do projeto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contém detalhes de informações e configurações utilizados para compilar o projeto.
   * **SRC**: O diretório que contém o **main\java\com\microsoft\examples** directory, onde irá criar a aplicação.
3. Eliminar o **src\test\java\com\microsoft\examples\apptest.java** ficheiro porque não está a ser utilizado neste exemplo.

## <a name="update-the-project-object-model"></a>Atualizar o modelo de objeto do projeto
1. Editar o **pom.xml** de ficheiros e adicione o seguinte código dentro do `<dependencies>` secção:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    Esta secção indica Maven que requer o projeto **hbase-cliente** versão **1.1.2**. No momento da compilação, esta dependência é transferida a partir do repositório de Maven predefinido. Pode utilizar o [pesquisa de repositório Central Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) para saber mais sobre esta dependência.

   > [!IMPORTANT]
   > O número de versão tem de corresponder à versão do HBase que é fornecido com o cluster do HDInsight. Utilize a tabela seguinte para determinar o número de versão correta.
   >
   >

   | Clusters do HDInsight versão | Versão do HBase para utilizar |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Para obter mais informações sobre as versões do HDInsight e componentes, consulte [quais são os diferentes componentes do Hadoop disponíveis com o HDInsight](hdinsight-component-versioning.md).
2. Se estiver a utilizar um cluster do HDInsight 3.3, também tem de adicionar o seguinte para o `<dependencies>` secção:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Esta dependência carregará os componentes de phoenix-core, que são utilizados pela versão do Hbase 1.1.x.
3. Adicione o seguinte código para o **pom.xml** ficheiro. Esta secção tem de estar dentro do `<project>...</project>` etiquetas no ficheiro, por exemplo, entre `</dependencies>` e `</project>`.

        <build>
          <sourceDirectory>src</sourceDirectory>
          <resources>
              <resource>
                <directory>${basedir}/conf</directory>
                <filtering>false</filtering>
                <includes>
                  <include>hbase-site.xml</include>
                </includes>
              </resource>
            </resources>
          <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
              </plugin>
            <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-shade-plugin</artifactId>
              <version>2.3</version>
              <configuration>
                <transformers>
                  <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                    </transformer>
                  </transformers>
              </configuration>
              <executions>
                <execution>
                  <phase>package</phase>
                  <goals>
                    <goal>shade</goal>
                  </goals>
                </execution>
              </executions>
            </plugin>
          </plugins>
        </build>

    O `<resources>` secção configura um recurso (**conf\hbase site.xml**) que contém informações de configuração para o HBase.

   > [!NOTE]
   > Também pode definir valores de configuração através de código. Veja os comentários no **CreateTable** exemplo que se segue para saber como fazê-lo.
   >
   >

    Isto `<plugins>` secção configura o [Plug-in do Maven compilador](http://maven.apache.org/plugins/maven-compiler-plugin/) e [Plug-in do Maven Shade](http://maven.apache.org/plugins/maven-shade-plugin/). O compilador de plug-in é utilizado para compilar a topologia. Shade Plug-in é utilizado para evitar a duplicação de licença no pacote JAR que é composta por Maven. O motivo que é utilizado é que os ficheiros de licença duplicado originar um erro em tempo de execução no cluster do HDInsight. Utilizar maven-shade-Plug-in com o `ApacheLicenseResourceTransformer` implementação impede este erro.

    O maven-shade-Plug-in também produz um uber jar (ou fat jar) que contém todas as dependências necessárias para a aplicação.
4. Guardar o **pom.xml** ficheiro.
5. Criar um novo diretório designado **conf** no **hbaseapp** diretório. No **conf** directory, crie um ficheiro denominado **hbase site.xml**. Utilize o seguinte como conteúdo do ficheiro:

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 The Apache Software Foundation
          *
          * Licensed to the Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See the NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  The ASF licenses this file
          * to you under the Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with the License.  You may obtain a copy of the License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed to in writing, software
          * distributed under the License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See the License for the specific language governing permissions and
          * limitations under the License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    Este ficheiro será utilizado para carregar a configuração do HBase para um cluster do HDInsight.

   > [!NOTE]
   > Este é um ficheiro de hbase-site.xml mínima e contém as definições bare mínimas para o cluster do HDInsight.

6. Guardar o **hbase site.xml** ficheiro.

## <a name="create-the-application"></a>Criar a aplicação
1. Vá para o **hbaseapp\src\main\java\com\microsoft\examples** diretório e o app.java de mudar o nome do ficheiro para **CreateTable.java**.
2. Abra o **CreateTable.java** de ficheiros e substitua o conteúdo existente pelo código seguinte:

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;
        import org.apache.hadoop.hbase.HTableDescriptor;
        import org.apache.hadoop.hbase.TableName;
        import org.apache.hadoop.hbase.HColumnDescriptor;
        import org.apache.hadoop.hbase.client.HTable;
        import org.apache.hadoop.hbase.client.Put;
        import org.apache.hadoop.hbase.util.Bytes;

        public class CreateTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Example of setting zookeeper values for HDInsight
            // in code instead of an hbase-site.xml file
            //
            // config.set("hbase.zookeeper.quorum",
            //            "zookeepernode0,zookeepernode1,zookeepernode2");
            //config.set("hbase.zookeeper.property.clientPort", "2181");
            //config.set("hbase.cluster.distributed", "true");
            // The following sets the znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

            // create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // create the table...
            HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
            // ... with two column families
            tableDescriptor.addFamily(new HColumnDescriptor("name"));
            tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
            admin.createTable(tableDescriptor);

            // define some people
            String[][] people = {
                { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
                { "2", "Franklin", "Holtz", "franklin@contoso.com" },
                { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
                { "4", "Rae", "Schroeder", "rae@contoso.com" },
                { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
                { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

            HTable table = new HTable(config, "people");

            // Add each person to the table
            //   Use the `name` column family for the name
            //   Use the `contactinfo` column family for the email
            for (int i = 0; i< people.length; i++) {
              Put person = new Put(Bytes.toBytes(people[i][0]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
              person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
              table.put(person);
            }
            // flush commits and close the table
            table.flushCommits();
            table.close();
          }
        }

    Este é o **CreateTable** classe, que irá criar uma tabela com o nome **pessoas** e preenchê-lo com alguns utilizadores predefinidas.
3. Guardar o **CreateTable.java** ficheiro.
4. No **hbaseapp\src\main\java\com\microsoft\examples** directory, crie um novo ficheiro designado **SearchByEmail.java**. Utilize o seguinte código como o conteúdo deste ficheiro:

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HTable;
        import org.apache.hadoop.hbase.client.Scan;
        import org.apache.hadoop.hbase.client.ResultScanner;
        import org.apache.hadoop.hbase.client.Result;
        import org.apache.hadoop.hbase.filter.RegexStringComparator;
        import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
        import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
        import org.apache.hadoop.hbase.util.Bytes;
        import org.apache.hadoop.util.GenericOptionsParser;

        public class SearchByEmail {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Use GenericOptionsParser to get only the parameters to the class
            // and not all the parameters passed (when using WebHCat for example)
            String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
            if (otherArgs.length != 1) {
              System.out.println("usage: [regular expression]");
              System.exit(-1);
            }

            // Open the table
            HTable table = new HTable(config, "people");

            // Define the family and qualifiers to be used
            byte[] contactFamily = Bytes.toBytes("contactinfo");
            byte[] emailQualifier = Bytes.toBytes("email");
            byte[] nameFamily = Bytes.toBytes("name");
            byte[] firstNameQualifier = Bytes.toBytes("first");
            byte[] lastNameQualifier = Bytes.toBytes("last");

            // Create a new regex filter
            RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
            // Attach the regex filter to a filter
            //   for the email column
            SingleColumnValueFilter filter = new SingleColumnValueFilter(
              contactFamily,
              emailQualifier,
              CompareOp.EQUAL,
              emailFilter
            );

            // Create a scan and set the filter
            Scan scan = new Scan();
            scan.setFilter(filter);

            // Get the results
            ResultScanner results = table.getScanner(scan);
            // Iterate over results and print  values
            for (Result result : results ) {
              String id = new String(result.getRow());
              byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
              String firstName = new String(firstNameObj);
              byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
              String lastName = new String(lastNameObj);
              System.out.println(firstName + " " + lastName + " - ID: " + id);
              byte[] emailObj = result.getValue(contactFamily, emailQualifier);
              String email = new String(emailObj);
              System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
            }
            results.close();
            table.close();
          }
        }

    O **SearchByEmail** classe pode ser utilizada para consultar linhas por endereço de correio eletrónico. Porque utiliza um filtro de expressão regular, pode fornecer uma cadeia ou uma expressão regular quando utilizar a classe.
5. Guardar o **SearchByEmail.java** ficheiro.
6. No **hbaseapp\src\main\hava\com\microsoft\examples** directory, crie um novo ficheiro designado **DeleteTable.java**. Utilize o seguinte código como o conteúdo deste ficheiro:

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;

        public class DeleteTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // Disable, and then delete the table
            admin.disableTable("people");
            admin.deleteTable("people");
          }
        }

    Esta classe é para a limpeza neste exemplo, desativando e remover a tabela criada pelo **CreateTable** classe.
7. Guardar o **DeleteTable.java** ficheiro.

## <a name="build-and-package-the-application"></a>Criar e a aplicação do pacote
1. Abra uma linha de comandos e altere os diretórios para o **hbaseapp** diretório.
2. Utilize o seguinte comando para criar um ficheiro JAR que contém a aplicação:

        mvn clean package

    Isto cleans quaisquer artefactos de compilação anterior, transfere quaisquer dependências que já não tenham sido instaladas, em seguida, baseia-se e pacotes a aplicação.
3. Quando o comando for concluído, o **hbaseapp\target** diretório contém um ficheiro denominado **hbaseapp-1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > O **hbaseapp-1.0-SNAPSHOT.jar** ficheiro é um uber jar (por vezes denominada uma jar fat,) que contém todas as dependências necessárias para executar a aplicação.

## <a name="upload-the-jar-file-and-start-a-job"></a>Carregar o ficheiro JAR e iniciar uma tarefa
Existem várias formas para carregar um ficheiro ao cluster do HDInsight, conforme descrito em [carregar dados para tarefas do Hadoop no HDInsight](hdinsight-upload-data.md). Os seguintes passos utilizam o Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Depois de instalar e configurar o Azure PowerShell, crie um novo ficheiro designado **hbase runner.psm1**. Utilize o seguinte como o conteúdo deste ficheiro:

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
        .EXAMPLE
        Start-HBaseExample -className "com.microsoft.examples.CreateTable"
        -clusterName "MyHDInsightCluster"

        .EXAMPLE
        Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
        -clusterName "MyHDInsightCluster"
        -emailRegex "contoso.com"

        .EXAMPLE
        Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
        -clusterName "MyHDInsightCluster"
        -emailRegex "^r" -showErr
        #>

        function Start-HBaseExample {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
        #The class to run
        [Parameter(Mandatory = $true)]
        [String]$className,

        #The name of the HDInsight cluster
        [Parameter(Mandatory = $true)]
        [String]$clusterName,

        #Only used when using SearchByEmail
        [Parameter(Mandatory = $false)]
        [String]$emailRegex,

        #Use if you want to see stderr output
        [Parameter(Mandatory = $false)]
        [Switch]$showErr
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get the login for the HDInsight cluster
        $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

        # The JAR
        $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

        # The job definition
        $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
            -JarFile $jarFile `
            -ClassName $className `
            -Arguments $emailRegex

        # Get the job output
        $job = Start-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobDefinition $jobDefinition `
            -HttpCredential $creds
        Write-Host "Wait for the job to complete ..." -ForegroundColor Green
        Wait-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobId $job.JobId `
            -HttpCredential $creds
        if($showErr)
        {
        Write-Host "STDERR"
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds `
                    -DisplayOutputType StandardError
        }
        Write-Host "Display the standard output ..." -ForegroundColor Green
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds
        }

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
        .EXAMPLE
        Add-HDInsightFile -localPath "C:\temp\data.txt"
        -destinationPath "example/data/data.txt"
        -ClusterName "MyHDInsightCluster"
        .EXAMPLE
        Add-HDInsightFile -localPath "C:\temp\data.txt"
        -destinationPath "example/data/data.txt"
        -ClusterName "MyHDInsightCluster"
        -Container "MyContainer"
        #>

        function Add-HDInsightFile {
            [CmdletBinding(SupportsShouldProcess = $true)]
            param(
                #The path to the local file.
                [Parameter(Mandatory = $true)]
                [String]$localPath,

                #The destination path and file name, relative to the root of the container.
                [Parameter(Mandatory = $true)]
                [String]$destinationPath,

                #The name of the HDInsight cluster
                [Parameter(Mandatory = $true)]
                [String]$clusterName,

                #If specified, overwrites existing files without prompting
                [Parameter(Mandatory = $false)]
                [Switch]$force
            )

            Set-StrictMode -Version 3

            # Is the Azure module installed?
            FindAzure

            # Get authentication for the cluster
            $creds=Get-Credential

            # Does the local path exist?
            if (-not (Test-Path $localPath))
            {
                throw "Source path '$localPath' does not exist."
            }

            # Get the primary storage container
            $storage = GetStorage -clusterName $clusterName

            # Upload file to storage, overwriting existing files if -force was used.
            Set-AzureStorageBlobContent -File $localPath `
                -Blob $destinationPath `
                -force:$force `
                -Container $storage.container `
                -Context $storage.context
        }

        function FindAzure {
            # Is there an active Azure subscription?
            $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
            if(-not($sub))
            {
                throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
            }
        }

        function GetStorage {
            param(
                [Parameter(Mandatory = $true)]
                [String]$clusterName
            )
            $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
            # Does the cluster exist?
            if (!$hdi)
            {
                throw "HDInsight cluster '$clusterName' does not exist."
            }
            # Create a return object for context & container
            $return = @{}
            $storageAccounts = @{}

            # Get storage information
            $resourceGroup = $hdi.ResourceGroup
            $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
            $container=$hdi.DefaultStorageContainer
            $storageAccountKey=(Get-AzureRmStorageAccountKey `
                -Name $storageAccountName `
            -ResourceGroupName $resourceGroup)[0].Value
            # Get the resource group, in case we need that
            $return.resourceGroup = $resourceGroup
            # Get the storage context, as we can't depend
            # on using the default storage context
            $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
            # Get the container, so we know where to
            # find/store blobs
            $return.container = $container
            # Return storage accounts to support finding all accounts for
            # a cluster
            $return.storageAccount = $storageAccountName
            $return.storageAccountKey = $storageAccountKey

            return $return
        }
        # Only export the verb-phrase things
        export-modulemember *-*

    Este ficheiro contém dois módulos:

   * **HDInsightFile adicionar** - utilizado para carregar ficheiros para o HDInsight
   * **Início HBaseExample** - utilizada para executar as classes que criou anteriormente
2. Guardar o **hbase runner.psm1** ficheiro.
3. Abra uma nova janela do PowerShell do Azure, altere os diretórios para o **hbaseapp** diretório e, em seguida, execute o seguinte comando.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Altere o caminho para a localização do **hbase runner.psm1** ficheiro criado anteriormente. Este procedimento regista o módulo para esta sessão do Azure PowerShell.
4. Utilize o seguinte comando para carregar o **hbaseapp-1.0-SNAPSHOT.jar** ao cluster do HDInsight.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Substitua **hdinsightclustername** com o nome do cluster do HDInsight. O comando carrega o **hbaseapp-1.0-SNAPSHOT.jar** para o **exemplo/v7** localização no armazenamento do primário para o seu cluster HDInsight.
5. Depois dos ficheiros são carregados, utilize o seguinte código para criar uma tabela utilizando o **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Substitua **hdinsightclustername** com o nome do cluster do HDInsight.

    Este comando cria uma nova tabela com o nome **pessoas** no cluster do HDInsight. Este comando não mostra resultados na janela da consola.
6. Para procurar entradas na tabela, utilize o seguinte comando:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Substitua **hdinsightclustername** com o nome do cluster do HDInsight.

    Este comando utiliza o **SearchByEmail** classe para pesquisar as linhas em que o **contactinformation** família de colunas e a **e-mail** coluna, contém a cadeia **contoso.com**. Deverá receber os seguintes resultados:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Utilizar **fabrikam.com** para o `-emailRegex` valor devolve os utilizadores que tenham **fabrikam.com** no campo do e-mail. Uma vez que esta pesquisa é implementada utilizando um filtro baseadas em expressões regular, também pode introduzir expressões regulares, tais como **^ r**, as entradas de devolve onde o e-mail começa com a letra "r".

## <a name="delete-the-table"></a>Eliminar a tabela
Quando tiver terminado com o exemplo, utilize o seguinte comando da sessão do PowerShell do Azure para eliminar o **pessoas** tabela utilizada neste exemplo:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Substitua **hdinsightclustername** com o nome do cluster do HDInsight.

## <a name="troubleshooting"></a>Resolução de problemas
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Não existem resultados ou resultados inesperados quando utilizar HBaseExample de início
Utilize o `-showErr` parâmetro para ver o erro padrão (STDERR) que é produzido ao executar a tarefa.
