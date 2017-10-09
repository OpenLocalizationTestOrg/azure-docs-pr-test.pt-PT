---
title: aaaNever arquivo de dados confidenciais em imagens personalizadas para o Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as diretrizes de Olá para armazenar dados no imagens personalizadas no Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="85343-103">Nunca armazenar dados confidenciais em imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="85343-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="85343-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="85343-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="85343-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="85343-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="85343-106">Ao alojar a sua própria aplicação no Azure RemoteApp, o primeiro passo de Olá é toocreate uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="85343-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="85343-107">Utilizamos que instâncias VM de toocreate imagem personalizada servem as suas aplicações tooyour utilizadores.</span><span class="sxs-lookup"><span data-stu-id="85343-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="85343-108">imagem personalizada Olá deve conter apenas aplicações e dados nunca confidenciais que podem ser perdidos, tais como bases de dados do SQL Server, ficheiros de técnicos ou ficheiros de dados especiais, como ficheiros do QuickBooks da empresa.</span><span class="sxs-lookup"><span data-stu-id="85343-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="85343-109">Todos os dados confidenciais devem residir externo tooAzure RemoteApp num servidor de ficheiros, outra VM do Azure, ou no SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="85343-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="85343-110">imagem de Olá deve apenas Olá aplicação anfitriã que se liga a origem de dados de toohello e apresenta dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="85343-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="85343-111">Reveja [requisitos para o Azure RemoteApp imagens](remoteapp-imagereqs.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="85343-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="85343-112">toounderstand por que motivo não deve armazenar dados confidenciais, tem de toounderstand como funciona o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="85343-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="85343-113">Quando uma coleção é criada ou atualizada, em segundo plano de Olá vários clones ou cópias da imagem de Olá são criadas.</span><span class="sxs-lookup"><span data-stu-id="85343-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="85343-114">Todas as instâncias de VM são réplicas exatas de imagem personalizada Olá; Quando os utilizadores iniciarem aplicações estão ligado tooone destas instâncias VM.</span><span class="sxs-lookup"><span data-stu-id="85343-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="85343-115">Mas hello mesma instância não é garantida e deve importa porque são não persistentes.</span><span class="sxs-lookup"><span data-stu-id="85343-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="85343-116">Olá, instâncias de VM alojamento Olá aplicações são não persistentes e podem ser destruída ou eliminada com base, por exemplo, durante a atualização da coleção.</span><span class="sxs-lookup"><span data-stu-id="85343-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="85343-117">Depois de coleção de Olá está aprovisionada e os utilizadores iniciam a ligação toohello VMs, dados de utilizador são persistentes e protegidos porque é guardado em armazenamento separado dentro de uma imagem VHD que chamamos um [disco de perfil de utilizador (UDP)](remoteapp-upd.md), que é que o perfil de utilizador Olá no c:\users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="85343-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="85343-118">Quando uma aplicação é iniciado, Olá UPD está montado e tratada, tal como um perfil de utilizador local pelo sistema de operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="85343-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="85343-119">Leia mais sobre como [Azure RemoteApp guarda os dados de utilizador e definições](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="85343-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="85343-120">Dados de exemplo que não devem residir na imagem de Olá:</span><span class="sxs-lookup"><span data-stu-id="85343-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="85343-121">Dados partilhada para os utilizadores tooaccess</span><span class="sxs-lookup"><span data-stu-id="85343-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="85343-122">BD do SQL ou base de dados de QuickBooks</span><span class="sxs-lookup"><span data-stu-id="85343-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="85343-123">Todos os dados em D:\\</span><span class="sxs-lookup"><span data-stu-id="85343-123">Any data in D:\\</span></span>

<span data-ttu-id="85343-124">Dados de exemplo que podem residir em Olá predefinido perfil toobe copiado para UPD todos os utilizadores:</span><span class="sxs-lookup"><span data-stu-id="85343-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="85343-125">Ficheiros de configuração por utilizador</span><span class="sxs-lookup"><span data-stu-id="85343-125">Configuration files per user</span></span>
* <span data-ttu-id="85343-126">Scripts que os utilizadores teriam preservados na respetiva UPD</span><span class="sxs-lookup"><span data-stu-id="85343-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="85343-127">Pontos de chave:</span><span class="sxs-lookup"><span data-stu-id="85343-127">Key points:</span></span>

* <span data-ttu-id="85343-128">Nunca armazene dados confidenciais que podem ser perdidos no imagem Olá ao criar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="85343-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="85343-129">Os dados confidenciais deve sempre residem num servidor de ficheiros separado, separe VM do Azure, na nuvem de Olá e instâncias de VM toohello externo sempre que aloja as suas aplicações no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="85343-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="85343-130">Dados de utilizador são guardados e persistir no disco de perfil de utilizador de Olá (UDP)</span><span class="sxs-lookup"><span data-stu-id="85343-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

