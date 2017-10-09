---
title: "os registos de aaaVisualizing fluxo do grupo de segurança de rede do Azure com Power BI | Microsoft Docs"
description: "Esta página descreve o modo de fluxo NSG toovisualize registo com o Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="ffc8d-103">Registos de fluxo do grupo de segurança de rede visualizing com o Power BI</span><span class="sxs-lookup"><span data-stu-id="ffc8d-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="ffc8d-104">Os registos de fluxo do grupo de segurança de rede permitem-lhe tooview informações sobre o tráfego IP de entrada e de saída nos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="ffc8d-105">Estes registos de fluxo mostram saídos e entrados fluxos numa base por regra, Olá fluxo de Olá NIC se aplica, informações de 5 cadeias de identificação sobre o fluxo de Olá (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego de Olá foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="ffc8d-106">Pode ser difícil toogain insights no registo de dados ao pesquisar manualmente os ficheiros de registo Olá do fluxo.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="ffc8d-107">Neste artigo, fornecemos toovisualize uma solução, o fluxo de mais recente regista e obter informações sobre o tráfego na sua rede.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="ffc8d-108">Cenário</span><span class="sxs-lookup"><span data-stu-id="ffc8d-108">Scenario</span></span>

<span data-ttu-id="ffc8d-109">No seguinte cenário de Olá, mas ligar conta de armazenamento toohello de ambiente de trabalho do Power BI que configurou como sink Olá relativamente aos nossos dados NSG fluxo de registo.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="ffc8d-110">Depois de ligar iremos tooour conta de armazenamento, o Power BI transfere e analisa Olá registos tooprovide uma representação visual de tráfego de Olá que é registado por grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="ffc8d-111">Os visuais Olá fornecidos no modelo de Olá que pode examinar a utilizar:</span><span class="sxs-lookup"><span data-stu-id="ffc8d-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="ffc8d-112">Talkers superiores</span><span class="sxs-lookup"><span data-stu-id="ffc8d-112">Top Talkers</span></span>
* <span data-ttu-id="ffc8d-113">Dados de fluxo de série de tempo por decisão direção e regra</span><span class="sxs-lookup"><span data-stu-id="ffc8d-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="ffc8d-114">Fluxos pelo endereço MAC de Interface de rede</span><span class="sxs-lookup"><span data-stu-id="ffc8d-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="ffc8d-115">Fluxos por NSG e regra</span><span class="sxs-lookup"><span data-stu-id="ffc8d-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="ffc8d-116">Fluxos por porta de destino</span><span class="sxs-lookup"><span data-stu-id="ffc8d-116">Flows by Destination Port</span></span>

<span data-ttu-id="ffc8d-117">modelo de Olá fornecido é editável por isso pode modificá-lo tooadd novos dados, os visuais, ou editar consultas toosuit às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="ffc8d-118">Configurar</span><span class="sxs-lookup"><span data-stu-id="ffc8d-118">Setup</span></span>

<span data-ttu-id="ffc8d-119">Antes de começar, tem de ter rede segurança grupo fluxo o registo ativado num ou vários grupos de segurança de rede na sua conta.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="ffc8d-120">Para obter instruções sobre como ativar a segurança de rede flua registos, consulte o seguinte artigo de toohello: [registo tooflow de introdução para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffc8d-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="ffc8d-121">Tem de ter também o cliente do ambiente de trabalho do Power BI de Olá instalado no seu computador e suficientemente Liberte espaço no sua máquina toodownload e carga Olá dados de registo que existe na sua conta do storage.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Diagrama de Visio][1]

### <a name="steps"></a><span data-ttu-id="ffc8d-123">Passos</span><span class="sxs-lookup"><span data-stu-id="ffc8d-123">Steps</span></span>

1. <span data-ttu-id="ffc8d-124">Transfira e abra Olá seguir o modelo do Power BI de Olá aplicações de ambiente de trabalho do Power BI [modelo os registos de fluxo de PowerBI de observador de rede](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="ffc8d-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="ffc8d-125">Introduza os parâmetros de consulta Olá necessário</span><span class="sxs-lookup"><span data-stu-id="ffc8d-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="ffc8d-126">**StorageAccountName** – Especifica toohello nome da conta de armazenamento de Olá fluxo NSG Olá que contêm os registos que teria como tooload e visualizar.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="ffc8d-127">**NumberOfLogFiles** – Especifica Olá número de ficheiros de registo que teria como toodownload e visualizar no Power BI.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="ffc8d-128">Por exemplo, se for especificado 50, Olá 50 ficheiros de registo mais recentes.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="ffc8d-129">Desativar temos 2 NSGs ativada e configurada toosend NSG fluxo registos toothis conta, em seguida, hello últimas 25 horas de registos pode ser visualizadas.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![principal do Power BI][2]

1. <span data-ttu-id="ffc8d-131">Introduza Olá chave de acesso para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="ffc8d-132">Pode encontrar chaves de acesso válido ao navegar no Olá Azure portal e selecionar a conta do storage de tooyour **chaves de acesso** a partir do menu de definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="ffc8d-133">Clique em **Connect** aplicar as alterações.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-133">Click **Connect** then apply changes.</span></span>

    ![chaves de acesso][3]

    ![chave de acesso 2][4]

4.  <span data-ttu-id="ffc8d-136">Os registos são transferir e analisá-la e pode agora utilizar visuais pré-criadas Olá.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="ffc8d-137">Compreender os visuais de Olá</span><span class="sxs-lookup"><span data-stu-id="ffc8d-137">Understanding hello visuals</span></span>

<span data-ttu-id="ffc8d-138">Fornecida Olá modelo são um conjunto de elementos visuais que ajudam a fazer sentido de Olá dados de registo de fluxo de NSG.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="ffc8d-139">Olá imagens que se seguem mostram um exemplo de dashboard que Olá aspeto quando preenchida com dados.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="ffc8d-140">A seguir Vamos examinar cada visual em maior detalhe</span><span class="sxs-lookup"><span data-stu-id="ffc8d-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="ffc8d-142">Talkers de principais de Olá mostra visual Olá IPs que iniciou Olá a maioria das ligações através de Olá período especificado.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="ffc8d-143">o tamanho das caixas de Olá Olá corresponde toohello número relativo de ligações.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="ffc8d-145">Olá gráficos de séries de tempo seguinte mostram Olá número de fluxos período Olá.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="ffc8d-146">gráfico superior Olá é segmentado por direcção do fluxo de Olá e Olá inferior é segmentado por decisão Olá efetuada (permitir ou negar).</span><span class="sxs-lookup"><span data-stu-id="ffc8d-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="ffc8d-147">Este visual, pode examinar as tendências de tráfego ao longo do tempo e detetar qualquer picos anormais ou recusar no tráfego ou segmentação do tráfego.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="ffc8d-149">Olá gráficos seguintes mostram Olá fluxos por interface de rede com Olá superior segmentados por direcção do fluxo e Olá inferior segmentados por decisão efetuada.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="ffc8d-150">Com esta informação, pode obter informações acerca da que as suas VMs comunicados Olá tooothers relativo a maioria das e se o tráfego tooa VM específica está a ser permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="ffc8d-152">Olá gráfico do anel roda a seguir mostra uma análise detalhada do fluxos por porta de destino.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="ffc8d-153">Com esta informação, pode ver portas de destino Olá utilizado mais frequentemente utilizadas numa Olá especificado período.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![anel][9]

<span data-ttu-id="ffc8d-155">Olá seguinte gráfico de barras mostra Olá fluxo por NSG e da regra.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="ffc8d-156">Com estas informações, pode ver Olá NSGs responsáveis por Olá mais tráfego e repartição Olá de tráfego de num NSG pela regra.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="ffc8d-158">Olá seguintes gráficos informativa apresentar informações sobre NSGs Olá presente nos registos de Olá, Olá número de fluxos capturadas ao longo do período de Olá e a data de Olá de registo mais antigo Olá capturada.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="ffc8d-159">Estas informações dão-lhe uma ideia dos quais os NSGs estão a ser registado e Olá intervalo de datas dos fluxos.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="ffc8d-162">Este modelo inclui Olá seguintes tooallow segmentações de dados tooview únicos Olá dados que é mais interessado em.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="ffc8d-163">Pode filtrar os grupos de recursos, os NSGs e regras.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="ffc8d-164">Também pode filtrar as informações de 5 cadeias de identificação, a decisão e a hora de Olá registo Olá foi escrito.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![segmentações de dados][13]

## <a name="conclusion"></a><span data-ttu-id="ffc8d-166">Conclusão</span><span class="sxs-lookup"><span data-stu-id="ffc8d-166">Conclusion</span></span>

<span data-ttu-id="ffc8d-167">Iremos mostrou neste cenário que ao utilizar registos de fluxo de grupo de segurança de rede fornecidos por observador de rede e o Power BI, iremos são toovisualize consegue e compreender o tráfego de Olá.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="ffc8d-168">Utilizar o modelo de Olá fornecido, o Power BI transfere registos Olá diretamente a partir do armazenamento e processa-los localmente.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="ffc8d-169">Modelo do tempo que demora tooload Olá varia consoante o número de Olá de ficheiros pedida e tamanho total dos ficheiros transferidos.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="ffc8d-170">Pode toocustomize livre este modelo para as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="ffc8d-171">Existem várias formas de várias que pode utilizar o Power BI com o fluxo de registos de grupo de segurança rede.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="ffc8d-172">Notas</span><span class="sxs-lookup"><span data-stu-id="ffc8d-172">Notes</span></span>

* <span data-ttu-id="ffc8d-173">Os registos por predefinição são armazenados no`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="ffc8d-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="ffc8d-174">Se outros dados existem noutro diretório Olá toopull de consultas e processamento de dados de Olá têm de ser modificados.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="ffc8d-175">modelo de Olá fornecido não é recomendado para utilização com mais de 1 GB de registos.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="ffc8d-176">Se tiver uma grande quantidade de registos, recomendamos que estiver a investigar uma solução utilizando outro arquivo de dados como o Data Lake ou SQL server.</span><span class="sxs-lookup"><span data-stu-id="ffc8d-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc8d-177">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="ffc8d-177">Next Steps</span></span>

<span data-ttu-id="ffc8d-178">Saiba como toovisualize o fluxo de NSG regista com Olá Elastick pilha, visitando [visualizar tooand de padrões de tráfego de rede da sua VMs utilizando ferramentas open source](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ffc8d-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
