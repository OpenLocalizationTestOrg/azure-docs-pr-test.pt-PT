---
title: aaaImplement Oracle Golden porta numa VM do Linux do Azure | Microsoft Docs
description: "Obter rapidamente uma porta de Golden Oracle cópias de segurança e em execução no seu ambiente do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="827bb-103">Implementar Oracle Golden porta numa VM com Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="827bb-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="827bb-104">Olá CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="827bb-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="827bb-105">Este detalhes guia como toouse Olá CLI do Azure toodeploy um Oracle 12c da base de dados da imagem de galeria do Azure Marketplace Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="827bb-106">Este documento mostra-lhe passo a passo como toocreate, instalar e configurar o Oracle Golden porta numa VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="827bb-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="827bb-107">Antes de começar, certifique-se de que Olá que CLI do Azure foi instalado.</span><span class="sxs-lookup"><span data-stu-id="827bb-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="827bb-108">Para obter mais informações, veja [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="827bb-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="827bb-109">Preparar o ambiente de Olá</span><span class="sxs-lookup"><span data-stu-id="827bb-109">Prepare hello environment</span></span>

<span data-ttu-id="827bb-110">instalação do tooperform Olá Oracle Golden porta, terá de VMs do Azure toocreate dois Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="827bb-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="827bb-111">imagem do Marketplace Olá utilizar toocreate Olá VMs é **Oracle: Oracle-base de dados-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="827bb-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="827bb-112">Também precisa de toobe familiarizado com vi do editor de Unix e noções básicas de x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="827bb-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="827bb-113">Olá segue-se um resumo da configuração do ambiente de Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="827bb-114">**Site primário**</span><span class="sxs-lookup"><span data-stu-id="827bb-114">**Primary site**</span></span> | <span data-ttu-id="827bb-115">**Replicar site**</span><span class="sxs-lookup"><span data-stu-id="827bb-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="827bb-116">**Versão de Oracle**</span><span class="sxs-lookup"><span data-stu-id="827bb-116">**Oracle release**</span></span> |<span data-ttu-id="827bb-117">Oracle 12c versão 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="827bb-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="827bb-118">Oracle 12c versão 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="827bb-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="827bb-119">**Nome do computador**</span><span class="sxs-lookup"><span data-stu-id="827bb-119">**Machine name**</span></span> |<span data-ttu-id="827bb-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="827bb-120">myVM1</span></span> |<span data-ttu-id="827bb-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="827bb-121">myVM2</span></span> |
> | <span data-ttu-id="827bb-122">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="827bb-122">**Operating system**</span></span> |<span data-ttu-id="827bb-123">Oracle Linux 6. x</span><span class="sxs-lookup"><span data-stu-id="827bb-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="827bb-124">Oracle Linux 6. x</span><span class="sxs-lookup"><span data-stu-id="827bb-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="827bb-125">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="827bb-125">**Oracle SID**</span></span> |<span data-ttu-id="827bb-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="827bb-126">CDB1</span></span> |<span data-ttu-id="827bb-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="827bb-127">CDB1</span></span> |
> | <span data-ttu-id="827bb-128">**Esquema de replicação**</span><span class="sxs-lookup"><span data-stu-id="827bb-128">**Replication schema**</span></span> |<span data-ttu-id="827bb-129">TESTE</span><span class="sxs-lookup"><span data-stu-id="827bb-129">TEST</span></span>|<span data-ttu-id="827bb-130">TESTE</span><span class="sxs-lookup"><span data-stu-id="827bb-130">TEST</span></span> |
> | <span data-ttu-id="827bb-131">**Porta Golden proprietário/replicar**</span><span class="sxs-lookup"><span data-stu-id="827bb-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="827bb-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="827bb-132">C##GGADMIN</span></span> |<span data-ttu-id="827bb-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="827bb-133">REPUSER</span></span> |
> | <span data-ttu-id="827bb-134">**Processo de porta de Golden**</span><span class="sxs-lookup"><span data-stu-id="827bb-134">**Golden Gate process**</span></span> |<span data-ttu-id="827bb-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="827bb-135">EXTORA</span></span> |<span data-ttu-id="827bb-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="827bb-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="827bb-137">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="827bb-137">Sign in tooAzure</span></span> 

