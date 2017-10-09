---
title: "aaaIT conector de gestão de serviço no OMS | Microsoft Docs"
description: "Utilize o monitor de toocentrally Olá conector de gestão de serviços de TI e gerir itens de trabalho ITSM Olá no OMS e resolva os problemas rapidamente."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Gerir centralmente a itens de trabalho ITSM utilizando o conector de gestão de serviços de TI (pré-visualização)

![Símbolo do conector de gestão do serviço IT](./media/log-analytics-itsmc/itsmc-symbol.png)

Pode utilizar Olá conector de gestão de serviço de TI (ITSMC) na análise de registos do OMS toocentrally monitorizar e gerir itens de trabalho em seu ITSM produtos/serviços.

Olá conector de gestão de serviços de TI integra seus serviços e produtos de gestão de serviço de TI (ITSM) existente com a análise de registos do OMS.  solução Olá tem integração bidirecional com ITSM produtos/serviços, onde fornece Olá OMS utilizadores incidentes de toocreate uma opção, alertas ou eventos na solução ITSM. conector Olá também importa dados, tais como incidentes e pedidos de alteração da solução ITSM para análise de registos do OMS.

Com o conector de gestão de serviços de TI, pode:

  - Monitorizar e gerir itens de trabalho para ITSM produtos/serviços utilizados em toda a organização centralmente.
  - Crie itens de trabalho ITSM (por exemplo, o alerta do evento, incidente) no ITSM de alertas do OMS e através de pesquisa de registo.
  - Leia os incidentes e pedidos de alteração da solução ITSM e correlacionar com dados de registo relevantes na área de trabalho de análise de registos.
  - Localize quaisquer eventos de atividade invulgares e inesperados e resolvê-los, mesmo antes dos utilizadores finais de Olá chamar e comunicá-los toohello técnico.
  - Importar dados de itens de trabalho para análise de registos e criar a chave de desempenho (KPI) do indicador relatórios.  Utilizar estes relatórios, pode identificar, avaliar e atuar sobre vários itens importantes, tais como a avaliação de malware.
  - Ver organizados dashboards para informações mais aprofundadas sobre incidentes, pedidos de alteração e sistemas afetados.
  - Resolva os problemas mais rápida através da correlação entre a com outras soluções de gestão na área de trabalho de análise de registos de Olá.


## <a name="prerequisites"></a>Pré-requisitos

tooimport Olá ITSM itens de trabalho para análise de registos do OMS, a solução de Olá requer uma ligação entre Olá conector de gestão de serviços de TI no Olá OMS e Olá TI SM produtos/serviços a partir do qual importar itens de trabalho de Olá.


## <a name="configuration"></a>Configuração

Adicionar Olá espaço de trabalho do conector de gestão de serviços de TI solução tooyour OMS, utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).

O conector de gestão do serviço IT mosaico como ver na Galeria de soluções de Olá:

