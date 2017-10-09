---
title: aaaUse Docker Compose numa VM com Linux no Azure | Microsoft Docs
description: "Como toouse Docker e Compose em máquinas virtuais Linux Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Obter iniciado com o Docker e Compose toodefine e executar uma aplicação de contentor multi no Azure
Com [Compose](http://github.com/docker/compose), que utiliza um toodefine do ficheiro de texto simples, uma aplicação consiste de vários contentores de Docker. Em seguida, de rotação cópias de segurança da aplicação num único comando que tudo toodeploy ambiente definido. Por exemplo, este artigo mostra como tooquickly configurar um blogue do WordPress com um back-end da base de dados MariaDB SQL numa VM com Ubuntu. Também pode utilizar Compose tooset das aplicações mais complexas.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Configurar uma VM com Linux como um anfitrião do Docker
Pode utilizar vários procedimentos do Azure e imagens disponíveis ou modelos do Resource Manager no Azure Marketplace de Olá toocreate uma VM com Linux e configurá-lo como um anfitrião de Docker. Por exemplo, consulte [utilizando Olá extensão da VM Docker toodeploy ambiente](dockerextension.md) tooquickly criar uma VM com Ubuntu com Olá extensão da VM do Azure Docker com um [modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Quando utiliza a extensão da VM de Docker Olá, a VM é automaticamente configurada como um anfitrião do Docker e Compose já está instalado.


### <a name="create-docker-host-with-azure-cli-20"></a>Criar anfitrião Docker com o Azure CLI 2.0
Olá de instalação mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login).

Em primeiro lugar, crie um grupo de recursos para o seu ambiente de Docker com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *westus* localização:

```azurecli
az group create --name myResourceGroup --location westus
```

Em seguida, implementar uma VM com [criar a implementação do grupo az](/cli/azure/group/deployment#create) que inclui a extensão de VM do Azure Docker Olá de [este modelo Azure Resource Manager no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Fornecer os seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword*, e *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Demora alguns minutos para Olá toofinish de implementação. Após a conclusão da implementação de Olá, [mover toonext passo](#verify-that-compose-is-installed) tooSSH tooyour VM. 

Opcionalmente, a linha de comandos do tooinstead controlo retorno toohello e implementação de Olá permitem continuam em segundo plano de Olá, adicione Olá `--no-wait` sinalizador toohello precedente comando. Este processo permite-lhe tooperform outras tarefas no Olá CLI enquanto continua a implementação de Olá alguns minutos. Em seguida, pode ver detalhes sobre o estado de anfitriões de Docker Olá com [mostrar de vm az](/cli/azure/vm#show). Olá exemplo seguinte verifica o estado de Olá da VM com o nome de Olá *myDockerVM* (Olá nome predefinido do modelo de Olá - não altere este nome) no grupo de recursos de Olá designado *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Quando este comando devolve *com êxito*, concluiu a implementação de Olá e pode SSH toohello VM na Olá passo a seguir.


## <a name="verify-that-compose-is-installed"></a>Certifique-se de que o Compose está instalado
Após a conclusão da implementação de Olá, SSH tooyour novo Docker anfitrião com o nome DNS Olá fornecido durante a implementação. Pode utilizar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview detalhes da sua VM, incluindo o nome DNS Olá.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck que compõem está instalado no Olá VM, execute Olá os seguintes comandos:

```bash
docker-compose --version
```

Poderá ver um resultado semelhante demasiado*1.6.2 de compose docker, crie 4d 72027*.

> [!TIP]
> Se utilizou o outro método toocreate um anfitrião do Docker e precisa de tooinstall compor a si, consulte Olá [compor documentação](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Criar um ficheiro de configuração docker-Compose.yml
Em seguida, crie um `docker-compose.yml` ficheiro, que é apenas um ficheiro de configuração de texto, toodefine Olá Docker contentores toorun no Olá VM. ficheiro de Olá Especifica Olá toorun de imagem em cada contentor (ou pode ser uma compilação de um Dockerfile), as variáveis de ambiente necessários e as dependências, portas e ligações de Olá entre contentores. Para obter detalhes sobre a sintaxe de ficheiro yml, consulte [compor a referência de ficheiro](https://docs.docker.com/compose/compose-file/).

Criar Olá *docker-Compose.yml* ficheiro da seguinte forma:

```bash
touch docker-compose.yml
```

Utilize o tooadd do editor de texto favorito alguns ficheiros de toohello de dados. Olá exemplo seguinte utiliza Olá *vi* editor:

```bash
vi docker-compose.yml
```

Colar Olá seguinte o exemplo para o ficheiro de texto. Esta configuração utilize imagens a partir do Olá [DockerHub registo](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Olá open source para blogging e o conteúdo de sistema de gestão) e um back-end ligado MariaDB SQL da base de dados. Introduza os seus próprios *MYSQL_ROOT_PASSWORD* da seguinte forma:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Iniciar contentores Olá com Compose
No Olá mesmo diretório como o *docker-Compose.yml* ficheiro, execute Olá seguinte comando (dependendo do seu ambiente, poderá ser necessário toorun `docker-compose` utilizando `sudo`):

```bash
docker-compose up -d
```

Este comando inicia contentores de Docker Olá especificados no *docker-Compose.yml*. Demorará um minuto ou dois para toocomplete este passo. Consulte toohello semelhante de saída seguinte exemplo:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Ser se toouse Olá **-d** opção no arranque, para que os contentores de Olá executam em segundo plano de Olá continuamente.


tooverify que são contentores Olá, tipo `docker-compose ps`. Deverá ver algo semelhante ao seguinte:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Pode agora ligar tooWordPress diretamente no Olá VM na porta 80. Abra um browser e introduza o nome DNS Olá da sua VM (tais como `http://mypublicdns.westus.cloudapp.azure.com`). Deverá ver agora Olá que wordpress iniciar o ecrã, onde pode concluir a instalação de Olá e começar a utilizar com a aplicação Olá.

![Ecrã de início do WordPress][wordpress_start]

## <a name="next-steps"></a>Passos seguintes
* Aceda toohello [Guia do utilizador de extensão de VM de Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obter mais opções tooconfigure Docker e Compose na sua VM de Docker. Por exemplo, uma opção é tooput Olá Compose yml ficheiro (tooJSON convertida) diretamente na configuração de Olá da Olá extensão da VM de Docker.
* Veja Olá [compor a referência da linha de comandos](http://docs.docker.com/compose/reference/) e [Guia do utilizador](http://docs.docker.com/compose/) para obter mais exemplos de criar e implementar aplicações de várias contentor.
* Está a utilizar um modelo Azure Resource Manager, o próprio ou um contribuíram de Olá [Comunidade](https://azure.microsoft.com/documentation/templates/), toodeploy uma VM do Azure com o Docker e uma aplicação configurar com Compose. Por exemplo, Olá [implementar um blogue do WordPress com Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) modelo utiliza Docker e Compose tooquickly implementar WordPress com um back-end de MySQL numa VM com Ubuntu.
* Tente integrar o Docker Compose com um cluster Docker Swarm. Consulte [utilizando compor com Swarm](https://docs.docker.com/compose/swarm/) para cenários.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
