---
title: aaaGet um ID de VM do Linux do Azure | Microsoft Docs
description: "Descreve como tooget e utilizar um único de VM do Azure Linux ID."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Aceder e utilizar ID exclusivo da VM do Azure
ID exclusivo de VM do Azure é um identificador de 128bits codificado armazenados em GUID do SMBIOS do todas as do Azure IaaS VMS e atualmente pode ser lidos utilizando comandos de BIOS da plataforma.

ID exclusivo de VM do Azure é uma propriedade só de leitura. ID exclusivo de VM do Azure não mudará após encerramento de reinício (está a ser planeada não planeada), iniciar/parar anula a alocação, autorrecuperação do serviço ou restaure no local. No entanto, se Olá VM é um instantâneo e copiado toocreate uma nova instância, o novo ID de VM do Azure está configurado.

> [!NOTE]
> Se tiver VMs mais antigas, criadas e, em execução, uma vez que esta nova funcionalidade foi implementada (18 de Setembro de 2014), reinicie o seu tooautomatically VM obter um ID exclusivo do Azure.
> 
> 

tooaccess Azure VM um ID exclusivo do dentro Olá VM:

## <a name="create-a-vm"></a>Criar uma VM
Para obter mais informações, consulte [criar uma Máquina Virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Ligar toohello VM
Para obter mais informações, consulte [SSH do Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>ID exclusivo de VM de consulta
Comando (exemplo utiliza **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Exemplo esperado resultados:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

Devido a tooBig bit Endian ordenação, hello real ID exclusivo da VM neste caso, serão:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

ID exclusivo de VM do Azure pode ser utilizado em cenários diferentes se Olá VM está em execução no Azure ou no local e pode ajudar os seus requisitos de controlo de licenciamento, relatórios ou gerais que pode ter de implementações do IaaS do Azure. Muitos fornecedores independentes de software de criação de aplicações e certificá-las no Azure podem exigir tooidentify uma VM do Azure ao longo do respetivo ciclo de vida e tootell se Olá VM está em execução no Azure, no local ou outros fornecedores de nuvem. Este identificador de plataforma por exemplo pode ajudar a detetar se o software de Olá está devidamente licenciado ou ajudar toocorrelate qualquer origem de tooits de dados VM, tais como tooassist sobre a configuração de métricas de direito de Olá para plataforma direita Olá e tootrack e correlacionar estas métricas entre outras utilizações.

