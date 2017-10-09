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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Resolução de problemas: Os nomes de dispositivos de VM com Linux são alterados

artigo de Olá explica por que motivo os nomes de dispositivos são alterados depois de reiniciar uma máquina virtual (VM) do Linux ou reattach discos Olá. Também fornece solução Olá para este problema.

## <a name="symptom"></a>Sintoma

Pode deparar-se Olá os seguintes problemas quando VMs do Linux em execução no Microsoft Azure.

- Olá VM falha tooboot após um reinício.

- Se os discos de dados estiver desligados e novamente ligados, os nomes de dispositivos de Olá para os discos foram alterados.

- Falha de uma aplicação ou script que faça referência a um disco com o nome do dispositivo. Determinar que Olá nome do dispositivo de disco Olá é alterado.

## <a name="cause"></a>Causa

Caminhos de dispositivo no Linux não são garantidos que toobe consistente entre reinícios. Nomes de dispositivos é composto por principal (letra) e números secundários.  Quando o controlador de dispositivo de armazenamento de Linux Olá Deteta um novo dispositivo, atribui tooit de números de dispositivo principal e secundária de intervalo de Olá disponíveis. Quando um dispositivo for removido, os números de dispositivos de Olá são toobe libertado reutilizado mais tarde.

Olá problema ocorre porque hello dispositivo análise no Linux agendada pelo subsistema de SCSI Olá acontece de forma assíncrona. Olá dispositivo final caminho nomenclatura pode variar entre reinícios. 

## <a name="solution"></a>Solução

tooresolve este problema, utilize a atribuição de nomes persistente. Existem quatro métodos toopersistent nomenclatura - por etiqueta de sistema de ficheiros, uuid, por id e caminho. Recomendamos que métodos UUID e etiqueta de sistema de ficheiros de Olá para VMs do Linux do Azure. 

A maioria das distribuições também fornecem a Olá **nofail** ou **nobootwait** fstab opções. Estas opções ativar um sistema tooboot mesmo disco Olá falha toomount no arranque. Consulte a documentação da distribuição Olá para obter mais informações sobre estes parâmetros. Para obter mais informações sobre como tooconfigure toouse uma VM com Linux um UUID quando adicionar um disco de dados, consulte o artigo [ligar toohello disco de nova VM com Linux toomount Olá](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Quando o agente do Linux do Azure de Olá estiver instalado numa VM, utiliza Udev regras tooconstruct um conjunto de ligações simbólicas em **/dev/disk/azure**. Estas regras de Udev podem ser utilizadas por aplicações e scripts tooidentify discos anexado toohello VM, o respetivo tipo pelo que Olá LUN.

## <a name="more-information"></a>Mais informações

### <a name="identify-disk-luns"></a>Identificar os LUNs do disco

Uma aplicação pode utilizar LUNs toofind todos os discos de Olá ligado e ao construir ligações simbólicas. agente Linux do Azure de Olá agora inclui regras de udev que configurar as ligações simbólicas de dispositivos de toohello um LUN, da seguinte forma:

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
                                 

Informações de LUN também podem ser obtidas a partir do convidado Linux do Olá utilizando lsscsi ou ferramenta semelhante da seguinte forma.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Estas informações de LUN convidado podem ser utilizadas com a subscrição do Azure metadados tooidentify Olá localização no armazenamento do Azure Olá VHD que armazena dados de partição Olá. Por exemplo, utilize a cli de az Olá:

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Detetar UUIDs não de sistema de ficheiros utilizando blkid

Um script ou a aplicação pode ler resultado Olá blkid ou semelhantes fontes de informação e construir as ligações simbólicas no **/dev** para utilização. saída de Olá mostrará Olá UUIDs não de todos os discos anexados toohello VM e Olá dispositivo ficheiro toowhich estão associados:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

regras de udev de waagent Olá construir um conjunto de ligações simbólicas em **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


aplicação Olá pode utilizar estas informações identificar o dispositivo de disco de arranque Olá e o disco de recursos (efémeras) Olá. No Azure, as aplicações devem consultar demasiado**/dev/disk/azure/root-part1** ou **/dev/disk/azure-resource-part1** toodiscover estas partições.

Se existirem partições adicionais na lista de blkid Olá, podem residirem num disco de dados. As aplicações podem manter Olá UUID para estas partições do e utilizar um caminho como Olá abaixo nome do dispositivo toodiscover Olá durante a execução:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Obter Olá regras de armazenamento do Azure mais recentes

regras de armazenamento do Azure mais recentes toohello, execute ésimo os seguintes comandos:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Para obter mais informações, consulte Olá seguintes artigos:

- [Ubuntu: Utilizando o UUID](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: A nomenclatura persistente](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: O UUIDs não pode fazer por si](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Introdução tooDevice no moderna Linux sistema de gestão](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

