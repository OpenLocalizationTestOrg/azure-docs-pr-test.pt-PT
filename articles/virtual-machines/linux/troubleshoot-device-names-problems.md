---
title: nomes de dispositivos VM aaaLinux foram alterados no Azure | Microsoft Docs
description: "Explica Olá por que razão são alterados nomes de dispositivo e fornecem soluções para este problema."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="ff69b-103">Resolução de problemas: Os nomes de dispositivos de VM com Linux são alterados</span><span class="sxs-lookup"><span data-stu-id="ff69b-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="ff69b-104">artigo de Olá explica por que motivo os nomes de dispositivos são alterados depois de reiniciar uma máquina virtual (VM) do Linux ou reattach discos Olá.</span><span class="sxs-lookup"><span data-stu-id="ff69b-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="ff69b-105">Também fornece solução Olá para este problema.</span><span class="sxs-lookup"><span data-stu-id="ff69b-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="ff69b-106">Sintoma</span><span class="sxs-lookup"><span data-stu-id="ff69b-106">Symptom</span></span>

<span data-ttu-id="ff69b-107">Pode deparar-se Olá os seguintes problemas quando VMs do Linux em execução no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ff69b-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="ff69b-108">Olá VM falha tooboot após um reinício.</span><span class="sxs-lookup"><span data-stu-id="ff69b-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="ff69b-109">Se os discos de dados estiver desligados e novamente ligados, os nomes de dispositivos de Olá para os discos foram alterados.</span><span class="sxs-lookup"><span data-stu-id="ff69b-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="ff69b-110">Falha de uma aplicação ou script que faça referência a um disco com o nome do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff69b-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="ff69b-111">Determinar que Olá nome do dispositivo de disco Olá é alterado.</span><span class="sxs-lookup"><span data-stu-id="ff69b-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="ff69b-112">Causa</span><span class="sxs-lookup"><span data-stu-id="ff69b-112">Cause</span></span>

<span data-ttu-id="ff69b-113">Caminhos de dispositivo no Linux não são garantidos que toobe consistente entre reinícios.</span><span class="sxs-lookup"><span data-stu-id="ff69b-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="ff69b-114">Nomes de dispositivos é composto por principal (letra) e números secundários.</span><span class="sxs-lookup"><span data-stu-id="ff69b-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="ff69b-115">Quando o controlador de dispositivo de armazenamento de Linux Olá Deteta um novo dispositivo, atribui tooit de números de dispositivo principal e secundária de intervalo de Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ff69b-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="ff69b-116">Quando um dispositivo for removido, os números de dispositivos de Olá são toobe libertado reutilizado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ff69b-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="ff69b-117">Olá problema ocorre porque hello dispositivo análise no Linux agendada pelo subsistema de SCSI Olá acontece de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="ff69b-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="ff69b-118">Olá dispositivo final caminho nomenclatura pode variar entre reinícios.</span><span class="sxs-lookup"><span data-stu-id="ff69b-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="ff69b-119">Solução</span><span class="sxs-lookup"><span data-stu-id="ff69b-119">Solution</span></span>

