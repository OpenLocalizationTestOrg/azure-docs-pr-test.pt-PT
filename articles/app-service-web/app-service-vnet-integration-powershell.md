---
title: "aaaConnect aplicação tooyour rede virtual com o PowerShell"
description: "Instruções sobre como tooconnect tooand trabalhar com redes virtuais utilizando o PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="3a339-103">Ligar a sua rede virtual de tooyour de aplicação utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a339-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="3a339-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="3a339-104">Overview</span></span>
<span data-ttu-id="3a339-105">No App Service do Azure, pode ligar-se a aplicação (web, móveis ou API) tooan rede virtual do Azure (VNet) na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="3a339-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="3a339-106">Esta funcionalidade é denominada a integração de VNet.</span><span class="sxs-lookup"><span data-stu-id="3a339-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="3a339-107">a funcionalidade de integração de VNet Olá não deve ser confundida com funcionalidade de ambiente de serviço de aplicações de Olá, permitindo-lhe toorun uma instância do App Service do Azure na sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="3a339-108">a funcionalidade de integração de VNet Olá tem uma interface de utilizador (IU) do novo portal de Olá que pode utilizar toointegrate com redes virtuais que são implementadas utilizando o modelo de implementação clássica Olá ou modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="3a339-109">Se pretender toolearn mais informações sobre a funcionalidade de Olá, veja [integrar a sua aplicação com uma Azure virtual network](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="3a339-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="3a339-110">Este artigo é não sobre como toouse Olá IU mas em vez disso, sobre como tooenable integração com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a339-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="3a339-111">Porque os comandos de Olá para cada modelo de implementação forem diferentes, este artigo tem uma secção para cada modelo de implementação.</span><span class="sxs-lookup"><span data-stu-id="3a339-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="3a339-112">Antes de continuar com este artigo, certifique-se de que tem:</span><span class="sxs-lookup"><span data-stu-id="3a339-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="3a339-113">Olá que Azure PowerShell SDK mais recente instalada.</span><span class="sxs-lookup"><span data-stu-id="3a339-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="3a339-114">Pode instalá-lo com Olá instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="3a339-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="3a339-115">Uma aplicação no serviço de aplicações do Azure em execução num padrão ou Premium SKU.</span><span class="sxs-lookup"><span data-stu-id="3a339-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="3a339-116">Redes virtuais clássicas</span><span class="sxs-lookup"><span data-stu-id="3a339-116">Classic virtual networks</span></span>
<span data-ttu-id="3a339-117">Esta secção explica três tarefas para as redes virtuais que utilizam o modelo de implementação clássica Olá:</span><span class="sxs-lookup"><span data-stu-id="3a339-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="3a339-118">Ligar a sua aplicação tooa pré-existentes rede virtual que tem um gateway e está configurado para a conetividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="3a339-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="3a339-119">Atualize as informações de integração de rede virtual para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a339-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="3a339-120">Desligue a sua aplicação da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="3a339-121">Ligar uma aplicação tooa VNet clássica</span><span class="sxs-lookup"><span data-stu-id="3a339-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="3a339-122">tooconnect uma aplicação tooa rede virtual, siga estes três passos:</span><span class="sxs-lookup"><span data-stu-id="3a339-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="3a339-123">Declare toohello web aplicação que irá associar uma rede virtual específico.</span><span class="sxs-lookup"><span data-stu-id="3a339-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="3a339-124">aplicação Olá irá gerar um certificado que irá receber toohello de rede virtual para a conetividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="3a339-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="3a339-125">Carregar Olá web app certificado toohello rede virtual e, em seguida, obter o pacote de VPN de ponto a site Olá URI.</span><span class="sxs-lookup"><span data-stu-id="3a339-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="3a339-126">Atualize a ligação de rede virtual da aplicação web Olá com o URI do pacote de ponto a site Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="3a339-127">Olá primeiro e terceiro passos são totalmente passível de ter scripts, mas o segundo passo de Olá requer uma ação única, manual através do portal Olá ou acesso tooperform **colocar** ou **PATCH** ações na rede virtual Olá Ponto final do Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a339-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="3a339-128">Contacte o suporte do Azure toohave esta opção ativada.</span><span class="sxs-lookup"><span data-stu-id="3a339-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="3a339-129">Antes de começar, certifique-se de que tem uma rede virtual clássica que tem conetividade ponto a site já ativada e um gateway implementado.</span><span class="sxs-lookup"><span data-stu-id="3a339-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="3a339-130">toocreate Olá gateway e ativar ponto a site conectividade, tem de portal de Olá toouse conforme descrito em [criar um gateway VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="3a339-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="3a339-131">Olá clássico rede virtual tem de toobe Olá mesma subscrição que o serviço de aplicações planear essa aplicação Olá contém que está a integrar.</span><span class="sxs-lookup"><span data-stu-id="3a339-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="3a339-132">Configurar o Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="3a339-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="3a339-133">Abra uma janela do PowerShell e configurar a sua conta do Azure e subscrição utilizando:</span><span class="sxs-lookup"><span data-stu-id="3a339-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3a339-134">Esse comando irá abrir uma linha de comandos tooget as suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a339-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="3a339-135">Depois de iniciar sessão, tem de utilizar uma das Olá subscrição Olá tooselect de comandos que pretende que o toouse a seguir.</span><span class="sxs-lookup"><span data-stu-id="3a339-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="3a339-136">Certifique-se de que está a utilizar subscrição Olá destinadas a sua rede virtual e o plano de serviço aplicacional no.</span><span class="sxs-lookup"><span data-stu-id="3a339-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="3a339-137">ou</span><span class="sxs-lookup"><span data-stu-id="3a339-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="3a339-138">Variáveis utilizadas neste artigo</span><span class="sxs-lookup"><span data-stu-id="3a339-138">Variables used in this article</span></span>
<span data-ttu-id="3a339-139">os comandos toosimplify, iremos irá definir um **$Configuration** variável do PowerShell com uma configuração especial Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="3a339-140">Defina uma variável da seguinte forma no PowerShell com Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="3a339-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="3a339-141">localização da aplicação Olá deve ser uma localização de Olá sem quaisquer espaços.</span><span class="sxs-lookup"><span data-stu-id="3a339-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="3a339-142">Por exemplo, EUA oeste é westus.</span><span class="sxs-lookup"><span data-stu-id="3a339-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="3a339-143">Olá o item seguinte é onde o certificado de Olá deve ser escrito.</span><span class="sxs-lookup"><span data-stu-id="3a339-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="3a339-144">Deve ser um caminho gravável no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="3a339-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="3a339-145">Certifique-se de que tooinclude. cer no fim de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="3a339-146">toosee que definir, tipo **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3a339-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="3a339-147">rest Olá desta secção assume que tem uma variável criada como descrito apenas.</span><span class="sxs-lookup"><span data-stu-id="3a339-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="3a339-148">Declarar Olá rede virtual toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="3a339-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="3a339-149">Utilize Olá seguir comando tootell Olá aplicação que irá utilizar esta rede virtual específico.</span><span class="sxs-lookup"><span data-stu-id="3a339-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="3a339-150">Isto fará com que Olá aplicação toogenerate certificados necessários:</span><span class="sxs-lookup"><span data-stu-id="3a339-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="3a339-151">Se este comando for bem sucedida, **$vnet** deve ter um **propriedades** variável na mesma.</span><span class="sxs-lookup"><span data-stu-id="3a339-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="3a339-152">Olá **propriedades** variável deve conter ambos um certificado thumbprint e Olá dados do certificado.</span><span class="sxs-lookup"><span data-stu-id="3a339-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="3a339-153">Carregar Olá web app certificado toohello rede virtual</span><span class="sxs-lookup"><span data-stu-id="3a339-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="3a339-154">Uma manual, único passo é necessário para cada subscrição e a combinação de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="3a339-155">Ou seja, se estiver a ligar aplicações na subscrição A tooVirtual rede A, terá de toodo este passo apenas assim, independentemente da forma como muitas aplicações que configurar.</span><span class="sxs-lookup"><span data-stu-id="3a339-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="3a339-156">Se estiver a adicionar uma nova rede virtual de tooanother de aplicação, terá de voltar toodo.</span><span class="sxs-lookup"><span data-stu-id="3a339-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="3a339-157">motivo de Olá para isto é que um conjunto de certificados é gerado um nível de subscrição no App Service do Azure e o conjunto de Olá é gerado uma vez para cada rede virtual que Olá aplicações estabelecerão ligação ao.</span><span class="sxs-lookup"><span data-stu-id="3a339-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="3a339-158">Olá certificados serão já foram definidos se seguido estes passos ou se integrado Olá mesma rede virtual com portal Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="3a339-159">Step-by-Olá primeiro passo é o ficheiro do toogenerate Olá. cer.</span><span class="sxs-lookup"><span data-stu-id="3a339-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="3a339-160">Step-by-Olá segundo passo é tooupload Olá. cer ficheiro tooyour rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="3a339-161">ficheiro. cer de Olá de toogenerate da chamada de API de Olá no Olá passo anterior, execute os seguintes comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="3a339-162">certificado de Olá irá ser encontrado na localização de Olá que **$Configuration.GeneratedCertificatePath** especifica.</span><span class="sxs-lookup"><span data-stu-id="3a339-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="3a339-163">certificado de Olá tooupload manualmente, utilize Olá [portal do Azure] [ azureportal] e **procurar (Virtual Network clássica)** > **deligaçõesdeVPN**  >  **Ponto a site** > **gerir certificados**.</span><span class="sxs-lookup"><span data-stu-id="3a339-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="3a339-164">Aqui, carregue o certificado.</span><span class="sxs-lookup"><span data-stu-id="3a339-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="3a339-165">Obter o pacote do ponto a site Olá</span><span class="sxs-lookup"><span data-stu-id="3a339-165">Get hello point-to-site package</span></span>
<span data-ttu-id="3a339-166">Olá próximo passo como configurar uma ligação de rede virtual numa aplicação web é tooget Olá ponto a site pacote e fornecê-lo tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3a339-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="3a339-167">Guarde Olá seguintes modelo tooa ficheiro chamado GetNetworkPackageUri.json algures no seu computador, por exemplo, C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="3a339-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="3a339-168">Definir os parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="3a339-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="3a339-169">Chamada Olá script:</span><span class="sxs-lookup"><span data-stu-id="3a339-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="3a339-170">variável de Olá **$output. Outputs.packageUri** agora irá conter Olá pacote URI toobe fornecido tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3a339-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="3a339-171">Carregar Olá ponto a site pacote tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="3a339-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="3a339-172">passo final Olá é tooprovide Olá aplicação com este pacote.</span><span class="sxs-lookup"><span data-stu-id="3a339-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="3a339-173">Basta executar o comando seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="3a339-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="3a339-174">Se uma mensagem pede-lhe tooconfirm que estiver a substituir um recurso existente, certifique-se de que tooallow-lo.</span><span class="sxs-lookup"><span data-stu-id="3a339-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="3a339-175">Depois deste comando for bem sucedida, a aplicação deve ser ligado toohello rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="3a339-176">sucesso tooconfirm, aceda a consola de aplicação tooyour e escreva Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="3a339-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="3a339-177">Se existir uma variável de ambiente chamada WEBSITE_VNETNAME que tem um valor que corresponde ao nome de Olá da rede virtual de destino Olá, todas as configurações de êxito.</span><span class="sxs-lookup"><span data-stu-id="3a339-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="3a339-178">Atualizar informações de integração de VNet clássicas</span><span class="sxs-lookup"><span data-stu-id="3a339-178">Update classic VNet integration information</span></span>
<span data-ttu-id="3a339-179">tooupdate ou ressincronizar as suas informações, basta repetir os passos de Olá que seguiu quando criou a integração de Olá assegurados primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="3a339-180">Esses passos são:</span><span class="sxs-lookup"><span data-stu-id="3a339-180">Those steps are:</span></span>

1. <span data-ttu-id="3a339-181">Defina as informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="3a339-181">Define your configuration information.</span></span>
2. <span data-ttu-id="3a339-182">Declare Olá rede virtual toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a339-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="3a339-183">Obter o pacote de ponto a site Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="3a339-184">Carregar Olá ponto a site pacote tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a339-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="3a339-185">Desligue a aplicação uma VNet clássica</span><span class="sxs-lookup"><span data-stu-id="3a339-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="3a339-186">toodisconnect Olá aplicação, precisa de informações de configuração de Olá que foi definidas durante a integração de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="3a339-187">Utilizar essas informações, há, em seguida, de um comando toodisconnect a aplicação da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="3a339-188">Redes virtuais do Gestor de recursos</span><span class="sxs-lookup"><span data-stu-id="3a339-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="3a339-189">Redes virtuais do Gestor de recursos tem APIs do Azure Resource Manager, que simplificar algumas processos quando comparados com redes virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="3a339-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="3a339-190">Temos um script que irá ajudar a concluir Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="3a339-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="3a339-191">Criar uma rede virtual do Gestor de recursos e integrar a sua aplicação com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="3a339-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="3a339-192">Criar um gateway, configure a conetividade ponto a site numa rede virtual do Resource Manager pré-existentes e, em seguida, integrar a sua aplicação com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="3a339-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="3a339-193">Integre a aplicação com uma pré-existentes rede virtual do Gestor de recursos que tem um gateway e ativar a conetividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="3a339-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="3a339-194">Desligue a sua aplicação da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="3a339-195">Script de integração de serviço de aplicações de VNet do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a339-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="3a339-196">Copie Olá seguinte script e guarde-o ficheiro de tooa.</span><span class="sxs-lookup"><span data-stu-id="3a339-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="3a339-197">Se não quiser que o script de Olá toouse, sentir toolearn livre do mesmo toosee como coisas tooset cópias de segurança com uma rede virtual do Gestor de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a339-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="3a339-198">Guarde uma cópia do script Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-198">Save a copy of hello script.</span></span> <span data-ttu-id="3a339-199">Neste artigo, é denominado V2VnetAllinOne.ps1, mas pode utilizar outro nome.</span><span class="sxs-lookup"><span data-stu-id="3a339-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="3a339-200">Não existem sem argumentos para este script.</span><span class="sxs-lookup"><span data-stu-id="3a339-200">There are no arguments for this script.</span></span> <span data-ttu-id="3a339-201">Pode simplesmente executá-la.</span><span class="sxs-lookup"><span data-stu-id="3a339-201">You simply run it.</span></span> <span data-ttu-id="3a339-202">Olá primeiro thing script Olá executará está a solicitar-lhe toosign no.</span><span class="sxs-lookup"><span data-stu-id="3a339-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="3a339-203">Depois de iniciar sessão, o script de Olá obtém os detalhes sobre a sua conta e devolve uma lista de subscrições.</span><span class="sxs-lookup"><span data-stu-id="3a339-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="3a339-204">Sem contar pedido Olá as suas credenciais, execução de script inicial Olá este aspeto:</span><span class="sxs-lookup"><span data-stu-id="3a339-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="3a339-205">Demonstração de subscrição (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="3a339-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="3a339-206">Teste MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="3a339-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="3a339-207">Subscrição de demonstração roxa (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="3a339-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="3a339-208">Escolher uma opção: 3</span><span class="sxs-lookup"><span data-stu-id="3a339-208">Choose an option: 3</span></span>

    <span data-ttu-id="3a339-209">Conta: ccompy@microsoft.com ambiente: subscrição AzureCloud: inquilino 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d: 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="3a339-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="3a339-210">Introduza Olá grupo de recursos da sua aplicação: hcdemo rg introduza Olá nome da sua aplicação: v2vnetpowershell o que fazer pretende toodo?</span><span class="sxs-lookup"><span data-stu-id="3a339-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="3a339-211">Adicionar uma aplicação de tooan nova rede Virtual</span><span class="sxs-lookup"><span data-stu-id="3a339-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="3a339-212">Adicionar uma aplicação de tooan de rede Virtual existente</span><span class="sxs-lookup"><span data-stu-id="3a339-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="3a339-213">Remover uma rede Virtual a partir de uma aplicação</span><span class="sxs-lookup"><span data-stu-id="3a339-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="3a339-214">Olá resto esta secção explica cada uma dessas três opções.</span><span class="sxs-lookup"><span data-stu-id="3a339-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="3a339-215">Criar uma VNet do Resource Manager e integrar com o mesmo</span><span class="sxs-lookup"><span data-stu-id="3a339-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="3a339-216">Selecione uma nova rede virtual que utiliza Olá modelo de implementação do Resource Manager e integrá-lo com a sua aplicação, de toocreate **1) adicionar uma nova rede Virtual de tooan aplicação**.</span><span class="sxs-lookup"><span data-stu-id="3a339-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="3a339-217">Esta ação irá solicitar-nome Olá da rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="3a339-218">A minha caso, como pode ver no Olá definições, os seguintes utilizei nome Olá, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="3a339-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="3a339-219">script de Olá fornece detalhes de Olá sobre Olá de rede virtual está a ser criada.</span><span class="sxs-lookup"><span data-stu-id="3a339-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="3a339-220">Se as pretendo, pode alterar qualquer um dos valores de Olá</span><span class="sxs-lookup"><span data-stu-id="3a339-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="3a339-221">Na execução deste exemplo, criar uma rede virtual que tenha Olá seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="3a339-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="3a339-222">Se quiser toochange qualquer um dos valores de Olá, escreva **Y** e efetuar alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="3a339-223">Quando estiver satisfeito com as definições de rede virtual Olá, escreva **N** ou simplesmente prima Enter quando lhe for pedido sobre como alterar as definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="3a339-224">A partir daí no até conclusão, o script de Olá informará alguns dos qual it' i's fazer antes de iniciar o gateway de rede virtual toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="3a339-225">Esse passo pode demorar até tooan hora.</span><span class="sxs-lookup"><span data-stu-id="3a339-225">That step can take up tooan hour.</span></span> <span data-ttu-id="3a339-226">Não existe nenhum indicador de progresso durante esta fase, mas script Olá irá informá-lo a quando gateway Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="3a339-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="3a339-227">Quando termina o script de Olá, irá indicar **concluído**.</span><span class="sxs-lookup"><span data-stu-id="3a339-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="3a339-228">Neste momento, terá de uma rede virtual do Gestor de recursos com o nome de Olá e definições que selecionou.</span><span class="sxs-lookup"><span data-stu-id="3a339-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="3a339-229">Esta nova rede virtual também será integrada com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a339-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="3a339-230">Integrar a sua aplicação com uma VNet do Resource Manager pré-existentes</span><span class="sxs-lookup"><span data-stu-id="3a339-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="3a339-231">Quando estiver a integrar uma rede virtual preexistentes, se fornecer uma Gestor de recursos de rede virtual não tem um gateway ou a conetividade ponto a site, Olá será definido o script que cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="3a339-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="3a339-232">Se Olá VNET já essas ações configurar, o script de Olá fica toohello direitas integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="3a339-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="3a339-233">toostart este processo, basta selecionar **2) adicione tooan uma rede Virtual existente aplicação**.</span><span class="sxs-lookup"><span data-stu-id="3a339-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="3a339-234">Esta opção só funciona se tiver uma pré-existentes rede virtual do Gestor de recursos que está a ser Olá mesma subscrição que a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a339-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="3a339-235">Depois de selecionar a opção de Olá, será apresentada uma lista de redes virtuais do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a339-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="3a339-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="3a339-236">v2demonetwork</span></span>
    2) <span data-ttu-id="3a339-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="3a339-237">v2pshell</span></span>
    3) <span data-ttu-id="3a339-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="3a339-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="3a339-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="3a339-239">v2asenetwork</span></span>
    5) <span data-ttu-id="3a339-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="3a339-240">v2pshell2</span></span>

    <span data-ttu-id="3a339-241">Escolher uma opção: 5</span><span class="sxs-lookup"><span data-stu-id="3a339-241">Choose an option: 5</span></span>

