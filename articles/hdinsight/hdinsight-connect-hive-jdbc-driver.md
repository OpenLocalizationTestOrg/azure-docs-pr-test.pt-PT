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
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="40100-104">Consulta do Hive através de controlador JDBC Olá no HDInsight</span><span class="sxs-lookup"><span data-stu-id="40100-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="40100-105">Saiba como o controlador JDBC Olá toouse de um toosubmit de aplicação Java Hive consulta tooHadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="40100-106">informações de Olá neste documento demonstra como tooconnect através de programação e Olá SQuirrel cliente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40100-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="40100-107">Para obter mais informações sobre Olá Interface de JDBC do Hive, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="40100-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40100-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="40100-108">Prerequisites</span></span>

* <span data-ttu-id="40100-109">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="40100-110">Os clusters baseados em Linux ou baseados em Windows de trabalho.</span><span class="sxs-lookup"><span data-stu-id="40100-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="40100-111">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="40100-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="40100-112">Para obter mais informações, consulte [HDInsight 3.3 extinção](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="40100-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="40100-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="40100-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="40100-114">SQuirreL é uma aplicação de cliente JDBC.</span><span class="sxs-lookup"><span data-stu-id="40100-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="40100-115">Olá [Java Developer Kit (JDK) versão 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="40100-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="40100-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="40100-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="40100-117">Maven é um projeto construir o sistema para projetos de Java que é utilizado pelo projeto Olá associado a este artigo.</span><span class="sxs-lookup"><span data-stu-id="40100-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="40100-118">Cadeia de ligação JDBC</span><span class="sxs-lookup"><span data-stu-id="40100-118">JDBC connection string</span></span>

<span data-ttu-id="40100-119">Cluster do HDInsight JDBC ligações tooan no Azure são efetuados mais 443 e tráfego de Olá está protegido por SSL.</span><span class="sxs-lookup"><span data-stu-id="40100-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="40100-120">gateway de público Olá que clusters Olá manter-se por trás redireciona Olá tráfego toohello porta que HiveServer2 é, na verdade, está a escutar.</span><span class="sxs-lookup"><span data-stu-id="40100-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="40100-121">Olá segue-se uma cadeia de ligação de exemplo:</span><span class="sxs-lookup"><span data-stu-id="40100-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="40100-122">Substitua `CLUSTERNAME` com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="40100-123">Autenticação</span><span class="sxs-lookup"><span data-stu-id="40100-123">Authentication</span></span>

<span data-ttu-id="40100-124">Ao estabelecer a ligação de Olá, tem de utilizar Olá HDInsight cluster admin nome e palavra-passe tooauthenticate toohello cluster gateway.</span><span class="sxs-lookup"><span data-stu-id="40100-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="40100-125">Quando ligar a partir de clientes JDBC, tais como o SQuirreL SQL, tem de introduzir Olá admin nome e uma palavra-passe nas definições do cliente.</span><span class="sxs-lookup"><span data-stu-id="40100-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="40100-126">A partir de uma aplicação Java, tem de utilizar Olá nome e uma palavra-passe ao estabelecer uma ligação.</span><span class="sxs-lookup"><span data-stu-id="40100-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="40100-127">Por exemplo, hello seguinte código Java abre uma nova ligação com a cadeia de ligação de Olá, admin nome e palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="40100-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="40100-128">Estabelecer ligação com o cliente SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="40100-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="40100-129">SQuirreL SQL é um cliente JDBC que pode ser tooremotely utilizados, executar consultas de ramo de registo com o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="40100-130">Olá passos partem do princípio de que já tiver instalado o SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="40100-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="40100-131">Copie controladores de ramo de registo JDBC Olá do seu cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="40100-132">Para **HDInsight baseado em Linux**, ficheiros de jar toodownload Olá necessário os passos de seguinte Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="40100-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="40100-133">Crie um diretório que contém ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="40100-134">Por exemplo, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="40100-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="40100-135">Numa linha de comandos, utilize seguinte de Olá comandos ficheiros de Olá toocopy do cluster do HDInsight Olá:</span><span class="sxs-lookup"><span data-stu-id="40100-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="40100-136">Substitua `USERNAME` com o nome da conta de utilizador SSH de Olá de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="40100-137">Substitua `CLUSTERNAME` com o nome de cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="40100-138">Para **HDInsight baseado em Windows**, utilize seguinte de Olá passos ficheiros do toodownload Olá jar.</span><span class="sxs-lookup"><span data-stu-id="40100-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="40100-139">Olá portal do Azure, selecione o cluster do HDInsight e, em seguida, selecione Olá **ambiente de trabalho remoto** ícone.</span><span class="sxs-lookup"><span data-stu-id="40100-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Ícone de ambiente de trabalho remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="40100-141">No painel de ambiente de trabalho remoto Olá, utilize Olá **Connect** cluster do botão tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="40100-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="40100-142">Se não estiver ativada Olá ambiente de trabalho remoto, utilize Olá formulário tooprovide um nome de utilizador e palavra-passe, em seguida, selecione **ativar** tooenable ambiente de trabalho remoto para o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Painel de ambiente de trabalho remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="40100-144">Depois de selecionar **Connect**, será transferido um ficheiro. rdp.</span><span class="sxs-lookup"><span data-stu-id="40100-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="40100-145">Utilize o cliente do ambiente de trabalho remoto toolaunch Olá este ficheiro.</span><span class="sxs-lookup"><span data-stu-id="40100-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="40100-146">Quando lhe for pedido, utilize o nome de utilizador de Olá e a palavra-passe que introduziu para acesso de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="40100-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="40100-147">Assim que estiver ligado, copie os seguintes ficheiros do computador local de tooyour sessão de ambiente de trabalho remoto Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="40100-148">Colocá-los num diretório local com o nome `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="40100-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="40100-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-JDBC-0.14.0.2.2.9.1-7-Standalone.JAR</span><span class="sxs-lookup"><span data-stu-id="40100-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="40100-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.JAR</span><span class="sxs-lookup"><span data-stu-id="40100-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="40100-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.JAR</span><span class="sxs-lookup"><span data-stu-id="40100-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="40100-152">versão de Olá números incluídos nos nomes de ficheiros e caminhos de Olá poderão ser diferentes para o cluster.</span><span class="sxs-lookup"><span data-stu-id="40100-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="40100-153">Desliga a sessão de ambiente de trabalho remoto de Olá assim que tiver concluído a copiar ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="40100-154">Inicie a aplicação de SQuirreL SQL Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="40100-155">Da esquerda Olá da janela de Olá, selecione **controladores**.</span><span class="sxs-lookup"><span data-stu-id="40100-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Separador de controladores no Olá esquerdo da janela de Olá](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="40100-157">Partir dos ícones Olá, Olá parte superior do Olá **controladores** caixa de diálogo, selecione de Olá  **+**  ícone toocreate um controlador.</span><span class="sxs-lookup"><span data-stu-id="40100-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Ícones de controladores](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="40100-159">Na caixa de diálogo do Olá Adicionar controlador, adicione Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="40100-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="40100-160">**Nome**: ramo de registo</span><span class="sxs-lookup"><span data-stu-id="40100-160">**Name**: Hive</span></span>
    * <span data-ttu-id="40100-161">**URL do exemplo**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="40100-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="40100-162">**Caminho de classe extra**: Utilize Olá adicionar botão tooadd Olá jar os ficheiros transferidos anteriormente</span><span class="sxs-lookup"><span data-stu-id="40100-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="40100-163">**Nome de classe**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="40100-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![controlador caixa de diálogo Adicionar](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="40100-165">Clique em **OK** toosave estas definições.</span><span class="sxs-lookup"><span data-stu-id="40100-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="40100-166">No lado esquerdo de Olá da janela de SQuirreL SQL Olá, selecione **Aliases**.</span><span class="sxs-lookup"><span data-stu-id="40100-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="40100-167">Em seguida, clique em Olá  **+**  ícone toocreate um alias de ligação.</span><span class="sxs-lookup"><span data-stu-id="40100-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![Adicionar novo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="40100-169">Os valores seguintes Olá de utilização para Olá **adicionar Alias** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40100-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="40100-170">**Nome**: Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="40100-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="40100-171">**Controlador**: Olá do utilize Olá pendente tooselect **Hive** controlador</span><span class="sxs-lookup"><span data-stu-id="40100-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="40100-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="40100-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="40100-173">Substitua **CLUSTERNAME** com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="40100-174">**Nome de utilizador**: nome da conta de início de sessão de cluster de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="40100-175">predefinição de Olá é `admin`.</span><span class="sxs-lookup"><span data-stu-id="40100-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="40100-176">**Palavra-passe**: Olá palavra-passe da conta de início de sessão do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-176">**Password**: hello password for hello cluster login account.</span></span>

 ![alias caixa de diálogo Adicionar](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="40100-178">Olá utilize **teste** tooverify botão que Olá funciona de ligação.</span><span class="sxs-lookup"><span data-stu-id="40100-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="40100-179">Quando **ligar à: Hive no HDInsight** é apresentada a caixa de diálogo, selecione **Connect** teste de Olá tooperform.</span><span class="sxs-lookup"><span data-stu-id="40100-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="40100-180">Se o teste de Olá for bem sucedida, verá um **ligação com êxito** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40100-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="40100-181">ligação de Olá toosave alias, utilize Olá **Ok** botão na parte inferior de Olá de Olá **adicionar Alias** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40100-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="40100-182">De Olá **ligar ao** lista pendente, Olá parte superior do SQuirreL SQL, selecione **do Hive no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="40100-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="40100-183">Quando lhe for pedido, selecione **Connect**.</span><span class="sxs-lookup"><span data-stu-id="40100-183">When prompted, select **Connect**.</span></span>

    ![caixa de diálogo de ligação](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="40100-185">Assim que estiver ligado, introduza Olá consulta na caixa de diálogo de consulta SQL de Olá a seguir e, em seguida, selecione Olá **executar** ícone.</span><span class="sxs-lookup"><span data-stu-id="40100-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="40100-186">área de resultados de Olá deve mostrar Olá os resultados da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![diálogo de consulta de SQL, incluindo os resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="40100-188">Ligar a partir de um exemplo de aplicação Java</span><span class="sxs-lookup"><span data-stu-id="40100-188">Connect from an example Java application</span></span>

<span data-ttu-id="40100-189">Um exemplo de utilização de um tooquery de cliente de Java do Hive no HDInsight está disponível em [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="40100-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="40100-190">Siga as instruções de Olá Olá repositório toobuild e execute o exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="40100-191">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="40100-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="40100-192">Erro inesperado Ocorreu tooopen tentar uma ligação de SQL</span><span class="sxs-lookup"><span data-stu-id="40100-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="40100-193">**Sintomas**: ao estabelecer a ligação de cluster do HDInsight tooan que é a versão 3.3 ou 3.4, poderá receber um erro que ocorreu um erro inesperado.</span><span class="sxs-lookup"><span data-stu-id="40100-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="40100-194">rastreio de pilha Olá para este erro começa com Olá seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="40100-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="40100-195">**Causa**: Este erro é causado por um erro de correspondência na versão Olá Olá commons codec.jar ficheiro utilizado pelo SQuirreL e Olá um necessários pelos componentes do ramo de registo JDBC Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="40100-196">**Resolução**: toofix este erro, Olá utilize os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="40100-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="40100-197">Transferir o ficheiro de jar de commons codec de Olá do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="40100-198">Sair SQuirreL e, em seguida, visite toohello diretório onde o SQuirreL está instalado no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="40100-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="40100-199">No diretório de SquirreL Olá, sob Olá `lib` diretório, substituir Olá existente commons-codec.jar com Olá um transferido a partir do cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="40100-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="40100-200">Reinicie o SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="40100-200">Restart SQuirreL.</span></span> <span data-ttu-id="40100-201">Erro de Olá já não deve ocorrer quando a ligação tooHive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40100-202">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="40100-202">Next steps</span></span>

<span data-ttu-id="40100-203">Agora que aprendeu como toouse JDBC toowork com o Hive, Olá de utilização seguintes hiperligações tooexplore toowork outras formas com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40100-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="40100-204">Carregar dados tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="40100-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="40100-205">Utilizar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="40100-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="40100-206">Utilizar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="40100-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="40100-207">Utilizar tarefas de MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="40100-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
