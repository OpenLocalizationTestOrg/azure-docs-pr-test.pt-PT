---
title: aaaCreate uma identidade de conta escolar ou profissional do AAD para Windows | Microsoft Docs
description: "Saiba como toocreate uma identidade profissionais ou escolar no Azure Active Directory toouse com as máquinas virtuais do Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: dd6e2381fd0aa503483aa786b36232e557729c4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a><span data-ttu-id="c65eb-103">Criar uma identidade de empresa ou escola no Azure Active Directory toouse com VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="c65eb-103">Creating a Work or School identity in Azure Active Directory toouse with Windows VMs</span></span>
<span data-ttu-id="c65eb-104">Se criou uma conta do Azure pessoal ou ter uma subscrição do MSDN pessoal e criado Olá conta do Azure tootake partido créditos do MSDN Azure Olá – utilizou um *conta Microsoft* identidade toocreate-lo.</span><span class="sxs-lookup"><span data-stu-id="c65eb-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="c65eb-105">Muitas funcionalidades excelentes do Azure – [os modelos de grupo de recursos](../../azure-resource-manager/resource-group-overview.md) é um exemplo - precisam de uma conta escolar ou profissional (uma identidade gerida pelo Azure Active Directory) toowork.</span><span class="sxs-lookup"><span data-stu-id="c65eb-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="c65eb-106">Pode seguir Olá as instruções abaixo toocreate que uma nova empresa ou escola conta porque Felizmente, é uma das ações de melhor Olá sobre a sua conta do Azure pessoal que são provenientes com um domínio do Azure Active Directory predefinidas que pode utilizar toocreate uma nova empresa ou escola conta que pode utilizar com as funcionalidades do Azure que o requerem.</span><span class="sxs-lookup"><span data-stu-id="c65eb-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="c65eb-107">No entanto, as alterações recentes tornam possível toomanage sua subscrição com qualquer tipo de conta do Azure utilizando Olá `azure login` método de início de sessão interativo descrito [aqui](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c65eb-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="c65eb-108">Pode utilizar essa mecanismo ou, pode seguir as instruções de Olá que se seguem.</span><span class="sxs-lookup"><span data-stu-id="c65eb-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="c65eb-109">Também pode [criar uma identidade profissionais ou escolar no Azure Active Directory toouse com VMs com Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c65eb-109">You can also [create a work or school identity in Azure Active Directory toouse with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

