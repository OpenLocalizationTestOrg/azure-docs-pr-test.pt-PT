---
title: "problemas de ligação de SSH aaaTroubleshoot tooan VM do Azure | Microsoft Docs"
description: "Como tootroubleshoot problemas, tais como 'falha de ligação SSH' ou ' SSH ligação recusada' para uma VM do Azure com o Linux."
keywords: "SSH ligação recusada, ssh erro, azure ssh, ligação SSH falhou"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="4e89d-104">Resolver problemas de SSH ligações tooan VM com Linux do Azure que falhe, erros de saída, ou é recusada</span><span class="sxs-lookup"><span data-stu-id="4e89d-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="4e89d-105">Existem várias razões se encontrar erros de Secure Shell (SSH), falhas de ligação de SSH, ou SSH é recusada quando tenta tooconnect tooa máquina de virtual com Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="4e89d-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="4e89d-106">Este artigo ajuda-o a localizar e problemas de Olá correto.</span><span class="sxs-lookup"><span data-stu-id="4e89d-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="4e89d-107">Pode utilizar Olá portal do Azure, CLI do Azure ou a extensão de acesso de VM para tootroubleshoot de Linux e resolver problemas de ligação.</span><span class="sxs-lookup"><span data-stu-id="4e89d-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="4e89d-108">Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="4e89d-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="4e89d-109">Em alternativa, pode ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e89d-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="4e89d-110">Aceda toohello [site de suporte do Azure](http://azure.microsoft.com/support/options/) e selecione **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="4e89d-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="4e89d-111">Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="4e89d-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="4e89d-112">Passos rápidos de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="4e89d-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="4e89d-113">Depois de cada passo de resolução de problemas, tente restabelecer a ligação toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="4e89d-114">Repor a configuração de SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="4e89d-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="4e89d-115">Repor Olá as credenciais de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e89d-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="4e89d-116">Certifique-se Olá [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) regras permitem tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="4e89d-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="4e89d-117">Certifique-se de que o grupo de segurança de rede existe uma regra de tráfego SSH toopermit (por predefinição, a porta TCP 22).</span><span class="sxs-lookup"><span data-stu-id="4e89d-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="4e89d-118">Não é possível utilizar o redirecionamento de porta / mapeamento sem utilizar um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e89d-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="4e89d-119">Verifique Olá [estado de funcionamento de recursos VM](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e89d-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="4e89d-120">Certifique-se de que Olá VM relatórios como estando em bom estado.</span><span class="sxs-lookup"><span data-stu-id="4e89d-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="4e89d-121">Se tiver de diagnóstico de arranque ativado, certifique-se de Olá VM não está a comunicar erros de arranque nos registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e89d-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="4e89d-122">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-122">Restart hello VM.</span></span>
6. <span data-ttu-id="4e89d-123">Reimplemente Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-123">Redeploy hello VM.</span></span>

