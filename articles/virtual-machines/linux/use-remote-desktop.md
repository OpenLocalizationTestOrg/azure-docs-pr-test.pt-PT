---
title: ambiente de trabalho remoto de aaaUse tooa VM com Linux no Azure | Microsoft Docs
description: "Saiba como tooinstall e configurar o ambiente de trabalho remoto (xrdp) tooconnect tooa VM com Linux no Azure com as ferramentas gráficas"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Instalar e configurar o ambiente de trabalho remoto tooconnect tooa VM com Linux no Azure
Máquinas de virtuais (VMs) com Linux no Azure, normalmente, são geridas Olá linha de comandos utilizando uma ligação secure shell (SSH). Quando tooLinux novo, ou para cenários de resolução de problemas rápidos, utilize Olá de ambiente de trabalho remoto pode ser mais fácil. Este artigo detalhes como tooinstall e configurar um ambiente de trabalho ([xfce](https://www.xfce.org)) e o ambiente de trabalho remoto ([xrdp](http://www.xrdp.org)) para a VM com Linux utilizando o modelo de implementação do Resource Manager Olá.


## <a name="prerequisites"></a>Pré-requisitos
Este artigo requer uma VM com Linux existente no Azure. Se precisar de toocreate uma VM, utilize um dos seguintes métodos de Olá:

- Olá [Azure CLI 2.0](quick-create-cli.md)
- Olá [portal do Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Instalar um ambiente de trabalho na sua VM do Linux
A maioria das VMs com Linux no Azure não dispõe de um ambiente de trabalho instalado por predefinição. VMs com Linux normalmente são geridas através de ligações SSH em vez de um ambiente de trabalho. Existem vários ambientes de trabalho no Linux que pode escolher. Dependendo da sua escolha de ambiente de trabalho, este pode consumir um too2 GB de espaço em disco e demorar 5 tooinstall de minutos too10 e configurar todos os pacotes de Olá necessário.

Olá exemplo seguinte instala lightweight Olá [xfce4](https://www.xfce.org/) ambiente de trabalho numa VM com Ubuntu. Os comandos para outras distribuições variam ligeiramente (utilizar `yum` tooinstall no Red Hat Enterprise Linux e configurar adequado `selinux` regras ou utilize `zypper` tooinstall no SUSE, por exemplo).

Primeiro, SSH tooyour VM. Olá exemplo seguinte liga toohello VM com o nome *myvm.westus.cloudapp.azure.com* Olá nome de utilizador do *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Se estiver a utilizar o Windows e precisar de mais informações sobre como utilizar o SSH, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).

Em seguida, instale xfce utilizando `apt` da seguinte forma:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Instalar e configurar um servidor de ambiente de trabalho remoto
Agora que tem instalado um ambiente de trabalho, configure um toolisten do serviço de ambiente de trabalho remoto para ligações de entrada. [xrdp](http://xrdp.org) é um servidor de protocolo RDP (Remote Desktop Protocol) de open source para que não está disponível na maioria das distribuições de Linux e funciona bem com xfce. Instale xrdp a VM com Ubuntu da seguinte forma:

```bash
sudo apt-get install xrdp
```

Indique xrdp que toouse de ambiente de trabalho quando iniciar a sessão. Configure xrdp toouse xfce como o seu ambiente de trabalho da seguinte forma:

```bash
echo xfce4-session >~/.xsession
```

Reinicie o serviço de xrdp de Olá para Olá alterações tootake efeito da seguinte forma:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Definir uma palavra-passe da conta de utilizador local
Se tiver criado uma palavra-passe para a sua conta de utilizador quando criou a VM, ignore este passo. Se utilizar a autenticação de chave SSH apenas e não dispõe de uma palavra-passe de conta local definido, especifique uma palavra-passe antes de utilizar xrdp toolog na tooyour VM. xrdp não pode aceitar chaves SSH para a autenticação. Olá seguinte exemplo Especifica uma palavra-passe da conta de utilizador Olá *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Especificar uma palavra-passe não atualizar os inícios de sessão de palavra-passe de toopermit de configuração do SSHD se atualmente não existir. Numa perspetiva de segurança, poderá desejar tooconnect tooyour VM com um túnel SSH através da autenticação baseada em chave e, em seguida, ligar tooxrdp. Se assim for, ignore Olá seguir passo sobre como criar um segurança grupo regra tooallow remoto ambiente de trabalho tráfego de rede.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Criar uma regra de grupo de segurança de rede para tráfego de ambiente de trabalho remoto
tooreach de tráfego de ambiente de trabalho remoto tooallow na VM com Linux, uma regra de grupo de segurança de rede necessita de toobe criado que permite o TCP na porta tooreach 3389 a VM. Para obter mais informações sobre regras do grupo de segurança de rede, consulte [que é um grupo de segurança de rede?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Também pode [utilize Olá toocreate portal do Azure, uma regra de grupo de segurança de rede](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Olá exemplos seguintes criar uma regra de grupo de segurança de rede com [criar regras de nsg az rede](/cli/azure/network/nsg/rule#create) denominado *myNetworkSecurityGroupRule* demasiado*permitir* tráfego na *tcp* porta *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Ligar a VM com Linux com um cliente de ambiente de trabalho remoto
Abra o seu cliente de ambiente de trabalho remoto local e ligue toohello endereço IP ou nome DNS da sua VM do Linux. Introduza Olá nome de utilizador e palavra-passe da conta de utilizador Olá na sua VM da seguinte forma:

![Ligar tooxrdp utilizando o cliente de ambiente de trabalho remoto](./media/use-remote-desktop/remote-desktop-client.png)

Após a autenticação, o ambiente de trabalho do Olá xfce irá carregar e ter um aspeto semelhante toohello seguinte exemplo:

![ambiente de trabalho xfce através de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Resolução de problemas
Se não conseguir ligar tooyour VM com Linux utilizando um cliente de ambiente de trabalho remoto, utilize `netstat` no seu tooverify de VM com Linux que a VM está à escuta para ligações RDP da seguinte forma:

```bash
sudo netstat -plnt | grep rdp
```

Olá seguinte exemplo mostra Olá VM está a escutar a porta TCP 3389 conforme esperado:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Se o serviço de xrdp Olá não está a escutar, numa VM com Ubuntu reinicie serviço Olá da seguinte forma:

```bash
sudo service xrdp restart
```

Reveja os registos na */var/registo*Thug na VM com Ubuntu indicações como serviço de Olá toowhy pode não estar a responder. Também pode monitorizar Olá syslog durante um tooview de tentativa de ligação de ambiente de trabalho remoto erros:

```bash
tail -f /var/log/syslog
```

Outras as distribuições do Linux, tais como Red Hat Enterprise Linux e SUSE podem ter os serviços de toorestart de diferentes formas e tooreview de localizações de ficheiro de registo alternativo.

Se não recebeu qualquer resposta no seu cliente de ambiente de trabalho remoto e não vir quaisquer eventos no registo do sistema de Olá, este comportamento indica que o tráfego de ambiente de trabalho remoto não é possível contactar Olá VM. Reveja a sua rede segurança grupo regras tooensure que tem uma regra toopermit TCP na porta 3389. Para obter mais informações, consulte [resolver problemas de conectividade de aplicação](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre como criar e utilizar chaves SSH com VMs com Linux, consulte [criar SSH chaves para VMs com Linux no Azure](mac-create-ssh-keys.md).

Para obter informações sobre como utilizar o SSH do Windows, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).

