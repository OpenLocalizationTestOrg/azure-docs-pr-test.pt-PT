---
title: aaaMonitor, diagnosticar e resolver problemas de armazenamento do Azure | Microsoft Docs
description: "Utilize as funcionalidades como o armazenamento, a análise do lado do cliente para o registo, e tooidentify outras ferramentas de terceiros, diagnosticar e resolver problemas relacionados com o Storage do Azure."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: d1e87d98-c763-4caa-ba20-2cf85f853303
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: fhryo-msft
ms.openlocfilehash: a33b3af7527223169be7cf3fed76c4765ff80e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Monitorizar, diagnosticar e resolver problemas do Armazenamento do Microsoft Azure
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Descrição geral
Diagnosticar e resolver problemas de uma aplicação distribuída alojada num ambiente de nuvem podem ser mais complexos do que em ambientes tradicionais. As aplicações podem ser implementadas numa infraestrutura PaaS ou IaaS, no local, num dispositivo móvel, ou numa combinação destas. Normalmente, o tráfego de rede da sua aplicação pode atravessar redes públicas e privadas e a aplicação pode utilizar várias tecnologias de armazenamento, como tabelas de armazenamento do Microsoft Azure, Blobs, filas ou ficheiros nos dados de tooother adição armazena, tais como relacional e bases de dados de documento.

toomanage essas aplicações com êxito, deve monitorizá-los de forma pró-ativa e compreender como toodiagnose e resolver problemas de todos os aspetos da-los e as tecnologias dependentes. Como um utilizador dos serviços de armazenamento do Azure, deve continuamente monitorizar os serviços de armazenamento de Olá a aplicação utiliza para efetuar quaisquer alterações inesperadas no comportamento (por exemplo, mais lenta do que os tempos de resposta habitual) e utilizar toocollect de registo mais detalhadas dados e tooanalyze um problema em profundidade. informações de diagnóstico de Olá que obter de monitorização e registo ajudará a toodetermine Olá causa de raiz Olá emitir a aplicação encontrada. Em seguida, pode resolver o problema de Olá e determinar os passos adequados de Olá que pode tomar tooremediate-lo. Armazenamento do Azure é um núcleo de serviço do Azure e constitui uma parte importante da maioria Olá das soluções que os clientes implementar toohello infraestrutura do Azure. Armazenamento do Azure inclui capacidades de monitorização de toosimplify, diagnosticar e resolver problemas de armazenamento nas suas aplicações baseado na nuvem.

> [!NOTE]
> Olá File storage do Azure não suporta o registo neste momento.
> 

Para uma guia prática tooend-a-ponto resolução de problemas em aplicações de armazenamento do Azure, consulte [ponto-a-ponto resolução de problemas com as métricas do Storage do Azure e o registo, o AzCopy e o Message Analyzer](storage-e2e-troubleshooting.md).

* [Introdução]
  * [Como este guia está organizado]
* [monitorização do seu serviço de armazenamento]
  * [Monitorização de estado de funcionamento do serviço]
  * [Capacidade de monitorização]
  * [Monitorização de disponibilidade]
  * [Monitorização do desempenho]
* [diagnosticar problemas de armazenamento]
  * [Problemas de estado de funcionamento de serviço]
  * [Problemas de desempenho]
  * [Erros de diagnóstico]
  * [Problemas de emulador de armazenamento]
  * [Ferramentas de registo de armazenamento]
  * [Utilizar ferramentas de registo de rede]
* [rastreio ponto-a-ponto]
  * [Correlacionar dados de registo]
  * [ID do pedido de cliente]
  * [ID do pedido de servidor]
  * [Carimbos]
* [orientações de resolução de problemas]
  * [métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]
  * [Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente Olá está com latência elevada]
  * [As métricas apresentam uma AverageServerLatency alta]
  * [Ocorrem atrasos inesperados na entrega de mensagens numa fila]
  * [métricas mostram um aumento no PercentThrottlingError]
  * [métricas mostram um aumento no PercentTimeoutError]
  * [As métricas apresentam um aumento do PercentNetworkError]
  * [cliente de Olá está a receber mensagens HTTP 403 (proibido)]
  * [cliente de Olá está a receber mensagens HTTP 404 (não for encontrado)]
  * [cliente de Olá está a receber mensagens de HTTP 409 (conflito)]
  * [métricas mostram PercentSuccess baixa ou entradas de registo de análise de ter operações com Estado de transação de ClientOtherErrors]
  * [Métricas de capacidade mostram um aumento inesperado na utilização da capacidade de armazenamento]
  * [Estão a experienciar inesperados reinícios das máquinas virtuais que tenham um grande número de VHDs ligados]
  * [O problema se for utilizar o emulador do storage Olá para programação ou testes]
  * [São encontrar problemas ao instalar Olá Azure SDK para .NET]
  * [Tem um problema com um serviço de armazenamento diferente]
  * [Resolução de problemas de armazenamento de ficheiros do Azure com o Windows e Linux](storage-troubleshoot-file-connection-problems.md)
* [Appendices]
  * [apêndice 1: utilizar o tráfego Fiddler toocapture HTTP e HTTPS]
  * [apêndice 2: com o Wireshark tráfego de rede de toocapture]
  * [apêndice 3: utilizar o tráfego de rede do Microsoft Message Analyzer toocapture]
  * [Apêndice 4: Utilizar tooview métricas e registo de dados do Excel]
  * [Apêndice 5: Monitorizar com o Application Insights para Visual Studio Team Services]

## <a name="introduction"></a>Introdução
Problemas relacionados com este mostra guia, como toouse funcionalidades como a análise de armazenamento do Azure, o registo do lado do cliente no Olá biblioteca de clientes do Storage do Azure e tooidentify outras ferramentas de terceiros, diagnosticar e resolver problemas de armazenamento do Azure.

![][1]

Este guia é toobe pretendido ler principalmente pelos programadores dos serviços online que utilizam serviços de armazenamento do Azure e os profissionais de TI responsáveis pela gestão desses serviços online. Olá objetivos deste guia são:

* toohelp manter o estado de funcionamento de Olá e o desempenho das suas contas do Storage do Azure.
* tooprovide-lhe processos necessários Olá e toohelp ferramentas decidir se um problema numa aplicação ou um problema relacionado com tooAzure armazenamento.
* tooprovide-lhe orientações acionável para resolver problemas relacionados com tooAzure armazenamento.

### <a name="how-this-guide-is-organized"></a>Como este guia está organizado
Olá a secção "[monitorização do seu serviço de armazenamento]" descreve como toomonitor Olá estado de funcionamento e desempenho dos seus serviços de armazenamento do Azure através de métricas de análise de armazenamento do Azure (as métricas do Storage).

Olá a secção "[diagnosticar problemas de armazenamento]" descreve como toodiagnose problemas com o Azure Storage Analytics registo (registo de armazenamento). Também descreve como utilizar o registo do lado do cliente tooenable hello instalações de uma das bibliotecas de cliente Olá, tais como Olá biblioteca de clientes de armazenamento para .NET ou Olá Azure SDK para Java.

Olá a secção "[rastreio ponto-a-ponto]" descreve como pode correlacionar informações Olá contidas em vários ficheiros de registo e dados de métricas.

Olá a secção "[orientações de resolução de problemas]" fornece orientações para resolução de problemas para algumas das Olá relacionadas com o armazenamento problemas comuns que poderá encontrar.

Olá "[Appendices]" incluem informações sobre como utilizar outras ferramentas, como o Wireshark e Netmon, para analisar dados de pacote, o Fiddler para analisar mensagens HTTP/HTTPS, de rede e o Microsoft Message Analyzer para correlacionar dados de registo.

