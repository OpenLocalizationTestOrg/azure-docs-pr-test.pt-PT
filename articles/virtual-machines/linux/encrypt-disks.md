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
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Como tooencrypt discos virtuais uma VM com Linux
Para segurança avançada máquina virtual (VM) e conformidade, discos virtuais no Azure podem ser encriptados. Discos estão encriptados com as chaves criptográficas que são protegidas um cofre de chaves do Azure. Pode controla estas chaves criptográficas e pode auditar a sua utilização. Este artigo descreve em detalhe como tooencrypt discos virtuais numa VM com Linux utilizando Olá Azure CLI 2.0. Também pode executar estes passos com Olá [CLI do Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandos rápidos
Se precisar de tooquickly realizar tarefas Olá, Olá Olá de detalhes de secção base os seguintes comandos tooencrypt discos virtuais a VM. Mais informações e o contexto de cada passo pode ser encontrado rest Olá documento Olá, [Iniciar aqui](#overview-of-disk-encryption).

Precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login). No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myKey*, e *myVM*.

Em primeiro lugar, ativar o fornecedor do Cofre de chaves do Azure Olá dentro da sua subscrição do Azure com [o registo de fornecedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um nome de grupo de recursos *myResourceGroup* no Olá *eastus* localização:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Criar um cofre de chaves do Azure com [az keyvault criar](/cli/azure/keyvault#create) e ativar Olá Cofre de chaves para utilização com a encriptação de disco. Especifique um nome exclusivo do Cofre de chaves para *keyvault_name* da seguinte forma:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Criar uma chave criptográfica no seu Cofre de chaves com [criar chave de keyvault az](/cli/azure/keyvault/key#create). Olá exemplo seguinte cria uma chave denominada *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Criar um principal de serviço com o Azure Active Directory com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac). identificadores de principal de serviço de Olá Olá autenticação e troca de chaves criptográficas do Cofre de chaves. Olá seguinte o exemplo de leituras na Olá os valores de principal de serviço Olá Id e palavra-passe para utilização nos comandos posteriores:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

palavra-passe de Olá é só de saída ao criar Olá principal de serviço. Se assim o desejar, ver e registo Olá palavra-passe (`echo $sp_password`). Pode listar os principais de serviço com [lista do az ad sp](/cli/azure/ad/sp#list) e ver informações adicionais sobre um serviço específico principal com [Mostrar do az ad sp](/cli/azure/ad/sp#show).

Definir as permissões no seu Cofre de chaves com [az keyvault set-policy](/cli/azure/keyvault#set-policy). No seguinte exemplo de Olá, hello ID de principal de serviço fornecido de Olá precedente comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Criar uma VM com [az vm criar](/cli/azure/vm#create) e anexar um disco de dados de 5 Gb. Apenas determinadas imagens do marketplace suportam encriptação de disco. Olá exemplo seguinte cria uma VM chamada `myVM` utilizando um **CentOS 7.2n** imagem:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM utilizando Olá `publicIpAddress` apresentado na saída de Olá de Olá precedente comando. Criar uma partição e o sistema de ficheiros, em seguida, montar o disco de dados de Olá. Para obter mais informações, consulte [ligar tooa disco de nova VM com Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Feche a sessão SSH.

Encriptar a VM com [ativar a encriptação de vm az](/cli/azure/vm/encryption#enable). Olá exemplo seguinte utiliza Olá `$sp_id` e `$sp_password` variáveis a partir de Olá anterior `ad sp create-for-rbac` comando:

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

Demora algum tempo para toocomplete de processo de encriptação de disco Olá. Monitorizar o estado de Olá do processo de Olá com [mostrar de encriptação de vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Olá estado Mostrar **EncryptionInProgress**. Aguarde até que o estado de Olá para relatórios de disco de SO de Olá **VMRestartPending**, em seguida, reinicie a VM com [reinício de vm az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Olá processo de encriptação de disco está finalizado durante o processo de arranque Olá, por isso, aguarde alguns minutos antes de a verificar o estado de Olá de encriptação com **mostrar de encriptação de vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Estado de Olá agora deve reportar disco Olá SO e discos de dados como **encriptado**.

## <a name="overview-of-disk-encryption"></a>Descrição geral de encriptação de disco
Discos virtuais em VMs do Linux são encriptados em rest utilizando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Não há sem encargos de encriptação de discos virtuais no Azure. As chaves criptográficas são armazenadas no Cofre de chaves do Azure utilizando a proteção de software, ou pode importar ou gerar as suas chaves nos módulos de segurança de Hardware (HSMs) certificadas tooFIPS normas de nível 2 140-2. Manter o controlo destas chaves criptográficas e pode auditar a sua utilização. Estas chaves criptográficas são utilizado tooencrypt e desencriptar discos virtuais anexados tooyour VM. Um principal de serviço do Azure Active Directory fornece um mecanismo seguro para emitir estas chaves criptográficas como VMs estão ligados à corrente ou desligar.

processo de Olá para encriptar uma VM é o seguinte:

1. Crie uma chave criptográfica num cofre de chaves do Azure.
2. Configure Olá criptografia chave toobe utilizada para encriptação de discos.
3. chave de criptografia Olá tooread de Olá Cofre de chaves do Azure, criar um serviço do Azure Active Directory principal com as permissões adequadas Olá.
4. Emita Olá comando tooencrypt os discos virtuais, especificando o principal de serviço do Azure Active Directory Olá e adequada toobe chave criptográfica utilizada.
5. pedidos principais de serviço do Azure Active Directory de Olá Olá necessário chave criptográfica do Cofre de chaves do Azure.
6. discos virtuais Olá estão encriptados com a chave criptográfica Olá fornecido.

## <a name="encryption-process"></a>Processo de encriptação
Encriptação de disco depende Olá os seguintes componentes adicionais:

* **O Cofre de chaves do Azure** -utilizado toosafeguard de chaves criptográficas e segredos utilizados para o processo de encriptação/desencriptação de disco Olá.
  * Se existir, pode utilizar um cofre de chaves do Azure existente. Não dispõe de toodedicate discos de tooencrypting um cofre de chaves.
  * limites administrativos tooseparate e visibilidade chave, pode criar um cofre de chaves dedicado.
* **Azure Active Directory** - identificadores Olá segura de troca de chaves criptográficas necessárias e as ações de pedido de autenticação para.
  * Normalmente, pode utilizar uma instância existente do Azure Active Directory para o alojamento da sua aplicação.
  * principal de serviço Olá fornece um mecanismo segura toorequest e chaves criptográficas adequada de Olá de ser emitido. Não estiver a desenvolver uma aplicação real, que se integra com o Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisitos e limitações
Cenários suportados e os requisitos para encriptação de disco de:

* Olá seguinte servidor Linux SKUs - Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.
* Todos os recursos (por exemplo, o Cofre de chaves, a conta de armazenamento e a VM) tem de constar Olá mesma região do Azure e subscrição.
* Um padrão, D, DS, G e GS série VMs.

Encriptação de disco não é atualmente suportada no Olá os seguintes cenários:

* Escalão básico VMs.
* VMs criadas utilizando o modelo de implementação clássica Olá.
* A desativação da encriptação de disco de SO em VMs do Linux.
* A atualizar as chaves criptográficas Olá numa VM com Linux já encriptados.

## <a name="create-azure-key-vault-and-keys"></a>Criar Cofre de chaves do Azure e as chaves
Precisa de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login). No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myKey*, e *myVM*.

primeiro passo de Olá é toocreate toostore um cofre de chaves do Azure, as chaves criptográficas. O Cofre de chaves do Azure pode armazenar as chaves, segredos, ou palavras-passe que lhe permitem toosecurely implementá-la nas suas aplicações e serviços. Para a encriptação de disco virtual, utilizar o Cofre de chaves toostore uma chave criptográfica que é utilizado tooencrypt ou desencriptar os discos virtuais.

Ativar o fornecedor do Cofre de chaves do Azure Olá dentro da sua subscrição do Azure com [o registo de fornecedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um nome de grupo de recursos *myResourceGroup* no Olá `eastus` localização:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Olá, Olá Cofre de chaves do Azure que contêm Olá chaves criptográfico e computação associada recursos, tais como o armazenamento e Olá própria VM tem de residir na mesma região. Criar um cofre de chaves do Azure com [az keyvault criar](/cli/azure/keyvault#create) e ativar Olá Cofre de chaves para utilização com a encriptação de disco. Especifique um nome exclusivo do Cofre de chaves para *keyvault_name* da seguinte forma:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Pode armazenar as chaves criptográficas utilizando software ou proteção de modelo de segurança de Hardware (HSM). Utilizar um HSM necessita de um cofre de chaves de premium. Há um toocreating custos adicionais um premium Cofre de chaves em vez de padrão Cofre de chaves que armazena as chaves protegidas por software. toocreate adicionar um premium Cofre de chaves no Olá precedente passo `--sku Premium` toohello comando. Olá exemplo seguinte utiliza as chaves protegidas de software, uma vez que criámos um cofre de chaves padrão.

Olá plataforma do Azure para ambos os modelos de proteção, tem de toobe concedido acesso Olá de toorequest chaves criptográficas quando Olá VM arranca discos virtuais do toodecrypt Olá. Criar uma chave criptográfica no seu Cofre de chaves com [criar chave de keyvault az](/cli/azure/keyvault/key#create). Olá exemplo seguinte cria uma chave denominada *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Criar Olá principal de serviço do Azure Active Directory
Quando os discos virtuais são encriptados ou desencriptados, especifique uma autenticação da conta toohandle Olá e troca de chaves criptográficas do Cofre de chaves. Esta conta, um principal de serviço do Azure Active Directory, permite Olá plataforma Azure toorequest Olá adequada as chaves criptográficas em nome Olá VM. Uma instância do Azure Active Directory predefinida está disponível na sua subscrição, apesar de muitas organizações têm dedicado diretórios do Azure Active Directory.

Criar um principal de serviço com o Azure Active Directory com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac). Olá seguinte o exemplo de leituras na Olá os valores de principal de serviço Olá Id e palavra-passe para utilização nos comandos posteriores:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

palavra-passe de Olá só é apresentada quando criar o serviço de Olá principal. Se assim o desejar, ver e registo Olá palavra-passe (`echo $sp_password`). Pode listar os principais de serviço com [lista do az ad sp](/cli/azure/ad/sp#list) e ver informações adicionais sobre um serviço específico principal com [Mostrar do az ad sp](/cli/azure/ad/sp#show).

toosuccessfully encriptar ou desencriptar discos virtuais, as permissões chave criptográfica Olá armazenados no Cofre de chaves tem de ser definido toopermit Olá do Azure Active Directory serviço principal tooread Olá chaves. Definir as permissões no seu Cofre de chaves com [az keyvault set-policy](/cli/azure/keyvault#set-policy). No seguinte exemplo de Olá, hello ID de principal de serviço fornecido de Olá precedente comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Criar a máquina virtual
tooactually encriptar alguns discos virtuais, permite criar uma VM e adicionar um disco de dados. Criar um tooencrypt VM com [az vm criar](/cli/azure/vm#create) e anexar um disco de dados de 5 Gb. Apenas determinadas imagens do marketplace suportam encriptação de disco. Olá exemplo seguinte cria uma VM chamada *myVM* utilizando um **CentOS 7.2n** imagem:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM utilizando Olá `publicIpAddress` apresentado na saída de Olá de Olá precedente comando. Criar uma partição e o sistema de ficheiros, em seguida, montar o disco de dados de Olá. Para obter mais informações, consulte [ligar tooa disco de nova VM com Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Feche a sessão SSH.


## <a name="encrypt-virtual-machine"></a>Encriptar a máquina virtual
discos virtuais do Olá tooencrypt, colocar em conjunto todos os componentes de Olá anterior:

1. Especifique Olá principal de serviço do Azure Active Directory e a palavra-passe.
2. Especifique Olá Cofre de chaves toostore Olá metadados para os discos encriptados.
3. Especifique Olá chaves criptográficas toouse para encriptação real Olá e a desencriptação.
4. Especifique se pretende tooencrypt disco de SO de Olá, discos de dados de Olá ou todos.

Encriptar a VM com [ativar a encriptação de vm az](/cli/azure/vm/encryption#enable). Olá exemplo seguinte utiliza Olá `$sp_id` e `$sp_password` variáveis a partir de Olá anterior `ad sp create-for-rbac` comando:

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

Demora algum tempo para toocomplete de processo de encriptação de disco Olá. Monitorizar o estado de Olá do processo de Olá com [mostrar de encriptação de vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Olá de saída é semelhante toohello seguinte o exemplo truncado:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Aguarde até que o estado de Olá para relatórios de disco de SO de Olá **VMRestartPending**, em seguida, reinicie a VM com [reinício de vm az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Olá processo de encriptação de disco está finalizado durante o processo de arranque Olá, por isso, aguarde alguns minutos antes de a verificar o estado de Olá de encriptação com **mostrar de encriptação de vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Estado de Olá agora deve reportar disco Olá SO e discos de dados como **encriptado**.


## <a name="add-additional-data-disks"></a>Adicionar discos de dados adicionais
Assim que encriptou os discos de dados, pode adicionar mais tarde adicionais de discos virtuais tooyour VM e também encriptá-las. Por exemplo, permite adicionar uma segunda tooyour de disco virtual VM da seguinte forma:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Execute novamente o discos virtuais do Olá comando tooencrypt Olá da seguinte forma:

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


## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações sobre como gerir o Cofre de chaves do Azure, incluindo a eliminação de chaves criptográficas e os cofres, consulte [gerir o Cofre de chaves ao utilizar a CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Para obter mais informações sobre a encriptação de disco, tais como preparar uma encriptados personalizado VM tooupload tooAzure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).
