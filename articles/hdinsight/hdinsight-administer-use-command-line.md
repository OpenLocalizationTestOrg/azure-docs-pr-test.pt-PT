---
title: clusters do Hadoop de aaaManage utilizando a CLI do Azure - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá Interface de linha de comandos do Azure toomanage Hadoop clusters no Azure HDInsight. Olá CLI do Azure funciona no Windows, Mac e Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Gerir clusters do Hadoop no HDInsight com Olá CLI do Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Saiba como toouse Olá [Interface de linha de comandos do Azure](../cli-install-nodejs.md) toomanage Hadoop clusters no Azure HDInsight. Olá CLI do Azure está implementada no Node.js. Pode ser utilizado em qualquer plataforma que suporte Node.js, incluindo Windows, Mac e Linux.

Este artigo abrange apenas a utilização Olá CLI do Azure com o HDInsight. Para obter um guia Geral sobre como toouse CLI do Azure, consulte [instalar e configurar a CLI do Azure][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, tem de ter o seguinte Olá:

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **CLI do Azure** -consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) para obter informações de instalação e configuração.
* **Ligar tooAzure**com Olá os seguintes comandos:
  
        azure login
  
    Para obter mais informações sobre a autenticação através de uma conta escolar ou profissional, consulte [ligar tooan subscrição do Azure a partir de Olá CLI do Azure](../xplat-cli-connect.md).
* **Modo do comutador toohello Azure Resource Manager**com Olá os seguintes comandos:
  
        azure config mode arm

tooget ajuda, utilize Olá **-h** mudar.  Por exemplo:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Criar clusters com Olá CLI
Consulte [criar clusters do HDInsight utilizando Olá CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Listar e mostrar os detalhes do cluster
Utilize Olá toolist de comandos a seguir e mostrar os detalhes do cluster:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Vista da linha de comandos da lista de cluster][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Eliminar clusters
Utilize Olá comando toodelete um cluster a seguir:

    azure hdinsight cluster delete <Cluster Name>

Também pode eliminar um cluster ao eliminar o grupo de recursos de Olá que contém o cluster de Olá. Tenha em atenção, esta ação irá eliminar todos os recursos de Olá no grupo de Olá, incluindo a conta do storage predefinida Olá.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Dimensionar clusters
Olá toochange tamanho de cluster do Hadoop:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Ativar/desativar o acesso HTTP para um cluster
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Ativar/desativar acesso RDP para um cluster
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu como tooperform diferentes HDInsight cluster tarefas administrativas. toolearn mais, consulte Olá seguintes artigos:

* [Administrar HDInsight utilizando Olá Portal do Azure][hdinsight-admin-portal]
* [Administrar HDInsight ao utilizar o Azure PowerShell][hdinsight-admin-powershell]
* [Get started with Azure HDInsight (Introdução ao Azure HDInsight)][hdinsight-get-started]
* [Como toouse Olá CLI do Azure][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Listar e Mostrar clusters"