![mosaico de conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Após a adição com êxito, verá Olá conector de gestão de serviços de TI em **OMS** > **definições** > **origens ligadas.**

![ITSMC ligado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Por predefinição, o Olá conector de gestão de serviços de TI atualiza os dados da ligação de Olá uma vez em cada 24 horas. toorefresh da ligação atualizações dos dados de forma instantânea para qualquer modelo ou as edições que efetuar, clique em Olá atualização botão apresentado seguinte tooyour a ligação.

 ![Atualização ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Pacotes de gestão
Esta solução não requer quaisquer pacotes de gestão.

## <a name="connected-sources"></a>Origens ligadas

Olá ITSM seguintes produtos/serviços são suportados pelo Olá conector de gestão de serviços de TI:

- [O System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Utilizar a solução de Olá

Depois de ligar Olá conector de gestão do serviço de TI do OMS com o serviço ITSM, serviços de análise de registos de Olá inicia a recolha de dados de Olá de Olá ligado ITSM produtos/serviços.

> [!NOTE]
> - Dados importados pela solução de conector de gestão de serviços de TI aparecem na análise de registos como eventos com o nome **ServiceDesk_CL**.
- Evento contém um campo com o nome **ServiceDeskWorkItemType_s**. que pode colocar o respetivo valor como incidentes, ou pedido de alteração, consoante Olá do item de trabalho dados contidos em Olá **ServiceDesk_CL** eventos.

## <a name="input-data"></a>Dados de entrada
Itens de trabalho importados do Olá ITSM produtos/serviços.

Olá informações seguintes mostram exemplos de dados recolhidos pelo conector do serviço de TI a gestão de Olá:

> [!NOTE]
> Consoante Olá do item de trabalho importado para análise de registos do tipo **ServiceDesk_CL** contém Olá seguintes campos:

**Item de trabalho:** **incidentes**  
ServiceDeskWorkItemType_s = "Incidente"

**Campos**

- ServiceDeskConnectionName
- ID do serviço de suporte técnico
- Estado
- Urgência
- Impacto
- Prioridade
- Escalamento
- Criado por
- Resolvido pelo
- Fechada pelo
- Origem
- Atribuído a
- Categoria
- Título
- Descrição
- Data de criação
- Data de fecho
- Data de resolução
- Data da última modificação
- Computador


**Item de trabalho:** **pedidos de alteração**

ServiceDeskWorkItemType_s = "ChangeRequest"

**Campos**
- ServiceDeskConnectionName
- ID do serviço de suporte técnico
- Criado por
- Fechada pelo
- Origem
- Atribuído a
- Título
- Tipo
- Categoria
- Estado
- Escalamento
- Estado de conflito
- Urgência
- Prioridade
- Risco
- Impacto
- Atribuído a
- Data de criação
- Data de fecho
- Data da última modificação
- Data de pedido
- Data de início planeada
- A ser planeada a data de fim
- Data de início do trabalho
- Data de fim de trabalho
- Descrição
- Computador

## <a name="output-data-for-a-servicenow-incident"></a>Dados de saída para um incidente de ServiceNow

| Campo do OMS | Campo ITSM |
|:--- |:--- |
| ServiceDeskId_s| Número |
| IncidentState_s | Estado |
| Urgency_s |Urgência |
| Impact_s |Impacto|
| Priority_s | Prioridade |
| CreatedBy_s | Abrir por |
| ResolvedBy_s | Resolvido pelo|
| ClosedBy_s  | Fechada pelo |
| Source_s| Tipo de contacto |
| AssignedTo_s | Atribuído demasiado |
| Category_s | Categoria |
| Title_s|  Breve descrição |
| Description_s|  Notas |
| CreatedDate_t|  Abrir |
| ClosedDate_t| Fechado|
| ResolvedDate_t|Resolvido|
| Computador  | item de configuração |

## <a name="output-data-for-a-servicenow-change-request"></a>Pedido de alteração de dados de saída para um ServiceNow

| Campo do OMS | Campo ITSM |
|:--- |:--- |
| ServiceDeskId_s| Número |
| CreatedBy_s | Pedido pelo |
| ClosedBy_s | Fechada pelo |
| AssignedTo_s | Atribuído demasiado |
| Title_s|  Breve descrição |
| Type_s|  Tipo |
| Category_s|  Catgory |
| CRState_s|  Estado|
| Urgency_s|  Urgência |
| Priority_s| Prioridade|
| Risk_s| Risco|
| Impact_s| Impacto|
| RequestedDate_t  | Pedido por data |
| ClosedDate_t | Data de fecho |
| PlannedStartDate_t  |     Data de início planeada |
| PlannedEndDate_t  |   Data de fim planeada |
| WorkStartDate_t  | Data de início real |
| WorkEndDate_t | Data de fim real|
| Description_s | Descrição |
| Computador  | Item de configuração |

**Ecrã de análise de registos de exemplo para dados ITSM:**

![Ecrã de análise do registo](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>Conector de gestão do serviço IT – integração com outras soluções do OMS

Conector de gestão do serviço IT, suporta atualmente a integração com Olá solução de mapa de serviço.

Mapa de serviço Deteta automaticamente Olá componentes da aplicação no Windows e comunicação entre os serviços de Olá sistemas Linux e mapas. Permite-lhe tooview seus servidores como considerá-los – como interligados sistemas que fornecem serviços críticos. Mapa de serviço mostra as ligações entre servidores, processos, e portas em qualquer arquitetura TCP ligados sem qualquer configuração necessária à instalação de um agente. Obter mais informações: [mapa de serviço](../operations-management-suite/operations-management-suite-service-map.md).

Esta integração, pode ver itens de suporte técnico Olá serviço criados em soluções ITSM Olá, conforme mostrado no seguinte exemplo de Olá:

![Solução integrada ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Criar itens de trabalho ITSM para alertas do OMS

Existência de alertas do OMS Olá, pode criar itens de trabalho associados no Olá ligado ITSM origens.  toodo Olá, utilize seguinte procedimento:

1. De **pesquisa registo** janela, executar um registo de tooview de consulta de pesquisa de dados. Os resultados da consulta são origem Olá para itens de trabalho.
2. No **pesquisa registo**, clique em **alerta** tooopen Olá **Adicionar regra de alerta** página.

    ![Ecrã de análise do registo](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. No Olá **Adicionar regra de alerta** janela, forneça detalhes Olá necessário para **nome**, **gravidade**, **consulta de pesquisa**, e  **Critérios de alerta** (medida janela/métrica de tempo).
4. Selecione **Sim** para **ITSM ações**.
5. Selecione a ligação de ITSM Olá **selecione ligação** lista.
6. Forneça detalhes Olá conforme necessário.
7. um item de trabalho separada para cada entrada de registo de Olá este alerta, selecione de toocreate **criar itens de trabalho individuais para cada entrada de registo** caixa de verificação.

    Ou

    Deixe este item de trabalho apenas uma caixa de verificação toocreate não seleccionado para qualquer número de entradas de registo neste alerta.

7. Clique em **Guardar**.

alerta OMS Olá será criada em **alertas**. Olá trabalho da ligação ITSM correspondente itens são criados quando for cumprida a condição do alerta Olá especificado.

## <a name="create-itsm-work-items-from-oms-logs"></a>Criar itens de trabalho ITSM a partir de registos do OMS

Pode criar itens de trabalho em origens de ITSM Olá ligado utilizando a pesquisa de registo do OMS. toodo Olá, utilize seguinte procedimento:

1. De **pesquisa registo**, procurar dados Olá necessário, selecione de detalhe de Olá e, em **Criar item de trabalho**.

    Olá **item de trabalho de ITSM criar** surge a janela:

    ![Ecrã de análise do registo](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Adicione os detalhes de Olá:

  - **Título do item de trabalho**: título para o item de trabalho de Olá.
  - **Descrição do item de trabalho**: uma descrição para o novo item de trabalho Olá.
  - **Afetados computador**: nome do computador olá onde estes dados de registo foi encontrados.
  - **Selecione a ligação**: ligação ITSM em que pretende toocreate este item de trabalho.
  - **Item de trabalho**: tipo de item de trabalho.

3. toouse um modelo de item de trabalho existente para um incidente, clique em **Sim** em **gerar item de trabalho baseado num modelo de Olá** opção e, em seguida, clique em **criar**.

    Ou,

    Clique em **não** se quiser tooprovide os valores personalizados.

4. Forneça os valores corretos Olá no Olá **contacte tipo**, **impacto**, **urgência**, **categoria**, e **Sub categoria**  caixas de texto e, em seguida, clique em **criar**.

item de trabalho de Olá será criado na Olá ITSM, que também pode ver no OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Resolver problemas de ligações de ITSM no OMS
1.  Se a ligação falha a partir IU da origem ligados e obter Olá **erro na ligação de guardar** da mensagem, Olá a seguir:
 - Em caso de ligações de ServiceNow, Cherwell e Provance, certifique-se a segredo de ID/cliente do nome de utilizador/palavra-passe e o cliente Olá introduzido corretamente para cada uma das ligações de Olá. Se Olá erro persistir, verifique se tem privilégios suficientes no Olá correspondente ITSM produto toomake Olá ligação.
 - No caso do Service Manager, certifique-se de que Olá Web aplicação for implementada com êxito e é criada a ligação híbrida. tooverify Olá é estabelecida ligação com êxito máquina do Olá no local do Service Manager, visite o URL da aplicação Web Olá conforme especificado na documentação de Olá para efetuar Olá [da ligação híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Se os dados a partir do ServiceNow não está a obter sincronizados na OMS, certifique-se de que essa instância do ServiceNow Olá não está suspenso. Isto poderá membros acontecer algum tempo no Olá instâncias de desenvolvimento do ServiceNow, se inativo. Outra forma, problema de Olá de relatório.
3.  Se os alertas são a obter desencadeados da OMS, mas os itens de trabalho não estão a obter criados no produto ITSM ou itens de configuração não estiver a obter itens de toowork criado/ligado ou para quaisquer informações genéricos, Olá a seguir:
 -  Solução do conector de gestão do serviço IT no portal do OMS pode ser utilizado tooget um resumo ligações/computador de trabalho itens/etc. Clique em mensagens de erro Olá no painel de estado de Olá, navegue demasiado**pesquisa de registo** e ver a ligação de Olá com erro de Olá utilizando detalhes da Olá na mensagem de erro de saudação.
 - diretamente pode ver informações de erros/relacionados Olá no Olá **pesquisa registo** página com *tipo = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Resolver problemas de implementação de aplicação de Web do Service Manager
1.  Em caso de problemas para implementação de aplicações web, certifique-se de que tem permissões suficientes na subscrição Olá mencionado toocreate/implementar recursos.
2.  Se **referência de objeto não definida tooinstance de um objeto** é apresentada a mensagem de erro durante a execução Olá [script](log-analytics-itsmc-service-manager-script.md) Certifique-se de que introduziu valores válidos em **configuração do utilizador**secção.
3.  Se falhar o espaço de nomes do toocreate service bus reencaminhamento, certifique-se de que Olá necessário fornecedor de recursos está registado na subscrição Olá. Se não registado manualmente criá-la de Olá portal do Azure. Também pode criá-la ao [criação da ligação híbrida Olá](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de Olá portal do Azure.


## <a name="contact-us"></a>Contacte-nos

Para consultas ou comentários sobre Olá conector de gestão de serviços de TI, contacte-nos [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Passos seguintes
[Adicionar ITSM produtos/serviços tooIT conector do serviço de gestão](log-analytics-itsmc-connections.md).