## <a name="monitoring-your-storage-service"></a>O serviço de armazenamento de monitorização
Se estiver familiarizado com a monitorização de desempenho do Windows, pode considerar as métricas do Storage como sendo equivalente Storage do Azure de contadores de Monitor de desempenho do Windows. As métricas do Storage, encontrará um conjunto abrangente de métricas (contadores na terminologia de Monitor de desempenho do Windows), tais como a disponibilidade do serviço, o número total de pedidos tooservice ou percentagem de pedidos com êxito tooservice. Para obter uma lista completa das métricas disponíveis Olá, consulte [armazenamento esquema da tabela de métricas de análise](http://msdn.microsoft.com/library/azure/hh343264.aspx). Pode especificar se pretende que toocollect de serviço de armazenamento Olá e métricas de agregação hora a hora ou a cada minuto. Para obter mais informações sobre como tooenable métricas e monitorizar as contas do storage, consulte o artigo [ativar as métricas do storage e visualizar dados de métricas](http://go.microsoft.com/fwlink/?LinkId=510865).

Pode escolher quais as métricas de hora a hora que pretende toodisplay no Olá [portal do Azure](https://portal.azure.com) e configurar regras de notificar os administradores por e-mail sempre que uma métrica de hora a hora excede um limiar específico. Para obter mais informações, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). 

serviço de armazenamento Olá recolhe métricas de utilizar um melhor esforço, mas não pode registar cada operação de armazenamento.

No portal do Azure Olá, pode ver as métricas como disponibilidade, total de pedidos e números de latência média de uma conta de armazenamento. Uma regra de notificação também foi configurada tooalert administrador se disponibilidade descerem abaixo de um determinado nível. De ver estes dados, uma área possíveis para investigação está a ser inferior a 100% dos percentagem de êxito de serviço para tabela Olá (para obter mais informações, consulte a secção de Olá "[métricas mostram PercentSuccess baixa ou entradas de registo de análise de ter operações com Estado de transação de ClientOtherErrors]").

Deverá monitorizar continuamente a tooensure de aplicações do Azure são bom estado de funcionamento e desempenho, tal como esperado pelo:

* Estabelecer algumas métricas de linha de base para a aplicação que irão permitir-lhe dados atuais toocompare e identificar quaisquer alterações significativas no comportamento de Olá de armazenamento do Azure e a sua aplicação. valores de Olá das métricas de linha de base será, em muitos casos, aplicações específicas e deve estabelecer quando estiver a testar a aplicação de desempenho.
* Gravar métricas minutos e utilizá-los toomonitor ativamente para erros inesperados e anomalias como picos em contagens de erro ou taxas de pedidos.
* Gravar as métricas de hora a hora e a utilizá-los valores médios toomonitor como erro de contagens de média e taxas de pedidos.
* Investigar potenciais problemas de utilizar ferramentas de diagnóstico, tal como explicado posteriormente na secção de Olá "[diagnosticar problemas de armazenamento]."

gráficos Olá Olá imagem a seguir mostram como Olá média que ocorre a cada hora com base nas métricas pode ocultar picos na atividade. métricas de hora a hora de Olá aparecem tooshow uma taxa de pedidos, gradual ao minuto Olá métricas revelar flutuações de Olá que realmente estão a decorrer.

![][3]

Olá resto esta secção descreve as métricas, deve monitorizar e por que motivo.

### <a name="monitoring-service-health"></a>Monitorização de estado de funcionamento do serviço
Pode utilizar Olá [portal do Azure](https://portal.azure.com) Olá de estado de funcionamento do tooview Olá do serviço de armazenamento Olá (e outros serviços do Azure) em todas as regiões do Azure em torno Olá mundo. Isto permite-lhe toosee imediatamente se um problema fora do controlo está a afetar Olá serviço de armazenamento na região de Olá que utilizar para a sua aplicação.

Olá [portal do Azure](https://portal.azure.com) também pode fornecer notificações de incidentes que afetam Olá vários serviços do Azure.
Nota: Estas informações estavam anteriormente disponíveis, juntamente com os dados históricos, no Olá [Dashboard do serviço Azure](http://status.azure.com).

Ao hello [portal do Azure](https://portal.azure.com) informações de estado de funcionamento de recolhe de dentro de Olá centros de dados do Azure (monitorização do interior-out), pode também considerar que periodicamente a adotar uma abordagem no exterior toogenerate das transações sintéticas aceder à sua aplicação web alojado no Azure de várias localizações. Olá serviços oferecidos por [Dynatrace](http://www.dynatrace.com/en/synthetic-monitoring) e o Application Insights para Visual Studio Team Services são exemplos desta abordagem no exterior. Para mais informações sobre o Application Insights para Visual Studio Team Services, consulte o apêndice Olá "[apêndice 5: monitorizar com o Application Insights para Visual Studio Team Services](#appendix-5)."

### <a name="monitoring-capacity"></a>Capacidade de monitorização
As métricas do Storage apenas armazena as métricas de capacidade para o serviço de blob Olá porque blobs conta normalmente para proporção de maior Olá dos dados armazenados (momento Olá de escrita, não é possível toouse as métricas do Storage toomonitor Olá capacidade as tabelas e filas) . Pode encontrar estes dados Olá **$MetricsCapacityBlob** tabela se tiver ativado a monitorização para Olá serviço Blob. As métricas do Storage regista estes dados uma vez por dia, e pode utilizar o valor Olá Olá **RowKey** toodetermine se linha Olá contém uma entidade que está relacionada com a dados toouser (valor **dados**) ou (de dados de análise valor **análise**). Cada entidade armazenada contém informações sobre a quantidade de Olá de armazenamento utilizado (**capacidade** medido em bytes) e o número atual de Olá de contentores (**ContainerCount**) e os blobs ( **ObjectCount**) em utilização na conta de armazenamento Olá. Para obter mais informações sobre as métricas de capacidade de Olá armazenadas no Olá **$MetricsCapacityBlob** tabela, consulte [armazenamento esquema da tabela de métricas de análise](http://msdn.microsoft.com/library/azure/hh343264.aspx).

> [!NOTE]
> Deverá monitorizar estes valores para um aviso inicial que está a atingir os limites de capacidade de Olá da sua conta de armazenamento. No portal do Azure Olá, pode adicionar toonotify de regras de alerta se a utilização do armazenamento agregado excede ou fica abaixo limiares que especificar.
> 
> 

Para obter ajuda a estimar o tamanho de Olá de vários objetos de armazenamento, tais como blobs, consulte a mensagem de blogue de Olá [compreender Azure armazenamento faturação – largura de banda, as transações e a capacidade](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

### <a name="monitoring-availability"></a>Monitorização de disponibilidade
Deverá monitorizar disponibilidade Olá dos serviços de armazenamento Olá na sua conta de armazenamento através da monitorização valor Olá Olá **disponibilidade** coluna na Olá tabelas de métricas de hora a hora ou minutos — **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Olá **disponibilidade** coluna contém um valor de percentagem que indica a disponibilidade de Olá Olá do serviço de ou operação de Olá API representado por linha Olá (Olá **RowKey** mostra se a linha de Olá contém métricas para o serviço de Olá como um todo, ou para uma operação de API específica).

Qualquer valor inferior a 100% indica que alguns pedidos de armazenamento estão a falhar. Pode ver por que motivo falhar, examinando Olá outras colunas nos dados de métricas de Olá que mostram como números de Olá dos pedidos com tipos de erro diferente **ServerTimeoutError**. Deve esperar toosee **disponibilidade** enquadram-se temporariamente inferior a 100% por motivos como servidor transitório tempos limite enquanto serviço Olá move o pedido de partições de balanceamento de carga de toobetter; Olá repetir lógica na sua aplicação de cliente deve processar estas condições intermitentes. artigo de Olá [operações de registadas análise de armazenamento e as mensagens de estado](http://msdn.microsoft.com/library/azure/hh343260.aspx) listas Olá tipos de transação que inclui as métricas do Storage no respetivo **disponibilidade** cálculo.

No Olá [portal do Azure](https://portal.azure.com), pode adicionar regras de alerta toonotify se **disponibilidade** para um serviço está abaixo de um limiar que especificar.

Olá "[orientações de resolução de problemas]" secção deste guia descreve alguns armazenamento serviço problemas relacionados tooavailability comuns.

### <a name="monitoring-performance"></a>Monitorização do desempenho
desempenho de Olá toomonitor dos serviços de armazenamento Olá, pode utilizar Olá seguintes métricas de Olá hora a hora e minutos tabelas de métricas.

* Olá valores Olá **AverageE2ELatency** e **AverageServerLatency** colunas mostram o serviço de armazenamento de Olá de tempo médio de Olá ou tipo de operação de API está a demorar tooprocess pedidos. **AverageE2ELatency** é uma medida de latência de ponto-a-ponto que inclui o tempo de Olá decorrido o pedido de Olá tooread e enviar uma resposta de Olá num pedido de Olá adição toohello tempo decorrido tooprocess (assim inclui latência de rede depois Olá pedido serviço de armazenamento Olá atingir); **AverageServerLatency** é uma medida do tempo de processamento de Olá apenas e exclui, por conseguinte, qualquer latência de rede relacionadas com toocommunicating com cliente Olá. Consulte a secção de Olá "[métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]" mais tarde neste guia para um debate do motivo poderão existir uma diferença significativa entre estes dois valores.
* Olá valores Olá **TotalIngress** e **TotalEgress** colunas Mostrar quantidade total de Olá de dados, em bytes, futuras do tooand ficar fora do seu serviço de armazenamento ou através de um tipo de operação de API específico.
* Olá valores Olá **TotalRequests** coluna Mostrar Olá número de pedidos que Olá o serviço de armazenamento da operação de API está a receber. **TotalRequests** é Olá número total de pedidos que o serviço de armazenamento Olá recebe.

Normalmente, irá monitorizar alterações inesperado em qualquer um destes valores como um indicador de que tem um problema que requerem a investigação.

No Olá [portal do Azure](https://portal.azure.com), pode adicionar regras de alerta toonotify se qualquer uma das métricas de desempenho de Olá para este serviço descerem abaixo ou excede um limiar que especificar.

Olá "[orientações de resolução de problemas]" secção deste guia descreve alguns armazenamento serviço problemas relacionados tooperformance comuns.

## <a name="diagnosing-storage-issues"></a>Diagnosticar problemas de armazenamento
Existem várias formas que que pode tornar-se em consideração um problema ou um problema na sua aplicação, estas incluem:

* Uma falha de principais que faz com que trabalhar de toocrash ou toostop da aplicação Olá.
* As alterações significativas de valores de linha de base nas métricas Olá que está a monitorizar, tal como descrito na secção anterior Olá "[monitorização do seu serviço de armazenamento]."
* Relatórios de utilizadores da sua aplicação que algumas operações específica não foram concluída conforme esperado ou que algumas funcionalidades não está a funcionar.
* Erros gerados na aplicação que aparecem nos ficheiros de registo ou através de algum outro método de notificação.

Normalmente, serviços de armazenamento problemas relacionados tooAzure enquadram-se um dos quatro amplas categorias:

* A aplicação tem um problema de desempenho comunicados pelos seus utilizadores, ou revelado por alterações de métricas de desempenho de Olá.
* Não há um problema com a infraestrutura de armazenamento do Azure de Olá num ou mais regiões.
* Verificou um erro comunicado pelos seus utilizadores, ou revelado por um aumento de uma das métricas de contagem de erros de Olá, monitorizar a sua aplicação.
* Durante o desenvolvimento e teste, pode utilizar o emulador de armazenamento local Olá; poderá encontrar alguns problemas que se relacionam com especificamente toousage do emulador de armazenamento Olá.

Olá secções seguintes descrevem os passos de Olá deve seguir toodiagnose e resolver problemas em cada um destes quatro categorias. Olá a secção "[orientações de resolução de problemas]" mais adiante neste guia, fornece mais detalhes, para alguns problemas comuns que poderá encontrar.

### <a name="service-health-issues"></a>Problemas de estado de funcionamento de serviço
Problemas de estado de funcionamento de serviço normalmente estão fora do controlo. Olá [portal do Azure](https://portal.azure.com) fornece informações sobre quaisquer problemas em curso com serviços do Azure, incluindo os serviços de armazenamento. Se tiver optado por armazenamento Georredundante com acesso de leitura quando criou a conta de armazenamento, em seguida, no evento Olá dos seus dados indisponível na localização principal Olá, a aplicação foi possível mudar temporariamente toohello cópia só de leitura na localização secundária Olá. toodo, a aplicação deve ser capaz de tooswitch entre utilizando as localizações de armazenamento primário e secundário Olá e ser capaz de toowork no modo de funcionalidade reduzida com dados só de leitura. bibliotecas de cliente de armazenamento do Azure Olá permitem-lhe toodefine uma política de repetição pode ler a partir do armazenamento secundário no caso de falha de uma leitura de armazenamento primário. A aplicação também tem de toobe em atenção que os dados de Olá na localização secundária Olá são eventualmente consistentes. Para obter mais informações, consulte a mensagem de blogue de Olá [as opções de redundância do armazenamento do Azure e de armazenamento redundantes do acesso de leitura Georreplicação](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

### <a name="performance-issues"></a>Problemas de desempenho
desempenho de Olá de uma aplicação pode ser subjective, especialmente perspetiva de um utilizador. Por conseguinte, é importante toohave da linha de base métricas disponíveis toohelp identificar qual poderá haver um problema de desempenho. Vários fatores poderão afetar o desempenho de Olá de um serviço de armazenamento do Azure da perspetiva de aplicação de cliente Olá. Estes fatores podem operar no serviço de armazenamento Olá, no cliente Olá ou na infraestrutura de rede Olá; é então importante toohave uma estratégia para identificar a origem de Olá do problema de desempenho de Olá.

Depois de ter identificado localização provável de Olá das causas Olá problema de desempenho de Olá de métricas de Olá, pode, em seguida, utilize Olá registo ficheiros toofind detalhados toodiagnose de informações e resolver o problema de Olá adicional.

Olá a secção "[orientações de resolução de problemas]" mais adiante neste guia fornece mais informações sobre algumas comuns desempenho relacionado com problemas que poderá encontrar.

### <a name="diagnosing-errors"></a>Erros de diagnóstico
Os utilizadores da sua aplicação podem notificá-lo de erros reportados pela aplicação de cliente Olá. As métricas do Storage também regista contagens dos tipos de erro diferente de serviços de armazenamento como **NetworkError**, **ClientTimeoutError**, ou **AuthorizationError**. Enquanto as métricas do Storage apenas regista contagens dos tipos de erro diferente, pode obter mais detalhes sobre pedidos individuais, examinando o lado do servidor, do lado do cliente e registos de rede. Normalmente, código de estado HTTP de Olá devolvido pelo serviço de armazenamento Olá fornecem uma indicação do motivo pelo qual o pedido de Olá falhou.

> [!NOTE]
> Lembre-se de que deverá toosee alguns erros intermitentes: por exemplo, os erros devido a condições de rede tootransient ou erros de aplicações.
> 
> 

Olá recursos seguintes são úteis para compreender os códigos de erro e de estado relacionadas com o armazenamento:

* [Códigos de erro de API de REST comuns](http://msdn.microsoft.com/library/azure/dd179357.aspx)
* [Códigos de erro do serviço blob](http://msdn.microsoft.com/library/azure/dd179439.aspx)
* [Códigos de erro do serviço fila](http://msdn.microsoft.com/library/azure/dd179446.aspx)
* [Códigos de erro do serviço tabela](http://msdn.microsoft.com/library/azure/dd179438.aspx)
* [Códigos de erro do serviço de ficheiro](https://msdn.microsoft.com/library/azure/dn690119.aspx)

### <a name="storage-emulator-issues"></a>Problemas de emulador de armazenamento
Olá SDK do Azure inclui um emulador do storage que pode executar uma estação de trabalho de desenvolvimento. Este emulador simula maioria do comportamento de Olá dos serviços de armazenamento do Azure Olá e é útil durante a programação e teste, permitindo-lhe toorun as aplicações que utilizam serviços de armazenamento do Azure sem Olá é necessário para uma subscrição do Azure e uma conta de armazenamento do Azure.

Olá "[orientações de resolução de problemas]" secção deste guia descreve alguns problemas comuns encontrados utilizando o emulador do storage Olá.

### <a name="storage-logging-tools"></a>Ferramentas de registo de armazenamento
O registo de armazenamento fornece o registo do lado do servidor de pedidos de armazenamento na sua conta do storage do Azure. Para obter mais informações sobre como tooenable o registo do lado do servidor e Olá de acesso no registo de dados, consulte [aceder aos dados de registo e ativar o registo de armazenamento](http://go.microsoft.com/fwlink/?LinkId=510867).

Olá biblioteca de clientes de armazenamento para .NET permite-lhe dados de registo do lado do cliente do toocollect que está relacionada com operações de toostorage efetuadas pela sua aplicação. Para obter mais informações, consulte [do lado do cliente registo com Olá biblioteca de clientes do Storage .NET](http://go.microsoft.com/fwlink/?LinkId=510868).

> [!NOTE]
> Em algumas circunstâncias (como falhas de autorização de SAS), um utilizador poderá reportar um erro para o qual pode encontrar sem dados de pedido no Olá os registos de armazenamento do lado do servidor. Pode utilizar as capacidades de registo de Olá de Olá biblioteca de clientes de armazenamento tooinvestigate se causa Olá problema de Olá no cliente Olá ou utilizar a rede de Olá tooinvestigate de ferramentas de monitorização de rede.
> 
> 

### <a name="using-network-logging-tools"></a>Utilizar ferramentas de registo de rede
Pode capturar o tráfego de Olá entre Olá o cliente e servidor tooprovide detalhada sobre a Olá dados Olá cliente e servidor são trocar e Olá subjacente condições de rede. Ferramentas de registo de rede útil incluem:

* [Fiddler](http://www.telerik.com/fiddler) é uma web livre depuração proxy que permite os cabeçalhos de Olá tooexamine e os dados do payload de mensagens de pedido e resposta HTTP e HTTPS. Para obter mais informações, consulte [apêndice 1: o tráfego utilizando o Fiddler toocapture HTTP e HTTPS](#appendix-1).
* [Monitor de rede da Microsoft (Netmon)](http://www.microsoft.com/download/details.aspx?id=4865) e [Wireshark](http://www.wireshark.org/) é rede livre analisadores de protocolo que lhe permitem tooview informações detalhadas do pacote de uma vasta gama de protocolos de rede. Para mais informações sobre o Wireshark, consulte "[apêndice 2: o tráfego de rede utilizando o Wireshark toocapture](#appendix-2)".
* Microsoft Message Analyzer é uma ferramenta da Microsoft que substitui Netmon que além toocapturing de rede e dados do pacote, ajuda-o a tooview e analisar dados de registo de Olá capturados a partir de outras ferramentas. Para obter mais informações, consulte "[apêndice 3: o tráfego de rede utilizando o Microsoft Message Analyzer toocapture](#appendix-3)".
* Se quiser tooperform um toocheck de teste de conectividade básica que o seu computador cliente pode ligar toohello serviço de armazenamento do Azure através de rede de Olá, fazê-lo não é possível utilizar o padrão de Olá **ping** ferramenta no cliente Olá. No entanto, pode utilizar Olá [ **tcping** ferramenta](http://www.elifulkerson.com/projects/tcping.php) toocheck conectividade.

Em muitos casos, os dados de registo Olá do registo de armazenamento e biblioteca de clientes de armazenamento de Olá serão suficiente toodiagnose um problema mas, em alguns cenários, poderá ser necessário Olá que informações que estas ferramentas de registo de rede podem fornecer mais detalhadas. Por exemplo, utilizar o Fiddler tooview permite que as mensagens HTTP e HTTPS tooview cabeçalho e o payload de dados enviados tooand do Olá os serviços de armazenamento, seriam ativar tooexamine como uma aplicação de cliente tentará novamente operações de armazenamento. Analisadores de protocolo, tais como o Wireshark operam ao nível do pacote de Olá, permitindo-lhe dados TCP de tooview, seriam ativar tootroubleshoot perda de pacotes e problemas de conectividade. Analisador de mensagens pode operar em camadas HTTP e TCP.

## <a name="end-to-end-tracing"></a>Rastreio de ponto a ponto
Utilizando uma variedade de ficheiros de registo de rastreio de ponto a ponto é uma técnica útil para investigar potenciais problemas. Pode utilizar informações de data/hora Olá dos seus dados de métricas como uma indicação de informações que o irão ajudar a resolver o problema de Olá detalhadas de toostart procurar nos ficheiros de registo de Olá para Olá de onde.

### <a name="correlating-log-data"></a>Correlacionar dados de registo
Ao visualizar registos de aplicações de cliente, rastreios rede e armazenamento do lado do servidor de registo é crítico toobe toocorrelate capaz de pedidos em Olá diferentes ficheiros de registo. ficheiros de registo Olá incluem um número de diferentes campos que são úteis como identificadores de correlação. id do pedido de cliente de Olá é Olá mais úteis campo toouse toocorrelate entradas nos registos de diferentes Olá. No entanto, por vezes, pode ser útil toouse id de pedido do servidor de Olá ou carimbos. Olá secções seguintes fornecem mais detalhes sobre estas opções.

### <a name="client-request-id"></a>ID do pedido de cliente
Biblioteca de clientes de armazenamento de Olá gera automaticamente um id de pedido de cliente exclusivos para cada pedido.

* Olá registo do lado do cliente que Olá biblioteca de clientes de armazenamento cria, id de pedido de cliente Olá aparece no Olá **ID do pedido de cliente** campo cada entrada de registo relacionadas com toohello pedido.
* Um rastreio de rede, tais como um capturado por Fiddler, id de pedido de cliente Olá é visível em mensagens de pedido como Olá **x-ms-client-request-id** valor de cabeçalho HTTP.
* No registo de registo do armazenamento de lado do servidor de Olá, id de pedido de cliente Olá é apresentado na coluna de ID de pedido de cliente Olá.

> [!NOTE]
> É possível vários pedidos tooshare Olá mesmo id de pedido de cliente, porque o cliente de Olá pode atribuir este valor (embora Olá biblioteca de clientes de armazenamento atribui automaticamente um novo valor). No caso de Olá de tentativas de cliente de Olá, todas as tentativas partilham Olá mesmo id de pedido de cliente. Olá maiúsculas e minúsculas de um lote enviado pelo cliente de Olá, lote de Olá tem um id de pedido de cliente único.
> 
> 

### <a name="server-request-id"></a>ID de pedido do servidor
serviço de armazenamento Olá gera automaticamente os ids de pedido do servidor.

* No registo de registo do armazenamento de lado do servidor de Olá, id de pedido do servidor de Olá aparece Olá **cabeçalho de ID do pedido** coluna.
* No rastreio de rede, tais como um capturado por Fiddler, id de pedido do servidor de Olá aparece nas mensagens de resposta como Olá **x-ms-request-id** valor de cabeçalho HTTP.
* Olá registo do lado do cliente que Olá biblioteca de clientes de armazenamento cria, id de pedido do servidor de Olá aparece no Olá **operação texto** coluna para a entrada de registo de Olá que mostra detalhes de resposta do servidor Olá.

> [!NOTE]
> serviço de armazenamento Olá sempre atribui um servidor único pedido de tooevery do id do pedido recebe, para que cada tentativa de repetição do cliente de Olá e cada operação incluído num batch tem um id de pedido de servidor único.
> 
> 

Se hello biblioteca de clientes de armazenamento emite um **StorageException** no cliente Olá, Olá **RequestInformation** propriedade contém um **RequestResult** objeto que inclui um **ServiceRequestID** propriedade. Também pode aceder um **RequestResult** objeto a partir de um **OperationContext** instância.

exemplo de código Olá abaixo demonstra como tooset personalizadas **ClientRequestId** valor ao anexar um **OperationContext** serviço de armazenamento do Olá pedido toohello de objeto. Também mostra como tooretrieve Olá **ServerRequestId** valor a partir da mensagem de resposta de saudação.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Carimbos
Também pode utilizar carimbos toolocate relacionadas com as entradas de registo, mas tenha o cuidado de qualquer relógio dissimetrias entre Olá cliente e o servidor que pode existir. Deve procurar mais ou menos de 15 minutos para que correspondam a entradas do lado do servidor com base no Olá timestamp no cliente Olá. Lembre-se esses metadados de blob Olá para blobs Olá métricas que contêm indica o intervalo de tempo de Olá armazenados no blob Olá; com base nas métricas Olá Isto é útil se tiver várias métricas blobs para Olá mesmo minuto ou hora.

## <a name="troubleshooting-guidance"></a>Documentação de orientação de resolução de problemas
Nesta secção irão ajudá-lo diagnóstico Olá e resolução de problemas de alguns dos problemas comuns de Olá a aplicação poderá encontrar ao utilizar os serviços de armazenamento do Azure Olá. Utilize a lista de Olá abaixo problema específico do toolocate Olá informações tooyour relevantes.

**Resolução de problemas da árvore de decisões**

---
O problema se relacionam toohello desempenho de um dos serviços de armazenamento Olá?

* [métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]
* [Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente Olá está com latência elevada]
* [As métricas apresentam uma AverageServerLatency alta]
* [Ocorrem atrasos inesperados na entrega de mensagens numa fila]

---
O problema relacionadas com a disponibilidade de toohello de um dos serviços de armazenamento Olá?

* [métricas mostram um aumento no PercentThrottlingError]
* [métricas mostram um aumento no PercentTimeoutError]
* [As métricas apresentam um aumento do PercentNetworkError]

---
 A aplicação cliente recebe uma resposta de 4XX (por exemplo, 404) HTTP um serviço de armazenamento?

* [cliente de Olá está a receber mensagens HTTP 403 (proibido)]
* [cliente de Olá está a receber mensagens HTTP 404 (não for encontrado)]
* [cliente de Olá está a receber mensagens de HTTP 409 (conflito)]

---
[métricas mostram PercentSuccess baixa ou entradas de registo de análise de ter operações com Estado de transação de ClientOtherErrors]

---
[Métricas de capacidade mostram um aumento inesperado na utilização da capacidade de armazenamento]

---
[Estão a experienciar inesperados reinícios das máquinas virtuais que tenham um grande número de VHDs ligados]

---
[O problema se for utilizar o emulador do storage Olá para programação ou testes]

---
[São encontrar problemas ao instalar Olá Azure SDK para .NET]

---
[Tem um problema com um serviço de armazenamento diferente]

---
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Métricas mostram AverageE2ELatency alta e baixa AverageServerLatency
Olá ilustração abaixo de Olá [portal do Azure](https://portal.azure.com) monitorização ferramenta mostra um exemplo em que hello **AverageE2ELatency** é significativamente maior Olá **AverageServerLatency**.

![][4]

Tenha em atenção que o serviço de armazenamento Olá calcula apenas métrica Olá **AverageE2ELatency** para pedidos com êxito e, ao contrário **AverageServerLatency**, inclui o tempo de Olá cliente Olá demora toosend Olá dados e receber a confirmação do serviço de armazenamento Olá. Por conseguinte, terá uma diferença entre **AverageE2ELatency** e **AverageServerLatency** pode ser um devido a aplicação de cliente de toohello a ser lenta toorespond ou tooconditions devida na rede de Olá.

> [!NOTE]
> Também pode ver **E2ELatency** e **ServerLatency** para operações de armazenamento individuais em Olá registo de armazenamento de dados de registo.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Investigar problemas de desempenho do cliente
Razões possíveis para o cliente de Olá responder lentamente incluem a falta de recursos, tais como CPU, memória ou a rede de largura de banda ou ter um número limitado de ligações disponíveis ou threads. Poderá estar tooresolve capaz de problema de Olá modificando Olá cliente código toobe mais eficiente (por exemplo através da utilização serviço de armazenamento de toohello chamadas assíncronas) ou através de uma Máquina Virtual maior (com mais memória e mais núcleos).

Para os serviços de tabela e fila de Olá, algoritmo de Nagle Olá pode também fazer com que alta **AverageE2ELatency** como em comparação com demasiado**AverageServerLatency**: Para mais informações consulte Olá publique [do Nagle Algoritmo não é amigável para pedidos de pequenas](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx). Pode desativar o algoritmo de Nagle Olá no código utilizando Olá **ServicePointManager** a classe de Olá **System.Net** espaço de nomes. Deve fazê-lo antes de efetuar qualquer tabela de toohello chamadas ou serviços da fila na sua aplicação, uma vez que isto não afeta as ligações que já estão a abrir. Olá seguinte exemplo provém de Olá **Application_Start** método numa função de trabalho.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Deve verificar Olá registos do lado do cliente toosee quantos pedidos da aplicação de cliente é submeter e verifique a existência .NET geral relacionadas com congestionamentos de desempenho no seu cliente, tais como CPU, libertação da memória de .NET, a utilização da rede ou memória. Como um ponto de partida para aplicações de cliente .NET de resolução de problemas, consulte [Debugging, rastreio e criação de perfis](http://msdn.microsoft.com/library/7fe0dd2y).

#### <a name="investigating-network-latency-issues"></a>Investigar problemas de latência de rede
Normalmente, latência elevada de ponto a ponto causada por rede Olá é devido a condições de tootransient. Pode investigar ambos os problemas de rede transitórios e persistente, tais como pacotes ignorados, utilizando ferramentas como Wireshark ou o Microsoft Message Analyzer.

Para obter mais informações sobre como utilizar o Wireshark tootroubleshoot problemas da rede, consulte "[apêndice 2: com o Wireshark tráfego de rede de toocapture]."

Para obter mais informações sobre a utilização de problemas de rede do Microsoft Message Analyzer tootroubleshoot, consulte "[apêndice 3: utilizar o tráfego de rede do Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente Olá está com latência elevada
Neste cenário, a causa mais provável Olá é um atraso na Olá pedidos de armazenamento atingir o serviço de armazenamento Olá. Deve investigar por que motivo pedidos de cliente de Olá são não tornando-o através do serviço blob toohello.

Uma razão possível para o cliente de Olá atrasando enviar pedidos é o que há um número limitado de ligações disponíveis ou threads.

Também deve verificar se o cliente de Olá é efetuar várias tentativas e investigue o motivo de Olá se for este caso de Olá. toodetermine se o cliente de Olá está a efetuar várias tentativas, pode:

* Examine os registos de análise de armazenamento Olá. Se várias tentativas estavam a acontecer, verá várias operações com Olá o mesmo ID de pedido de cliente, mas com um servidor diferente do pedido IDs.
* Examine os registos de cliente Olá. O registo verboso indicará que ocorreu uma repetição.
* Depurar o seu código e verifique as propriedades de Olá de Olá **OperationContext** objeto associado ao pedido de Olá. Se a operação de Olá repetiu, Olá **RequestResults** propriedade incluirá o pedido de servidor exclusivo vários IDs. Também pode verificar o início de Olá e fim de cada pedido. Para obter mais informações, consulte o código de exemplo Olá na secção de Olá [ID do pedido de servidor].

Se existirem não existem problemas no cliente Olá, deve investigar potenciais problemas de rede, tais como a perda de pacotes. Pode utilizar as ferramentas, como problemas de rede tooinvestigate Wireshark ou Microsoft Message Analyzer.

Para obter mais informações sobre como utilizar o Wireshark tootroubleshoot problemas da rede, consulte "[apêndice 2: com o Wireshark tráfego de rede de toocapture]."

Para obter mais informações sobre a utilização de problemas de rede do Microsoft Message Analyzer tootroubleshoot, consulte "[apêndice 3: utilizar o tráfego de rede do Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-high-AverageServerLatency"></a>Métricas mostram AverageServerLatency elevada
No caso de Olá de alta **AverageServerLatency** para pedidos de transferência de blob, deve utilizar Olá armazenamento registo registos toosee se existirem pedidos repetidos de Olá mesmo blob (ou conjunto de blobs). Para o blob de carregar pedidos, deve investigar os blocos que tamanho Olá cliente está a utilizar (por exemplo, blocos inferior a 64 KB de tamanho pode resultar em sobrecargas, a menos que lê Olá estão a também ser inferior a 64K segmentos), e se vários clientes estiver a carregar bloqueia toohello mesmo Blob em paralelo. Também deverá verificar as métricas de por minuto de Olá para picos no número de Olá de pedidos que resultam exceder Olá por segundo metas de escalabilidade: também ver "[métricas mostram um aumento no PercentTimeoutError]."

Se vir alto **AverageServerLatency** para pedidos de transferência do blob quando existe são repetidos pedidos Olá mesmo blob ou um conjunto de blobs, em seguida, deve considerar a colocação em cache estas blobs com a Cache do Azure ou Olá entrega de conteúdos do Azure Rede (CDN). Para pedidos de carregamento, pode melhorar o débito de Olá utilizando um tamanho de bloco maior. Para consultas tootables, é também possível tooimplement do lado do cliente a colocação em cache em clientes que realizam Olá mesmo operações de consulta e olá onde os dados não mudam frequentemente.

Elevada **AverageServerLatency** valores também podem ser um sintoma de tabelas mal concebidas ou acrescentar/preceder anti padrão de consultas que o resultado das operações de análise ou que siga Olá. Consulte "[métricas mostram um aumento no PercentThrottlingError]" para obter mais informações.

> [!NOTE]
> Pode encontrar uma lista de verificação abrangente desempenho lista de verificação aqui: [desempenho de armazenamento do Microsoft Azure e a lista de verificação de escalabilidade](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Ocorrerem atrasos inesperados na entrega de mensagens numa fila
Se um atraso entre a hora de Olá uma aplicação adiciona uma mensagem tooa fila e Olá tempo torna-se disponíveis tooread da fila de Olá, em seguida, que deve tomar Olá problema de Olá toodiagnose de passos a seguir:

* Certifique-se a aplicação Olá é adicionar com êxito a fila de toohello Olá mensagens. Verifique a aplicação Olá não está a repetir Olá **AddMessage** método várias vezes antes de ter êxito. os registos de biblioteca de clientes de armazenamento Olá mostrará quaisquer tentativas repetidas das operações de armazenamento.
* Certifique-se de que não há nenhum relógio dissimetrias entre a função de trabalho de Olá que adiciona a fila de toohello Olá mensagens e a função de trabalho de Olá que lê a mensagem de saudação da fila de Olá que faz com que são apresentadas como se houver um atraso no processamento.
* Verifique se a função de trabalho de Olá que lê mensagens hello da fila de Olá é falhar. Se um cliente de fila chama Olá **GetMessage** método falhar, mas toorespond com uma confirmação, mensagem de saudação continuará invisível em fila Olá até Olá **invisibilityTimeout** do período. Neste momento, a mensagem de saudação fica disponível para processar novamente.
* Verifique se o comprimento da fila Olá é crescer ao longo do tempo. Isto pode ocorrer se não tiver tooprocess disponíveis suficientes do workers, todos os Olá mensagens outros funcionários estão a colocar em fila Olá. Também deve consultar Olá métricas toosee se estão a falhar pedidos de eliminação e Olá anular contagem de mensagens, que pode indicar repetido a mensagem de saudação toodelete tentativas falhadas.
* Examine Olá registos de registo de armazenamento para as operações de fila que tenham superior que o esperado **E2ELatency** e **ServerLatency** valores ao longo de um período de tempo que o habitual.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Métricas mostram um aumento no PercentThrottlingError
Limitação erros ocorrem quando exceder os objetivos de escalabilidade Olá de um serviço de armazenamento. serviço de armazenamento Olá não esta tooensure que nenhum cliente único ou inquilino pode utilizar o serviço de Olá em despesa Olá de terceiros. Para obter mais informações, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md) para obter detalhes sobre metas de desempenho para partições dentro de contas de armazenamento e os objetivos de escalabilidade para contas de armazenamento.

Se hello **PercentThrottlingError** métrica apresentar um aumento na percentagem de Olá de pedidos que estão a falhar com um erro de limitação, tem de tooinvestigate um dos dois cenários:

* [Aumento transitório PercentThrottlingError]
* [Aumento permanente PercentThrottlingError erro]

Um aumento de **PercentThrottlingError** ocorre frequentemente em Olá mesma hora como um aumento no número de Olá de pedidos de armazenamento ou quando são inicialmente carregar testar a sua aplicação. Isto pode também manifesto do próprio no cliente Olá como "503 servidor ocupado" ou mensagens de estado HTTP "500 tempo limite da operação" de operações de armazenamento.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Aumento transitório PercentThrottlingError
Se vir picos no valor Olá **PercentThrottlingError** que a operação com períodos de grande atividade para a aplicação Olá, deve implementar um back exponencial (não linear) desativar estratégia para tentativas no seu cliente: Isto irá reduzir a carga de imediato Olá na partição de Olá e ajudar a sua toosmooth aplicação os picos de tráfego. Para obter mais informações sobre como as políticas de repetição de tooimplement utilizando Olá biblioteca de clientes de armazenamento, consulte [Microsoft.WindowsAzure.Storage.RetryPolicies espaço de nomes](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx).

> [!NOTE]
> Também poderá ver picos no valor Olá **PercentThrottlingError** que não a operação com períodos de grande atividade para a aplicação Olá: Olá aqui na causa mais provável é o serviço de armazenamento de Olá mover partições tooimprove carga balanceamento.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Aumento permanente PercentThrottlingError erro
Se vir um valor consistentemente elevado para **PercentThrottlingError** seguir um aumento permanente os volumes de transação, ou quando estiver a efetuar o carregamento inicial testes na sua aplicação, em seguida, terá de tooevaluate como a aplicação está a utilizar as partições de armazenamento e se está a aproximar-se os objetivos de escalabilidade Olá para uma conta de armazenamento. Por exemplo, se vir a limitação de erros de uma fila (que conta como uma única partição), em seguida, deve considerar a utilização transações de Olá filas adicionais toospread entre várias partições. Se vir limitação erros numa tabela, terá de tooconsider um toospread de esquema de criação de partições diferente a utilizar as suas transações entre várias partições através da utilização de uma vasta gama de valores de chave de partição. Uma causa comum deste problema é Olá preceder/acrescentar o padrão de anti onde selecionou data Olá como chave de partição Olá e, em seguida, todos os dados num dia específico é escrito tooone partição: sob carga, isto pode resultar num estrangulamento de escrita. Deve considerar uma estrutura de criação de partições diferente ou avaliar se utilizando o blob storage pode ser a melhor solução. Também deve verificar se a limitação de Olá está a ocorrer em resultado picos de tráfego e investigar formas de suavização seu padrão de pedidos.

Deve ser em consideração os limites de escalabilidade Olá definido para a conta de armazenamento Olá se distribuir as suas transações entre várias partições. Por exemplo, se utilizou as dez filas cada máximo de Olá de processamento de 2.000 1KB mensagens em fila por segundo, serão no Olá limite geral de 20.000 mensagens em fila por segundo Olá conta de armazenamento. Se precisar de tooprocess mais de 20.000 entidades por segundo, deve considerar a utilização de várias contas de armazenamento. Deve também tenha em consideração esse tamanho Olá dos seus pedidos e entidades tem um impacto no quando o serviço de armazenamento Olá acelera os seus clientes: Se tiver o maior pedidos e as entidades, pode ser limitadas mais cedo.

Estrutura da consulta ineficaz pode também fazer com que os limites de escalabilidade de Olá toohit para partições de tabela. Por exemplo, uma consulta com um filtro que seleciona apenas uma percentagem de entidades de Olá numa partição, mas que analisa todas as entidades de Olá numa partição terá tooaccess cada entidade. Cada entidade ler contabilizará um número total de Olá de transações em dessa partição; Por conseguinte, pode facilmente alcançar os objetivos de escalabilidade Olá.

> [!NOTE]
> Os testes de desempenho devem ficar a saber de qualquer estruturas de consulta ineficaz na sua aplicação.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Métricas mostram um aumento no PercentTimeoutError
Métricas de apresentar um aumento no **PercentTimeoutError** para um dos seus serviços de armazenamento. Em Olá mesmo tempo, hello cliente recebe um elevado volume de mensagens de estado HTTP "500 tempo limite da operação" de operações de armazenamento.

> [!NOTE]
> Poderá ver erros de tempo limite temporariamente como serviço de armazenamento de Olá a carga de pedidos de saldos movendo um partição tooa novo servidor.
> 
> 

Olá **PercentTimeoutError** métrica é uma agregação de Olá seguir métricas: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, e **SASServerTimeoutError**.

tempos limite de servidor Olá são causados por um erro no servidor de Olá. tempos limite de cliente Olá acontecer porque uma operação no servidor de Olá excedeu o tempo limite de Olá especificado pelo cliente de Olá; Por exemplo, um cliente utilizando Olá biblioteca de clientes de armazenamento pode definir o limite de tempo para uma operação utilizando Olá **ServerTimeout** propriedade Olá **QueueRequestOptions** classe.

Tempos limite de servidor indicarem um problema com o serviço de armazenamento de Olá que requerem a investigação. Pode utilizar as métricas toosee se são atingir os limites de escalabilidade de Olá para serviço Olá e tooidentify qualquer picos de tráfego que poderá estar a causar o problema. Se o problema de Olá intermitente, pode ser devido balanceamento tooload atividade no serviço de Olá. Se o problema de Olá é persistente e não é causado pela sua aplicação atingir os limites de escalabilidade Olá do serviço de Olá, deve aumentar um problema de suporte. Para tempos limite de cliente, tem de decidir se Olá limite de tempo definido valor adequado tooan em cliente Olá e Olá ou altera o valor do tempo limite definido no cliente Olá ou investigar a forma como pode melhorar o desempenho de Olá das operações de Olá no serviço de armazenamento Olá, para exemplo por otimizar as consultas de tabela ou reduzir o tamanho de Olá das mensagens.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Métricas mostram um aumento no PercentNetworkError
Métricas de apresentar um aumento no **PercentNetworkError** para um dos seus serviços de armazenamento. Olá **PercentNetworkError** métrica é uma agregação de Olá seguir métricas: **NetworkError**, **AnonymousNetworkError**, e  **SASNetworkError**. Estes ocorrerem quando o serviço de armazenamento Olá Deteta um erro de rede quando Olá cliente faz um pedido de armazenamento.

Olá causa mais comum deste erro é um cliente desligar antes de um tempo limite expira no serviço de armazenamento Olá. Deve investigar código Olá no seu toounderstand de cliente por que razão e quando o cliente de Olá desligar do serviço de armazenamento Olá. Também pode utilizar o Wireshark, Microsoft Message Analyzer ou Tcping problemas de conectividade de rede tooinvestigate do cliente de Olá. Estas ferramentas estão descritas em Olá [Appendices].

### <a name="the-client-is-receiving-403-messages"></a>cliente de Olá está a receber mensagens HTTP 403 (proibido)
Se a aplicação cliente que está a gerar erros de HTTP 403 (proibido), uma causa provável é que o cliente Olá estiver a utilizar um expirada acesso assinatura partilhado (SAS) quando envia um pedido de armazenamento (embora outras causas possíveis incluem as chaves inválido, dissimetrias do relógio e vazio cabeçalhos). Se uma chave SAS expirada causa Olá, não visualizará quaisquer entradas de dados de registo do registo de armazenamento de lado do servidor da Olá. Olá tabela seguinte mostra um exemplo do registo do lado do cliente Olá gerado pelo Olá biblioteca de clientes do Storage que ilustra a ocorrer este problema:

| Origem | Verbosidade | Verbosidade | Id do pedido de cliente | Texto de operação |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-... |Iniciar a operação com a localização principal por PrimaryOnly do modo de localização. |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-... |Iniciar síncrona pedido toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;Tama = mypolicy&amp;sig = OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-... |A aguardar resposta. |
| Microsoft.WindowsAzure.Storage |Aviso |2 |85d077ab-... |Excepção emitida ao aguardar pela resposta: Olá o servidor remoto devolveu um erro: proibido (403)... |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-... |Resposta recebida. Código de estado = 403, ID do pedido = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = ETag =. |
| Microsoft.WindowsAzure.Storage |Aviso |2 |85d077ab-... |Ocorreu uma excepção durante a operação de Olá: Olá o servidor remoto devolveu um erro: proibido (403)... |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-... |A verificar se a operação de Olá deve ser repetida. Contagem de tentativas = 0, código de estado HTTP 403, exceção de = = Olá de servidor remoto devolvida um erro: proibido (403)... |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-... |foi definida a localização seguinte do Olá tooPrimary, com base no modo de localização de Olá. |
| Microsoft.WindowsAzure.Storage |Erro |1 |85d077ab-... |Política de repetição não permitiu para uma nova tentativa. Falha do servidor remoto Olá devolveu um erro: proibido (403). |

Neste cenário, deve investigar por que motivo Olá SAS token irá expirar antes do cliente de Olá envia o servidor de token toohello Olá:

* Normalmente, não deverá definir uma hora de início quando cria um SAS para um cliente toouse imediatamente. Se existirem pequeno relógio diferenças entre o anfitrião de Olá gerar através de SAS Olá Olá hora atual e o serviço de armazenamento de Olá, em seguida, é possível Olá armazenamento serviço tooreceive uma SAS que ainda não é válida.
* Não deve definir um período de tempo muito curto expiração numa SAS. Novamente, relógio pequeno as diferenças entre os anfitriões de Olá gerar Olá SAS e o serviço de armazenamento Olá pode levar tooa SAS parecer expira anteriormente que o antecipado.
* Olá parâmetro de versão na chave SAS Olá (por exemplo **sv = 2015-04-05**) versão Olá de correspondência de Olá biblioteca de clientes do Storage que está a utilizar? Recomendamos que utilize sempre a versão mais recente do Olá do Olá [biblioteca de clientes de armazenamento](https://www.nuget.org/packages/WindowsAzure.Storage/).
* Se voltar a gerar as chaves de acesso de armazenamento, isto pode invalidar quaisquer tokens SAS existentes. Isto pode ser um problema se gerar tokens SAS com um tempo de expiração longo para toocache de aplicações de cliente.

Se estiver a utilizar tokens de SAS do Olá biblioteca de clientes de armazenamento toogenerate, em seguida, é fácil toobuild um token válido. No entanto, se estiver a utilizar Olá API REST do Storage e construir manualmente os tokens SAS Olá deve lê tópico Olá [delegar o acesso com uma assinatura de acesso partilhado](http://msdn.microsoft.com/library/azure/ee395415.aspx).

### <a name="the-client-is-receiving-404-messages"></a>cliente de Olá está a receber mensagens HTTP 404 (não for encontrado)
Se a aplicação de cliente Olá recebe uma mensagem de HTTP 404 (não for encontrado) do servidor de Olá, isto implica que Olá objeto Olá o cliente foi tentar toouse (por exemplo, uma entidade, tabelas, BLOBs, contentor ou filas) não existe no serviço de armazenamento Olá. Há uma série de razões possíveis para tal, tais como:

* [cliente de Olá ou outro objeto de Olá de processo eliminado anteriormente]
* [Um problema de autorização de assinatura de acesso partilhado (SAS)]
* [No código JavaScript do lado do cliente não tem o objeto de permissão de tooaccess Olá]
* [Falha de rede]

#### <a name="client-previously-deleted-the-object"></a>cliente de Olá ou outro objeto de Olá de processo eliminado anteriormente
Em cenários onde Olá cliente está a tentar tooread, atualização ou eliminação de dados num serviço de armazenamento, normalmente, é fácil tooidentify no lado do servidor Olá regista uma operação anterior que eliminou o objeto de Olá em questão a partir do serviço de armazenamento Olá. Muito frequentemente, os dados de registo Olá mostram esse objeto de Olá eliminado outro utilizador ou processo. No registo de registo do armazenamento de lado do servidor de Olá, hello tipo de operação e pedida objeto-colunas chave mostram quando um cliente eliminado um objeto.

Cenário de Olá em que um cliente está a tentar tooinsert um objeto, poderá não ser imediatamente óbvios razão pela qual esta operação resulta numa resposta de HTTP 404 (não for encontrado) uma vez que hello cliente está a criar um novo objeto. No entanto, se o cliente de Olá está a criar um blob, tem de ser capaz de toofind contentor de BLOBs de Olá, se o cliente de Olá está a criar uma mensagem tem de ser capaz de toofind uma fila, e se o cliente de Olá é adicionar uma linha tem de ser capaz de toofind tabela de Olá.

Pode utilizar o registo do lado do cliente Olá de Olá biblioteca de clientes de armazenamento toogain que um mais detalhadas compreensão dos quando o cliente de Olá envia pedidos específicos toohello serviço de armazenamento.

Olá seguinte de lado do cliente de registo gerado pela biblioteca de clientes de armazenamento de Olá ilustra Olá problema quando o cliente de Olá não é possível localizar o contentor de Olá para BLOBs Olá que está a criar. Este registo inclui detalhes de Olá seguintes operações de armazenamento:

| ID do pedido | Operação |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** contentor de blob do método toodelete Olá. Tenha em atenção que esta operação inclui um **HEAD** toocheck quanto à existência de Olá do contentor de Olá do pedido. |
| e2d06d78... |**CreateIfNotExists** contentor de blob do método toocreate Olá. Tenha em atenção que esta operação inclui um **HEAD** pedido que verifica a existência de Olá do contentor de Olá. Olá **HEAD** devolve uma mensagem 404, mas continua operacional. |
| de8b1c3c-... |**UploadFromStream** blob do método toocreate Olá. Olá **colocar** pedido falha apresentando uma mensagem 404 |

Entradas de registo:

| ID do pedido | Texto de operação |
| --- | --- |
| 07b26a5d-... |A iniciar toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer pedido síncrono. |
| 07b26a5d-... |StringToSign = HEAD...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 de Jun de 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |A aguardar resposta. |
| 07b26a5d-... |Resposta recebida. Código de estado 200, ID do pedido de = = eeead849... Content-MD5 = ETag = &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Cabeçalhos de resposta foram processados com êxito, prosseguir com a restante Olá operação Olá. |
| 07b26a5d-... |Transferir o corpo da resposta. |
| 07b26a5d-... |Operação concluída com êxito. |
| 07b26a5d-... |A iniciar toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer pedido síncrono. |
| 07b26a5d-... |StringToSign = DELETE...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 de Jun de 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |A aguardar resposta. |
| 07b26a5d-... |Resposta recebida. Código de estado = 202, ID do pedido = 6ab2a4cf-..., Content-MD5 = ETag =. |
| 07b26a5d-... |Cabeçalhos de resposta foram processados com êxito, prosseguir com a restante Olá operação Olá. |
| 07b26a5d-... |Transferir o corpo da resposta. |
| 07b26a5d-... |Operação concluída com êxito. |
| e2d06d78-... |A iniciar toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer pedido assíncrono.</td> |
| e2d06d78-... |StringToSign = HEAD...x-ms-client-request-id:e2d06d78-...x-ms-date:Tue, 03 de Jun de 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |A aguardar resposta. |
| de8b1c3c-... |A iniciar toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt pedido síncrono. |
| de8b1c3c-... |StringToSign = PUT... 64.qCmF+TQLPhq/YYK50mP9ZQ==...x-MS-blob-type:BlockBlob.x-MS-Client-Request-ID:de8b1c3c-...x-MS-Date:TUE, 03 de Jun de 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |A preparar os dados de pedido de toowrite. |
| e2d06d78-... |Excepção emitida ao aguardar pela resposta: Olá o servidor remoto devolveu um erro: (404) não encontrado... |
| e2d06d78-... |Resposta recebida. Código de estado 404, ID do pedido de = = 353ae3bc-..., Content-MD5 = ETag =. |
| e2d06d78-... |Cabeçalhos de resposta foram processados com êxito, prosseguir com a restante Olá operação Olá. |
| e2d06d78-... |Transferir o corpo da resposta. |
| e2d06d78-... |Operação concluída com êxito. |
| e2d06d78-... |A iniciar toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer pedido assíncrono. |
| e2d06d78-... |StringToSign = PUT... 0...x-MS-Client-Request-ID:e2d06d78-...x-MS-Date:TUE, 03 de Jun de 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |A aguardar resposta. |
| de8b1c3c-... |Escrever os dados no pedido. |
| de8b1c3c-... |A aguardar resposta. |
| e2d06d78-... |Excepção emitida ao aguardar pela resposta: Olá o servidor remoto devolveu um erro: conflito (409)... |
| e2d06d78-... |Resposta recebida. Código de estado = 409, ID do pedido = c27da20e-..., Content-MD5 = ETag =. |
| e2d06d78-... |Transferir o corpo da resposta de erro. |
| de8b1c3c-... |Excepção emitida ao aguardar pela resposta: Olá o servidor remoto devolveu um erro: (404) não encontrado... |
| de8b1c3c-... |Resposta recebida. Código de estado 404, ID do pedido de = = 0eaeab3e-..., Content-MD5 = ETag =. |
| de8b1c3c-... |Ocorreu uma excepção durante a operação de Olá: Olá o servidor remoto devolveu um erro: (404) não encontrado... |
| de8b1c3c-... |Política de repetição não permitiu para uma nova tentativa. Falha do servidor remoto Olá devolveu um erro: (404) não encontrado... |
| e2d06d78-... |Política de repetição não permitiu para uma nova tentativa. Falha do servidor remoto Olá devolveu um erro: conflito (409)... |

Neste exemplo, o registo Olá mostra que o cliente Olá é interleaving pedidos de Olá **CreateIfNotExists** método (pedido id e2d06d78...), com pedidos de Olá de Olá **UploadFromStream** (método de8b1c3c-...); Isto acontece porque a aplicação de cliente Olá é a invocar estes métodos de forma assíncrona. Deve modificar o código assíncrona Olá Olá cliente tooensure que cria o contentor de Olá antes de tentar tooupload blob de tooa quaisquer dados no contentor. Idealmente, deve criar todos os seus contentores antecipadamente.

#### <a name="SAS-authorization-issue"></a>Um problema de autorização de assinatura de acesso partilhado (SAS)
Se a aplicação de cliente Olá tenta toouse uma chave SAS que não inclua as permissões necessárias Olá para a operação de Olá, o serviço de armazenamento Olá devolve um cliente de toohello de mensagem de HTTP 404 (não for encontrado). Em Olá mesmo tempo, verá também um valor diferente de zero para **SASAuthorizationError** no métricas Olá.

Olá, a tabela seguinte mostra uma mensagem de registo do lado do servidor de exemplo do ficheiro de registo do registo de armazenamento Olá:

| Nome | Valor |
| --- | --- |
| Hora de início de pedido | 2014-05-30T06:17:48.4473697Z |
| Tipo de operação     | GetBlobProperties            |
| Estado do pedido     | SASAuthorizationError        |
| Código de estado HTTP   | 404                          |
| Tipo de autenticação| SAs                          |
| Tipo de serviço       | Blobs                         |
| URL do pedido        | https://domemaildist.blob.Core.Windows.NET/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ? sv = 2014-02-14 & sr = Tama & c = mypolicy & sig = XXXXX&;api-version = 2014-02-14 |
| Cabeçalho de id do pedido  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| ID do pedido de cliente  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |


Deve investigar por que motivo está a tentar tooperform uma operação que tem não foram concedido permissões para a aplicação cliente.

#### <a name="JavaScript-code-does-not-have-permission"></a>No código JavaScript do lado do cliente não tem o objeto de permissão de tooaccess Olá
Se estiver a utilizar um cliente de JavaScript e serviço de armazenamento de Olá está a devolver mensagens HTTP 404, verifique se existem Olá seguintes erros de JavaScript no browser Olá:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> Pode utilizar ferramentas de programador Olá F12 no Internet Explorer tootrace Olá mensagens trocadas entre o browser Olá e o serviço de armazenamento de Olá quando a resolução de problemas de JavaScript do lado do cliente.
> 
> 

Estes erros ocorrerem porque o browser da web Olá implementa Olá [mesma política de origem](http://www.w3.org/Security/wiki/Same_Origin_Policy) vêm de restrição de segurança que impede que uma página web chamar uma API num domínio diferente da página de Olá Olá domínio.

toowork em torno Olá JavaScript problema, pode configurar cruzada origem Resource Sharing (CORS) para Olá armazenamento serviço Olá cliente está a aceder. Para obter mais informações, consulte [suporte de partilha de recursos de várias origens (CORS) para serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dn535601.aspx).

Olá, código de exemplo a seguir mostra como tooconfigure o blob service tooallow JavaScript em execução no Olá Contoso tooaccess de domínio um blob no seu serviço de armazenamento de BLOBs:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Falha de rede
Em algumas circunstâncias, pacotes de rede perdida podem levar toohello serviço de armazenamento que o cliente de toohello de mensagens HTTP 404. Por exemplo, quando a aplicação de cliente está a eliminar uma entidade do serviço de tabela Olá Consulte cliente Olá gerar um relatório de exceção de armazenamento um "HTTP 404 (não for encontrado)" mensagem de estado do serviço de tabela Olá. Quando estiver a investigar tabela Olá no serviço de armazenamento de tabela Olá, verá que o serviço de Olá eliminou entidade Olá conforme foi pedido.

Detalhes da exceção Olá no cliente Olá incluem o id de pedido de Olá (7e84f12d …) atribuído pelo serviço de tabela Olá para o pedido de Olá: pode utilizar este detalhes do pedido de informação toolocate Olá nos registos de armazenamento do lado do servidor de Olá procurando no Olá  **cabeçalho de id de pedido** coluna no ficheiro de registo Olá. Também pode utilizar Olá métricas tooidentify quando falhas como esta situação ocorrer e, em seguida, procure os ficheiros de registo Olá com base em Olá tempo Olá métricas registadas este erro. Este mostra de entrada de registo Olá eliminação falhou com uma mensagem de estado de "Cliente outro erro HTTP (404)". Olá mesmo entrada de registo também inclui o id do pedido Olá gerado pelo cliente Olá Olá **client-request-id** coluna (813ea74f...).

registo do lado do servidor de Olá também inclui a entrada de outra com Olá mesmo **client-request-id** operação para eliminar o valor (813ea74f...) para um com êxito Olá mesma entidade e de Olá mesmo cliente. Esta operação de eliminação com êxito demorou local muito pouco tempo antes de Olá pedido de eliminação falhou.

causa mais provável Olá este cenário é que o cliente Olá enviado um pedido de eliminação para o serviço tabela de Olá entidade toohello, que foi concluída com êxito, mas não recebeu uma confirmação do servidor de Olá (talvez devido tooa problema de temporários da rede). cliente de Olá, em seguida, automaticamente repetida operação Olá (utilizando Olá mesmo **client-request-id**), e esta tentativa falhou porque a entidade de Olá já tinha sido eliminada.

Se este problema ocorrer com frequência, deve investigar por que motivo está a falhar tooreceive confirmações do serviço de tabela Olá cliente Olá. Se o problema de Olá intermitente, deve trap erro de "HTTP (404) não encontrada" Olá e cliente Olá de sessão, mas permitir Olá toocontinue de cliente.

### <a name="the-client-is-receiving-409-messages"></a>cliente de Olá está a receber mensagens de HTTP 409 (conflito)
Olá tabela seguinte mostra um extrair do registo do lado do servidor de Olá para duas operações de cliente: **DeleteIfExists** seguido imediatamente por **CreateIfNotExists** utilizando Olá o mesmo nome de contentor do blob. Tenha em atenção que a operação de cada cliente resulta em duas pedidos enviados toohello server, primeiro um **GetContainerProperties** pedido toocheck existência do contentor de Olá, seguido de Olá **DeleteContainer** ou  **CreateContainer** pedido.

| Timestamp | Operação | resultado | Nome do contentor | Id do pedido de cliente |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-... |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-... |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-... |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-... |

Olá código na aplicação de cliente Olá elimina e, em seguida, recria imediatamente um contentor do blob utilizando Olá mesmo nome: Olá **CreateIfNotExists** método (pedidos de cliente ID bc881924-...), eventualmente, falha com Olá HTTP 409 (conflito) erro. Quando um cliente Elimina contentores de BLOBs, tabelas ou filas que há um breve período antes de nome de Olá fica disponível novamente.

aplicação de cliente Olá deve utilizar os nomes de contentor exclusivo sempre que cria novos contentores se o padrão de eliminação/recrie Olá é comum.

### <a name="metrics-show-low-percent-success"></a>Métricas mostram PercentSuccess baixa ou entradas de registo de análise tem operações com o estado de transação de ClientOtherErrors
Olá **PercentSuccess** métrica captura a percentagem de Olá de operações que foram bem-sucedidas, com base no respetivo código de estado de HTTP. Contagem de operações com códigos de estado de 2XX conclusão com êxito, enquanto as operações com códigos de estado no 3XX, 4XX 5XX intervalos são contadas como Olá sem e inferior **PercentSucess** valor métrico. Nos ficheiros de registo de armazenamento do lado do servidor de Olá, estas operações são registadas com um Estado de transação de **ClientOtherErrors**.

É importante toonote que estas operações concluíram com êxito e, por conseguinte, não afetam outras métricas, como a disponibilidade. Alguns exemplos de operações que ser executado com êxito, mas que pode resultar em códigos de estado HTTP sem incluem:

* **ResourceNotFound** (não foi encontrado 404), por exemplo de uma ação obter pedido tooa blob que não existe.
* **ResouceAlreadyExists** (conflito 409), por exemplo a partir de um **CreateIfNotExist** operação onde o recurso de Olá já existe.
* **ConditionNotMet** (não modificados 304), por exemplo a partir de uma operação condicional, tais como quando um cliente envia um **ETag** valor e um HTTP **If-None-Match** cabeçalho toorequest uma imagem apenas se for foi atualizado desde a última operação de Olá.

Pode encontrar uma lista de códigos de erro de REST API comuns que os serviços de armazenamento de Olá devolvem página Olá [códigos de erro da API de REST comuns](http://msdn.microsoft.com/library/azure/dd179357.aspx).

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Métricas de capacidade mostram um aumento inesperado na utilização da capacidade de armazenamento
Se vir repentino, alterações inesperadas na utilização da capacidade na sua conta de armazenamento, pode investigar motivos Olá observando primeiro as métricas de disponibilidade; Por exemplo, um aumento no número de Olá de pedidos de eliminação falhou pode originar tooan aumento na quantidade de Olá do armazenamento de BLOBs que estiver a utilizar como operações de limpeza específico de aplicação que poderá ter esperado toobe libertar espaço poderá não funcionar conforme esperado (na exemplo, porque os tokens SAS Olá utilizados para libertar espaço expiraram).

### <a name="you-are-experiencing-unexpected-reboots"></a>Estão a experienciar reinícios inesperados de Virtual Machines do Azure que tenham um grande número de VHDs ligados
Se uma Máquina Virtual do Azure (VM) tem um grande número de VHDs anexados que se encontrem no Olá mesma conta de armazenamento, poderá exceder os objetivos de escalabilidade Olá para uma conta de armazenamento individuais causar Olá toofail VM. Deve verificar as métricas de minuto Olá Olá conta de armazenamento (**TotalRequests**/**TotalIngress**/**TotalEgress**) para picos que exceder os objetivos de escalabilidade Olá para uma conta de armazenamento. Consulte a secção de Olá "[métricas mostram um aumento no PercentThrottlingError]" para a assistência para determinar se a limitação ocorreu na sua conta de armazenamento.

Em geral, cada entrada individuais ou a operação de saída num VHD de uma Máquina Virtual traduz demasiado**obter página** ou **colocar página** operações em Olá subjacente blob de página. Por conseguinte, pode utilizar Olá estimados IOPS para o ambiente tootune VHDs quantos pode numa única conta de armazenamento com base no comportamento específico de Olá da sua aplicação. Não é recomendada a ter mais de 40 discos uma única conta de armazenamento. Consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md) para obter detalhes sobre Olá atual os objetivos de escalabilidade para contas de armazenamento, em particular Olá pedido total velocidade total largura de banda e para o tipo de Olá da conta de armazenamento que está a utilizar .
Se está a exceder os objetivos de escalabilidade Olá para a sua conta de armazenamento, deve colocar os seus VHDs vários diferentes contas tooreduce Olá atividade de armazenamento em cada conta individual.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>O problema se for utilizar o emulador do storage Olá para programação ou testes
Normalmente, utilizar o emulador de armazenamento de Olá durante o desenvolvimento e teste o requisito de Olá tooavoid para uma conta de armazenamento do Azure. problemas comuns de Olá que podem ocorrer quando estiver a utilizar o emulador do storage Olá são:

* [Funcionalidade "X" não está a funcionar no emulador do storage Olá]
* [Erro "valor Olá para um dos cabeçalhos de Olá HTTP não está no formato correto Olá" quando utilizar Olá emulador de armazenamento]
* [Emulador de armazenamento Olá em execução é necessários privilégios administrativos]

#### <a name="feature-X-is-not-working"></a>Funcionalidade "X" não está a funcionar no emulador do storage Olá
emulador do storage Olá não suporta todas Olá funcionalidades dos serviços de armazenamento do Azure Olá, tais como o serviço de Olá de ficheiros. Para obter mais informações, consulte [Olá utilizar emulador do Storage do Azure para desenvolvimento e teste](storage-use-emulator.md).

Para essas funcionalidades que Olá armazenamento emulador não suporta, utilize o serviço de armazenamento do Azure Olá na nuvem de Olá.

#### <a name="error-HTTP-header-not-correct-format"></a>Erro "valor Olá para um dos cabeçalhos de Olá HTTP não está no formato correto Olá" quando utilizar Olá emulador de armazenamento
Está a testar a aplicação que utilize Olá biblioteca de clientes de armazenamento contra Olá de chamadas de método e emulador de armazenamento local, como **CreateIfNotExists** falha com o erro de Olá uma mensagem "Olá valor para um dos cabeçalhos de Olá HTTP não é em formato correto Olá." Isto indica que Olá versão do emulador do storage Olá estiver a utilizar não suporta a versão de Olá da biblioteca de clientes de armazenamento de Olá estiver a utilizar. Biblioteca de clientes de armazenamento de Olá adiciona cabeçalho Olá **x-ms-version** tooall Olá pedidos faz. Se o emulador do storage Olá não reconhece o valor Olá Olá **x-ms-version** cabeçalho, rejeita o pedido de Olá.

Pode utilizar valor Olá toosee de registos de cliente da biblioteca de armazenamento de Olá de Olá **cabeçalho x-ms-version** está a enviar. Também pode ver o valor Olá Olá **cabeçalho x-ms-version** se utilizar a pedidos de Olá Fiddler tootrace da sua aplicação de cliente.

Este cenário ocorre normalmente se instalar e utilizar a versão mais recente do Olá do Olá biblioteca de clientes de armazenamento sem atualizar o emulador do storage Olá. Deve instalar a versão mais recente do Olá do emulador do storage Olá ou utilizar o armazenamento na nuvem em vez de emulador de Olá para desenvolvimento e teste.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Emulador de armazenamento Olá em execução é necessários privilégios administrativos
Lhe for pedido para as credenciais de administrador ao executar o emulador do storage Olá. Isto só ocorre quando são inicializar emulador do storage Olá para Olá pela primeira vez. Depois de ter a inicializar o emulador do storage Olá, não precisa de privilégios administrativos toorun-a novamente.

Para obter mais informações, consulte [Olá utilizar emulador do Storage do Azure para desenvolvimento e teste](storage-use-emulator.md). Tenha em atenção que também pode inicializar emulador do storage Olá no Visual Studio, será também necessitam de privilégios administrativos.

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>São encontrar problemas ao instalar Olá Azure SDK para .NET
Quando tenta tooinstall Olá SDK, falha tentar tooinstall Olá emulador do storage no seu computador local. registo de instalação de Olá contém uma das seguintes mensagens de Olá:

* CAQuietExec: Erro: não é possível tooaccess a instância do SQL
* CAQuietExec: Erro: não é possível toocreate base de dados

causa de Olá é um problema com a instalação existente de LocalDB. Por predefinição, o emulador do storage Olá utiliza LocalDB toopersist dados quando que simula serviços do storage do Azure Olá. Pode repor a sua instância da LocalDB executando Olá os seguintes comandos numa janela de linha de comandos antes de tentar tooinstall Olá SDK.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Olá **eliminar** comando remove quaisquer ficheiros de base de dados antigos de instalações anteriores do emulador de armazenamento Olá.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Tem um problema com um serviço de armazenamento diferente
Se a secções de resolução de problemas anteriores Olá incluir o problema de Olá que estão a ter com um serviço de armazenamento, deve adotar Olá segue abordagem toodiagnosing e resolver o seu problema.

* Verifique o toosee métricas se existir qualquer alteração do seu comportamento esperado de linha de base. De métricas de Olá, poderá ser capaz de toodetermine se o problema de Olá é transitório ou permanente e as operações de armazenamento Olá problema está a afetar.
* Pode utilizar informações de métricas de Olá toohelp procurar os dados de registo do lado do servidor para obter informações mais detalhadas sobre quaisquer erros que estão a ocorrer. Esta informação pode ajudar a resolver o problema de Olá.
* Se as informações de Olá nos registos do lado do servidor de Olá não suficientes tootroubleshoot Olá problema com êxito, pode utilizar o comportamento Olá tooinvestigate de registos do lado do cliente de biblioteca de clientes de armazenamento de Olá da sua aplicação de cliente e ferramentas como o Fiddler, Wireshark, e o Microsoft Message Analyzer tooinvestigate sua rede.

Para obter mais informações sobre como utilizar o Fiddler, consulte "[apêndice 1: utilizar o tráfego Fiddler toocapture HTTP e HTTPS]."

Para obter mais informações sobre como utilizar o Wireshark, consulte "[apêndice 2: com o Wireshark tráfego de rede de toocapture]."

Para obter mais informações sobre como utilizar o Microsoft Message Analyzer, consulte "[apêndice 3: utilizar o tráfego de rede do Microsoft Message Analyzer toocapture]."

## <a name="appendices"></a>Appendices
appendices Olá descrevem várias ferramentas que poderão considerar úteis quando estiver a diagnosticar e resolver problemas com o Storage do Azure (e outros serviços). Estas ferramentas não fazem parte do armazenamento do Azure e alguns são produtos de terceiros. Como tal, as ferramentas de Olá abordadas estes appendices não são abrangidas por qualquer contrato de suporte que poderá ter com o Microsoft Azure ou o armazenamento do Azure e, por conseguinte, como parte do processo de avaliação, deve examinar Olá suporte e licenciamento opções disponíveis a partir do fornecedores de Olá destas ferramentas.

### <a name="appendix-1"></a>Apêndice 1: Utilizar o Fiddler toocapture HTTP e o tráfego HTTPS
[Fiddler](http://www.telerik.com/fiddler) é uma ferramenta útil para analisar o tráfego HTTP e HTTPS Olá entre a sua aplicação cliente e Olá serviço de armazenamento do Azure que está a utilizar.

> [!NOTE]
> Fiddler capaz de descodificar tráfego HTTPS; deve ler documentação de Fiddler Olá cuidadosamente toounderstand como fazê-lo e as implicações de segurança de Olá toounderstand.
> 
> 

Este anexo fornece breve obter instruções sobre como tooconfigure Fiddler toocapture tráfego entre o computador local do olá onde instalou o Fiddler e Olá dos serviços de armazenamento do Azure.

Depois de ter sido iniciada Fiddler, irá começar a capturar o tráfego HTTP e HTTPS no seu computador local. Olá, são alguns comandos útil para controlar o Fiddler:

* Parar e iniciar a capturar o tráfego. No menu principal Olá, aceda demasiado**ficheiro** e, em seguida, clique em **capturar tráfego** tootoggle capturar e desativar.
* Guarde os dados de tráfego capturada. No menu principal Olá, aceda demasiado**ficheiro**, clique em **guardar**e, em seguida, clique em **todas as sessões**: Isto permite que o tráfego de Olá toosave num ficheiro de arquivo de sessão. Pode recarregar um arquivo de sessão mais tarde para uma análise ou enviá-lo se for pedida tooMicrosoft suporte.

quantidade de Olá toolimit de tráfego que capture o Fiddler, pode utilizar filtros que configurar na Olá **filtros** Olá separador captura de ecrã a seguir mostra um filtro que capture apenas o tráfego enviado toohello  **contosoemaildist.TABLE.Core.Windows.NET** ponto final de armazenamento:

![][5]

### <a name="appendix-2"></a>Apêndice 2: Tráfego de rede de toocapture Wireshark utilizando o
[Wireshark](http://www.wireshark.org/) é um analisador de protocolos de rede que permite-lhe tooview informações detalhadas do pacote de uma vasta gama de protocolos de rede.

Olá seguinte procedimento mostra como toocapture informações detalhadas do pacote de tráfego a partir do computador local olá onde instalou o serviço de tabela Wireshark toohello na sua conta do storage do Azure.

1. Inicie o Wireshark no seu computador local.
2. No Olá **iniciar** secção, interface de rede local selecione Olá ou interfaces que são toohello ligado à internet.
3. Clique em **capturar opções**.
4. Adicionar um filtro toohello **capturar filtro** caixa de texto. Por exemplo, **alojar contosoemaildist.table.core.windows.net** irá configurar o Wireshark toocapture apenas pacotes enviados tooor do ponto final do serviço de tabela Olá no Olá **contosoemaildist** armazenamento conta. Veja Olá [lista completa de filtros de capturar](http://wiki.wireshark.org/CaptureFilters).
   
   ![][6]
5. Clique em **iniciar**. Wireshark agora irá capturar todos os tooor de envio de pacotes hello do ponto final do serviço de tabela Olá como utilizar a aplicação de cliente no seu computador local.
6. Quando tiver terminado, no Olá menu principal clique **capturar** e, em seguida, **parar**.
7. Olá toosave capturados dados num Wireshark capturar ficheiro, clique no menu principal de Olá **ficheiro** e, em seguida, **guardar**.

WireShark dar destaque quaisquer erros que existem na Olá **packetlist** janela. Também pode utilizar Olá **especialista informações** janela (clique **analisar**, em seguida, **especialista informações**) tooview um resumo de erros e avisos.

![][7]

Também pode selecionar dados TCP de Olá tooview como camada da aplicação Olá vê-lo ao clicar no Olá dados TCP e selecionando **siga fluxo TCP**. Isto é particularmente útil se capturou sua informação sem um filtro de captura. Para obter mais informações, consulte [seguintes fluxos TCP](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html).

![][8]

> [!NOTE]
> Para obter mais informações sobre como utilizar o Wireshark, consulte Olá [Wireshark utilizadores guia](http://www.wireshark.org/docs/wsug_html_chunked).
> 
> 

### <a name="appendix-3"></a>Apêndice 3: Utilizar o tráfego de rede do Microsoft Message Analyzer toocapture
Pode utilizar o Microsoft Message Analyzer toocapture HTTP e o tráfego HTTPS num tooFiddler de forma semelhante e capturar o tráfego de rede num tooWireshark de forma semelhante.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Configurar uma sessão de rastreio web utilizando o Microsoft Message Analyzer
tooconfigure uma sessão de rastreio web para o tráfego HTTP e HTTPS, utilizando o Microsoft Message Analyzer, executar Olá Microsoft Message Analyzer aplicação e, em seguida, no Olá **ficheiro** menu, clique em **captura/rastreio**. Na lista de Olá dos cenários de rastreio disponíveis, selecione **Web Proxy**. Em seguida, no Olá **configuração de cenário de rastreio** painel, no Olá **HostnameFilter** caixa de texto, adicionar nomes de Olá dos seus pontos finais de armazenamento (pode procurar estes nomes Olá [deportaldoAzure](https://portal.azure.com)). Por exemplo, se hello o nome da sua conta de armazenamento do Azure é **contosodata**, deve adicionar Olá seguir toohello **HostnameFilter** caixa de texto:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Um caráter de espaço separa Olá nomes de anfitrião.
> 
> 

Quando estiver pronto toostart recolha de dados de rastreio, clique em Olá **Start With** botão.

Para obter mais informações sobre Olá Microsoft Message Analyzer **Web Proxy** de rastreio, consulte [fornecedor do Microsoft-PEF-WebProxy](http://technet.microsoft.com/library/jj674814.aspx).

Olá incorporada **Web Proxy** trace no Microsoft Message Analyzer baseia-se no Fiddler; pode capturar o tráfego HTTPS do lado do cliente e apresentar mensagens HTTPS não encriptadas. Olá **Web Proxy** funciona ao configurar um proxy local para todos os tráfego HTTP e HTTPS, que concede-lhe acesso toounencrypted mensagens de rastreio.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnosticar problemas de rede com o Microsoft Message Analyzer
Além disso toousing Olá Microsoft Message Analyzer **Web Proxy** rastreio toocapture detalhes sobre Olá tráfego HTTP/HTTPs entre o serviço de armazenamento Olá e uma aplicação de cliente Olá, também pode utilizar incorporado Olá  **Camada de ligação local** toocapture informações de pacotes de rede de rastreio. Este permite toocapture dados semelhantes toothat que pode capturar com o Wireshark e diagnosticar problemas de rede, tais como remover pacotes.

Olá seguinte captura de ecrã mostra um exemplo **camada de ligação Local** rastreio com algumas **informativa** mensagens hello **DiagnosisTypes** coluna. Clicar no ícone Olá **DiagnosisTypes** coluna mostra detalhes de Olá de mensagem de saudação. Neste exemplo, o servidor de Olá retransmissão mensagem #305 porque não recebeu uma confirmação de cliente de Olá:

![][9]

Quando criar a sessão de rastreio Olá no Microsoft Message Analyzer, pode especificar os filtros tooreduce Olá do ruído no rastreio Olá. No Olá **capturar / rastreio** página onde definir o rastreio de Olá, clique em Olá **configurar** ligação seguinte demasiado**Microsoft-Windows-NDIS-PacketCapture**. Olá seguinte captura de ecrã mostra uma configuração de filtros de tráfego TCP para endereços IP Olá dos três serviços de armazenamento:

![][10]

Para obter mais informações sobre Olá rastreio de camada de ligação Microsoft mensagem analisador Local, consulte [fornecedor do Microsoft-PEF NDIS PacketCapture](http://technet.microsoft.com/library/jj659264.aspx).

### <a name="appendix-4"></a>Apêndice 4: Utilizar tooview métricas e registo de dados do Excel
Diversas ferramentas permitem-lhe dados de métricas de armazenamento de Olá toodownload do table storage do Azure no formato delimitado que faz com que dados de Olá tooload fácil para o Excel para visualização e análise. Dados de registo de armazenamento do armazenamento de Blobs do Azure já estão no formato delimitado que pode carregar para o Excel. No entanto, terá de cabeçalhos de coluna apropriado tooadd com base nas informações de Olá em [formato de registo de análise do armazenamento](http://msdn.microsoft.com/library/azure/hh343259.aspx) e [armazenamento esquema da tabela de métricas de análise](http://msdn.microsoft.com/library/azure/hh343264.aspx).

tooimport seu armazenamento dados do registo para o Excel depois transfiram-a partir do armazenamento de BLOBs:

* No Olá **dados** menu, clique em **do texto**.
* Procurar ficheiro de registo de toohello pretende tooview e clique em **importação**.
* No passo 1 Olá **Assistente de importação de texto**, selecione **delimitado**.

No passo 1 Olá **Assistente de importação de texto**, selecione **ponto e vírgula** como Olá delimitador apenas e escolha double-aspa como Olá **qualificador de texto**. Em seguida, clique em **concluir** e escolha onde tooplace Olá dados do seu livro.

### <a name="appendix-5"></a>Apêndice 5: Monitorizar com o Application Insights para Visual Studio Team Services
Também pode utilizar a funcionalidade do Olá Application Insights para Visual Studio Team Services como parte da sua monitorização de desempenho e disponibilidade. Esta ferramenta pode:

* Certifique-se de que o serviço web está disponível e reativa. Se a aplicação é um web site ou uma aplicação de dispositivo que utiliza um serviço web, este pode testar o URL de cada alguns minutos a partir de localizações em torno Olá mundo e informá-lo se houver um problema.
* Diagnostique rapidamente quaisquer problemas de desempenho ou exceções no seu serviço web. Determinar se estão a ser transferidos da CPU ou de outros recursos, obter rastreios de pilha de exceções e facilmente procurar rastreios de registo. Se hello remoções de desempenho da aplicação abaixo limites aceitáveis, podemos enviar um e-mail. Pode monitorizar os serviços web .NET e Java.

Pode encontrar mais informações em [o que é Application Insights?](../application-insights/app-insights-overview.md).

<!--Anchors-->
[Introdução]: #introduction
[Como este guia está organizado]: #how-this-guide-is-organized

[monitorização do seu serviço de armazenamento]: #monitoring-your-storage-service
[Monitorização de estado de funcionamento do serviço]: #monitoring-service-health
[Capacidade de monitorização]: #monitoring-capacity
[Monitorização de disponibilidade]: #monitoring-availability
[Monitorização do desempenho]: #monitoring-performance

[diagnosticar problemas de armazenamento]: #diagnosing-storage-issues
[Problemas de estado de funcionamento de serviço]: #service-health-issues
[Problemas de desempenho]: #performance-issues
[Erros de diagnóstico]: #diagnosing-errors
[Problemas de emulador de armazenamento]: #storage-emulator-issues
[Ferramentas de registo de armazenamento]: #storage-logging-tools
[Utilizar ferramentas de registo de rede]: #using-network-logging-tools

[rastreio ponto-a-ponto]: #end-to-end-tracing
[Correlacionar dados de registo]: #correlating-log-data
[ID do pedido de cliente]: #client-request-id
[ID do pedido de servidor]: #server-request-id
[Carimbos]: #timestamps

[orientações de resolução de problemas]: #troubleshooting-guidance
[métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente Olá está com latência elevada]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[As métricas apresentam uma AverageServerLatency alta]: #metrics-show-high-AverageServerLatency
[Ocorrem atrasos inesperados na entrega de mensagens numa fila]: #you-are-experiencing-unexpected-delays-in-message-delivery

[métricas mostram um aumento no PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Aumento transitório PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Aumento permanente PercentThrottlingError erro]: #permanent-increase-in-PercentThrottlingError
[métricas mostram um aumento no PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[As métricas apresentam um aumento do PercentNetworkError]: #metrics-show-an-increase-in-PercentNetworkError

[cliente de Olá está a receber mensagens HTTP 403 (proibido)]: #the-client-is-receiving-403-messages
[cliente de Olá está a receber mensagens HTTP 404 (não for encontrado)]: #the-client-is-receiving-404-messages
[cliente de Olá ou outro objeto de Olá de processo eliminado anteriormente]: #client-previously-deleted-the-object
[Um problema de autorização de assinatura de acesso partilhado (SAS)]: #SAS-authorization-issue
[No código JavaScript do lado do cliente não tem o objeto de permissão de tooaccess Olá]: #JavaScript-code-does-not-have-permission
[Falha de rede]: #network-failure
[cliente de Olá está a receber mensagens de HTTP 409 (conflito)]: #the-client-is-receiving-409-messages

[métricas mostram PercentSuccess baixa ou entradas de registo de análise de ter operações com Estado de transação de ClientOtherErrors]: #metrics-show-low-percent-success
[Métricas de capacidade mostram um aumento inesperado na utilização da capacidade de armazenamento]: #capacity-metrics-show-an-unexpected-increase
[Estão a experienciar inesperados reinícios das máquinas virtuais que tenham um grande número de VHDs ligados]: #you-are-experiencing-unexpected-reboots
[O problema se for utilizar o emulador do storage Olá para programação ou testes]: #your-issue-arises-from-using-the-storage-emulator
[Funcionalidade "X" não está a funcionar no emulador do storage Olá]: #feature-X-is-not-working
[Erro "valor Olá para um dos cabeçalhos de Olá HTTP não está no formato correto Olá" quando utilizar Olá emulador de armazenamento]: #error-HTTP-header-not-correct-format
[Emulador de armazenamento Olá em execução é necessários privilégios administrativos]: #storage-emulator-requires-administrative-privileges
[São encontrar problemas ao instalar Olá Azure SDK para .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Tem um problema com um serviço de armazenamento diferente]: #you-have-a-different-issue-with-a-storage-service

[Appendices]: #appendices
[apêndice 1: utilizar o tráfego Fiddler toocapture HTTP e HTTPS]: #appendix-1
[apêndice 2: com o Wireshark tráfego de rede de toocapture]: #appendix-2
[apêndice 3: utilizar o tráfego de rede do Microsoft Message Analyzer toocapture]: #appendix-3
[Apêndice 4: Utilizar tooview métricas e registo de dados do Excel]: #appendix-4
[Apêndice 5: Monitorizar com o Application Insights para Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting/overview.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-2.png
