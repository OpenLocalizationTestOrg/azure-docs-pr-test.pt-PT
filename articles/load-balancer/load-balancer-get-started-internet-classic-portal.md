---
title: "Balanceador de carga aaaCreate um-para a Internet - portal do Azure clássico | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga com acesso à Internet no modelo de implementação clássica utilizando Olá portal clássico do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Introdução à criação de um Internet com o Balanceador de carga (clássica) na Olá portal clássico do Azure

> [!div class="op_single_selector"]
> * [Portal Clássico do Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure tem atualmente dois modelos de implementação: Azure Resource Manager e clássico. Confirme que compreende os [modelos e ferramentas de implementação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure. Pode ver a documentação de Olá de diversas ferramentas clicando Olá nos separadores na parte superior de Olá deste artigo. Este artigo abrange o modelo de implementação clássica Olá. Também pode [Saiba como o utilizando o Gestor de recursos do Azure de Balanceador de carga de toocreate um para a Internet](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Configurar um balanceador de carga com acesso à Internet para máquinas virtuais

Na ordem tooload equilibrar o tráfego de rede de Olá Internet em Olá máquinas de virtuais de um serviço em nuvem, terá de criar um conjunto com balanceamento de carga. Este procedimento assume que já criou máquinas de virtuais Olá e que estão todos os dentro Olá mesmo serviço em nuvem.

**tooconfigure um conjunto com balanceamento de carga para as máquinas virtuais**

1. No portal clássico do Azure Olá, clique em **máquinas virtuais**e, em seguida, clique no nome de Olá de uma máquina virtual no conjunto com balanceamento de carga de Olá.
2. Clique em **Pontos finais** e, em seguida, clique em **Adicionar**.
3. No Olá **adicionar uma máquina de virtual do ponto final tooa** página, clique em seta para a direita Olá.
4. No Olá **especificar detalhes de Olá do ponto final de Olá** página:

   * No **nome**, escreva um nome para o ponto final de Olá ou selecione nome Olá Olá lista de pontos finais predefinidos para protocolos comuns.
   * No **protocolo**, selecione o protocolo de Olá necessário pelo tipo de Olá de ponto final, TCP ou UDP, conforme necessário.
   * No **Porta pública e privada porta**, escreva os números de porta Olá que pretende Olá toouse de máquina virtual, conforme necessário. Pode utilizar uma porta privada Olá e regras de firewall no tráfego de tooredirect Olá máquinas virtuais de uma forma que é adequado para a sua aplicação. Porta privada Olá pode Olá igual a porta pública Olá. Por exemplo, para um ponto final para o tráfego web (HTTP), pode atribuir porta 80 tooboth Olá públicas e privadas porta.

5. Selecione **criar um conjunto com balanceamento de carga**e, em seguida, clique em seta para a direita Olá.
6. No Olá **configurar conjunto com balanceamento de carga de Olá** página, escreva um nome para o conjunto com balanceamento de carga de Olá e, em seguida, atribuir valores de Olá para o comportamento de sonda de Olá Balanceador de carga do Azure. Olá Load Balancer utiliza sondas toodetermine se Olá máquinas de virtuais em conjunto com balanceamento de carga de Olá estiverem disponíveis tooreceive tráfego de entrada.
7. Clique em Olá marca de verificação toocreate Olá com balanceamento de carga ponto final. Verá **Sim** no Olá **o nome do conjunto com balanceamento de carga** coluna Olá **pontos finais** página para a máquina virtual de Olá.
8. No portal de Olá, clique em **máquinas virtuais**, clique no nome de Olá de uma máquina virtual adicional no conjunto com balanceamento de carga de Olá, clique em **pontos finais**e, em seguida, clique em **adicionar**.
9. No Olá **adicionar uma máquina de virtual do ponto final tooa** página, clique em **adicionar ponto final tooan com balanceamento de carga conjunto existente**, selecione o nome de Olá do conjunto de balanceamento de carga Olá e, em seguida, clique em seta para a direita Olá.
10. No Olá **especificar detalhes de Olá do ponto final de Olá** página, escreva um nome para o ponto final de Olá e, em seguida, clique em marca de verificação Olá.

Para Olá outras máquinas virtuais em conjunto com balanceamento de carga de Olá, repita os passos 8 a 10.

## <a name="next-steps"></a>Passos seguintes

[Começar a configurar um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição de balanceador de carga](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
