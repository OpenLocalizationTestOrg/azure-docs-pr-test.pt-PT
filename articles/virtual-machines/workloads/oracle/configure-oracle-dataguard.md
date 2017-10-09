---
title: "aaaImplement Oracle Data Guard numa máquina virtual com Linux do Azure | Microsoft Docs"
description: "Obter rapidamente Oracle Data Guard cópias de segurança e em execução no seu ambiente do Azure."
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="8cbcc-103">Implementar o Oracle Data Guard numa máquina virtual com Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbcc-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="8cbcc-104">CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="8cbcc-105">Este artigo descreve como toouse CLI do Azure toodeploy uma base de dados Oracle 12c da base de dados Olá Azure imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="8cbcc-106">Este artigo, em seguida, mostra-lhe, passo a passo, como tooinstall e configurar a proteção de dados numa máquina virtual do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="8cbcc-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="8cbcc-107">Antes de começar, certifique-se de que a CLI do Azure está instalado.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="8cbcc-108">Para obter mais informações, consulte Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8cbcc-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="8cbcc-109">Preparar o ambiente de Olá</span><span class="sxs-lookup"><span data-stu-id="8cbcc-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="8cbcc-110">Pressupostos</span><span class="sxs-lookup"><span data-stu-id="8cbcc-110">Assumptions</span></span>

<span data-ttu-id="8cbcc-111">tooinstall Oracle Data Guard, terá de VMs do Azure toocreate dois Olá mesmo conjunto de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="8cbcc-112">Olá VM principal (myVM1) tem uma instância de Oracle em execução.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="8cbcc-113">Olá que VM em modo de espera (myVM2) tem o software de Oracle de Olá instalado apenas.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="8cbcc-114">Olá imagem do Marketplace que utilize toocreate Olá VMs é Oracle: Oracle-base de dados-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="8cbcc-115">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="8cbcc-115">Sign in tooAzure</span></span> 

