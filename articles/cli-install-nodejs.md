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
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="6571a-103">Instalar Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6571a-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6571a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6571a-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="6571a-105">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6571a-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="6571a-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6571a-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="6571a-107">Este tópico descreve como tooinstall Olá Azure CLI 1.0, que está incorporada no nodeJs e suporta a API de implementação clássica todas as chamadas, bem como um grande número de atividades de implementação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6571a-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="6571a-108">Deve utilizar Olá [Azure CLI 2.0](/cli/azure/overview) para implementações de CLI novo ou forward-looking e gestão.</span><span class="sxs-lookup"><span data-stu-id="6571a-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="6571a-109">Instale rapidamente toouse de Interface de linha de comandos do Azure (CLI do Azure 1.0) Olá um conjunto de open source baseada na shell de comandos para criar e gerir recursos no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6571a-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="6571a-110">Tem várias opções tooinstall estas ferramentas de plataforma no seu computador:</span><span class="sxs-lookup"><span data-stu-id="6571a-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="6571a-111">**pacote npm** - execução (Gestor de pacotes Olá para JavaScript) tooinstall Olá mais recente do Azure CLI 1.0 pacote npm no seu SO ou a distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="6571a-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="6571a-112">Requer node.js e npm no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6571a-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="6571a-113">**Instalador** -transferir um instalador para a instalação fácil no Mac ou o Windows.</span><span class="sxs-lookup"><span data-stu-id="6571a-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="6571a-114">**Contentor de docker** - começar a utilizar Olá CLI mais recente num contentor de Docker prontos para execução.</span><span class="sxs-lookup"><span data-stu-id="6571a-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="6571a-115">Requer que os anfitriões de Docker no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6571a-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="6571a-116">Para mais opções e em segundo plano, consulte o repositório de projeto Olá no [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="6571a-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="6571a-117">Assim que estiver instalado Olá CLI do Azure 1.0, [ligá-lo com a sua subscrição do Azure](xplat-cli-connect.md) e execução Olá **azure** comandos a partir da sua interface de linha de comandos (Bash, Terminal, linha de comandos e assim sucessivamente) toowork com os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6571a-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="6571a-118">Opção 1: Instalar um pacote npm</span><span class="sxs-lookup"><span data-stu-id="6571a-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="6571a-119">tooinstall Olá CLI de um pacote npm, certifique-se de que transferiu e instalou Olá [mais recente Node.js e npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="6571a-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="6571a-120">Em seguida, executar **npm instalar** pacote do tooinstall Olá cli do azure:</span><span class="sxs-lookup"><span data-stu-id="6571a-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="6571a-121">Sobre as distribuições do Linux, poderá ser necessário toouse **sudo** toosuccessfully executar Olá **npm** comando da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6571a-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="6571a-122">Se precisar de tooinstall ou atualizar Node.js e npm no seu SO ou a distribuição de Linux, recomendamos que instale a versão de Node.js LTS mais recente Olá (4. x).</span><span class="sxs-lookup"><span data-stu-id="6571a-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="6571a-123">Se utilizar uma versão mais antiga, poderá obter erros de instalação.</span><span class="sxs-lookup"><span data-stu-id="6571a-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="6571a-124">Se preferir, transferir Olá Linux mais recente [ficheiros tar] [ linux-installer] para Olá npm pacote localmente.</span><span class="sxs-lookup"><span data-stu-id="6571a-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="6571a-125">Em seguida, instalar o pacote de npm transferido de Olá da seguinte forma (sobre as distribuições do Linux, poderá ter toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="6571a-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="6571a-126">Opção 2: Utilizar um instalador</span><span class="sxs-lookup"><span data-stu-id="6571a-126">Option 2: Use an installer</span></span>
<span data-ttu-id="6571a-127">Se utilizar um computador Mac ou Windows, Olá seguintes programas de instalação do CLI está disponível para transferência:</span><span class="sxs-lookup"><span data-stu-id="6571a-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="6571a-128">[Instalador do Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="6571a-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="6571a-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="6571a-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="6571a-130">No Windows, também pode transferir Olá [instalador de plataforma Web](https://go.microsoft.com/?linkid=9828653) tooinstall Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="6571a-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="6571a-131">Oferece este instalador Olá opção tooinstall adicionais do Azure SDK e as ferramentas de linha de comandos após a instalação Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="6571a-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="6571a-132">Opção 3: Utilizar um contentor de Docker</span><span class="sxs-lookup"><span data-stu-id="6571a-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="6571a-133">Se tiver configurado o computador como um [Docker](https://docs.docker.com/engine/understanding-docker/) anfitrião, pode executar hello mais recente do Azure CLI 1.0 num contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="6571a-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="6571a-134">Execute hello os seguintes comandos (sobre as distribuições do Linux, poderá ter toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="6571a-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="6571a-135">Executar comandos da CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6571a-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="6571a-136">Depois de Olá CLI do Azure 1.0 está instalado, execute Olá **azure** comando da sua interface de utilizador da linha de comandos (Bash, Terminal, linha de comandos e assim sucessivamente).</span><span class="sxs-lookup"><span data-stu-id="6571a-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="6571a-137">Por exemplo, o comando de ajuda do toorun Olá, escreva o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="6571a-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="6571a-138">Em algumas distribuições de Linux, poderá receber um erro semelhante demasiado`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="6571a-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="6571a-139">Este erro provém de instalações recentes do Node.js a ser instalado em /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="6571a-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="6571a-140">toofix, criar um ligação simbólica demasiado/usr/bin/nó ao executar o comando:</span><span class="sxs-lookup"><span data-stu-id="6571a-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="6571a-141">versão de Olá toosee de Olá Azure CLI 1.0 instalado, Olá tipo seguintes:</span><span class="sxs-lookup"><span data-stu-id="6571a-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="6571a-142">Agora, está pronto!</span><span class="sxs-lookup"><span data-stu-id="6571a-142">Now you are ready!</span></span> <span data-ttu-id="6571a-143">todos os tooaccess Olá toowork de comandos da CLI com os seus próprios recursos, [ligar tooyour subscrição do Azure a partir de Olá CLI do Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6571a-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6571a-144">Quando utilizar a CLI do Azure pela primeira vez, é apresentada uma mensagem a perguntar se pretende tooallow as informações de utilização do Microsoft toocollect.</span><span class="sxs-lookup"><span data-stu-id="6571a-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="6571a-145">A participação é voluntária.</span><span class="sxs-lookup"><span data-stu-id="6571a-145">Participation is voluntary.</span></span> <span data-ttu-id="6571a-146">Se escolher tooparticipate, pode parar em qualquer altura executando `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="6571a-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="6571a-147">tooenable participação em qualquer altura, execute `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="6571a-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="6571a-148">Atualizar Olá CLI</span><span class="sxs-lookup"><span data-stu-id="6571a-148">Update hello CLI</span></span>
<span data-ttu-id="6571a-149">Microsoft frequentemente versões versões atualizadas dos Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6571a-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="6571a-150">Reinstalar Olá CLI utilizando o instalador Olá do seu sistema operativo ou executar o contentor de Docker Olá mais recente.</span><span class="sxs-lookup"><span data-stu-id="6571a-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="6571a-151">Ou, se tiver hello mais recente Node.js e npm instalado, atualizar, escrevendo Olá seguinte (nas distribuições do Linux, poderá ter toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="6571a-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="6571a-152">Ativar a conclusão de separador</span><span class="sxs-lookup"><span data-stu-id="6571a-152">Enable tab completion</span></span>
<span data-ttu-id="6571a-153">Conclusão de separador de comandos da CLI é suportada para Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="6571a-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="6571a-154">tooenable-lo na zsh, execute:</span><span class="sxs-lookup"><span data-stu-id="6571a-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="6571a-155">tooenable-lo na bash, execute:</span><span class="sxs-lookup"><span data-stu-id="6571a-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="6571a-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6571a-156">Next steps</span></span>
* <span data-ttu-id="6571a-157">[Ligar a partir de Olá CLI tooyour subscrição do Azure](xplat-cli-connect.md) toocreate e gerir recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6571a-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="6571a-158">toolearn mais informações sobre Olá CLI do Azure, transferir o código de origem, problemas, ou contribuir toohello projeto, visite Olá [repositório do GitHub para Olá CLI do Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="6571a-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="6571a-159">Se tiver dúvidas sobre como utilizar Olá CLI do Azure ou do Azure, visite Olá [fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="6571a-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
