---
title: par de chaves aaaCreate um SSH para VMs com Linux no Azure | Microsoft Docs
description: "Criar um par de chaves pública e privada SSH para as VMs do Azure Linux de forma segura."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Criar um par de chaves pública e privada SSH para as VMs do Linux

Este artigo mostra como toogenerate uma protocol versão 2 RSA pública e privada chave SSH ficheiro par toouse com VMs com Linux.  Com um par de chaves SSH, pode criar máquinas virtuais no Azure predefinido toousing chaves SSH para a autenticação, eliminando a necessidade de Olá de palavras-passe toolog no.  As palavras-passe podem ser adivinhadas e abrir as suas VMs segurança toorelentless força bruta tentativas tooguess a palavra-passe. VMs criadas com modelos do Azure ou Olá `azure-cli` podem incluir a chave pública SSH como parte da implementação de Olá, remover um passo de configuração de implementação de post da desativação de inícios de sessão de palavra-passe para SSH.

## <a name="quick-commands"></a>Comandos Rápidos

Execute Olá os seguintes comandos da shell de deteção, substituindo os exemplos de Olá com as seus próprios opções.

O ficheiro de chave pública SSH é criado por predefinição em `~/.ssh/id_rsa.pub`. Quando lhe for pedido Olá os seguintes comandos a utilizar, deve criar uma "frase de acesso" toosecure a chave privada. (o frase de acesso de Olá é que uma palavra-passe utilizada tooencrypt a chave privada.)

```bash
ssh-keygen -t rsa -b 2048 
```

Adicionar chave de Olá recém-criado demasiado`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> Olá acima trabalho comandos em sistemas operativos Linux quase todas as distribuições, mas não necessariamente funcionam nos contentores, como o ambiente de Olá pode forma radicalmente restrita. 

## <a name="detailed-walkthrough"></a>Instruções Detalhadas

A utilização de chaves públicas e privadas de SSH é Olá toolog de forma mais fácil em servidores de Linux tooyour. [Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de forma muito mais segura no tooyour Linux ou na VM BSD no Azure que as palavras-passe, que podem ser ataque de força bruta mais facilmente.

> [!IMPORTANT]
> A sua chave pública pode ser partilhada com qualquer pessoa; mas apenas o utilizador (ou a infraestrutura de segurança local) possui a chave privada.  a chave privada SSH Olá deve ter um [palavra-passe muito segura](https://www.xkcd.com/936/) (origem:[xkcd.com](https://xkcd.com)) toosafeguard-lo.  Esta palavra-passe é a chave privada de SSH do tooaccess apenas Olá e **não é** palavra-passe de conta de utilizador Olá.  Quando adiciona uma chave SSH tooyour palavra-passe, encripta a chave privada Olá utilizando AES de 128 bits, para que hello chave privada é inútil sem Olá palavra-passe toodecrypt-lo.  Se um atacante stole a chave privada e que a chave não tinha uma palavra-passe, este seria capaz de toouse ou privada chave toolog nos servidores de tooany ter Olá de chave pública correspondente.  Se a chave privada for protegida por palavra-passe, não pode ser utilizada por esse atacante, fornecendo uma camada adicional de segurança à sua infraestrutura no Azure.

Este artigo cria a versão do protocolo SSH 2 RSA públicos e privados ficheiros de chaves, que são recomendados para implementações em Olá Resource Manager.  *SSH-rsa* chaves são necessárias no Olá [portal](https://portal.azure.com) para implementações do Resource Manager e clássico.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>Desativar as palavras-passe SSH com as chaves SSH

O Azure requer, pelo menos, 2048 bits e chaves públicas e privadas com o formato ssh-rsa. utilização de chaves toocreate Olá `ssh-keygen`, que pede-lhe uma série de perguntas e, em seguida, escreve uma chave privada e uma chave pública correspondente. Quando é criada uma VM do Azure, chave pública Olá é copiado demasiado`~/.ssh/authorized_keys`.  As chaves SSH no `~/.ssh/authorized_keys` são utilizados toochallenge Olá cliente toomatch Olá chave privada correspondente numa ligação de início de sessão SSH.  Quando uma VM com Linux do Azure é criada a utilizar chaves SSH para a autenticação, o Azure configura Olá SSHD server toonot permite inícios de sessão de palavra-passe, apenas as chaves SSH.  Por conseguinte, através da criação de VMs do Linux do Azure com chaves SSH, pode ajudar a implementação da VM Olá segura e guardar pessoalmente o passo de configuração pós-implementação típica Olá da desativação de palavras-passe no ficheiro de configuração de sshd_config Olá.

## <a name="using-ssh-keygen"></a>Utilizar o ssh-keygen

Este comando cria uma palavra-passe protegida (encriptado) par de chaves SSH com o RSA de 2048 bits e é comentado tooeasily identificá-lo.  

SSH chaves são por predefinição mantida na Olá `~/.ssh` diretório.  Se não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando criá-lo por si com Olá permissões corretas.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Comando explicado*

`ssh-keygen`= Olá programa utilizado toocreate Olá chaves

`-t rsa`= o tipo de chave toocreate que é o formato RSA Olá [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`= bits da chave de Olá