<span data-ttu-id="3a339-242">Selecione simplesmente Olá de rede virtual pretende toointegrate com.</span><span class="sxs-lookup"><span data-stu-id="3a339-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="3a339-243">Se já tiver um gateway que tem conetividade ponto a site ativada, o script de Olá simplesmente integrar a aplicação com a sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3a339-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="3a339-244">Se não tiver um gateway, terá de sub-rede do gateway toospecify Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="3a339-245">A sub-rede do gateway tem de estar no seu espaço de endereços de rede virtual e não pode ser qualquer outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="3a339-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="3a339-246">Se tiver uma rede virtual sem um gateway e execute este passo, coisas este aspeto:</span><span class="sxs-lookup"><span data-stu-id="3a339-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="3a339-247">Neste exemplo, criar um gateway de rede virtual que tenha Olá seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="3a339-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="3a339-248">Se quiser toochange qualquer um dessas definições, pode fazê.</span><span class="sxs-lookup"><span data-stu-id="3a339-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="3a339-249">Caso contrário, prima Enter e script Olá irá criar o gateway e anexar a rede virtual do tooyour de aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a339-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="3a339-250">hora de criação do gateway Olá ainda é uma hora, embora, por isso, certifique-se de que que tenha em atenção.</span><span class="sxs-lookup"><span data-stu-id="3a339-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="3a339-251">Quando tudo estiver concluído, o script de Olá indicará **concluído**.</span><span class="sxs-lookup"><span data-stu-id="3a339-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="3a339-252">Desligar a aplicação a partir de uma VNet do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a339-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="3a339-253">A aplicação da sua rede virtual não tirá gateway Olá ou desativar a conetividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="3a339-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="3a339-254">Pode, após todos os, estar a utilizar, de outra coisa.</span><span class="sxs-lookup"><span data-stu-id="3a339-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="3a339-255">-Também não desligue-o de todas as outras aplicações que não sejam Olá um fornecida.</span><span class="sxs-lookup"><span data-stu-id="3a339-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="3a339-256">tooperform esta ação, selecione **3) remover uma rede Virtual a partir de uma aplicação**.</span><span class="sxs-lookup"><span data-stu-id="3a339-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="3a339-257">Quando o fizer, verá algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="3a339-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="3a339-258">Embora o script de Olá indica eliminar, não elimina a rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="3a339-259">Apenas é a remoção integração Olá.</span><span class="sxs-lookup"><span data-stu-id="3a339-259">It’s just removing hello integration.</span></span> <span data-ttu-id="3a339-260">Depois de confirmar que este é o que pretende toodo, o comando de Olá é processado bastante rapidamente e indica **verdadeiro** quando é efetuada.</span><span class="sxs-lookup"><span data-stu-id="3a339-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
