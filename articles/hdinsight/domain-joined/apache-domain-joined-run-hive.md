---
title: "Configurar políticas de Hive no HDInsight associados a um domínio - Azure | Microsoft Docs"
description: Saiba mais...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 35a74ffb6a30fe2ae7db686be5b6774800ce37b1
ms.sourcegitcommit: 828cd4b47fbd7d7d620fbb93a592559256f9d234
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/18/2018
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight"></a>Configurar políticas de Hive no HDInsight associados a um domínio
Saiba como configurar políticas do Apache Ranger para o Hive. Neste artigo, irá criar duas políticas do Ranger para restringir o acesso a hivesampletable. O hivesampletable é fornecido com clusters do HDInsight. Após ter configurado as políticas, utilize o Excel e o controlador ODBC para estabelecer uma ligação a tabelas do Hive no HDInsight.

## <a name="prerequisites"></a>Pré-requisitos
* Um cluster do HDInsight associado a um domínio. Consulte [Configurar clusters do HDInsight associado a um Domínio](apache-domain-joined-configure.md).
* Uma estação de trabalho com o Office 2016, o Office 2013 Professional Plus, o Office 365 Pro Plus, o Excel 2013 Standalone ou o Office 2010 Professional Plus.

## <a name="connect-to-apache-ranger-admin-ui"></a>Ligar à IU do Apache Ranger Admin
**Para ligar à IU do Ranger Admin**

1. Num browser, ligue-se à IU do Ranger Admin. O URL é https://&lt;ClusterName>.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > O Ranger utiliza credenciais diferentes do que o cluster do Hadoop. Para impedir browsers utilizar credenciais em cache do Hadoop, utilize a nova janela do InPrivate browser para estabelecer a ligação para a IU do Admin Ranger.
   >
   >