<span data-ttu-id="4e89d-124">Continue a ler para explicações e passos de resolução de problemas mais detalhados.</span><span class="sxs-lookup"><span data-stu-id="4e89d-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="4e89d-125">Problemas de ligação do métodos disponíveis tootroubleshoot SSH</span><span class="sxs-lookup"><span data-stu-id="4e89d-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="4e89d-126">Pode repor as credenciais ou configuração de SSH utilizando um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="4e89d-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="4e89d-127">[Portal do Azure](#use-the-azure-portal) - ótimo se precisar de tooquickly repor a configuração de SSH Olá ou chave SSH e não ter Olá instalar as ferramentas do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e89d-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="4e89d-128">[Azure CLI 2.0](#use-the-azure-cli-20) - se de que já está na linha de comandos Olá, rapidamente configuração de SSH Olá de reposição ou credenciais.</span><span class="sxs-lookup"><span data-stu-id="4e89d-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="4e89d-129">Também pode utilizar Olá [CLI do Azure 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="4e89d-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="4e89d-130">[Azure extensão VMAccessForLinux](#use-the-vmaccess-extension) - criar e reutilizar json definição ficheiros tooreset Olá utilizador ou de configuração de credenciais de SSH.</span><span class="sxs-lookup"><span data-stu-id="4e89d-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="4e89d-131">Depois de cada passo de resolução de problemas, tente ligar novamente tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="4e89d-132">Se ainda não é possível estabelecer ligação, repita o passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="4e89d-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="4e89d-133">Utilizar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e89d-133">Use hello Azure portal</span></span>
<span data-ttu-id="4e89d-134">Olá portal do Azure fornece um Olá tooreset de forma rápida credenciais de utilizador ou de configuração de SSH sem instalar quaisquer ferramentas no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="4e89d-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="4e89d-135">Selecione a VM Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e89d-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4e89d-136">Desloque para baixo toohello **suporte + resolução de problemas** secção e selecione **Repor palavra-passe** como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="4e89d-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Repor configuração SSH ou as credenciais no Olá portal do Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="4e89d-138">Repor a configuração de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="4e89d-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="4e89d-139">Como primeiro passo, selecione `Reset configuration only` de Olá **modo** menu pendente de Olá anterior a captura de ecrã, em seguida, clique em Olá **repor** botão.</span><span class="sxs-lookup"><span data-stu-id="4e89d-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="4e89d-140">Quando esta ação tiver sido concluída, repita tooaccess a VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="4e89d-141">Repor as credenciais de SSH para um utilizador</span><span class="sxs-lookup"><span data-stu-id="4e89d-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="4e89d-142">as credenciais de Olá tooreset de um utilizador existente, selecione `Reset SSH public key` ou `Reset password` de Olá **modo** menu pendente que aparece Olá anterior a captura de ecrã.</span><span class="sxs-lookup"><span data-stu-id="4e89d-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="4e89d-143">Especifique o nome de utilizador Olá e uma chave SSH ou nova palavra-passe, em seguida, clique em Olá **repor** botão.</span><span class="sxs-lookup"><span data-stu-id="4e89d-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="4e89d-144">Também pode criar um utilizador com privilégios sudo no Olá VM a partir deste menu.</span><span class="sxs-lookup"><span data-stu-id="4e89d-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="4e89d-145">Introduza um novo nome de utilizador e palavra-passe associada ou chave SSH e, em seguida, clique em Olá **repor** botão.</span><span class="sxs-lookup"><span data-stu-id="4e89d-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="4e89d-146">Utilizar Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e89d-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="4e89d-147">Se ainda não o fez, instale Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4e89d-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4e89d-148">Se criar e carregar uma imagem de disco do Linux personalizada, certifique-se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="4e89d-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="4e89d-149">Para VMs criadas com imagens Gallery, esta extensão de acesso já está instalado e configurado por si.</span><span class="sxs-lookup"><span data-stu-id="4e89d-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="4e89d-150">Repor configuração SSH</span><span class="sxs-lookup"><span data-stu-id="4e89d-150">Reset SSH configuration</span></span>
<span data-ttu-id="4e89d-151">Pode inicialmente tente repor Olá SSH toodefault dos valores de configuração e reiniciando Olá SSH servidor Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="4e89d-152">Tenha em atenção que isto não alterar o nome de conta de utilizador Olá, palavra-passe ou chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="4e89d-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="4e89d-153">Olá exemplo seguinte utiliza [az vm utilizador reposição-ssh](/cli/azure/vm/user#reset-ssh) tooreset Olá SSH configuração Olá VM com o nome `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-154">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="4e89d-155">Repor as credenciais de SSH para um utilizador</span><span class="sxs-lookup"><span data-stu-id="4e89d-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="4e89d-156">Olá exemplo seguinte utiliza [atualização de utilizador de vm az](/cli/azure/vm/user#update) tooreset Olá credenciais para `myUsername` toohello o valor especificado na `myPassword`, na VM com o nome de Olá `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-157">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="4e89d-158">Se utilizar a autenticação de chave SSH, pode repor a chave SSH Olá para um determinado utilizador.</span><span class="sxs-lookup"><span data-stu-id="4e89d-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="4e89d-159">Olá exemplo seguinte utiliza **az vm acesso de utilizador do linux do conjunto** tooupdate Olá SSH chave armazenada num `~/.ssh/id_rsa.pub` para com o nome de utilizador de Olá `myUsername`, na VM com o nome de Olá `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-160">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="4e89d-161">Utilizar Olá VMAccess extensão</span><span class="sxs-lookup"><span data-stu-id="4e89d-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="4e89d-162">lê Olá extensão de acesso de VM para Linux num ficheiro json que define ações toocarry enviados. Estas ações incluem repor SSHD, repor uma chave SSH ou adicionar um utilizador.</span><span class="sxs-lookup"><span data-stu-id="4e89d-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="4e89d-163">Continuar a utilizar Olá de toocall Olá CLI do Azure extensão VMAccess, mas pode reutilizar ficheiros json de Olá através de várias VMs se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="4e89d-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="4e89d-164">Esta abordagem permite-lhe toocreate um repositório de ficheiros json que pode ser chamado para fornecido cenários.</span><span class="sxs-lookup"><span data-stu-id="4e89d-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="4e89d-165">Repor SSHD</span><span class="sxs-lookup"><span data-stu-id="4e89d-165">Reset SSHD</span></span>
<span data-ttu-id="4e89d-166">Crie um ficheiro denominado `settings.json` com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="4e89d-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="4e89d-167">Utilizar Olá CLI do Azure,, em seguida, chame Olá `VMAccessForLinux` extensão tooreset a ligação de SSHD especificando o ficheiro json.</span><span class="sxs-lookup"><span data-stu-id="4e89d-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="4e89d-168">Olá exemplo seguinte utiliza [conjunto de extensão de vm az](/cli/azure/vm/extension#set) tooreset SSHD na VM com o nome de Olá `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-169">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="4e89d-170">Repor as credenciais de SSH para um utilizador</span><span class="sxs-lookup"><span data-stu-id="4e89d-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="4e89d-171">Se SSHD aparece toofunction corretamente, pode redefini Olá as credenciais para um utilizador giver.</span><span class="sxs-lookup"><span data-stu-id="4e89d-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="4e89d-172">palavra-passe Olá de tooreset para um utilizador, crie um ficheiro denominado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="4e89d-173">Olá exemplo seguinte repõe as credenciais Olá `myUsername` toohello o valor especificado na `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="4e89d-174">Introduza Olá seguintes linhas no seu `settings.json` ficheiro, utilizando os seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="4e89d-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="4e89d-175">Ou tooreset Olá chave SSH para um utilizador, primeiro crie um ficheiro denominado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="4e89d-176">Olá exemplo seguinte repõe as credenciais Olá `myUsername` toohello o valor especificado na `myPassword`, na VM com o nome de Olá `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-177">Introduza Olá seguintes linhas no seu `settings.json` ficheiro, utilizando os seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="4e89d-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="4e89d-178">Depois de criar o ficheiro json, utilize Olá do Olá CLI do Azure toocall `VMAccessForLinux` tooreset extensão, as credenciais do utilizador do SSH, especificando o ficheiro json.</span><span class="sxs-lookup"><span data-stu-id="4e89d-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="4e89d-179">Olá exemplo seguinte repõe as credenciais no Olá VM com o nome `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-180">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="4e89d-181">Utilizar Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e89d-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="4e89d-182">Se ainda não o fez, [instalar Olá CLI do Azure 1.0 e ligar tooyour subscrição do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4e89d-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="4e89d-183">Certifique-se de que estiver a utilizar o modo Resource Manager da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="4e89d-184">Se criar e carregar uma imagem de disco do Linux personalizada, certifique-se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="4e89d-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="4e89d-185">Para VMs criadas com imagens Gallery, esta extensão de acesso já está instalado e configurado por si.</span><span class="sxs-lookup"><span data-stu-id="4e89d-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="4e89d-186">Repor configuração SSH</span><span class="sxs-lookup"><span data-stu-id="4e89d-186">Reset SSH configuration</span></span>
<span data-ttu-id="4e89d-187">configuração de SSHD Olá próprio pode estar configurado incorretamente ou Olá serviço encontrou um erro.</span><span class="sxs-lookup"><span data-stu-id="4e89d-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="4e89d-188">Só pode repor SSHD toomake se configuração de SSH Olá em si é válida.</span><span class="sxs-lookup"><span data-stu-id="4e89d-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="4e89d-189">Repor SSHD deve ser Olá primeiro resolução de problemas passo que tomar.</span><span class="sxs-lookup"><span data-stu-id="4e89d-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="4e89d-190">Olá exemplo seguinte repõe SSHD numa VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-191">Utilize os seus próprios nomes de grupo de recursos e de VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="4e89d-192">Repor as credenciais de SSH para um utilizador</span><span class="sxs-lookup"><span data-stu-id="4e89d-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="4e89d-193">Se SSHD aparece toofunction corretamente, pode redefini Olá palavra-passe para um utilizador giver.</span><span class="sxs-lookup"><span data-stu-id="4e89d-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="4e89d-194">Olá exemplo seguinte repõe as credenciais Olá `myUsername` toohello o valor especificado na `myPassword`, na VM com o nome de Olá `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-195">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="4e89d-196">Se utilizar a autenticação de chave SSH, pode repor a chave SSH Olá para um determinado utilizador.</span><span class="sxs-lookup"><span data-stu-id="4e89d-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="4e89d-197">Olá seguintes atualizações de exemplo Olá SSH chave armazenada num `~/.ssh/id_rsa.pub` para com o nome de utilizador de Olá `myUsername`, na VM com o nome de Olá `myVM` no `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-198">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="4e89d-199">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="4e89d-199">Restart a VM</span></span>
<span data-ttu-id="4e89d-200">Se tiver de repor as credenciais de utilizador e a configuração de SSH do Olá ou encontrou um erro na fazê-lo, pode tentar reiniciar Olá VM tooaddress subjacente problemas de computação.</span><span class="sxs-lookup"><span data-stu-id="4e89d-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4e89d-201">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e89d-201">Azure portal</span></span>
<span data-ttu-id="4e89d-202">toorestart uma VM utilizando Olá do Azure selecione portal, a VM e clique em Olá **reiniciar** botão como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="4e89d-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Reiniciar uma VM no Olá portal do Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="4e89d-204">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e89d-204">Azure CLI 1.0</span></span>
<span data-ttu-id="4e89d-205">Olá reinícios de exemplo a seguir Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-206">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="4e89d-207">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4e89d-207">Azure CLI 2.0</span></span>
<span data-ttu-id="4e89d-208">Olá exemplo seguinte utiliza [reinício de vm az](/cli/azure/vm#restart) toorestart Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-209">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="4e89d-210">Reimplementar uma VM</span><span class="sxs-lookup"><span data-stu-id="4e89d-210">Redeploy a VM</span></span>
<span data-ttu-id="4e89d-211">Pode voltar a implementar um nó de tooanother VM no Azure, o que poderá corrigir problemas de rede subjacentes.</span><span class="sxs-lookup"><span data-stu-id="4e89d-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="4e89d-212">Para obter informações sobre voltar a implementar uma VM, consulte [Reimplementar toonew de máquina virtual do Azure nó](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e89d-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="4e89d-213">Depois de concluída esta operação, dados do disco efémeras serão perdidos e endereços IP dinâmicos que estão associados a máquina virtual de Olá serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="4e89d-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="4e89d-214">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e89d-214">Azure portal</span></span>
<span data-ttu-id="4e89d-215">tooredeploy uma VM utilizando hello do Azure selecione portal, a VM e desloque para baixo toohello **suporte + resolução de problemas** secção.</span><span class="sxs-lookup"><span data-stu-id="4e89d-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="4e89d-216">Clique em Olá **Reimplementar** botão como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="4e89d-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Volte a implementar uma VM no Olá portal do Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="4e89d-218">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e89d-218">Azure CLI 1.0</span></span>
<span data-ttu-id="4e89d-219">Olá seguir redeploys exemplo Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-220">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="4e89d-221">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4e89d-221">Azure CLI 2.0</span></span>
<span data-ttu-id="4e89d-222">Olá seguinte exemplo, utilize [volte a implementar az vm](/cli/azure/vm#redeploy) tooredeploy Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4e89d-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="4e89d-223">Utilize os seus próprios valores da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4e89d-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="4e89d-224">VMs criadas utilizando o modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="4e89d-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="4e89d-225">Repita estes passos tooresolve Olá mais comuns SSH falhas de ligação para VMs que foram criadas utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="4e89d-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="4e89d-226">Depois de cada passo, tente restabelecer a ligação toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="4e89d-227">Reponha o acesso remoto de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e89d-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e89d-228">No Olá portal do Azure, selecione a VM e clique em Olá **repor remoto...**  botão.</span><span class="sxs-lookup"><span data-stu-id="4e89d-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="4e89d-229">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4e89d-229">Restart hello VM.</span></span> <span data-ttu-id="4e89d-230">No Olá [portal do Azure](https://portal.azure.com), selecione a VM e clique em Olá **reiniciar** botão.</span><span class="sxs-lookup"><span data-stu-id="4e89d-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="4e89d-231">Reimplemente Olá VM tooa novo Azure nó.</span><span class="sxs-lookup"><span data-stu-id="4e89d-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="4e89d-232">Para obter informações sobre como tooredeploy uma VM, consulte [Reimplementar toonew de máquina virtual do Azure nó](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e89d-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="4e89d-233">Depois de concluída esta operação, dados do disco efémeras serão perdidos e endereços IP dinâmicos que estão associados a máquina virtual de Olá serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="4e89d-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="4e89d-234">Siga as instruções de Olá em [como tooreset uma palavra-passe ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:</span><span class="sxs-lookup"><span data-stu-id="4e89d-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="4e89d-235">Olá de reposição de palavra-passe ou chave SSH.</span><span class="sxs-lookup"><span data-stu-id="4e89d-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="4e89d-236">Criar um *sudo* conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="4e89d-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="4e89d-237">Repor a configuração de SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="4e89d-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="4e89d-238">Verificar o estado de funcionamento de recursos de uma VM Olá para quaisquer problemas de plataforma.</span><span class="sxs-lookup"><span data-stu-id="4e89d-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="4e89d-239">Selecione a VM e desloque para baixo **definições** > **verificar o estado de funcionamento**.</span><span class="sxs-lookup"><span data-stu-id="4e89d-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e89d-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4e89d-240">Additional resources</span></span>
* <span data-ttu-id="4e89d-241">Se ainda não é possível tooSSH tooyour VM após seguinte Olá após passos, consulte o artigo [mais passos de resolução de problemas](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview adicional passos tooresolve seu problema.</span><span class="sxs-lookup"><span data-stu-id="4e89d-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="4e89d-242">Para obter mais informações sobre resolução de problemas de acesso de aplicação, consulte [aplicação tooan acesso de resolução de problemas em execução numa máquina virtual do Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4e89d-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="4e89d-243">Para obter mais informações sobre resolução de problemas de máquinas virtuais que foram criadas utilizando o modelo de implementação clássica Olá, consulte [como tooreset uma palavra-passe ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e89d-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

