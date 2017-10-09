---
title: "clusters do HDInsight de aaaCustomize com ações de script - Azure | Microsoft Docs"
description: "Adicione componentes personalizados que clusters do HDInsight baseado em tooLinux com ações de Script. Ações de script são scripts de Bash que podem ser utilizado toocustomize Olá cluster configuração ou adicione serviços adicionais e utilitários como Hue, Solr ou R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Personalizar clusters do HDInsight baseado em Linux através da ação de Script

O HDInsight fornece uma opção de configuração denominada **ação de Script** que invoca scripts personalizados que personalizar cluster Olá. Estes scripts são utilizado tooinstall componentes adicionais e alterar as definições de configuração. Ações de script podem ser utilizadas durante ou após a criação do cluster.

> [!IMPORTANT]
> ações de script do Olá capacidade toouse num cluster já em execução só está disponível para clusters do HDInsight baseado em Linux.
>
> Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

Ações de script também podem ser publicada toohello Azure Marketplace como uma aplicação do HDInsight. Alguns exemplos de Olá neste documento mostram como instalar uma aplicação do HDInsight utilizando os comandos de ação de script do PowerShell e Olá .NET SDK. Para obter mais informações sobre as aplicações do HDInsight, consulte [aplicações HDInsight publicar para Olá Azure Marketplace](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Permissões

Se estiver a utilizar um cluster do HDInsight associados a um domínio, existem dois Ambari as permissões necessárias ao utilizar as ações de script com o cluster Olá:

* **AMBARI. EXECUTAR\_personalizada\_comando**: função de administrador do Ambari Olá tenha esta permissão, por predefinição.
* **CLUSTER. EXECUTAR\_personalizada\_comando**: ambos Olá administrador de Cluster do HDInsight e administrador de Ambari tem esta permissão, por predefinição.

Para obter mais informações sobre como trabalhar com permissões com o HDInsight associados a um domínio, consulte [gerir clusters do HDInsight associados a um domínio](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Controlo de acesso

Se não tiver Olá administrador/proprietário da sua subscrição do Azure, a conta tem de ter, pelo menos, **contribuinte** acesso toohello recursos grupo que contém o cluster do HDInsight Olá.

Além disso, se estiver a criar, pelo menos, um cluster do HDInsight, alguém com **contribuinte** acesso toohello subscrição do Azure tem tiver registado anteriormente fornecedor Olá para o HDInsight. Registo de fornecedor ocorre quando um utilizador com a subscrição do Contribuidor acesso toohello cria um recurso para Olá pela primeira vez no subscrição Olá. Também pode ser feito sem a criação de um recurso, ao [registar o fornecedor com REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Para obter mais informações sobre como trabalhar com a gestão de acesso, consulte Olá seguintes documentos:

* [Introdução à gestão de acesso no Olá portal do Azure](../active-directory/role-based-access-control-what-is.md)
* [Utilização de recursos de subscrição do Azure de tooyour toomanage acesso função atribuições](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Noções sobre ações de Script

Uma ação de Script é simplesmente um script de deteção que fornece um URI para e os parâmetros para. script de Olá é executado em nós de cluster do HDInsight Olá. Olá seguem-se as características e as funcionalidades de ações de script.

* Deve ser armazenado no URI que é acessível a partir do cluster do HDInsight Olá. Olá, são as localizações de armazenamento possíveis:

    * Um **Azure Data Lake Store** conta que seja acessível ao cluster do HDInsight Olá. Para obter informações sobre como utilizar o Azure Data Lake Store com o HDInsight, consulte [criar um cluster do HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Quando utilizar um script armazenado no Data Lake Store, o formato de URI Olá é `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Olá serviço principal HDInsight utiliza tooaccess Data Lake Store tem de ter acesso de leitura toohello script.

    * Um blob num **conta de armazenamento do Azure** é que as contas de armazenamento primário ou adicionais Olá para o cluster do HDInsight Olá. HDInsight é concedido acesso tooboth um destes tipos de contas de armazenamento durante a criação do cluster.

    * Um ficheiro pública partilha serviço como o Blob do Azure, o GitHub, OneDrive, Dropbox, etc.

        Por exemplo URIs, consulte Olá [scripts de ação de script de exemplo](#example-script-action-scripts) secção.

        > [!WARNING]
        > HDInsight suporta apenas __para fins gerais__ contas de armazenamento do Azure. Não suporta atualmente Olá __armazenamento de BLOBs__ tipo de conta.

* Pode ser restringida demasiado**em apenas determinados tipos de nó**para nós principais de exemplo ou nós de trabalho.

  > [!NOTE]
  > Quando utilizado com o HDInsight Premium, pode especificar que o script de Olá deve ser utilizado no nó de extremidade Olá.

* Pode ser **persistente** ou **ad hoc**.

    **Persistente** scripts são cluster do tooworker aplicados nós adicionados toohello depois Olá script é executado. Por exemplo, quando o cluster de Olá de dimensionamento.

    Um script persistente também podem ser aplicadas alterações tipo de nó de tooanother, tais como um nó principal.

  > [!IMPORTANT]
  > Ações de script persistentes tem de ter um nome exclusivo.

    **Ad hoc** scripts não são mantidos. Não são cluster do tooworker aplicados nós adicionados toohello depois de script de Olá tem foi executada. Pode promover subsequentemente um tooa scripts ad hoc persistente script ou despromover um script de ad hoc de tooan de script persistentes.

  > [!IMPORTANT]
  > Ações de script utilizadas durante a criação do cluster automaticamente são mantidas.
  >
  > Scripts que não são falhar persistem, mesmo se especificamente a indicar que devem ser.

* Pode aceitar **parâmetros** que são utilizados pelo script de Olá durante a execução.
* Executar com **privilégios de nível de raiz** em nós de cluster Olá.
* Pode ser utilizada através de Olá **portal do Azure**, **Azure PowerShell**, **CLI do Azure**, ou **SDK .NET do HDInsight**

cluster de Olá mantém um histórico de todos os scripts que tenha sido executado. histórico de Olá é útil quando for necessário toofind Olá ID de um script para operações de promoção ou despromoção.

> [!IMPORTANT]
> Não há nenhum tooundo de forma automática Olá as alterações efetuadas por uma ação de script. Inverter manualmente as alterações de Olá ou fornecer um script que inverte-los.


### <a name="script-action-in-hello-cluster-creation-process"></a>Ação de script no processo de criação do cluster Olá

Ações de script utilizadas durante a criação do cluster são ligeiramente diferentes do script foi executadas ações num cluster existente:

* script de Olá é **automaticamente persistente**.
* A **falha** em Olá script pode originar toofail de processo de criação de cluster Olá.

Olá diagrama seguinte ilustra quando a ação de Script é executada durante o processo de criação de Olá:

![Personalização de cluster do HDInsight e fases durante a criação do cluster][img-hdi-cluster-states]

executar script de Olá enquanto HDInsight está a ser configurado. Nesta fase, Olá script é executado em paralelo em todos os Olá especificados de nós no cluster Olá e é executado com privilégios de raiz em nós de Olá.

> [!NOTE]
> Uma vez script Olá é executado com privilégios de nível de raiz em nós de cluster Olá, pode efetuar operações como parar e iniciar serviços, incluindo os serviços relacionados com o Hadoop. Se parar os serviços, certifique-se de que serviço de Ambari Olá e outros serviços relacionados com o Hadoop estão em execução antes da execução do script Olá é concluída. Estes serviços são necessários toosuccessfully determinar o estado de funcionamento de Olá e estado do cluster de Olá enquanto está a ser criada.


Durante a criação do cluster, pode utilizar várias ações de script em simultâneo. Estes scripts são invocados por ordem de Olá em que foram especificadas.

> [!IMPORTANT]
> Ações de script tem de concluir dentro de 60 minutos ou tempo limite. Durante o aprovisionamento de cluster, o script de Olá é executada simultaneamente com outros processos de instalação e configuração. Disputa pelos recursos, tais como a largura de banda de CPU, tempo ou de rede pode fazer com que Olá script tootake mais toofinish que-lo no seu ambiente de desenvolvimento.
>
> Olá toominimize tempo demora toorun Olá script, evite tarefas, tais como transferir e compilar aplicações a partir da origem. Pré-compilar aplicações e armazenar os binários de Olá no armazenamento do Azure.


### <a name="script-action-on-a-running-cluster"></a>Ação de script num cluster em execução

Ao contrário das ações utilizadas durante a criação do cluster, uma falha num script são executadas num cluster já em execução do script não automaticamente causa Olá cluster toochange tooa falhada estado. Depois de um script estiver concluído, o cluster Olá deverá devolver tooa "a executar o" Estado.

> [!IMPORTANT]
> Mesmo que o cluster de Olá tem um Estado 'em execução', hello script falhada pode quebraram coisas. Por exemplo, um script foi possível eliminar ficheiros necessários pelo cluster Olá.
>
> Ações de scripts executam com privilégios de raiz, pelo que deve certificar-se de que compreende o que faz um script antes de aplicá-la tooyour cluster.

Ao aplicar um cluster de tooa de script, o estado do cluster Olá alterações toofrom **executar** demasiado**aceites**, em seguida, **HDInsight configuração**e, finalmente, faça uma cópia demasiado**Executar** para scripts com êxito. Estado de script de Olá é registado no histórico de ações de script de Olá e pode utilizar este toodetermine informações se o script de Olá foi concluída com êxito ou falha. Por exemplo, Olá `Get-AzureRmHDInsightScriptActionHistory` cmdlet do PowerShell pode ser utilizados tooview Olá estado de um script. Devolve informações toohello semelhante seguinte texto:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Se tiver alterado a palavra-passe de utilizador (administrador) do Olá cluster após a criação do cluster de Olá, script ações executaram este cluster poderá falhar. Se tiver quaisquer ações de script persistentes que nós de trabalho de destino, estes scripts podem falhar ao dimensionar o cluster de Olá.

## <a name="example-script-action-scripts"></a>Scripts de ação de Script de exemplo

Scripts de ação de script podem ser utilizadas através de Olá utilitários os seguintes:

* Portal do Azure
* Azure PowerShell
* CLI do Azure
* SDK de .NET do HDInsight

O HDInsight fornece Olá de tooinstall scripts os seguintes componentes nos clusters do HDInsight:

| Nome | Script |
| --- | --- |
| **Adicionar uma conta de armazenamento do Azure** |https://hdiconfigactions.blob.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.SH. Consulte [cluster do HDInsight adicionar armazenamento adicional tooan](hdinsight-hadoop-add-storage.md). |
| **Instalar a Hue** |https://hdiconfigactions.blob.Core.Windows.NET/linuxhueconfigactionv02/Install-hue-uber-v02.SH. Consulte [instalar e utilizar Hue no HDInsight clusters](hdinsight-hadoop-hue-linux.md). |
| **Instalar Presto** |https://RAW.githubusercontent.com/hdinsight/presto-hdinsight/Master/installpresto.SH. Consulte [instalar e utilizar Presto no HDInsight clusters](hdinsight-hadoop-install-presto.md). |
| **Instalar Solr** |https://hdiconfigactions.blob.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.SH. Consulte [instalar e utilizar Solr no HDInsight clusters](hdinsight-hadoop-solr-install-linux.md). |
| **Instalar Giraph** |https://hdiconfigactions.blob.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.SH. Consulte [instalar e utilizar Giraph no HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md). |
| **Pré-carregar as bibliotecas Hive** |https://hdiconfigactions.blob.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.SH. Consulte [bibliotecas adicionar Hive nos clusters do HDInsight](hdinsight-hadoop-add-hive-libraries.md). |
| **Instalar ou atualizar o Mono** | https://hdiconfigactions.blob.Core.Windows.NET/Install-mono/Install-mono.bash. Consulte [instalação ou atualização Mono no HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Utilizar uma ação de Script durante a criação do cluster

Esta secção fornece exemplos sobre diferentes formas de Olá que pode utilizar ações de script ao criar um cluster do HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Utilizar uma ação de Script durante a criação do cluster de Olá portal do Azure

1. Começar a criar um cluster, conforme descrito em [clusters do Hadoop criar no HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Pare quando chegar Olá __resumo do Cluster__ secção.

2. De Olá __resumo do Cluster__ secção, selecione de Olá __editar__ hiperligação para __definições avançadas__.

    ![Definições avançadas de ligação](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. De Olá __definições avançadas__ secção, selecione __ações de Script__. De Olá __ações de Script__ secção, selecione __+ submeter novos__

    ![Submeter uma nova ação de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Olá utilize __selecionar um script__ entrada tooselect um script pré-cópia efetuado. toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o script.

    ![Adicionar um script no formulário de script selecione Olá](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Olá, a tabela seguinte descreve os elementos de Olá no formulário de Olá:

    | Propriedade | Valor |
    | --- | --- |
    | Selecione um script | toouse seu próprio script, selecione __personalizada__. Caso contrário, selecione um dos scripts de Olá fornecido. |
    | Nome |Especifique um nome para a ação de script de Olá. |
    | Scripts de bash URI |Especifique Olá URI toohello script que é invocada toocustomize Olá cluster. |
    | Trabalho/HEAD/Zookeeper |Especificar Olá nós (**Head**, **trabalho**, ou **ZooKeeper**) que personalização Olá script é executado. |
    | Parâmetros |Especifique parâmetros de Olá, se necessário pelo script de Olá. |

    Olá utilize __manter esta ação de script__ tooensure de entrada que Olá script é aplicada durante operações de dimensionamento.

5. Selecione __criar__ script de Olá toosave. Em seguida, pode utilizar __+ submeter novo__ tooadd outro script.

    ![Várias ações de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Quando tiver concluído a adição de scripts, utilize Olá __selecione__ botão e, em seguida, Olá __seguinte__ botão tooreturn toohello __resumo do Cluster__ secção.

3. cluster de Olá toocreate, selecione __criar__ de Olá __resumo do Cluster__ seleção.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Utilizar uma ação de Script a partir de modelos Azure Resource Manager

Exemplos de Olá desta secção demonstram como toouse script ações com modelos Azure Resource Manager.

#### <a name="before-you-begin"></a>Antes de começar

* Para obter informações sobre como configurar uma estação de trabalho toorun cmdlets do Powershell do HDInsight, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).
* Para obter instruções sobre como toocreate modelos, consulte [modelos Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Se tiver não utilizado anteriormente Azure PowerShell com o Resource Manager, consulte o artigo [utilizar o Azure PowerShell com o Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Criar clusters através da ação de Script

1. Copie Olá seguinte localização do modelo tooa no seu computador. Este modelo instala Giraph em Olá headnodes e de trabalho nós Olá cluster. Também pode verificar se o modelo JSON Olá é válido. Cole o conteúdo do modelo [JSONLint](http://jsonlint.com/), uma ferramenta de validação JSON online.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Inicie o Azure PowerShell e inicie sessão tooyour conta do Azure. Depois de fornecer as suas credenciais, o comando de Olá devolve informações sobre a sua conta.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Se tiver várias subscrições, forneça o ID de subscrição de Olá desejar toouse para implementação.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Pode utilizar `Get-AzureRmSubscription` tooget uma lista de todas as subscrições associadas à sua conta, que inclui o ID de subscrição de Olá para cada um deles.

4. Se não tiver um grupo de recursos existente, crie um grupo de recursos. Forneça o nome de Olá do grupo de recursos de Olá e a localização que precisa para a sua solução. Um resumo do grupo de recursos novo Olá é devolvido.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate uma implementação para o grupo de recursos, executar Olá **New-AzureRmResourceGroupDeployment** de comandos e fornecer os parâmetros necessários Olá. parâmetros de Olá incluem Olá dados os seguintes:

    * Um nome para a implementação
    * nome de Olá do seu grupo de recursos
    * caminho de Olá ou modelo de toohello de URL que criou.

  Se o seu modelo necessita de quaisquer parâmetros, tem de passar esses parâmetros bem. Neste caso, ação de script Olá tooinstall R no cluster de Olá não requer quaisquer parâmetros.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    São tooprovide pedido valores para parâmetros de Olá definidos no modelo de Olá.

1. Quando o grupo de recursos de Olá tiver sido implementado, é apresentado um resumo da implementação de Olá.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Se a implementação falhar, pode utilizar Olá os seguintes cmdlets tooget informações sobre falhas de Olá.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Utilizar uma ação de Script durante a criação do cluster a partir do Azure PowerShell

Nesta secção, vamos utilizar Olá [adicionar AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts, utilizando a ação de Script toocustomize um cluster. Antes de continuar, certifique-se de que tem instalado e configurado o Azure PowerShell. Para obter informações sobre como configurar uma estação de trabalho toorun cmdlets do PowerShell do HDInsight, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

Olá script seguinte demonstra como tooapply uma ação de script ao criar um cluster com o PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Pode demorar vários minutos antes de Olá cluster é criado.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Utilizar uma ação de Script durante a criação do cluster de Olá SDK .NET do HDInsight

Olá SDK .NET do HDInsight fornece bibliotecas de cliente que torna mais fácil toowork com o HDInsight a partir de uma aplicação .NET. Para um exemplo de código, consulte [baseado em Linux criar clusters do HDInsight utilizando Olá .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Aplicar tooa uma ação de Script a executar o cluster

Nesta secção, saiba como tooapply script tooa ações a executar o cluster.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Aplicar tooa uma ação de Script a executar o cluster de Olá portal do Azure

1. De Olá [portal do Azure](https://portal.azure.com), selecione o cluster do HDInsight.

2. Na descrição geral do Olá HDInsight cluster, selecione Olá **ações de Script** mosaico.

    ![Mosaico de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Também pode selecionar **todas as definições** e, em seguida, selecione **ações de Script** de Olá secção de definições.

3. Na parte superior de Olá de Olá secção ações de Script, selecione **submeter novo**.

    ![Adicionar um tooa de script a executar o cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Olá utilize __selecionar um script__ entrada tooselect um script pré-cópia efetuado. toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o script.

    ![Adicionar um script no formulário de script selecione Olá](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Olá, a tabela seguinte descreve os elementos de Olá no formulário de Olá:

    | Propriedade | Valor |
    | --- | --- |
    | Selecione um script | toouse seu próprio script, selecione __personalizado__. Caso contrário, selecione um script fornecidos. |
    | Nome |Especifique um nome para a ação de script de Olá. |
    | Scripts de bash URI |Especifique Olá URI toohello script que é invocada toocustomize Olá cluster. |
    | Trabalho/HEAD/Zookeeper |Especificar Olá nós (**Head**, **trabalho**, ou **ZooKeeper**) que personalização Olá script é executado. |
    | Parâmetros |Especifique parâmetros de Olá, se necessário pelo script de Olá. |

    Olá utilize __manter esta ação de script__ script de Olá se toomake entrada é aplicada durante operações de dimensionamento.

5. Por último, utilize Olá **criar** o cluster de toohello do botão tooapply Olá script.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Aplicar tooa uma ação de Script a executar o cluster a partir do Azure PowerShell

Antes de continuar, certifique-se de que tem instalado e configurado o Azure PowerShell. Para obter informações sobre como configurar uma estação de trabalho toorun cmdlets do PowerShell do HDInsight, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

Olá exemplo seguinte demonstra como tooapply um cluster em execução do script ação tooa:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Uma vez concluída a operação de Olá, receberá informações toohello semelhante, seguinte texto:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Aplicar tooa uma ação de Script a executar o cluster de Olá CLI do Azure

Antes de continuar, certifique-se de que instalou e configurou Olá CLI do Azure. Para obter mais informações, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure modo Resource Manager, utilize Olá seguinte comando na linha de comandos Olá:

        azure config mode arm

2. Utilize Olá seguir tooauthenticate tooyour subscrição do Azure.

        azure login

3. Utilize os seguintes comandos tooapply um tooa de ação de script a executar o cluster de Olá

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Se omitir parâmetros para este comando, é-lhe pedida-los. Se Olá script especificar com `-u` aceite parâmetros, pode especificá-los utilizando Olá `-p` parâmetro.

    Os tipos de nó válido são `headnode`, `workernode`, e `zookeeper`. Se o script de Olá deve ser aplicado toomultiple tipos de nó, especificar os tipos de Olá separados por um ';'. Por exemplo, `-n headnode;workernode`.

    toopersist Olá script, adicione Olá `--persistOnSuccess`. Pode também manter hello script mais tarde utilizando `azure hdinsight script-action persisted set`.

    Uma vez concluída a tarefa de Olá, receberá toohello semelhante de saída seguinte texto:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Aplicar tooa uma ação de Script a executar o cluster utilizando a REST API

Consulte [executar ações de Script num cluster em execução](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Aplicar tooa uma ação de Script a executar o cluster de Olá SDK .NET do HDInsight

Para obter um exemplo de utilização Olá .NET SDK tooapply scripts tooa cluster, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Ver histórico, promover e despromover ações de Script

### <a name="using-hello-azure-portal"></a>Utilizar Olá portal do Azure

1. De Olá [portal do Azure](https://portal.azure.com), selecione o cluster do HDInsight.

2. Na descrição geral do Olá HDInsight cluster, selecione Olá **ações de Script** mosaico.

    ![Mosaico de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Também pode selecionar **todas as definições** e, em seguida, selecione **ações de Script** de Olá secção de definições.

4. Um histórico de scripts para este cluster é apresentado no Olá secção ações de Script. Estas informações incluem uma lista de scripts persistentes. Olá captura de ecrã abaixo, pode ver essa Olá Solr script foi executada neste cluster. Olá captura de ecrã mostra quaisquer scripts persistentes.

    ![Secção de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. A seleção de um script do histórico de Olá apresenta a secção de propriedades de Olá para este script. De Olá parte superior do ecrã de Olá, pode voltar a executar o script de Olá ou promovê-lo.

    ![Propriedades de ações de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Também pode utilizar Olá **...**  toohello direito de entradas das ações do Olá ações de Script secção tooperform.

    ![Ações de script... utilização](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Utilizar o Azure PowerShell

| Utilize o seguinte Olá... | demasiado... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Obter informações sobre ações de script persistentes |
| Get-AzureRmHDInsightScriptActionHistory |Obter um histórico de script ações aplicadas toohello cluster ou os detalhes para um script específico |
| Set-AzureRmHDInsightPersistedScriptAction |Promove um ad hoc tooa de ação de script persistentes ação de script |
| Remove-AzureRmHDInsightPersistedScriptAction |Despromove uma ação do script persistentes ação tooan ad hoc |

> [!IMPORTANT]
> Utilizar `Remove-AzureRmHDInsightPersistedScriptAction` não anular ações Olá efetuadas por um script. Este cmdlet apenas remove o sinalizador persistente Olá.

Olá seguinte script de exemplo demonstra utilizando Olá cmdlets toopromote, em seguida, despromover um script.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Utilizar Olá CLI do Azure

| Utilize o seguinte Olá... | demasiado... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Obter uma lista de ações de script persistentes |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Obter informações sobre uma ação de script persistentes específico |
| `azure hdinsight script-action history list <clustername>` |Obter um histórico de script ações aplicadas toohello cluster |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Obter informações sobre uma ação de script específico |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Promove um ad hoc tooa de ação de script persistentes ação de script |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Despromove uma ação do script persistentes ação tooan ad hoc |

> [!IMPORTANT]
> Utilizar `azure hdinsight script-action persisted delete` não anular ações Olá efetuadas por um script. Este cmdlet apenas remove o sinalizador persistente Olá.

### <a name="using-hello-hdinsight-net-sdk"></a>Utilizar Olá SDK .NET do HDInsight

Para obter um exemplo de utilização Olá .NET SDK tooretrieve histórico de script de um cluster, promover ou despromover scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Este exemplo mostra também como tooinstall uma aplicação do HDInsight utilizando Olá .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Suporte para o software de open source utilizados nos clusters do HDInsight

Olá serviço Microsoft Azure HDInsight utiliza um ecossistema de tecnologias de open source formado em torno do Hadoop. Microsoft Azure fornece um nível geral de suporte para tecnologias de open source. Para obter mais informações, consulte Olá **suporte âmbito** secção Olá [site FAQ de suporte do Azure](https://azure.microsoft.com/support/faq/). Olá serviço HDInsight fornece um nível adicional de suporte para componentes incorporados.

Existem dois tipos de componentes de open source que estão disponíveis no Olá serviço HDInsight:

* **Componentes incorporados** -estes componentes são previamente instalados nos clusters do HDInsight e fornecer a funcionalidade principal do cluster de Olá. Por exemplo, YARN ResourceManager, idioma de consulta do Hive Olá (HiveQL) e biblioteca de Mahout Olá pertencem toothis categoria. Uma lista completa dos componentes de cluster está disponível no [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight](hdinsight-component-versioning.md).
* **Componentes personalizados** -, como um utilizador do cluster de Olá, pode instalar ou utilizar na sua carga de trabalho qualquer componente disponível na Comunidade Olá ou criado por si.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados. Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.
>
> Componentes personalizados recebem suporte comercialmente razoáveis toohelp toofurther poderá resolver o problema de Olá. Suporte da Microsoft pode ser capaz de tooresolve problema de Olá ou poderão pedir-lhe canais disponíveis tooengage para tecnologias de código aberto olá onde se encontra profundo conhecimentos para que a tecnologia. Por exemplo, existem vários sites de Comunidade que podem ser utilizadas, como: [fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Também projetos do Apache tem sites de projeto no [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).

Olá serviço HDInsight fornece várias formas componentes personalizados toouse. Olá mesmo nível de suporte aplica-se, independentemente da forma como um componente utilizado ou não está instalado no cluster de Olá. Olá lista seguinte descreve formas mais comuns Olá que componentes personalizados podem ser utilizados nos clusters do HDInsight:

1. Submissão de tarefa - Hadoop ou outros tipos de tarefas que executarem ou utilizam componentes personalizados pode ser submetidos toohello cluster.

2. Personalização de cluster - durante a criação do cluster, pode especificar definições adicionais e componentes personalizados que estão instalados em nós de cluster Olá.

3. Fornecem exemplos de como estes componentes podem ser utilizados nos clusters do HDInsight Olá amostras - para componentes personalizados populares, a Microsoft e outras pessoas. Estes exemplos são fornecidos sem suporte.

## <a name="troubleshooting"></a>Resolução de problemas

Pode utilizar Ambari web IU tooview informações registadas pelas ações de script. Se o script de Olá falhar durante a criação do cluster, os registos de Olá também estão disponíveis na conta do storage predefinida Olá associada ao cluster Olá. Esta secção fornece informações sobre como tooretrieve Olá registos utilizando ambas estas opções.

### <a name="using-hello-ambari-web-ui"></a>Utilizar Olá IU da Web do Ambari

1. No seu browser, navegue até toohttps://CLUSTERNAME.azurehdinsight.net. Substitua CLUSTERNAME pelo nome de Olá do cluster do HDInsight.

    Quando lhe for pedido, introduza o nome da conta de administrador Olá (administrador) e palavra-passe para o cluster de Olá. Poderá ter credenciais de administrador de Olá tooreenter num formulário web.

2. Na barra de Olá na Olá parte superior da página Olá, selecione Olá **ops** entrada. É apresentada uma lista de atuais e anteriores operações executadas no cluster de Olá através do Ambari.

    ![Barra de IU do Ambari web com ops selecionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Localizar as entradas de Olá que tenham **executar\_customscriptaction** no Olá **operações** coluna. Estas entradas são criadas quando executar ações de Script de Olá.

    ![Captura de ecrã de operações](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    Olá tooview STDOUT e STDERR resultado. o, selecione a entrada de run\customscriptaction Olá e desagregar através de ligações de Olá. Este resultado é gerado quando executa o script de Olá e pode conter informações úteis.

### <a name="access-logs-from-hello-default-storage-account"></a>Registos de acesso da conta do storage predefinida Olá

Se a criação do cluster Olá falhar devido a erro de ação de script tooa, Olá registos podem ser acedidos da conta de armazenamento de cluster Olá.

* Olá os registos de armazenamento estão disponíveis em `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Captura de ecrã de operações](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    Neste diretório, Olá registos são organizados em separado para headnode, workernode e nós de zookeeper. Alguns exemplos incluem:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Nó de trabalho** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Nós de zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Todos os stdout e stderr do anfitrião correspondente Olá é carregado toohello conta de armazenamento. Há um **resultado -\*. txt** e **erros -\*. txt** para cada ação de script. ficheiro de saída *.txt Olá contém informações sobre Olá URI de script de Olá que recebeu a ser executado no anfitrião de Olá. Por exemplo

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* É possível criar repetidamente um cluster de ação de script com Olá mesmo nome. Esse caso, poder diferenciar os registos relevantes Olá com base no nome da pasta data Olá. Por exemplo, a estrutura da pasta de Olá para um cluster (mycluster) criado em datas diferentes aparece toohello semelhante seguintes entradas de registo:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Se criar um cluster de ação de script com Olá mesmo nome no Olá mesmo dia, pode utilizar ficheiros de registo relevantes do Olá prefixo exclusivo tooidentify Olá.

* Se criar um cluster quase 12:00:00 (meia-noite), é possível que os ficheiros de registo Olá span em dois dias. Nestes casos, verá duas pastas data diferente para Olá mesmo cluster.

* Carregamento contentor de predefinido do toohello de ficheiros de registo pode demorar até too5 minutos, especialmente para grandes clusters. Por isso, se pretender que os registos de Olá tooaccess, não deverá imediatamente Eliminar cluster Olá se falhar de uma ação de script.

### <a name="ambari-watchdog"></a>Watchdog do Ambari

> [!WARNING]
> Não altere Olá palavra-passe para Olá Ambari watchdog do (hdinsightwatchdog) no cluster do HDInsight baseado em Linux. A alteração Olá palavra-passe para esta conta de quebras de ações de script Olá capacidade toorun novo num cluster do HDInsight Olá.

### <a name="cant-import-name-blobservice"></a>Não é possível importar o nome BlobService

__Sintomas__: Olá falha de ação de script. Toohello semelhante de texto seguinte erro é apresentado quando visualizar operação Olá no Ambari:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Causa__: Este erro ocorre se atualizar o cliente de armazenamento do Azure de Python Olá que está incluída no cluster do HDInsight Olá. HDInsight espera que o cliente de armazenamento do Azure 0.20.0.

__Resolução__: tooresolve este erro, manualmente estabeleçam ligação através do nó de cluster da tooeach `ssh` e versão de cliente de armazenamento correta do comando tooreinstall Olá Olá utilize os seguintes:

```
sudo pip install azure-storage==0.20.0
```

Para obter informações sobre a ligação toohello cluster com SSH, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Histórico não mostra scripts utilizados durante a criação do cluster

Se o cluster foi criado antes de 15 de Março de 2016, não poderá ver uma entrada no histórico de ação de Script. Se redimensionar cluster Olá após 15 de Março de 2016, os scripts de Olá com durante a criação do cluster são apresentados no histórico de como estas são aplicadas toonew nós no cluster de Olá como parte da Olá redimensionar a operação.

Existem duas exceções:

* Se o cluster foi criado antes de 1 de Setembro de 2015. Esta data é quando foram introduzidas ações de Script. Qualquer cluster criado antes desta data não foi ter utilizar ações de Script para a criação do cluster.

* Se utilizar várias ações de Script durante a criação do cluster e utilizado Olá mesmo nome para vários scripts ou Olá mesmo nome, mesmo URI, mas parâmetros diferentes de vários scripts. Nestes casos, receberá Olá seguinte erro:

    Não existe nenhum script de nova ações podem ser executadas neste cluster devido a nomes do script tooconflicting em scripts existentes. Nomes do script fornecidos no cluster criar tem de ser exclusivos. Os scripts existentes são executadas no redimensionamento.

## <a name="next-steps"></a>Passos seguintes

* [Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Instalar e utilizar Solr nos clusters do HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Instalar e utilizar Giraph nos clusters do HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Adicionar o cluster de HDInsight tooan armazenamento adicional](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fases durante a criação do cluster"
