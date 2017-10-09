---
title: "solução de mapa de aaaService Self-paced demonstração | Microsoft Docs"
description: "Mapa de serviço é uma solução no Operations Management Suite (OMS) que Deteta automaticamente os componentes da aplicação no Windows e comunicação entre os serviços de Olá sistemas Linux e mapas.  Esta é uma demonstração paced automática que explica utilizando tooidentify de mapa de serviço e diagnosticar um problema simulado numa aplicação web."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Demonstração personalizada do Operations Management Suite (OMS) - Mapa de Serviço
Esta é uma demonstração paced automática que explica utilizando Olá [solução de mapa de serviço](operations-management-suite-service-map.md) no Operations Management Suite (OMS) tooidentify e diagnosticar um problema simulado numa aplicação web.  Mapa de serviço Deteta automaticamente os componentes da aplicação em sistemas Windows e Linux e mapas Olá comunicação entre os serviços.  Consolida também dados recolhidos por outro tooassist de serviços do OMS no analisar o desempenho e identificar problemas.  Também iremos utilizar [pesquisas de registo na análise de registos](../log-analytics/log-analytics-log-searches.md) toodrill baixo nos dados recolhidos de problema de raiz do ordem tooidentify Olá.


## <a name="scenario-description"></a>Descrição do cenário
Apenas tiver recebido uma notificação de aplicação de Portal de cliente ACME Olá está a ter problemas de desempenho.  informações de apenas Olá que são que estes problemas iniciado sobre 4:00 am PST hoje.  Não inteiramente tem a certeza de que todos os componentes de Olá desse portal Olá está dependente exceto um conjunto de servidores web.  

