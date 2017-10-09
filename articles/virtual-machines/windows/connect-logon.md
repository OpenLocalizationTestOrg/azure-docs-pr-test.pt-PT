---
title: aaaConnect tooa VM do Windows Server | Microsoft Docs
description: "Saiba como tooconnect e iniciar sessão utilizando o tooa VM do Windows hello do Azure modelo de implementação de Gestor de recursos de portal e Olá."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Como o registo no tooan virtual do Azure e tooconnect máquina com o Windows
Irá utilizar Olá **Connect** botão no Olá toostart portal do Azure, uma sessão de ambiente de trabalho remoto (RDP) a partir de um ambiente de trabalho do Windows. Ligue primeiro toohello máquina e, em seguida, iniciar sessão.

Se estiver a tentar tooconnect tooa VM do Windows de um Mac, terá de tooinstall como um cliente RDP para Mac [ambiente de trabalho remoto](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Ligar a máquina virtual de toohello
1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. No menu do Hub de Olá, clique em **máquinas virtuais**.
3. Selecione a máquina virtual de Olá na lista de Olá.
4. No painel de Olá para a máquina virtual de Olá, clique em **Connect**.
   
    ![Captura de ecrã do Olá Mostrar portal do Azure como tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Se hello **Connect** botão no portal de Olá estiver a cinzento e não são tooAzure ligado através de um [Express Route](../../expressroute/expressroute-introduction.md) ou [VPN Site a Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) ligação, terá de toocreate e Atribua à VM um endereço IP público antes de poder utilizar o RDP. Pode ler mais sobre [endereços IP públicos no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Inicie sessão na máquina virtual de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Passos seguintes
Caso se depare com problemas quando tenta tooconnect, consulte [ligações de resolução de problemas de ambiente de trabalho remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Este artigo orienta-o ao longo do diagnóstico e da resolução de problemas comuns.

