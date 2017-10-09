---
title: "aaaMigrate uma rede virtual do Azure (clássica) de uma região do grupo de afinidade tooa | Microsoft Docs"
description: "Saiba como uma rede virtual (clássica) de uma afinidade de toomigrate grupo tooa região."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Migrar uma rede virtual (clássica) a partir de uma região de tooa do grupo de afinidade

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que implementações mais novas utilizem o modelo de implementação do Resource Manager Olá.

Grupos de afinidades Certifique-se de que os recursos criados no Olá mesmo grupo de afinidade fisicamente alojadas por servidores que estão fechar em conjunto, permitindo toocommunicate estes recursos mais rápida. No passado, Olá, grupos de afinidade eram um requisito para criar redes virtuais (clássicas). Nessa altura, o serviço do Gestor de rede Olá que geridos redes virtuais (clássicas) só pode funcionar dentro de um conjunto de servidores físicos ou unidade de escala. Melhoramentos da arquitetura aumentou âmbito Olá da região de tooa de gestão de rede.

Como resultado estas melhorias da arquitetura, grupos de afinidades já não são recomendados, ou necessários para as redes virtuais (clássicas). utilização de Olá de grupos de afinidade para redes virtuais (clássicas) é substituída pela regiões. Redes virtuais (clássica) que estão associados a regiões são denominadas redes virtuais regionais.

Recomendamos que não utilize grupos de afinidade em geral. Para além do requisito de rede virtual Olá, grupos de afinidades também estavam toouse importante tooensure recursos, tais como a computação (clássica) e armazenamento (clássica), foram colocadas perto de si. No entanto, com a arquitetura de rede do Azure atual Olá, estes requisitos de posicionamento são já não são necessários.

> [!IMPORTANT]
> Embora seja tecnicamente possível toocreate uma rede virtual que está associada um grupo de afinidade, não há nenhum toodo razão apelativa para. Muitas funcionalidades de rede virtual, tais como grupos de segurança de rede, só estão disponíveis ao utilizar uma rede virtual regional e não estão disponíveis para as redes virtuais que estão associados a grupos de afinidades.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Editar o ficheiro de configuração de rede Olá

1. Exporte ficheiro de configuração de rede de Olá. toolearn como tooexport uma configuração de rede através do PowerShell de ficheiros ou Olá interface de linha de comandos do Azure (CLI) 1.0, consulte [configurar uma rede virtual com um ficheiro de configuração de rede](virtual-networks-using-network-configuration-file.md#export).
2. Editar o ficheiro de configuração de rede Olá, substituindo **AffinityGroup** com **localização**. Especifique um Azure [região](https://azure.microsoft.com/regions) para **localização**.
   
   > [!NOTE]
   > Olá **localização** Olá região que especificou para o grupo de afinidade de Olá que está associado a sua rede virtual (clássica). Por exemplo, se a rede virtual (clássica) está associada um grupo de afinidade que está localizado em EUA oeste, ao migrar, o **localização** tem de apontar tooWest E.U.A.. 
   > 
   > 
   
    Edite Olá seguintes linhas no ficheiro de configuração de rede, substituindo os valores de Olá com os seus próprios: 
   
    **Valor antigo:** \<VirtualNetworkSitename = AffinityGroup "VNetUSWest" = "VNetDemoAG"\> 
   
    **Valor novo:** \<VirtualNetworkSitename = "VNetUSWest" localização "EUA Oeste" de =\>
3. Guardar as alterações e [importar](virtual-networks-using-network-configuration-file.md#import) Olá tooAzure de configuração de rede.

> [!NOTE]
> Esta migração não irá causar qualquer período de inatividade tooyour serviços.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Que toodo se tiver uma VM (clássica) num grupo de afinidade
VMs (clássica) que estão atualmente a ser um grupo de afinidade não é necessário toobe removido do grupo de afinidade de Olá. Depois de uma VM for implementada, é a unidade de escala único tooa implementado. Grupos de afinidades pode restringir o conjunto de Olá de tamanhos VM disponíveis para uma nova implementação de VM, mas qualquer VM existente que é implementada já está restringida toohello conjunto da VM tamanhos disponíveis na unidade de escala Olá que Olá VM é implementada. Porque Olá que VM já se encontra implementada tooa unidade de escala, remover uma VM a partir de um grupo de afinidade não tem efeito em Olá VM.