<span data-ttu-id="8cbcc-116">Inicie sessão tooyour subscrição do Azure utilizando Olá [início de sessão az](/cli/azure/#login) de comandos e siga Olá no ecrã de instruções.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="8cbcc-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8cbcc-117">Create a resource group</span></span>

<span data-ttu-id="8cbcc-118">Criar um grupo de recursos utilizando Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8cbcc-119">Um grupo de recursos do Azure é um contentor lógico na qual os recursos são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8cbcc-120">Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `westus` localização:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="8cbcc-121">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="8cbcc-121">Create an availability set</span></span>

<span data-ttu-id="8cbcc-122">Criar um conjunto de disponibilidade é opcional, mas é recomendada.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="8cbcc-123">Para obter mais informações, consulte [diretrizes de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="8cbcc-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="8cbcc-124">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8cbcc-124">Create a virtual machine</span></span>

<span data-ttu-id="8cbcc-125">Criar uma VM utilizando Olá [az vm criar](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="8cbcc-126">Olá exemplo seguinte cria duas VMs com o nome `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="8cbcc-127">Também cria chaves SSH, se estes ainda não existir numa localização chave predefinido.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="8cbcc-128">toouse específicos de um conjunto de chaves, utilize Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="8cbcc-129">Crie myVM1 (principal):</span><span class="sxs-lookup"><span data-stu-id="8cbcc-129">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="8cbcc-130">Depois de criar Olá VM, a CLI do Azure mostra informações toohello semelhante seguinte o exemplo.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="8cbcc-131">Tenha em atenção o valor Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="8cbcc-132">Utilize este Olá tooaccess de endereço VM.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="8cbcc-133">Criar myVM2 (modo de espera):</span><span class="sxs-lookup"><span data-stu-id="8cbcc-133">Create myVM2 (standby):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="8cbcc-134">Tenha em atenção o valor Olá `publicIpAddress` depois de criar myVM2.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="8cbcc-135">Abra a porta TCP Olá conectividade</span><span class="sxs-lookup"><span data-stu-id="8cbcc-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="8cbcc-136">Este passo configura pontos finais externos, que permite que a base de dados do acesso remoto toohello Oracle.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="8cbcc-137">Abra a porta de Olá para myVM1:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="8cbcc-138">resultado de Olá deverá ter um aspeto semelhante toohello seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="8cbcc-139">Abra a porta de Olá para myVM2:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="8cbcc-140">Ligar a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="8cbcc-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="8cbcc-141">Toocreate uma sessão SSH com a máquina virtual de Olá de comando seguinte Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="8cbcc-142">Substitua o endereço IP Olá Olá `publicIpAddress` valor para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="8cbcc-143">Criar base de dados de Olá myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="8cbcc-144">Olá Oracle software já está instalada na imagem do Marketplace Olá, pelo que o passo seguinte Olá é a base de dados do tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="8cbcc-145">Superutilizador do comutador toohello Oracle:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="8cbcc-146">Crie base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-146">Create hello database:</span></span>

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
<span data-ttu-id="8cbcc-147">Saídas deverá ter um aspeto semelhante toohello seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-147">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="8cbcc-148">Definir variáveis ORACLE_SID e ORACLE_HOME Olá:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="8cbcc-149">Opcionalmente, pode adicionar ORACLE_HOME e ORACLE_SID toohello /home/oracle/.bashrc o ficheiro, para que estas definições são guardadas para consulta futuros inícios de sessão:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="8cbcc-150">Configurar a proteção de dados</span><span class="sxs-lookup"><span data-stu-id="8cbcc-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="8cbcc-151">Ativar o modo de registo de arquivo em myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="8cbcc-152">Ativar o registo de imposição e certifique-se, pelo menos, um ficheiro de registo está presente:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="8cbcc-153">Crie registos de Refazer em modo de espera:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="8cbcc-154">Ativar Flashback (que facilita a recuperação muito) e defina o modo de ESPERA\_ficheiro\_tooauto de gestão.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="8cbcc-155">Sair SQL * Plus depois disso.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="8cbcc-156">Configurar o serviço em myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="8cbcc-157">Editar ou criar o ficheiro de tnsnames.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8cbcc-158">Adicione Olá seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-158">Add hello following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="8cbcc-159">Editar ou criar o ficheiro de listener.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8cbcc-160">Adicione Olá seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-160">Add hello following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="8cbcc-161">Ative o Mediador de proteção de dados:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="8cbcc-162">Inicie o serviço de escuta de Olá:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="8cbcc-163">Configurar o serviço no myVM2 (modo de espera)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="8cbcc-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="8cbcc-165">Inicie sessão como Oracle:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="8cbcc-166">Editar ou criar o ficheiro de tnsnames.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8cbcc-167">Adicione Olá seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-167">Add hello following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="8cbcc-168">Editar ou criar o ficheiro de listener.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8cbcc-169">Adicione Olá seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-169">Add hello following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="8cbcc-170">Inicie o serviço de escuta de Olá:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="8cbcc-171">Restaurar Olá toomyVM2 de base de dados (modo de espera)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="8cbcc-172">Crie Olá parâmetro ficheiro /tmp/initcdb1_stby.ora com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="8cbcc-173">Crie pastas:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="8cbcc-174">Crie um ficheiro de palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="8cbcc-175">Iniciar a base de dados de Olá no myVM2:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="8cbcc-176">Restaure a base de dados de Olá utilizando Olá RMAN ferramenta:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="8cbcc-177">Execute os seguintes comandos no RMAN de Olá:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="8cbcc-178">Deverá ver o seguinte de toohello semelhante mensagens aquando da conclusão do comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="8cbcc-179">Saída RMAN.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="8cbcc-180">Opcionalmente, pode adicionar ORACLE_HOME e ORACLE_SID toohello /home/oracle/.bashrc o ficheiro, para que estas definições são guardadas para consulta futuros inícios de sessão:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="8cbcc-181">Ative o Mediador de proteção de dados:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="8cbcc-182">Configure o Mediador de proteção de dados no myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="8cbcc-183">Inicie o Gestor de proteção de dados e inicie sessão utilizando SYS e uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="8cbcc-184">(Não utilize a autenticação de SO.) Execute o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-184">(Do not use OS authentication.) Perform hello following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="8cbcc-185">Configuração de Olá de revisão:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-185">Review hello configuration:</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="8cbcc-186">Concluiu o programa de configuração do Olá Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="8cbcc-187">secção seguinte Olá mostra-lhe como tootest Olá conectividade e de comutador.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="8cbcc-188">Ligar a base de dados de Olá da máquina do cliente de Olá</span><span class="sxs-lookup"><span data-stu-id="8cbcc-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="8cbcc-189">Atualizar ou criar Olá tnsnames.ora ficheiro no seu computador cliente.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="8cbcc-190">Este ficheiro, geralmente, está a ser $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="8cbcc-191">Substitua os endereços IP Olá com o seu `publicIpAddress` valores para myVM1 e myVM2:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="8cbcc-192">Iniciar o SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="8cbcc-193">Configuração de proteção de dados de Olá de teste</span><span class="sxs-lookup"><span data-stu-id="8cbcc-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="8cbcc-194">Mude ao longo da base de dados Olá no myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="8cbcc-195">tooswitch do primário toostandby (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="8cbcc-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="8cbcc-196">Pode agora ligar-se em modo de espera toohello de base de dados.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="8cbcc-197">Iniciar o SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="8cbcc-198">Mude ao longo da base de dados Olá no myVM2 (modo de espera)</span><span class="sxs-lookup"><span data-stu-id="8cbcc-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="8cbcc-199">tooswitch ativação pós-falha, execute o seguinte Olá no myVM2:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-199">tooswitch over, run hello following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="8cbcc-200">Novamente, deve ser agora a base de dados primária tooconnect capaz de toohello.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="8cbcc-201">Iniciar o SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="8cbcc-202">Concluiu a instalação de Olá e a configuração da proteção de dados no Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="8cbcc-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="8cbcc-203">Eliminar a máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="8cbcc-203">Delete hello virtual machine</span></span>

<span data-ttu-id="8cbcc-204">Quando já não precisar hello VM, pode utilizar Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbcc-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8cbcc-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8cbcc-205">Next steps</span></span>

[<span data-ttu-id="8cbcc-206">Tutorial: Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="8cbcc-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="8cbcc-207">Explorar amostras de CLI do Azure de implementação de VM</span><span class="sxs-lookup"><span data-stu-id="8cbcc-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
