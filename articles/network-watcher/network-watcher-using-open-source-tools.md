---
title: "aaaVisualize padrões de tráfego de rede com o observador de rede do Azure e ferramentas open source | Microsoft Docs"
description: "Esta página descreve como os pacotes de observador de rede toouse capturar com Capanalysis toovisualize tráfego padrões tooand das suas VMs."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="e1752-103">Visualizar tooand de padrões de tráfego de rede da sua VMs utilizando ferramentas open source</span><span class="sxs-lookup"><span data-stu-id="e1752-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="e1752-104">Capturas de pacotes contêm dados de rede que lhe permitem tooperform forenses de rede e de inspeção de pacotes aprofundada.</span><span class="sxs-lookup"><span data-stu-id="e1752-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="e1752-105">Existem abre-se muitas ferramentas de origem que pode utilizar tooanalyze pacote capturas toogain informações sobre a sua rede.</span><span class="sxs-lookup"><span data-stu-id="e1752-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="e1752-106">Uma ferramenta deste tipo é CapAnalysis, uma ferramenta de visualização de captura de pacotes de código aberto.</span><span class="sxs-lookup"><span data-stu-id="e1752-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="e1752-107">Visualizar dados de captura de pacotes é uma forma útil tooquickly derivar conhecimentos aprofundados acerca do padrões e anomalias dentro da sua rede.</span><span class="sxs-lookup"><span data-stu-id="e1752-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="e1752-108">Visualizações também fornecem um meio de partilhar estas informações de forma facilmente consumíveis.</span><span class="sxs-lookup"><span data-stu-id="e1752-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="e1752-109">Observador de rede do Azure fornece que Olá toocapture capacidade captura de dados importantes, permitindo-lhe tooperform pacote na sua rede.</span><span class="sxs-lookup"><span data-stu-id="e1752-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="e1752-110">Neste artigo, fornecemos instruções de como toovisualize e obter conhecimentos aprofundados sobre pacote captura utilizar CapAnalysis com o observador de rede.</span><span class="sxs-lookup"><span data-stu-id="e1752-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="e1752-111">Cenário</span><span class="sxs-lookup"><span data-stu-id="e1752-111">Scenario</span></span>

<span data-ttu-id="e1752-112">Tiver uma aplicação web simples implementada numa VM no Azure pretender toouse open source para ferramentas toovisualize respetivo tooquickly de tráfego de rede identificar padrões de fluxo e qualquer anomalias possíveis.</span><span class="sxs-lookup"><span data-stu-id="e1752-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="e1752-113">Com o observador de rede, pode obter uma captura de pacotes do seu ambiente de rede e armazene-o diretamente na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e1752-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="e1752-114">CapAnalysis, em seguida, pode inserir Olá captura de pacotes diretamente a partir do blob de armazenamento Olá e visualizar o respetivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="e1752-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![cenário][1]

## <a name="steps"></a><span data-ttu-id="e1752-116">Passos</span><span class="sxs-lookup"><span data-stu-id="e1752-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="e1752-117">Instalar CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="e1752-117">Install CapAnalysis</span></span>

<span data-ttu-id="e1752-118">tooinstall CapAnalysis numa máquina virtual, pode consultar as instruções de oficial toohello https://www.capanalysis.net/ca/how-to-install-capanalysis aqui.</span><span class="sxs-lookup"><span data-stu-id="e1752-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="e1752-119">Ordem CapAnalysis acedem remotamente aos, precisamos tooopen porta 9877 na sua VM ao adicionar uma nova regra de segurança de entrada.</span><span class="sxs-lookup"><span data-stu-id="e1752-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="e1752-120">Para obter mais informações sobre como criar regras nos grupos de segurança de rede, consulte demasiado[criar regras num NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="e1752-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="e1752-121">Assim que a regra de Olá foi adicionada com êxito, deve ser capaz de tooaccess CapAnalysis do`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="e1752-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="e1752-122">Utilize a sessão de captura de um pacote de toostart de observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="e1752-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="e1752-123">Observador de rede permite-lhe toocapture pacotes tootrack o tráfego que entra e sai de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e1752-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="e1752-124">Pode consultar as instruções toohello em [capturas de pacotes de gerir com o observador de rede](network-watcher-packet-capture-manage-portal.md) toostart uma sessão de captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="e1752-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="e1752-125">Nesta captura de pacotes pode ser armazenada num toobe de blob de armazenamento acedido por CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="e1752-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="e1752-126">Carregar um tooCapAnalysis de captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="e1752-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="e1752-127">Diretamente pode carregar uma captura de pacotes executada por observador de rede utilizando o separador de "Importação de URL" Olá e fornecer um blob de armazenamento de toohello ligação onde está armazenada a captura de pacotes hello.</span><span class="sxs-lookup"><span data-stu-id="e1752-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="e1752-128">Quando fornecer um tooCapAnalysis de ligação, certifique-se tooappend um URL SAS do blob de armazenamento token toohello.</span><span class="sxs-lookup"><span data-stu-id="e1752-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="e1752-129">toodo, navegue tooShared assinatura de acesso da conta de armazenamento Olá, designar Olá permitido permissões e prima toocreate de botão Olá SAS de gerar um token.</span><span class="sxs-lookup"><span data-stu-id="e1752-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="e1752-130">Em seguida, pode acrescentar este URL de blob de armazenamento de captura do SAS token toohello pacotes.</span><span class="sxs-lookup"><span data-stu-id="e1752-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="e1752-131">Olá URL resultante será algo semelhante ao seguinte: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="e1752-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="e1752-132">Capturas de pacotes analisa</span><span class="sxs-lookup"><span data-stu-id="e1752-132">Analyzing packet captures</span></span>

