---
title: "aaaManage as suas aplicações no Visual Studio | Microsoft Docs"
description: "Utilizar o Visual Studio toocreate, desenvolver, pacote, implementar e depurar os seus serviços e aplicações de Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="d630e-103">Utilize a escrita de toosimplify do Visual Studio e a gestão das suas aplicações de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d630e-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="d630e-104">Pode gerir as suas aplicações do Azure Service Fabric e serviços através do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d630e-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="d630e-105">Assim que tiver [configurar o ambiente de desenvolvimento](service-fabric-get-started.md), pode utilizar as aplicações de Service Fabric do Visual Studio toocreate, adicionar serviços, ou o pacote, registar e implementar aplicações no seu cluster de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="d630e-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="d630e-106">Implementar a aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d630e-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="d630e-107">Por predefinição, a implementar uma aplicação combina Olá os seguintes passos para uma operação simple:</span><span class="sxs-lookup"><span data-stu-id="d630e-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="d630e-108">Criar o pacote de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="d630e-108">Creating hello application package</span></span>
2. <span data-ttu-id="d630e-109">Carregamento Olá pacote toohello imagem loja de aplicações</span><span class="sxs-lookup"><span data-stu-id="d630e-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="d630e-110">Registar o tipo de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="d630e-110">Registering hello application type</span></span>
4. <span data-ttu-id="d630e-111">Remover quaisquer instâncias de aplicações em execução</span><span class="sxs-lookup"><span data-stu-id="d630e-111">Removing any running application instances</span></span>
5. <span data-ttu-id="d630e-112">Criar uma instância de aplicação</span><span class="sxs-lookup"><span data-stu-id="d630e-112">Creating an application instance</span></span>