<span data-ttu-id="ff69b-120">tooresolve este problema, utilize a atribuição de nomes persistente.</span><span class="sxs-lookup"><span data-stu-id="ff69b-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="ff69b-121">Existem quatro métodos toopersistent nomenclatura - por etiqueta de sistema de ficheiros, uuid, por id e caminho.</span><span class="sxs-lookup"><span data-stu-id="ff69b-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="ff69b-122">Recomendamos que métodos UUID e etiqueta de sistema de ficheiros de Olá para VMs do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff69b-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="ff69b-123">A maioria das distribuições também fornecem a Olá **nofail** ou **nobootwait** fstab opções.</span><span class="sxs-lookup"><span data-stu-id="ff69b-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="ff69b-124">Estas opções ativar um sistema tooboot mesmo disco Olá falha toomount no arranque.</span><span class="sxs-lookup"><span data-stu-id="ff69b-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="ff69b-125">Consulte a documentação da distribuição Olá para obter mais informações sobre estes parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ff69b-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="ff69b-126">Para obter mais informações sobre como tooconfigure toouse uma VM com Linux um UUID quando adicionar um disco de dados, consulte o artigo [ligar toohello disco de nova VM com Linux toomount Olá](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="ff69b-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="ff69b-127">Quando o agente do Linux do Azure de Olá estiver instalado numa VM, utiliza Udev regras tooconstruct um conjunto de ligações simbólicas em **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="ff69b-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="ff69b-128">Estas regras de Udev podem ser utilizadas por aplicações e scripts tooidentify discos anexado toohello VM, o respetivo tipo pelo que Olá LUN.</span><span class="sxs-lookup"><span data-stu-id="ff69b-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="ff69b-129">Mais informações</span><span class="sxs-lookup"><span data-stu-id="ff69b-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="ff69b-130">Identificar os LUNs do disco</span><span class="sxs-lookup"><span data-stu-id="ff69b-130">Identify disk LUNs</span></span>

<span data-ttu-id="ff69b-131">Uma aplicação pode utilizar LUNs toofind todos os discos de Olá ligado e ao construir ligações simbólicas.</span><span class="sxs-lookup"><span data-stu-id="ff69b-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="ff69b-132">agente Linux do Azure de Olá agora inclui regras de udev que configurar as ligações simbólicas de dispositivos de toohello um LUN, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ff69b-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="ff69b-133">Informações de LUN também podem ser obtidas a partir do convidado Linux do Olá utilizando lsscsi ou ferramenta semelhante da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="ff69b-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="ff69b-134">Estas informações de LUN convidado podem ser utilizadas com a subscrição do Azure metadados tooidentify Olá localização no armazenamento do Azure Olá VHD que armazena dados de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="ff69b-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="ff69b-135">Por exemplo, utilize a cli de az Olá:</span><span class="sxs-lookup"><span data-stu-id="ff69b-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="ff69b-136">Detetar UUIDs não de sistema de ficheiros utilizando blkid</span><span class="sxs-lookup"><span data-stu-id="ff69b-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="ff69b-137">Um script ou a aplicação pode ler resultado Olá blkid ou semelhantes fontes de informação e construir as ligações simbólicas no **/dev** para utilização.</span><span class="sxs-lookup"><span data-stu-id="ff69b-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="ff69b-138">saída de Olá mostrará Olá UUIDs não de todos os discos anexados toohello VM e Olá dispositivo ficheiro toowhich estão associados:</span><span class="sxs-lookup"><span data-stu-id="ff69b-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="ff69b-139">regras de udev de waagent Olá construir um conjunto de ligações simbólicas em **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="ff69b-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="ff69b-140">aplicação Olá pode utilizar estas informações identificar o dispositivo de disco de arranque Olá e o disco de recursos (efémeras) Olá.</span><span class="sxs-lookup"><span data-stu-id="ff69b-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="ff69b-141">No Azure, as aplicações devem consultar demasiado**/dev/disk/azure/root-part1** ou **/dev/disk/azure-resource-part1** toodiscover estas partições.</span><span class="sxs-lookup"><span data-stu-id="ff69b-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="ff69b-142">Se existirem partições adicionais na lista de blkid Olá, podem residirem num disco de dados.</span><span class="sxs-lookup"><span data-stu-id="ff69b-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="ff69b-143">As aplicações podem manter Olá UUID para estas partições do e utilizar um caminho como Olá abaixo nome do dispositivo toodiscover Olá durante a execução:</span><span class="sxs-lookup"><span data-stu-id="ff69b-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="ff69b-144">Obter Olá regras de armazenamento do Azure mais recentes</span><span class="sxs-lookup"><span data-stu-id="ff69b-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="ff69b-145">regras de armazenamento do Azure mais recentes toohello, execute ésimo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ff69b-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="ff69b-146">Para obter mais informações, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="ff69b-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="ff69b-147">Ubuntu: Utilizando o UUID</span><span class="sxs-lookup"><span data-stu-id="ff69b-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="ff69b-148">Red Hat: A nomenclatura persistente</span><span class="sxs-lookup"><span data-stu-id="ff69b-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="ff69b-149">Linux: O UUIDs não pode fazer por si</span><span class="sxs-lookup"><span data-stu-id="ff69b-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="ff69b-150">Udev: Introdução tooDevice no moderna Linux sistema de gestão</span><span class="sxs-lookup"><span data-stu-id="ff69b-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

