---
title: aaaMove ficheiros tooand de VMs do Linux do Azure com o SCP | Microsoft Docs
description: "Mover em segurança tooand de ficheiros de uma VM com Linux no Azure utilizando o SCP e um par de chaves SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Mover tooand de ficheiros de uma VM com Linux através de SCP

Este artigo mostra como toomove ficheiros de cópia de segurança tooan VM do Linux do Azure a estação de trabalho ou de uma VM do Azure Linux baixo tooyour estação de trabalho, utilizando Secure cópia (SCP). Mover ficheiros entre a estação de trabalho e de uma VM com Linux, rapidamente e segura, é essencial para gerir a sua infraestrutura do Azure. 

Para este artigo, é necessário um Linux VM implementado no Azure com [ficheiros de chaves públicos e privados SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Também precisa de um cliente de SCP para o seu computador local. É desenvolvida com SSH e incluído na shell de deteção predefinidas Olá da maioria dos computadores Linux e Mac e algumas shells do Windows.

## <a name="quick-commands"></a>Comandos rápidos

Copiar um ficheiro de cópia de segurança toohello VM com Linux

```bash
scp file azureuser@azurehost:directory/targetfile
```

Copie um ficheiro de Olá VM com Linux

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Instruções detalhadas

Como exemplos, podemos mover um ficheiro de configuração do Azure se tooa VM com Linux e obtenha um diretório do ficheiro de registo, ambos utilizando chaves SCP e SSH.   

## <a name="ssh-key-pair-authentication"></a>Autenticação do par de chaves SSH

SCP utiliza SSH para a camada de transporte Olá. SSH identificadores Olá autenticação no anfitrião de destino Olá, e este move-Olá num túnel encriptado fornecido por predefinição com SSH. Para a autenticação SSH, podem ser utilizadas nomes de utilizador e palavras-passe. No entanto, a autenticação de chave pública e privada SSH são recomendadas como melhor prática de segurança. Uma vez SSH tem autenticado ligação Olá, o SCP começa, em seguida, ao copiar o ficheiro de Olá. Utilizar está corretamente configurada `~/.ssh/config` e SSH chaves públicas e privadas, ligação Olá SCP podem ser estabelecidas pela utilização de apenas um nome de servidor (ou endereço IP). Se tiver apenas uma chave SSH, SCP procura-lo no Olá `~/.ssh/` diretório e utiliza-o por predefinição toolog no toohello VM.

Para obter mais informações sobre como configurar a sua `~/.ssh/config` e chaves públicas e privadas SSH, consulte [criar SSH chaves](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP tooa um ficheiro VM com Linux

Para o primeiro exemplo Olá, iremos copiar um ficheiro de configuração do Azure se tooa VM com Linux que é utilizado toodeploy automatização. Porque este ficheiro contém credenciais de API do Azure, nomeadamente segredos, segurança, é importante. túnel encriptados Olá fornecida pelo SSH protege o conteúdo de Olá do ficheiro de Olá.

Olá, os seguintes comandos cópias Olá local *.azure/configuração* tooan VM do Azure com o FQDN do ficheiro *myserver.eastus.cloudapp.azure.com*. nome de utilizador de admin Olá no Olá VM do Azure é *azureuser* . Olá ficheiro é visado toohello */home/azureuser/* diretório. Substitua os seus próprios valores neste comando.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>SCP um diretório de uma VM com Linux

Neste exemplo, vamos copiar um diretório de ficheiros de registo de Olá VM com Linux para baixo tooyour estação de trabalho. Um ficheiro de registo pode ou não pode conter dados confidenciais ou secretos. No entanto, utilizar o SCP garante conteúdo Olá Olá dos ficheiros de registo é encriptado. A utilização de ficheiros do SCP tootransfer Olá é tooget de forma mais fácil Olá Olá diretório de registo e ficheiros baixo tooyour estação de trabalho tendo simultaneamente segura.

Olá seguinte comando copia ficheiros Olá */homeazureuser/registos/* diretório no diretório /tmp dos locais do Olá VM do Azure toohello:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Olá `-r` cli sinalizador dá instruções ao ficheiros do SCP toorecursively cópia Olá e diretórios do ponto de Olá do diretório de Olá listado no comando Olá.  Tenha em atenção que Olá sintaxe da linha de comandos é também tooa semelhante `cp` copiar o comando.

## <a name="next-steps"></a>Passos seguintes

* [Gerir utilizadores, SSH e verificação ou discos de reparação em VMs do Linux do Azure utilizando Olá extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
