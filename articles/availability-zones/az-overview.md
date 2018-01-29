---
title: "Descrição geral da disponibilidade zonas | Microsoft Docs"
description: "Este artigo fornece uma descrição geral das zonas de disponibilidade no Azure."
services: 
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
tags: 
ms.assetid: 
ms.service: azure
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2017
ms.author: markgal
ms.custom: mvc I am an ITPro and application developer, and I want to protect (use Availability Zones) my applications and data against data center failure (to build Highly Available applications).
ms.openlocfilehash: a0e654637bc4aca4230c56cc7c1706f5cd73622e
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2018
---
# <a name="overview-of-availability-zones-in-azure-preview"></a>Descrição geral das zonas de disponibilidade no Azure (pré-visualização)

Zonas de disponibilidade ajudar a protegê-lo contra falhas de nível de centro de dados. Onde estão localizados dentro de uma região do Azure e cada um tem a suas próprias independente de origem, rede e arrefecimento de energia. Para garantir a resiliência, há um mínimo de três zonas separadas em todas as regiões ativadas. A separação física e lógica das zonas de disponibilidade numa região protege a aplicações e dados de falhas de nível de zona. 

![Vista concetual de uma zona ficar numa região](./media/az-overview/az-graphic-two.png)

## <a name="regions-that-support-availability-zones"></a>Regiões que suportam zonas de disponibilidade

- EUA Leste 2
- Centro dos EUA
- Europa Ocidental
- Centro de França

## <a name="services-that-support-availability-zones"></a>Serviços que suportam zonas de disponibilidade

Os serviços do Azure que suportam zonas de disponibilidade são:

- Máquinas Virtuais do Linux
- Máquinas Virtuais do Windows
- Conjuntos de Dimensionamento de Máquinas Virtuais
- Managed Disks
- Load balancer
- Endereço IP público
- Armazenamento com redundância de zona

## <a name="get-started-with-the-availability-zones-preview"></a>Começar com a pré-visualização de zonas de disponibilidade

A pré-visualização de zonas de disponibilidade está disponível nos EUA Leste 2, Central dos EUA, Europa Ocidental e regiões França Central para serviços específicos do Azure. 

1. [Inscrever-se para as zonas de disponibilidade de pré-visualização](http://aka.ms/azenroll). 
2. Inicie sessão sua subscrição do Azure.
3. Escolha uma região que suporte zonas de disponibilidade.
4. Utilize uma das ligações seguintes para começar a utilizar zonas disponibilidade com o serviço. 
    - [Criar uma máquina virtual](../virtual-machines/windows/create-portal-availability-zone.md)
    - [Criar um conjunto de dimensionamento de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-use-availability-zones.md)
    - [Adicionar um disco gerido com o PowerShell](../virtual-machines/windows/attach-disk-ps.md#add-an-empty-data-disk-to-a-virtual-machine)
    - [Balanceador de carga](../load-balancer/load-balancer-standard-overview.md)

## <a name="next-steps"></a>Passos Seguintes
- [Modelos de início rápido](http://aka.ms/azqs)