2. Inicie sessão com o nome de utilizador e a palavra-passe do domínio do administrador do cluster:

    ![Home page do Ranger associada a um Domínio do HDInsight](./media/apache-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Atualmente, o Ranger só funciona com o Yarn e o Hive.

## <a name="create-domain-users"></a>Criar Utilizadores de domínio
Em [Configurar clusters do HDInsight associados a um Domínio](apache-domain-joined-configure.md#optional-create-ad-users-and-groups), criou o hiveruser1 e o hiveuser2. Utilize a conta de dois utilizador neste tutorial.

## <a name="create-ranger-policies"></a>Criar políticas do Ranger
Nesta secção, vai criar duas políticas Ranger para aceder ao hivesampletable. Conceda permissão selecionada em diferentes conjuntos de colunas. Ambos os utilizadores foram criados em [Configurar clusters do HDInsight associado a um Domínio](apache-domain-joined-configure.md#optional-create-ad-users-and-groups).  Na secção seguinte, irá testar as duas políticas no Excel.

**Para criar políticas do Ranger**

1. Abra a IU do Ranger Admin. Consulte [Ligar à IU do Apache Ranger Admin](#connect-to-apache-ranager-admin-ui).
2. Clique em **&lt;ClusterName >_hive**, em **Hive**. Deverá ver duas políticas de pré-configuração.
3. Clique em **Adicionar Nova Política**, e, em seguida, introduza os seguintes valores:

   * Nome da política: read-hivesampletable-all
   * Base de dados do Hive: predefinido
   * tabela: hivesampletable
   * Coluna do Hive: *
   * Selecione o Utilizador: hiveuser1
   * Permissões: selecionar

     ![Configuração da política do Hive do Ranger associada a um Domínio do HDInsight](./media/apache-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Se um utilizador de domínio não for povoado em Selecionar Utilizador, aguarde um momento enquanto o Ranger é sincronizado com o AAD.
     >
     >
4. Clique em **Adicionar** para guardar a política.
5. Repita os dois últimos passos para criar outra política com as seguintes propriedades:

   * Nome da política: read-hivesampletable-devicemake
   * Base de dados do Hive: predefinido
   * tabela: hivesampletable
   * Coluna do Hive: clientid, devicemake
   * Selecione o Utilizador: hiveuser2
   * Permissões: selecionar

## <a name="create-hive-odbc-data-source"></a>Criar a origem de dados do ODBC do Hive
As instruções podem ser encontradas em [Criar origem de dados do ODBC do Hive](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).  

 | Propriedade  |Descrição |
 | --- | --- |
 | Nome da Origem de Dados | Atribua um nome para a sua origem de dados |
 | Anfitrião | Introduza &lt;HDInsightClusterName>.azurehdinsight.net. Por exemplo, myHDICluster.azurehdinsight.net |
 | Porta | Utilize **443**. (Esta porta foi alterada de 563 para 443.) |
 | Base de Dados | Use **Predefinição**. |
 | Tipo de Servidor do Hive | Selecione **Servidor do Hive 2** |
 | Mecanismo | Selecione **Serviço do Azure HDInsight** |
 | Caminho HTTP | Deixe em branco. |
 | Nome de Utilizador | Introduza hiveuser1@contoso158.onmicrosoft.com. Se for diferente, atualize o nome de domínio. |
 | Palavra-passe | Introduza a palavra-passe para hiveuser1. |

Certifique-se de que clica em **Teste**, antes de guardar a origem de dados.

## <a name="import-data-into-excel-from-hdinsight"></a>Importe dados para o Excel a partir do HDInsight
Na última secção, configurou duas políticas.  O hiveuser1 tem a permissão de seleção em todas as colunas e o hiveuser2 tem a permissão de seleção em duas colunas. Nesta secção, representa os dois utilizadores para importar dados para o Excel.

1. Abra um livro novo ou existente no Excel.
2. No separador **Dados**, clique em **De Outras Origens de Dados** e, em seguida, clique em **Do Assistente de Ligação de Dados** para iniciar o **Assistente de Ligação de Dados**.

    ![Abrir assistente de ligação de dados][img-hdi-simbahiveodbc.excel.dataconnection]
3. Selecione **ODBC DSN** como a origem de dados e, em seguida, clique em **Seguinte**.
4. Nas origens de dados do ODBC, selecione o nome da origem de dados que criou no passo anterior e, em seguida, clique em **Seguinte**.
5. Reintroduza a palavra-passe para o cluster no assistente e, em seguida, clique em **OK**. Aguarde que a caixa de diálogo **Selecionar Base de Dados e Tabela** se abra. Esta ação pode demorar alguns segundos.
6. Selecione **hivesampletable** e, em seguida, clique em **Seguinte**.
7. Clique em **Concluir**.
8. Na caixa de diálogo **Importar Dados**, pode alterar ou especificar a consulta. Para o fazer, clique em **Propriedades**. Esta ação pode demorar alguns segundos.
9. Clique no separador **Definição**. O texto do comando é:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Através das políticas do Ranger que definiu, o hiveuser1 tem permissão de seleção em todas as colunas.  Por isso, esta consulta funciona com as credenciais do hiveuser1, mas esta consulta não funciona com as credenciais do hiveuser2.

   ![Propriedades da Ligação][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Clique em **OK** para fechar a caixa de diálogo Propriedades da Ligação.
11. Clique em **OK** para fechar a caixa de diálogo **Importar Dados**.  
12. Reintroduza a palavra-passe para hiveuser1 e clique em **OK**. Demora alguns segundos antes de os dados serem importados para o Excel. Quando estiver concluído, deverá ver 11 colunas de dados.

Para testar a política segundo (leitura-hivesampletable-devicemake), que criou na última secção

1. Adicione uma nova folha no Excel.
2. Siga o último procedimento para importar os dados.  É a única alteração que efetuar utilizar credenciais do hiveuser2 em vez do hiveuser1. Isto falhar porque hiveuser2 só tem permissão para ver duas colunas. Deve receber o erro seguinte:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Siga o mesmo procedimento para importar dados. Desta vez, utilize as credenciais do hiveuser2 e modifique a instrução de seleção de:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    para:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Quando estiver concluído, deverá ver duas colunas de dados importados.

## <a name="next-steps"></a>Passos Seguintes
* Para configurar um cluster do HDInsight associado a um domínio, veja [Configurar clusters do HDInsight associados a um domínio](apache-domain-joined-configure.md).
* Para gerir um cluster do HDInsight associados a um domínio, consulte [clusters do HDInsight associados a um domínio gerir](apache-domain-joined-manage.md).
* Para executar consultas do Hive com o SSH nos clusters do HDInsight associados a um domínio, consulte [utilizar o SSH com o HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Para Ligar o Hive com o JDBC do Hive, consulte [Connect to Hive on Azure HDInsight using the Hive JDBC driver (Ligar ao Hive no Azure HDInsight com o controlador JBDC do Hive)](../hadoop/apache-hadoop-connect-hive-jdbc-driver.md)
* Para ligar o Excel ao Hadoop com ODBC do Hive, consulte [Connect Excel to Hadoop with the Microsoft Hive ODBC drive (Ligar o Excel ao Hadoop com o controlador do ODBC do Microsoft Hive)](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md)
* Para ligar o Excel ao Hadoop com o Power Query, consulte [Connect Excel to Hadoop by using Power Query (Ligar o Excel ao Hadoop com o Power Query)](../hadoop/apache-hadoop-connect-excel-power-query.md)
