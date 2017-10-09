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
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Implementar o Oracle Data Guard numa máquina virtual com Linux do Azure 

CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts. Este artigo descreve como toouse CLI do Azure toodeploy uma base de dados Oracle 12c da base de dados Olá Azure imagem do Marketplace. Este artigo, em seguida, mostra-lhe, passo a passo, como tooinstall e configurar a proteção de dados numa máquina virtual do Azure (VM).

Antes de começar, certifique-se de que a CLI do Azure está instalado. Para obter mais informações, consulte Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparar o ambiente de Olá
### <a name="assumptions"></a>Pressupostos

tooinstall Oracle Data Guard, terá de VMs do Azure toocreate dois Olá mesmo conjunto de disponibilidade:

- Olá VM principal (myVM1) tem uma instância de Oracle em execução.
- Olá que VM em modo de espera (myVM2) tem o software de Oracle de Olá instalado apenas.

Olá imagem do Marketplace que utilize toocreate Olá VMs é Oracle: Oracle-base de dados-Ee:12.1.0.2:latest.

### <a name="sign-in-tooazure"></a>Inicie sessão no tooAzure 

Inicie sessão tooyour subscrição do Azure utilizando Olá [início de sessão az](/cli/azure/#login) de comandos e siga Olá no ecrã de instruções.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos utilizando Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contentor lógico na qual os recursos são implementados e geridos. 

Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `westus` localização:

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade

Criar um conjunto de disponibilidade é opcional, mas é recomendada. Para obter mais informações, consulte [diretrizes de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

Criar uma VM utilizando Olá [az vm criar](/cli/azure/vm#create) comando. 

Olá exemplo seguinte cria duas VMs com o nome `myVM1` e `myVM2`. Também cria chaves SSH, se estes ainda não existir numa localização chave predefinido. toouse específicos de um conjunto de chaves, utilize Olá `--ssh-key-value` opção.

Crie myVM1 (principal):
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

Depois de criar Olá VM, a CLI do Azure mostra informações toohello semelhante seguinte o exemplo. Tenha em atenção o valor Olá `publicIpAddress`. Utilize este Olá tooaccess de endereço VM.

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

Criar myVM2 (modo de espera):
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

Tenha em atenção o valor Olá `publicIpAddress` depois de criar myVM2.

### <a name="open-hello-tcp-port-for-connectivity"></a>Abra a porta TCP Olá conectividade

Este passo configura pontos finais externos, que permite que a base de dados do acesso remoto toohello Oracle.

Abra a porta de Olá para myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

resultado de Olá deverá ter um aspeto semelhante toohello seguinte resposta:

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

Abra a porta de Olá para myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Ligar a máquina virtual de toohello

Toocreate uma sessão SSH com a máquina virtual de Olá de comando seguinte Olá de utilização. Substitua o endereço IP Olá Olá `publicIpAddress` valor para a máquina virtual.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Criar base de dados de Olá myVM1 (principal)

Olá Oracle software já está instalada na imagem do Marketplace Olá, pelo que o passo seguinte Olá é a base de dados do tooinstall Olá. 

Superutilizador do comutador toohello Oracle:

```bash
$ sudo su - oracle
```

Crie base de dados de Olá:

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
Saídas deverá ter um aspeto semelhante toohello seguinte resposta:

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

Definir variáveis ORACLE_SID e ORACLE_HOME Olá:

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

Opcionalmente, pode adicionar ORACLE_HOME e ORACLE_SID toohello /home/oracle/.bashrc o ficheiro, para que estas definições são guardadas para consulta futuros inícios de sessão:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Configurar a proteção de dados

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Ativar o modo de registo de arquivo em myVM1 (principal)

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
Ativar o registo de imposição e certifique-se, pelo menos, um ficheiro de registo está presente:

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Crie registos de Refazer em modo de espera:

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

Ativar Flashback (que facilita a recuperação muito) e defina o modo de ESPERA\_ficheiro\_tooauto de gestão. Sair SQL * Plus depois disso.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>Configurar o serviço em myVM1 (principal)

Editar ou criar o ficheiro de tnsnames.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.

Adicione Olá seguintes entradas:

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

Editar ou criar o ficheiro de listener.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.

Adicione Olá seguintes entradas:

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

Ative o Mediador de proteção de dados:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Inicie o serviço de escuta de Olá:

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>Configurar o serviço no myVM2 (modo de espera)

SSH toomyVM2:

```bash 
$ ssh azureuser@<publicIpAddress>
```

Inicie sessão como Oracle:

```bash
$ sudo su - oracle
```

Editar ou criar o ficheiro de tnsnames.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.

Adicione Olá seguintes entradas:

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

Editar ou criar o ficheiro de listener.ora Olá, o que se encontra na pasta de ORACLE_HOME\network\admin Olá $.

Adicione Olá seguintes entradas:

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

Inicie o serviço de escuta de Olá:

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Restaurar Olá toomyVM2 de base de dados (modo de espera)

Crie Olá parâmetro ficheiro /tmp/initcdb1_stby.ora com Olá seguinte conteúdo:
```bash
*.db_name='cdb1'
```

Crie pastas:

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Crie um ficheiro de palavra-passe:

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Iniciar a base de dados de Olá no myVM2:

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Restaure a base de dados de Olá utilizando Olá RMAN ferramenta:

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Execute os seguintes comandos no RMAN de Olá:
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Deverá ver o seguinte de toohello semelhante mensagens aquando da conclusão do comando de Olá. Saída RMAN.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

Opcionalmente, pode adicionar ORACLE_HOME e ORACLE_SID toohello /home/oracle/.bashrc o ficheiro, para que estas definições são guardadas para consulta futuros inícios de sessão:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Ative o Mediador de proteção de dados:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Configure o Mediador de proteção de dados no myVM1 (principal)

Inicie o Gestor de proteção de dados e inicie sessão utilizando SYS e uma palavra-passe. (Não utilize a autenticação de SO.) Execute o seguinte Olá:

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

Configuração de Olá de revisão:
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

Concluiu o programa de configuração do Olá Oracle Data Guard. secção seguinte Olá mostra-lhe como tootest Olá conectividade e de comutador.

### <a name="connect-hello-database-from-hello-client-machine"></a>Ligar a base de dados de Olá da máquina do cliente de Olá

Atualizar ou criar Olá tnsnames.ora ficheiro no seu computador cliente. Este ficheiro, geralmente, está a ser $ORACLE_HOME\network\admin.

Substitua os endereços IP Olá com o seu `publicIpAddress` valores para myVM1 e myVM2:

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

Iniciar o SQL * Plus:

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>Configuração de proteção de dados de Olá de teste

### <a name="switch-over-hello-database-on-myvm1-primary"></a>Mude ao longo da base de dados Olá no myVM1 (principal)

tooswitch do primário toostandby (cdb1 toocdb1_stby):

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

Pode agora ligar-se em modo de espera toohello de base de dados.

Iniciar o SQL * Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>Mude ao longo da base de dados Olá no myVM2 (modo de espera)

tooswitch ativação pós-falha, execute o seguinte Olá no myVM2:
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

Novamente, deve ser agora a base de dados primária tooconnect capaz de toohello.

Iniciar o SQL * Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Concluiu a instalação de Olá e a configuração da proteção de dados no Oracle Linux.


## <a name="delete-hello-virtual-machine"></a>Eliminar a máquina virtual de Olá

Quando já não precisar hello VM, pode utilizar Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passos seguintes

[Tutorial: Criar máquinas virtuais altamente disponíveis](../../linux/create-cli-complete.md)

[Explorar amostras de CLI do Azure de implementação de VM](../../linux/cli-samples.md)
