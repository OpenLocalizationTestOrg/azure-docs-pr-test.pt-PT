---
title: "Olá aaaModify dados 0 definições num dispositivo StorSimple | Microsoft Docs"
description: "Saiba como toouse do Windows PowerShell para StorSimple tooreconfigure Olá interface rede DATA 0 no dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>Modificar definições da interface de rede 0 de dados de Olá no dispositivo StorSimple
## <a name="overview"></a>Descrição geral
O dispositivo Microsoft Azure StorSimple possui seis interfaces de rede, a partir dos dados 0 tooDATA 5. Olá dados 0 interface é sempre configurada através da interface do Windows PowerShell Olá ou consola de série de Olá e é automaticamente ativado para a nuvem. Tenha em atenção que não é possível configurar interface rede DATA 0 através de Olá portal clássico do Azure. 

Olá dados 0 interface de rede pela primeira vez é configurada através do Assistente de configuração de Olá durante a implementação inicial de dispositivo do StorSimple Olá. Quando o dispositivo de Olá está num modo operacional, poderá ser necessário tooreconfigure dados 0 definições. Este tutorial fornece dois métodos toomodify dados 0 as definições de rede, tanto através do Windows PowerShell para StorSimple.

Depois de ler este tutorial, será capaz de:

* Modificar dados 0 definição através do Assistente de configuração de Olá de rede
* Modificar as definições de rede 0 de dados através de Olá `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modificar as definições de rede 0 de dados através do Assistente de configuração
Pode reconfigurar as definições de rede 0 de dados através da interface do Windows PowerShell toohello do dispositivo StorSimple a ligar e iniciar uma sessão de Assistente de configuração. Efetuar Olá passos toomodify dados 0 os seguintes definições:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>definições de rede 0 toomodify dados através do Assistente de configuração
1. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**. Quando lhe for pedido fornecer Olá **palavra-passe de administrador do dispositivo**. palavra-passe predefinida de Olá é `Password1`.
2. Na linha de comandos Olá, escreva:
   
    `Invoke-HcsSetupWizard`
3. Um Assistente de configuração irá aparecer toohelp configurar Olá dados 0 interface do seu dispositivo. Forneça novos valores para o endereço IP Olá, o gateway e máscara de rede.

> [!NOTE]
> Olá fixo controladores IPs terá toobe reconfigurado através de Olá **configurar** página do dispositivo StorSimple Olá Olá portal clássico do Azure. Para mais informações, visite demasiado[modificar interfaces de rede](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modificar as definições de rede 0 de dados através do cmdlet Set-HcsNetInterface
Tooreconfigure uma maneira alternativa DATA 0 é de interface de rede através da utilização de Olá de Olá `Set-HcsNetInterface` cmdlet. Olá cmdlet é executado a partir da interface do Windows PowerShell Olá do dispositivo StorSimple. Quando utilizar este procedimento, controlador Olá IPs fixo também pode ser configurado aqui. Efetuar Olá passos toomodify Olá dados 0 os seguintes definições: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>definições de rede 0 toomodify dados através do cmdlet Olá HcsNetInterface conjunto
1. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**. Quando lhe for pedido forneça a palavra-passe de administrador de dispositivo Olá. palavra-passe predefinida de Olá é `Password1`.
2. Na linha de comandos Olá, escreva:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Entre parênteses Retos Olá angled, escreva Olá os seguintes valores para os dados 0:
   
   * Endereço IPv4
   * Gateway de IPv4
   * Máscara de sub-rede IPv4
   * Endereço IPv4 fixo para o controlador 0
   * Endereço IPv4 fixo para o controlador 1
     
     Para obter mais informações sobre a utilização de Olá deste cmdlet, visite demasiado[do Windows PowerShell para StorSimple referência de cmdlet](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Passos seguintes
* tooconfigure interfaces de rede que não sejam dados 0, pode utilizar Olá [Configurar página no portal clássico do Azure de Olá](storsimple-modify-device-config.md). 
* Se ocorrer algum problema quando configurar as interfaces de rede, consulte demasiado[resolver problemas de implementação](storsimple-troubleshoot-deployment.md).

