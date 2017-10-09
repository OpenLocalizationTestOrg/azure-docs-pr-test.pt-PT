---
title: par de chaves aaaDetailed passos toocreate um SSH para VMs com Linux no Azure | Microsoft Docs
description: "Saiba mais passos adicionais toocreate um par de chaves público e privado SSH para VMs com Linux no Azure, juntamente com certificados específicos para os casos de utilização diferentes."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Instruções detalhada sobre o toocreate um par de chaves SSH e certificados adicionais para uma VM com Linux no Azure
Com um par de chaves SSH, pode criar máquinas virtuais no Azure predefinido toousing chaves SSH para a autenticação, eliminando a necessidade de Olá de palavras-passe toolog no. As palavras-passe podem ser adivinhadas e abrir as suas VMs segurança toorelentless força bruta tentativas tooguess a palavra-passe. VMs criadas com modelos de Olá CLI do Azure ou o Gestor de recursos podem incluir a chave pública SSH como parte da implementação de Olá, remover um passo de configuração de implementação de post da desativação de inícios de sessão de palavra-passe para SSH. Este artigo fornece os passos detalhados e exemplos adicionais de geração de certificados, tal como para utilização com máquinas virtuais do Linux. Se quiser tooquickly criar e utilizar um par de chaves SSH, consulte [como toocreate uma chave de pública e privada SSH emparelhe para VMs com Linux no Azure](mac-create-ssh-keys.md).

## <a name="understanding-ssh-keys"></a>Noções sobre chaves SSH

