---
title: "aaaTroubleshooting e monitorização de SAP HANA no Azure (instâncias de grande) | Microsoft Docs"
description: "Resolver problemas e monitorizar SAP HANA num (instâncias de grande) do Azure."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Como tootroubleshoot e monitor SAP HANA (instâncias de grande) no Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Monitorização de SAP HANA no Azure (instâncias de grandes)

SAP HANA no Azure (instâncias de grande) é igual a partir de qualquer outra implementação de IaaS — precisa de toomonitor que Olá SO e Olá é fazê-lo e como consumam estes Olá os seguintes recursos:

- CPU
- Memória
- Largura de banda de rede
- Espaço em disco

Como com máquinas virtuais do Azure tem toofigure se classes de recursos de Olá acima indicadas são suficientes ou se estes obterem esgotados. Eis mais detalhes em cada um dos diferentes classes de Olá:

**Consumo de recursos de CPU:** rácio Olá que SAP definido para determinados carga de trabalho contra HANA é imposta toomake certificar-se de que deve ser suficiente recursos de CPU disponível toowork através de dados de Olá que são armazenados na memória. Contudo, poderão existir casos onde HANA consome muita CPU execução de consultas devido toomissing índices ou problemas semelhantes. Isto significa que, deve monitorizar o consumo de recursos de CPU de unidade de instância grande de HANA Olá, bem como os recursos de CPU consumidos pelos serviços do Olá específicos HANA.

**Consumo de memória:** é importante toomonitor do dentro HANA, bem como fora HANA na unidade de Olá. Dentro do HANA, monitorize como dados de Olá está a consumir HANA atribuída memória em ordem toostay dentro Olá necessário dimensionamento diretrizes do SAP. Também deve consumo de memória toomonitor Olá instância grande obter toomake nível se de que software adicional instalado não-HANA não consumir demasiada memória e, por conseguinte, com HANA competem para ter memória.

**Largura de banda de rede:** gateway de VNet do Azure Olá é limitado em largura de banda de dados mover para Olá VNet do Azure, pelo que é útil dados falsificados Olá toomonitor recebidos por todos os Olá VMs do Azure dentro de um toofigure VNet enviados como fechar estiver toohello limites de Olá do Azure Selecionou de SKU de gateway. Na unidade de instância grande HANA Olá, fazer sentido toomonitor recebidos e enviados tráfego de rede, bem como e controlar tookeep de volumes de Olá que são processados ao longo do tempo.

**Espaço em disco:** consumo de espaço em disco é normalmente aumenta ao longo do tempo. Existem muitos motivos para tal, mas a maioria de todos os são: o volume de dados aumenta, execução de transação registo cópias de segurança, armazenar os ficheiros de rastreio e efetuar instantâneos de armazenamento. Por conseguinte, é importante toomonitor a utilização de espaço em disco e gerir o espaço de disco Olá associado à unidade de instância grande HANA Olá.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Monitorização e resolução de problemas do lado HANA

Na ordem tooeffectively analisar problemas relacionados tooSAP HANA no Azure (instâncias de grande), é útil toonarrow para baixo de causas raiz Olá um problema. SAP publicou uma grande quantidade de documentação toohelp.

Aplicável perguntas mais frequentes sobre o tooSAP relacionados HANA desempenho pode ser encontrado na Olá segue SAP notas:

- [A nota #2222200 – FAQ: SAP HANA rede](https://launchpad.support.sap.com/#/notes/2222200)
- [A nota #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)
- [A nota #199997 – FAQ: SAP HANA memória](https://launchpad.support.sap.com/#/notes/2177064)
- [Nota SAP #200000 – FAQ: Otimização do desempenho SAP HANA](https://launchpad.support.sap.com/#/notes/2000000)
- [SAP nota #199930 – FAQ: Análise de e/s SAP HANA](https://launchpad.support.sap.com/#/notes/1999930)
- [A nota #2177064 – FAQ: SAP HANA serviço reiniciar e falhas](https://launchpad.support.sap.com/#/notes/2177064)

**SAP HANA alertas**

Como primeiro passo, verifique Olá SAP HANA alerta os registos atuais. Na SAP HANA Studio, vá demasiado**consola de administração: alertas: Mostrar: todos os alertas**. Este separador mostra todos os alertas de SAP HANA por valores específicos (memória física livre, a utilização da CPU, etc.) que se inserem fora Olá definir mínimo e máximos limiares. Por predefinição, as verificações de são atualizados de automática a cada 15 minutos.

![Na SAP HANA Studio, vá tooAdministration consola: alertas: Mostrar: todos os alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Para um alerta acionado devido a definição de limiar tooimproper, uma resolução é o valor do tooreset toohello predefinido ou um valor de limiar mais razoável.

![Repor o valor predefinido de toohello ou um valor de limiar razoável mais](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Olá seguintes alertas pode indicar problemas de recursos de CPU:

- Utilização da CPU do anfitrião (5 alertas)
- Operação de ponto de reposição mais recente (28 alerta)
- Duração de ponto de reposição (54 em alertas)

Poderá reparar elevado consumo de CPU na base de dados SAP HANA uma das seguintes Olá:

- 5 (utilização da CPU do anfitrião) do alerta é gerado para utilização de CPU atual ou passada
- Olá apresentado a utilização da CPU no ecrã descrição geral de Olá

![Apresentar a utilização da CPU no ecrã descrição geral de Olá](./media/troubleshooting-monitoring/image3-cpu-usage.png)

gráfico de carga Olá poderá mostrar elevado consumo de CPU ou de elevado consumo no Olá nos últimos:

![gráfico de carga Olá poderá mostrar elevado consumo de CPU ou de elevado consumo em Olá passado](./media/troubleshooting-monitoring/image4-load-graph.png)

Um alerta acionado devido a utilização de toohigh da CPU pode ser causado por vários motivos, incluindo, mas não se limitando: execução de determinados transações, carregamento de dados, pendente de tarefas, execução longa instruções SQL e o desempenho de consulta inválido (por exemplo, com BW no HANA cubos).

Consulte toohello [resolução de problemas de SAP HANA: CPU relacionados faz com que e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) para os passos de resolução de problemas detalhada do site.

**Sistema operativo**

Uma das mais importante de Olá verificações para SAP HANA no Linux é toomake certificar-se de que as páginas enorme transparente estão desativadas, consulte [2131662 de n. º de nota SAP – transparente enorme páginas (THP) nos servidores do SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- Pode verificar se transparente páginas enorme estão ativadas através de Olá os seguintes comandos do Linux: **cat /sys/kernel/mm/transparent\_hugepage/ativa**
- Se _sempre_ é colocado entre parênteses Retos, tal como indicado abaixo, significa que as páginas de enorme transparente Olá estão ativadas: [sempre] madvise nunca; se _nunca_ é colocado entre parênteses Retos, tal como indicado abaixo, significa que Olá transparente Páginas enormes estão desativadas: sempre madvise [nunca]

Olá seguir Linux comando deverá devolver nada: **rpm - pergunta e resposta | grep ulimit.** Se parecer que _ulimit_ é instalado, desinstale-a imediatamente.

**Memória**

Pode observar que quantidade de Olá de memória atribuída pelo Olá SAP HANA base de dados é superior ao esperado. Olá alertas a seguir indica problemas com utilização elevada da memória:

- Utilização de memória física do anfitrião (1 alerta)
- Utilização da memória de servidor de nomes (12 alerta)
- Utilização da memória total das tabelas de arquivo de coluna (40 alerta)
- Utilização de memória dos serviços (43 alerta)
- Utilização de memória de armazenamento principal de tabelas de arquivo de coluna (45 alerta)
- Ficheiros de informação de tempo de execução (46 alerta)

Consulte toohello [resolução de problemas de SAP HANA: problemas de memória](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) para os passos de resolução de problemas detalhada do site.

**Rede**

Consulte demasiado[2081065 de n. º de nota SAP – resolução de problemas de rede do SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) e executar passos este a nota de resolução de problemas de rede de Olá.

1. Analisar reportadas round-trip tempo entre o servidor e cliente.
  A. Executar script de SQL Olá [ _HANA\_rede\_clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Analise a comunicação internós.
  A. Executar script de SQL [ _HANA\_rede\_serviços_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Execute o comando Linux **ifconfig** (saída de Olá mostra se quaisquer perdas de pacotes estão a ocorrer).
4. Execute o comando Linux **tcpdump**.

Além disso, utilize open source para Olá [IPERF](https://iperf.fr/) ferramenta (ou semelhante) desempenho de rede toomeasure real da aplicação.

Consulte toohello [resolução de problemas de SAP HANA: desempenho de rede e problemas de conectividade](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) para os passos de resolução de problemas detalhada do site.

**Armazenamento**

Da perspetiva de um utilizador final, uma aplicação (ou sistema Olá como um todo) é executado sluggishly, não responde ou até pode parecer toohang se existem problemas de desempenho de e/s. No Olá **Volumes** separador SAP HANA Studio, pode ver Olá ligado volumes e os volumes são utilizados por cada serviço.

![No separador de Volumes de Olá no SAP HANA Studio, pode ver Olá ligado volumes e os volumes são utilizados por cada serviço](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Volumes a ligados na parte inferior do Olá do ecrã de Olá, pode ver os detalhes do Olá volumes, tais como ficheiros e estatísticas de e/s.

![Volumes a ligados na parte inferior do Olá do ecrã de Olá, pode ver os detalhes do Olá volumes, tais como ficheiros e estatísticas de e/s](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Consulte toohello [resolução de problemas de SAP HANA: e/s relacionados causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [resolução de problemas de SAP HANA: disco relacionados causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) para os passos de resolução de problemas detalhada do site.

**Ferramentas de diagnóstico**

Executar uma verificação de estado de funcionamento do SAP HANA através de HANA\_configuração\_Minichecks. Esta ferramenta devolve potencialmente críticos problemas técnicos que devem já ter sido gerados como alertas no Studio do SAP HANA.

Consulte demasiado[1969700 de n. º de nota SAP – coleção de instrução de SQL para SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e transferir nota do Olá SQL Statements.zip ficheiro toothat anexado. Armazene este ficheiro. zip no disco rígido local de Olá.

No SAP HANA Studio, Olá **informações do sistema** separador, clique com o botão direito no Olá **nome** coluna e selecione **instruções SQL de importação**.

![No SAP HANA Studio no separador de informações do sistema de Olá, faça duplo clique na coluna de nome de Olá e selecione instruções SQL de importação](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Selecione Olá SQL Statements.zip ficheiro armazenado localmente, e uma pasta com instruções de SQL correspondentes Olá será importada. Neste momento, Olá que várias verificações de diagnóstico diferentes podem ser executadas com estas instruções SQL.

Por exemplo, requisitos de largura de banda de replicação do sistema do SAP HANA tootest, faça duplo clique Olá **largura de banda** instrução em **replicação: largura de banda** e selecione **abra** na consola do SQL Server.

instrução de SQL completa Olá abre toobe de parâmetros de entrada (secção de modificação) que permite alterar e, em seguida, executar.

![instrução de SQL completa Olá abre toobe de parâmetros de entrada (secção de modificação) que permite alterar e, em seguida, executar](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Outro exemplo é right-clicking nas instruções de Olá em **replicação: Descrição geral**. Selecione **executar** no menu de contexto de Olá:

![Outro exemplo é right-clicking nas instruções de Olá em replicação: Descrição geral. Selecione executar a partir do menu de contexto de Olá](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Isto resulta nas informações que ajuda a resolver o problema:

![Este procedimento resultará num informações que o irão ajudar na resolução de problemas](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Olá, mesmo para HANA\_configuração\_Minichecks e verificação para qualquer _X_ marcas de escala no Olá _C_ coluna (crítico).

Saídas de exemplo:

**HANA\_configuração\_MiniChecks\_Rev102.01 + 1** para verifica geral SAP HANA.

![HANA\_configuração\_MiniChecks\_Rev102.01 + 1 para verificações de SAP HANA gerais](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_serviços\_descrição geral** para uma descrição geral de que os serviços de SAP HANA estão atualmente em execução.

![HANA\_serviços\_descrição geral para uma descrição geral de que os serviços de SAP HANA estão atualmente em execução](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_serviços\_estatísticas** para SAP HANA service informações (CPU, memória, etc.).

![HANA\_serviços\_as estatísticas de SAP HANA informações de serviço ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_configuração\_descrição geral\_Rev110 +** para obter informações gerais na instância do Olá SAP HANA.

![HANA\_configuração\_descrição geral\_Rev110 + para obter informações gerais na instância de SAP HANA Olá](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_configuração\_parâmetros\_Rev70 +** toocheck parâmetros de SAP HANA.

![HANA\_configuração\_parâmetros\_Rev70 + toocheck parâmetros de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

