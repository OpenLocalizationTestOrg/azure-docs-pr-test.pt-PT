---
title: "aaaAzure Docker Compose pré-visualização do serviço de recursos de infraestrutura"
description: "Azure Service Fabric aceita o Docker Compose toomake de formato-contentores existente mais fácil do tooorchestrate, utilizando o Service Fabric. Este suporte está atualmente em pré-visualização."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="3666d-104">Suporte de aplicações do docker Compose no Service Fabric do Azure (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="3666d-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="3666d-105">Docker utiliza Olá [docker-Compose.yml](https://docs.docker.com/compose) ficheiro para definir o contentor várias aplicações.</span><span class="sxs-lookup"><span data-stu-id="3666d-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="3666d-106">toomake-lo mais fácil para os clientes familiarizados com o Docker tooorchestrate contentor as aplicações existentes no Azure Service Fabric, incluímos suporte de pré-visualização para o Docker Compose nativamente na plataforma de Olá.</span><span class="sxs-lookup"><span data-stu-id="3666d-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="3666d-107">Service Fabric pode aceitar a versão 3 e posterior do `docker-compose.yml` ficheiros.</span><span class="sxs-lookup"><span data-stu-id="3666d-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="3666d-108">Porque este suporte está em pré-visualização, apenas um subconjunto de diretivas de Compose é suportado.</span><span class="sxs-lookup"><span data-stu-id="3666d-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="3666d-109">Por exemplo, as atualizações de aplicações não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="3666d-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="3666d-110">No entanto, pode sempre remover e implementar aplicações em vez de atualização-los.</span><span class="sxs-lookup"><span data-stu-id="3666d-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="3666d-111">toouse esta pré-visualização, criar o cluster com a versão 5.7 ou superior do tempo de execução do Olá Service Fabric através de Olá portal do Azure, juntamente com Olá correspondente SDK.</span><span class="sxs-lookup"><span data-stu-id="3666d-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="3666d-112">Esta funcionalidade está em pré-visualização e não é suportada na produção.</span><span class="sxs-lookup"><span data-stu-id="3666d-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="3666d-113">Implementar um ficheiro de Docker Compose no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3666d-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="3666d-114">Olá os comandos seguintes criam uma aplicação de Service Fabric (com o nome `fabric:/TestContainerApp` no Olá anterior exemplo), que pode monitorizar e gerir como qualquer outra aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3666d-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="3666d-115">Pode utilizar o nome de aplicação especificada Olá para consultas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="3666d-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="3666d-116">Utilizar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3666d-116">Use PowerShell</span></span>

<span data-ttu-id="3666d-117">Crie uma aplicação de Service Fabric compor a partir de um ficheiro docker-Compose.yml executando o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="3666d-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="3666d-118">`RegistryUserName`e `RegistryPassword` Consulte nome de utilizador de registo de contentor de toohello e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="3666d-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="3666d-119">Após concluir aplicação Olá, pode verificar o estado utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3666d-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="3666d-120">toodelete Olá Compose aplicação através do PowerShell, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3666d-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="3666d-121">Utilizar a CLI do Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="3666d-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="3666d-122">Em alternativa, pode utilizar Olá os seguintes comandos da CLI de recursos de infraestrutura de serviço:</span><span class="sxs-lookup"><span data-stu-id="3666d-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="3666d-123">Depois de criar aplicação Olá, pode verificar o estado utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3666d-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="3666d-124">Olá toodelete Compose aplicação, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3666d-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="3666d-125">Diretivas de Compose suportadas</span><span class="sxs-lookup"><span data-stu-id="3666d-125">Supported Compose directives</span></span>

<span data-ttu-id="3666d-126">Esta pré-visualização suporta um subconjunto das opções de configuração de Olá Olá Compose versão 3 o formato, incluindo Olá primitivos os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3666d-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="3666d-127">Serviços > Implementar > réplicas</span><span class="sxs-lookup"><span data-stu-id="3666d-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="3666d-128">Serviços > Implementar > colocação > restrições</span><span class="sxs-lookup"><span data-stu-id="3666d-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="3666d-129">Serviços > Implementar > recursos > limites</span><span class="sxs-lookup"><span data-stu-id="3666d-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="3666d-130">-cpu partilhas</span><span class="sxs-lookup"><span data-stu-id="3666d-130">-cpu-shares</span></span>
    * <span data-ttu-id="3666d-131">-memória</span><span class="sxs-lookup"><span data-stu-id="3666d-131">-memory</span></span>
    * <span data-ttu-id="3666d-132">-memória-troca</span><span class="sxs-lookup"><span data-stu-id="3666d-132">-memory-swap</span></span>
* <span data-ttu-id="3666d-133">Serviços > comandos</span><span class="sxs-lookup"><span data-stu-id="3666d-133">Services > Commands</span></span>
* <span data-ttu-id="3666d-134">Serviços > ambiente</span><span class="sxs-lookup"><span data-stu-id="3666d-134">Services > Environment</span></span>
* <span data-ttu-id="3666d-135">Serviços > portas</span><span class="sxs-lookup"><span data-stu-id="3666d-135">Services > Ports</span></span>
* <span data-ttu-id="3666d-136">Serviços > imagem</span><span class="sxs-lookup"><span data-stu-id="3666d-136">Services > Image</span></span>
* <span data-ttu-id="3666d-137">Serviços > isolamento (apenas para o Windows)</span><span class="sxs-lookup"><span data-stu-id="3666d-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="3666d-138">Serviços > registo > controladores</span><span class="sxs-lookup"><span data-stu-id="3666d-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="3666d-139">Serviços > registo > controladores > Opções</span><span class="sxs-lookup"><span data-stu-id="3666d-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="3666d-140">Volume & implementar > Volume</span><span class="sxs-lookup"><span data-stu-id="3666d-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="3666d-141">Configurar o cluster Olá para impor limites de recursos, conforme descrito em [governação de recursos do Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3666d-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="3666d-142">Todos os outras diretivas Docker Compose não são suportadas para esta pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="3666d-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="3666d-143">Cálculo ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="3666d-143">ServiceDnsName computation</span></span>

<span data-ttu-id="3666d-144">Se o nome de serviço Olá que especificou num ficheiro Compose é um nome de domínio completamente qualificado (ou seja, contém um ponto [.]), o nome DNS Olá registado pelo Service Fabric é `<ServiceName>` (incluindo o ponto de Olá).</span><span class="sxs-lookup"><span data-stu-id="3666d-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="3666d-145">Caso contrário, cada segmento de caminho no nome da aplicação Olá torna-se uma etiqueta de domínio no nome de DNS do serviço Olá, com Olá primeiro segmento de caminho tornar-se a etiqueta de Olá de domínio de nível superior.</span><span class="sxs-lookup"><span data-stu-id="3666d-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="3666d-146">Por exemplo, se Olá especificado o nome da aplicação é `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` seria Olá nome DNS registado.</span><span class="sxs-lookup"><span data-stu-id="3666d-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="3666d-147">Diferenças entre Compose (definição de instância) e o modelo de aplicação de Service Fabric (definição de tipo)</span><span class="sxs-lookup"><span data-stu-id="3666d-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="3666d-148">Um ficheiro docker-Compose.yml descreve um conjunto implementável de contentores, incluindo as respetivas propriedades e configurações.</span><span class="sxs-lookup"><span data-stu-id="3666d-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="3666d-149">Por exemplo, o ficheiro de Olá pode conter variáveis de ambiente e portas.</span><span class="sxs-lookup"><span data-stu-id="3666d-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="3666d-150">Também pode especificar parâmetros de implementação, tais como restrições de posicionamento, limites de recursos e nomes DNS no ficheiro de docker-Compose.yml Olá.</span><span class="sxs-lookup"><span data-stu-id="3666d-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="3666d-151">Olá [modelo de aplicação de Service Fabric](service-fabric-application-model.md) Olá, utiliza tipos de serviço e tipos de aplicações, onde pode ter várias instâncias da aplicação do mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="3666d-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="3666d-152">Por exemplo, pode ter uma instância da aplicação por cliente.</span><span class="sxs-lookup"><span data-stu-id="3666d-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="3666d-153">Este modelo baseado no tipo suporta várias versões do Olá mesmo tipo de aplicação que está registado com Olá tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="3666d-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="3666d-154">Por exemplo, cliente um pode ter uma aplicação com instâncias com tipo 1.0 do AppTypeA e cliente B pode ter outra aplicação instanciada com Olá mesmo tipo e versão.</span><span class="sxs-lookup"><span data-stu-id="3666d-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="3666d-155">Definir os tipos de aplicação Olá em manifestos da aplicação Olá e especificar parâmetros de nome e a implementação da aplicação Olá quando criar aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="3666d-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="3666d-156">Embora este modelo oferece flexibilidade, iremos também estiver a planear toosupport um modelo de implementação mais simples, instância baseada em onde tipos são implícitos de ficheiro de manifesto Olá.</span><span class="sxs-lookup"><span data-stu-id="3666d-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="3666d-157">Neste modelo, cada aplicação obtém o seu próprio manifesto independente.</span><span class="sxs-lookup"><span data-stu-id="3666d-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="3666d-158">Iremos são pré-visualização deste esforço adicionando suporte para docker-Compose.yml, que é um formato de implementação com base na instância.</span><span class="sxs-lookup"><span data-stu-id="3666d-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3666d-159">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3666d-159">Next steps</span></span>

* <span data-ttu-id="3666d-160">Ler sobre Olá [modelo de aplicação de Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="3666d-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="3666d-161">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3666d-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
