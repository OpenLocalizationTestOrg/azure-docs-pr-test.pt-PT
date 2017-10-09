---
title: aaaConvert um Azure tooa do conjunto de dimensionamento | Microsoft Docs
description: "Criar e implementar um dimensionamento da máquina virtual do Azure do Linux com Olá CLI do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Converter um conjunto de dimensionamento de tooa de máquina virtual do Azure existente

Este tutorial mostra como toouse Azure CLI 2.0 tooconvert definir um dimensionamento de máquina virtual de tooa da máquina virtual. Também Saiba como definir a configuração de Olá tooautomate das máquinas de virtuais Olá na escala de Olá. Para mais informações sobre como tooinstall CLI do Azure 2.0, consulte o artigo [introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Para mais informações sobre conjuntos de dimensionamento, consulte [conjuntos de dimensionamento de Máquina Virtual](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Passo 1 – desaprovisionar Olá VM

Utilize o SSH tooconnect toohello VM.

Olá deprovision VM Olá VM do Azure agente toodelete ficheiros e dados a utilizar. Para obter uma descrição detalhada do desaprovisionamento, consulte [capturar uma máquina virtual Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Passo 2 - capturar uma imagem de Olá VM

Para obter uma descrição detalhada de captura, consulte [capturar uma máquina virtual Linux](capture-image.md).

Desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalizar Olá VM com [az vm Generalizar](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Criar uma imagem do recurso de VM Olá com [criar imagem az](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Passo 3 – criar conjunto de dimensionamento de Olá

Obter Olá **id** da imagem de Olá.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Criar uma VM a partir do seu recurso de imagem com [az vmss criar](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Este comando também ligado um disco de dados de 10gb. Tenha em atenção que, consoante Olá VM tamanho escolhida (utilizámos **Standard_DS1_v2**), número de Olá de discos de dados permitidas é diferente. Para obter mais informações, consulte Olá [tamanhos de máquina virtual](sizes.md).

Depois de o conjunto de dimensionamento de Olá depois de concluída, ligar tooit. Obter uma lista de endereços IP para instâncias de Olá para SSH com [az vmss lista-instância--informações de ligação](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Agora pode ligar o disco de dados de Olá instância tooinitialize toohello máquina virtual

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Passo 4 - disco de dados de Olá inicializar

Enquanto a máquina virtual de toohello ligado, particionar o disco de Olá com `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Escrever uma partição de toohello do sistema de ficheiros com Olá `mkfs` comando:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Monte o disco novo Olá para que seja acessível no sistema de operativo Olá:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

disco Olá pode agora ser acede através de Olá datadrive pontodemontagem, que pode ser verificado com `ls /datadrive/`.

Termine a sessão SSH Olá.


## <a name="step-5---configure-firewall"></a>Passo 5 - configurar a firewall

Punch um negro através de Olá firewall toohello webserver alojada pelo conjunto de dimensionamento de Olá. Quando foi criado o conjunto de dimensionamento de Olá, também foi criado a um balanceador de carga e utilizou- **SSH** toohello máquinas de virtuais individuais. tooopen uma porta, terá de dois tipos de informações, que pode obter utilizando a CLI do Azure.

* **Conjunto de endereços IP de front-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Conjunto de endereços de IP back-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Com os dois nomes, pode abrir a porta **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Passo 6 - automatizar a configuração

o disco de dados de Olá tem toobe configurada em cada instância de máquina virtual. Iremos pode automatizar a configuração de Olá da máquina virtual de Olá com Olá **CustomScript** extensão.

Em primeiro lugar, crie um *.sh* script que inclui os comandos de formato de disco Olá.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Em seguida, carregue esse Olá de toowhere do ficheiro de script **CustomScript** extensão consegue aceder-lhe. Uma cópia está disponível [aqui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Criar um ficheiro local com o nome **settings.json** e coloque hello os seguintes blocos JSON no mesmo. Olá `flieUris` propriedade deve ser definida toowhere foi carregado o ficheiro de script para.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Implementar o dimensionamento de tooyour este comando com Olá **CustomScript** extensão, referenciar Olá **settings.json** ficheiro acabamos de criar.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Esta extensão é executado automaticamente em todas as instâncias atuais e quaisquer instâncias mais tarde criadas pelo dimensionamento.

## <a name="step-7---configure-autoscale-rules"></a>Passo 7 – configurar regras de dimensionamento automático

Atualmente, as regras de dimensionamento automático não podem ser definidas na CLI do Azure. Olá utilize [portal do Azure](https://portal.azure.com) dimensionamento automático de tooconfigure.

## <a name="step-8---management-tasks"></a>Passo 8 - as tarefas de gestão

Ao longo do ciclo de vida de Olá de conjunto de dimensionamento de Olá, poderá ser necessário toorun uma ou mais tarefas de gestão. Além disso, poderá ser útil toocreate scripts que automatizem várias tarefas de ciclo de vida e Olá CLI do Azure fornece uma forma rápida toodo essas tarefas. Seguem-se algumas tarefas comuns.

### <a name="get-connection-info"></a>Obter as informações de ligação

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Contagem de instâncias do conjunto (dimensionamento manual)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Eliminar grupo de recursos

Também eliminar um grupo de recursos elimina todos os recursos contidos.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre algumas das dimensionamento da máquina virtual Olá definir funcionalidades introduzidas neste tutorial, consulte Olá seguintes informações:

- [Descrição geral de conjuntos de dimensionamento de Máquina Virtual do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Descrição Geral do Balanceador de Carga do Azure (Azure Load Balancer overview)](../../load-balancer/load-balancer-overview.md)
- [Controlar o fluxo de tráfego de rede com grupos de segurança de rede](../../virtual-network/virtual-networks-nsg.md)