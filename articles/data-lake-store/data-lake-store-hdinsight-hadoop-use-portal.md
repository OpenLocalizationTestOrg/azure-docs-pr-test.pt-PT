---
title: "clusters aaaUse Olá toocreate do portal do Azure, Azure HDInsight com o Data Lake Store | Microsoft Docs"
description: "Utilizar Olá toocreate portal do Azure e utilizar clusters do HDInsight com o Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Criar clusters do HDInsight com o Data Lake Store utilizando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Utilizar Olá portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Utilize o PowerShell (para armazenamento de predefinido)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Utilize o PowerShell (para armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utilize o Gestor de recursos](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Saiba como toouse Olá toocreate portal do Azure um cluster do HDInsight com uma conta do Azure Data Lake Store como armazenamento de predefinido Olá ou um armazenamento adicional. Apesar de armazenamento adicional é opcional para um cluster do HDInsight, é recomendado toostore dados da sua empresa no Olá mais contas do storage.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, certifique-se de que cumpriu Olá os seguintes requisitos:

* **Uma subscrição do Azure**. Aceda demasiado[avaliação gratuita do Azure obter](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do Azure Data Lake Store**. Siga as instruções de Olá do [introdução ao Azure Data Lake Store utilizando o portal do Azure de Olá](data-lake-store-get-started-portal.md). Também tem de criar uma pasta raiz na conta de Olá.  Neste tutorial, uma pasta de raiz denominada __/clusters__ é utilizado.
* **Um principal de serviço do Azure Active Directory**. Este tutorial fornece instruções sobre como toocreate um principal de serviço no Azure Active Directory (Azure AD). No entanto, toocreate um principal de serviço, tem de ser um administrador do Azure AD. Se for um administrador, pode ignorar este pré-requisito e continue com tutorial de Olá.

    >[!NOTE]
    >Pode criar um serviço principal, apenas se for um administrador do Azure AD. O administrador do Azure AD tem de criar um serviço principal antes de poder criar um cluster do HDInsight com o Data Lake Store. Além disso, o principal de serviço Olá tem de ser criado com um certificado, conforme descrito em [criar um principal de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Criar um cluster do HDInsight

Nesta secção, criará um cluster do HDInsight com contas de Data Lake Store predefinida Olá ou armazenamento adicional Olá. Este artigo foca-se apenas Olá parte configurar contas de Data Lake Store.  Para informações de criação do cluster geral Olá e procedimentos, consulte [clusters do Hadoop criar no HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Criar um cluster com o Data Lake Store, como armazenamento de predefinido

**toocreate um HDInsight cluster com uma Data Lake Store, como a conta do storage predefinida Olá**

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Siga [criar clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) para obter informações gerais de Olá sobre a criação de clusters do HDInsight.
3. No Olá **armazenamento** painel, em **tipo de armazenamento primário**, selecione **Data Lake Store**e, em seguida, introduza Olá seguintes informações:

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "adicionar cluster de principal tooHDInsight do serviço")

    - **Conta Selecione Data Lake Store**: selecione uma conta existente do Data Lake Store. É necessária uma conta de Data Lake Store existente.  Consulte [pré-requisitos](#prereuisites).
    - **Caminho da raiz**: introduza um caminho de onde os ficheiros de cluster específicos Olá são toobe armazenado. Na captura de ecrã Olá, é __/clusters myhdiadlcluster/__, na qual Olá __/clusters__ pasta tem de existir hello Portal cria *myhdicluster* pasta.  Olá *myhdicluster* é o nome do cluster Olá.
    - **Acesso de data Lake Store**: configurar o acesso entre a conta de Data Lake Store Olá e cluster do HDInsight. Para obter instruções, consulte [acesso de configurar o Data Lake Store](#configure-data-lake-store-access).
    - **Contas de armazenamento adicional**: as contas de adicionar contas de armazenamento do Azure como armazenamento adicional do cluster de Olá. tooadd adicionais Lake os arquivos de dados é feito ao conceder permissões de cluster Olá nos dados de mais contas de Data Lake Store ao configurar a conta do Data Lake Store como tipo de armazenamento primário Olá. Veja [Configurar o acesso ao Data Lake Store](#configure-data-lake-store-access).

4. No Olá **acesso de Data Lake Store**, clique em **selecione**e, em seguida, continuar com a criação do cluster, conforme descrito em [clusters do Hadoop criar no HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Criar um cluster com o Data Lake Store, como armazenamento adicional

Olá instruções que se seguem criar um cluster do HDInsight com uma conta de armazenamento do Azure como armazenamento de predefinido Olá e uma conta de Data Lake Store, como um armazenamento adicional.
**toocreate um HDInsight cluster com uma Data Lake Store, como a conta do storage predefinida Olá**

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Siga [criar clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) para obter informações gerais de Olá sobre a criação de clusters do HDInsight.
3. No Olá **armazenamento** painel, em **tipo de armazenamento primário**, selecione **Storage do Azure**e, em seguida, introduza Olá seguintes informações:

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "adicionar cluster de principal tooHDInsight do serviço")

    - **Método de seleção**: Utilize um dos Olá seguintes opções:

        * toospecify uma conta de armazenamento que faz parte da sua subscrição do Azure, selecione **minhas subscrições**e, em seguida, selecione a conta de armazenamento Olá.
        * uma conta de armazenamento que está fora da sua subscrição do Azure, selecione de toospecify **chave de acesso**e, em seguida, fornecer informações de Olá para Olá fora da conta de armazenamento.

    - **Contentor predefinido**: Utilize o valor predefinido de Olá ou especifique o nome da sua própria.

    - Contas de armazenamento adicionais: adicione mais contas de armazenamento do Azure como armazenamento adicional Olá.
    - Acesso de data Lake Store: configurar o acesso entre a conta de Data Lake Store Olá e cluster do HDInsight. Para obter instruções, consulte [acesso de configurar o Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurar o acesso do Data Lake Store 

Nesta secção, configure o acesso de Data Lake Store de clusters do HDInsight através de um principal de serviço do Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Especifique um principal de serviço

De Olá portal do Azure, pode utilizar um principal de serviço existente ou crie um novo.

**toocreate um principal de serviço de Olá portal do Azure**

1. Clique em **acesso de Data Lake Store** a partir do painel de arquivo de Olá.
2. No Olá **acesso de Data Lake Store** painel, clique em **criar nova**.
3. Clique em **Principal de serviço**e, em seguida, siga as instruções de Olá toocreate um principal de serviço.
4. Transferir o certificado de Olá se decidir toouse-lo novamente na Olá futura. Transferir o certificado de Olá é útil que se pretender toouse Olá o mesmo serviço principal quando criar clusters do HDInsight adicionais.

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "adicionar cluster de principal tooHDInsight do serviço")

4. Clique em **acesso** acesso da pasta tooconfigure Olá.  Consulte [configurar permissões de ficheiro](#configure-file-permissions).


**toouse um principal de Olá portal do Azure de serviço existente**

1. Clique em **acesso de Data Lake Store**.
1. No Olá **acesso de Data Lake Store** painel, clique em **utilizar existente**.
2. Clique em **Principal de serviço**e, em seguida, selecione um principal de serviço. 
3. Carregar o certificado de Olá (ficheiro. pfx) que está associada a sua principal de serviço selecionado e, em seguida, introduza a palavra-passe de certificados de Olá.

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "adicionar cluster de principal tooHDInsight do serviço")

4. Clique em **acesso** acesso da pasta tooconfigure Olá.  Consulte [configurar permissões de ficheiro](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Configurar permissões de ficheiro

Olá configura são diferentes consoante se conta Olá é utilizada como armazenamento de predefinido Olá ou uma conta de armazenamento adicional:

- Utilizado como armazenamento de predefinido

    - permissão no nível de raiz de Olá de Olá conta do Data Lake Store
    - permissão no nível de raiz de Olá de Olá armazenamento de cluster do HDInsight. Por exemplo, Olá __/clusters__ pasta utilizada anteriormente no tutorial Olá.
- Utilizar como um armazenamento adicional

    - Permissão em pastas olá onde precisa de ficheiro acesso.

**permissão de tooassign em Olá nível de raiz de conta do Data Lake Store**

1. No Olá **acesso de Data Lake Store** painel, clique em **acesso**. Olá **Selecione as permissões do ficheiro** é aberto o painel. Lista todas as contas de Data Lake Store Olá na sua subscrição.
2. Paire o rato (não clique) rato Olá através de nome de Olá de Olá toomake Olá caixa de verificação visível, em seguida, selecione Olá caixa de verificação de conta de Data Lake Store.

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "adicionar cluster de principal tooHDInsight do serviço")

  Por predefinição, __ler__, __escrever__, AND __executar__ são todos os selecionados.

3. Clique em **selecione** no Olá parte inferior da página Olá.
4. Clique em **executar** tooassign permissão.
5. Clique em **Concluído**.

**permissão de tooassign em Olá nível de raiz de cluster do HDInsight**

1. No Olá **acesso de Data Lake Store** painel, clique em **acesso**. Olá **Selecione as permissões do ficheiro** é aberto o painel. Lista todas as contas de Data Lake Store Olá na sua subscrição.
1. De Olá **Selecione as permissões do ficheiro** painel, clique em tooshow de nome do Data Lake Store Olá respetivo conteúdo.
2. Selecione a raiz de armazenamento de cluster de HDInsight Olá, selecionando a caixa de verificação Olá esquerda Olá da pasta de Olá. De acordo com toohello captura de ecrã anterior, é de raiz de armazenamento de cluster Olá __/clusters__ pasta que especificou ao selecionar Olá Data Lake Store, como armazenamento de predefinido.
3. Definir permissões de Olá na pasta Olá.  Por predefinição, ler, escrever e executar são todos os selecionados.
4. Clique em **selecione** no Olá parte inferior da página Olá.
5. Clique em **Executar**.
6. Clique em **Concluído**.

Se estiver a utilizar o Data Lake Store como armazenamento adicional, tem de atribuir permissão apenas para pastas de Olá que pretende que o tooaccess do cluster do HDInsight Olá. Por exemplo, Olá captura de ecrã abaixo, deve fornecer acesso apenas demasiado**hdiaddonstorage** pasta numa conta do Data Lake Store.

![Atribuir o cluster de HDInsight do serviço principal permissões toohello](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "cluster do HDInsight toohello atribuir serviço permissões principal")


## <a name="verify-cluster-set-up"></a>Verifique a configuração de cluster

Após a conclusão da configuração do cluster Olá, no painel do cluster de Olá, certifique-se os seus resultados efetuando um ou ambos Olá os seguintes passos:

* tooverify que Olá armazenamento associado para o cluster de Olá é a conta de Data Lake Store Olá que especificou, clique em **contas do Storage** no painel esquerdo Olá.

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "adicionar cluster de principal tooHDInsight do serviço")

* tooverify Olá principal de serviço está corretamente associado ao cluster do HDInsight Olá, clique em **acesso de Data Lake Store** no painel esquerdo Olá.

    ![Cluster de principal tooHDInsight do serviço de adicionar](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "adicionar cluster de principal tooHDInsight do serviço")


## <a name="examples"></a>Exemplos

Após configurou o armazenamento do cluster de Olá com o Data Lake Store, consulte toothese os exemplos de como toouse HDInsight cluster dados de Olá tooanalyze armazenados no Data Lake Store.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Executar uma consulta do Hive contra dados num arquivo Data Lake (como armazenamento primário)

toorun uma consulta do Hive, utilizar a interface de vistas do Hive de Olá no portal do Olá Ambari. Para obter instruções sobre como vistas toouse Ambari Hive, consulte [Olá utilize vista do Hive com o Hadoop no HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Quando trabalha com dados de uma Data Lake Store, existem alguns toochange de cadeias.

Se utilizar, por exemplo, Olá cluster que criou com o Data Lake Store, como armazenamento primário, os dados de toohello do caminho de Olá são: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Um toocreate de consulta do Hive uma tabela a partir de dados de exemplo que estão armazenadas no Olá conta do Data Lake Store aspeto Olá a seguinte instrução:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Descrições:
* `adl://hdiadlstorage.azuredatalakestore.net/`é Olá raiz de Olá conta do Data Lake Store.
* `/clusters/myhdiadlcluster`é Olá raiz dos dados de cluster Olá que especificou ao criar o cluster de Olá.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`é Olá localização do ficheiro de exemplo de Olá que utilizou na consulta de Olá.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Executar uma consulta do Hive contra dados num arquivo Data Lake (como armazenamento adicional)

Se o cluster Olá que criou utiliza armazenamento de BLOBs, como armazenamento de predefinido, os dados de exemplo de Olá não estão contidos no Olá conta do Azure Data Lake Store que é utilizada como armazenamento adicional. Nesse caso, primeiro transferir dados Olá do Blob storage toohello Data Lake Store e, em seguida, executar consultas de Olá, conforme mostrado no Olá anterior exemplo.

Para obter informações sobre como toocopy do armazenamento de BLOBs tooa Data Lake do arquivo de dados, consulte Olá seguintes artigos:

* [Utilizar o Distcp toocopy dados entre os blobs de armazenamento do Azure e de Data Lake Store](data-lake-store-copy-data-wasb-distcp.md)
* [Utilizar AdlCopy toocopy dados do armazenamento do Azure blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Utilizar o Data Lake Store com um cluster do Spark
Pode utilizar um tarefas toorun Spark cluster Spark nos dados que são armazenados num arquivo Data Lake. Para obter mais informações, consulte [dados em utilizar o Spark do HDInsight cluster tooanalyze no Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Utilizar o Data Lake Store numa topologia de Storm
Pode utilizar dados de toowrite do Data Lake Store Olá de uma topologia do Storm. Para obter instruções sobre como tooachieve neste cenário, consulte [utilização do Azure Data Lake Store com Apache Storm com o HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Consultar também
* [PowerShell: Criar um toouse de cluster do HDInsight Data Lake Store](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
