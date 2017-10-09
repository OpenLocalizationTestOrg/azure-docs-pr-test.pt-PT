---
title: aaaHow toomonitor uma conta de armazenamento do Azure | Microsoft Docs
description: "Saiba como toomonitor uma conta de armazenamento no Azure utilizando Olá portal do Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Monitorizar uma conta de armazenamento no Olá portal do Azure

[Análise de armazenamento do Azure](../storage-analytics.md) fornece métricas para todos os serviços de armazenamento e os registos para blobs, filas e tabelas. Pode utilizar Olá [portal do Azure](https://portal.azure.com) tooconfigure que métricas e registos é registada para a sua conta e configure gráficos que fornecem representações visuais dos seus dados de métricas.

> [!NOTE]
> Não existem custos associados a examinar os dados de monitorização no Olá portal do Azure. Para obter mais informações, consulte [faturação e de análise de armazenamento](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> Atualmente File storage do Azure suporta métricas da análise de armazenamento, mas ainda não suporta o registo.
>
> Contas de armazenamento com um tipo de replicação de com redundância de zona de armazenamento (ZRS) atualmente não dispõe de métricas de Olá ou a capacidade do registo ativada.
> 
> Para um guia aprofundado sobre como utilizar a análise de armazenamento e outro tooidentify de ferramentas, diagnosticar e resolver problemas relacionados com o Storage do Azure, consulte [monitorizar, diagnosticar e resolver problemas de armazenamento do Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Configurar a monitorização de uma conta de armazenamento

1. No Olá [portal do Azure](https://portal.azure.com), selecione **contas do Storage**, em seguida, no dashboard de conta ao hello do tooopen de nome Olá armazenamento conta.
1. Selecione **diagnóstico** no Olá **monitorização** secção do painel de menu Olá.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Selecione Olá **tipo** dos dados de métricas para cada **serviço** desejar toomonitor e Olá **política de retenção** para dados de Olá. Também pode desativar a monitorização, definindo **estado** demasiado**desativar**.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Existem dois tipos de métricas, pode ativar para cada serviço, que estão ativadas por predefinição para novas contas de armazenamento:

   * **Agregação**: recolhe métricas como percentagens de entrada/saída, disponibilidade, latência e êxito. Estas métricas são agregadas para serviços de ficheiros, tabela, fila e blob Olá.
   * **Por API**: na adição toohello agregado métricas recolhe Olá mesmo conjunto de métricas para cada operação de armazenamento na Olá API do serviço de armazenamento do Azure.

   política de retenção de dados de Olá tooset, mover Olá **retenção (dias)** controlo de deslize ou introduza o número de Olá de dias de dados tooretain, de 1 too365. predefinição de Olá para novas contas de armazenamento é sete dias. Se não pretender que tooset uma política de retenção, introduza zero. Se não houver nenhuma política de retenção, está a funcionar tooyou toodelete Olá dados de monitorização.

   > [!WARNING]
   > São-lhe cobrados quando eliminar manualmente os dados de métricas. Dados de análise obsoletos (mais antigos do que a política de retenção de dados) foi eliminados pelo sistema Olá sem custos. É recomendável definir uma política de retenção com base no quanto pretende tooretain dados de análise de armazenamento para a sua conta. Consulte [que cobra pode implicar ao ativar as métricas do storage?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) para obter mais informações.
   >

1. Quando concluir a configuração de monitorização de Olá, selecione **guardar**.

Um conjunto predefinido de métricas é apresentado nos gráficos no painel de conta de armazenamento Olá, bem como painéis de serviço individual Olá (blob, fila, tabela e ficheiro). Assim que tiver ativado as métricas para um serviço, pode demorar tooan hora para dados tooappear no respetivos gráficos. Pode selecionar **editar** em qualquer métrica gráfico demasiado[configurar as métricas](#how-to-customize-metrics-charts) são apresentadas no gráfico de Olá.

Pode desativar a recolha de métricas e registo definindo **estado** demasiado**desativar**.

> [!NOTE]
> Storage do Azure utiliza [tabela armazenamento](../common/storage-introduction.md#table-storage) métricas de Olá toostore para a sua conta de armazenamento e métricas de Olá arquivos em tabelas na sua conta. Para obter mais informações, consulte. [Como são armazenadas as métricas](../common/storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Personalizar gráficos de métricas

Utilize Olá seguir o procedimento toochoose que tooview de métricas de armazenamento um gráfico de métricas. 

1. Comece por apresentar um gráfico de métrica de armazenamento no Olá portal do Azure. Pode encontrar gráficos no Olá **painel de conta de armazenamento** e no Olá **métricas** painel para um serviço individual (blob, fila, tabela, o ficheiro).

   Neste exemplo, iremos trabalhar com Olá seguinte gráfico que aparece no Olá **painel de conta de armazenamento**:

   ![Seleção de gráfico no portal do Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Em seguida, clique em qualquer lugar na Olá do Olá gráfico tooopen **métrica** painel. Selecione **editar gráfico** tooopen Olá **editar gráfico** painel.

   ![Botão de gráfico no painel de gráfico editar](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. No Olá **editar gráfico** painel, selecione de Olá **intervalo de tempo** de Olá métricas toodisplay no gráfico de Olá e Olá **serviço** (blob, fila, tabela, de ficheiros) cujas métricas desejar toodisplay. Aqui selecionamos toodisplay Olá passado métricas da semana para o serviço de blob Olá:

   ![Seleção de intervalo e o serviço de hora no painel de editar gráfico Olá](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Selecione Olá indivíduo **métricas** como tinha apresentado no gráfico de Olá, em seguida, clique em **OK**. Por exemplo, aqui iremos escolheu toodisplay Olá *ContainerCount* e *ObjectCount* métricas:

   ![Seleção de métrica individuais no painel de editar gráfico](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

As definições de gráfico não afetam a coleção de Olá, agregação ou o armazenamento dos dados na conta do storage Olá de monitorização, Olá apenas de visualização de dados de métricas.

### <a name="metrics-availability-in-charts"></a>Disponibilidade de métricas nos gráficos

lista de Olá de alterações de métricas disponíveis com base no serviço que escolheu no Olá pendente e de um tipo de unidade de gráfico de Olá Olá que estiver a editar. Por exemplo, pode selecionar métricas de percentagem, como *PercentNetworkError* e *PercentThrottlingError* apenas se estiver a editar um gráfico que mostra as unidades de medida como percentagem:

![Gráfico de percentagem de erro de pedido no Olá portal do Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Resolução de métricas

métricas de Olá que selecionou no diagnóstico determina a resolução de Olá de métricas de Olá que estão disponíveis para a sua conta:

* **Agregação** monitorização fornece métricas como percentagens de entrada/saída, disponibilidade, latência e êxito. Estas métricas são agregadas de Olá blob, tabela, ficheiro e serviços da fila.
* **Por API** disponibiliza melhorar resolução, métricas disponíveis para operações de armazenamento individuais, além disso toohello agregados de nível de serviço.

## <a name="configure-metrics-alerts"></a>Configurar alertas de métricas

Pode criar alertas toonotify que quando limiares tem sido atingidos de métricas de recurso de armazenamento.

1. Olá tooopen **painel regras de alerta**, desloque para baixo toohello **monitorização** secção Olá **painel Menu** e selecione **regras de alerta**.
1. Selecione **Adicionar alerta** tooopen Olá **adicionar uma regra de alerta** painel
1. Selecione um **recursos** (blob, ficheiro, fila, tabela) a partir da Olá pendente e introduza um **nome** e **Descrição** para a nova regra de alerta.
1. Selecione Olá **métrica** para o qual gostaria de tooadd um alerta, um alerta **condição**e um **limiar**. alterações de tipos de Olá limiar unidade consoante métrica Olá que escolheu. Por exemplo, "contagem" é um tipo de unidade para Olá *ContainerCount*, enquanto a unidade de Olá para Olá *PercentNetworkError* métrica é uma percentagem.
1. Selecione Olá **período**. As métricas que atingirem ou excedem Olá limiar dentro do acionador de período Olá um alerta.
1. (Opcional) Configurar **E-Mail** e **Webhook** notificações. Para obter mais informações sobre webhooks, consulte [configurar um webhook num alerta métrico Azure](../../monitoring-and-diagnostics/insights-webhooks-alerts.md). Se não configurar notificações de e-mail ou webhook, alertas irão aparecer apenas em Olá portal do Azure.

![Painel 'Adicionar uma regra de alerta' no Olá portal do Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Adicionar métricas gráficos toohello portal dashboard

Pode adicionar gráficos de métricas do Storage do Azure de qualquer um dos armazenamento contas tooyour dashboard do portal do.

1. Clique em selecionar **editar dashboard** ao visualizar o dashboard na Olá [portal do Azure](https://portal.azure.com).
1. No Olá **mosaico galeria**, selecione **localizar os mosaicos por** > **tipo**.
1. Selecione **tipo** > **contas do Storage**.
1. No **recursos**, selecione a conta de armazenamento Olá cujas métricas desejar tooadd toohello dashboard.
1. Selecione **categorias** > **monitorização**.
1. Gráfico de arrastar e largar Olá mosaico no dashboard para a métrica de Olá que pretende apresentar. Repita para todas as métricas que gostaria de apresentadas no dashboard de Olá. Olá seguinte imagem, Olá "Blobs - Total de pedidos do" gráfico é realçado, por exemplo, mas todos os gráficos de Olá estão disponíveis para colocação no dashboard.

   ![Galeria de mosaico no portal do Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Selecione **feito personalizar** perto Olá parte superior do dashboard de Olá quando tiver terminado a adição de gráficos.

Depois de adicionar dashboard tooyour de gráficos, pode personalizar ainda mais-las conforme descrito em [personalizar gráficos de métricas](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Configurar o registo

Pode instruir os registos de diagnóstico do Storage do Azure toosave para de leitura, escrita e eliminação pedidos para Olá blob, tabela e serviços da fila. política de retenção de dados de Olá definir também se aplica toothese registos.

> [!NOTE]
> Atualmente File storage do Azure suporta métricas da análise de armazenamento, mas ainda não suporta o registo.
>

1. No Olá [portal do Azure](https://portal.azure.com), selecione **contas do Storage**, em seguida, nome de Olá do painel de conta ao armazenamento do Olá de tooopen Olá armazenamento conta.
1. Selecione **diagnóstico** no Olá **monitorização** secção do painel de menu Olá.

    ![Diagnóstico item de menu sob monitorização na Olá portal do Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Certifique-se **estado** estiver definido demasiado**no**e selecione Olá **serviços** para o qual gostaria de tooenable registo.

    ![Configure o registo no Olá portal do Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Clique em **Guardar**.

os registos de diagnóstico de Olá são guardados no contentor do blob denominado $logs na sua conta de armazenamento. Pode ver os dados de registo Olá utilizar um Explorador de armazenamento como Olá [Explorador de armazenamento do Microsoft](http://storageexplorer.com), ou através de programação utilizando a biblioteca de clientes do storage Olá ou PowerShell.

Para obter informações sobre como aceder ao contentor de Olá $logs, consulte [aceder aos dados de registo e ativar o registo de armazenamento](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Passos seguintes

* Obter mais informações sobre [métricas, registo e faturação](../storage-analytics.md) para análise de armazenamento.
* [Ativar dados de métricas de métricas e vista de armazenamento do Azure](../storage-enable-and-view-metrics.md) utilizando o PowerShell e através de programação com c#.
