---
title: aaaSecure a Internet das coisas (IoT) no Azure | Microsoft Docs
description: " Azure internet dos serviços de coisas (IoT) oferecem uma vasta gama de capacidades. Este artigo ajuda-o a compreender como toosecure suas soluções de IoT no Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="e1373-104">Descrição geral de segurança da Internet das coisas</span><span class="sxs-lookup"><span data-stu-id="e1373-104">Internet of Things security overview</span></span>
<span data-ttu-id="e1373-105">Azure internet dos serviços de coisas (IoT) oferecem uma vasta gama de capacidades.</span><span class="sxs-lookup"><span data-stu-id="e1373-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="e1373-106">Estes serviços de nível empresarial permitem-lhe:</span><span class="sxs-lookup"><span data-stu-id="e1373-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="e1373-107">Recolher dados de dispositivos</span><span class="sxs-lookup"><span data-stu-id="e1373-107">Collect data from devices</span></span>
* <span data-ttu-id="e1373-108">Analisar fluxos de dados em movimento</span><span class="sxs-lookup"><span data-stu-id="e1373-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="e1373-109">Armazenar e consultar grandes conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="e1373-109">Store and query large data sets</span></span>
* <span data-ttu-id="e1373-110">Visualizar dados em tempo real e dados históricos</span><span class="sxs-lookup"><span data-stu-id="e1373-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="e1373-111">Integrar com sistemas de back-office</span><span class="sxs-lookup"><span data-stu-id="e1373-111">Integrate with back-office systems</span></span>

<span data-ttu-id="e1373-112">toodeliver estas capacidades, o Azure IoT Suite reúne vários Azure serviços com extensões personalizadas, como soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="e1373-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="e1373-113">Estas soluções pré-configuradas são implementações de base de padrões de solução IoT comuns que o ajudam a hora de Olá tooreduce que demorar toodeliver suas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="e1373-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="e1373-114">Utilizar kits de desenvolvimento de software de IoT Olá, pode personalizar e expandir estas soluções toomeet os seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="e1373-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="e1373-115">Também pode utilizar estas soluções como exemplos ou modelos quando estiver a desenvolver novas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="e1373-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="e1373-116">Olá IoT do Azure suite é uma solução poderosa para as suas necessidades de IoT.</span><span class="sxs-lookup"><span data-stu-id="e1373-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="e1373-117">No entanto, é importância upmost que as suas soluções de IoT concebidas com segurança em mente desde o início de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1373-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="e1373-118">Devido a Olá sheer número de dispositivos de IoT qualquer incidente de segurança pode tornar rapidamente um evento ampla com consequências significativas.</span><span class="sxs-lookup"><span data-stu-id="e1373-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="e1373-119">toohelp que compreende como toosecure suas soluções de IoT, temos Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="e1373-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="e1373-120">Arquitetura de segurança</span><span class="sxs-lookup"><span data-stu-id="e1373-120">Security architecture</span></span>
<span data-ttu-id="e1373-121">Ao conceber um sistema, é importante toounderstand Olá ameaças toothat sistema e adicionar defesas adequadas em conformidade, como sistema de Olá é concebido e criado de.</span><span class="sxs-lookup"><span data-stu-id="e1373-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="e1373-122">É importante toodesign Olá produto Olá início com segurança em mente, porque a compreender como um atacante poderá ser capaz de toocompromise um sistema de ajuda Certifique-se mitigações adequadas estão no local a partir do início de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1373-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="e1373-123">Pode saber mais sobre a arquitetura de segurança de IoT através da leitura [Internet das coisas segurança arquitetura](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="e1373-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="e1373-124">Este artigo aborda Olá os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="e1373-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="e1373-125">Segurança começa com um modelo de ameaça</span><span class="sxs-lookup"><span data-stu-id="e1373-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="e1373-126">Segurança de IoT</span><span class="sxs-lookup"><span data-stu-id="e1373-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="e1373-127">Olá de modelação de ameaça arquitetura de referência do IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="e1373-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="e1373-128">Segurança de Olá fundo cópias de segurança</span><span class="sxs-lookup"><span data-stu-id="e1373-128">Security from hello ground up</span></span>
<span data-ttu-id="e1373-129">Olá IoT pode representar um único segurança, privacidade e conformidade desafios toobusinesses em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="e1373-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="e1373-130">Ao contrário de tecnologia de informático tradicional onde estes problemas está centrada no software e como é implementado, o IoT seja relativo o que acontece quando Olá informático e universos físico Olá convergir.</span><span class="sxs-lookup"><span data-stu-id="e1373-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="e1373-131">Proteger soluções de IoT requer garantir segura de aprovisionamento de dispositivos, conectividade segura entre estes dispositivos e a nuvem de Olá e a proteção de proteger os dados na nuvem de Olá durante o processamento e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e1373-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="e1373-132">Trabalhar com essas funcionalidades, no entanto, são dispositivos restrita de recursos, distribuição geográfica dos implementações e muitos dispositivos dentro de uma solução.</span><span class="sxs-lookup"><span data-stu-id="e1373-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="e1373-133">Pode saber como segurança toohandle nas seguintes áreas lendo [segurança da Internet das coisas de Olá fundo](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="e1373-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="e1373-134">artigo de Olá aborda Olá os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="e1373-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="e1373-135">Proteger a infraestrutura de Olá fundo cópias de segurança</span><span class="sxs-lookup"><span data-stu-id="e1373-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="e1373-136">Microsoft Azure – segura IoT infraestrutura para a sua empresa</span><span class="sxs-lookup"><span data-stu-id="e1373-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="e1373-137">Melhores práticas</span><span class="sxs-lookup"><span data-stu-id="e1373-137">Best Practices</span></span>
<span data-ttu-id="e1373-138">Proteger uma infraestrutura de IoT requer uma estratégia de segurança-na profundidade rigorosas.</span><span class="sxs-lookup"><span data-stu-id="e1373-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="e1373-139">De proteger dados numa nuvem Olá, proteger a integridade dos dados enquanto em trânsito através de Olá internet pública, dispositivos de aprovisionamento de toosecurely, cada camada baseia-se maior garantia de segurança Olá infraestrutura global.</span><span class="sxs-lookup"><span data-stu-id="e1373-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="e1373-140">Pode saber sobre a segurança da Internet das coisas melhores práticas através da leitura [práticas recomendadas de segurança de Internet das coisas](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="e1373-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="e1373-141">artigo de Olá aborda Olá os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="e1373-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="e1373-142">Fabricante de hardware de IoT/integrador</span><span class="sxs-lookup"><span data-stu-id="e1373-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="e1373-143">Para programadores de solução IoT</span><span class="sxs-lookup"><span data-stu-id="e1373-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="e1373-144">Implementador de solução IoT</span><span class="sxs-lookup"><span data-stu-id="e1373-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="e1373-145">Operador de solução IoT</span><span class="sxs-lookup"><span data-stu-id="e1373-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
