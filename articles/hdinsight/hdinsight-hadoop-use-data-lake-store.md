---
title: aaaUse Data Lake Store com o Hadoop no Azure HDInsight | Microsoft Docs
description: "Saiba como tooquery dados do Azure Data Lake Store e toostore resulta da sua análise."
keywords: "armazenamento de blobs, hdfs, dados estruturados, dados não estruturados, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Utilizar o Data Lake Store com clusters do Azure HDInsight

dados de tooanalyze no cluster do HDInsight, pode armazenar dados Olá está no [Storage do Azure](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), ou ambos. Ambas as opções de armazenamento permitem-lhe eliminar toosafely clusters do HDInsight que são utilizados para o cálculo sem que haja perda de dados do utilizador.

Neste artigo, ficará a saber como o Data Lake Store funciona com clusters do HDInsight. toolearn como funciona o Storage do Azure com clusters do HDInsight, consulte [clusters de utilizar o Storage do Azure com o Azure HDInsight](hdinsight-hadoop-use-blob-storage.md). Para obter mais informações sobre a criação de um cluster do HDInsight, veja [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Criar clusters do Hadoop no HDInsight).

> [!NOTE]
> O Data Lake Store é sempre acedido através de um canal seguro, pelo que não existe nenhum nome de esquema de sistema de ficheiros `adls`. Utiliza sempre `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Disponibilidades para clusters do HDInsight

O Hadoop suporta uma noção do sistema de ficheiros Olá predefinido. sistema de ficheiros Olá predefinido implica um esquema predefinido e à autoridade. Também pode ser caminhos relativos tooresolve utilizados. Durante o processo de criação de cluster de HDInsight Olá, pode especificar um contentor do blob no Storage do Azure como sistema de ficheiros Olá predefinido ou com o HDInsight 3.5 e versões mais recentes, pode selecionar o Storage do Azure ou do Azure Data Lake Store como sistema de ficheiros predefinido Olá com um algumas exceções. 

Os clusters do HDInsight podem utilizar o Data Lake Store de duas formas:

* Como armazenamento de predefinido Olá
* Como armazenamento adicional, com o Azure Storage Blob como armazenamento predefinido.

A partir de agora, apenas algumas das Olá HDInsight cluster utilizando o Data Lake Store como armazenamento de predefinido e contas de armazenamento adicional de suporte de tipos/versões:

| Tipo de cluster do HDInsight | Data Lake Store como armazenamento predefinido | Data Lake Store como armazenamento adicional| Notas |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight versão 3.6 | Sim | Sim | |
| HDInsight versão 3.5 | Sim | Sim | Com exceção de Olá do HBase|
| HDInsight versão 3.4 | Não | Sim | |
| HDInsight versão 3.3 | Não | Não | |
| HDInsight versão 3.2 | Não | Sim | |
| HDInsight Premium (escalão)| Não | Não | |
| Storm | | |Pode utilizar dados do Data Lake Store toowrite de uma topologia do Storm. Também pode utilizar o Data Lake Store para dados de referência que podem então ser lidos por uma topologia Storm.|

Utilizar o Data Lake Store como uma conta de armazenamento adicional não afetar o desempenho ou Olá capacidade tooread ou escrever tooAzure armazenamento do cluster de Olá.


## <a name="use-data-lake-store-as-default-storage"></a>Utilizar o Data Lake Store como armazenamento predefinido

Quando o HDInsight é implementado com o Data Lake Store, como armazenamento de predefinido, os ficheiros relacionados com o cluster de Olá são armazenados no Data Lake Store no Olá seguinte localização:

    adl://mydatalakestore/<cluster_root_path>/

onde `<cluster_root_path>` é Olá nome de uma pasta que cria no Data Lake Store. Ao especificar um caminho de raiz para cada cluster, pode utilizar Olá a mesma conta de Data Lake Store para mais de um cluster. Por isso, pode ter uma configuração em que:

* Cluster1 pode utilizar o caminho de Olá`adl://mydatalakestore/cluster1storage`
* Cluster2 pode utilizar o caminho de Olá`adl://mydatalakestore/cluster2storage`

Tenha em atenção que ambos Olá clusters utilize Olá mesma conta do Data Lake Store **mydatalakestore**. Cada cluster tem tooits acesso possui sistema de ficheiros de raiz no Data Lake Store. Olá experiência de implementação no portal do Azure em particular pede-lhe toouse um nome de pasta, tais como **/clusters/\<clustername >** para o caminho da raiz de Olá.

toobe toouse capaz de um arquivo Data Lake como armazenamento de predefinido, tem de conceder Olá serviço acesso principal toohello seguintes caminhos:

