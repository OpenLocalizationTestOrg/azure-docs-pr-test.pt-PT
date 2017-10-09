---
title: aaaMonitor Surface Hubs com Log Analytics do Azure | Microsoft Docs
description: "Utilize Olá Surface Hub solução tootrack Olá estado de funcionamento do seu Surface Hubs e compreender como estão a ser utilizados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Monitorizar Surface Hubs tootrack de análise de registos com o respetivo estado de funcionamento

![Símbolo de Hub de superfície](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

Este artigo descreve como pode utilizar Olá solução Surface Hub na análise de registos toomonitor Microsoft Surface Hub dispositivos Olá Microsoft Operations Management Suite (OMS). Inicie sessão ajuda a análise que controlar o estado de funcionamento de Olá do seu Surface Hubs, bem como a compreender como estão a ser utilizados.

Cada Surface Hub tem Olá que Microsoft Monitoring Agent instalado. O através do agente de Olá que pode enviar dados a partir do seu tooOMS Surface Hub. Ficheiros de registo são lidos a partir do seu Surface Hubs e estão, em seguida, são enviados o serviço do toohello OMS. Problemas, como servidores estar offline, Olá calendário não sincronizar ou se a conta de dispositivo Olá é toolog não é possível para o Skype são apresentados na OMS no dashboard do Olá Surface Hub. Ao utilizar dados Olá no dashboard de Olá, pode identificar dispositivos que não estão em execução, ou que estão a ter outros problemas e potencialmente aplicar correções para problemas de Olá detetado.

## <a name="installing-and-configuring-hello-solution"></a>Instalar e configurar a solução de Olá
Utilize Olá tooinstall informações a seguir e configurar a solução de Olá. Na ordem toomanage o Surface Hubs de Olá Microsoft Operations Management Suite (OMS), terá de Olá seguintes:

* Uma subscrição válida demasiado[OMS](http://www.microsoft.com/oms).
* Um [subscrição OMS](https://azure.microsoft.com/pricing/details/log-analytics/) nível que irão suportar o número de Olá de dispositivos que pretende toomonitor. Preços do OMS variam consoante o número de dispositivos inscritos e a quantidade de dados-processos. Poderá ser útil tootake isto em consideração ao planear a sua implementação Surface Hub.

Em seguida, irá adicionar uma subscrição de Microsoft Azure existente do OMS subscrição tooyour ou criar uma nova área de trabalho diretamente através do portal do OMS Olá. Instruções detalhadas para utilizando um dos métodos é [introdução à análise de registos](log-analytics-get-started.md). Depois de configurada Olá subscrição OMS, existem duas formas tooenroll os seus dispositivos Surface Hub:

* Automaticamente através do Intune
* Manualmente através de **definições** no seu dispositivo Surface Hub.

## <a name="set-up-monitoring"></a>Configurar a monitorização
Pode monitorizar o estado de funcionamento de Olá e a atividade dos seus Surface Hub através da análise do registo no OMS. Pode inscrever Olá Surface Hub no OMS através do Intune ou localmente utilizando **definições** no Olá Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Ligar tooOMS Surface Hubs através do Intune
Irá precisar de a Olá ID e a chave da área de trabalho para a área de trabalho do OMS Olá que irão gerir a sua Surface Hubs. Pode obter as do portal do OMS Olá.

O Intune é um produto Microsoft permite-lhe toocentrally gerir Olá OMS as definições de configuração que são aplicado tooone ou mais dos seus dispositivos. Siga estes passos tooconfigure os seus dispositivos através do Intune:

1. Inicie sessão no tooIntune.
2. Navegue demasiado**definições** > **origens ligadas**.
3. Criar ou editar uma política baseada no modelo do Olá Surface Hub.
4. Navegue toohello secção OMS (informações operacionais do Azure) da política de Olá e adicionar Olá *ID da área de trabalho* e *chave da área de trabalho* toohello política.
5. Guarde política de Olá.
6. Associe política Olá grupo adequado do Olá dos dispositivos.

   ![Política do Intune](./media/log-analytics-surface-hubs/intune.png)

Intune, em seguida, sincroniza-se as definições de OMS Olá com dispositivos Olá no grupo de destino Olá, inscrevendo-os na sua área de trabalho do OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Ligar tooOMS Surface Hubs utilizando a aplicação de definições de Olá
Irá precisar de a Olá ID e a chave da área de trabalho para a área de trabalho do OMS Olá que irão gerir a sua Surface Hubs. Pode obter as do portal do OMS Olá.

Se não utilizar o Intune toomanage seu ambiente, pode inscrever dispositivos manualmente através de **definições** em cada Surface Hub:

1. A partir do seu Surface Hub, abra **definições**.
2. Introduza as credenciais de administrador do dispositivo Olá quando lhe for pedido.
3. Clique em **este dispositivo**e Olá em **monitorização**, clique em **configurar definições do OMS**.
4. Selecione **Ativar monitorização**.
5. Na caixa de diálogo do definições do OMS de Olá, escreva Olá **ID da área de trabalho** e Olá tipo **chave da área de trabalho**.  
   ![definições](./media/log-analytics-surface-hubs/settings.png)
6. Clique em **OK** configuração de Olá toocomplete.

Uma confirmação é apresentado a informar se pretende ou não Olá configuração OMS com êxito foi aplicada toohello dispositivo. Se tiver sido, é apresentada uma mensagem a indicar que o agente Olá ligado com êxito o serviço do toohello OMS. dispositivo Olá, em seguida, começa a enviar dados tooOMS onde pode ver e atuar no mesmo.

## <a name="monitor-surface-hubs"></a>Monitor de Surface Hubs
Monitorização do seu Surface Hubs utilizar OMS é muito como monitorizar todos os outros dispositivos inscritos.

1. Inicie sessão no toohello portal do OMS.
2. Navegue até o dashboard de pacote de solução do toohello Surface Hub.
3. É apresentado o estado de funcionamento do seu dispositivo.

   ![Dashboard de Hub de superfície](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Pode criar [alertas](log-analytics-alerts.md) com base na procura de registo existentes ou personalizados. Utilizar Olá de dados de Olá que OMS recolhe do seu Surface Hubs, pode procurar problemas e alerta em condições de Olá por si para os seus dispositivos.

## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados Surface Hub.
* Criar [alertas](log-analytics-alerts.md) toonotify-o quando ocorrem problemas com o Surface Hubs.
