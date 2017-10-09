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
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="94c13-103">Mover uma VM do Windows de tooAzure Amazon Web Services (AWS) com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="94c13-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="94c13-104">Se estiver a avaliar virtual machines do Azure para alojar cargas de trabalho, pode exportar uma instância de VM do Windows do Amazon Web Services (AWS) EC2 existente e carregar Olá tooAzure de disco rígido virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="94c13-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="94c13-105">Uma vez Olá que VHD é carregada, pode criar uma nova VM no Azure de Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="94c13-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="94c13-106">Este tópico aborda a mover de uma única VM de AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="94c13-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="94c13-107">Se pretender toomove VMs do AWS tooAzure à escala, veja [migrar máquinas virtuais no tooAzure Amazon Web Services (AWS) com o Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="94c13-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="94c13-108">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="94c13-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="94c13-109">Pode carregar tooAzure de VHDs generalizado e especializado.</span><span class="sxs-lookup"><span data-stu-id="94c13-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="94c13-110">Cada tipo requer a preparação Olá VM antes de exportar a partir do AWS.</span><span class="sxs-lookup"><span data-stu-id="94c13-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="94c13-111">**Generalizado VHD** -um VHD generalizado apresentou todas as informações da sua conta pessoal removidas utilizando Sysprep.</span><span class="sxs-lookup"><span data-stu-id="94c13-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="94c13-112">Se tenciona toouse Olá VHD como uma imagem toocreate novas VMs do, deve:</span><span class="sxs-lookup"><span data-stu-id="94c13-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="94c13-113">[Preparar uma VM do Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="94c13-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="94c13-114">Generalize a máquina virtual de Olá utilizando Sysprep.</span><span class="sxs-lookup"><span data-stu-id="94c13-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="94c13-115">**Especializada VHD** -um VHD especializado mantém as contas de utilizador Olá, aplicações e outros dados de estado de original VM.</span><span class="sxs-lookup"><span data-stu-id="94c13-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="94c13-116">Se tenciona toouse Olá VHD-é toocreate uma nova VM, certifique-se de que Olá os passos seguintes é concluída.</span><span class="sxs-lookup"><span data-stu-id="94c13-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="94c13-117">[Preparar uma tooAzure tooupload do VHD do Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="94c13-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="94c13-118">**Não** generalizar Olá VM com o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="94c13-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="94c13-119">Remova quaisquer agentes que estão instalados no Olá VM (ou seja, as ferramentas do VMware) e ferramentas de Virtualização do convidado.</span><span class="sxs-lookup"><span data-stu-id="94c13-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="94c13-120">Certifique-se Olá VM é toopull configurado o endereço IP e as definições de DNS através do DHCP.</span><span class="sxs-lookup"><span data-stu-id="94c13-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="94c13-121">Isto garante que o servidor Olá obtém um endereço IP no Olá VNet durante o arranque.</span><span class="sxs-lookup"><span data-stu-id="94c13-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="94c13-122">Exportar e transferir Olá VHD</span><span class="sxs-lookup"><span data-stu-id="94c13-122">Export and download hello VHD</span></span> 

<span data-ttu-id="94c13-123">Exporte Olá EC2 instância tooa VHD num registo de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="94c13-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="94c13-124">Siga os passos de Olá descritos no tópico de documentação do Amazon Olá [exportar uma instância como uma VM utilizando o VM para importar/exportar](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) e execução Olá [criar instância-exportação-tarefas](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) Olá tooexport do comando EC2 ficheiro VHD tooa de instância.</span><span class="sxs-lookup"><span data-stu-id="94c13-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="94c13-125">Olá exportado ficheiro VHD é guardado no registo de Olá Amazon S3 que especificar.</span><span class="sxs-lookup"><span data-stu-id="94c13-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="94c13-126">Olá sintaxe básica para exportar Olá VHD está abaixo, apenas substituir o texto do marcador de posição de Olá no <brackets> com as suas informações.</span><span class="sxs-lookup"><span data-stu-id="94c13-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="94c13-127">Assim que tenha sido exportada Olá VHD, siga instruções Olá [como transferir um objeto de um registo de S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) Olá toodownload VHD do ficheiro de registo de Olá S3.</span><span class="sxs-lookup"><span data-stu-id="94c13-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="94c13-128">AWS cobra taxas de transferência de dados para a transferência Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="94c13-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="94c13-129">Consulte [preços do Amazon S3](https://aws.amazon.com/s3/pricing/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="94c13-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94c13-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="94c13-130">Next steps</span></span>

<span data-ttu-id="94c13-131">Agora pode carregar Olá VHD tooAzure e criar uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="94c13-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="94c13-132">Se tiver executado Sysprep na sua origem demasiado**Generalizar** -lo antes de exportar, consulte [carregar um VHD generalizado e utilizá-la toocreate um novas VMs no Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="94c13-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="94c13-133">Se não foi possível executar o Sysprep antes de exportar, hello VHD é considerado **especializadas**, consulte [carregar um tooAzure especializada do VHD e criar uma nova VM](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="94c13-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
