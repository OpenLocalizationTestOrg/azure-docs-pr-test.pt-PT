---
title: "aaaUsing SAP em máquinas virtuais do Linux | Microsoft Docs"
description: "Aprenda a utilizar o SAP nas máquinas virtuais do Linux (VMs) | Microsoft Azure"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="abe87-103">Utilizando o SAP em máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="abe87-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="abe87-104">É um termo bastante utilizado que é obtenham mais importância dentro Olá da indústria IT, de pequenas empresas segurança toolarge e multinational as empresas têm a informática em nuvem.</span><span class="sxs-lookup"><span data-stu-id="abe87-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="abe87-105">Microsoft Azure é Olá plataforma de serviços em nuvem da Microsoft que oferece um largo espetro de possibilidades de novo.</span><span class="sxs-lookup"><span data-stu-id="abe87-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="abe87-106">Agora os clientes são toorapidly capaz de aprovisionar e aprovisionar desativação aplicações como serviços em nuvem, pelo que não são limitado tootechnical ou budgeting restrições.</span><span class="sxs-lookup"><span data-stu-id="abe87-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="abe87-107">Em vez de investir tempo e orçamento na infraestrutura de hardware, as empresas podem concentrar-se na aplicação Olá, os processos de negócios e suas vantagens para os clientes e utilizadores.</span><span class="sxs-lookup"><span data-stu-id="abe87-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="abe87-108">Com as máquinas virtuais do Microsoft Azure, a Microsoft oferece uma infraestrutura completa como uma plataforma de serviço (IaaS).</span><span class="sxs-lookup"><span data-stu-id="abe87-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="abe87-109">As aplicações baseadas em SAP NetWeaver são suportadas em Máquinas Virtuais do Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="abe87-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="abe87-110">documentos técnicos Olá abaixo descrevem como tooplan e implementar SAP NetWeaver com base em aplicações em máquinas virtuais do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="abe87-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="abe87-111">Também pode implementar aplicações de NetWeaver SAP com base em [máquinas virtuais Windows](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abe87-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="abe87-112">SAP NetWeaver em máquinas de virtuais do Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="abe87-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="abe87-113">Título: aaaTesting SAP NetWeaver em VMs do Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="abe87-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="abe87-114">Resumo: Não há nenhum oficial de suporte SAP para executar SAP NetWeaver em VMs do Linux do Azure, neste ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="abe87-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="abe87-115">Contudo, clientes aconselhável toodo alguns testes ou podem considerar toorun SAP demonstração ou formação sistemas em VMs do Linux do Azure, desde que não é necessário para contactar o suporte SAP.</span><span class="sxs-lookup"><span data-stu-id="abe87-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="abe87-116">Este artigo deverão ajudar a configurar as VMs do Azure SUSE Linux para executar o SAP e fornece algumas sugestões básicas ordem tooavoid pitfalls de potenciais comuns.</span><span class="sxs-lookup"><span data-stu-id="abe87-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="abe87-117">Atualizada: De Dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="abe87-117">Updated: December 2015</span></span>

[<span data-ttu-id="abe87-118">Este artigo pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="abe87-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

