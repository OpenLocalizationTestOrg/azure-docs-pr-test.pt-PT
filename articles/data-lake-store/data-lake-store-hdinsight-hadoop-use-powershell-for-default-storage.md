---
title: aaaCreate HDInsight clusters, com o Data Lake Store, como armazenamento de predefinido utilizando o PowerShell | Microsoft Docs
description: Utilizar o Azure PowerShell toocreate e utilizar clusters do HDInsight com o Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Criar clusters do HDInsight com o Data Lake Store como armazenamento de predefinido utilizando o PowerShell
> [!div class="op_single_selector"]
> * [Utilizar Olá portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Utilize o PowerShell (para armazenamento de predefinido)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Utilize o PowerShell (para armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utilize o Gestor de recursos](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Saiba como clusters de toouse Azure PowerShell tooconfigure Azure HDInsight com o Azure Data Lake Store, como armazenamento de predefinido. Para obter instruções sobre como criar um cluster do HDInsight com o Data Lake Store, como armazenamento adicional, consulte [criar um cluster do HDInsight com o Data Lake Store, como armazenamento adicional](data-lake-store-hdinsight-hadoop-use-powershell.md).

Seguem-se algumas considerações importantes para utilizar o HDInsight com o Data Lake Store:

* Olá opção toocreate os clusters do HDInsight com acesso tooData Lake Store, como armazenamento de predefinição está disponível para o HDInsight versão 3.5 e 3.6.

* Olá opção toocreate clusters do HDInsight com aceder tooData Lake Store, como o armazenamento de predefinido é *não está disponível* para clusters do HDInsight Premium.

tooconfigure toowork HDInsight com o Data Lake Store utilizando o PowerShell, siga instruções Olá secções junto cinco Olá.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, certifique-se de que cumpre os requisitos de Olá:

* **Uma subscrição do Azure**: aceda demasiado[avaliação gratuita do Azure obter](https://azure.microsoft.com/pricing/free-trial/).
* **O Azure PowerShell 1.0 ou superior**: consulte [como tooinstall e configurar o PowerShell](/powershell/azure/overview).
* **Software Development Kit (SDK) do Windows**: tooinstall Windows SDK, aceda demasiado[transfere e ferramentas para Windows 10](https://dev.windows.com/en-us/downloads). Olá SDK é toocreate utilizado um certificado de segurança.
* **Principal de serviço do Azure Active Directory**: Este tutorial descreve como toocreate um principal de serviço no Azure Active Directory (Azure AD). No entanto, toocreate um principal de serviço, tem de ser um administrador do Azure AD. Se for um administrador, pode ignorar este pré-requisito e continue com tutorial de Olá.

    >[!NOTE]
    >Pode criar um serviço principal, apenas se for um administrador do Azure AD. O administrador do Azure AD tem de criar um serviço principal antes de poder criar um cluster do HDInsight com o Data Lake Store. Olá principal de serviço tem de ser criado com um certificado, conforme descrito em [criar um principal de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Criar uma conta do Data Lake Store
toocreate uma conta de Data Lake Store, Olá seguintes:

1. Do ambiente de trabalho, abra uma janela do PowerShell e, em seguida, introduza fragmentos Olá abaixo. Quando estiver toosign pedido no início de sessão como um dos administradores da subscrição de Olá ou proprietários. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Se registar o fornecedor de recursos do Data Lake Store Olá e receber um erro semelhante demasiado`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, a subscrição poderá não estar na lista de permissões para o Data Lake Store. tooenable sua subscrição do Azure para pré-visualização pública do Data Lake Store Olá, siga as instruções de Olá em [introdução ao Azure Data Lake Store utilizando o portal do Azure de Olá](data-lake-store-get-started-portal.md).
    >

2. Conta do Data Lake Store está associada um grupo de recursos do Azure. Comece por criar um grupo de recursos.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Deverá ver um resultado como esta:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Crie uma conta de Data Lake Store. conta de Olá nome que especificar tem de conter apenas letras minúsculas e números.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Deverá ver um resultado como Olá seguinte:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. Utilizar o Data Lake Store como armazenamento de predefinido requer toospecify que uma raiz caminho toowhich Olá cluster específicos os ficheiros são copiados durante a criação do cluster. toocreate um caminho de raiz, o que é **/clusters/hdiadlcluster** no fragmento de Olá, utilize Olá os seguintes cmdlets:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configurar a autenticação para baseada em funções aceder tooData Lake Store
Cada subscrição do Azure está associada uma entidade do Azure AD. Utilizadores e serviços que aceder a recursos de subscrição utilizando Olá portal do Azure ou Olá API do Azure Resource Manager, devem primeiro autenticar com o Azure AD. É concedido acesso tooAzure subscrições e serviços ao lhes atribuir função adequada da Olá um recurso do Azure. Para os serviços, um principal de serviço identifica o serviço de Olá no Azure AD.

Esta secção ilustra como serviço toogrant uma aplicação, tais como o HDInsight, tooan de acesso a recursos do Azure (Olá conta do Data Lake Store que criou anteriormente). Fazê-lo ao criar um serviço principal para a aplicação Olá e atribuir funções tooit através do PowerShell.

tooset configurar a autenticação do Active Directory para o Azure Data Lake, executar tarefas de Olá Olá duas secções a seguir.

### <a name="create-a-self-signed-certificate"></a>Criar um certificado autoassinado
Certifique-se de que tem [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de prosseguir Olá passos nesta secção. Tem de ter também criou um diretório, tais como *C:\mycertdir*, onde criar certificado Olá.

1. A partir da janela do PowerShell Olá, aceder localização toohello onde instalou o SDK do Windows (normalmente, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) e utilizar Olá [MakeCert] [ makecert] utilitário toocreate um certificado autoassinado e uma chave privada. Utilize Olá os seguintes comandos:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Será pedido tooenter Olá chave palavra-passe privada. Depois de comando Olá é executado com êxito, deverá ver **CertFile.cer** e **mykey.pvk** no diretório de certificado Olá que especificou.
2. Olá utilize [Pvk2Pfx] [ pvk2pfx] utilitário tooconvert Olá .pvk e. cer ficheiros se MakeCert tooa criado o ficheiro de. pfx. Execute Olá os seguintes comandos:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Quando lhe for pedido, introduza Olá chave palavra-passe privada que especificou anteriormente. Olá valor que especificar para Olá **-po** parâmetro é a palavra-passe de Olá associado ao arquivo. pfx Olá. Comando Olá tenha sido concluída com êxito, verá também uma **CertFile.pfx** no diretório de certificado Olá que especificou.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Criar um Azure AD e um principal de serviço
Nesta secção, criar um principal de serviço para uma aplicação do Azure AD, atribuir um principal de serviço de toohello de função e efetue a autenticação como principal de serviço Olá, fornecendo um certificado. toocreate uma aplicação no Azure AD, execute Olá os seguintes comandos:

1. Colar Olá os seguintes cmdlets na janela de consola do PowerShell Olá. Certifique-se de que especificou para Olá o valor Olá **- DisplayName** propriedade é exclusiva. Olá valores para **- home page** e **- IdentiferUris** são valores de marcador de posição e não são verificadas.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Criar um principal de serviço com o ID da aplicação Olá.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Conceda a raiz de Data Lake Store de toohello do acesso principal do serviço de Olá e todas as pastas de Olá no caminho da raiz Olá que especificou anteriormente. Utilize Olá os seguintes cmdlets:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Criar um cluster do HDInsight com Linux com o Data Lake Store, como armazenamento de predefinido Olá

Nesta secção, vai criar um cluster do HDInsight Hadoop Linux com o Data Lake Store como armazenamento de predefinido Olá. Nesta versão, Olá cluster do HDInsight e Data Lake Store tem de constar Olá mesma localização.

1. Obter o ID de inquilino de subscrição de Olá e armazena toouse mais tarde.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Crie cluster do HDInsight Olá utilizando Olá os seguintes cmdlets:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Cmdlet Olá tenha sido concluída com êxito, deverá ver um resultado que lista os detalhes do cluster Olá.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Executar tarefas de teste em Olá HDInsight cluster toouse Data Lake Store
Depois de configurar um cluster do HDInsight, pode executar tarefas de teste no mesmo tooensure pode aceder a Data Lake Store. toodo por isso, executar um toocreate de tarefa do Hive de exemplo a uma tabela que utiliza dados de exemplo de Olá que já se encontra disponíveis no Data Lake Store em  *<cluster root>/example/data/sample.log*.

Nesta secção, efetuar uma ligação Secure Shell (SSH) para Olá cluster do HDInsight com Linux que criou e, em seguida, executar uma consulta do Hive de exemplo.

* Se estiver a utilizar um toomake de cliente do Windows uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se estiver a utilizar um toomake de cliente do Linux uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Depois de efetuar a ligação de Olá, inicie a interface de linha de comandos de ramo de registo de Olá (CLI) utilizando Olá os seguintes comandos:

        hive
2. Olá tooenter utilize Olá CLI seguir as instruções toocreate uma nova tabela com o nome **veículos** utilizando dados de exemplo de Olá no Data Lake Store:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Deverá ver um resultado de consulta Olá na consola SSH Olá.

    >[!NOTE]
    >Olá dados de exemplo do caminho toohello no Olá precedente comando CREATE TABLE são `adl:///example/data/`, onde `adl:///` é Olá cluster raiz. Exemplo de Olá de raiz do cluster de Olá que é especificado neste tutorial, os seguintes comandos Olá é `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Pode utilizar alternativa mais curta Olá ou fornecer Olá caminho completo toohello cluster de raiz.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Aceder ao Data Lake Store utilizando comandos HDFS
Depois de ter configurado Olá HDInsight cluster toouse Data Lake Store, pode utilizar distribuídas ficheiro sistema Hadoop (HDFS) shell comandos tooaccess Olá arquivo.

Nesta secção, efetuar uma ligação SSH para Olá cluster do HDInsight com Linux que criou e, em seguida, executar os comandos HDFS Olá.

* Se estiver a utilizar um toomake de cliente do Windows uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se estiver a utilizar um toomake de cliente do Linux uma ligação SSH num cluster de Olá, consulte o artigo [utilizar o SSH com Hadoop baseado em Linux no HDInsight a partir do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Depois de efetuadas ligação Olá, listam os ficheiros de Olá no Data Lake Store utilizando Olá os seguintes comandos de sistema de ficheiros do HDFS.

    hdfs dfs -ls adl:///

Também pode utilizar Olá `hdfs dfs -put` comando tooupload alguns ficheiros tooData Lake Store e, em seguida, utilize `hdfs dfs -ls` tooverify se os ficheiros de Olá foram carregados com êxito.

## <a name="see-also"></a>Consultar também
* [Portal do Azure: criar um toouse de cluster do HDInsight Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
