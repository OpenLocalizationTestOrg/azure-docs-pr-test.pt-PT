---
title: discos aaaEncrypt uma VM com Linux no Azure | Microsoft Docs
description: "Como tooencrypt discos virtuais uma VM com Linux para utilizar segurança avançada Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="25f07-103">Como tooencrypt discos virtuais uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="25f07-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="25f07-104">Para segurança avançada máquina virtual (VM) e conformidade, discos virtuais no Azure podem ser encriptados.</span><span class="sxs-lookup"><span data-stu-id="25f07-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="25f07-105">Discos estão encriptados com as chaves criptográficas que são protegidas um cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="25f07-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="25f07-106">Pode controla estas chaves criptográficas e pode auditar a sua utilização.</span><span class="sxs-lookup"><span data-stu-id="25f07-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="25f07-107">Este artigo descreve em detalhe como tooencrypt discos virtuais numa VM com Linux utilizando Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="25f07-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="25f07-108">Também pode executar estes passos com Olá [CLI do Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25f07-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="25f07-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="25f07-109">Quick commands</span></span>
<span data-ttu-id="25f07-110">Se precisar de tooquickly realizar tarefas Olá, Olá Olá de detalhes de secção base os seguintes comandos tooencrypt discos virtuais a VM.</span><span class="sxs-lookup"><span data-stu-id="25f07-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="25f07-111">Mais informações e o contexto de cada passo pode ser encontrado rest Olá documento Olá, [Iniciar aqui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="25f07-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="25f07-112">Precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="25f07-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="25f07-113">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="25f07-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="25f07-114">Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myKey*, e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="25f07-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="25f07-115">Em primeiro lugar, ativar o fornecedor do Cofre de chaves do Azure Olá dentro da sua subscrição do Azure com [o registo de fornecedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="25f07-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="25f07-116">Olá exemplo seguinte cria um nome de grupo de recursos *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="25f07-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="25f07-117">Criar um cofre de chaves do Azure com [az keyvault criar](/cli/azure/keyvault#create) e ativar Olá Cofre de chaves para utilização com a encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="25f07-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="25f07-118">Especifique um nome exclusivo do Cofre de chaves para *keyvault_name* da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="25f07-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="25f07-119">Criar uma chave criptográfica no seu Cofre de chaves com [criar chave de keyvault az](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="25f07-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="25f07-120">Olá exemplo seguinte cria uma chave denominada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="25f07-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="25f07-121">Criar um principal de serviço com o Azure Active Directory com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="25f07-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="25f07-122">identificadores de principal de serviço de Olá Olá autenticação e troca de chaves criptográficas do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="25f07-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="25f07-123">Olá seguinte o exemplo de leituras na Olá os valores de principal de serviço Olá Id e palavra-passe para utilização nos comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="25f07-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="25f07-124">palavra-passe de Olá é só de saída ao criar Olá principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="25f07-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="25f07-125">Se assim o desejar, ver e registo Olá palavra-passe (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="25f07-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="25f07-126">Pode listar os principais de serviço com [lista do az ad sp](/cli/azure/ad/sp#list) e ver informações adicionais sobre um serviço específico principal com [Mostrar do az ad sp](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="25f07-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="25f07-127">Definir as permissões no seu Cofre de chaves com [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="25f07-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="25f07-128">No seguinte exemplo de Olá, hello ID de principal de serviço fornecido de Olá precedente comando:</span><span class="sxs-lookup"><span data-stu-id="25f07-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="25f07-129">Criar uma VM com [az vm criar](/cli/azure/vm#create) e anexar um disco de dados de 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="25f07-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="25f07-130">Apenas determinadas imagens do marketplace suportam encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="25f07-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="25f07-131">Olá exemplo seguinte cria uma VM chamada `myVM` utilizando um **CentOS 7.2n** imagem:</span><span class="sxs-lookup"><span data-stu-id="25f07-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="25f07-132">SSH tooyour VM utilizando Olá `publicIpAddress` apresentado na saída de Olá de Olá precedente comando.</span><span class="sxs-lookup"><span data-stu-id="25f07-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="25f07-133">Criar uma partição e o sistema de ficheiros, em seguida, montar o disco de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="25f07-134">Para obter mais informações, consulte [ligar tooa disco de nova VM com Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="25f07-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="25f07-135">Feche a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="25f07-135">Close your SSH session.</span></span>

<span data-ttu-id="25f07-136">Encriptar a VM com [ativar a encriptação de vm az](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="25f07-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="25f07-137">Olá exemplo seguinte utiliza Olá `$sp_id` e `$sp_password` variáveis a partir de Olá anterior `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="25f07-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="25f07-138">Demora algum tempo para toocomplete de processo de encriptação de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="25f07-139">Monitorizar o estado de Olá do processo de Olá com [mostrar de encriptação de vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="25f07-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25f07-140">Olá estado Mostrar **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="25f07-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="25f07-141">Aguarde até que o estado de Olá para relatórios de disco de SO de Olá **VMRestartPending**, em seguida, reinicie a VM com [reinício de vm az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="25f07-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25f07-142">Olá processo de encriptação de disco está finalizado durante o processo de arranque Olá, por isso, aguarde alguns minutos antes de a verificar o estado de Olá de encriptação com **mostrar de encriptação de vm az**:</span><span class="sxs-lookup"><span data-stu-id="25f07-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25f07-143">Estado de Olá agora deve reportar disco Olá SO e discos de dados como **encriptado**.</span><span class="sxs-lookup"><span data-stu-id="25f07-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="25f07-144">Descrição geral de encriptação de disco</span><span class="sxs-lookup"><span data-stu-id="25f07-144">Overview of disk encryption</span></span>
<span data-ttu-id="25f07-145">Discos virtuais em VMs do Linux são encriptados em rest utilizando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="25f07-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="25f07-146">Não há sem encargos de encriptação de discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="25f07-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="25f07-147">As chaves criptográficas são armazenadas no Cofre de chaves do Azure utilizando a proteção de software, ou pode importar ou gerar as suas chaves nos módulos de segurança de Hardware (HSMs) certificadas tooFIPS normas de nível 2 140-2.</span><span class="sxs-lookup"><span data-stu-id="25f07-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="25f07-148">Manter o controlo destas chaves criptográficas e pode auditar a sua utilização.</span><span class="sxs-lookup"><span data-stu-id="25f07-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="25f07-149">Estas chaves criptográficas são utilizado tooencrypt e desencriptar discos virtuais anexados tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="25f07-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="25f07-150">Um principal de serviço do Azure Active Directory fornece um mecanismo seguro para emitir estas chaves criptográficas como VMs estão ligados à corrente ou desligar.</span><span class="sxs-lookup"><span data-stu-id="25f07-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="25f07-151">processo de Olá para encriptar uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="25f07-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="25f07-152">Crie uma chave criptográfica num cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="25f07-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="25f07-153">Configure Olá criptografia chave toobe utilizada para encriptação de discos.</span><span class="sxs-lookup"><span data-stu-id="25f07-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="25f07-154">chave de criptografia Olá tooread de Olá Cofre de chaves do Azure, criar um serviço do Azure Active Directory principal com as permissões adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="25f07-155">Emita Olá comando tooencrypt os discos virtuais, especificando o principal de serviço do Azure Active Directory Olá e adequada toobe chave criptográfica utilizada.</span><span class="sxs-lookup"><span data-stu-id="25f07-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="25f07-156">pedidos principais de serviço do Azure Active Directory de Olá Olá necessário chave criptográfica do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="25f07-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="25f07-157">discos virtuais Olá estão encriptados com a chave criptográfica Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="25f07-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="25f07-158">Processo de encriptação</span><span class="sxs-lookup"><span data-stu-id="25f07-158">Encryption process</span></span>
<span data-ttu-id="25f07-159">Encriptação de disco depende Olá os seguintes componentes adicionais:</span><span class="sxs-lookup"><span data-stu-id="25f07-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="25f07-160">**O Cofre de chaves do Azure** -utilizado toosafeguard de chaves criptográficas e segredos utilizados para o processo de encriptação/desencriptação de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="25f07-161">Se existir, pode utilizar um cofre de chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="25f07-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="25f07-162">Não dispõe de toodedicate discos de tooencrypting um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="25f07-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="25f07-163">limites administrativos tooseparate e visibilidade chave, pode criar um cofre de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="25f07-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="25f07-164">**Azure Active Directory** - identificadores Olá segura de troca de chaves criptográficas necessárias e as ações de pedido de autenticação para.</span><span class="sxs-lookup"><span data-stu-id="25f07-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="25f07-165">Normalmente, pode utilizar uma instância existente do Azure Active Directory para o alojamento da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="25f07-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="25f07-166">principal de serviço Olá fornece um mecanismo segura toorequest e chaves criptográficas adequada de Olá de ser emitido.</span><span class="sxs-lookup"><span data-stu-id="25f07-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="25f07-167">Não estiver a desenvolver uma aplicação real, que se integra com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25f07-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="25f07-168">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="25f07-168">Requirements and limitations</span></span>
<span data-ttu-id="25f07-169">Cenários suportados e os requisitos para encriptação de disco de:</span><span class="sxs-lookup"><span data-stu-id="25f07-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="25f07-170">Olá seguinte servidor Linux SKUs - Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="25f07-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="25f07-171">Todos os recursos (por exemplo, o Cofre de chaves, a conta de armazenamento e a VM) tem de constar Olá mesma região do Azure e subscrição.</span><span class="sxs-lookup"><span data-stu-id="25f07-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="25f07-172">Um padrão, D, DS, G e GS série VMs.</span><span class="sxs-lookup"><span data-stu-id="25f07-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="25f07-173">Encriptação de disco não é atualmente suportada no Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="25f07-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="25f07-174">Escalão básico VMs.</span><span class="sxs-lookup"><span data-stu-id="25f07-174">Basic tier VMs.</span></span>
* <span data-ttu-id="25f07-175">VMs criadas utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="25f07-176">A desativação da encriptação de disco de SO em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="25f07-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="25f07-177">A atualizar as chaves criptográficas Olá numa VM com Linux já encriptados.</span><span class="sxs-lookup"><span data-stu-id="25f07-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="25f07-178">Criar Cofre de chaves do Azure e as chaves</span><span class="sxs-lookup"><span data-stu-id="25f07-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="25f07-179">Precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="25f07-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="25f07-180">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="25f07-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="25f07-181">Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myKey*, e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="25f07-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="25f07-182">primeiro passo de Olá é toocreate toostore um cofre de chaves do Azure, as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="25f07-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="25f07-183">O Cofre de chaves do Azure pode armazenar as chaves, segredos, ou palavras-passe que lhe permitem toosecurely implementá-la nas suas aplicações e serviços.</span><span class="sxs-lookup"><span data-stu-id="25f07-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="25f07-184">Para a encriptação de disco virtual, utilizar o Cofre de chaves toostore uma chave criptográfica que é utilizado tooencrypt ou desencriptar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="25f07-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="25f07-185">Ativar o fornecedor do Cofre de chaves do Azure Olá dentro da sua subscrição do Azure com [o registo de fornecedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="25f07-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="25f07-186">Olá exemplo seguinte cria um nome de grupo de recursos *myResourceGroup* no Olá `eastus` localização:</span><span class="sxs-lookup"><span data-stu-id="25f07-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="25f07-187">Olá, Olá Cofre de chaves do Azure que contêm Olá chaves criptográfico e computação associada recursos, tais como o armazenamento e Olá própria VM tem de residir na mesma região.</span><span class="sxs-lookup"><span data-stu-id="25f07-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="25f07-188">Criar um cofre de chaves do Azure com [az keyvault criar](/cli/azure/keyvault#create) e ativar Olá Cofre de chaves para utilização com a encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="25f07-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="25f07-189">Especifique um nome exclusivo do Cofre de chaves para *keyvault_name* da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="25f07-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="25f07-190">Pode armazenar as chaves criptográficas utilizando software ou proteção de modelo de segurança de Hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="25f07-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="25f07-191">Utilizar um HSM necessita de um cofre de chaves de premium.</span><span class="sxs-lookup"><span data-stu-id="25f07-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="25f07-192">Há um toocreating custos adicionais um premium Cofre de chaves em vez de padrão Cofre de chaves que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="25f07-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="25f07-193">toocreate adicionar um premium Cofre de chaves no Olá precedente passo `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="25f07-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="25f07-194">Olá exemplo seguinte utiliza as chaves protegidas de software, uma vez que criámos um cofre de chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="25f07-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="25f07-195">Olá plataforma do Azure para ambos os modelos de proteção, tem de toobe concedido acesso Olá de toorequest chaves criptográficas quando Olá VM arranca discos virtuais do toodecrypt Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="25f07-196">Criar uma chave criptográfica no seu Cofre de chaves com [criar chave de keyvault az](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="25f07-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="25f07-197">Olá exemplo seguinte cria uma chave denominada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="25f07-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="25f07-198">Criar Olá principal de serviço do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25f07-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="25f07-199">Quando os discos virtuais são encriptados ou desencriptados, especifique uma autenticação da conta toohandle Olá e troca de chaves criptográficas do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="25f07-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="25f07-200">Esta conta, um principal de serviço do Azure Active Directory, permite Olá plataforma Azure toorequest Olá adequada as chaves criptográficas em nome Olá VM.</span><span class="sxs-lookup"><span data-stu-id="25f07-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="25f07-201">Uma instância do Azure Active Directory predefinida está disponível na sua subscrição, apesar de muitas organizações têm dedicado diretórios do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25f07-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="25f07-202">Criar um principal de serviço com o Azure Active Directory com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="25f07-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="25f07-203">Olá seguinte o exemplo de leituras na Olá os valores de principal de serviço Olá Id e palavra-passe para utilização nos comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="25f07-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="25f07-204">palavra-passe de Olá só é apresentada quando criar o serviço de Olá principal.</span><span class="sxs-lookup"><span data-stu-id="25f07-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="25f07-205">Se assim o desejar, ver e registo Olá palavra-passe (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="25f07-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="25f07-206">Pode listar os principais de serviço com [lista do az ad sp](/cli/azure/ad/sp#list) e ver informações adicionais sobre um serviço específico principal com [Mostrar do az ad sp](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="25f07-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="25f07-207">toosuccessfully encriptar ou desencriptar discos virtuais, as permissões chave criptográfica Olá armazenados no Cofre de chaves tem de ser definido toopermit Olá do Azure Active Directory serviço principal tooread Olá chaves.</span><span class="sxs-lookup"><span data-stu-id="25f07-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="25f07-208">Definir as permissões no seu Cofre de chaves com [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="25f07-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="25f07-209">No seguinte exemplo de Olá, hello ID de principal de serviço fornecido de Olá precedente comando:</span><span class="sxs-lookup"><span data-stu-id="25f07-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="25f07-210">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="25f07-210">Create virtual machine</span></span>
<span data-ttu-id="25f07-211">tooactually encriptar alguns discos virtuais, permite criar uma VM e adicionar um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="25f07-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="25f07-212">Criar um tooencrypt VM com [az vm criar](/cli/azure/vm#create) e anexar um disco de dados de 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="25f07-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="25f07-213">Apenas determinadas imagens do marketplace suportam encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="25f07-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="25f07-214">Olá exemplo seguinte cria uma VM chamada *myVM* utilizando um **CentOS 7.2n** imagem:</span><span class="sxs-lookup"><span data-stu-id="25f07-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="25f07-215">SSH tooyour VM utilizando Olá `publicIpAddress` apresentado na saída de Olá de Olá precedente comando.</span><span class="sxs-lookup"><span data-stu-id="25f07-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="25f07-216">Criar uma partição e o sistema de ficheiros, em seguida, montar o disco de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="25f07-217">Para obter mais informações, consulte [ligar tooa disco de nova VM com Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="25f07-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="25f07-218">Feche a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="25f07-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="25f07-219">Encriptar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="25f07-219">Encrypt virtual machine</span></span>
<span data-ttu-id="25f07-220">discos virtuais do Olá tooencrypt, colocar em conjunto todos os componentes de Olá anterior:</span><span class="sxs-lookup"><span data-stu-id="25f07-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="25f07-221">Especifique Olá principal de serviço do Azure Active Directory e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="25f07-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="25f07-222">Especifique Olá Cofre de chaves toostore Olá metadados para os discos encriptados.</span><span class="sxs-lookup"><span data-stu-id="25f07-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="25f07-223">Especifique Olá chaves criptográficas toouse para encriptação real Olá e a desencriptação.</span><span class="sxs-lookup"><span data-stu-id="25f07-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="25f07-224">Especifique se pretende tooencrypt disco de SO de Olá, discos de dados de Olá ou todos.</span><span class="sxs-lookup"><span data-stu-id="25f07-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="25f07-225">Encriptar a VM com [ativar a encriptação de vm az](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="25f07-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="25f07-226">Olá exemplo seguinte utiliza Olá `$sp_id` e `$sp_password` variáveis a partir de Olá anterior `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="25f07-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="25f07-227">Demora algum tempo para toocomplete de processo de encriptação de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="25f07-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="25f07-228">Monitorizar o estado de Olá do processo de Olá com [mostrar de encriptação de vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="25f07-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25f07-229">Olá de saída é semelhante toohello seguinte o exemplo truncado:</span><span class="sxs-lookup"><span data-stu-id="25f07-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="25f07-230">Aguarde até que o estado de Olá para relatórios de disco de SO de Olá **VMRestartPending**, em seguida, reinicie a VM com [reinício de vm az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="25f07-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25f07-231">Olá processo de encriptação de disco está finalizado durante o processo de arranque Olá, por isso, aguarde alguns minutos antes de a verificar o estado de Olá de encriptação com **mostrar de encriptação de vm az**:</span><span class="sxs-lookup"><span data-stu-id="25f07-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25f07-232">Estado de Olá agora deve reportar disco Olá SO e discos de dados como **encriptado**.</span><span class="sxs-lookup"><span data-stu-id="25f07-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="25f07-233">Adicionar discos de dados adicionais</span><span class="sxs-lookup"><span data-stu-id="25f07-233">Add additional data disks</span></span>
<span data-ttu-id="25f07-234">Assim que encriptou os discos de dados, pode adicionar mais tarde adicionais de discos virtuais tooyour VM e também encriptá-las.</span><span class="sxs-lookup"><span data-stu-id="25f07-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="25f07-235">Por exemplo, permite adicionar uma segunda tooyour de disco virtual VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="25f07-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="25f07-236">Execute novamente o discos virtuais do Olá comando tooencrypt Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="25f07-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="25f07-237">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="25f07-237">Next steps</span></span>
* <span data-ttu-id="25f07-238">Para obter mais informações sobre como gerir o Cofre de chaves do Azure, incluindo a eliminação de chaves criptográficas e os cofres, consulte [gerir o Cofre de chaves ao utilizar a CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="25f07-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="25f07-239">Para obter mais informações sobre a encriptação de disco, tais como preparar uma encriptados personalizado VM tooupload tooAzure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="25f07-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
