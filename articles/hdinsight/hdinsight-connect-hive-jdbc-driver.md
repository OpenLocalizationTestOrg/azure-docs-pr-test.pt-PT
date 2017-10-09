---
title: "aaaQuery do Hive através do controlador JDBC Olá - Azure HDInsight | Microsoft Docs"
description: "Utilize o controlador JDBC Olá de um tooHadoop de consultas do Hive de toosubmit de aplicação de Java no HDInsight. Liga através de programação e de cliente de SQuirrel SQL Olá."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Consulta do Hive através de controlador JDBC Olá no HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Saiba como o controlador JDBC Olá toouse de um toosubmit de aplicação Java Hive consulta tooHadoop no Azure HDInsight. informações de Olá neste documento demonstra como tooconnect através de programação e Olá SQuirrel cliente do SQL Server.

Para obter mais informações sobre Olá Interface de JDBC do Hive, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Pré-requisitos

* Um Hadoop no cluster do HDInsight. Os clusters baseados em Linux ou baseados em Windows de trabalho.

  > [!IMPORTANT]
  > Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, consulte [HDInsight 3.3 extinção](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL é uma aplicação de cliente JDBC.

* Olá [Java Developer Kit (JDK) versão 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.

* [Apache Maven](https://maven.apache.org). Maven é um projeto construir o sistema para projetos de Java que é utilizado pelo projeto Olá associado a este artigo.

## <a name="jdbc-connection-string"></a>Cadeia de ligação JDBC

Cluster do HDInsight JDBC ligações tooan no Azure são efetuados mais 443 e tráfego de Olá está protegido por SSL. gateway de público Olá que clusters Olá manter-se por trás redireciona Olá tráfego toohello porta que HiveServer2 é, na verdade, está a escutar. Olá segue-se uma cadeia de ligação de exemplo:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Substitua `CLUSTERNAME` com o nome de Olá de cluster do HDInsight.

## <a name="authentication"></a>Autenticação

Ao estabelecer a ligação de Olá, tem de utilizar Olá HDInsight cluster admin nome e palavra-passe tooauthenticate toohello cluster gateway. Quando ligar a partir de clientes JDBC, tais como o SQuirreL SQL, tem de introduzir Olá admin nome e uma palavra-passe nas definições do cliente.

A partir de uma aplicação Java, tem de utilizar Olá nome e uma palavra-passe ao estabelecer uma ligação. Por exemplo, hello seguinte código Java abre uma nova ligação com a cadeia de ligação de Olá, admin nome e palavra-passe:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Estabelecer ligação com o cliente SQuirreL SQL

SQuirreL SQL é um cliente JDBC que pode ser tooremotely utilizados, executar consultas de ramo de registo com o cluster do HDInsight. Olá passos partem do princípio de que já tiver instalado o SQuirreL SQL.

1. Copie controladores de ramo de registo JDBC Olá do seu cluster do HDInsight.

    * Para **HDInsight baseado em Linux**, ficheiros de jar toodownload Olá necessário os passos de seguinte Olá de utilização.

        1. Crie um diretório que contém ficheiros de Olá. Por exemplo, `mkdir hivedriver`.

        2. Numa linha de comandos, utilize seguinte de Olá comandos ficheiros de Olá toocopy do cluster do HDInsight Olá:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Substitua `USERNAME` com o nome da conta de utilizador SSH de Olá de cluster Olá. Substitua `CLUSTERNAME` com o nome de cluster do HDInsight Olá.

    * Para **HDInsight baseado em Windows**, utilize seguinte de Olá passos ficheiros do toodownload Olá jar.

        1. Olá portal do Azure, selecione o cluster do HDInsight e, em seguida, selecione Olá **ambiente de trabalho remoto** ícone.

            ![Ícone de ambiente de trabalho remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. No painel de ambiente de trabalho remoto Olá, utilize Olá **Connect** cluster do botão tooconnect toohello. Se não estiver ativada Olá ambiente de trabalho remoto, utilize Olá formulário tooprovide um nome de utilizador e palavra-passe, em seguida, selecione **ativar** tooenable ambiente de trabalho remoto para o cluster de Olá.

            ![Painel de ambiente de trabalho remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Depois de selecionar **Connect**, será transferido um ficheiro. rdp. Utilize o cliente do ambiente de trabalho remoto toolaunch Olá este ficheiro. Quando lhe for pedido, utilize o nome de utilizador de Olá e a palavra-passe que introduziu para acesso de ambiente de trabalho remoto.

        3. Assim que estiver ligado, copie os seguintes ficheiros do computador local de tooyour sessão de ambiente de trabalho remoto Olá de Olá. Colocá-los num diretório local com o nome `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-JDBC-0.14.0.2.2.9.1-7-Standalone.JAR
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.JAR
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.JAR

            > [!NOTE]
            > versão de Olá números incluídos nos nomes de ficheiros e caminhos de Olá poderão ser diferentes para o cluster.

        4. Desliga a sessão de ambiente de trabalho remoto de Olá assim que tiver concluído a copiar ficheiros de Olá.

2. Inicie a aplicação de SQuirreL SQL Olá. Da esquerda Olá da janela de Olá, selecione **controladores**.

    ![Separador de controladores no Olá esquerdo da janela de Olá](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Partir dos ícones Olá, Olá parte superior do Olá **controladores** caixa de diálogo, selecione de Olá  **+**  ícone toocreate um controlador.

    ![Ícones de controladores](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. Na caixa de diálogo do Olá Adicionar controlador, adicione Olá seguintes informações:

    * **Nome**: ramo de registo
    * **URL do exemplo**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Caminho de classe extra**: Utilize Olá adicionar botão tooadd Olá jar os ficheiros transferidos anteriormente
    * **Nome de classe**: org.apache.hive.jdbc.HiveDriver

   ![controlador caixa de diálogo Adicionar](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Clique em **OK** toosave estas definições.

5. No lado esquerdo de Olá da janela de SQuirreL SQL Olá, selecione **Aliases**. Em seguida, clique em Olá  **+**  ícone toocreate um alias de ligação.

    ![Adicionar novo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Os valores seguintes Olá de utilização para Olá **adicionar Alias** caixa de diálogo.

    * **Nome**: Hive no HDInsight

    * **Controlador**: Olá do utilize Olá pendente tooselect **Hive** controlador

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Substitua **CLUSTERNAME** com o nome de Olá de cluster do HDInsight.

    * **Nome de utilizador**: nome da conta de início de sessão de cluster de Olá de cluster do HDInsight. predefinição de Olá é `admin`.

    * **Palavra-passe**: Olá palavra-passe da conta de início de sessão do cluster Olá.

 ![alias caixa de diálogo Adicionar](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Olá utilize **teste** tooverify botão que Olá funciona de ligação. Quando **ligar à: Hive no HDInsight** é apresentada a caixa de diálogo, selecione **Connect** teste de Olá tooperform. Se o teste de Olá for bem sucedida, verá um **ligação com êxito** caixa de diálogo.

    ligação de Olá toosave alias, utilize Olá **Ok** botão na parte inferior de Olá de Olá **adicionar Alias** caixa de diálogo.

7. De Olá **ligar ao** lista pendente, Olá parte superior do SQuirreL SQL, selecione **do Hive no HDInsight**. Quando lhe for pedido, selecione **Connect**.

    ![caixa de diálogo de ligação](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Assim que estiver ligado, introduza Olá consulta na caixa de diálogo de consulta SQL de Olá a seguir e, em seguida, selecione Olá **executar** ícone. área de resultados de Olá deve mostrar Olá os resultados da consulta de Olá.

        select * from hivesampletable limit 10;

    ![diálogo de consulta de SQL, incluindo os resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Ligar a partir de um exemplo de aplicação Java

Um exemplo de utilização de um tooquery de cliente de Java do Hive no HDInsight está disponível em [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Siga as instruções de Olá Olá repositório toobuild e execute o exemplo de Olá.

## <a name="troubleshooting"></a>Resolução de problemas

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Erro inesperado Ocorreu tooopen tentar uma ligação de SQL

**Sintomas**: ao estabelecer a ligação de cluster do HDInsight tooan que é a versão 3.3 ou 3.4, poderá receber um erro que ocorreu um erro inesperado. rastreio de pilha Olá para este erro começa com Olá seguintes linhas:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Causa**: Este erro é causado por um erro de correspondência na versão Olá Olá commons codec.jar ficheiro utilizado pelo SQuirreL e Olá um necessários pelos componentes do ramo de registo JDBC Olá.

**Resolução**: toofix este erro, Olá utilize os seguintes passos:

1. Transferir o ficheiro de jar de commons codec de Olá do cluster do HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Sair SQuirreL e, em seguida, visite toohello diretório onde o SQuirreL está instalado no seu sistema. No diretório de SquirreL Olá, sob Olá `lib` diretório, substituir Olá existente commons-codec.jar com Olá um transferido a partir do cluster do HDInsight Olá.

3. Reinicie o SQuirreL. Erro de Olá já não deve ocorrer quando a ligação tooHive no HDInsight.

## <a name="next-steps"></a>Passos seguintes

Agora que aprendeu como toouse JDBC toowork com o Hive, Olá de utilização seguintes hiperligações tooexplore toowork outras formas com o Azure HDInsight.

* [Carregar dados tooHDInsight](hdinsight-upload-data.md)
* [Utilizar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Utilizar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Utilizar tarefas de MapReduce com o HDInsight](hdinsight-use-mapreduce.md)
