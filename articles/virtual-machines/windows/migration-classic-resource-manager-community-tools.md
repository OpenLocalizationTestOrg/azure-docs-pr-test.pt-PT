---
title: "ferramentas de aaaCommunity - mover recursos clássicos tooAzure Resource Manager | Microsoft Docs"
description: "Este artigo catálogos Olá ferramentas tem sido fornecidas pelo Olá Comunidade toohelp migre recursos IaaS do modelo de implementação Azure Resource Manager toohello clássico."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>Comunidade ferramentas toomigrate IaaS recursos do Gestor de recursos de tooAzure clássico
Este artigo catálogos Olá ferramentas que foram fornecidos pelo Olá Comunidade tooassist com a migração de recursos IaaS do modelo de implementação Azure Resource Manager toohello clássico.

> [!NOTE]
> Estas ferramentas não são suportadas oficialmente por Support da Microsoft. Por conseguinte, estão abertos obtido no GitHub e estamos tooaccept satisfeito PRs para correções ou cenários adicionais. tooreport um problema, utilize Olá GitHub emite funcionalidade.
> 
> Migrar com estas ferramentas irá causar período de indisponibilidade para a Máquina Virtual clássica. Se estiver à procura de migração de plataforma suportada, visite 
> 
>   * [Migração de plataforma suportada dos recursos IaaS da pilha do clássico tooAzure Resource Manager](migration-classic-resource-manager-overview.md)
>   * [Técnica detalhada da plataforma suportada a migração de clássico tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md)
>   * [Migrar os recursos IaaS de clássico tooAzure Gestor de recursos com o Azure PowerShell](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
Esta é uma coleção de ferramentas de programa auxiliar criada como parte da empresa as migrações do tooAzure de gestão de serviço do Azure Resource Manager. Esta ferramenta permite-lhe tooreplicate a infraestrutura para outra subscrição que pode ser utilizada para fins de teste de migração e iron eventuais problemas antes de executar a migração de Olá na sua subscrição de produção.

[Documentação da ferramenta de ligação toohello](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz é uma opção adicional de toomigrate um conjunto completo de recursos do Resource Manager IaaS de tooAzure de recursos do clássicos IaaS. Olá migração pode ocorrer em Olá mesma subscrição ou entre subscrições e tipos de subscrição (ex: subscrições de CSP).

[Documentação da ferramenta de ligação toohello](https://github.com/Azure/migAz)

## <a name="next-steps"></a>Passos Seguintes

* [Descrição geral da migração de plataforma suportada dos recursos IaaS do clássico tooAzure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Técnica detalhada da plataforma suportada a migração do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planeamento da migração de recursos IaaS do clássico tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utilizar o PowerShell toomigrate IaaS recursos do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utilizar recursos de IaaS toomigrate CLI do clássico tooAzure Resource Manager](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Consultar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Olá revisão mais perguntas mais frequentes sobre a migração de IaaS de recursos do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

