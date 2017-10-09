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
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="bc2e1-103">Como tootroubleshoot e monitor SAP HANA (instâncias de grande) no Azure</span><span class="sxs-lookup"><span data-stu-id="bc2e1-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="bc2e1-104">Monitorização de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="bc2e1-105">SAP HANA no Azure (instâncias de grande) é igual a partir de qualquer outra implementação de IaaS — precisa de toomonitor que Olá SO e Olá é fazê-lo e como consumam estes Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="bc2e1-106">CPU</span><span class="sxs-lookup"><span data-stu-id="bc2e1-106">CPU</span></span>
- <span data-ttu-id="bc2e1-107">Memória</span><span class="sxs-lookup"><span data-stu-id="bc2e1-107">Memory</span></span>
- <span data-ttu-id="bc2e1-108">Largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="bc2e1-108">Network bandwidth</span></span>
- <span data-ttu-id="bc2e1-109">Espaço em disco</span><span class="sxs-lookup"><span data-stu-id="bc2e1-109">Disk space</span></span>

<span data-ttu-id="bc2e1-110">Como com máquinas virtuais do Azure tem toofigure se classes de recursos de Olá acima indicadas são suficientes ou se estes obterem esgotados.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="bc2e1-111">Eis mais detalhes em cada um dos diferentes classes de Olá:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="bc2e1-112">**Consumo de recursos de CPU:** rácio Olá que SAP definido para determinados carga de trabalho contra HANA é imposta toomake certificar-se de que deve ser suficiente recursos de CPU disponível toowork através de dados de Olá que são armazenados na memória.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="bc2e1-113">Contudo, poderão existir casos onde HANA consome muita CPU execução de consultas devido toomissing índices ou problemas semelhantes.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="bc2e1-114">Isto significa que, deve monitorizar o consumo de recursos de CPU de unidade de instância grande de HANA Olá, bem como os recursos de CPU consumidos pelos serviços do Olá específicos HANA.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="bc2e1-115">**Consumo de memória:** é importante toomonitor do dentro HANA, bem como fora HANA na unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="bc2e1-116">Dentro do HANA, monitorize como dados de Olá está a consumir HANA atribuída memória em ordem toostay dentro Olá necessário dimensionamento diretrizes do SAP.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="bc2e1-117">Também deve consumo de memória toomonitor Olá instância grande obter toomake nível se de que software adicional instalado não-HANA não consumir demasiada memória e, por conseguinte, com HANA competem para ter memória.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="bc2e1-118">**Largura de banda de rede:** gateway de VNet do Azure Olá é limitado em largura de banda de dados mover para Olá VNet do Azure, pelo que é útil dados falsificados Olá toomonitor recebidos por todos os Olá VMs do Azure dentro de um toofigure VNet enviados como fechar estiver toohello limites de Olá do Azure Selecionou de SKU de gateway.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="bc2e1-119">Na unidade de instância grande HANA Olá, fazer sentido toomonitor recebidos e enviados tráfego de rede, bem como e controlar tookeep de volumes de Olá que são processados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="bc2e1-120">**Espaço em disco:** consumo de espaço em disco é normalmente aumenta ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="bc2e1-121">Existem muitos motivos para tal, mas a maioria de todos os são: o volume de dados aumenta, execução de transação registo cópias de segurança, armazenar os ficheiros de rastreio e efetuar instantâneos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="bc2e1-122">Por conseguinte, é importante toomonitor a utilização de espaço em disco e gerir o espaço de disco Olá associado à unidade de instância grande HANA Olá.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="bc2e1-123">Monitorização e resolução de problemas do lado HANA</span><span class="sxs-lookup"><span data-stu-id="bc2e1-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="bc2e1-124">Na ordem tooeffectively analisar problemas relacionados tooSAP HANA no Azure (instâncias de grande), é útil toonarrow para baixo de causas raiz Olá um problema.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="bc2e1-125">SAP publicou uma grande quantidade de documentação toohelp.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="bc2e1-126">Aplicável perguntas mais frequentes sobre o tooSAP relacionados HANA desempenho pode ser encontrado na Olá segue SAP notas:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="bc2e1-127">A nota #2222200 – FAQ: SAP HANA rede</span><span class="sxs-lookup"><span data-stu-id="bc2e1-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="bc2e1-128">A nota #2100040 – FAQ: SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="bc2e1-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="bc2e1-129">A nota #199997 – FAQ: SAP HANA memória</span><span class="sxs-lookup"><span data-stu-id="bc2e1-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="bc2e1-130">Nota SAP #200000 – FAQ: Otimização do desempenho SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bc2e1-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="bc2e1-131">SAP nota #199930 – FAQ: Análise de e/s SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bc2e1-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="bc2e1-132">A nota #2177064 – FAQ: SAP HANA serviço reiniciar e falhas</span><span class="sxs-lookup"><span data-stu-id="bc2e1-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="bc2e1-133">**SAP HANA alertas**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="bc2e1-134">Como primeiro passo, verifique Olá SAP HANA alerta os registos atuais.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="bc2e1-135">Na SAP HANA Studio, vá demasiado**consola de administração: alertas: Mostrar: todos os alertas**.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="bc2e1-136">Este separador mostra todos os alertas de SAP HANA por valores específicos (memória física livre, a utilização da CPU, etc.) que se inserem fora Olá definir mínimo e máximos limiares.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="bc2e1-137">Por predefinição, as verificações de são atualizados de automática a cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![Na SAP HANA Studio, vá tooAdministration consola: alertas: Mostrar: todos os alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="bc2e1-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-139">**CPU**</span></span>

