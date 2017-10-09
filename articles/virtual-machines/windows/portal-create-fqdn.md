---
title: aaaCreate FQDN para uma VM com o Windows hello portal do Azure | Microsoft Docs
description: "Saiba como toocreate um nome de domínio completamente qualificado, ou FQDN, para um Gestor de recursos com base em máquina virtual no Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Criar um nome de domínio completamente qualificado no Olá portal do Azure para uma VM do Windows

Quando cria uma máquina virtual (VM) no Olá [portal do Azure](https://portal.azure.com), um recurso IP público para a máquina virtual de Olá é criado automaticamente. Utilize este Olá de acesso de tooremotely de endereço IP VM. Embora o portal de Olá não cria um [nome de domínio completamente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou FQDN, pode criar um depois hello é criada a VM. Este artigo demonstra Olá passos toocreate um nome DNS ou o FQDN.

## <a name="create-a-fqdn"></a>Criar um FQDN
Este artigo pressupõe que já criou uma VM. Se necessário, pode [criar uma VM no portal de Olá](quick-create-portal.md) ou [com o Azure PowerShell](quick-create-powershell.md). Assim que a VM está a funcionar, siga estes passos:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Pode agora ligar remotamente toohello VM com este nome DNS, tal como para o protocolo de ambiente de trabalho remoto (RDP).

## <a name="next-steps"></a>Passos seguintes
Agora que a VM tem um nome IP e DNS público, pode implementar comuns das estruturas de aplicações ou serviços como o IIS, SQL Server ou SharePoint.

Também pode ler mais sobre [com o Resource Manager](../../azure-resource-manager/resource-group-overview.md) para sugestões sobre como criar as suas implementações do Azure.

