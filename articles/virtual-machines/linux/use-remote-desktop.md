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
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="dc6c6-103">Instalar e configurar o ambiente de trabalho remoto tooconnect tooa VM com Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="dc6c6-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="dc6c6-104">Máquinas de virtuais (VMs) com Linux no Azure, normalmente, são geridas Olá linha de comandos utilizando uma ligação secure shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="dc6c6-105">Quando tooLinux novo, ou para cenários de resolução de problemas rápidos, utilize Olá de ambiente de trabalho remoto pode ser mais fácil.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="dc6c6-106">Este artigo detalhes como tooinstall e configurar um ambiente de trabalho ([xfce](https://www.xfce.org)) e o ambiente de trabalho remoto ([xrdp](http://www.xrdp.org)) para a VM com Linux utilizando o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="dc6c6-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dc6c6-107">Prerequisites</span></span>
<span data-ttu-id="dc6c6-108">Este artigo requer uma VM com Linux existente no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="dc6c6-109">Se precisar de toocreate uma VM, utilize um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="dc6c6-110">Olá [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="dc6c6-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="dc6c6-111">Olá [portal do Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="dc6c6-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="dc6c6-112">Instalar um ambiente de trabalho na sua VM do Linux</span><span class="sxs-lookup"><span data-stu-id="dc6c6-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="dc6c6-113">A maioria das VMs com Linux no Azure não dispõe de um ambiente de trabalho instalado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="dc6c6-114">VMs com Linux normalmente são geridas através de ligações SSH em vez de um ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="dc6c6-115">Existem vários ambientes de trabalho no Linux que pode escolher.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="dc6c6-116">Dependendo da sua escolha de ambiente de trabalho, este pode consumir um too2 GB de espaço em disco e demorar 5 tooinstall de minutos too10 e configurar todos os pacotes de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="dc6c6-117">Olá exemplo seguinte instala lightweight Olá [xfce4](https://www.xfce.org/) ambiente de trabalho numa VM com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="dc6c6-118">Os comandos para outras distribuições variam ligeiramente (utilizar `yum` tooinstall no Red Hat Enterprise Linux e configurar adequado `selinux` regras ou utilize `zypper` tooinstall no SUSE, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="dc6c6-119">Primeiro, SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="dc6c6-120">Olá exemplo seguinte liga toohello VM com o nome *myvm.westus.cloudapp.azure.com* Olá nome de utilizador do *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="dc6c6-121">Se estiver a utilizar o Windows e precisar de mais informações sobre como utilizar o SSH, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="dc6c6-122">Em seguida, instale xfce utilizando `apt` da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="dc6c6-123">Instalar e configurar um servidor de ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="dc6c6-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="dc6c6-124">Agora que tem instalado um ambiente de trabalho, configure um toolisten do serviço de ambiente de trabalho remoto para ligações de entrada.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="dc6c6-125">[xrdp](http://xrdp.org) é um servidor de protocolo RDP (Remote Desktop Protocol) de open source para que não está disponível na maioria das distribuições de Linux e funciona bem com xfce.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="dc6c6-126">Instale xrdp a VM com Ubuntu da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="dc6c6-127">Indique xrdp que toouse de ambiente de trabalho quando iniciar a sessão.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="dc6c6-128">Configure xrdp toouse xfce como o seu ambiente de trabalho da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="dc6c6-129">Reinicie o serviço de xrdp de Olá para Olá alterações tootake efeito da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="dc6c6-130">Definir uma palavra-passe da conta de utilizador local</span><span class="sxs-lookup"><span data-stu-id="dc6c6-130">Set a local user account password</span></span>
<span data-ttu-id="dc6c6-131">Se tiver criado uma palavra-passe para a sua conta de utilizador quando criou a VM, ignore este passo.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="dc6c6-132">Se utilizar a autenticação de chave SSH apenas e não dispõe de uma palavra-passe de conta local definido, especifique uma palavra-passe antes de utilizar xrdp toolog na tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="dc6c6-133">xrdp não pode aceitar chaves SSH para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="dc6c6-134">Olá seguinte exemplo Especifica uma palavra-passe da conta de utilizador Olá *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="dc6c6-135">Especificar uma palavra-passe não atualizar os inícios de sessão de palavra-passe de toopermit de configuração do SSHD se atualmente não existir.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="dc6c6-136">Numa perspetiva de segurança, poderá desejar tooconnect tooyour VM com um túnel SSH através da autenticação baseada em chave e, em seguida, ligar tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="dc6c6-137">Se assim for, ignore Olá seguir passo sobre como criar um segurança grupo regra tooallow remoto ambiente de trabalho tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="dc6c6-138">Criar uma regra de grupo de segurança de rede para tráfego de ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="dc6c6-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="dc6c6-139">tooreach de tráfego de ambiente de trabalho remoto tooallow na VM com Linux, uma regra de grupo de segurança de rede necessita de toobe criado que permite o TCP na porta tooreach 3389 a VM.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="dc6c6-140">Para obter mais informações sobre regras do grupo de segurança de rede, consulte [que é um grupo de segurança de rede?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="dc6c6-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="dc6c6-141">Também pode [utilize Olá toocreate portal do Azure, uma regra de grupo de segurança de rede](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dc6c6-142">Olá exemplos seguintes criar uma regra de grupo de segurança de rede com [criar regras de nsg az rede](/cli/azure/network/nsg/rule#create) denominado *myNetworkSecurityGroupRule* demasiado*permitir* tráfego na *tcp* porta *3389*.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="dc6c6-143">Ligar a VM com Linux com um cliente de ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="dc6c6-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="dc6c6-144">Abra o seu cliente de ambiente de trabalho remoto local e ligue toohello endereço IP ou nome DNS da sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="dc6c6-145">Introduza Olá nome de utilizador e palavra-passe da conta de utilizador Olá na sua VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Ligar tooxrdp utilizando o cliente de ambiente de trabalho remoto](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="dc6c6-147">Após a autenticação, o ambiente de trabalho do Olá xfce irá carregar e ter um aspeto semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![ambiente de trabalho xfce através de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="dc6c6-149">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="dc6c6-149">Troubleshoot</span></span>
<span data-ttu-id="dc6c6-150">Se não conseguir ligar tooyour VM com Linux utilizando um cliente de ambiente de trabalho remoto, utilize `netstat` no seu tooverify de VM com Linux que a VM está à escuta para ligações RDP da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="dc6c6-151">Olá seguinte exemplo mostra Olá VM está a escutar a porta TCP 3389 conforme esperado:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="dc6c6-152">Se o serviço de xrdp Olá não está a escutar, numa VM com Ubuntu reinicie serviço Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="dc6c6-153">Reveja os registos na */var/registo*Thug na VM com Ubuntu indicações como serviço de Olá toowhy pode não estar a responder.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="dc6c6-154">Também pode monitorizar Olá syslog durante um tooview de tentativa de ligação de ambiente de trabalho remoto erros:</span><span class="sxs-lookup"><span data-stu-id="dc6c6-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="dc6c6-155">Outras as distribuições do Linux, tais como Red Hat Enterprise Linux e SUSE podem ter os serviços de toorestart de diferentes formas e tooreview de localizações de ficheiro de registo alternativo.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="dc6c6-156">Se não recebeu qualquer resposta no seu cliente de ambiente de trabalho remoto e não vir quaisquer eventos no registo do sistema de Olá, este comportamento indica que o tráfego de ambiente de trabalho remoto não é possível contactar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="dc6c6-157">Reveja a sua rede segurança grupo regras tooensure que tem uma regra toopermit TCP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="dc6c6-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="dc6c6-158">Para obter mais informações, consulte [resolver problemas de conectividade de aplicação](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="dc6c6-159">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dc6c6-159">Next steps</span></span>
<span data-ttu-id="dc6c6-160">Para obter mais informações sobre como criar e utilizar chaves SSH com VMs com Linux, consulte [criar SSH chaves para VMs com Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="dc6c6-161">Para obter informações sobre como utilizar o SSH do Windows, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="dc6c6-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