<span data-ttu-id="e1752-133">CapAnalysis oferece várias opções toovisualize a captura de pacotes, cada análise fornecer numa perspetiva de diferentes.</span><span class="sxs-lookup"><span data-stu-id="e1752-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="e1752-134">Com estas resumos visual, pode compreender as tendências de tráfego de rede e rapidamente detetar qualquer atividade invulgar.</span><span class="sxs-lookup"><span data-stu-id="e1752-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="e1752-135">Algumas destas funcionalidades são mostradas nas Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1752-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="e1752-136">Tabelas de fluxo</span><span class="sxs-lookup"><span data-stu-id="e1752-136">Flow Tables</span></span>

    <span data-ttu-id="e1752-137">Este oferece tabela Olá a lista de fluxos de dados do pacote Olá, Olá carimbo de hora associado Olá fluxos e Olá vários protocolos associados às fluxo Olá, bem como o IP de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="e1752-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![página de fluxo de capanalysis][5]

1. <span data-ttu-id="e1752-139">Descrição geral do protocolo</span><span class="sxs-lookup"><span data-stu-id="e1752-139">Protocol Overview</span></span>

    <span data-ttu-id="e1752-140">Este painel permite-lhe tooquickly Consulte distribuição Olá de tráfego de rede através de Olá vários protocolos e localizações geográficas.</span><span class="sxs-lookup"><span data-stu-id="e1752-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![Descrição geral do protocolo de capanalysis][6]

1. <span data-ttu-id="e1752-142">Estatísticas</span><span class="sxs-lookup"><span data-stu-id="e1752-142">Statistics</span></span>

    <span data-ttu-id="e1752-143">Este painel permite estatísticas de tráfego de rede tooview – bytes enviados e recebidos a partir de origem e destino IPs, fluxos para cada um dos Olá origem e de destino IPs, o protocolo utilizado para vários fluxos e a duração de Olá dos fluxos.</span><span class="sxs-lookup"><span data-stu-id="e1752-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![estatísticas de capanalysis][7]

1. <span data-ttu-id="e1752-145">geomap</span><span class="sxs-lookup"><span data-stu-id="e1752-145">Geomap</span></span>

    <span data-ttu-id="e1752-146">Este painel fornece-lhe uma vista de mapa de tráfego de rede, cores dimensionamento toohello volume de tráfego de cada país.</span><span class="sxs-lookup"><span data-stu-id="e1752-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="e1752-147">Pode selecionar países realçado tooview as estatísticas de fluxo adicionais, tais como a proporção Olá de dados enviados e recebidos IPs desse país.</span><span class="sxs-lookup"><span data-stu-id="e1752-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="e1752-149">Filtros</span><span class="sxs-lookup"><span data-stu-id="e1752-149">Filters</span></span>

    <span data-ttu-id="e1752-150">CapAnalysis fornece um conjunto de filtros para análise rápida de pacotes específicos.</span><span class="sxs-lookup"><span data-stu-id="e1752-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="e1752-151">Por exemplo, pode escolher dados de Olá toofilter pelo protocolo toogain específico conhecimentos aprofundados acerca desse subconjunto de tráfego.</span><span class="sxs-lookup"><span data-stu-id="e1752-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filtros][11]

    <span data-ttu-id="e1752-153">Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn mais sobre as capacidades de todos os CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="e1752-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e1752-154">Conclusão</span><span class="sxs-lookup"><span data-stu-id="e1752-154">Conclusion</span></span>

<span data-ttu-id="e1752-155">Funcionalidade de captura de pacotes do observador de rede permite-lhe forenses de rede do toocapture Olá dados tooperform necessário e compreender melhor o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="e1752-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="e1752-156">Neste cenário, iremos mostrou como capturas de pacotes do observador de rede podem facilmente ser integradas com ferramentas de visualização de open source.</span><span class="sxs-lookup"><span data-stu-id="e1752-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="e1752-157">Utilizando ferramentas open source, tais como capturas de pacotes de toovisualize CapAnalysis, é possível efetuar a inspeção de pacotes aprofundada e identificar rapidamente as tendências dentro do seu tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="e1752-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1752-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e1752-158">Next steps</span></span>

<span data-ttu-id="e1752-159">toolearn mais informações sobre os registos de fluxo NSG, visite [os registos de NSG fluxo](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e1752-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="e1752-160">Saiba como toovisualize o fluxo de NSG regista com o Power BI, visitando [visualizar NSG flui registos com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="e1752-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
