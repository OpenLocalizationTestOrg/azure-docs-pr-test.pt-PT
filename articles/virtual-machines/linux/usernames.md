---
title: aaaSelecting nomes de utilizador do Linux | Microsoft Docs
description: "Saiba como nomes de utilizador tooselect para uma máquina virtual do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Selecionar Nomes de Utilizador para Linux no Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Quando aprovisionar uma máquina virtual do Linux no Azure tem de especificar o nome de Olá de um utilizador não raiz que pode utilizar mais tarde toolog para Olá VM. Pode optar por nome de Olá do novo utilizador de Olá, ou se Olá, aprovisionamento através do portal clássico do Azure pode aceitar a predefinição de Olá azureuser"nome".

Na maioria dos casos, este utilizador não existe na imagem base Olá e será criado durante o processo de aprovisionamento de Olá. Se o utilizador Olá existe na imagem de VM base Olá, em seguida, agente Linux do Azure de Olá simplesmente configura palavra-passe de Olá e/ou a chave SSH para esse utilizador com base nas informações de Olá especificado ao criar Olá VM.

**No entanto**, Linux define um conjunto de nomes de utilizador que não deve ser utilizada. Olá irá do processo de aprovisionamento **falhar** se tentar tooprovision uma VM com Linux utilizando um utilizador existente de sistema, que é definido como um utilizador com UID 0 e 99. Um exemplo típico é Olá `root` utilizador, que tem UID 0.

* Consulte também: [Linux padrão Base - intervalos de ID de utilizador](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Olá segue-se uma lista de utilizadores de sistema incorporada comuns para CentOS e Ubuntu que deve evitar utilizar quando aprovisionar uma máquina virtual do Linux no Azure. Esta lista é apenas um exemplo, consulte toohello documentação para a distribuição tooensure esse nome de utilizador Olá optar por não causar conflito com um utilizador existente do sistema.

## <a name="centos"></a>CentOS
* abrt
* ADM
* áudio
* Reciclagem
* CD-ROM
* cgred
* daemon
* dbus
* dialout
* DIP
* disco
* disquetes
* FTP
* FTP
* jogos
* Gopher
* haldaemon
* parar
* kmem
* bloqueio
* LP
* capacidade de correio
* Man
* memória
* nfsnobody
* ninguém
* NTP
* operador
* oprofile
* postdrop
* sufixo
* qpidd
* raiz
* RPC
* rpcuser
* saslauth
* Encerramento
* slocate
* sshd
* stapdev
* stapusr
* Sincronização
* SYS
* banda
* Teste
* tcpdump
* TTY
* utilizadores
* utempter
* utmp
* UUCP
* vcsa
* vídeo
* roda

## <a name="ubuntu"></a>Ubuntu
* ADM
* Admin
* áudio
* cópia de segurança
* Reciclagem
* CD-ROM
* crontab
* daemon
* dialout
* DIP
* disco
* Fax
* disquetes
* fuse
* jogos
* gnats
* IRC
* kmem
* horizontal
* libuuid
* lista
* LP
* capacidade de correio
* Man
* messagebus
* mlocate
* netdev
* Notícias de última hora
* ninguém
* nogroup
* operador
* plugdev
* Proxy
* raiz
* SASL
* sombra de volumes
* SRC
* SSH
* sshd
* funcionários
* sudo
* Sincronização
* SYS
* syslog
* banda
* TTY
* utilizadores
* utmp
* UUCP
* vídeo
* voz
* whoopsie
* dados de www

