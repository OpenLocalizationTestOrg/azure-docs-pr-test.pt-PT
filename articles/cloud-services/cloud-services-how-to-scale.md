---
title: "aaaAuto dimensionar um serviço em nuvem no portal clássico Olá | Microsoft Docs"
description: "(clássica) Saiba como toouse Olá tooconfigure portal clássico regras de dimensionamento automático para uma função de web do serviço de nuvem ou a função de trabalho no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Como tooconfigure automática de dimensionamento para um serviço em nuvem no portal clássico Olá
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-scale-portal.md)
> * [Portal Clássico do Azure](cloud-services-how-to-scale.md)

Na página de escala de Olá do Olá portal clássico do Azure, pode configurar as definições de dimensionamento automático para a função da web ou função de trabalho. Em alternativa, pode configurar o dimensionamento manual em vez de com base em regras de dimensionamento automático.

> [!NOTE]
> Este artigo foca-se as funções web e de trabalho do serviço em nuvem. Quando cria uma máquina virtual (clássica) diretamente, está alojada num serviço em nuvem. Algumas destas informações aplicam-se os tipos de toothese de máquinas virtuais. Dimensionamento de um conjunto de disponibilidade de máquinas virtuais está apenas a encerrá-los e desativar a com base nas regras de dimensionamento de Olá que configura. Para obter mais informações sobre as máquinas virtuais e conjuntos de disponibilidade, consulte [gerir Olá disponibilidade das Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Deve considerar Olá seguintes informações antes de configurar o dimensionamento para a sua aplicação:

* Dimensionamento é afetado pela utilização do núcleo.

    Instâncias de função maior utilizem mais núcleos. Pode dimensionar uma aplicação apenas dentro do limite de Olá de núcleos para a sua subscrição. Por exemplo, diga a que sua subscrição tem um limite de 20 núcleos. Se executar uma aplicação com dois serviços de cloud média (um total de 4 núcleos), pode apenas Dimensionar outras implementações de serviço em nuvem na sua subscrição por Olá restantes 16 núcleos. Para obter mais informações acerca dos tamanhos, consulte [tamanhos do serviço em nuvem](cloud-services-sizes-specs.md).

* Tem de criar uma fila e associá-la a uma função antes de a poder dimensionar a uma aplicação com base num limiar da mensagem. Para obter mais informações, consulte [como toouse Olá o serviço de armazenamento de filas](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Pode dimensionar recursos que estão ligado tooyour serviço em nuvem. Para obter mais informações sobre ligar os recursos, consulte [como: ligar um serviço de nuvem do recurso tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable elevada disponibilidade da aplicação, deve garantir que é implementado com dois ou mais instâncias de função. Para obter mais informações, consulte [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Dimensionamento de agenda
Por predefinição, todas as funções não siga uma agenda específica. Por conseguinte, aplicam-se as definições alteradas tooall vezes e todos os dias ao longo do ano Olá. Se quiser, pode configurar o dimensionamento de manual ou automática para um dos seguintes modos de Olá:

* Dias da semana
* Fim de semana
* Nights semana
* Mornings semana
* Datas específicas
* Intervalos de data específica

Olá agenda definição é configurada em Olá [portal clássico do Azure](https://manage.windowsazure.com/) no Olá  
**Serviços em nuvem** > **\[seu serviço em nuvem\]** > **escala**  >   **\[Produção ou transição\]**  página.

Clique em Olá **configurar vezes agenda** botão para cada função que pretende toochange.

![Dimensionamento automático com base numa agenda o serviço em nuvem][scale_schedules]

## <a name="manual-scale"></a>Escala Manual
No Olá **escala** página, pode manualmente aumentar ou diminuir Olá diversas instâncias em execução num serviço em nuvem. Esta definição estiver configurada para cada agenda criou ou tooall tempo se não tiver criado uma agenda.

1. No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.
   
   > [!TIP]
   > Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.

2. Clique em **escala**.
3. Selecione o agendamento de Olá pretende toochange dimensionamento opções para. *Não períodos agendados* é a predefinição de Olá, se tiver não agendamentos definidos.
4. Determinar Olá **escala da métrica** secção e selecione **NONE**. Esta definição é a predefinição de Olá para todas as funções.
5. Cada função no serviço de nuvem Olá tem um controlo de deslize para alterar o número de Olá de toouse de instâncias.
   
    ![Dimensionar manualmente uma função de serviço em nuvem][manual_scale]
   
    Se precisar de mais instâncias, poderá ser necessário toochange Olá [tamanho da máquina virtual de serviço de nuvem](cloud-services-sizes-specs.md).
6. Clique em **Guardar**.  
   Instâncias de função são adicionadas ou removidas consoante as suas seleções.

> [!TIP]
> Sempre que consulte ![][tip_icon] mover o rato tooit e pode obter ajuda sobre o que uma definição específica faz.

## <a name="automatic-scale---cpu"></a>Escala automática - CPU
Este modo dimensiona se percentagem média do Olá de utilização da CPU ficar acima ou abaixo limiares especificados. Instâncias de função são criadas ou eliminadas quando isto acontece.

1. No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.
   
   > [!TIP]
   > Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.

2. Clique em **escala**.
3. Selecione o agendamento de Olá pretende toochange dimensionamento opções para. *Não períodos agendados* é a predefinição de Olá, se tiver não agendamentos definidos.
4. Determinar Olá **escala da métrica** secção e selecione **CPU**.
5. Agora pode configurar um intervalo mínimo e máximo de instâncias de funções, utilização de CPU de destino Olá (tootrigger um trabalho de dimensionamento) e quantas instâncias tooscale e reduzir verticalmente pelo.

![Dimensionar uma função de serviço de nuvem por carga de cpu][cpu_scale]

> [!TIP]
> Sempre que consulte ![][tip_icon] mover o rato tooit e pode obter ajuda sobre o que uma definição específica faz.

## <a name="automatic-scale---queue"></a>Escala automática - a fila
Este modo dimensiona automaticamente se Olá número de mensagens numa fila ficar acima ou abaixo de um limiar especificado. Instâncias de função são criadas ou eliminadas quando isto acontece.

1. No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.
   
   > [!TIP]
   > Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.

2. Clique em **escala**.
3. Determinar Olá **escala da métrica** secção e selecione **fila**.
4. Agora pode configurar um intervalo mínimo e máximo de instâncias de funções, fila de Olá e número de mensagens de fila tooprocess para cada instância e quantas instâncias tooscale, acima e abaixo pelo.

![Dimensionar uma função de serviço de nuvem por uma fila de mensagens][queue_scale]

> [!TIP]
> Sempre que consulte ![][tip_icon] mover o rato tooit e pode obter ajuda sobre o que uma definição específica faz.

## <a name="scale-linked-resources"></a>Dimensionar recursos ligados
Frequentemente, quando dimensionar uma função, seja a base de dados do tooscale benéfico Olá que aplicação Olá está também a utilizar. Se ligar o serviço de nuvem de toohello de base de dados de Olá, pode aceder a Olá dimensionamento definições para o recurso de clicando Olá de ligação adequado.

1. No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.
   
   > [!TIP]
   > Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.

2. Clique em **escala**.
3. Determinar Olá **ligado recursos** secção e clique em **gerir escala desta base de dados**.
   
   > [!NOTE]
   > Se não vir um **ligado recursos** secção, provavelmente, não tem quaisquer recursos ligados.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