<span data-ttu-id="bc2e1-140">Para um alerta acionado devido a definição de limiar tooimproper, uma resolução é o valor do tooreset toohello predefinido ou um valor de limiar mais razoável.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Repor o valor predefinido de toohello ou um valor de limiar razoável mais](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="bc2e1-142">Olá seguintes alertas pode indicar problemas de recursos de CPU:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="bc2e1-143">Utilização da CPU do anfitrião (5 alertas)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="bc2e1-144">Operação de ponto de reposição mais recente (28 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="bc2e1-145">Duração de ponto de reposição (54 em alertas)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="bc2e1-146">Poderá reparar elevado consumo de CPU na base de dados SAP HANA uma das seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="bc2e1-147">5 (utilização da CPU do anfitrião) do alerta é gerado para utilização de CPU atual ou passada</span><span class="sxs-lookup"><span data-stu-id="bc2e1-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="bc2e1-148">Olá apresentado a utilização da CPU no ecrã descrição geral de Olá</span><span class="sxs-lookup"><span data-stu-id="bc2e1-148">hello displayed CPU usage on hello overview screen</span></span>

![Apresentar a utilização da CPU no ecrã descrição geral de Olá](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="bc2e1-150">gráfico de carga Olá poderá mostrar elevado consumo de CPU ou de elevado consumo no Olá nos últimos:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![gráfico de carga Olá poderá mostrar elevado consumo de CPU ou de elevado consumo em Olá passado](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="bc2e1-152">Um alerta acionado devido a utilização de toohigh da CPU pode ser causado por vários motivos, incluindo, mas não se limitando: execução de determinados transações, carregamento de dados, pendente de tarefas, execução longa instruções SQL e o desempenho de consulta inválido (por exemplo, com BW no HANA cubos).</span><span class="sxs-lookup"><span data-stu-id="bc2e1-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="bc2e1-153">Consulte toohello [resolução de problemas de SAP HANA: CPU relacionados faz com que e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) para os passos de resolução de problemas detalhada do site.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bc2e1-154">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-154">**Operating System**</span></span>

<span data-ttu-id="bc2e1-155">Uma das mais importante de Olá verificações para SAP HANA no Linux é toomake certificar-se de que as páginas enorme transparente estão desativadas, consulte [2131662 de n. º de nota SAP – transparente enorme páginas (THP) nos servidores do SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="bc2e1-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="bc2e1-156">Pode verificar se transparente páginas enorme estão ativadas através de Olá os seguintes comandos do Linux: **cat /sys/kernel/mm/transparent\_hugepage/ativa**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="bc2e1-157">Se _sempre_ é colocado entre parênteses Retos, tal como indicado abaixo, significa que as páginas de enorme transparente Olá estão ativadas: [sempre] madvise nunca; se _nunca_ é colocado entre parênteses Retos, tal como indicado abaixo, significa que Olá transparente Páginas enormes estão desativadas: sempre madvise [nunca]</span><span class="sxs-lookup"><span data-stu-id="bc2e1-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="bc2e1-158">Olá seguir Linux comando deverá devolver nada: **rpm - pergunta e resposta | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="bc2e1-159">Se parecer que _ulimit_ é instalado, desinstale-a imediatamente.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="bc2e1-160">**Memória**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-160">**Memory**</span></span>

<span data-ttu-id="bc2e1-161">Pode observar que quantidade de Olá de memória atribuída pelo Olá SAP HANA base de dados é superior ao esperado.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="bc2e1-162">Olá alertas a seguir indica problemas com utilização elevada da memória:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="bc2e1-163">Utilização de memória física do anfitrião (1 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="bc2e1-164">Utilização da memória de servidor de nomes (12 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="bc2e1-165">Utilização da memória total das tabelas de arquivo de coluna (40 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="bc2e1-166">Utilização de memória dos serviços (43 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="bc2e1-167">Utilização de memória de armazenamento principal de tabelas de arquivo de coluna (45 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="bc2e1-168">Ficheiros de informação de tempo de execução (46 alerta)</span><span class="sxs-lookup"><span data-stu-id="bc2e1-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="bc2e1-169">Consulte toohello [resolução de problemas de SAP HANA: problemas de memória](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) para os passos de resolução de problemas detalhada do site.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bc2e1-170">**Rede**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-170">**Network**</span></span>

<span data-ttu-id="bc2e1-171">Consulte demasiado[2081065 de n. º de nota SAP – resolução de problemas de rede do SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) e executar passos este a nota de resolução de problemas de rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="bc2e1-172">Analisar reportadas round-trip tempo entre o servidor e cliente.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="bc2e1-173">A.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-173">A.</span></span> <span data-ttu-id="bc2e1-174">Executar script de SQL Olá [ _HANA\_rede\_clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="bc2e1-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="bc2e1-175">Analise a comunicação internós.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-175">Analyze internode communication.</span></span>
  <span data-ttu-id="bc2e1-176">A.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-176">A.</span></span> <span data-ttu-id="bc2e1-177">Executar script de SQL [ _HANA\_rede\_serviços_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="bc2e1-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="bc2e1-178">Execute o comando Linux **ifconfig** (saída de Olá mostra se quaisquer perdas de pacotes estão a ocorrer).</span><span class="sxs-lookup"><span data-stu-id="bc2e1-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="bc2e1-179">Execute o comando Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="bc2e1-180">Além disso, utilize open source para Olá [IPERF](https://iperf.fr/) ferramenta (ou semelhante) desempenho de rede toomeasure real da aplicação.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="bc2e1-181">Consulte toohello [resolução de problemas de SAP HANA: desempenho de rede e problemas de conectividade](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) para os passos de resolução de problemas detalhada do site.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bc2e1-182">**Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-182">**Storage**</span></span>

<span data-ttu-id="bc2e1-183">Da perspetiva de um utilizador final, uma aplicação (ou sistema Olá como um todo) é executado sluggishly, não responde ou até pode parecer toohang se existem problemas de desempenho de e/s.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="bc2e1-184">No Olá **Volumes** separador SAP HANA Studio, pode ver Olá ligado volumes e os volumes são utilizados por cada serviço.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![No separador de Volumes de Olá no SAP HANA Studio, pode ver Olá ligado volumes e os volumes são utilizados por cada serviço](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="bc2e1-186">Volumes a ligados na parte inferior do Olá do ecrã de Olá, pode ver os detalhes do Olá volumes, tais como ficheiros e estatísticas de e/s.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Volumes a ligados na parte inferior do Olá do ecrã de Olá, pode ver os detalhes do Olá volumes, tais como ficheiros e estatísticas de e/s](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="bc2e1-188">Consulte toohello [resolução de problemas de SAP HANA: e/s relacionados causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [resolução de problemas de SAP HANA: disco relacionados causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) para os passos de resolução de problemas detalhada do site.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bc2e1-189">**Ferramentas de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="bc2e1-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="bc2e1-190">Executar uma verificação de estado de funcionamento do SAP HANA através de HANA\_configuração\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="bc2e1-191">Esta ferramenta devolve potencialmente críticos problemas técnicos que devem já ter sido gerados como alertas no Studio do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="bc2e1-192">Consulte demasiado[1969700 de n. º de nota SAP – coleção de instrução de SQL para SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e transferir nota do Olá SQL Statements.zip ficheiro toothat anexado.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="bc2e1-193">Armazene este ficheiro. zip no disco rígido local de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="bc2e1-194">No SAP HANA Studio, Olá **informações do sistema** separador, clique com o botão direito no Olá **nome** coluna e selecione **instruções SQL de importação**.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![No SAP HANA Studio no separador de informações do sistema de Olá, faça duplo clique na coluna de nome de Olá e selecione instruções SQL de importação](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="bc2e1-196">Selecione Olá SQL Statements.zip ficheiro armazenado localmente, e uma pasta com instruções de SQL correspondentes Olá será importada.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="bc2e1-197">Neste momento, Olá que várias verificações de diagnóstico diferentes podem ser executadas com estas instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="bc2e1-198">Por exemplo, requisitos de largura de banda de replicação do sistema do SAP HANA tootest, faça duplo clique Olá **largura de banda** instrução em **replicação: largura de banda** e selecione **abra** na consola do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="bc2e1-199">instrução de SQL completa Olá abre toobe de parâmetros de entrada (secção de modificação) que permite alterar e, em seguida, executar.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![instrução de SQL completa Olá abre toobe de parâmetros de entrada (secção de modificação) que permite alterar e, em seguida, executar](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="bc2e1-201">Outro exemplo é right-clicking nas instruções de Olá em **replicação: Descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="bc2e1-202">Selecione **executar** no menu de contexto de Olá:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-202">Select **Execute** from hello context menu:</span></span>

![Outro exemplo é right-clicking nas instruções de Olá em replicação: Descrição geral.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="bc2e1-205">Isto resulta nas informações que ajuda a resolver o problema:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-205">This results in information that helps with troubleshooting:</span></span>

![Este procedimento resultará num informações que o irão ajudar na resolução de problemas](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="bc2e1-207">Olá, mesmo para HANA\_configuração\_Minichecks e verificação para qualquer _X_ marcas de escala no Olá _C_ coluna (crítico).</span><span class="sxs-lookup"><span data-stu-id="bc2e1-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="bc2e1-208">Saídas de exemplo:</span><span class="sxs-lookup"><span data-stu-id="bc2e1-208">Sample outputs:</span></span>

<span data-ttu-id="bc2e1-209">**HANA\_configuração\_MiniChecks\_Rev102.01 + 1** para verifica geral SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_configuração\_MiniChecks\_Rev102.01 + 1 para verificações de SAP HANA gerais](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="bc2e1-211">**HANA\_serviços\_descrição geral** para uma descrição geral de que os serviços de SAP HANA estão atualmente em execução.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_serviços\_descrição geral para uma descrição geral de que os serviços de SAP HANA estão atualmente em execução](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="bc2e1-213">**HANA\_serviços\_estatísticas** para SAP HANA service informações (CPU, memória, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc2e1-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="bc2e1-214">HANA\_serviços\_as estatísticas de SAP HANA informações de serviço</span><span class="sxs-lookup"><span data-stu-id="bc2e1-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="bc2e1-215">**HANA\_configuração\_descrição geral\_Rev110 +** para obter informações gerais na instância do Olá SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_configuração\_descrição geral\_Rev110 + para obter informações gerais na instância de SAP HANA Olá](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="bc2e1-217">**HANA\_configuração\_parâmetros\_Rev70 +** toocheck parâmetros de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bc2e1-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_configuração\_parâmetros\_Rev70 + toocheck parâmetros de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

