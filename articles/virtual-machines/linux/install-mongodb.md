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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="16661-103">Como tooinstall e configurar o MongoDB numa VM com Linux</span><span class="sxs-lookup"><span data-stu-id="16661-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="16661-104">[MongoDB](http://www.mongodb.org) é um popular open source e de elevado desempenho base de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="16661-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="16661-105">Este artigo mostra como tooinstall e configurar o MongoDB numa VM com Linux com Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="16661-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="16661-106">Também pode executar estes passos com Olá [CLI do Azure 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="16661-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="16661-107">Os exemplos são apresentados como esse detalhe para:</span><span class="sxs-lookup"><span data-stu-id="16661-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="16661-108">Instalar e configurar uma instância do MongoDB básica manualmente</span><span class="sxs-lookup"><span data-stu-id="16661-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="16661-109">Criar uma instância do MongoDB básica com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="16661-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="16661-110">Criar um MongoDB complexo define de cluster em partição horizontal com a réplica com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="16661-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="16661-111">Instalar e configurar o MongoDB numa VM manualmente</span><span class="sxs-lookup"><span data-stu-id="16661-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="16661-112">MongoDB [fornecem instruções de instalação](https://docs.mongodb.com/manual/administration/install-on-linux/) para distros Linux, incluindo Red Hat / CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="16661-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="16661-113">Olá exemplo seguinte cria um *CentOS* VM.</span><span class="sxs-lookup"><span data-stu-id="16661-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="16661-114">toocreate neste ambiente, precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="16661-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="16661-115">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="16661-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="16661-116">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="16661-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="16661-117">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="16661-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="16661-118">Olá exemplo seguinte cria uma VM chamada *myVM* com um utilizador com o nome *azureuser* utilizando a autenticação de chave pública SSH</span><span class="sxs-lookup"><span data-stu-id="16661-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="16661-119">SSH toohello VM com o seu próprio nome de utilizador e Olá `publicIpAddress` listado no resultado de Olá do passo anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="16661-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="16661-120">origens de instalação de Olá tooadd para o MongoDB, crie um **yum** ficheiro repositório da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="16661-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="16661-121">Ficheiro de repositório do MongoDB Olá aberta para edição.</span><span class="sxs-lookup"><span data-stu-id="16661-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="16661-122">Adicione Olá seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="16661-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="16661-123">Instalar MongoDB utilizando **yum** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="16661-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="16661-124">Por predefinição, é imposta SELinux nas imagens do CentOS que o impede de aceder a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="16661-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="16661-125">Instalar ferramentas de gestão de política e configurar SELinux tooallow MongoDB toooperate no respetiva 27017 a porta TCP predefinida da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="16661-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="16661-126">Inicie o serviço de MongoDB Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="16661-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="16661-127">Verifique a instalação do MongoDB de Olá ao ligar utilizando Olá local `mongo` cliente:</span><span class="sxs-lookup"><span data-stu-id="16661-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="16661-128">Teste agora a instância do MongoDB Olá adicionar alguns dados e, em seguida, procure:</span><span class="sxs-lookup"><span data-stu-id="16661-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="16661-129">Se assim o pretender, configure o MongoDB toostart automaticamente durante um reinício do sistema:</span><span class="sxs-lookup"><span data-stu-id="16661-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="16661-130">Criar a instância do MongoDB básica no CentOS através de um modelo</span><span class="sxs-lookup"><span data-stu-id="16661-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="16661-131">Pode criar uma instância do MongoDB básica numa única VM CentOS utilizando Olá seguir o modelo de início rápido do Azure a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="16661-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="16661-132">Este modelo utiliza a extensão de Script personalizado Olá para Linux tooadd um **yum** repositório tooyour recém-criado CentOS VM e, em seguida, instalar MongoDB.</span><span class="sxs-lookup"><span data-stu-id="16661-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="16661-133">[Instância do MongoDB básica no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="16661-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="16661-134">toocreate neste ambiente, precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="16661-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="16661-135">Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="16661-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="16661-136">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="16661-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="16661-137">Em seguida, implementar a modelo de MongoDB Olá com [criar a implementação do grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="16661-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="16661-138">Definir os seus próprios recursos os nomes e tamanhos sempre que necessário, tais como para *newStorageAccountName*, *virtualNetworkName*, e *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="16661-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="16661-139">Inicie sessão no toohello VM utilizando Olá endereço DNS público da sua VM.</span><span class="sxs-lookup"><span data-stu-id="16661-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="16661-140">Pode ver o endereço DNS público Olá com [mostrar de vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="16661-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="16661-141">SSH tooyour VM com o seu próprio nome de utilizador e o endereço DNS público:</span><span class="sxs-lookup"><span data-stu-id="16661-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="16661-142">Verifique a instalação do MongoDB de Olá ao ligar utilizando Olá local `mongo` cliente da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="16661-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="16661-143">Agora teste Olá instância ao adicionar alguns dados e procura da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="16661-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="16661-144">Criar um Cluster de em partição horizontal do MongoDB complexos no CentOS através de um modelo</span><span class="sxs-lookup"><span data-stu-id="16661-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="16661-145">Pode criar um cluster da MongoDB complexo utilizando Olá seguir o modelo de início rápido do Azure a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="16661-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="16661-146">Este modelo segue Olá [melhores práticas do MongoDB em partição horizontal cluster](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundância e elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="16661-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="16661-147">modelo de Olá cria dois shards, com três nós em cada conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="16661-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="16661-148">Uma réplica do servidor de configuração definida com três nós também é criada, juntamente com dois **mongos** router servidores tooprovide consistência tooapplications em shards Olá.</span><span class="sxs-lookup"><span data-stu-id="16661-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="16661-149">[Cluster de fragmentação do MongoDB em CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="16661-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="16661-150">Este cluster em partição horizontal do MongoDB complexo a implementação requer mais de 20 núcleos, que é normalmente Olá predefinido contagem de núcleos por região para uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="16661-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="16661-151">Abra um tooincrease de pedido de suporte do Azure a contagem de núcleos.</span><span class="sxs-lookup"><span data-stu-id="16661-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="16661-152">toocreate neste ambiente, precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="16661-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="16661-153">Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="16661-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="16661-154">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="16661-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="16661-155">Em seguida, implementar a modelo de MongoDB Olá com [criar a implementação do grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="16661-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="16661-156">Definir os seus próprios recursos os nomes e tamanhos sempre que necessário, tais como para *mongoAdminUsername*, *sizeOfDataDiskInGB*, e *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="16661-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="16661-157">Esta implementação pode demorar mais de uma hora toodeploy e configurar todas as instâncias VM de Olá.</span><span class="sxs-lookup"><span data-stu-id="16661-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="16661-158">Olá `--no-wait` sinalizador é utilizado no fim de Olá do Olá anterior a linha de comandos do comando tooreturn controlo toohello assim que a implementação do modelo Olá foi aceite por Olá plataforma Azure.</span><span class="sxs-lookup"><span data-stu-id="16661-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="16661-159">Em seguida, pode ver o estado de implementação de Olá com [mostrar de implementação do grupo de az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="16661-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="16661-160">Olá seguintes vistas de exemplo Olá estado para Olá *myMongoDBCluster* implementação no Olá *myResourceGroup* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="16661-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="16661-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="16661-161">Next steps</span></span>
<span data-ttu-id="16661-162">Nestes exemplos, a ligar a instância do MongoDB toohello localmente partir Olá VM.</span><span class="sxs-lookup"><span data-stu-id="16661-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="16661-163">Se pretender que a instância do MongoDB toohello tooconnect de outra VM ou de rede, certifique-se Olá adequado [regras do grupo de segurança de rede são criadas](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="16661-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="16661-164">Estes exemplos implementar ambiente MongoDB de núcleos de Olá para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="16661-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="16661-165">Aplique as opções de configuração de segurança Olá necessário para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="16661-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="16661-166">Para obter mais informações, consulte Olá [docs de segurança do MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="16661-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="16661-167">Para obter mais informações sobre como criar modelos de utilização, consulte Olá [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16661-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="16661-168">modelos do Azure Resource Manager Olá utilizam toodownload de extensão de Script personalizado Olá e executar scripts nas suas VMs.</span><span class="sxs-lookup"><span data-stu-id="16661-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="16661-169">Para obter mais informações, consulte [Using Olá extensão de Script personalizado do Azure com as máquinas virtuais Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="16661-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

