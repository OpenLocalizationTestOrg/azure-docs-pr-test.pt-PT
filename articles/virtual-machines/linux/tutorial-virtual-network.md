---
title: "aaaAzure redes virtuais e máquinas virtuais do Linux | Microsoft Docs"
description: "Tutorial - Gerir redes virtuais do Azure e máquinas virtuais do Linux com Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Gerir redes virtuais do Azure e máquinas virtuais do Linux com Olá CLI do Azure

Máquinas virtuais do Azure utilizar redes do Azure para a comunicação de rede internos e externos. Este tutorial explica duas máquinas virtuais a implementar e configurar redes do Azure para estas VMs. Exemplos de Olá neste tutorial partem do princípio de que as VMs de Olá estão a alojar uma aplicação web com um back-end da base de dados, no entanto, uma aplicação não está implementada no tutorial Olá. Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Implementar uma rede virtual
> * Criar uma sub-rede dentro de uma rede virtual
> * Ligar máquinas virtuais tooa sub-rede
> * Gerir endereços IP públicos de máquina virtual
> * Proteger o tráfego de internet de entrada
> * Proteger o tráfego de tooVM VM


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Descrição geral de redes VM

Redes virtuais do Azure ativar as ligações de rede seguro entre máquinas virtuais, Olá internet e outros serviços do Azure, tais como a base de dados SQL do Azure. Redes virtuais são divididas em segmentos lógicos denominados sub-redes. Sub-redes são utilizadas toocontrol fluxo de rede e como um limite de segurança. Quando implementar uma VM, incluem-se, geralmente, uma interface de rede virtual, que é anexado tooa sub-rede.

## <a name="deploy-virtual-network"></a>Implementar a rede virtual

Para este tutorial, é criada uma única rede virtual com duas sub-redes. Uma sub-rede do front-end para alojar uma aplicação web e uma sub-rede de back-end para o alojamento de um servidor de base de dados.

Antes de poder criar uma rede virtual, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myRGNetwork* na localização de eastus Olá.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Criar a rede virtual

