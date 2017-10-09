---
title: "segurança aaaIntegrate as estruturas da arquitetura do Azure | Microsoft Docs"
description: " Este artigo ajuda-o a compreender a arquitetura de serviços e aplicações de Olá no Azure toomake-lo mais fácil toointegrate segurança para o design e implementação. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="872bc-103">Arquitetura de aplicações no Azure</span><span class="sxs-lookup"><span data-stu-id="872bc-103">Application architecture on Azure</span></span>
<span data-ttu-id="872bc-104">toohelp Proteja as soluções baseadas na nuvem no Microsoft Azure, uma forte foundation da arquitetura é fundamental.</span><span class="sxs-lookup"><span data-stu-id="872bc-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="872bc-105">Arquitetos de TI, designers e os implementadores beneficiam um conhecimento forte da arquitetura de serviços e aplicações.</span><span class="sxs-lookup"><span data-stu-id="872bc-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="872bc-106">Este conhecimento básico ajuda-o a compreender a todos os componentes de Olá das suas soluções baseado na nuvem e torna mais fácil toointegrate segurança em todos os aspetos da sua estrutura e implementação.</span><span class="sxs-lookup"><span data-stu-id="872bc-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="872bc-107">Podemos ter Olá seguintes toohelp, com os seus as investigações da arquitetura e estruturas:</span><span class="sxs-lookup"><span data-stu-id="872bc-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="872bc-108">Infographics da arquitetura</span><span class="sxs-lookup"><span data-stu-id="872bc-108">Architectural infographics</span></span>
* <span data-ttu-id="872bc-109">Esquemas da arquitetura</span><span class="sxs-lookup"><span data-stu-id="872bc-109">Architectural blueprints</span></span>
* <span data-ttu-id="872bc-110">Conjunto de símbolo de cloud e enterprise</span><span class="sxs-lookup"><span data-stu-id="872bc-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="872bc-111">Modelo de Visio 3D blueprint</span><span class="sxs-lookup"><span data-stu-id="872bc-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="872bc-112">Infographics da arquitetura</span><span class="sxs-lookup"><span data-stu-id="872bc-112">Architectural infographics</span></span>
<span data-ttu-id="872bc-113">A Microsoft publica relacionados da arquitetura várias cartazes infographics.</span><span class="sxs-lookup"><span data-stu-id="872bc-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="872bc-114">Estas definições incluem:</span><span class="sxs-lookup"><span data-stu-id="872bc-114">They include:</span></span>

* [<span data-ttu-id="872bc-115">Criar aplicações de nuvem do mundo Real</span><span class="sxs-lookup"><span data-stu-id="872bc-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="872bc-116">Dimensionamento com serviços em nuvem</span><span class="sxs-lookup"><span data-stu-id="872bc-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="872bc-117">Esquemas da arquitetura</span><span class="sxs-lookup"><span data-stu-id="872bc-117">Architectural blueprints</span></span>
<span data-ttu-id="872bc-118">A Microsoft publica um conjunto de alto nível [esquemas da arquitetura](http://aka.ms/azblueprints) que mostra como toobuild tipos específicos de sistemas com produtos Microsoft.</span><span class="sxs-lookup"><span data-stu-id="872bc-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="872bc-119">Cada blueprint inclui r:</span><span class="sxs-lookup"><span data-stu-id="872bc-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="872bc-120">Ficheiros baseado no Visio 2003 flat 2D que pode transferir e modificar</span><span class="sxs-lookup"><span data-stu-id="872bc-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="872bc-121">Perspetiva 3D colorful PDF ficheiro toointroduce Olá blueprint tooless técnico público</span><span class="sxs-lookup"><span data-stu-id="872bc-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="872bc-122">Vídeo que explica versão 3D Olá</span><span class="sxs-lookup"><span data-stu-id="872bc-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="872bc-123">Conjunto de símbolo de cloud e enterprise</span><span class="sxs-lookup"><span data-stu-id="872bc-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="872bc-124">[Ver Olá Visio e o vídeo de preparação de símbolos](http://aka.ms/CnESymbolsVideo) e, em seguida, [transferir o conjunto de nuvem e empresa símbolo Olá](http://aka.ms/CnESymbols) toohelp criar materiais técnicos que descrevem o Azure, Windows Server, SQL Server e muito mais.</span><span class="sxs-lookup"><span data-stu-id="872bc-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="872bc-125">Pode utilizar os símbolos de Olá nos diagramas de arquitetura, materiais de formação, apresentações, datasheets, infographics, documentos técnicos e documentação de terceiros, mesmo se Olá livro trains as pessoas toouse produtos da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="872bc-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="872bc-126">No entanto, não deveriam para utilização em interfaces de utilizador.</span><span class="sxs-lookup"><span data-stu-id="872bc-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="872bc-127">Modelo de Visio 3D blueprint</span><span class="sxs-lookup"><span data-stu-id="872bc-127">3D blueprint Visio template</span></span>
<span data-ttu-id="872bc-128">Olá 3D versões do Olá [esquemas de arquitetura Microsoft](http://aka.ms/azblueprints) inicialmente foram criados numa ferramenta de terceiros.</span><span class="sxs-lookup"><span data-stu-id="872bc-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="872bc-129">Um novo modelo de Visio 2013 (e versões posterior) vem incluído no 5 de Agosto de 2015 como parte de um [decorrer de certificação do Microsoft Architecture distribuído EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="872bc-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="872bc-130">modelo de Olá também está disponível fora Olá decorrer.</span><span class="sxs-lookup"><span data-stu-id="872bc-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="872bc-131">[Ver as vídeo de formação Olá](http://aka.ms/3dBlueprintTemplateVideo) primeiro para saber o que pode fazer</span><span class="sxs-lookup"><span data-stu-id="872bc-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="872bc-132">Transferir Olá [Microsoft modelo de Visio Blueprint 3d](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="872bc-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="872bc-133">Transferir Olá [Cloud e Enterprise símbolos](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse com modelo 3D Olá</span><span class="sxs-lookup"><span data-stu-id="872bc-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