<span data-ttu-id="827bb-138">Inicie sessão no tooyour subscrição do Azure com Olá [início de sessão az](/cli/azure/#login) comando.</span><span class="sxs-lookup"><span data-stu-id="827bb-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="827bb-139">Em seguida, siga Olá no ecrã instruções.</span><span class="sxs-lookup"><span data-stu-id="827bb-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="827bb-140">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="827bb-140">Create a resource group</span></span>

<span data-ttu-id="827bb-141">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="827bb-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="827bb-142">Um grupo de recursos do Azure é um contentor lógico para os recursos do Azure são implementados e para que possam ser geridos.</span><span class="sxs-lookup"><span data-stu-id="827bb-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="827bb-143">Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `westus` localização.</span><span class="sxs-lookup"><span data-stu-id="827bb-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="827bb-144">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="827bb-144">Create an availability set</span></span>

<span data-ttu-id="827bb-145">Olá seguir passo é opcional mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="827bb-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="827bb-146">Para obter mais informações, consulte [guia de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="827bb-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="827bb-147">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="827bb-147">Create a virtual machine</span></span>

<span data-ttu-id="827bb-148">Criar uma VM com Olá [az vm criar](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="827bb-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="827bb-149">Olá exemplo seguinte cria duas VMs com o nome `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="827bb-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="827bb-150">Crie chaves SSH se estes ainda não existir numa localização chave predefinido.</span><span class="sxs-lookup"><span data-stu-id="827bb-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="827bb-151">toouse específicos de um conjunto de chaves, utilize Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="827bb-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="827bb-152">Crie myVM1 (principal):</span><span class="sxs-lookup"><span data-stu-id="827bb-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="827bb-153">Depois de Olá que VM foi criada, Olá CLI do Azure mostra informações toohello semelhante seguinte o exemplo.</span><span class="sxs-lookup"><span data-stu-id="827bb-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="827bb-154">(Tome nota do Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="827bb-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="827bb-155">Este endereço é utilizado tooaccess Olá VM.)</span><span class="sxs-lookup"><span data-stu-id="827bb-155">This address is used tooaccess hello VM.)</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="827bb-156">Criar myVM2 (replicar):</span><span class="sxs-lookup"><span data-stu-id="827bb-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="827bb-157">Tome nota do Olá `publicIpAddress` bem depois de terem sido criadas.</span><span class="sxs-lookup"><span data-stu-id="827bb-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="827bb-158">Abra a porta TCP Olá conectividade</span><span class="sxs-lookup"><span data-stu-id="827bb-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="827bb-159">Olá passo seguinte consiste em tooconfigure pontos finais externos, que lhe permitem a base de dados Oracle de Olá tooaccess remotamente.</span><span class="sxs-lookup"><span data-stu-id="827bb-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="827bb-160">tooconfigure Olá pontos finais externos, executados os seguintes comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="827bb-161">Abra a porta de Olá para myVM1:</span><span class="sxs-lookup"><span data-stu-id="827bb-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="827bb-162">resultados de Olá deverá ter um aspeto semelhante toohello seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="827bb-162">hello results should look similar toohello following response:</span></span>

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="827bb-163">Abra a porta de Olá para myVM2:</span><span class="sxs-lookup"><span data-stu-id="827bb-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="827bb-164">Ligar a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="827bb-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="827bb-165">Toocreate uma sessão SSH com a máquina virtual de Olá de comando seguinte Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="827bb-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="827bb-166">Substitua o endereço IP Olá Olá `publicIpAddress` da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="827bb-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="827bb-167">Criar base de dados de Olá myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="827bb-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="827bb-168">Olá Oracle software já está instalada na imagem do Marketplace Olá, pelo que o passo seguinte Olá é a base de dados do tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="827bb-169">Execute software Olá como Superutilizador do Olá 'oracle':</span><span class="sxs-lookup"><span data-stu-id="827bb-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="827bb-170">Crie base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-170">Create hello database:</span></span>

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
<span data-ttu-id="827bb-171">Saídas deverá ter um aspeto semelhante toohello seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="827bb-171">Outputs should look similar toohello following response:</span></span>

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="827bb-172">Definir variáveis ORACLE_SID e ORACLE_HOME Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="827bb-173">Opcionalmente, pode adicionar ORACLE_HOME e ORACLE_SID toohello .bashrc o ficheiro, para que estas definições são guardadas para consulta futuros inícios de sessão:</span><span class="sxs-lookup"><span data-stu-id="827bb-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="827bb-174">Iniciar o serviço de escuta do Oracle</span><span class="sxs-lookup"><span data-stu-id="827bb-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="827bb-175">Criar base de dados de Olá myVM2 (replicar)</span><span class="sxs-lookup"><span data-stu-id="827bb-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="827bb-176">Crie base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-176">Create hello database:</span></span>

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
<span data-ttu-id="827bb-177">Definir variáveis ORACLE_SID e ORACLE_HOME Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="827bb-178">Opcionalmente, pode adicionado ORACLE_HOME ORACLE_SID toohello .bashrc ficheiro e, para que estas definições são guardadas para consulta futuros inícios de sessão.</span><span class="sxs-lookup"><span data-stu-id="827bb-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="827bb-179">Iniciar o serviço de escuta do Oracle</span><span class="sxs-lookup"><span data-stu-id="827bb-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="827bb-180">Configurar a porta Golden</span><span class="sxs-lookup"><span data-stu-id="827bb-180">Configure Golden Gate</span></span> 
<span data-ttu-id="827bb-181">tooconfigure Golden porta, siga os passos de Olá nesta secção.</span><span class="sxs-lookup"><span data-stu-id="827bb-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="827bb-182">Ativar o modo de registo de arquivo em myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="827bb-182">Enable archive log mode on myVM1 (primary)</span></span>

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
<span data-ttu-id="827bb-183">Ativar o registo de imposição e certifique-se, pelo menos, um ficheiro de registo está presente.</span><span class="sxs-lookup"><span data-stu-id="827bb-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="827bb-184">Transferir o software de porta de Golden</span><span class="sxs-lookup"><span data-stu-id="827bb-184">Download Golden Gate software</span></span>
<span data-ttu-id="827bb-185">toodownload e preparar o software de Oracle Golden porta Olá, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="827bb-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="827bb-186">Transferir Olá **fbo_ggs_Linux_x64_shiphome.zip** ficheiro a partir do Olá [página de transferência do Oracle Golden porta](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="827bb-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="827bb-187">Em Olá transferir título **12.x.x.x Oracle GoldenGate para Oracle Linux x86-64**, deverá haver um conjunto de toodownload de ficheiros. zip.</span><span class="sxs-lookup"><span data-stu-id="827bb-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="827bb-188">Depois de transferir o computador de cliente de tooyour de ficheiros. zip Olá, utilize o protocolo Secure de cópia (SCP) toocopy Olá ficheiros tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="827bb-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="827bb-189">Mover Olá. zip ficheiros toohello **/ optar ativamente por participar** pasta.</span><span class="sxs-lookup"><span data-stu-id="827bb-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="827bb-190">Em seguida, altere o proprietário de Olá dos ficheiros de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="827bb-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="827bb-191">Descomprimir ficheiros de Olá (instalação Olá Linux deszipe utilitário se ainda não estiver instalado):</span><span class="sxs-lookup"><span data-stu-id="827bb-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="827bb-192">Permissão de alteração:</span><span class="sxs-lookup"><span data-stu-id="827bb-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="827bb-193">Preparar o cliente de Olá e VM toorun x11 (para clientes Windows)</span><span class="sxs-lookup"><span data-stu-id="827bb-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="827bb-194">Este passo é opcional.</span><span class="sxs-lookup"><span data-stu-id="827bb-194">This is an optional step.</span></span> <span data-ttu-id="827bb-195">Pode ignorar este passo se estiver a utilizar um cliente Linux ou já ter x11 programa de configuração.</span><span class="sxs-lookup"><span data-stu-id="827bb-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="827bb-196">Transfira o PuTTY e Xming tooyour Windows de computador:</span><span class="sxs-lookup"><span data-stu-id="827bb-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="827bb-197">Transfira o PuTTY</span><span class="sxs-lookup"><span data-stu-id="827bb-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="827bb-198">Transferir Xming</span><span class="sxs-lookup"><span data-stu-id="827bb-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="827bb-199">Depois de instalar o PuTTY, no Olá PuTTY pasta (por exemplo, c:\Programas\Microsoft Files\PuTTY), execute puttygen.exe (gerador de chave PuTTY).</span><span class="sxs-lookup"><span data-stu-id="827bb-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="827bb-200">No gerador de chave PuTTY:</span><span class="sxs-lookup"><span data-stu-id="827bb-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="827bb-201">toogenerate Olá uma chave, selecione **gerar** botão.</span><span class="sxs-lookup"><span data-stu-id="827bb-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="827bb-202">Copiar conteúdos de Olá da chave de Olá (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="827bb-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="827bb-203">Selecione Olá **Guardar chave privada** botão.</span><span class="sxs-lookup"><span data-stu-id="827bb-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="827bb-204">Ignorar o aviso de Olá que aparece e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="827bb-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Captura de ecrã da página de gerador de chave PuTTY Olá](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="827bb-206">Na sua VM, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="827bb-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="827bb-207">Crie um ficheiro denominado **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="827bb-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="827bb-208">Cole o conteúdo de Olá da chave de Olá neste ficheiro e, em seguida, guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="827bb-209">chave de Olá tem de conter a cadeia de Olá `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="827bb-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="827bb-210">Além disso, os conteúdos de Olá da chave de Olá tem de ser uma única linha de texto.</span><span class="sxs-lookup"><span data-stu-id="827bb-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="827bb-211">Inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="827bb-211">Start PuTTY.</span></span> <span data-ttu-id="827bb-212">No Olá **categoria** painel, selecione **ligação** > **SSH** > **Auth**. No Olá **ficheiro de chave privada para autenticação** caixa, navegue toohello chave que gerou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="827bb-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Captura de ecrã da página de definir a chave privada Olá](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="827bb-214">No Olá **categoria** painel, selecione **ligação** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="827bb-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="827bb-215">Em seguida, selecione Olá **reencaminhamento de X11 de ativar** caixa.</span><span class="sxs-lookup"><span data-stu-id="827bb-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Captura de ecrã da página de ativar X11 Olá](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="827bb-217">No Olá **categoria** painel, vá demasiado**sessão**.</span><span class="sxs-lookup"><span data-stu-id="827bb-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="827bb-218">Introduza as informações do anfitrião Olá e, em seguida, selecione **abra**.</span><span class="sxs-lookup"><span data-stu-id="827bb-218">Enter hello host information, and then select **Open**.</span></span>

  ![Captura de ecrã da página de sessão de Olá](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="827bb-220">Instalar software Golden porta</span><span class="sxs-lookup"><span data-stu-id="827bb-220">Install Golden Gate software</span></span>

<span data-ttu-id="827bb-221">tooinstall Oracle Golden porta, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="827bb-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="827bb-222">Inicie sessão como oracle.</span><span class="sxs-lookup"><span data-stu-id="827bb-222">Sign in as oracle.</span></span> <span data-ttu-id="827bb-223">(Deve ser capaz de toosign sem pedidos para uma palavra-passe). Certifique-se de que Xming está em execução antes de iniciar a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="827bb-224">Selecione 'GoldenGate Oracle para a base de dados Oracle 12c'.</span><span class="sxs-lookup"><span data-stu-id="827bb-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="827bb-225">Em seguida, selecione **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="827bb-225">Then select **Next** toocontinue.</span></span>

  ![Captura de ecrã da página de instalação selecionar instalador Olá](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="827bb-227">Alterar a localização do software de Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-227">Change hello software location.</span></span> <span data-ttu-id="827bb-228">Em seguida, selecione Olá **iniciar o Gestor de** caixa e introduza a localização da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="827bb-229">Selecione **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="827bb-229">Select **Next** toocontinue.</span></span>

  ![Captura de ecrã da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="827bb-231">Alterar o diretório de inventário de Olá e, em seguida, selecione **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="827bb-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Captura de ecrã da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="827bb-233">No Olá **resumo** ecrã, selecione **instalar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="827bb-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Captura de ecrã da página de instalação selecionar instalador Olá](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="827bb-235">Poderá ser pedido toorun um script como 'raiz'.</span><span class="sxs-lookup"><span data-stu-id="827bb-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="827bb-236">Se assim for, abra uma sessão separada, ssh toohello VM, tooroot de sudo e, em seguida, execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="827bb-237">Selecione **OK** continuar.</span><span class="sxs-lookup"><span data-stu-id="827bb-237">Select **OK** continue.</span></span>

  ![Captura de ecrã da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="827bb-239">Quando concluir a instalação de Olá, selecione **fechar** processo de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="827bb-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Captura de ecrã da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="827bb-241">Configurar o serviço em myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="827bb-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="827bb-242">Criar ou atualizar o ficheiro de tnsnames.ora Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="827bb-243">Crie Olá Golden porta contas de proprietário e utilizador.</span><span class="sxs-lookup"><span data-stu-id="827bb-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="827bb-244">conta de proprietário de Olá deve ter o prefixo de C# #.</span><span class="sxs-lookup"><span data-stu-id="827bb-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="827bb-245">Crie conta de utilizador de teste de porta de Golden Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="827bb-246">Configure o ficheiro de parâmetros de extrair Olá.</span><span class="sxs-lookup"><span data-stu-id="827bb-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="827bb-247">Inicie a interface de linha de comandos de porta dourada Olá (ggsci):</span><span class="sxs-lookup"><span data-stu-id="827bb-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="827bb-248">Adicione Olá seguinte ficheiro de parâmetros de EXTRAIR toohello (utilizando os comandos de vi).</span><span class="sxs-lookup"><span data-stu-id="827bb-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="827bb-249">Chave de Esc prima, ': wq!'</span><span class="sxs-lookup"><span data-stu-id="827bb-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="827bb-250">ficheiro toosave.</span><span class="sxs-lookup"><span data-stu-id="827bb-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="827bb-251">Registar extraia - extrair integrada:</span><span class="sxs-lookup"><span data-stu-id="827bb-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="827bb-252">Configurar pontos de verificação de extração e iniciar extrair em tempo real:</span><span class="sxs-lookup"><span data-stu-id="827bb-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="827bb-253">Neste passo, encontrará Olá iniciar SCN, que será utilizado posteriormente, numa secção diferentes:</span><span class="sxs-lookup"><span data-stu-id="827bb-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="827bb-254">Configurar o serviço no myVM2 (replicar)</span><span class="sxs-lookup"><span data-stu-id="827bb-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="827bb-255">Criar ou atualizar o ficheiro de tnsnames.ora Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="827bb-256">Crie uma conta de replicar:</span><span class="sxs-lookup"><span data-stu-id="827bb-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="827bb-257">Crie uma conta de utilizador de teste Golden porta:</span><span class="sxs-lookup"><span data-stu-id="827bb-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="827bb-258">REPLICAT parâmetro tooreplicate as alterações ao ficheiro:</span><span class="sxs-lookup"><span data-stu-id="827bb-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="827bb-259">Conteúdo do ficheiro de parâmetros REPORA:</span><span class="sxs-lookup"><span data-stu-id="827bb-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="827bb-260">Configure um ponto de verificação replicat:</span><span class="sxs-lookup"><span data-stu-id="827bb-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="827bb-261">Configurar a replicação de Olá (myVM1 e myVM2)</span><span class="sxs-lookup"><span data-stu-id="827bb-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="827bb-262">1. Configurar a replicação de Olá myVM2 (replicar)</span><span class="sxs-lookup"><span data-stu-id="827bb-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="827bb-263">Atualize o ficheiro de Olá com seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="827bb-264">Em seguida, reinicie o serviço do Gestor de Olá:</span><span class="sxs-lookup"><span data-stu-id="827bb-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="827bb-265">2. Configurar a replicação de Olá myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="827bb-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="827bb-266">Inicie o carregamento inicial Olá e verifique a existência de erros:</span><span class="sxs-lookup"><span data-stu-id="827bb-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="827bb-267">3. Configurar a replicação de Olá myVM2 (replicar)</span><span class="sxs-lookup"><span data-stu-id="827bb-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="827bb-268">Alterar Olá número SCN com o número de Olá que obteve anteriormente:</span><span class="sxs-lookup"><span data-stu-id="827bb-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="827bb-269">replicação de Olá foi iniciada e pode testá-lo através da inserção de novas tabelas de tooTEST de registos.</span><span class="sxs-lookup"><span data-stu-id="827bb-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="827bb-270">Ver tarefa e o estado de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="827bb-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="827bb-271">Ver relatórios</span><span class="sxs-lookup"><span data-stu-id="827bb-271">View reports</span></span>
<span data-ttu-id="827bb-272">os relatórios de tooview no myVM1, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="827bb-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="827bb-273">os relatórios de tooview no myVM2, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="827bb-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="827bb-274">Ver estado e histórico</span><span class="sxs-lookup"><span data-stu-id="827bb-274">View status and history</span></span>
<span data-ttu-id="827bb-275">tooview estado e histórico em myVM1, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="827bb-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="827bb-276">tooview estado e histórico em myVM2, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="827bb-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="827bb-277">Esta ação conclui a instalação de Olá e a configuração da porta Golden no Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="827bb-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="827bb-278">Eliminar a máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="827bb-278">Delete hello virtual machine</span></span>

<span data-ttu-id="827bb-279">Quando este já não é necessário, Olá os seguintes comandos pode ser grupo de recursos de Olá tooremove utilizado, VM e relacionados todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="827bb-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="827bb-280">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="827bb-280">Next steps</span></span>

[<span data-ttu-id="827bb-281">Tutorial sobre a criação de máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="827bb-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="827bb-282">Explorar amostras de CLI de implementação de VM</span><span class="sxs-lookup"><span data-stu-id="827bb-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