## <a name="classic-portal-and-x509-certs"></a>Portal clássico e certificados X.509

Se estiver a utilizar Olá Azure [portal clássico](https://manage.windowsazure.com/), necessita de certificados x. 509 para chaves SSH Olá.  Não existem outros tipos de chaves públicas SSH permitidas, estas *devem* ser certificados X.509.

toocreate um certificado x. 509 da sua chave privada de SSH-RSA existente:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Implementação clássica com `asm`

Se estiver a utilizar clássico Olá implementar a modelo (gestão de serviço do Azure CLI `asm`), pode utilizar uma chave pública SSH-RSA ou um RFC4716 formatado chave num **. pem** contentor.  chave pública Olá SSH-RSA é o que foi criado anteriormente no utilizando artigo `ssh-keygen`.

toocreate um RFC4716 formatado chave a partir de uma chave pública SSH:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Exemplo de ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

nome do par de chaves de Olá para este artigo.  Ter um par de chaves com o nome **id_rsa** Olá predefinido e algumas ferramentas podem contar Olá **id_rsa** nome de ficheiro de chave privada, de modo que é uma boa ideia. diretório de Olá `~/.ssh/` é Olá localização predefinida pares de chaves SSH e o ficheiro de configuração SSH Olá.  Se não for especificado com um caminho completo, `ssh-keygen` irá criar chaves Olá no diretório de trabalho atual Olá, não Olá predefinido `~/.ssh`.

Obter uma listagem de Olá `~/.ssh` diretório.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Palavra-passe da chave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`refere-se a chave privada do tooa palavra-passe utilizada tooencrypt Olá como "uma frase de acesso."  É *vivamente* recomendado tooadd pares de chaves de tooyour uma frase de acesso. Sem uma frase de acesso proteção Olá chave privada, qualquer pessoa com o ficheiro de chave Olá pode utilizá-la toolog no servidor de tooany que tem Olá de chave pública correspondente. Adicionar uma frase de acesso oferece mais proteção no caso de alguém toogain capaz de acesso tooyour ficheiro de chave privada, dando-lhe as chaves do tempo toochange Olá utilizado tooauthenticate.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Utilizar o ssh-agent toostore a palavra-passe da chave privada

frase de acesso do ficheiro tooavoid escrever a sua chave privada com cada início de sessão SSH, pode utilizar `ssh-agent` toocache a palavra-passe do ficheiro de chave privada. Se estiver a utilizar um Mac, Olá OSX Keychain armazena Olá privada chave palavras-passe em segurança quando invocar `ssh-agent`.

Certifique-se e utilizar `ssh-agent` e `ssh-add` tooinform Olá SSH sistema sobre ficheiros de chave Olá, para que o frase de acesso de Olá não terá de toobe utilizado de forma interativa.

```bash
eval "$(ssh-agent -s)"
```

Agora adicione chave privada Olá demasiado`ssh-agent` utilizando o comando de Olá `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Olá chave palavra-passe privada está agora armazenado numa `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>Utilizar `ssh-copy-id` nova chave de tooinstall Olá
Se já tiver criado uma VM pode instalar Olá novo SSH pública chave tooyour VM com Linux com Olá comando a seguir, substituindo o nome de utilizador do Olá VM e o endereço do servidor Olá com os seus próprios valores:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Criar e configurar um ficheiro de configuração SSH

É uma melhor toocreate de prática e configurar um `~/.ssh/config` toospeed de ficheiro dos inícios de sessão e para otimizar o seu comportamento do cliente SSH.

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

Em seguida cópias de segurança é toocreate VMs do Linux do Azure utilizando Olá nova chave pública SSH.  As VMs do Azure que são criadas com uma chave pública SSH como início de sessão Olá melhor são protegidas que VMs criadas com o método de início de sessão predefinido de Olá, palavras-passe.  As VMs do Azure criadas com chaves SSH são, por predefinição, configuradas com as palavras-passe desativadas, evitando tentativas de adivinhação forçadas. Se necessitar de mais assistência na criação do par de chaves SSH ou necessitam de certificados adicionais, tais como para utilização com o portal clássico Olá, consulte [detalhadas pares de chaves SSH do passos toocreate e certificados](create-ssh-keys-detailed.md).

* [Criar uma VM do Linux segura com um modelo do Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM com Linux segura utilizando Olá portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM com Linux segura utilizando Olá CLI do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
