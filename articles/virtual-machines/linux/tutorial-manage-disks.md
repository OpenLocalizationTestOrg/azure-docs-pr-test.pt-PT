---
title: "aaaManage Azure discos com Olá CLI do Azure | Microsoft Docs"
description: "Tutorial - Gerir discos do Azure com Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Gerir discos do Azure com Olá CLI do Azure

Máquinas virtuais do Azure utilizar sistema de operativo discos toostore Olá VMs, aplicações e dados. Quando cria uma VM é importante toochoose um tamanho de disco e a carga de trabalho de toohello adequado esperado de configuração. Este tutorial abrange a implementação e gestão de discos VM. Pode obter informações sobre:

> [!div class="checklist"]
> * Discos de SO e discos temporários
> * discos de dados
> * Standard e discos Premium
> * Desempenho de disco
> * Anexar e preparar os discos de dados
> * O redimensionamento de discos
> * Instantâneos de disco


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Predefinição discos do Azure

Quando é criada uma máquina virtual do Azure, dois discos são automaticamente anexados toohello máquina. 

**Disco do sistema operativo** - discos de sistema operativo podem ser dimensionados de forma segurança too1 terabyte e anfitriões Olá sistema de operativo VMs. etiqueta do disco de SO de Olá */dev/sda* por predefinição. disco Olá colocação em cache de configuração do disco do SO Olá está otimizado para desempenho do SO. Devido a esta configuração, Olá disco do SO **não devem** alojar aplicações ou dados. Para aplicações e dados, utilize os discos de dados, que estão descritos neste artigo. 

**Disco temporário** -temporários discos utilizam uma unidade de estado sólido que está localizada em Olá mesmo anfitrião do Azure como Olá VM. Discos temporários são altamente performant e podem ser utilizados para operações, tais como o processamento de dados temporária. No entanto, se Olá VM for movido tooa novo anfitrião, todos os dados armazenados num disco temporário são removidos. o tamanho do disco temporário Olá Olá é determinado pelo Olá tamanho da VM. Discos temporários são etiquetados */dev/sdb* e ter uma pontodemontagem de */mnt*.

### <a name="temporary-disk-sizes"></a>Tamanhos de disco temporário

| Tipo | Tamanho da VM | Tamanho máximo de disco temporário (GB) |
|----|----|----|
| [Fins gerais](sizes-general.md) | A e a série de D | 800 |
| [Com otimização de computação](sizes-compute.md) | Série F | 800 |
| [Com otimização de memória](../virtual-machines-windows-sizes-memory.md) | Série de D e G | 6144 |
| [Com otimização de armazenamento](../virtual-machines-windows-sizes-storage.md) | Série de L | 5630 |
| [GPU](sizes-gpu.md) | Série N | 1440 |
| [Elevado desempenho](sizes-hpc.md) | A e a série de H | 2000 |

## <a name="azure-data-disks"></a>Discos de dados do Azure

Discos de dados adicionais podem ser adicionados para instalar aplicações e armazenar dados. Os discos de dados devem ser utilizados em qualquer situação em que o armazenamento de dados durável e reativa for pretendido. Cada disco de dados tem uma capacidade máxima de 1 terabyte. o tamanho da máquina virtual de Olá Olá determina quantos discos de dados podem ser anexado tooa VM. Para cada núcleo VM, podem ser anexados a discos de dados de dois. 

### <a name="max-data-disks-per-vm"></a>Discos de dados de máx. por VM

| Tipo | Tamanho da VM | Discos de dados de máx. por VM |
|----|----|----|
| [Fins gerais](sizes-general.md) | A e a série de D | 32 |
| [Com otimização de computação](sizes-compute.md) | Série F | 32 |
| [Com otimização de memória](../virtual-machines-windows-sizes-memory.md) | Série de D e G | 64 |
| [Com otimização de armazenamento](../virtual-machines-windows-sizes-storage.md) | Série de L | 64 |
| [GPU](sizes-gpu.md) | Série N | 48 |
| [Elevado desempenho](sizes-hpc.md) | A e a série de H | 32 |

## <a name="vm-disk-types"></a>Tipos de disco da VM

O Azure oferece dois tipos de disco.

### <a name="standard-disk"></a>Disco Standard