A utilização de chaves públicas e privadas de SSH é Olá toolog de forma mais fácil em servidores de Linux tooyour. [Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de forma muito mais segura no tooyour Linux ou na VM BSD no Azure que as palavras-passe, que podem ser ataque de força bruta mais facilmente.

A sua chave pública pode ser partilhada com qualquer pessoa; mas apenas o utilizador (ou a infraestrutura de segurança local) possui a chave privada.  a chave privada SSH Olá deve ter um [palavra-passe muito segura](https://www.xkcd.com/936/) (origem:[xkcd.com](https://xkcd.com)) toosafeguard-lo.  Esta palavra-passe é apenas tooaccess Olá SSH ficheiro de chave privada e **não é** palavra-passe de conta de utilizador Olá.  Quando adiciona uma chave SSH tooyour palavra-passe, encripta a chave privada Olá utilizando AES de 128 bits, para que hello chave privada é inútil sem Olá palavra-passe toodecrypt-lo.  Se um atacante stole a chave privada e que a chave não tinha uma palavra-passe, este seria capaz de toouse ou privada chave toolog nos servidores de tooany ter Olá de chave pública correspondente.  Se a chave privada for protegida por palavra-passe, não pode ser utilizada por esse atacante, fornecendo uma camada adicional de segurança à sua infraestrutura no Azure.

Este artigo cria uma versão de protocolo SSH que par de ficheiro de chave pública e privada do 2 RSA (também referida tooas "ssh-rsa" chaves), que é recomendados para implementações com o Azure Resource Manager. *SSH-rsa* chaves são necessárias no Olá [portal](https://portal.azure.com) para implementações do Resource Manager e clássico.

## <a name="ssh-keys-use-and-benefits"></a>Utilização e vantagens das chaves SSH

O Azure requer, pelo menos, 2048 bits, o SSH protocolo versão 2 RSA formato chaves públicas e privadas; o ficheiro de chave pública Olá tem Olá `.pub` formato de contentor. utilização de chaves toocreate Olá `ssh-keygen`, que pede-lhe uma série de perguntas e, em seguida, escreve uma chave privada e uma chave pública correspondente. Quando é criada uma VM do Azure, Azure cópias Olá toohello de chave pública `~/.ssh/authorized_keys` pasta Olá VM. As chaves SSH no `~/.ssh/authorized_keys` são utilizados toochallenge Olá cliente toomatch Olá chave privada correspondente numa ligação de início de sessão SSH.  Quando uma VM com Linux do Azure é criada a utilizar chaves SSH para a autenticação, o Azure configura Olá SSHD server toonot permite inícios de sessão de palavra-passe, apenas as chaves SSH.  Por conseguinte, através da criação de VMs do Linux do Azure com chaves SSH, pode ajudar a proteger a implementação da VM Olá e guardar si próprio passo de configuração pós-implementação típica Olá da desativação de palavras-passe em Olá **sshd_config** ficheiro.

## <a name="using-ssh-keygen"></a>Utilizar o ssh-keygen

Este comando cria uma palavra-passe protegida (encriptado) par de chaves SSH com o RSA de 2048 bits e é comentado tooeasily identificá-lo.  

SSH chaves são por predefinição mantida na Olá `~/.ssh` diretório.  Se não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando criá-lo por si com Olá permissões corretas.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*Comando explicado*

`ssh-keygen`= Olá programa utilizado toocreate Olá chaves

`-t rsa`= o tipo de chave toocreate que é o formato RSA Olá [wikipedia][parens no fim](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits da chave de Olá

`-C "azureuser@myserver"`= um comentário final toohello anexado tooeasily do ficheiro de chave pública de Olá identificá-lo.  Normalmente, uma mensagem de e-mail é utilizada como comentários de Olá, mas pode utilizar o que funciona melhor para a sua infraestrutura.

## <a name="classic-deploy-using-asm"></a>Implementação clássica com `asm`

Se estiver a utilizar o modelo de implementação clássica Olá (`asm` modo no Olá CLI), pode utilizar uma chave pública SSH-RSA ou um RFC4716 formatado chave num contentor pem.  chave pública Olá SSH-RSA é o que foi criado anteriormente no utilizando artigo `ssh-keygen`.

toocreate um RFC4716 formatado chave a partir de uma chave pública SSH:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Exemplo de ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Ficheiros de chave guardados:

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

nome do par de chaves de Olá para este artigo.  Ter um par de chaves com o nome **id_rsa** Olá predefinido e algumas ferramentas podem contar Olá **id_rsa** nome de ficheiro de chave privada, de modo que é uma boa ideia. diretório de Olá `~/.ssh/` é Olá localização predefinida pares de chaves SSH e o ficheiro de configuração SSH Olá.  Se não for especificado com um caminho completo, `ssh-keygen` cria chaves Olá no diretório de trabalho atual Olá, não predefinido de Olá `~/.ssh`.

Obter uma listagem de Olá `~/.ssh` diretório.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

Palavra-passe da chave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`refere-se a palavra-passe de tooa para o ficheiro de chave privada Olá como "uma frase de acesso."  É *vivamente* recomendado tooadd uma chave privada de tooyour de palavra-passe. Sem um palavra-passe proteção Olá ficheiro de chave, qualquer pessoa com ficheiros Olá pode utilizá-la toolog no servidor de tooany que tem Olá de chave pública correspondente. Adicionar uma palavra-passe (frase de acesso) proporciona proteção mais no caso de alguém toogain capaz de acesso tooyour ficheiro de chave privada, dando-lhe as chaves do tempo toochange Olá utilizado tooauthenticate.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Utilizar o ssh-agent toostore a palavra-passe da chave privada

tooavoid escrever a palavra-passe do ficheiro de chave privada com cada início de sessão SSH, pode utilizar `ssh-agent` toocache a palavra-passe do ficheiro de chave privada. Se estiver a utilizar um Mac, Olá OSX Keychain armazena Olá privada chave palavras-passe em segurança quando invocar `ssh-agent`.

Certifique-se e utilizar o ssh-agent e ssh-adicionar tooinform Olá SSH sistema sobre ficheiros de chave Olá, para que o frase de acesso de Olá não terá de toobe utilizado de forma interativa.

```bash
eval "$(ssh-agent -s)"
```

Agora adicione chave privada Olá demasiado`ssh-agent` utilizando o comando de Olá `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Olá chave palavra-passe privada está agora armazenado numa `ssh-agent`.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>Utilizar `ssh-copy-id` toocopy Olá tooan chave existente VM
Se já tiver criado uma VM pode instalar Olá novo SSH pública chave tooyour VM com Linux com:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Criar e configurar um ficheiro de configuração SSH

É um toocreate de melhores práticas recomendadas e configurar um `~/.ssh/config` toospeed de ficheiro dos inícios de sessão e para otimizar o seu comportamento do cliente SSH.

Olá seguinte exemplo mostra uma configuração padrão.

### <a name="create-hello-file"></a>Criar ficheiro de Olá

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Edite Olá ficheiro tooadd Olá nova configuração de SSH:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Ficheiro `~/.ssh/config` de exemplo:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Esta configuração SSH fornecem lhe secções para cada servidor tooenable cada toohave seu próprio par de chaves dedicado. Olá predefinições (`Host *`) são para quaisquer anfitriões que não corresponde a nenhum dos Olá anfitriões específicos superiores cópias de segurança no ficheiro de configuração de Olá.

### <a name="config-file-explained"></a>Ficheiro de configuração explicado

`Host`= o nome de Olá do anfitrião de Olá a ser chamado no Olá terminal.  `ssh fedora22`indica `SSH` valores de Olá toouse no bloco de definições de Olá etiquetadas `Host fedora22` Nota: anfitrião pode ser qualquer etiqueta que seja lógica para a sua utilização e não representa o nome do anfitrião real Olá de qualquer servidor.

`Hostname 102.160.203.241`= o endereço IP de Olá ou nome DNS para o servidor de Olá acedido.

`User ahmet`= toouse de conta de utilizador remoto Olá quando iniciam sessão no servidor de toohello.

`PubKeyAuthentication yes`= Indica a SSH pretende toouse um toolog de chave SSH.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= a chave privada SSH Olá e correspondente toouse de chave pública para autenticação.

## <a name="ssh-into-linux-without-a-password"></a>SSH no Linux sem uma palavra-passe

Agora que tem um par de chaves SSH e um ficheiro de configuração SSH configurado, é capaz de toolog no tooyour VM com Linux rapidamente e em segurança. Olá pela primeira vez que iniciar a sessão no servidor de tooa utilizando um linhas de comandos de Olá chave SSH, para a frase de acesso de Olá para esse ficheiro de chave.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Comando explicado

Quando `ssh fedora22` é executado SSH primeiro localiza e carrega todas as definições de Olá `Host fedora22` bloco e, em seguida, carrega todas Olá restantes definições do Olá último bloqueio, `Host *`.

## <a name="next-steps"></a>Passos Seguintes

Em seguida cópias de segurança é toocreate VMs do Linux do Azure utilizando Olá nova chave pública SSH.  As VMs do Azure que são criadas com uma chave pública SSH como início de sessão Olá melhor são protegidas que VMs criadas com o método de início de sessão predefinido de Olá, palavras-passe.  As VMs do Azure criadas com chaves SSH são, por predefinição, configuradas com as palavras-passe desativadas, evitando tentativas de adivinhação forçadas.

* [Criar uma VM do Linux segura com um modelo do Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM com Linux segura utilizando Olá portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM com Linux segura utilizando Olá CLI do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
