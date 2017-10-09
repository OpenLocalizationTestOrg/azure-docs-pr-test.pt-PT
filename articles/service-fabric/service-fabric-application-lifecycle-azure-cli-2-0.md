---
title: "aplicações do Azure Service Fabric aaaManage a utilizar o Azure CLI 2.0"
description: "Saiba como toodeploy e remover aplicações a partir de um Azure Service Fabric cluster utilizando o Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="975db-103">Gerir uma aplicação de Service Fabric do Azure utilizando o Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="975db-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="975db-104">Saiba como toocreate e eliminar aplicações em execução num cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="975db-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="975db-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="975db-105">Prerequisites</span></span>

* <span data-ttu-id="975db-106">Instale a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="975db-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="975db-107">Em seguida, selecione o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="975db-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="975db-108">Para obter mais informações, consulte [introdução ao Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="975db-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="975db-109">Ter uma Service Fabric aplicação pacote pronto toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="975db-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="975db-110">Para obter mais informações sobre como tooauthor e pacote de aplicação, leia sobre Olá [modelo de aplicação de Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="975db-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="975db-111">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="975db-111">Overview</span></span>

<span data-ttu-id="975db-112">toodeploy uma nova aplicação, conclua estes passos:</span><span class="sxs-lookup"><span data-stu-id="975db-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="975db-113">Carregar um arquivo de imagem de Service Fabric de toohello de pacote de aplicação.</span><span class="sxs-lookup"><span data-stu-id="975db-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="975db-114">Aprovisione um tipo de aplicação.</span><span class="sxs-lookup"><span data-stu-id="975db-114">Provision an application type.</span></span>
3. <span data-ttu-id="975db-115">Especificar e criar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="975db-115">Specify and create an application.</span></span>
4. <span data-ttu-id="975db-116">Especifique e criação de serviços.</span><span class="sxs-lookup"><span data-stu-id="975db-116">Specify and create services.</span></span>

<span data-ttu-id="975db-117">tooremove uma aplicação existente, conclua estes passos:</span><span class="sxs-lookup"><span data-stu-id="975db-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="975db-118">Elimine aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-118">Delete hello application.</span></span>
2. <span data-ttu-id="975db-119">Olá de não aprovisionamento associadas ao tipo de aplicação.</span><span class="sxs-lookup"><span data-stu-id="975db-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="975db-120">Elimine o conteúdo da loja Olá imagem.</span><span class="sxs-lookup"><span data-stu-id="975db-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="975db-121">Implementar uma nova aplicação</span><span class="sxs-lookup"><span data-stu-id="975db-121">Deploy a new application</span></span>

<span data-ttu-id="975db-122">toodeploy uma nova aplicação Olá concluída seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="975db-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="975db-123">Carregar um arquivo de imagens do toohello de pacote de aplicação nova</span><span class="sxs-lookup"><span data-stu-id="975db-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="975db-124">Antes de criar uma aplicação, carregue o arquivo de imagens de Service Fabric pacote toohello Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="975db-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="975db-125">Por exemplo, se o pacote de aplicação está a ser Olá `app_package_dir` diretório, Olá utilize os seguintes diretórios de Olá tooupload de comandos:</span><span class="sxs-lookup"><span data-stu-id="975db-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="975db-126">Para pacotes de aplicações grandes, pode especificar Olá `--show-progress` opção toodisplay progresso Olá carregamento Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="975db-127">Tipo de aplicação Olá aprovisionar</span><span class="sxs-lookup"><span data-stu-id="975db-127">Provision hello application type</span></span>

<span data-ttu-id="975db-128">Quando o carregamento de Olá estiver concluído, Aprovisione aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="975db-129">tooprovision Olá aplicação Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="975db-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="975db-130">Olá valor para `application-type-build-path` é Olá nome do diretório de olá onde o seu pacote de aplicação que carregou.</span><span class="sxs-lookup"><span data-stu-id="975db-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="975db-131">Criar uma aplicação a partir de um tipo de aplicação</span><span class="sxs-lookup"><span data-stu-id="975db-131">Create an application from an application type</span></span>

<span data-ttu-id="975db-132">Depois de aprovisionar aplicação Olá, utilize Olá tooname de comando a seguir e criar a sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="975db-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="975db-133">`app-name`é o nome de Olá que pretende que toouse para a instância da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="975db-134">Pode obter os parâmetros adicionais do manifesto de aplicação aprovisionados anteriormente Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="975db-135">nome da aplicação Olá tem de começar com o prefixo de Olá `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="975db-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="975db-136">Criar serviços para a nova aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="975db-136">Create services for hello new application</span></span>

<span data-ttu-id="975db-137">Depois de criar uma aplicação, crie serviços da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="975db-138">No seguinte exemplo de Olá, vamos criar um novo serviço sem monitorização de estado da nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="975db-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="975db-139">Serviços de Olá que pode criar a partir de uma aplicação estão definidos num manifesto de serviço no pacote de aplicação aprovisionados anteriormente Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="975db-140">Verifique o estado de funcionamento e implementação de aplicação</span><span class="sxs-lookup"><span data-stu-id="975db-140">Verify application deployment and health</span></span>

<span data-ttu-id="975db-141">tooverify que uma aplicação e do serviço foram implementados com êxito, verifique se estão listados Olá aplicação e do serviço:</span><span class="sxs-lookup"><span data-stu-id="975db-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="975db-142">tooverify que o serviço de Olá está em bom estado, utilize semelhante comandos tooretrieve Olá estado de funcionamento do serviço de Olá e aplicação Olá:</span><span class="sxs-lookup"><span data-stu-id="975db-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="975db-143">Bom estado de funcionamento dos serviços e aplicações têm um `HealthState` valor `Ok`.</span><span class="sxs-lookup"><span data-stu-id="975db-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="975db-144">Remover uma aplicação existente</span><span class="sxs-lookup"><span data-stu-id="975db-144">Remove an existing application</span></span>

<span data-ttu-id="975db-145">tooremove uma aplicação completa Olá seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="975db-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="975db-146">Eliminar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="975db-146">Delete hello application</span></span>

<span data-ttu-id="975db-147">toodelete Olá aplicação Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="975db-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="975db-148">Anular o aprovisionamento de tipo de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="975db-148">Unprovision hello application type</span></span>

<span data-ttu-id="975db-149">Depois de eliminar aplicação Olá, pode anular o aprovisionamento de tipo de aplicação Olá se já não precisar dele.</span><span class="sxs-lookup"><span data-stu-id="975db-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="975db-150">tipo de aplicação Olá toounprovision, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="975db-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="975db-151">versão de nome e tipo do tipo de Olá tem de corresponder ao nome de Olá e a versão no manifesto de aplicação aprovisionados anteriormente Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="975db-152">Eliminar o pacote de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="975db-152">Delete hello application package</span></span>

<span data-ttu-id="975db-153">Depois de ter anulou o aprovisionamento tipo de aplicação Olá, pode eliminar o pacote de aplicação Olá Olá do arquivo de imagens se já não precisar dele.</span><span class="sxs-lookup"><span data-stu-id="975db-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="975db-154">Eliminação de pacotes de aplicações ajuda-o reclamar espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="975db-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="975db-155">pacote de aplicação do Olá toodelete Olá do arquivo de imagens, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="975db-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="975db-156">`content-path`deve ser Olá nome do diretório de Olá que carregou quando criou a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="975db-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="975db-157">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="975db-157">Related articles</span></span>

* [<span data-ttu-id="975db-158">Introdução ao Service Fabric e à CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="975db-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* <span data-ttu-id="975db-159">[Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Introdução ao XPlat CLI do Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="975db-159">[Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