O Armazenamento Standard está protegido por HDDs e fornece armazenamento económico, mantendo o desempenho. Discos padrão são ideais para um dev económica e teste de carga de trabalho.

### <a name="premium-disk"></a>Disco Premium

Os discos Premium são apoiados por disco de elevado desempenho, baixa latência baseadas em SSD. Perfeita para as VMs com a carga de trabalho de produção. Armazenamento Premium suporta-série DS, série DSv2-série, série GS e série FS VMs. Os discos Premium são fornecidos em três tipos (P10, P20, P30), o tamanho do disco de Olá Olá determina o tipo de disco Olá. Quando selecionar, um valor de Olá de tamanho de disco é arredondado toohello tipo do próximo. Por exemplo, se o tamanho do disco de Olá for inferior a 128 GB, o tipo de disco Olá é P10. Se o tamanho do disco Olá entre 129 GB e 512 GB, o tamanho de Olá é um P20. Nada mais 512 GB, o tamanho de Olá é um P30.

### <a name="premium-disk-performance"></a>Desempenho do disco Premium

|Tipo de disco de armazenamento Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Tamanho do disco (arredondar) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOPs Máx por disco | 500 | 2,300 | 5,000 |
Débito por disco | 100 MB/s | 150 MB/s | 200 MB/s |

Enquanto Olá acima tabela identifica os IOPS máximo por disco, um nível mais elevado de desempenho pode ser alcançado ao striping vários discos de dados. Por exemplo, uma VM Standard_GS5 pode alcançar um máximo de 80.000 IOPS. Para obter informações detalhadas sobre o IOPS máximo por VM, consulte [tamanhos de VM com Linux](sizes.md).

## <a name="create-and-attach-disks"></a>Criar e anexar discos

Os discos de dados podem ser criados e ligados ao tempo de criação de VM ou tooan existente VM.

### <a name="attach-disk-at-vm-creation"></a>Anexar o disco durante a criação de VM

