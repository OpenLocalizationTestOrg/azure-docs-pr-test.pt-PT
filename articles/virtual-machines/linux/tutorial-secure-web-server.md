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
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Proteger um servidor web com certificados SSL numa máquina virtual com Linux no Azure
servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser utilizado o tráfego da web tooencrypt. Estes certificados SSL podem ser armazenados no Cofre de chaves do Azure e permitem implementações seguras de máquinas virtuais (VMs) do certificados tooLinux no Azure. Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar um cofre de chaves do Azure
> * Gerar ou carregar um certificado toohello Cofre de chaves
> * Criar uma VM e instalar o servidor de web NGINX Olá
> * Inserir o certificado de Olá no Olá VM e configurar NGINX com um enlace SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Descrição geral
O Cofre de chaves do Azure salvaguarda as chaves criptográficas e segredos, esses certificados ou palavras-passe. O Cofre de chaves ajuda a simplificar o processo de gestão de certificados de Olá e permite-lhe controlo toomaintain das chaves de acesso esses certificados. Pode criar um certificado autoassinado no interior do Cofre de chaves ou carregar um certificado existente, fidedigno que já possui.

Em vez de utilizar uma imagem de VM personalizada, incluindo certificados integrada-in, inserir certificados para uma VM em execução. Este processo garante que os certificados mais atualizadas à sua Olá estão instalados num servidor web durante a implementação. Se renovar ou substituir um certificado, não tem também toocreate uma nova imagem VM personalizada. certificados mais recentes Olá são automaticamente injetados como criar VMs adicionais. Durante o processo de todo Olá, certificados de Olá nunca deixam Olá plataforma do Azure ou estão expostos num script, o histórico da linha de comandos ou o modelo.


## <a name="create-an-azure-key-vault"></a>Criar um cofre de chaves do Azure
Antes de poder criar um cofre de chaves e certificados, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupSecureWeb* no Olá *eastus* localização:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Em seguida, crie um cofre de chaves com [az keyvault criar](/cli/azure/keyvault#create) e ative-a para utilização quando implementar uma VM. Cada Cofre de chaves requer um nome exclusivo e deve ser todas as letras maiúsculas e minúsculas. Substitua  *<mykeyvault>*  no Olá seguinte o exemplo com o seu próprio nome exclusivo do Cofre de chaves:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Gerar um certificado e armazenar no Cofre de chaves
Para utilização em produção, deve importar um certificado válido assinado por um fornecedor fidedigno com [importação de certificados de keyvault az](/cli/azure/certificate#import). Para este tutorial, hello exemplo seguinte mostra como pode gerar um certificado autoassinado com [Criar certificado de keyvault az](/cli/azure/certificate#create) que utiliza a política de certificado Olá predefinida:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Preparar um certificado para utilização com uma VM
certificado de Olá toouse durante Olá VM criar processo, obtenha Olá ID do certificado com [az keyvault lista-as versões do segredo](/cli/azure/keyvault/secret#list-versions). Converter o certificado de Olá com [az vm formato-secret](/cli/azure/vm#format-secret). Olá seguinte exemplo atribui resultado Olá toovariables estes comandos para facilidade de utilização no Olá passos seguintes:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Criar um toosecure de configuração de nuvem init NGINX
[Nuvem init](https://cloudinit.readthedocs.io) é uma abordagem amplamente utilizado toocustomize uma VM com Linux como arranca para Olá pela primeira vez. Pode utilizar pacotes de tooinstall init de nuvem e escrever ficheiros, ou utilizadores tooconfigure e segurança. Como nuvem init é executado durante o processo de arranque inicial Olá, existem não existem passos adicionais ou necessário tooapply de agentes a configuração.

Quando cria uma VM, certificados e chaves são armazenadas no Olá protegido */var/lib/waagent/* diretório. a adição de tooautomate Olá certificado toohello VM e configurar o servidor de web de Olá, utilize init de nuvem. Neste exemplo, instalar e configurar o servidor de web Olá NGINX. Pode utilizar Olá mesmo processar tooinstall e configurar o Apache. 

Crie um ficheiro denominado *nuvem-init-web-server.txt* e colar Olá seguinte configuração:

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

### <a name="create-a-secure-vm"></a>Criar uma VM segura
Agora criar uma VM com [az vm criar](/cli/azure/vm#create). dados de certificado Olá são injetados do Cofre de chaves com Olá `--secrets` parâmetro. Passar na configuração de nuvem init Olá com Olá `--custom-data` parâmetro:

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

Demora alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e Olá toostart de aplicação. Quando tiver sido criado Olá VM, tome nota do Olá `publicIpAddress` apresentado pela Olá CLI do Azure. Este endereço é utilizado tooaccess seu site num browser.

tooallow proteger web tráfego tooreach a VM, abra a porta 443 de Olá Internet com [az vm open-porta](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Aplicação de web seguro Olá de teste
Agora pode abrir um browser e introduza *https://<publicIpAddress>*  na barra de endereço Olá. Forneça o suas próprias público endereços IP a partir Olá VM criar o processo. Aceite o aviso de segurança de Olá se utilizou um certificado autoassinado:

![Aceitar o aviso de segurança do browser web](./media/tutorial-secure-web-server/browser-warning.png)

O site NGINX protegido, em seguida, é apresentado como no seguinte exemplo de Olá:

![Site NGINX está em execução segura de vista](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Passos seguintes

Neste tutorial, protegidos por um servidor de web NGINX com um certificado SSL armazenado no Cofre de chaves do Azure. Aprendeu a:

> [!div class="checklist"]
> * Criar um cofre de chaves do Azure
> * Gerar ou carregar um certificado toohello Cofre de chaves
> * Criar uma VM e instalar o servidor de web NGINX Olá
> * Inserir o certificado de Olá no Olá VM e configurar NGINX com um enlace SSL

Siga este toosee ligação criadas previamente amostras de script da máquina virtual.

> [!div class="nextstepaction"]
> [Exemplos de script de máquina virtual do Windows](./cli-samples.md)