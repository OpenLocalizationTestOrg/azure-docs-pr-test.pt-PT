---
title: "aaaInstall MongoDB numa VM com Linux com Olá CLI do Azure | Microsoft Docs"
description: "Saiba como tooinstall e configurar o MongoDB num Olá de iusing de máquina virtual Linux do Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Como tooinstall e configurar o MongoDB numa VM com Linux
[MongoDB](http://www.mongodb.org) é um popular open source e de elevado desempenho base de dados NoSQL. Este artigo mostra como tooinstall e configurar o MongoDB numa VM com Linux com Olá Azure CLI 2.0. Também pode executar estes passos com Olá [CLI do Azure 1.0](install-mongodb-nodejs.md). Os exemplos são apresentados como esse detalhe para:

* [Instalar e configurar uma instância do MongoDB básica manualmente](#manually-install-and-configure-mongodb-on-a-vm)
* [Criar uma instância do MongoDB básica com um modelo do Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Criar um MongoDB complexo define de cluster em partição horizontal com a réplica com um modelo do Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Instalar e configurar o MongoDB numa VM manualmente
MongoDB [fornecem instruções de instalação](https://docs.mongodb.com/manual/administration/install-on-linux/) para distros Linux, incluindo Red Hat / CentOS, SUSE, Ubuntu e Debian. Olá exemplo seguinte cria um *CentOS* VM. toocreate neste ambiente, precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

Crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroup --location eastus
```

Crie uma VM com [az vm create](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada *myVM* com um utilizador com o nome *azureuser* utilizando a autenticação de chave pública SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello VM com o seu próprio nome de utilizador e Olá `publicIpAddress` listado no resultado de Olá do passo anterior Olá:

```bash
ssh azureuser@<publicIpAddress>
```

origens de instalação de Olá tooadd para o MongoDB, crie um **yum** ficheiro repositório da seguinte forma:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Ficheiro de repositório do MongoDB Olá aberta para edição. Adicione Olá seguintes linhas:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Instalar MongoDB utilizando **yum** da seguinte forma:

```bash
sudo yum install -y mongodb-org
```

Por predefinição, é imposta SELinux nas imagens do CentOS que o impede de aceder a MongoDB. Instalar ferramentas de gestão de política e configurar SELinux tooallow MongoDB toooperate no respetiva 27017 a porta TCP predefinida da seguinte forma:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Inicie o serviço de MongoDB Olá da seguinte forma:

```bash
sudo service mongod start
```

Verifique a instalação do MongoDB de Olá ao ligar utilizando Olá local `mongo` cliente:

```bash
mongo
```

Teste agora a instância do MongoDB Olá adicionar alguns dados e, em seguida, procure:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

Se assim o pretender, configure o MongoDB toostart automaticamente durante um reinício do sistema:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Criar a instância do MongoDB básica no CentOS através de um modelo
Pode criar uma instância do MongoDB básica numa única VM CentOS utilizando Olá seguir o modelo de início rápido do Azure a partir do GitHub. Este modelo utiliza a extensão de Script personalizado Olá para Linux tooadd um **yum** repositório tooyour recém-criado CentOS VM e, em seguida, instalar MongoDB.

* [Instância do MongoDB básica no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate neste ambiente, precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login). Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroup --location eastus
```

Em seguida, implementar a modelo de MongoDB Olá com [criar a implementação do grupo az](/cli/azure/group/deployment#create). Definir os seus próprios recursos os nomes e tamanhos sempre que necessário, tais como para *newStorageAccountName*, *virtualNetworkName*, e *vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

Inicie sessão no toohello VM utilizando Olá endereço DNS público da sua VM. Pode ver o endereço DNS público Olá com [mostrar de vm az](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour VM com o seu próprio nome de utilizador e o endereço DNS público:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Verifique a instalação do MongoDB de Olá ao ligar utilizando Olá local `mongo` cliente da seguinte forma:

```bash
mongo
```

Agora teste Olá instância ao adicionar alguns dados e procura da seguinte forma:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Criar um Cluster de em partição horizontal do MongoDB complexos no CentOS através de um modelo
Pode criar um cluster da MongoDB complexo utilizando Olá seguir o modelo de início rápido do Azure a partir do GitHub. Este modelo segue Olá [melhores práticas do MongoDB em partição horizontal cluster](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundância e elevada disponibilidade. modelo de Olá cria dois shards, com três nós em cada conjunto de réplicas. Uma réplica do servidor de configuração definida com três nós também é criada, juntamente com dois **mongos** router servidores tooprovide consistência tooapplications em shards Olá.

* [Cluster de fragmentação do MongoDB em CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Este cluster em partição horizontal do MongoDB complexo a implementação requer mais de 20 núcleos, que é normalmente Olá predefinido contagem de núcleos por região para uma subscrição. Abra um tooincrease de pedido de suporte do Azure a contagem de núcleos.

toocreate neste ambiente, precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login). Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroup --location eastus
```

Em seguida, implementar a modelo de MongoDB Olá com [criar a implementação do grupo az](/cli/azure/group/deployment#create). Definir os seus próprios recursos os nomes e tamanhos sempre que necessário, tais como para *mongoAdminUsername*, *sizeOfDataDiskInGB*, e *configNodeVmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

Esta implementação pode demorar mais de uma hora toodeploy e configurar todas as instâncias VM de Olá. Olá `--no-wait` sinalizador é utilizado no fim de Olá do Olá anterior a linha de comandos do comando tooreturn controlo toohello assim que a implementação do modelo Olá foi aceite por Olá plataforma Azure. Em seguida, pode ver o estado de implementação de Olá com [mostrar de implementação do grupo de az](/cli/azure/group/deployment#show). Olá seguintes vistas de exemplo Olá estado para Olá *myMongoDBCluster* implementação no Olá *myResourceGroup* grupo de recursos:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Passos seguintes
Nestes exemplos, a ligar a instância do MongoDB toohello localmente partir Olá VM. Se pretender que a instância do MongoDB toohello tooconnect de outra VM ou de rede, certifique-se Olá adequado [regras do grupo de segurança de rede são criadas](nsg-quickstart.md).

Estes exemplos implementar ambiente MongoDB de núcleos de Olá para fins de desenvolvimento. Aplique as opções de configuração de segurança Olá necessário para o seu ambiente. Para obter mais informações, consulte Olá [docs de segurança do MongoDB](https://docs.mongodb.com/manual/security/).

Para obter mais informações sobre como criar modelos de utilização, consulte Olá [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

modelos do Azure Resource Manager Olá utilizam toodownload de extensão de Script personalizado Olá e executar scripts nas suas VMs. Para obter mais informações, consulte [Using Olá extensão de Script personalizado do Azure com as máquinas virtuais Linux](extensions-customscript.md).

