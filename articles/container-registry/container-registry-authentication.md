---
title: aaaAuthenticate com um registo de contentor do Azure | Microsoft Docs
description: Como toolog no registo de contentor do Azure tooan utilizando um Azure Active Directory service principal ou uma conta de administrador
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="67ee8-103">Autenticar com um registo de contentor do Docker privado</span><span class="sxs-lookup"><span data-stu-id="67ee8-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="67ee8-104">toowork com imagens do contentor num registo de contentor do Azure, inicie sessão com a Olá `docker login` comando.</span><span class="sxs-lookup"><span data-stu-id="67ee8-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="67ee8-105">Pode iniciar sessão utilizando um  **[principal de serviço do Azure Active Directory](../active-directory/active-directory-application-objects.md)**  específicas do registo ou **conta de administrador**.</span><span class="sxs-lookup"><span data-stu-id="67ee8-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="67ee8-106">Este artigo fornece mais detalhes sobre estas identidades.</span><span class="sxs-lookup"><span data-stu-id="67ee8-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="67ee8-107">Principal de serviço</span><span class="sxs-lookup"><span data-stu-id="67ee8-107">Service principal</span></span>

<span data-ttu-id="67ee8-108">Pode [atribuir um principal de serviço](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registo e utilizá-lo para a autenticação básica do Docker.</span><span class="sxs-lookup"><span data-stu-id="67ee8-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="67ee8-109">É recomendado utilizar um principal de serviço para a maioria dos cenários.</span><span class="sxs-lookup"><span data-stu-id="67ee8-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="67ee8-110">Forneça o ID da aplicação Olá e palavra-passe de toohello principal do serviço Olá `docker login` comando, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="67ee8-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="67ee8-111">Assim que a sessão iniciada, Docker coloca em cache as credenciais de Olá, por isso não terá de ID de aplicação do tooremember Olá.</span><span class="sxs-lookup"><span data-stu-id="67ee8-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="67ee8-112">Se quiser, pode voltar a gerar Olá palavra-passe de um principal de serviço, executando Olá `az ad sp reset-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="67ee8-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="67ee8-113">Permitem principais de serviço [acesso baseado em funções](../active-directory/role-based-access-control-configure.md) tooa registo.</span><span class="sxs-lookup"><span data-stu-id="67ee8-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="67ee8-114">Funções disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="67ee8-114">Available roles are:</span></span>
  * <span data-ttu-id="67ee8-115">Leitor (acesso só de solicitação).</span><span class="sxs-lookup"><span data-stu-id="67ee8-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="67ee8-116">Contribuidor (push e pull).</span><span class="sxs-lookup"><span data-stu-id="67ee8-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="67ee8-117">Proprietário (extração, push e atribuir funções tooother utilizadores).</span><span class="sxs-lookup"><span data-stu-id="67ee8-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="67ee8-118">Acesso anónimo não está disponível sobre os registos do contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ee8-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="67ee8-119">Pode utilizar imagens públicas [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="67ee8-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="67ee8-120">Pode atribuir vários principais de serviço tooa registo, que permite-lhe acesso toodefine para diferentes utilizadores ou aplicações.</span><span class="sxs-lookup"><span data-stu-id="67ee8-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="67ee8-121">Principais de serviço também ativar registo de tooa conectividade "sem interface" no programador ou cenários de DevOps como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ee8-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="67ee8-122">Implementações de contentores de sistemas de tooorchestration um registo, incluindo DC/OS, Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="67ee8-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="67ee8-123">Pode também solicitar toorelated de registos do contentor serviços do Azure, tal como [serviço de contentor](../container-service/index.yml), [do serviço de aplicações](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/)entre outros.</span><span class="sxs-lookup"><span data-stu-id="67ee8-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="67ee8-124">Contínuas integração e a implementação soluções (por exemplo, o Visual Studio Team Services ou Jenkins) que criar imagens de contentor e emiti-las tooa registo.</span><span class="sxs-lookup"><span data-stu-id="67ee8-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="67ee8-125">Conta de administrador</span><span class="sxs-lookup"><span data-stu-id="67ee8-125">Admin account</span></span>
<span data-ttu-id="67ee8-126">Com cada registo que criar, é criada automaticamente uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="67ee8-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="67ee8-127">Por predefinição está desativada conta Olá, mas pode ativá-la e gerir credenciais Olá, por exemplo através de Olá [portal](container-registry-get-started-portal.md#manage-registry-settings) ou utilizando Olá [comandos de Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="67ee8-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="67ee8-128">Cada conta de administrador é fornecida com duas palavras-passe, que podem ser novamente geradas.</span><span class="sxs-lookup"><span data-stu-id="67ee8-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="67ee8-129">duas palavras-passe Olá permitem-lhe registo do toomaintain ligações toohello utilizando uma palavra-passe enquanto volta a gerar Olá outra palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="67ee8-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="67ee8-130">Se a conta de Olá estiver ativada, pode passar de nome de utilizador de Olá e a palavra-passe toohello `docker login` comando para registo de toohello de autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="67ee8-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="67ee8-131">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="67ee8-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="67ee8-132">conta de administrador Olá foi concebida para um único utilizador tooaccess Olá de registo, principalmente para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="67ee8-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="67ee8-133">Não é recomendado tooshare credenciais de conta de administrador Olá entre os outros utilizadores.</span><span class="sxs-lookup"><span data-stu-id="67ee8-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="67ee8-134">Todos os utilizadores são apresentados como um registo de toohello de utilizador único.</span><span class="sxs-lookup"><span data-stu-id="67ee8-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="67ee8-135">Alterar ou desativar esta conta desativa o acesso de registo para todos os utilizadores que utilizam credenciais Olá.</span><span class="sxs-lookup"><span data-stu-id="67ee8-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="67ee8-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="67ee8-136">Next steps</span></span>
* <span data-ttu-id="67ee8-137">[Push imagem primeiro utilizar Olá CLI do Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="67ee8-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="67ee8-138">Para obter mais informações sobre a autenticação na pré-visualização de registo do contentor de Olá, consulte Olá [blogue](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="67ee8-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