## <a name="components-and-features-used"></a>Componentes e funcionalidades utilizados
- [Solução Mapa de Serviço](operations-management-suite-service-map.md)
- [Pesquisa de registos do Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Instruções

### <a name="1-connect-toohello-oms-experience-center"></a>1. Ligar toohello OMS experiência Center
Este percurso através de utiliza Olá [Operations Management Suite experiência Center](https://experience.mms.microsoft.com/) que fornece um ambiente do OMS completado com dados de exemplo. Comece por seguir esta ligação, forneça as informações e, em seguida, selecione Olá **informações e análises** cenário.


### <a name="2-start-service-map"></a>2. Iniciar Mapa de Serviço
Iniciar a solução de mapa de serviço Olá ao clicar no Olá **mapa de serviço** mosaico.

![Mosaico do Mapa de Serviço](media/operations-management-suite-walkthrough-servicemap/tile.png)

é apresentada a consola de mapa de serviço Olá.  Olá painel esquerdo é uma lista de computadores no seu ambiente com o agente de mapa de serviço Olá instalado.  Irá selecionar computador Olá que pretende que o tooview desta lista.

![Lista de computadores](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Ver computador
Sabemos que servidores de web de Olá são denominados AcmeWFE001 e AcmeWFE002, pelo que este parece um toostart local razoável.  Clique no **AcmeWFE001**.  Isto apresenta mapa Olá para AcmeWFE001 e todas as dependências dele.  Pode ver os processos em execução no computador selecionado Olá e que comunicam com os serviços externos.

![Servidor Web](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Estamos preocupados com desempenho Olá do nosso web aplicação, por isso, clique em Olá **AcmeAppPool (agrupamento de aplicações do IIS)** processo.  Isto apresenta detalhes de Olá para que este processo e realça as respetivas dependências.  

![Conjunto de Aplicações](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Alterar o período de tempo

Iremos falar esse problema Olá iniciado às 4:00, por isso, vamos ver que estava a acontecer nessa altura. Clique em **intervalo de tempo** e alterar Olá tempo too4: 00 AM PST (manter Olá data atual e ajustar o fuso horário local) com uma duração de 20 minutos.

![Selecionador de hora](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Ver alerta

Agora, Vemos que Olá **acmetomcat** dependência tem um alerta apresentado, pelo que é a nossa potencial problema.  Clique no ícone de alerta de Olá no **acmetomcat** detalhes de Olá tooshow para alerta de Olá.  Podemos ver que temos utilização crítica da CPU e podemos expandi-la para obter mais detalhes.  Isto é provavelmente o que está a causar a lentidão do nosso desempenho. 

![Alerta](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Ver desempenho

Vamos olhar de forma mais atenta para **acmetomcat**.  Clique na Olá superior direita do **acmetomcat** e selecione **carga servidor mapa** tooshow Olá detalhe e dependências para esta máquina. Iremos pode, em seguida, procure um pouco mais para esses tooverify de contadores de desempenho nosso suspeita.  Selecione Olá **desempenho** Olá do separador toodisplay [contadores de desempenho recolhidos pelo registo Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) ao longo do intervalo de tempo de Olá.  É possível ver que estamos a obter picos periódicos em Olá processador e memória.

![Desempenho](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Ver monitorização de alterações
Vamos ver se conseguimos perceber o que poderá ter causado esta utilização elevada.  Clique em Olá **resumo** separador.  Esta opção fornece informações que OMS tem recolhidas a partir do computador Olá como falha ligações, os alertas críticos e alterações de software.  Já deverão ser expandidas secções com interessantes informações recentes e pode expandir outras informações de tooinspect secções que contêm.


Se a **Monitorização de Alterações** ainda não estiver aberta, então expanda-a.  Isto mostra as informações recolhidas pelo Olá [solução de controlo de alterações](../log-analytics/log-analytics-change-tracking.md).  Parece que ocorreu uma alteração de software efetuada durante este período de tempo.  Clique em **Software** tooget detalhes.  Um processo de cópia de segurança foi adicionado toohello máquina apenas depois de 4 horas da Manhã, pelo que esta opção é apresentada culprit de Olá toobe para recursos excessivos de Olá consumida.

![Monitorização de alterações](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Ver detalhes na Pesquisa de Registos
Iremos pode verificar isto observando Olá mais informações de desempenho recolhidas no repositório de análise de registos de Olá detalhadas.  Clique em Olá **alertas** separador novamente e, em seguida, dos Olá **elevado da CPU** alertas.  Clique em **Mostrar na Pesquisa de Registos**.  Esta ação abre a janela de pesquisa de registo de olá onde pode efetuar [pesquisas de registo](../log-analytics/log-analytics-log-searches.md) em relação a quaisquer dados armazenados no repositório de Olá.  Mapa de serviço já preenchidos para-num queriy alerta de Olá tooretrieve estamos interessados.  

![Pesquisas de registos](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Abrir pesquisa guardada
Vamos ver se podemos pode obter alguns mais detalhadamente na recolha de desempenho de Olá que gerou este alerta e verificar o nosso suspeita que problemas Olá estão a ser provocados por esse processo de cópia de segurança.  Alterar o intervalo de tempo de Olá demasiado**6 horas**.  Em seguida, clique em **Favoritos** e desloque-se para baixo toohello guardado procura **mapa de serviço**.  Estas são as consultas que criámos especificamente para esta análise.  Clique em **Cinco processos principais pela CPU para acmetomcat**.

![Pesquisa guardada](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


Esta consulta devolve uma lista de Olá principais 5 processos a consumir do processador no **acmetomcat**.  Pode inspecionar Olá consulta tooget uma linguagem de consulta de toohello introdução utilizada para pesquisas de registo.  Se interessado em processos de Olá noutros computadores, pode modificar Olá consulta tooretrieve essas informações.

Neste caso, é possível ver o processo de cópia de segurança de Olá consistentemente está a consumir cerca de 60% de CPU do servidor de aplicação Olá.  É bastante óbvio que este novo processo é responsável pelo nosso problema de desempenho.  A nossa solução seria obviamente tooremove neste novo software de servidor de aplicação Olá de cópia de segurança.  Iremos foi realmente tirar partido do pretendido Estado Configuration (DSC) gerido pelas políticas de toodefine de automatização do Azure que certifique-se de que este processo é executado nunca nestes sistemas críticos.


## <a name="summary-points"></a>Pontos de resumo
- O [Mapa de Serviço](operations-management-suite-service-map.md) fornece-lhe uma vista da sua aplicação completa, mesmo se não conhecer todos os respetivos servidores e as dependências.
- Mapa de serviço analisa os dados recolhidos pelo outro toohelp de soluções do OMS identifica problemas com a sua aplicação e a respetiva infraestrutura subjacente.
- [Inicie sessão pesquisas](../log-analytics/log-analytics-log-searches.md) permitem-lhe toodrill para baixo em dados específicos recolhidos no repositório de análise de registos de Olá.    

## <a name="next-steps"></a>Passos seguintes
- Saiba mais sobre o [Mapa de Serviço](operations-management-suite-service-map.md).
- [Implemente e configure](operations-management-suite-service-map-configure.md) o Mapa de Serviço.
- Saiba mais sobre o [Log Analytics](../log-analytics/log-analytics-overview.md) que é necessário para o Mapa de Serviço e armazena dados operacionais armazenados por agentes.