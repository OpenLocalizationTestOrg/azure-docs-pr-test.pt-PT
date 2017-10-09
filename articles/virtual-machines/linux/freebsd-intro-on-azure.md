---
title: aaaIntroduction tooFreeBSD no Azure | Microsoft Docs
description: "Saiba como utilizar FreeBSD máquinas de virtuais no Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Introdução tooFreeBSD no Azure
Este tópico fornece uma descrição geral da execução de uma máquina virtual de FreeBSD no Azure.

## <a name="overview"></a>Descrição geral
FreeBSD do Microsoft Azure é que um sistema operativo do computador avançadas utilizada servidores moderna toopower, ambientes de trabalho e plataformas incorporadas.

Microsoft Corporation é disponibilizar imagens de FreeBSD no Azure com Olá [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) pré-configurados. Atualmente, hello seguintes versões de FreeBSD são oferecidas como imagens pela Microsoft:

- FreeBSD 10.3-versão
- FreeBSD 11.0-versão

agente de Olá é responsável pela comunicação entre Olá FreeBSD VM e Olá recursos de infraestrutura do Azure para operações como aprovisionamento Olá VM na primeira utilização (nome de utilizador, palavra-passe ou chave SSH, o nome do anfitrião, etc.) e a funcionalidade de ativação para extensões VM seletivos.

Para versões futuras do FreeBSD, estratégia Olá é toostay atual e disponibilizar versões mais recentes de Olá pouco tempo depois de serem publicados pela equipa de engenharia Olá FreeBSD versão.

## <a name="deploying-a-freebsd-virtual-machine"></a>Implementar uma máquina virtual de FreeBSD
Implementar uma máquina virtual de FreeBSD é um processo simples utilizando uma imagem de Olá Azure Marketplace da Olá portal do Azure:

- [10.3 FreeBSD em Olá Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 FreeBSD em Olá Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Criar uma VM de FreeBSD através da CLI do Azure 2.0 no FreeBSD
Primeiro tem de tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) apesar de os seguintes comandos numa máquina FreeBSD.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Se bash não está instalado no seu computador FreeBSD, execute os seguintes comandos antes da instalação de Olá. 

```bash
sudo pkg install bash
```

Se o python não está instalado no seu computador FreeBSD, execute os seguintes comandos antes da instalação de Olá. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Durante a instalação de Olá, é-lhe perguntado `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Se responder `y` e introduza `/etc/rc.conf` como `a path tooan rc file tooupdate`, pode satisfazer problema Olá `ERROR: [Errno 13] Permission denied`. tooresolve este problema, só deverá conceder Olá escrita toocurrent direita utilizador ficheiro Olá `etc/rc.conf`.

Agora pode iniciar sessão no Azure e criar a VM FreeBSD. Segue-se um exemplo toocreate FreeBSD 11.0 VM. Também pode adicionar parâmetro Olá `--public-ip-address-dns-name` com um nome globalmente exclusivo de DNS para um IP público criado recentemente. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

Em seguida, pode iniciar sessão no tooyour FreeBSD VM através do endereço de ip de Olá impresso na saída de Olá de acima implementação. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Extensões VM para FreeBSD
Seguem-se as extensões de VM suportadas no FreeBSD.

### <a name="vmaccess"></a>VMAccess
Olá [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extensão pode:

* Repor Olá palavra-passe de utilizador de sudo original Olá.
* Crie um novo utilizador de sudo com palavra-passe de Olá especificada.
* Definir a chave de anfitrião público de Olá com a chave de Olá fornecido.
* Repor chave de anfitrião público Olá fornecido durante a chave de anfitrião Olá é se não for indicado de aprovisionamento de VM.
* Abra a porta SSH Olá (22) e restaurar Olá sshd_config se reset_ssh estiver definido tootrue.
* Remova Olá de utilizador existente.
* Verifique os discos.
* Repare um disco adicionado.

### <a name="customscript"></a>CustomScript
Olá [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extensão pode:

* Se for indicado, transfira scripts de Olá personalizado do Storage do Azure ou armazenamento público externo (por exemplo, o GitHub).
* Execute script de ponto de entrada Olá.
* Suporta comandos inline.
* Converta o estilo de Windows tabulação na shell e Python scripts automaticamente.
* Remova automaticamente LM na shell e Python scripts.
* Proteger os dados confidenciais do CommandToExecute.

> [!NOTE]
> FreeBSD VM só suporta CustomScript versão 1. x, por agora.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Autenticação: os nomes de utilizador, palavras-passe e chaves SSH
Quando estiver a criar uma máquina virtual de FreeBSD utilizando Olá portal do Azure, tem de fornecer um nome de utilizador, palavra-passe ou chave pública SSH.
Para implementar uma máquina virtual de FreeBSD no Azure, os nomes de utilizador não tem de corresponder ao nomes das contas de sistema (UID < 100) já está presente na máquina virtual de Olá ("raiz", por exemplo).
Atualmente, apenas Olá RSA chave SSH é suportado. Tem de começar com uma chave SSH com várias linhas `---- BEGIN SSH2 PUBLIC KEY ----` e terminar com `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>A obtenção de privilégios de Superutilizador
conta de utilizador Olá, que é especificada durante a implementação da instância de máquina virtual no Azure é uma conta com privilégios. Olá pacote de sudo foi instalado no Olá publicados FreeBSD imagem.
Depois de que tem sessão iniciada através desta conta de utilizador, pode executar comandos como raiz utilizando a sintaxe do comando Olá.

```
$ sudo <COMMAND>
```

Opcionalmente, pode obter uma shell de raiz utilizando `sudo -s`.

## <a name="known-issues"></a>Problemas conhecidos
Olá [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.2 tem um [problema conhecido] (https://github.com/Azure/WALinuxAgent/pull/517) que faz com que a falha de aprovisionar Olá para FreeBSD VM no Azure. Olá correção capturada pelos [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.3 e versões posteriores. 

## <a name="next-steps"></a>Passos seguintes
* Aceda demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate uma VM FreeBSD.
* Se pretender que toobring o seus próprios tooAzure FreeBSD, consulte demasiado[criar e carregar um FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).