Nos Olá [az rede vnet criar](/cli/azure/network/vnet#create) comando toocreate uma rede virtual. Neste exemplo, é denominado rede Olá *mvVnet* e é dado um prefixo de endereço de *10.0.0.0/16*. Uma sub-rede também é criada com um nome de *mySubnetFrontEnd* e um prefixo de *10.0.1.0/24*. Mais tarde no tutorial uma VM de front-end é ligado toothis sub-rede. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Criar sub-rede

Uma nova sub-rede é adicionada a rede virtual toohello utilizando Olá [az rede vnet sub-rede](/cli/azure/network/vnet/subnet#create) comando. Neste exemplo, é denominado sub-rede Olá *mySubnetBackEnd* e é dado um prefixo de endereço de *10.0.2.0/24*. Esta sub-rede é utilizada com todos os serviços de back-end.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

Neste momento, uma rede foi criada e segmentada em duas sub-redes, um para serviços front-end e outra para serviços de back-end. Na secção seguinte, Olá, as máquinas virtuais são criadas e ligados a sub-redes toothese.

## <a name="understand-public-ip-address"></a>Compreender o endereço IP público

Um endereço IP público permite toobe de recursos do Azure acessíveis no Olá internet. Esta secção do tutorial Olá, é criada uma VM toodemonstrate como endereços toowork com IP público.

### <a name="allocation-method"></a>Método de alocação

Um endereço IP público que pode ser atribuído como dinâmico ou estático. Por predefinição, o endereço IP público dinamicamente atribuído. Endereços IP dinâmicos são lançados quando uma VM é desalocada. Este comportamento faz com que toochange de endereço IP de Olá durante qualquer operação que inclua uma Desalocação da VM.

método de alocação de Olá pode ser definido toostatic, que garante que o endereço IP Olá permanecem atribuídos tooa VM, mesmo durante um Estado desalocado. Quando utilizar um endereço IP estaticamente atribuído, não não possível especificar endereços IP Olá próprio. Em vez disso, é atribuído partir de um conjunto de endereços disponíveis.

### <a name="dynamic-allocation"></a>Alocação dinâmica

Ao criar uma VM com Olá [az vm criar](/cli/azure/vm#create) comando, Olá público IP endereço alocação método predefinido é dinâmico. No seguinte exemplo de Olá, é criada uma VM com um endereço IP dinâmico. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Alocação estática

Ao criar uma máquina virtual utilizando Olá [az vm criar](/cli/azure/vm#create) comando, incluir Olá `--public-ip-address-allocation static` argumento tooassign um endereço IP público estático. Esta operação não é demonstrada neste tutorial, no entanto na Olá secção seguinte, um endereço IP alocado dinamicamente é alterada tooa estaticamente o endereço alocado. 

### <a name="change-allocation-method"></a>Alterar o método de alocação

método de alocação de endereço IP Olá pode ser alterado utilizando Olá [atualização de ip público de rede az](/cli/azure/network/public-ip#update) comando. Neste exemplo, Olá método de alocação de endereço IP de front-end VM é alterado de Olá toostatic.

Em primeiro lugar, desalocar Olá VM.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Olá utilize [atualização de ip público de rede az](/cli/azure/network/public-ip#update) método de alocação de Olá tooupdate de comandos. Neste caso, Olá `--allocation-method` está a ser definido demasiado*estático*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Inicie Olá VM.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Nenhum endereço IP público

Muitas vezes, uma VM não necessitam de toobe acessível através de Olá internet. toocreate uma VM sem um endereço IP público, utilize Olá `--public-ip-address ""` argumento com um conjunto vazio de aspas duplas. Esta configuração é demonstrada mais à frente neste tutorial

## <a name="secure-network-traffic"></a>Proteja o tráfego de rede

Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede ligado tooAzure redes virtuais (VNet). Os NSGs podem ser associados toosubnets ou as interfaces de rede individuais. Quando um NSG é associado uma interface de rede, aplica-se apenas Olá associado à VM. Quando um NSG é associado tooa sub-rede, Olá aplicam-se regras tooall recursos ligados toohello sub-rede. 

### <a name="network-security-group-rules"></a>Regras do grupo de segurança de rede

Regras do NSG definem portas de rede durante o qual o tráfego é permitido ou negado. regras de Olá podem incluir intervalos de endereços IP de origem e de destino para que o tráfego é controlado entre sistemas específicos ou sub-redes. Regras do NSG também incluem uma prioridade de (entre 1 — e 4096). As regras são avaliadas por ordem de Olá de prioridade. Uma regra com uma prioridade de 100 é avaliada antes de uma regra com prioridade 200.

Todos os NSGs contêm um conjunto de regras predefinidas. regras de predefinidas Olá não podem ser eliminadas, mas como lhes é atribuída a prioridade mais baixa Olá, podem ser substituídas pelas regras de Olá que criar.

- **Rede virtual** - tráfego com origem e de fim numa rede virtual é permitido nas direções de entrada e saídas.
- **Internet** - o tráfego de saída é permitido, mas o tráfego de entrada está bloqueado.
- **O Balanceador de carga** -carga balanceador tooprobe Olá estado de funcionamento permitir do Azure das VMs e instâncias de função. Se não estiver a utilizar um conjunto com balanceamento de carga, pode substituir esta regra.

### <a name="create-network-security-groups"></a>Criar grupos de segurança de rede

Um grupo de segurança de rede pode ser criado em Olá mesmo tempo, como uma VM utilizando Olá [az vm criar](/cli/azure/vm#create) comando. Ao fazê-lo, Olá NSG é associado a interface de rede de VMs de Olá e uma regra de NSG é criada automaticamente tooallow tráfego na porta *22* de uma origem. Anteriormente no tutorial, Olá front-end NSG foi criado automaticamente com Olá VM front-end. Uma regra NSG também foi criada para a porta 22 automaticamente. 

Em alguns casos, poderá ser útil toopre-criar um NSG, por exemplo, quando não devem ser criadas regras SSH predefinidas ou quando Olá NSG deve ser anexado tooa sub-rede. 

Olá utilize [az rede nsg criar](/cli/azure/network/nsg#create) comando toocreate um grupo de segurança de rede.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Em vez de associação de interface de rede do Olá NSG tooa, está associada a uma sub-rede. Nesta configuração, qualquer VM que é anexado toohello sub-rede herda as regras do NSG Olá.

Atualizar a sub-rede existente Olá designada *mySubnetBackEnd* com Olá novo NSG.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Agora criar uma máquina virtual, que é anexado toohello *mySubnetBackEnd*. Tenha em atenção que Olá `--nsg` argument tem um valor de aspas duplas vazios. Um NSG não precisa de toobe criado com Olá VM. Olá VM é sub-rede de back-end toohello anexado, o que é protegida com Olá pré-criadas NSG de back-end. Este NSG aplica-se toohello VM. Além disso, repare que Olá `--public-ip-address` argument tem um valor de aspas duplas vazios. Esta configuração cria uma VM sem um endereço IP público. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Proteger o tráfego de entrada

Quando hello front-end VM foi criada, NSG foi criada uma regra tooallow tráfego de entrada na porta 22. Esta regra permite SSH ligações toohello VM. Neste exemplo, também deve ser permitido tráfego na porta *80*. Esta configuração permite que um toobe de aplicação web acedida num Olá VM.

Olá utilize [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra para a porta *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Olá VM front-end agora só é acessível na porta *22* e a porta *80*. Todos os outro tráfego de entrada é bloqueado no grupo de segurança de rede Olá. Poderá ser útil toovisualize as configurações de regra do Olá NSG. Configuração de regras NSG Olá retorno com Olá [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Saída:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Proteger o tráfego de tooVM VM

Regras do grupo de segurança de rede também podem aplicar entre as VMs. Para este exemplo Olá VM front-end tem toocommunicate com Olá VM de back-end na porta *22* e *3306*. Esta configuração permite ligações SSH de Olá VM front-end e também permitir que uma aplicação no front-end VM toocommunicate Olá com uma base de dados MySQL back-end. Todo o restante tráfego deve ser bloqueado entre Olá front-end e back-end máquinas virtuais.

Olá utilize [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra para a porta 22. Tenha em atenção que Olá `--source-address-prefix` argumento especifica um valor de *10.0.1.0/24*. Esta configuração assegura que apenas o tráfego de sub-rede de front-end Olá é permitido através de Olá NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Agora, adicione uma regra para o tráfego de MySQL na porta 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Por fim, porque os NSGs tem uma regra predefinida, permitindo todo o tráfego entre VMs na Olá mesma VNet, uma regra pode ser criada para Olá back-end NSGs tooblock todo o tráfego. Repare que Olá `--priority` é atribuído um valor de *300*, que é menor do que Olá ambas as regras do NSG e MySQL. Esta configuração assegura que o tráfego SSH e o MySQL ainda é permitido através de Olá NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Olá VM de back-end agora só é acessível na porta *22* e a porta *3306* da sub-rede Olá de front-end. Todos os outro tráfego de entrada é bloqueado no grupo de segurança de rede Olá. Poderá ser útil toovisualize as configurações de regra do Olá NSG. Configuração de regras NSG Olá retorno com Olá [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Saída:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, criou e redes do Azure como toovirtual relacionados máquinas protegidas. Aprendeu a:

> [!div class="checklist"]
> * Implementar uma rede virtual
> * Criar uma sub-rede dentro de uma rede virtual
> * Ligar máquinas virtuais tooa sub-rede
> * Gerir endereços IP públicos de máquina virtual
> * Proteger o tráfego de internet de entrada
> * Proteger o tráfego de tooVM VM

Produzir toohello seguinte toolearn tutorial sobre como proteger dados em máquinas virtuais utilizando cópia de segurança do Azure. 

> [!div class="nextstepaction"]
> [Cópia de segurança de computadores virtuais Linux no Azure](./tutorial-backup-vms.md)
