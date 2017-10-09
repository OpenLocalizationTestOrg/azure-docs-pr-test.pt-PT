---
title: "aaaCreate conjuntos de dimensionamento de Máquina Virtual para Linux no Azure | Microsoft Docs"
description: "Criar e implementar uma aplicação altamente disponível em VMs do Linux utilizando um conjunto de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Criar um conjunto de dimensionamento de Máquina Virtual e implementar uma aplicação altamente disponível no Linux
Um conjunto de dimensionamento de máquina virtual permite-lhe toodeploy e gerir um conjunto de máquinas virtuais idênticas de dimensionamento automático. Pode dimensionar o número de Olá de VMs no conjunto de dimensionamento de Olá manualmente ou definir tooautoscale regras com base na utilização de CPU, a pedido de memória ou tráfego de rede. Neste tutorial, implementa um conjunto no Azure de dimensionamento de máquina virtual. Saiba como:

> [!div class="checklist"]
> * Utilizar a cloud init toocreate tooscale uma aplicação
> * Criar um conjunto de dimensionamento de máquina virtual
> * Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento
> * Ver informações de ligação para as instâncias do conjunto de dimensionamento
> * Utilizar discos de dados num conjunto de dimensionamento


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Descrição geral do conjunto de dimensionamento
Um conjunto de dimensionamento de máquina virtual permite-lhe toodeploy e gerir um conjunto de máquinas virtuais idênticas de dimensionamento automático. Conjuntos de dimensionamento Olá utilize componentes mesmos como aprendeu sobre tutorial anterior Olá demasiado[criar VMs de elevada](tutorial-availability-sets.md). As VMs num conjunto de dimensionamento são criadas num conjunto e distribuídos por domínios de falhas e de atualização de lógica de disponibilidade.

As VMs são criadas conforme necessário de um conjunto de dimensionamento. Definir dimensionamento automático regras toocontrol como e quando VMs são adicionadas ou removidas do conjunto de dimensionamento de Olá. Estas regras podem acionar com base nas métricas, tais como a carga de CPU, utilização de memória ou tráfego de rede.

Os conjuntos de dimensionamento suporte cópias de segurança too1, 000 VMs ao utilizar uma imagem de plataforma do Azure. Para cargas de trabalho de produção, pode ser útil demasiado[criar uma imagem VM personalizada](tutorial-custom-images.md). Pode criar cópias de segurança too100 VMs na escala definido quando utilizar uma imagem personalizada.


## <a name="create-an-app-tooscale"></a>Criar uma aplicação tooscale
Para utilização em produção, pode ser útil demasiado[criar uma imagem VM personalizada](tutorial-custom-images.md) que inclui a aplicação instalada e configurada. Para este tutorial, permite personalizar Olá que VMS no primeiro arranque tooquickly ver um conjunto em ação de dimensionamento.

Um tutorial anterior, aprendeu [como toocustomize uma máquina virtual do Linux no primeiro arranque](tutorial-automate-vm-deployment.md) com init de nuvem. Pode utilizar Olá tooinstall de ficheiro mesma configuração de nuvem init NGINX e executar uma aplicação Node.js "Olá, mundo" simples. 