- raiz de conta de Data Lake Store Olá.  Por exemplo: adl://mydatalakestore/.
- pasta de Olá para todas as pastas de cluster.  Por exemplo: adl://mydatalakestore/clusters.
- pasta de Olá para cluster Olá.  Por exemplo: adl://mydatalakestore/clusters/cluster1storage.

Para obter mais informações sobre como criar o principal de serviço e conceder acesso, veja [Configurar o acesso ao arquivo do Data Lake Store](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Utilizar o Data Lake Store como armazenamento adicional

Pode utilizar o Data Lake Store como armazenamento adicional para o cluster de Olá bem. Nestes casos, o armazenamento de cluster de Olá predefinido pode ser um Blob de armazenamento do Azure ou uma conta de Data Lake Store. Se estiver a executar tarefas do HDInsight em relação a dados de Olá armazenados no Data Lake Store, como armazenamento adicional, tem de utilizar ficheiros de toohello Olá caminho completamente qualificado. Por exemplo:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Tenha em atenção que não existe nenhum **cluster_root_path** no URL de Olá agora. Isto acontece porque o Data Lake Store não é um armazenamento de predefinido neste caso, pelo que tudo o que precisa toodo é fornecer Olá caminho toohello ficheiros.

toobe toouse capaz de um arquivo Data Lake como armazenamento adicional, o pode precisa apenas de toogrant Olá serviço acesso principal toohello caminhos onde estão armazenados os ficheiros.  Por exemplo:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Para obter mais informações sobre como criar o principal de serviço e conceder acesso, veja [Configurar o acesso ao arquivo do Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Utilizar mais de uma conta do Data Lake Store

Adicionar uma conta de Data Lake Store como adicionais e adicionar mais do que um Data Lake Store contas são conseguidas ao dar permissão ao cluster HDInsight Olá nos dados de contas de Data Lake Store um orar mais. Veja [Configurar o acesso ao Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurar o acesso ao arquivo do Data Lake Store

tooconfigure acesso de arquivo Data Lake do cluster do HDInsight, tem de ter um principal de serviço (Azure AD) de diretório Active Directory do Azure. Apenas um administrador do Azure AD pode criar um principal de serviço. o principal de serviço Olá tem de ser criado com um certificado. Para obter mais informações, veja [Configurar o acesso ao Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) e [Criar um principal de serviço com certificado autoassinado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Se pretender toouse Azure Data Lake Store como armazenamento adicional para o cluster do HDInsight, recomendamos vivamente que fazê-lo ao criar o cluster Olá, tal como descrito neste artigo. A adição de Azure Data Lake Store como armazenamento adicional tooan o cluster do HDInsight existente é um processo mais complicado e tooerrors suscetíveis.
>

## <a name="access-files-from-hello-cluster"></a>Acesso aos ficheiros do cluster de Olá

Existem várias formas de poder aceder a ficheiros de Olá no Data Lake Store de um cluster do HDInsight.

* **Com o nome completamente qualificado Olá**. Com esta abordagem, que fornece o ficheiro de toohello Olá caminho completo que pretende que o tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Utilizando o formato de caminho encurtado Olá**. Com esta abordagem, substitua caminho Olá toohello raiz de cluster de cópia de segurança com adl: / / /. Por isso, no exemplo de Olá acima, pode substituir `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` com `adl:///`.

        adl:///<file path>

* **Utilizar o caminho relativo Olá**. Com esta abordagem, fornecer apenas ficheiro de toohello Olá caminho relativo que pretende que o tooaccess. Por exemplo, se o ficheiro de toohello Olá caminho completo é:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Pode aceder ao hello do mesmo ficheiro sample.log utilizando este caminho relativo.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Criar clusters do HDInsight com acesso tooData Lake Store

Utilize Olá seguintes ligações para instruções detalhadas sobre como toocreate clusters do HDInsight com acesso tooData Lake Store.

* [Utilizar o Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [Utilizar o PowerShell (com o Data Lake Store como armazenamento predefinido)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Utilizar o PowerShell (com o Data Lake Store como armazenamento adicional)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Utilizar modelos do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu como toouse compatível com HDFS Azure Data Lake Store com o HDInsight. Isto permite-lhe toobuild dimensionável e de longa duração, arquivar soluções de aquisição de dados e a utilização HDInsight toounlock Olá informações Olá armazenado estruturadas e os dados não estruturados.

Para obter mais informações, consulte:

* [Get started with Azure HDInsight (Introdução ao Azure HDInsight)][hdinsight-get-started]
* [Introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Use Hive with HDInsight (Utilizar o Hive com o HDInsight)][hdinsight-use-hive]
* [Use Pig with HDInsight (Utilizar o Pig com o HDInsight)][hdinsight-use-pig]
* [Utilizar assinaturas de acesso partilhado do Azure armazenamento toorestrict acesso toodata com o HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
