---
title: aaaSecure certificados de um servidor web com SSL no Azure | Microsoft Docs
description: "Saiba como certificados de servidor web do toosecure Olá NGINX com SSL numa VM com Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="95a17-103">Proteger um servidor web com certificados SSL numa máquina virtual com Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="95a17-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="95a17-104">servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser utilizado o tráfego da web tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="95a17-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="95a17-105">Estes certificados SSL podem ser armazenados no Cofre de chaves do Azure e permitem implementações seguras de máquinas virtuais (VMs) do certificados tooLinux no Azure.</span><span class="sxs-lookup"><span data-stu-id="95a17-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="95a17-106">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="95a17-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95a17-107">Criar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="95a17-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="95a17-108">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="95a17-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="95a17-109">Criar uma VM e instalar o servidor de web NGINX Olá</span><span class="sxs-lookup"><span data-stu-id="95a17-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="95a17-110">Inserir o certificado de Olá no Olá VM e configurar NGINX com um enlace SSL</span><span class="sxs-lookup"><span data-stu-id="95a17-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="95a17-111">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="95a17-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="95a17-112">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="95a17-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="95a17-113">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="95a17-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="95a17-114">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="95a17-114">Overview</span></span>
<span data-ttu-id="95a17-115">O Cofre de chaves do Azure salvaguarda as chaves criptográficas e segredos, esses certificados ou palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="95a17-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="95a17-116">O Cofre de chaves ajuda a simplificar o processo de gestão de certificados de Olá e permite-lhe controlo toomaintain das chaves de acesso esses certificados.</span><span class="sxs-lookup"><span data-stu-id="95a17-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="95a17-117">Pode criar um certificado autoassinado no interior do Cofre de chaves ou carregar um certificado existente, fidedigno que já possui.</span><span class="sxs-lookup"><span data-stu-id="95a17-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="95a17-118">Em vez de utilizar uma imagem de VM personalizada, incluindo certificados integrada-in, inserir certificados para uma VM em execução.</span><span class="sxs-lookup"><span data-stu-id="95a17-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="95a17-119">Este processo garante que os certificados mais atualizadas à sua Olá estão instalados num servidor web durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="95a17-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="95a17-120">Se renovar ou substituir um certificado, não tem também toocreate uma nova imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="95a17-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="95a17-121">certificados mais recentes Olá são automaticamente injetados como criar VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="95a17-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="95a17-122">Durante o processo de todo Olá, certificados de Olá nunca deixam Olá plataforma do Azure ou estão expostos num script, o histórico da linha de comandos ou o modelo.</span><span class="sxs-lookup"><span data-stu-id="95a17-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="95a17-123">Criar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="95a17-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="95a17-124">Antes de poder criar um cofre de chaves e certificados, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="95a17-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="95a17-125">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupSecureWeb* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="95a17-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="95a17-126">Em seguida, crie um cofre de chaves com [az keyvault criar](/cli/azure/keyvault#create) e ative-a para utilização quando implementar uma VM.</span><span class="sxs-lookup"><span data-stu-id="95a17-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="95a17-127">Cada Cofre de chaves requer um nome exclusivo e deve ser todas as letras maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="95a17-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="95a17-128">Substitua  *<mykeyvault>*  no Olá seguinte o exemplo com o seu próprio nome exclusivo do Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="95a17-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="95a17-129">Gerar um certificado e armazenar no Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="95a17-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="95a17-130">Para utilização em produção, deve importar um certificado válido assinado por um fornecedor fidedigno com [importação de certificados de keyvault az](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="95a17-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="95a17-131">Para este tutorial, hello exemplo seguinte mostra como pode gerar um certificado autoassinado com [Criar certificado de keyvault az](/cli/azure/certificate#create) que utiliza a política de certificado Olá predefinida:</span><span class="sxs-lookup"><span data-stu-id="95a17-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="95a17-132">Preparar um certificado para utilização com uma VM</span><span class="sxs-lookup"><span data-stu-id="95a17-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="95a17-133">certificado de Olá toouse durante Olá VM criar processo, obtenha Olá ID do certificado com [az keyvault lista-as versões do segredo](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="95a17-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="95a17-134">Converter o certificado de Olá com [az vm formato-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="95a17-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="95a17-135">Olá seguinte exemplo atribui resultado Olá toovariables estes comandos para facilidade de utilização no Olá passos seguintes:</span><span class="sxs-lookup"><span data-stu-id="95a17-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="95a17-136">Criar um toosecure de configuração de nuvem init NGINX</span><span class="sxs-lookup"><span data-stu-id="95a17-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="95a17-137">[Nuvem init](https://cloudinit.readthedocs.io) é uma abordagem amplamente utilizado toocustomize uma VM com Linux como arranca para Olá pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="95a17-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="95a17-138">Pode utilizar pacotes de tooinstall init de nuvem e escrever ficheiros, ou utilizadores tooconfigure e segurança.</span><span class="sxs-lookup"><span data-stu-id="95a17-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="95a17-139">Como nuvem init é executado durante o processo de arranque inicial Olá, existem não existem passos adicionais ou necessário tooapply de agentes a configuração.</span><span class="sxs-lookup"><span data-stu-id="95a17-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="95a17-140">Quando cria uma VM, certificados e chaves são armazenadas no Olá protegido */var/lib/waagent/* diretório.</span><span class="sxs-lookup"><span data-stu-id="95a17-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="95a17-141">a adição de tooautomate Olá certificado toohello VM e configurar o servidor de web de Olá, utilize init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="95a17-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="95a17-142">Neste exemplo, instalar e configurar o servidor de web Olá NGINX.</span><span class="sxs-lookup"><span data-stu-id="95a17-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="95a17-143">Pode utilizar Olá mesmo processar tooinstall e configurar o Apache.</span><span class="sxs-lookup"><span data-stu-id="95a17-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="95a17-144">Crie um ficheiro denominado *nuvem-init-web-server.txt* e colar Olá seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="95a17-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="95a17-145">Criar uma VM segura</span><span class="sxs-lookup"><span data-stu-id="95a17-145">Create a secure VM</span></span>
<span data-ttu-id="95a17-146">Agora criar uma VM com [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="95a17-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="95a17-147">dados de certificado Olá são injetados do Cofre de chaves com Olá `--secrets` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="95a17-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="95a17-148">Passar na configuração de nuvem init Olá com Olá `--custom-data` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="95a17-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="95a17-149">Demora alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e Olá toostart de aplicação.</span><span class="sxs-lookup"><span data-stu-id="95a17-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="95a17-150">Quando tiver sido criado Olá VM, tome nota do Olá `publicIpAddress` apresentado pela Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a17-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="95a17-151">Este endereço é utilizado tooaccess seu site num browser.</span><span class="sxs-lookup"><span data-stu-id="95a17-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="95a17-152">tooallow proteger web tráfego tooreach a VM, abra a porta 443 de Olá Internet com [az vm open-porta](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="95a17-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="95a17-153">Aplicação de web seguro Olá de teste</span><span class="sxs-lookup"><span data-stu-id="95a17-153">Test hello secure web app</span></span>
<span data-ttu-id="95a17-154">Agora pode abrir um browser e introduza *https://<publicIpAddress>*  na barra de endereço Olá.</span><span class="sxs-lookup"><span data-stu-id="95a17-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="95a17-155">Forneça o suas próprias público endereços IP a partir Olá VM criar o processo.</span><span class="sxs-lookup"><span data-stu-id="95a17-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="95a17-156">Aceite o aviso de segurança de Olá se utilizou um certificado autoassinado:</span><span class="sxs-lookup"><span data-stu-id="95a17-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Aceitar o aviso de segurança do browser web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="95a17-158">O site NGINX protegido, em seguida, é apresentado como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="95a17-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Site NGINX está em execução segura de vista](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="95a17-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="95a17-160">Next steps</span></span>

<span data-ttu-id="95a17-161">Neste tutorial, protegidos por um servidor de web NGINX com um certificado SSL armazenado no Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a17-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="95a17-162">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="95a17-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95a17-163">Criar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="95a17-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="95a17-164">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="95a17-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="95a17-165">Criar uma VM e instalar o servidor de web NGINX Olá</span><span class="sxs-lookup"><span data-stu-id="95a17-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="95a17-166">Inserir o certificado de Olá no Olá VM e configurar NGINX com um enlace SSL</span><span class="sxs-lookup"><span data-stu-id="95a17-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="95a17-167">Siga este toosee ligação criadas previamente amostras de script da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="95a17-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95a17-168">Exemplos de script de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="95a17-168">Windows virtual machine script samples</span></span>](./cli-samples.md)