---
title: "Olá aaaInstall CLI do Azure 1.0 | Microsoft Docs"
description: "Instalar Olá 1.0 de CLI do Azure para Mac, Linux e Windows toostart utilizando os serviços do Azure"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Instalar Olá CLI do Azure 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [CLI do Azure 1.0](cli-install-nodejs.md)
> * [CLI 2.0 do Azure](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Este tópico descreve como tooinstall Olá Azure CLI 1.0, que está incorporada no nodeJs e suporta a API de implementação clássica todas as chamadas, bem como um grande número de atividades de implementação do Resource Manager. Deve utilizar Olá [Azure CLI 2.0](/cli/azure/overview) para implementações de CLI novo ou forward-looking e gestão.

Instale rapidamente toouse de Interface de linha de comandos do Azure (CLI do Azure 1.0) Olá um conjunto de open source baseada na shell de comandos para criar e gerir recursos no Microsoft Azure. Tem várias opções tooinstall estas ferramentas de plataforma no seu computador:

* **pacote npm** - execução (Gestor de pacotes Olá para JavaScript) tooinstall Olá mais recente do Azure CLI 1.0 pacote npm no seu SO ou a distribuição de Linux. Requer node.js e npm no seu computador.
* **Instalador** -transferir um instalador para a instalação fácil no Mac ou o Windows.
* **Contentor de docker** - começar a utilizar Olá CLI mais recente num contentor de Docker prontos para execução. Requer que os anfitriões de Docker no seu computador.

Para mais opções e em segundo plano, consulte o repositório de projeto Olá no [GitHub](https://github.com/azure/azure-xplat-cli).

Assim que estiver instalado Olá CLI do Azure 1.0, [ligá-lo com a sua subscrição do Azure](xplat-cli-connect.md) e execução Olá **azure** comandos a partir da sua interface de linha de comandos (Bash, Terminal, linha de comandos e assim sucessivamente) toowork com os recursos do Azure.

## <a name="option-1-install-an-npm-package"></a>Opção 1: Instalar um pacote npm
tooinstall Olá CLI de um pacote npm, certifique-se de que transferiu e instalou Olá [mais recente Node.js e npm](https://nodejs.org/en/download/package-manager/). Em seguida, executar **npm instalar** pacote do tooinstall Olá cli do azure:

```bash
npm install -g azure-cli
```

Sobre as distribuições do Linux, poderá ser necessário toouse **sudo** toosuccessfully executar Olá **npm** comando da seguinte forma:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Se precisar de tooinstall ou atualizar Node.js e npm no seu SO ou a distribuição de Linux, recomendamos que instale a versão de Node.js LTS mais recente Olá (4. x). Se utilizar uma versão mais antiga, poderá obter erros de instalação.

Se preferir, transferir Olá Linux mais recente [ficheiros tar] [ linux-installer] para Olá npm pacote localmente. Em seguida, instalar o pacote de npm transferido de Olá da seguinte forma (sobre as distribuições do Linux, poderá ter toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Opção 2: Utilizar um instalador
Se utilizar um computador Mac ou Windows, Olá seguintes programas de instalação do CLI está disponível para transferência:

* [Instalador do Mac OS X][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> No Windows, também pode transferir Olá [instalador de plataforma Web](https://go.microsoft.com/?linkid=9828653) tooinstall Olá CLI. Oferece este instalador Olá opção tooinstall adicionais do Azure SDK e as ferramentas de linha de comandos após a instalação Olá CLI.

## <a name="option-3-use-a-docker-container"></a>Opção 3: Utilizar um contentor de Docker
Se tiver configurado o computador como um [Docker](https://docs.docker.com/engine/understanding-docker/) anfitrião, pode executar hello mais recente do Azure CLI 1.0 num contentor de Docker. Execute hello os seguintes comandos (sobre as distribuições do Linux, poderá ter toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Executar comandos da CLI do Azure 1.0
Depois de Olá CLI do Azure 1.0 está instalado, execute Olá **azure** comando da sua interface de utilizador da linha de comandos (Bash, Terminal, linha de comandos e assim sucessivamente). Por exemplo, o comando de ajuda do toorun Olá, escreva o seguinte Olá:

```azurecli
azure help
```

> [!NOTE]
> Em algumas distribuições de Linux, poderá receber um erro semelhante demasiado`/usr/bin/env: ‘node’: No such file or directory`. Este erro provém de instalações recentes do Node.js a ser instalado em /usr/bin/nodejs. toofix, criar um ligação simbólica demasiado/usr/bin/nó ao executar o comando:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

versão de Olá toosee de Olá Azure CLI 1.0 instalado, Olá tipo seguintes:

```azurecli
azure --version
```

Agora, está pronto! todos os tooaccess Olá toowork de comandos da CLI com os seus próprios recursos, [ligar tooyour subscrição do Azure a partir de Olá CLI do Azure](xplat-cli-connect.md).

> [!NOTE]
> Quando utilizar a CLI do Azure pela primeira vez, é apresentada uma mensagem a perguntar se pretende tooallow as informações de utilização do Microsoft toocollect. A participação é voluntária. Se escolher tooparticipate, pode parar em qualquer altura executando `azure telemetry --disable`. tooenable participação em qualquer altura, execute `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Atualizar Olá CLI
Microsoft frequentemente versões versões atualizadas dos Olá CLI do Azure. Reinstalar Olá CLI utilizando o instalador Olá do seu sistema operativo ou executar o contentor de Docker Olá mais recente. Ou, se tiver hello mais recente Node.js e npm instalado, atualizar, escrevendo Olá seguinte (nas distribuições do Linux, poderá ter toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Ativar a conclusão de separador
Conclusão de separador de comandos da CLI é suportada para Mac e Linux.

tooenable-lo na zsh, execute:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable-lo na bash, execute:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Passos seguintes
* [Ligar a partir de Olá CLI tooyour subscrição do Azure](xplat-cli-connect.md) toocreate e gerir recursos do Azure.
* toolearn mais informações sobre Olá CLI do Azure, transferir o código de origem, problemas, ou contribuir toohello projeto, visite Olá [repositório do GitHub para Olá CLI do Azure](https://github.com/azure/azure-xplat-cli).
* Se tiver dúvidas sobre como utilizar Olá CLI do Azure ou do Azure, visite Olá [fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
