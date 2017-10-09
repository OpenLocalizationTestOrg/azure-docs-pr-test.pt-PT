---
title: "aaaHow tooplan sua rede virtual para uma coleção do Azure RemoteApp | Microsoft Docs"
description: "Saiba como tooplan sua rede virtual para uma coleção do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Como tooplan a rede virtual para o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Este documento descreve como tooset segurança de rede virtual do Azure (VNET) e a sub-rede de Olá para o Azure RemoteApp. Se não estiver familiarizado com redes virtuais do Azure, esta é uma funcionalidade que ajuda a toovirtualize a sua rede infraestrutura toohello nuvem e toocreate soluções híbridas com o Azure e aos seus recursos no local. Pode ler mais sobre o assunto [aqui](../virtual-network/virtual-networks-overview.md).

Se pretender que as políticas de segurança toodefine para o tráfego (entrado e saído) na sua rede virtual em que está a implementar o Azure RemoteApp, recomendamos vivamente a criação de uma sub-rede separada para o Azure RemoteApp de rest de Olá das implementações no Olá do Azure rede virtual. Para mais informações sobre como as políticas de segurança de toodefine no seu Azure virtual rede sub-rede, leia [o que é um grupo de segurança de rede (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Tipos de coleções do Azure RemoteApp com redes virtuais do Azure
Olá gráficos seguintes mostram Olá duas opções de coleção diferente quando quiser toouse uma rede virtual.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Coleção de nuvem do Azure RemoteApp com VNET
 ![O Azure RemoteApp - coleção na nuvem com uma VNET](./media/remoteapp-planvpn/ra-cloudvpn.png)

Representa uma coleção do Azure RemoteApp em todos os recursos de Olá que os anfitriões de sessão de RemoteApp Olá têm de tooaccess estão implementados no Azure. Podem estar em Olá mesma VNET, como Olá VNET do RemoteApp ou uma VNET diferentes no Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Coleção de híbrida do Azure RemoteApp com VNET
![O Azure RemoteApp - coleção híbrida com uma VNET](./media/remoteapp-planvpn/ra-hybridvpn.png)

Representa uma coleção do Azure RemoteApp em que alguns dos recursos de Olá que os anfitriões de sessão de RemoteApp Olá têm de tooaccess estão implementados no local. Olá VNET do RemoteApp é toohello ligado no local rede, utilizando tecnologias de híbridos do Azure como VPN de site para site ou uma Expressroute.

## <a name="how-hello-system-works"></a>Como funciona o sistema de Olá
Em Olá abrange o Azure RemoteApp implementa máquinas virtuais do Azure (com a imagem carregada) toohello sub-rede da rede virtual que escolheu durante o aprovisionamento. Se tiver optado por uma coleção híbrida, iremos tente tooresolve Olá FQDN do controlador de domínio de Olá que introduziu no Olá aprovisionamento de fluxo de trabalho com o servidor DNS Olá fornecido na rede virtual Olá.  
Se estiver a ligar tooan de rede virtual existente, certifique-se de que tooexpose Olá necessário as portas nos seus grupos de segurança de rede na sua sub-rede do Azure RemoteApp. 

Recomendamos que utilize um [sub-rede suficientemente grande para o Azure RemoteApp](remoteapp-vnetsizing.md). Olá maior suportada pela rede Virtual do Azure é /8 (utilizando as definições de sub-rede CIDR). A sub-rede deve ser suficientemente grande tooaccommodate todos os Olá RemoteApp as VMs do Azure durante vertical quando mais utilizadores estão a aceder a aplicações de Olá. 

Seguem-se as coisas de Olá, terá de tooenable na sua sub-rede de rede virtual: 

1. Tráfego de saída da sub-rede Olá deve ser permitido na porta intervalo 10101 10175 toocommunicate com um dos serviços de Azure RemoteApp internos Olá.
2. Tráfego de saída deve ser permitido a partir do seu tooAzure tooconnect de sub-rede armazenamento na porta 443
3. Se tiver o Active Directory alojado no Azure, certifique-se qualquer VM na sub-rede da rede virtual para o Azure RemoteApp Olá tooconnect capaz de controlador de domínio de toothat. Olá DNS na rede virtual Olá deve ser capaz de tooresolve Olá FQDN deste controlador de domínio.

## <a name="virtual-network-with-forced-tunneling"></a>Rede virtual com a imposição do túnel
[Imposição do túnel](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) é agora suportado para todas as novas coleções do Azure RemoteApp. Estamos atualmente não suportam migração Olá um toosupport coleção existente imposição do túnel.  Terá toodelete todas as suas coleções existentes utilizando Olá VNET que está a ligar tooAzure RemoteApp e crie um novo um tooget imposição do túnel ativado no seu coleções. 