Criar um grupo de recursos com Olá [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Criar uma VM utilizando Olá [az vm criar]( /cli/azure/vm#create) comando. Olá `--datadisk-sizes-gb` argumento é utilizado toospecify que um disco adicional deve ser criado e ligados a máquina virtual de toohello. toocreate e anexar mais de um disco, utilize uma lista delimitada por espaços de valores de tamanho de disco. No seguinte exemplo de Olá, é criada uma VM com discos de dados de dois, ambos os 128 GB. Porque os tamanhos de disco Olá 128 GB, estes discos são configurados como P10s, que fornecem IOPS máximo de 500 por disco.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Anexar o disco tooexisting VM

toocreate e anexar uma novo disco tooan máquina virtual existente, utilize Olá [anexar o disco da vm az](/cli/azure/vm/disk#attach) comando. Olá exemplo seguinte cria um disco premium, 128 gigabytes de tamanho e anexa-toohello que VM criada no último passo de Olá.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Preparar os discos de dados

Depois de um disco foi anexado toohello máquina, sistema de operativo Olá tem toobe configurado toouse Olá disco. Olá seguinte exemplo mostra como toomanually configurar um disco. Este processo também pode ser automatizado utilizando nuvem-init, que é abordada um [tutorial posterior](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuração manual

Crie uma ligação SSH com a máquina virtual de Olá. Substitua os endereços IP do exemplo Olá Olá IP público de máquina virtual de Olá.

```azurecli-interactive 
ssh 52.174.34.95
```

Criar partições do disco Olá com `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Escrever uma partição de toohello do sistema de ficheiros utilizando Olá `mkfs` comando.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Monte o disco novo Olá para que seja acessível no sistema de operativo Olá.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

disco Olá agora pode ser acedido através de Olá *datadrive* pontodemontagem, que pode ser verificada executando Olá `df -h` comando. 

```bash
df -h
```

saída de Olá mostra unidade novo Olá montada em */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure Olá unidade é remontadas da após um reinício, tem de ser adicionado toohello *etc/fstab* ficheiro. toodo por isso, obter Olá UUID de disco Olá com Olá `blkid` utilitário.

```bash
sudo -i blkid
```

saída de Olá apresenta Olá UUID da unidade de Olá, `/dev/sdc1` neste caso.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Adicionar uma linha de toohello semelhante seguir toohello *etc/fstab* ficheiro. Também em atenção que escrever barreiras as eficazes pode ser desativada através de *barreira = 0*, esta configuração pode melhorar o desempenho de disco. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Agora que hello disco tiver sido configurado, feche a sessão SSH Olá.

```bash
exit
```

## <a name="resize-vm-disk"></a>Redimensionar disco da VM

Assim que tiver sido implementada uma VM, disco de sistema operativo Olá ou qualquer discos de dados anexados podem ser aumentados de tamanho. Aumentar o tamanho de Olá de um disco é vantajoso quando necessitar de mais espaço de armazenamento ou de um nível mais elevado de desempenho (P10 P20, P30). Tenha em atenção de que não podem ser diminuídos discos de tamanho.

Antes de aumentar o tamanho do disco, Olá Id ou nome do disco de Olá é necessária. Olá utilize [lista de discos az](/cli/azure/vm/disk#list) comando tooreturn todos os discos num grupo de recursos. Tome nota do nome do disco Olá que gostaria de tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Olá VM também tem de ser desalocada. Olá utilize [az vm desalocar]( /cli/azure/vm#deallocate) toostop de comandos e desalocar Olá VM.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Olá utilize [atualização de disco az](/cli/azure/vm/disk#update) disco do comando tooresize Olá. Neste exemplo redimensiona um disco chamado *myDataDisk* too1 terabyte.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Depois de concluída a operação de redimensionamento Olá, inicie Olá VM.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Se tiver redimensionado Olá disco do sistema de operativo, partição Olá é automaticamente expandido. Se tiver redimensionado um disco de dados, quaisquer partições atuais tem toobe expandido no sistema de operativo Olá VMs.

## <a name="snapshot-azure-disks"></a>Instantâneos de discos do Azure

Criar um instantâneo de disco cria uma leitura cópia apenas, o ponto no tempo de disco Olá. Instantâneos VM do Azure são úteis para guardar rapidamente o estado de Olá de uma VM antes de efetuar alterações de configuração. O evento Olá hello alterações de configuração de provar toobe indesejado, estado de VM pode ser restaurado utilizando instantâneos de Olá. Quando uma VM tem mais de um disco, é obtido um instantâneo de cada disco independentemente Olá outras pessoas. Para fazer cópias de segurança da aplicação, considere parar Olá VM antes de tirar instantâneos de disco. Em alternativa, utilize Olá [serviço de cópia de segurança do Azure](/azure/backup/), que permite tooperform automatizada cópias de segurança ao hello VM está em execução.

### <a name="create-snapshot"></a>Criar instantâneo

Antes de criar um instantâneo de disco da máquina virtual, hello Id ou nome do disco de Olá é necessária. Olá utilize [mostrar de vm az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id de disco do comando tooreturn Olá. Neste exemplo, um id de disco Olá é armazenado numa variável, para que possa ser utilizado num passo posterior.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Agora que tem o id de Olá do disco da máquina virtual Olá, hello comando seguinte cria um instantâneo do disco de Olá.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Criar disco de instantâneo

Este instantâneo, em seguida, pode ser convertido para um disco, o que pode ser utilizado toorecreate Olá máquina.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Restauro do instantâneo de máquina virtual

recuperação da máquina virtual toodemonstrate, eliminar Olá existente a máquina virtual. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Crie uma nova máquina virtual a partir de discos de instantâneo Olá.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Reattach disco de dados

Todos os discos de dados tem de máquina de virtual toohello toobe novamente ligado.

Localizar primeiro o nome de disco de dados de Olá utilizando Olá [lista de discos az](https://docs.microsoft.com/cli/azure/disk#list) comando. Neste exemplo locais Olá nome do disco de Olá numa variável designada *datadisk*, que é utilizada no passo seguinte Olá.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Olá utilize [anexar o disco da vm az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco do comando tooattach Olá.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, aprendeu sobre os tópicos de discos VM, tais como:

> [!div class="checklist"]
> * Discos de SO e discos temporários
> * discos de dados
> * Standard e discos Premium
> * Desempenho de disco
> * Anexar e preparar os discos de dados
> * O redimensionamento de discos
> * Instantâneos de disco

Produzir toohello seguinte toolearn tutorial sobre automatizar a configuração de VM.

> [!div class="nextstepaction"]
> [Automatizar a configuração da VM](./tutorial-automate-vm-deployment.md)
