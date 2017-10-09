---
title: "aaaReset palavra-passe de VM com Linux e SSH de chave de Olá CLI | Microsoft Docs"
description: "Como toouse Olá extensão VMAccess tooreset de Interface de linha de comandos do Azure (CLI) Olá uma palavra-passe de VM com Linux ou chave SSH, corrija a configuração de SSH Olá e verificar a consistência de disco"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Como tooreset uma palavra-passe de VM com Linux ou chave SSH, corrija a configuração de SSH Olá e verificação de consistência de disco com a extensão de VMAccess Olá
Se não conseguir ligar tooa máquina de virtual com Linux no Azure devido a uma palavra-passe esquecida, uma chave Secure Shell (SSH) incorreto ou um problema com a configuração de SSH Olá, utilizar Olá extensão VMAccessForLinux com palavra-passe do Olá CLI do Azure tooreset Olá ou chave SSH, corrigir Olá configuração SSH e verificação de consistência de disco. 

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Saiba como demasiado[executar estes passos, utilizando o modelo do Resource Manager Olá](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Com Olá CLI do Azure, utilizar Olá **conjunto de extensão de vm do azure** comando a partir dos seus comandos de tooaccess de interface de linha de comandos (Bash, Terminal, linha de comandos). Executar **conjunto de extensão de vm do azure ajuda** para utilização de extensão de detalhado.

Com Olá CLI do Azure, pode fazê-lo Olá seguintes tarefas:

* [Olá de reposição de palavra-passe](#pwresetcli)
* [Repor a chave SSH Olá](#sshkeyresetcli)
* [Repor Olá palavra-passe e Olá a chave SSH](#resetbothcli)
* [Criar uma nova conta de utilizador de sudo](#createnewsudocli)
* [Repor a configuração de SSH Olá](#sshconfigresetcli)
* [Eliminar um utilizador](#deletecli)
* [Apresentar o estado de Olá de Olá extensão VMAccess](#statuscli)
* [Verificação de consistência de discos adicionados](#checkdisk)
* [Reparar discos adicionados na sua VM do Linux](#repairdisk)

## <a name="prerequisites"></a>Pré-requisitos
Terá de seguinte de Olá toodo:

* Terá de demasiado[instalar Olá CLI do Azure](../../../cli-install-nodejs.md) e [ligar tooyour subscrição](../../../xplat-cli-connect.md) toouse Azure recursos associados à sua conta.
* Conjunto Olá modo correto para o modelo de implementação clássica Olá, escrevendo o seguinte Olá Olá linha de comandos:
    ``` 
        azure config mode asm
    ```
* Ter uma nova palavra-passe ou o conjunto de chaves SSH, se quiser tooreset uma. Não precisa de estes se pretender que a configuração de SSH tooreset Olá.

## <a name="pwresetcli"></a>Olá de reposição de palavra-passe
1. Crie um ficheiro no seu computador local com o nome PrivateConf.json com estas linhas. Substitua **myUserName** e  **myP@ssW0rd**  com o seu nome de utilizador e palavra-passe e definir a sua própria data de expiração.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Repor a chave SSH Olá
1. Crie um ficheiro denominado PrivateConf.json com estes conteúdos. Substitua Olá **myUserName** e **mySSHKey** valores pelas suas informações.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Repor palavra-passe de Olá e a chave SSH Olá
1. Crie um ficheiro denominado PrivateConf.json com estes conteúdos. Substitua Olá **myUserName**, **mySSHKey** e  **myP@ssW0rd**  valores pelas suas informações.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Criar uma nova conta de utilizador de sudo

Se se esquecer da sua nome de utilizador, pode utilizar VMAccess toocreate um novo com a autoridade de sudo Olá. Neste caso, Olá existente nome de utilizador e palavra-passe não será modificado.

toocreate um novo utilizador de sudo com acesso de palavra-passe, utilize Olá script no [Olá de reposição de palavra-passe](#pwresetcli) e especifique o nome de utilizador novo Olá.

toocreate um novo utilizador de sudo com acesso de chave SSH, utilize Olá script no [repor a chave SSH Olá](#sshkeyresetcli) e especifique o nome de utilizador novo Olá.

Também pode utilizar [Repor palavra-passe de Olá e a chave SSH Olá](#resetbothcli) toocreate um novo utilizador com palavra-passe e acesso de chave SSH.

## <a name="sshconfigresetcli"></a>Repor a configuração de SSH Olá
Se a configuração de SSH Olá está num estado indesejado, poderá também perder acesso toohello VM. Pode utilizar Olá VMAccess extensão tooreset Olá configuração tooits estado predefinido. toodo por isso, basta chave do tooset Olá "reset_ssh" demasiado "True". extensão de Olá irá reiniciar o servidor SSH Olá, abra a porta SSH Olá na sua VM e repor os valores de toodefault de configuração de SSH Olá. conta de utilizador Olá (nome, palavra-passe ou chaves SSH) não será alterada.

> [!NOTE]
> ficheiro de configuração de SSH Olá obtém repor está localizado em /etc/ssh/sshd_config.
> 
> 

1. Crie um ficheiro denominado PrivateConf.json com este conteúdo.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Eliminar um utilizador
Se quiser toodelete uma conta de utilizador sem iniciar sessão no toohello VM diretamente, pode utilizar este script.

1. Crie um ficheiro denominado PrivateConf.json com este conteúdo, substituindo Olá tooremove de nome de utilizador para **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Apresentar o estado de Olá de Olá extensão VMAccess
Estado de Olá toodisplay de Olá extensão VMAccess, execute este comando.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Verificação de consistência de discos adicionados
toorun ou a fsck em todos os discos na sua máquina virtual do Linux, será seguintes elementos terão toodo Olá:

1. Crie um ficheiro denominado PublicConf.json com este conteúdo. Verifique o que disco assume um valor booleano para se toocheck discos anexados a máquina virtual de tooyour ou não. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Execute este comando tooexecute, substituindo o nome de Olá da sua máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Discos de reparação
toorepair discos que não estão a montar ou que têm erros de configuração de montagem, utilize a configuração de montagem de Olá de tooreset extensão VMAccess Olá na sua máquina virtual do Linux. Substituindo o nome de Olá do disco para **myDisk**.

1. Crie um ficheiro denominado PublicConf.json com este conteúdo. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Execute este comando tooexecute, substituindo o nome de Olá da sua máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Passos seguintes
* Se quiser toouse cmdlets do Azure PowerShell ou a palavra-passe do Azure Resource Manager modelos tooreset Olá ou a chave SSH, corrija a configuração de SSH Olá e verificar a consistência de disco, consulte Olá [documentação da extensão VMAccess no GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* Também pode utilizar Olá [portal do Azure](https://portal.azure.com) palavra-passe do tooreset Olá ou chave SSH de uma VM com Linux implementados no modelo de implementação clássica Olá. Atualmente não é possível utilizar Olá efetue portal toothis para implementar uma VM com Linux no modelo de implementação do Resource Manager Olá.
* Consulte [sobre extensões de máquina virtual e funcionalidades](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre a utilização de extensões VM para máquinas virtuais do Azure.