Na sua shell atual, crie um ficheiro denominado *nuvem init.txt* e colar Olá seguindo a configuração. Por exemplo, crie o ficheiro de Olá no Olá Shell na nuvem não no seu computador local. Introduza `sensible-editor cloud-init.txt` toocreate Olá ficheiro e ver uma lista de editores disponíveis. Certifique-se de que o ficheiro init de nuvem todo Olá foi corretamente copiado, Olá especialmente a primeira linha:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a>Criar um conjunto de dimensionamento
Antes de poder criar um conjunto de dimensionamento, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupScaleSet* no Olá *eastus* localização:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Agora criar um conjunto com de dimensionamento de máquina virtual [az vmss criar](/cli/azure/vmss#create). Olá exemplo seguinte cria um conjunto nomeado de dimensionamento *myScaleSet*, utiliza Olá do Olá nuvem init ficheiro toocustomize VM e gera chaves SSH, caso não existam:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Este demora alguns minutos toocreate e configurar todos os recursos de conjunto de dimensionamento de Olá e VMs. Existem tarefas em segundo plano que continue toorun após Olá CLI do Azure devolve toohello linha. Pode ser outro alguns minutos antes de poder aceder Olá aplicação.


## <a name="allow-web-traffic"></a>Permitir o tráfego da web
Foi criado automaticamente como parte do conjunto de dimensionamento de máquina virtual de Olá a um balanceador de carga. Balanceador de carga Olá distribui o tráfego por um conjunto de VMs definidos através de regras de Balanceador de carga. Pode saber mais sobre conceitos de Balanceador de carga e a configuração no próximo tutorial Olá, [como tooload equilibrar as máquinas virtuais no Azure](tutorial-load-balancer.md).

tooallow tráfego tooreach Olá web app, crie uma regra com [criar regra de lb az rede](/cli/azure/network/lb/rule#create). Olá exemplo seguinte cria uma regra com o nome *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Testar a aplicação
toosee à aplicação Node.js na web Olá, obter o endereço IP público de Olá do seu Balanceador de carga com [mostrar de ip público de rede az](/cli/azure/network/public-ip#show). Olá exemplo seguinte obtém o endereço IP Olá *myScaleSetLBPublicIP* criada como parte do conjunto de dimensionamento de Olá:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Introduza o endereço IP público Olá no tooa browser. aplicação de Olá é apresentada, incluindo o nome de anfitrião de Olá do Olá VM que Olá de carga do tráfego do Balanceador distribuída para:

![Aplicação Node.js em execução](./media/tutorial-create-vmss/running-nodejs-app.png)

toosee Olá conjunto de dimensionamento em ação, pode forçar atualização a carga do web browser toosee Olá balanceador distribuir o tráfego entre todas as VMs de Olá executar a sua aplicação.


## <a name="management-tasks"></a>Tarefas de gestão
Ao longo do ciclo de vida de Olá de conjunto de dimensionamento de Olá, poderá ser necessário toorun uma ou mais tarefas de gestão. Além disso, poderá ser útil toocreate scripts que automatizem várias tarefas de ciclo de vida. Olá 2.0 de CLI do Azure fornece uma forma rápida toodo essas tarefas. Seguem-se algumas tarefas comuns.

### <a name="view-vms-in-a-scale-set"></a>Vista VMs num conjunto de dimensionamento
definir uma lista de VMs em execução no seu dimensionamento de tooview, utilize [az vmss-instâncias da lista](/cli/azure/vmss#list-instances) da seguinte forma:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Olá de saída é semelhante toohello seguinte exemplo:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Aumentar ou diminuir instâncias de VM
toosee Olá diversas instâncias atualmente tem num conjunto de dimensionamento, utilize [mostrar de vmss az](/cli/azure/vmss#show) e consultar no *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Pode, em seguida, manualmente aumentar ou diminuir o número de Olá das máquinas virtuais em conjunto com de dimensionamento de Olá [escala de vmss az](/cli/azure/vmss#scale). Olá exemplo a seguir define Olá número de VMs no seu dimensionamento definido demasiado*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Regras de dimensionamento automático permitem-lhe definir como tooscale ou reduzir verticalmente o número de Olá de VMs no seu dimensionamento definido na resposta toodemand como tráfego de rede ou a utilização da CPU. Atualmente, estas regras não podem ser definidas no Azure CLI 2.0. Olá utilize [portal do Azure](https://portal.azure.com) dimensionamento automático de tooconfigure.

### <a name="get-connection-info"></a>Obter as informações de ligação
as informações da ligação tooobtain sobre Olá VMs no seu conjuntos de dimensionamento, utilize [az vmss lista-instância--informações de ligação](/cli/azure/vmss#list-instance-connection-info). Este comando devolve o endereço IP público Olá e a porta para cada VM que permite-lhe tooconnect com SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Utilizar discos de dados com conjuntos de dimensionamento
Pode criar e utilizar discos de dados com conjuntos de dimensionamento. Um tutorial anterior, aprendeu como demasiado[discos Azure gerir](tutorial-manage-disks.md) que destaca Olá melhores práticas e melhorias de desempenho para a criação de aplicações em discos de dados em vez de disco Olá SO.

### <a name="create-scale-set-with-data-disks"></a>Criar conjunto de dimensionamento com discos de dados
toocreate uma escala definido e anexe discos de dados, adicionar Olá `--data-disk-sizes-gb` parâmetro toohello [az vmss criar](/cli/azure/vmss#create) comando. Olá exemplo seguinte cria um conjunto com de dimensionamento *50*discos de dados de Gb ligados tooeach instância:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Quando instâncias são removidas de um conjunto de dimensionamento, também são removidos quaisquer discos de dados anexados.

### <a name="add-data-disks"></a>Adicionar discos de dados
definir um tooinstances de disco de dados no seu dimensionamento de tooadd, utilize [anexar o disco de vmss az](/cli/azure/vmss/disk#attach). Olá exemplo seguinte adiciona um *50*instância de tooeach do disco Gb:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Desanexar os discos de dados
definir um tooinstances de disco de dados no seu dimensionamento de tooremove, utilize [desanexar o disco de vmss az](/cli/azure/vmss/disk#detach). Olá exemplo a seguir remove o disco de dados de Olá em LUN *2* de cada instância:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Passos seguintes
Neste tutorial, vai criar um conjunto de dimensionamento de máquina virtual. Aprendeu a:

> [!div class="checklist"]
> * Utilizar a cloud init toocreate tooscale uma aplicação
> * Criar um conjunto de dimensionamento de máquina virtual
> * Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento
> * Ver informações de ligação para as instâncias do conjunto de dimensionamento
> * Utilizar discos de dados num conjunto de dimensionamento

Produzir toolearn tutorial seguinte de toohello mais informações sobre conceitos para máquinas virtuais de balanceamento de carga.

> [!div class="nextstepaction"]
> [Máquinas virtuais de balanceamento de carga](tutorial-load-balancer.md)