<span data-ttu-id="d630e-113">No Visual Studio, premindo **F5** implementa a aplicação e anexar instâncias da aplicação Olá depurador tooall.</span><span class="sxs-lookup"><span data-stu-id="d630e-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="d630e-114">Pode utilizar **Ctrl + F5** toodeploy uma aplicação sem depuração, ou pode publicar tooa local ou perfil de publicação de clusters remotos utilizando Olá.</span><span class="sxs-lookup"><span data-stu-id="d630e-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="d630e-115">Para obter mais informações, consulte [publicar um cluster de remoto tooa aplicação utilizando o Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d630e-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="d630e-116">Modo de depuração de aplicações</span><span class="sxs-lookup"><span data-stu-id="d630e-116">Application Debug Mode</span></span>
<span data-ttu-id="d630e-117">Visual Studio fornecem uma propriedade denominada **modo de depuração da aplicação**, que controla a forma como pretende que a implementação de aplicação do Visual estúdios toohandle como parte de depuração.</span><span class="sxs-lookup"><span data-stu-id="d630e-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="d630e-118">Olá tooset propriedade do modo de depuração de aplicações</span><span class="sxs-lookup"><span data-stu-id="d630e-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="d630e-119">No Olá Service Fabric aplicação do projeto (*.sfproj) menu de atalho, escolha **propriedades** (ou prima Olá **F4** chave).</span><span class="sxs-lookup"><span data-stu-id="d630e-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="d630e-120">No Olá **propriedades** janela, conjunto Olá **modo de depuração da aplicação** propriedade.</span><span class="sxs-lookup"><span data-stu-id="d630e-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Definir a propriedade de modo de depuração de aplicações][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="d630e-122">Modos de depuração de aplicações</span><span class="sxs-lookup"><span data-stu-id="d630e-122">Application Debug Modes</span></span>

1. <span data-ttu-id="d630e-123">**Atualizar aplicação** este modo permite-lhe alterar tooquickly e depurar o seu código e suporta a edição de ficheiros estáticos web durante a depuração.</span><span class="sxs-lookup"><span data-stu-id="d630e-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="d630e-124">Este modo só funciona se o cluster de desenvolvimento local está a ser [1 nó modo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="d630e-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="d630e-125">**Remover aplicação** causas Olá toobe aplicação removido quando termina a sessão de depuração Olá.</span><span class="sxs-lookup"><span data-stu-id="d630e-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="d630e-126">**Auto atualização** aplicação Olá continua toorun quando termina a sessão de depuração Olá.</span><span class="sxs-lookup"><span data-stu-id="d630e-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="d630e-127">Olá próxima sessão de depuração irão tratar implementação Olá como uma atualização.</span><span class="sxs-lookup"><span data-stu-id="d630e-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="d630e-128">processo de atualização de Olá preserva todos os dados que introduziu numa sessão de depuração anterior.</span><span class="sxs-lookup"><span data-stu-id="d630e-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="d630e-129">**Manter aplicações** Olá mantém de aplicação em execução no cluster de Olá quando hello terminar sessão de depuração.</span><span class="sxs-lookup"><span data-stu-id="d630e-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="d630e-130">Olá início do Olá próxima sessão de depuração, a aplicação Olá será removida.</span><span class="sxs-lookup"><span data-stu-id="d630e-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="d630e-131">Para **automática atualizar** os dados são preservados aplicando Olá atualização as capacidades das aplicações de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d630e-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="d630e-132">Para obter mais informações sobre como atualizar aplicações e como pode executar uma atualização num ambiente real, consulte [atualização da aplicação de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d630e-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="d630e-133">Adicionar uma aplicação de Service Fabric de tooyour de serviço</span><span class="sxs-lookup"><span data-stu-id="d630e-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="d630e-134">Pode adicionar novos serviços o tooyour aplicação tooextend sua funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="d630e-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="d630e-135">tooensure que o serviço de Olá está incluído no seu pacote de aplicação, adicione o serviço de Olá através de Olá **novo serviço de recursos de infraestrutura...**  item de menu.</span><span class="sxs-lookup"><span data-stu-id="d630e-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Adicionar um novo serviço de Service Fabric][newservice]

<span data-ttu-id="d630e-137">Selecione uma aplicação de tooyour tooadd de tipo de projeto de Service Fabric e especifique um nome para o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="d630e-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="d630e-138">Consulte [escolher uma estrutura para o seu serviço](service-fabric-choose-framework.md) toohelp decidir qual serviço escreva toouse.</span><span class="sxs-lookup"><span data-stu-id="d630e-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Selecionar uma aplicação do Service Fabric serviço projeto tipo tooadd tooyour][addserviceproject]

<span data-ttu-id="d630e-140">é adicionado o novo serviço de Olá tooyour solução e pacote de aplicação existente.</span><span class="sxs-lookup"><span data-stu-id="d630e-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="d630e-141">Olá referências de serviço e uma instância de serviço predefinido será adicionado toohello o manifesto da aplicação, que provocou toobe de serviço Olá criado e iniciado Olá próxima vez que implementa a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d630e-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![o manifesto da aplicação tooyour está a ser adicionado por Olá novo serviço][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="d630e-143">Pacote da aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d630e-143">Package your Service Fabric application</span></span>
<span data-ttu-id="d630e-144">aplicação de Olá toodeploy e o cluster de tooa serviços, terá de toocreate um pacote de aplicação.</span><span class="sxs-lookup"><span data-stu-id="d630e-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="d630e-145">pacote de Olá organiza manifesto da aplicação Olá, manifestos de serviço e outros ficheiros necessários num esquema específico.</span><span class="sxs-lookup"><span data-stu-id="d630e-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="d630e-146">Visual Studio configura e gere Olá pacote na pasta do projeto de aplicação Olá, no diretório do Olá 'pkg'.</span><span class="sxs-lookup"><span data-stu-id="d630e-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="d630e-147">Ao clicar em **pacote** de Olá **aplicação** cria do menu de contexto ou atualizações Olá pacote de aplicação.</span><span class="sxs-lookup"><span data-stu-id="d630e-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="d630e-148">Remover aplicações e tipos de aplicação utilizando o Explorador de nuvem</span><span class="sxs-lookup"><span data-stu-id="d630e-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="d630e-149">Pode efetuar operações de gestão de cluster básico a partir do Visual Studio através do Explorador de nuvem, o que pode iniciar a partir de Olá **vista** menu.</span><span class="sxs-lookup"><span data-stu-id="d630e-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="d630e-150">Por exemplo, pode eliminar as aplicações e anular o aprovisionamento de tipos de aplicações em clusters locais ou remotos.</span><span class="sxs-lookup"><span data-stu-id="d630e-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Remover uma aplicação][removeapplication]

> [!TIP]
> <span data-ttu-id="d630e-152">Para mais rica funcionalidades de gestão de cluster, consulte [visualizar o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d630e-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d630e-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d630e-153">Next steps</span></span>
* [<span data-ttu-id="d630e-154">Modelo de aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d630e-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="d630e-155">Implementação de aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d630e-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="d630e-156">Gerir aplicações parâmetros para vários ambientes</span><span class="sxs-lookup"><span data-stu-id="d630e-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="d630e-157">Depurar a aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d630e-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="d630e-158">Visualizar o cluster utilizando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="d630e-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png