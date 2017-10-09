---
title: aaaUsing tooDev tooPublish de Scripts do Windows PowerShell e ambientes de teste | Microsoft Docs
description: Saiba como toouse do Windows PowerShell scripts de ambientes de toodevelopment e teste de toopublish do Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="06e42-103">Com o Windows PowerShell scripts toopublish toodev e teste ambientes</span><span class="sxs-lookup"><span data-stu-id="06e42-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="06e42-104">Quando cria uma aplicação web no Visual Studio, pode gerar um script do Windows PowerShell que pode utilizar a publicação de Olá de tooautomate posterior do seu Web site tooAzure como uma aplicação Web no App Service do Azure ou uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06e42-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="06e42-105">Pode editar e expandir os seus requisitos de script do Windows PowerShell Olá no toosuit de editor do Visual Studio Olá ou integrar o script de Olá compilação existente, teste e publicação de scripts.</span><span class="sxs-lookup"><span data-stu-id="06e42-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="06e42-106">Utilizar estes scripts, pode aprovisionar versões personalizadas (também conhecido como ambientes de desenvolvimento e teste) do seu site para utilização temporária.</span><span class="sxs-lookup"><span data-stu-id="06e42-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="06e42-107">Por exemplo, poderá configurar uma versão específica do seu site numa máquina virtual do Azure ou num Olá ranhura toorun um Web site de teste um conjunto de teste, reproduzir de erros, teste uma correção de erros, versão de avaliação de uma alteração proposta ou configurar um ambiente personalizado para um demonstração ou apresentação.</span><span class="sxs-lookup"><span data-stu-id="06e42-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="06e42-108">Depois de criar um script que publica o seu projeto, pode recriar ambientes idênticos, executando novamente o script Olá conforme necessário ou executar script de Olá com a seus próprios compilação do seu toocreate de aplicação web num ambiente personalizado para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="06e42-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="06e42-109">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="06e42-109">What you need</span></span>
* <span data-ttu-id="06e42-110">Azure SDK 2.3 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="06e42-111">Consulte [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="06e42-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="06e42-112">Não é necessário scripts de Olá toogenerate do Olá Azure SDK para projetos web.</span><span class="sxs-lookup"><span data-stu-id="06e42-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="06e42-113">Esta funcionalidade destina-se a projetos web, não funções da web nos serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="06e42-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="06e42-114">O Azure PowerShell 0.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="06e42-115">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="06e42-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="06e42-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="06e42-117">Ferramentas adicionais</span><span class="sxs-lookup"><span data-stu-id="06e42-117">Additional tools</span></span>
<span data-ttu-id="06e42-118">Ferramentas adicionais e recursos para trabalhar com o PowerShell no Visual Studio para desenvolvimento do Azure estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="06e42-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="06e42-119">Consulte [PowerShell Tools para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="06e42-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="06e42-120">Gerar Olá publicar scripts</span><span class="sxs-lookup"><span data-stu-id="06e42-120">Generating hello publish scripts</span></span>
<span data-ttu-id="06e42-121">Pode gerar Olá publicar scripts para uma máquina virtual que aloja o seu Web site quando criar um novo projeto seguindo [estas instruções](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e42-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="06e42-122">Também pode [gerar publicar scripts para as web apps no App Service do Azure](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="06e42-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="06e42-123">Scripts que gera o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06e42-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="06e42-124">Visual Studio gera uma pasta de nível de solução denominada **PublishScripts** que contém dois ficheiros do Windows PowerShell, um script de publicar para a máquina virtual ou Web site e um módulo que contém as funções que pode utilizar Olá scripts.</span><span class="sxs-lookup"><span data-stu-id="06e42-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="06e42-125">Visual Studio também gera um ficheiro no formato JSON Olá que especifica os detalhes de Olá do projeto de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="06e42-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="06e42-126">Script de publicar do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="06e42-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="06e42-127">Olá publicar o script contém específico publicar os passos para implementar tooa site ou a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06e42-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="06e42-128">O Visual Studio fornece sintaxe coloração para desenvolvimento do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06e42-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="06e42-129">Ajuda para as funções de Olá está disponível e livremente pode editar funções de Olá no Olá script toosuit os requisitos de alteração.</span><span class="sxs-lookup"><span data-stu-id="06e42-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="06e42-130">Módulo do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="06e42-130">Windows PowerShell module</span></span>
<span data-ttu-id="06e42-131">Olá do Windows PowerShell módulo gera do Visual Studio contém funções que Olá publicar utiliza de script.</span><span class="sxs-lookup"><span data-stu-id="06e42-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="06e42-132">Estas são as funções do Azure PowerShell e não são toobe pretendido modificado.</span><span class="sxs-lookup"><span data-stu-id="06e42-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="06e42-133">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="06e42-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="06e42-134">Ficheiro de configuração JSON</span><span class="sxs-lookup"><span data-stu-id="06e42-134">JSON configuration file</span></span>
<span data-ttu-id="06e42-135">ficheiro JSON Olá é criado na Olá **configurações** pasta e contém dados de configuração que especifica exatamente qual tooAzure toodeploy de recursos.</span><span class="sxs-lookup"><span data-stu-id="06e42-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="06e42-136">Olá o nome do ficheiro de Olá que gera o Visual Studio é projeto-nome-WAWS-dev.json se tiver criado um Web site ou o nome de projeto-VM-dev.json se tiver criado uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06e42-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="06e42-137">Eis um exemplo de um ficheiro de configuração JSON que é gerado quando criar um Web site.</span><span class="sxs-lookup"><span data-stu-id="06e42-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="06e42-138">A maioria dos valores de Olá são facilmente compreensíveis.</span><span class="sxs-lookup"><span data-stu-id="06e42-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="06e42-139">nome do Web site Olá é gerado pelo Azure, pelo que não poderá corresponder ao nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="06e42-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="06e42-140">Quando cria uma máquina virtual, o ficheiro de configuração JSON Olá procura semelhante toohello seguinte.</span><span class="sxs-lookup"><span data-stu-id="06e42-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="06e42-141">Tenha em atenção que um serviço em nuvem foi criado como um contentor para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="06e42-142">máquina virtual de Olá contém Olá habitual os pontos finais para o acesso web através de HTTP e HTTPS, bem como pontos finais para o Web Deploy, que lhe permite publicar Web site de toohello do seu computador local, o ambiente de trabalho remoto e o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06e42-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="06e42-143">Pode editar Olá JSON configuração toochange o que acontece quando executar Olá publicar scripts.</span><span class="sxs-lookup"><span data-stu-id="06e42-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="06e42-144">Olá `cloudService` e `virtualMachine` secções são necessárias, mas pode eliminar Olá `databases` secção se não o tiver.</span><span class="sxs-lookup"><span data-stu-id="06e42-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="06e42-145">Propriedades de Olá que estão vazios no ficheiro de configuração predefinida do Olá que gera o Visual Studio são opcionais; que têm valores no ficheiro de configuração predefinido Olá são necessários.</span><span class="sxs-lookup"><span data-stu-id="06e42-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="06e42-146">Se tiver um site que tenha vários ambientes de implementação (conhecidos como ranhuras) em vez de um site de produção único no Azure, pode incluir nome de ranhura Olá no nome de Olá do Web site de Olá no ficheiro de configuração do Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="06e42-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="06e42-147">Por exemplo, se tiver um site com o nome **mysite** e uma ranhura para o mesmo nome **testar** , em seguida, Olá URI é mysite test.cloudapp.net, mas Olá toouse de nome correto no ficheiro de configuração de Olá mysite(test) .</span><span class="sxs-lookup"><span data-stu-id="06e42-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="06e42-148">Só pode fazer isto, se o Web site de Olá e ranhuras já existem na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="06e42-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="06e42-149">Se não existirem, criar site Olá executando o script de Olá sem especificar ranhura Olá, em seguida, criar ranhura Olá no Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), e após executar o script de Olá com o nome de Web site modificado Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="06e42-150">Para obter mais informações sobre as ranhuras de implementação para aplicações web, consulte [configurar ambientes para web apps no App Service do Azure de teste](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="06e42-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="06e42-151">Como toorun Olá publicar scripts</span><span class="sxs-lookup"><span data-stu-id="06e42-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="06e42-152">Se nunca tiver executado um script do Windows PowerShell antes, primeiro tem de definir Olá execução política tooenable scripts toorun.</span><span class="sxs-lookup"><span data-stu-id="06e42-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="06e42-153">Esta é a segurança funcionalidade tooprevent os utilizadores executem scripts do Windows PowerShell se não estiverem toomalware vulnerável ou vírus que envolvam a execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="06e42-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="06e42-154">Executar script de Olá</span><span class="sxs-lookup"><span data-stu-id="06e42-154">Run hello script</span></span>
1. <span data-ttu-id="06e42-155">Crie pacote Olá Web Deploy para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="06e42-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="06e42-156">Um pacote do Web Deploy é um arquivo comprimido (ficheiro. zip) que contêm ficheiros que pretende que o Web site de tooyour toocopy ou máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06e42-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="06e42-157">Pode criar pacotes Web Deploy no Visual Studio para qualquer aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06e42-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Criar Web implementar o pacote](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="06e42-159">Para obter mais informações, consulte [como: criar um pacote de implementação Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="06e42-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="06e42-160">Também pode automatizar criação Olá do pacote do Web Deploy, conforme descrito na secção de Olá **Customizing e expandir Olá publicar scripts** mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="06e42-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="06e42-161">No **Explorador de soluções**, abra o menu de contexto de Olá para script Olá e, em seguida, escolha **abra o ISE do PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="06e42-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="06e42-162">Se este for Olá pela primeira vez que executar scripts do Windows PowerShell no computador, abra uma janela de linha de comandos com privilégios de administrador e Olá tipo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="06e42-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="06e42-163">Inicie sessão tooAzure com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="06e42-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="06e42-164">Quando lhe for pedido, forneça o nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="06e42-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="06e42-165">Tenha em atenção que, ao automatizar o script de Olá, este método de fornecer credenciais do Azure não irão funcionar.</span><span class="sxs-lookup"><span data-stu-id="06e42-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="06e42-166">Em vez disso, deve utilizar as credenciais do Olá. publishsettings ficheiro tooprovide.</span><span class="sxs-lookup"><span data-stu-id="06e42-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="06e42-167">Uma vez, pode utiliza apenas comandos Olá **Get-AzurePublishSettingsFile** Olá toodownload de ficheiros a partir do Azure e utilizar após **importação AzurePublishSettingsFile** ficheiros de Olá tooimport.</span><span class="sxs-lookup"><span data-stu-id="06e42-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="06e42-168">Para obter instruções detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06e42-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="06e42-169">(Opcional) Se quiser toocreate Azure recursos, tais como máquina virtual de Olá, a base de dados e o Web site sem a publicação da sua aplicação web, utilizam Olá **publicar WebApplication.ps1** comando com Olá **-configuração** argumento definido toohello ficheiro de configuração de JSON.</span><span class="sxs-lookup"><span data-stu-id="06e42-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="06e42-170">Esta linha de comandos utiliza toodetermine de ficheiro de configuração do Olá JSON que toocreate de recursos.</span><span class="sxs-lookup"><span data-stu-id="06e42-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="06e42-171">Porque utiliza as predefinições de Olá para outros argumentos da linha de comandos, cria Olá recursos, mas não publicar a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06e42-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="06e42-172">Olá – opção verbosa dá-lhe obter mais informações sobre o que acontece.</span><span class="sxs-lookup"><span data-stu-id="06e42-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="06e42-173">Olá utilize **publicar WebApplication.ps1** conforme mostrado dos Olá seguinte script de Olá tooinvoke de exemplos de comandos e publicar a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06e42-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="06e42-174">Se precisar de predefinições de Olá toooverride para qualquer uma das Olá outros argumentos, tais como o nome da subscrição Olá, publicar o nome do pacote, credenciais de máquina virtual ou as credenciais do servidor de base de dados, pode especificar os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="06e42-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="06e42-175">Olá utilize **– verboso** opção toosee mais informações sobre o progresso de Olá de Olá processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="06e42-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="06e42-176">Se estiver a criar uma máquina virtual, o comando de Olá aspeto Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="06e42-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="06e42-177">Este exemplo mostra também como toospecify Olá credenciais para várias bases de dados.</span><span class="sxs-lookup"><span data-stu-id="06e42-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="06e42-178">Para máquinas de virtuais Olá que criar estes scripts, certificado SSL Olá não é de uma autoridade de raiz fidedigna.</span><span class="sxs-lookup"><span data-stu-id="06e42-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="06e42-179">Por conseguinte, terá de toouse Olá **– AllowUntrusted** opção.</span><span class="sxs-lookup"><span data-stu-id="06e42-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="06e42-180">script de Olá pode criar bases de dados, mas não criar servidores de base de dados.</span><span class="sxs-lookup"><span data-stu-id="06e42-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="06e42-181">Se quiser toocreate um servidor de base de dados, pode utilizar Olá **New-AzureSqlDatabaseServer** funcionar em Olá módulo do Azure.</span><span class="sxs-lookup"><span data-stu-id="06e42-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="06e42-182">Personalizar e expandir Olá publicar scripts</span><span class="sxs-lookup"><span data-stu-id="06e42-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="06e42-183">Pode personalizar Olá publicar script e o ficheiro de configuração JSON.</span><span class="sxs-lookup"><span data-stu-id="06e42-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="06e42-184">Olá funções no módulo do Windows PowerShell Olá **AzureWebAppPublishModule.psm1** não são toobe pretendido modificado.</span><span class="sxs-lookup"><span data-stu-id="06e42-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="06e42-185">Se apenas pretender toospecify uma base de dados diferente ou alterar algumas das propriedades de Olá da máquina virtual de Olá, edite o ficheiro de configuração do Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="06e42-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="06e42-186">Se pretender que a funcionalidade de Olá tooextend de Olá script tooautomate criar e testar o projeto, pode implementar os stubs de função no **publicar WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="06e42-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="06e42-187">tooautomate compilar o projeto, adicione o código que chama MSBuild demasiado`New-WebDeployPackage` conforme mostrado neste exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="06e42-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="06e42-188">Olá caminho toohello MSBuild comando é diferente consoante a versão de Olá do Visual Studio que instalou.</span><span class="sxs-lookup"><span data-stu-id="06e42-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="06e42-189">caminho correto do Olá tooget, pode utilizar a função de Olá **Get-MSBuildCmd**, conforme mostrado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="06e42-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="06e42-190">tooautomate compilar o projeto</span><span class="sxs-lookup"><span data-stu-id="06e42-190">tooautomate building your project</span></span>
1. <span data-ttu-id="06e42-191">Adicionar Olá `$ProjectFile` parâmetro na secção de global param Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="06e42-192">Copiar a função de Olá `Get-MSBuildCmd` no seu ficheiro de script.</span><span class="sxs-lookup"><span data-stu-id="06e42-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="06e42-193">Substitua `New-WebDeployPackage` com Olá seguinte código e substitua Olá marcadores de posição no Olá linha construir `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="06e42-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="06e42-194">Este código é para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="06e42-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="06e42-195">Se estiver a utilizar o Visual Studio 2013, altere Olá **VisualStudioVersion** propriedade abaixo demasiado`12.0`.</span><span class="sxs-lookup"><span data-stu-id="06e42-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="06e42-196">toobuild a aplicação web, utilize MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="06e42-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="06e42-197">Para obter ajuda, consulte a referência da linha de comandos MSBuild: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="06e42-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="06e42-198">Iniciar a execução do comando de compilação de Olá</span><span class="sxs-lookup"><span data-stu-id="06e42-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="06e42-199">Chamar Olá `New-WebDeployPackage` função antes desta linha: `$Config = Read-ConfigFile $Configuration` para aplicações web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="06e42-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="06e42-200">Invocar script Olá personalizada de linha de comandos utilizando a transmissão Olá `$Project` argumento, tal como em Olá linha de comandos de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="06e42-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="06e42-201">tooautomate testar da sua aplicação, adicione o código demasiado`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="06e42-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="06e42-202">Ser toouncomment se linhas Olá **publicar WebApplication.ps1** onde estas funções são denominadas.</span><span class="sxs-lookup"><span data-stu-id="06e42-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="06e42-203">Se não fornecer uma implementação, pode criar manualmente o projeto com o Visual Studio e, em seguida, execute Olá publicar script toopublish tooAzure.</span><span class="sxs-lookup"><span data-stu-id="06e42-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="06e42-204">Função publicação resumo</span><span class="sxs-lookup"><span data-stu-id="06e42-204">Publishing function summary</span></span>
<span data-ttu-id="06e42-205">Ajuda tooget para funções que pode utilizar Olá linha de comandos do Windows PowerShell, utilize o comando de Olá `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="06e42-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="06e42-206">Ajuda Olá inclui ajuda de parâmetro e exemplos.</span><span class="sxs-lookup"><span data-stu-id="06e42-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="06e42-207">Olá texto de ajuda do mesmo é também nos ficheiros de origem do script de Olá, **AzureWebAppPublishModule.psm1** e **publicar WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="06e42-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="06e42-208">script de Olá e ajuda está localizada no seu idioma de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06e42-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="06e42-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="06e42-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="06e42-210">Nome de função</span><span class="sxs-lookup"><span data-stu-id="06e42-210">Function name</span></span> | <span data-ttu-id="06e42-211">Descrição</span><span class="sxs-lookup"><span data-stu-id="06e42-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06e42-212">Adicionar-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="06e42-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="06e42-213">Cria uma nova base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="06e42-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="06e42-214">AzureSQLDatabases adicionar</span><span class="sxs-lookup"><span data-stu-id="06e42-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="06e42-215">Cria bases de dados SQL do Azure a partir de valores de Olá num ficheiro de configuração de JSON Olá que gera o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06e42-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="06e42-216">Adicionar-AzureVM</span><span class="sxs-lookup"><span data-stu-id="06e42-216">Add-AzureVM</span></span> |<span data-ttu-id="06e42-217">Cria uma máquina virtual do Azure e devolve o que URL de Olá de Olá implementado VM.</span><span class="sxs-lookup"><span data-stu-id="06e42-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="06e42-218">Olá função configura os pré-requisitos de Olá e, em seguida, Olá chamadas **New-AzureVM** funcionar (módulo do Azure) toocreate uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06e42-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="06e42-219">AzureVMEndpoints adicionar</span><span class="sxs-lookup"><span data-stu-id="06e42-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="06e42-220">Adiciona a nova máquina de virtual de tooa pontos finais de entrada e devolve Olá máquina de virtual com o novo ponto de final Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="06e42-221">AzureVMStorage adicionar</span><span class="sxs-lookup"><span data-stu-id="06e42-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="06e42-222">Cria uma nova conta de armazenamento do Azure na subscrição atual Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="06e42-223">nome de Olá da conta de Olá começa com "devtest" seguido de uma cadeia alfanumérica exclusiva.</span><span class="sxs-lookup"><span data-stu-id="06e42-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="06e42-224">a função Olá devolve o nome de Olá Olá novo da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="06e42-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="06e42-225">Tem de especificar uma localização ou um grupo de afinidades Olá nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="06e42-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="06e42-226">AzureWebsite adicionar</span><span class="sxs-lookup"><span data-stu-id="06e42-226">Add-AzureWebsite</span></span> |<span data-ttu-id="06e42-227">Cria um Web site com o nome especificado Olá e localização.</span><span class="sxs-lookup"><span data-stu-id="06e42-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="06e42-228">Esta função chama Olá **New-AzureWebsite** funcionar em Olá módulo do Azure.</span><span class="sxs-lookup"><span data-stu-id="06e42-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="06e42-229">Se a subscrição de Olá já não incluir um Web site com o nome especificado Olá, esta função cria o Web site de Olá e devolve um objeto de Web site.</span><span class="sxs-lookup"><span data-stu-id="06e42-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="06e42-230">Caso contrário, devolve `$null`.</span><span class="sxs-lookup"><span data-stu-id="06e42-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="06e42-231">Subscrição de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="06e42-231">Backup-Subscription</span></span> |<span data-ttu-id="06e42-232">Guarda Olá atual subscrição do Azure no Olá `$Script:originalSubscription` variável no âmbito de script. Esta função guarda a subscrição do Azure atual de Olá (tal como obtidas pelo `Get-AzureSubscription -Current`) e a conta do storage e subscrição Olá que é alterada por este script (armazenado na variável Olá `$UserSpecifiedSubscription`) e a respetiva conta de armazenamento, no âmbito de script.</span><span class="sxs-lookup"><span data-stu-id="06e42-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="06e42-233">Ao guardar os valores de Olá, pode utilizar uma função, como `Restore-Subscription`, toorestore Olá original atual subscrição e o armazenamento toocurrent estado da conta se tiver alterado o estado atual do Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="06e42-234">Localizar-AzureVM</span><span class="sxs-lookup"><span data-stu-id="06e42-234">Find-AzureVM</span></span> |<span data-ttu-id="06e42-235">Obtém Olá especificado máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="06e42-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="06e42-236">Formato DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="06e42-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="06e42-237">Prepends mensagem de saudação data e hora tooa.</span><span class="sxs-lookup"><span data-stu-id="06e42-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="06e42-238">Esta função foi concebida para mensagens escritas toohello erro e Verbose fluxos.</span><span class="sxs-lookup"><span data-stu-id="06e42-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="06e42-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="06e42-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="06e42-240">Monta uma ligação cadeia tooconnect tooan SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="06e42-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="06e42-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="06e42-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="06e42-242">Devolve Olá nome Olá primeiro da conta de armazenamento com o padrão de nome de Olá "devtest*" (sensível) no grupo de afinidade ou a localização especificado no Olá. Se Olá "devtest*" conta de armazenamento não corresponde à localização de Olá ou o grupo de afinidade, função Olá ignora-lo.</span><span class="sxs-lookup"><span data-stu-id="06e42-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="06e42-243">Tem de especificar uma localização ou um grupo de afinidade.</span><span class="sxs-lookup"><span data-stu-id="06e42-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="06e42-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="06e42-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="06e42-245">Devolve uma ferramenta do comando toorun Olá MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="06e42-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="06e42-246">Novo AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="06e42-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="06e42-247">Localiza ou cria uma máquina virtual na subscrição Olá que corresponda a valores de Olá no ficheiro de configuração do Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="06e42-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="06e42-248">WebPackage publicar</span><span class="sxs-lookup"><span data-stu-id="06e42-248">Publish-WebPackage</span></span> |<span data-ttu-id="06e42-249">Uma web e utiliza MsDeploy.exe publicou o pacote. Zip ficheiro toodeploy recursos tooa site.</span><span class="sxs-lookup"><span data-stu-id="06e42-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="06e42-250">Esta função não gera qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="06e42-250">This function doesn't generate any output.</span></span> <span data-ttu-id="06e42-251">Se Olá chamada tooMSDeploy.exe falhar, a função de Olá emite uma exceção.</span><span class="sxs-lookup"><span data-stu-id="06e42-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="06e42-252">tooget mais detalhadas de saída, utilize Olá **-Verbose** opção.</span><span class="sxs-lookup"><span data-stu-id="06e42-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="06e42-253">WebPackageToVM publicar</span><span class="sxs-lookup"><span data-stu-id="06e42-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="06e42-254">Verifica os valores de parâmetros de Olá e, em seguida, chama Olá **publicar WebPackage** função.</span><span class="sxs-lookup"><span data-stu-id="06e42-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="06e42-255">Leitura ConfigFile</span><span class="sxs-lookup"><span data-stu-id="06e42-255">Read-ConfigFile</span></span> |<span data-ttu-id="06e42-256">Valida o ficheiro de configuração JSON Olá e devolve uma tabela hash de valores selecionados.</span><span class="sxs-lookup"><span data-stu-id="06e42-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="06e42-257">Subscrição de restauro</span><span class="sxs-lookup"><span data-stu-id="06e42-257">Restore-Subscription</span></span> |<span data-ttu-id="06e42-258">Repõe Olá subscrição toohello original subscrição atual.</span><span class="sxs-lookup"><span data-stu-id="06e42-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="06e42-259">Teste AzureModule</span><span class="sxs-lookup"><span data-stu-id="06e42-259">Test-AzureModule</span></span> |<span data-ttu-id="06e42-260">Devolve `$true` se Olá instalada a versão de módulo do Azure é 0.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="06e42-261">Devolve `$false` se o módulo Olá não está instalado ou uma versão anterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="06e42-262">Esta função não tem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="06e42-262">This function has no parameters.</span></span> |
| <span data-ttu-id="06e42-263">Teste AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="06e42-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="06e42-264">Devolve `$true` se versão Olá Olá módulo Azure for 0.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="06e42-265">Devolve `$false` se o módulo Olá não está instalado ou uma versão anterior.</span><span class="sxs-lookup"><span data-stu-id="06e42-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="06e42-266">Esta função não tem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="06e42-266">This function has no parameters.</span></span> |
| <span data-ttu-id="06e42-267">Teste HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="06e42-267">Test-HttpsUrl</span></span> |<span data-ttu-id="06e42-268">Converte o objeto de URI de tooa Olá entrada URL.</span><span class="sxs-lookup"><span data-stu-id="06e42-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="06e42-269">Devolve `$True` se Olá URL absoluto e a esquema é https.</span><span class="sxs-lookup"><span data-stu-id="06e42-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="06e42-270">Devolve `$false` se Olá URL é relativo, a esquema não é HTTPS ou cadeia de entrada Olá não pode ser convertida tooa URL.</span><span class="sxs-lookup"><span data-stu-id="06e42-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="06e42-271">Membro de teste</span><span class="sxs-lookup"><span data-stu-id="06e42-271">Test-Member</span></span> |<span data-ttu-id="06e42-272">Devolve `$true` se uma propriedade ou método é um membro do objeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="06e42-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="06e42-273">Caso contrário, devolve `$false`.</span><span class="sxs-lookup"><span data-stu-id="06e42-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="06e42-274">Escrita ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="06e42-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="06e42-275">Escreve uma mensagem de erro o prefixo Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="06e42-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="06e42-276">Esta função chama Olá **formato DevTestMessageWithTime** tempo de Olá tooprepend função antes de escrever o fluxo de erro do Olá mensagens toohello.</span><span class="sxs-lookup"><span data-stu-id="06e42-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="06e42-277">Escrita HostWithTime</span><span class="sxs-lookup"><span data-stu-id="06e42-277">Write-HostWithTime</span></span> |<span data-ttu-id="06e42-278">Escreve um programa de anfitrião de toohello de mensagem (**escrita anfitrião**) o prefixo Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="06e42-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="06e42-279">efeito Olá de escrever o programa de anfitrião toohello varia.</span><span class="sxs-lookup"><span data-stu-id="06e42-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="06e42-280">A maioria dos programas nesse anfitrião do Windows PowerShell escrever estas mensagens toostandard saída.</span><span class="sxs-lookup"><span data-stu-id="06e42-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="06e42-281">Escrita VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="06e42-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="06e42-282">Escreve uma mensagem verbosa prefixo Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="06e42-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="06e42-283">Uma vez que chama **Write-Verbose**, mensagem de saudação apresenta apenas quando Olá script é executado com Olá **verboso** parâmetro ou quando Olá **VerbosePreference** preferência é Definir demasiado**continuar**.</span><span class="sxs-lookup"><span data-stu-id="06e42-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="06e42-284">**Publicar-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="06e42-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="06e42-285">Nome de função</span><span class="sxs-lookup"><span data-stu-id="06e42-285">Function name</span></span> | <span data-ttu-id="06e42-286">Descrição</span><span class="sxs-lookup"><span data-stu-id="06e42-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06e42-287">Novo AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="06e42-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="06e42-288">Cria recursos do Azure, tais como um Web site ou a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06e42-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="06e42-289">Novo WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="06e42-289">New-WebDeployPackage</span></span> |<span data-ttu-id="06e42-290">Esta função não está implementada.</span><span class="sxs-lookup"><span data-stu-id="06e42-290">This function isn't implemented.</span></span> <span data-ttu-id="06e42-291">Pode adicionar comandos no toobuild função seu projeto.</span><span class="sxs-lookup"><span data-stu-id="06e42-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="06e42-292">AzureWebApplication publicar</span><span class="sxs-lookup"><span data-stu-id="06e42-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="06e42-293">Publica um tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06e42-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="06e42-294">Publicar-WebApplication</span><span class="sxs-lookup"><span data-stu-id="06e42-294">Publish-WebApplication</span></span> |<span data-ttu-id="06e42-295">Cria e implementa as aplicações Web, as máquinas virtuais, bases de dados SQL e contas de armazenamento para um projeto web do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06e42-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="06e42-296">Teste-WebApplication</span><span class="sxs-lookup"><span data-stu-id="06e42-296">Test-WebApplication</span></span> |<span data-ttu-id="06e42-297">Esta função não está implementada.</span><span class="sxs-lookup"><span data-stu-id="06e42-297">This function isn't implemented.</span></span> <span data-ttu-id="06e42-298">Pode adicionar comandos no tootest função da aplicação.</span><span class="sxs-lookup"><span data-stu-id="06e42-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06e42-299">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06e42-299">Next steps</span></span>
<span data-ttu-id="06e42-300">Saiba mais sobre os scripts do PowerShell através da leitura [Scripting com o Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e ver outros scripts do PowerShell do Azure em Olá [Centro de scripts](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="06e42-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
