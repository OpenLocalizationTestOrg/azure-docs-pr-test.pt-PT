---
title: aaaCreate Hadoop clusters utilizando os modelos - Azure HDInsight | Microsoft Docs
description: Saiba como toocreate clusters para o HDInsight utilizando modelos do Resource Manager
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Criar clusters do Hadoop no HDInsight com modelos do Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Neste artigo, saiba mais formas de vários clusters toocreate Azure HDInsight com modelos Azure Resource Manager. Para obter mais informações, consulte [implementar uma aplicação com o modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). toolearn sobre outras ferramentas de criação do cluster e funcionalidades, clique em Seletor de separador Olá na parte superior de Olá deste página ou consulte [métodos de criação do Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

instruções de Olá toofollow neste artigo, precisa de:

* Um [subscrição do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* CLI do Azure PowerShell e/ou do Azure.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Modelos do Resource Manager
Um modelo do Resource Manager permite Olá toocreate fácil para a sua aplicação numa operação única e coordenada os seguintes:
* Clusters do HDInsight e os recursos dependentes (como conta de armazenamento predefinida de Olá)
* Outros recursos (por exemplo, SQL Database do Azure toouse Apache Sqoop)

No modelo de Olá, é possível definir recursos Olá que são necessários para a aplicação Olá. Também especificar valores de tooinput de parâmetros de implementação para os diferentes ambientes. Olá modelo é constituído por JSON e expressões que utilize tooconstruct valores para a sua implementação.

Pode encontrar exemplos de modelo do HDInsight em [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Utilizar várias plataformas [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) com Olá [extensão do Gestor de recursos](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou um modelo de Olá de toosave ao editor de texto num ficheiro na sua estação de trabalho. Pode saber como toocall Olá modelo através da utilização de métodos diferentes.

Para obter mais informações sobre modelos do Resource Manager, consulte Olá seguintes artigos:

* [Modelos do Azure Resource Manager autor](../azure-resource-manager/resource-group-authoring-templates.md)
* [Implementar uma aplicação com modelos Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Gerar modelos

Ao utilizar Olá portal do Azure, pode configurar todas as propriedades de Olá de um cluster e, em seguida, guardar o modelo de Olá antes de o implementar. Em seguida, pode reutilizar o modelo de Olá.

**toogenerate um modelo ao utilizar Olá portal do Azure**

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **novo** no menu à esquerda Olá, clique em **Intelligence + análise**e, em seguida, clique em **HDInsight**.
3. Siga as propriedades de tooenter Olá instruções. Pode utilizar qualquer um dos Olá **criação rápida** ou Olá **personalizada** opção.
4. No Olá **resumo** separador, clique em **transferir modelo e os parâmetros**:

    ![HDInsight Hadoop criar transferências de modelo de Gestor de recursos de cluster](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    É apresentada uma lista de ficheiro de modelo Olá, o ficheiro de parâmetros e o código amostras utilizadas toodeploy Olá modelo:

    ![HDInsight Hadoop Criar cluster as opções de transferência do modelo do Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    Aqui, pode transferir o modelo de Olá, guardá-lo a biblioteca de modelos de tooyour ou implementar a modelo Olá.

    tooaccess um modelo na biblioteca, clique em **mais serviços** no menu à esquerda de Olá e, em seguida, clique em **modelos** (em Olá **outros** categoria).

    > [!Note]
    > ficheiro de modelo e os parâmetros de Olá tem de ser utilizado em conjunto. Caso contrário, pode obter resultados inesperados. Por exemplo, Olá predefinido **clusterKind** valor da propriedade é sempre **hadoop**, não obstante que especifique antes de transferir o modelo de Olá.



## <a name="deploy-with-powershell"></a>Implementar com o PowerShell

Este procedimento cria um cluster do Hadoop no HDInsight.

1. Guardar o ficheiro JSON Olá no Olá [apêndice](#appx-a-arm-template) tooyour estação de trabalho. Olá script do PowerShell, nome de ficheiro Olá é `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Definir Olá parâmetros e variáveis se for necessário.
3. Execute o modelo de Olá utilizando Olá seguinte script do PowerShell:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    Olá script do PowerShell configura o nome do cluster apenas Olá. o nome de conta do storage Olá é "hard-coded" no modelo de Olá. São palavra-passe de utilizador de cluster de Olá tooenter pedido. (o nome de utilizador do Olá predefinido é **admin**.) Também são palavra-passe de utilizador SSH de Olá tooenter pedido. (nome de utilizador SSH Olá predefinido é **sshuser**.)  

Para obter mais informações, consulte [implementar com o PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Implementar com a CLI
Olá exemplo a seguir utiliza a interface de linha de comandos (CLI) do Azure. Cria um cluster e a conta do storage dependente e contentor ao chamar um modelo do Resource Manager:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

São tooenter pedido:
* nome do cluster Olá.
* palavra-passe utilizador cluster Olá (o nome de utilizador do Olá predefinido é **admin**.)
* palavra-passe utilizador SSH Olá (nome de utilizador SSH Olá predefinido é **sshuser**.)

Olá código a seguir fornece parâmetros inline:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Implementar com Olá REST API
Consulte [implementar com Olá REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Implementar com o Visual Studio
 Utilizar o Visual Studio toocreate um projeto do grupo de recursos e implementá-la tooAzure através da interface de utilizador Olá. Seleciona o tipo de Olá de tooinclude de recursos no seu projeto. Esses recursos são adicionados automaticamente o modelo do Resource Manager toohello. projeto de Olá também fornece um modelo de Olá de toodeploy de script do PowerShell.

Para um toousing introdução Visual Studio com grupos de recursos, consulte [criar e implementar grupos de recursos do Azure através do Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Resolução de problemas

Caso se depare com problemas com a criação de clusters do HDInsight, veja [aceder aos requisitos de controlo](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu a várias formas toocreate um cluster do HDInsight. toolearn mais, consulte Olá seguintes artigos:

* Para obter um exemplo de implementação de recursos através da biblioteca de cliente .NET Olá, consulte [implementar recursos com bibliotecas .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para obter um exemplo detalhado para implementar uma aplicação, consulte [aprovisionar e implementar micro-serviços previsibilidade no Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Para obter orientações sobre como implementar os seus ambientes de toodifferent solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](../solution-dev-test-environments.md).
* toolearn sobre Olá as secções do modelo do Azure Resource Manager Olá, consulte [criação de modelos](../azure-resource-manager/resource-group-authoring-templates.md).
* Para obter uma lista de funções de Olá, pode utilizar um modelo Azure Resource Manager, consulte [funções de modelo](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Apêndice: Resource Manager modelo toocreate um cluster de Hadoop
Olá modelo Azure Resource Manager seguinte cria um cluster do Hadoop baseados em Linux com Olá dependentes conta de armazenamento Azure.

> [!NOTE]
> Este exemplo inclui informações de configuração para o metastore do Hive e metastore do Oozie. Remover a secção de Olá ou configurar secção Olá antes de utilizar o modelo de Olá.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Apêndice: Resource Manager modelo toocreate um cluster do Spark

Esta secção fornece um modelo do Resource Manager que pode utilizar toocreate um cluster do HDInsight Spark. Este modelo inclui as configurações de `spark-defaults` e `spark-thrift-sparkconf` (para os clusters do Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (para os clusters do Spark 2). Além disso toothis, HDInsight calcula e define as configurações, tais como `spark.executor.instances`, `spark.executor.memory`, e `spark.executor.cores` com base no tamanho de cluster Olá. 

Se qualquer um parâmetro numa secção como parte do modelo de Olá próprio, HDInsight não calcular e definir Olá outros parâmetros de Olá mesma secção. Por exemplo, o parâmetro `spark.executor.instances` está a ser Olá `spark-defaults` configuração. Se definir o parâmetro outro (por exemplo, `spark.yarn.exector.memoryOverhead`) no Olá `spark-defaults` configuração, HDInsight não calcular e defina Olá `spark.executor.instances` , bem como parâmetro.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
