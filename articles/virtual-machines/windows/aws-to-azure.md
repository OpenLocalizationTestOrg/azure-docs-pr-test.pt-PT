---
title: aaaMove um tooAzure VMs do Windows AWS | Microsoft Docs
description: "Mova um tooAzure de instância do Amazon Web Services (AWS) EC2 Windows máquinas virtuais com o Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Mover uma VM do Windows de tooAzure Amazon Web Services (AWS) com o PowerShell

Se estiver a avaliar virtual machines do Azure para alojar cargas de trabalho, pode exportar uma instância de VM do Windows do Amazon Web Services (AWS) EC2 existente e carregar Olá tooAzure de disco rígido virtual (VHD). Uma vez Olá que VHD é carregada, pode criar uma nova VM no Azure de Olá VHD. 

Este tópico aborda a mover de uma única VM de AWS tooAzure. Se pretender toomove VMs do AWS tooAzure à escala, veja [migrar máquinas virtuais no tooAzure Amazon Web Services (AWS) com o Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Preparar Olá VM 
 
Pode carregar tooAzure de VHDs generalizado e especializado. Cada tipo requer a preparação Olá VM antes de exportar a partir do AWS. 

- **Generalizado VHD** -um VHD generalizado apresentou todas as informações da sua conta pessoal removidas utilizando Sysprep. Se tenciona toouse Olá VHD como uma imagem toocreate novas VMs do, deve: 
 
    * [Preparar uma VM do Windows](prepare-for-upload-vhd-image.md).  
    * Generalize a máquina virtual de Olá utilizando Sysprep.  

 
- **Especializada VHD** -um VHD especializado mantém as contas de utilizador Olá, aplicações e outros dados de estado de original VM. Se tenciona toouse Olá VHD-é toocreate uma nova VM, certifique-se de que Olá os passos seguintes é concluída.  
    * [Preparar uma tooAzure tooupload do VHD do Windows](prepare-for-upload-vhd-image.md). **Não** generalizar Olá VM com o Sysprep. 
    * Remova quaisquer agentes que estão instalados no Olá VM (ou seja, as ferramentas do VMware) e ferramentas de Virtualização do convidado. 
    * Certifique-se Olá VM é toopull configurado o endereço IP e as definições de DNS através do DHCP. Isto garante que o servidor Olá obtém um endereço IP no Olá VNet durante o arranque.  


## <a name="export-and-download-hello-vhd"></a>Exportar e transferir Olá VHD 

Exporte Olá EC2 instância tooa VHD num registo de Amazon S3. Siga os passos de Olá descritos no tópico de documentação do Amazon Olá [exportar uma instância como uma VM utilizando o VM para importar/exportar](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) e execução Olá [criar instância-exportação-tarefas](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) Olá tooexport do comando EC2 ficheiro VHD tooa de instância. 

Olá exportado ficheiro VHD é guardado no registo de Olá Amazon S3 que especificar. Olá sintaxe básica para exportar Olá VHD está abaixo, apenas substituir o texto do marcador de posição de Olá no <brackets> com as suas informações.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Assim que tenha sido exportada Olá VHD, siga instruções Olá [como transferir um objeto de um registo de S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) Olá toodownload VHD do ficheiro de registo de Olá S3. 

> [!IMPORTANT]
> AWS cobra taxas de transferência de dados para a transferência Olá VHD. Consulte [preços do Amazon S3](https://aws.amazon.com/s3/pricing/) para obter mais informações.


## <a name="next-steps"></a>Passos seguintes

Agora pode carregar Olá VHD tooAzure e criar uma nova VM. 

- Se tiver executado Sysprep na sua origem demasiado**Generalizar** -lo antes de exportar, consulte [carregar um VHD generalizado e utilizá-la toocreate um novas VMs no Azure](upload-generalized-managed.md)
- Se não foi possível executar o Sysprep antes de exportar, hello VHD é considerado **especializadas**, consulte [carregar um tooAzure especializada do VHD e criar uma nova VM](create-vm-specialized.md)

 
