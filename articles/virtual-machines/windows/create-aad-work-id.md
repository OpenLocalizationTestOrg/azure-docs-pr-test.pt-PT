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
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a>Criar uma identidade de empresa ou escola no Azure Active Directory toouse com VMs do Windows
Se criou uma conta do Azure pessoal ou ter uma subscrição do MSDN pessoal e criado Olá conta do Azure tootake partido créditos do MSDN Azure Olá – utilizou um *conta Microsoft* identidade toocreate-lo. Muitas funcionalidades excelentes do Azure – [os modelos de grupo de recursos](../../azure-resource-manager/resource-group-overview.md) é um exemplo - precisam de uma conta escolar ou profissional (uma identidade gerida pelo Azure Active Directory) toowork. Pode seguir Olá as instruções abaixo toocreate que uma nova empresa ou escola conta porque Felizmente, é uma das ações de melhor Olá sobre a sua conta do Azure pessoal que são provenientes com um domínio do Azure Active Directory predefinidas que pode utilizar toocreate uma nova empresa ou escola conta que pode utilizar com as funcionalidades do Azure que o requerem.

No entanto, as alterações recentes tornam possível toomanage sua subscrição com qualquer tipo de conta do Azure utilizando Olá `azure login` método de início de sessão interativo descrito [aqui](../../xplat-cli-connect.md). Pode utilizar essa mecanismo ou, pode seguir as instruções de Olá que se seguem. Também pode [criar uma identidade profissionais ou escolar no Azure Active Directory toouse com VMs com Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

