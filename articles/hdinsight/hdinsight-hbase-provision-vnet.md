---
title: aaaCreate HBase clusters numa rede Virtual - Azure | Microsoft Docs
description: "Introdução ao hbase no Azure HDInsight. Saiba como clusters de toocreate HBase do HDInsight na Azure Virtual Network."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Criar clusters de HBase no HDInsight na Azure Virtual Network
Saiba como toocreate HBase do HDInsight Azure clusters num [Azure Virtual Network][1].

Com a integração de rede virtual, clusters de HBase podem ser implementado toohello mesmo virtual de rede como as suas aplicações, por isso, que aplicações podem comunicar diretamente com o HBase. Olá benefícios incluem:

* Ligação direta Olá web aplicação toohello nós Olá HBase cluster, que permite a comunicação através de procedimento remoto de HBase Java chamar APIs (RPC).
* Desempenho melhorado por não ter o tráfego aceda ao longo de vários gateways e Balanceadores de carga.
* Olá capacidade tooprocess informações confidenciais de forma mais segura sem a exposição de um ponto final público.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, tem de ter Olá seguintes itens:

* **Uma subscrição do Azure**. Consulte [Obter versão de avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Uma estação de trabalho com o Azure PowerShell**. Consulte [instalar e utilizar o Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Criar cluster HBase numa rede virtual
Nesta secção, cria um cluster HBase baseado em Linux com a conta do armazenamento do Azure dependente Olá uma rede virtual do Azure utilizando um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Para outros métodos de criação do cluster e compreender as definições de Olá, consulte [criar clusters do HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Para obter mais informações sobre como utilizar um modelo toocreate Hadoop clusters no HDInsight, consulte [clusters do Hadoop criar no HDInsight com modelos Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Algumas propriedades estão hard-coded para o modelo de Olá. Por exemplo:
>
> * **Localização**: EUA Leste 2
> * **Versão do cluster**: 3.5
> * **Número de nós de trabalho de cluster**: 2
> * **Conta de armazenamento de predefinido**: uma cadeia exclusiva
> * **Nome da rede virtual**: &lt;nome do Cluster >-vnet
> * **Espaço de endereços de rede virtual**: 10.0.0.0/16
> * **Nome da sub-rede**: subnet1
> * **Intervalo de endereços da sub-rede**: 10.0.0.0/24
>
> &lt;Nome do cluster > é substituído pelo nome do cluster Olá fornecer ao utilizar o modelo de Olá.
>
>

1. Clique em Olá seguinte imagem tooopen Olá o modelo de Olá portal do Azure. modelo de Olá está localizado num [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. De Olá **implementação personalizada** painel, introduza Olá seguintes propriedades:

   * **Subscrição**: selecione o cluster do HDInsight toocreate Olá uma subscrição do Azure utilizado, Olá conta do Storage dependente e Olá rede virtual do Azure.
   * **Grupo de recursos**: selecione **criar nova**e especifique um nome do novo grupo de recursos.
   * **Localização**: selecione uma localização para o grupo de recursos de Olá.
   * **ClusterName**: introduza um nome para toobe de cluster de Hadoop Olá criado.
   * **Nome de início de sessão e palavra-passe do cluster**: nome de início de sessão predefinido Olá é **admin**.
   * **Nome de utilizador do SSH e a palavra-passe**: é o nome de utilizador do Olá predefinido **sshuser**.  Pode alterá-lo.
   * **Concordo toohello termos e condições de Olá indicadas acima**: (selecionar)
3. Clique em **Comprar**. Demora cerca de 20 minutos toocreate um cluster. Depois de Olá cluster for criado, pode clicar em Painel de cluster Olá no tooopen portal Olá-lo.

Depois de concluir o tutorial Olá, pode querer cluster de Olá toodelete. Com o HDInsight, os dados são armazenados no Storage do Azure, pelo que pode eliminar um cluster em segurança quando este não está a ser utilizado. Também lhe é cobrado o valor de um cluster do HDInsight mesmo quando não o está a utilizar. Uma vez que os custos de Olá de cluster Olá são muitas vezes mais do que os custos de Olá de armazenamento, faz sentido em termos económicos toodelete clusters quando não estão em utilização. Para obter instruções de Olá da eliminação de um cluster, consulte [Olá de clusters de gerir Hadoop no HDInsight utilizando o portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

toobegin trabalhar com o novo cluster de HBase, pode utilizar os procedimentos de Olá encontrados no [introdução ao hbase com o Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Ligar o cluster de HBase toohello com APIs de RPC de Java de HBase
1. Criar uma infraestrutura como uma máquina virtual de serviço (IaaS) para Olá a mesma rede virtual do Azure e Olá mesma sub-rede. Para obter instruções sobre como criar uma nova máquina virtual de IaaS, consulte [criar uma Máquina Virtual a executar o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Quando os seguintes passos de Olá neste documento, tem de utilizar Olá os seguintes valores para a configuração de rede Olá:

   * **Rede virtual**: &lt;nome do Cluster >-vnet
   * **Sub-rede**: subnet1

   > [!IMPORTANT]
   > Substitua &lt;nome do Cluster > com o nome de Olá utilizado ao criar o cluster do HDInsight Olá nos passos anteriores.
   >
   >

   Utilizar estes valores, Olá máquina virtual está colocada em Olá mesma rede virtual e sub-rede que o cluster do HDInsight Olá. Esta configuração permite-lhes toodirectly comunicam entre si. Há um toocreate de forma um cluster do HDInsight com um nó de extremidade vazio. nó de extremidade Olá pode ser o cluster de Olá de toomanage utilizados.  Para obter mais informações, consulte [utilizar nós edge vazio no HDInsight](hdinsight-apps-use-edge-node.md).

2. Quando utilizar um tooHBase de tooconnect de aplicação Java remotamente, tem de utilizar o nome de domínio completamente qualificado (FQDN) do Olá. toodetermine, tem de obter o sufixo DNS de específico da ligação de Olá do cluster de HBase Olá. toodo, pode utilizar um dos seguintes métodos de Olá:

   * Utilize um toomake de browser Web uma chamada do Ambari:

     Procurar toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / aloja? minimal_response = true. Transforma um ficheiro JSON com os sufixos DNS por Olá.
   * Utilize Olá Ambari site:

     1. Procurar demasiado https://&lt;ClusterName >. azurehdinsight.net.
     2. Clique em **anfitriões** no menu superior Olá.
   * Utilize chamadas REST de toomake Curl:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     No Olá devolveu dados de JavaScript Object Notation (JSON), localizar a entrada de "host_name" Olá. Contém Olá FQDN para nós de Olá no cluster de Olá. Por exemplo:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     parte de Olá do Olá domínio nome que começa com o nome do cluster Olá é o sufixo DNS de Olá. Por exemplo, mycluster.b1.cloudapp.net.
   * Utilizar o Azure PowerShell

     Olá de utilização seguintes Olá do Azure PowerShell script tooregister **Get-ClusterDetail** função, o que pode ser o sufixo DNS de Olá tooreturn utilizado:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Após a execução Olá Azure o script do PowerShell seguinte de Olá utilize comando sufixo DNS de Olá tooreturn utilizando Olá **Get-ClusterDetail** função. Especifique o nome do cluster HBase do HDInsight, o nome de administrador e a palavra-passe de administrador ao utilizar este comando.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Este comando devolve o sufixo DNS de Olá. Por exemplo, **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify Olá máquina virtual pode comunicar com Olá HBase cluster, utilize o comando de Olá `ping headnode0.<dns suffix>` da máquina virtual de Olá. Por exemplo, executar um ping headnode0.mycluster.b1.cloudapp.net.

toouse estas informações numa aplicação Java, pode seguir passos Olá [utilizar Maven toobuild Java aplicações que utilizam o HBase com o HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate uma aplicação. aplicação de Olá toohave ligar tooa remoto HBase servidor, modifique Olá **hbase site.xml** ficheiro Olá de toouse este exemplo FQDN para Zookeeper. Por exemplo:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Para obter mais informações sobre resolução de nomes em redes virtuais do Azure, incluindo como toouse o próprio servidor DNS, consulte [resolução de nomes (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, aprendeu como toocreate um cluster HBase. toolearn mais, consulte:

* [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Utilize nós de limite vazio no HDInsight](hdinsight-apps-use-edge-node.md)
* [Configurar a replicação do HBase no HDInsight](hdinsight-hbase-replication.md)
* [Criar clusters do Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Introdução ao hbase com o Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Analisar dados de sentimento do Twitter com o HBase no HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Descrição geral da rede virtual][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalhes de aprovisionamento para o novo cluster de HBase Olá"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Utilize a ação de Script toocustomize um cluster HBase"

[azure-preview-portal]: https://portal.azure.com
