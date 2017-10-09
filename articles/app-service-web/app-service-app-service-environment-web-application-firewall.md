---
title: "aaaConfiguring uma Firewall de aplicação Web (WAF) para o ambiente de serviço de aplicações"
description: "Saiba como tooconfigure uma aplicação web de firewall à frente do seu ambiente de serviço de aplicações."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="a7784-103">Configurar uma Firewall de aplicação Web (WAF) para o ambiente de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="a7784-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="a7784-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="a7784-104">Overview</span></span>
<span data-ttu-id="a7784-105">Web firewalls de aplicação, como Olá [Barracuda WAF para o Azure](https://www.barracuda.com/programs/azure) que está disponível no Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ajuda a proteger as suas aplicações web através da inspeção de tráfego de entrada web tooblock SQL injections, processamento de scripts entre sites, software maligno carregamentos & aplicação DDoS e outros ataques.</span><span class="sxs-lookup"><span data-stu-id="a7784-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="a7784-106">É também inspeciona respostas hello dos servidores de back-end web Olá para prevenção de perda de dados (DLP).</span><span class="sxs-lookup"><span data-stu-id="a7784-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="a7784-107">Combinada com isolamento Olá e dimensionamento adicionais fornecidas pelo ambientes do App Service, esta opção fornece um ambiente ideal toohost empresariais críticos as aplicações web que necessitam de pedidos maliciosos toowithstand e o tráfego de elevado volume.</span><span class="sxs-lookup"><span data-stu-id="a7784-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="a7784-108">Configurar</span><span class="sxs-lookup"><span data-stu-id="a7784-108">Setup</span></span>
<span data-ttu-id="a7784-109">Para este documento que irá configurar o nosso ambiente de serviço de aplicações por trás da carga de vários com balanceamento de instâncias de Barracuda WAF para que apenas o tráfego de Olá WAF pode alcançar Olá ambiente de serviço de aplicações e não estar acessível a partir do Olá DMZ.</span><span class="sxs-lookup"><span data-stu-id="a7784-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="a7784-110">Também temos Traffic Manager do Azure à frente do nosso saldo de tooload de instâncias de Barracuda WAF entre centros de dados do Azure e regiões.</span><span class="sxs-lookup"><span data-stu-id="a7784-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="a7784-111">Um diagrama de alto nível da configuração de Olá teria aspeto que é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a7784-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Arquitetura][Architecture] 

> <span data-ttu-id="a7784-113">Nota: com a introdução de Olá das [ILB suporte para o ambiente de serviço de aplicações](app-service-environment-with-internal-load-balancer.md), pode configurar Olá ASE toobe inacessível de Olá DMZ e só ser rede privada toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a7784-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="a7784-114">Configurar o ambiente de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="a7784-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="a7784-115">tooconfigure um ambiente de serviço de aplicações Consulte demasiado[nossa documentação](app-service-web-how-to-create-an-app-service-environment.md) no assunto Olá.</span><span class="sxs-lookup"><span data-stu-id="a7784-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="a7784-116">Assim que tiver um ambiente de serviço de aplicações criado, pode criar [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) e [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) neste ambiente que serão todas protegidos por trás Olá WAF iremos Configure na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="a7784-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="a7784-117">Configurar o serviço de nuvem WAF Barracuda</span><span class="sxs-lookup"><span data-stu-id="a7784-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="a7784-118">Barracuda tem um [artigo detalhado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre como implementar o respetivo WAF numa máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="a7784-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="a7784-119">Mas uma vez que pretende redundância e introduz um ponto único de falha, pretende que a instância de WAF toodeploy, pelo menos, 2 VMs num Olá mesmo serviço em nuvem quando seguir estas instruções.</span><span class="sxs-lookup"><span data-stu-id="a7784-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="a7784-120">Adicionar pontos finais tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="a7784-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="a7784-121">Assim que tiver 2 ou instâncias de VM de WAF mais no seu serviço em nuvem pode utilizar Olá [portal do Azure](https://portal.azure.com/) tooadd HTTP e HTTPS pontos finais que são utilizados pela sua aplicação, como mostrado na imagem de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="a7784-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Configurar o ponto final][ConfigureEndpoint]

<span data-ttu-id="a7784-123">Se as suas aplicações utilizam outros pontos finais, certifique-se tooadd esses lista toothis bem.</span><span class="sxs-lookup"><span data-stu-id="a7784-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="a7784-124">Configurar Barracuda WAF através do seu Portal de gestão</span><span class="sxs-lookup"><span data-stu-id="a7784-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="a7784-125">Barracuda WAF utiliza 8000 de porta de TCP para a configuração através do seu portal de gestão.</span><span class="sxs-lookup"><span data-stu-id="a7784-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="a7784-126">Uma vez que temos várias instâncias de VMs de WAF Olá, terá de passos de Olá toorepeat aqui descritos para cada instância VM.</span><span class="sxs-lookup"><span data-stu-id="a7784-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="a7784-127">Nota: Depois de terminar com a configuração de WAF, remova Olá TCP/8000 ponto final de todos os seus tookeep WAF VMs sua WAF segura.</span><span class="sxs-lookup"><span data-stu-id="a7784-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="a7784-128">Adicione o ponto final de gestão de Olá conforme mostrado na imagem de Olá abaixo tooconfigure sua WAF Barracuda.</span><span class="sxs-lookup"><span data-stu-id="a7784-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Adicionar ponto final de gestão][AddManagementEndpoint]

<span data-ttu-id="a7784-130">Utilize um ponto de final de gestão de toohello de toobrowse do browser no seu serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a7784-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="a7784-131">Se o seu serviço em nuvem é chamado test.cloudapp.net, seria aceder a este ponto final navegando toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="a7784-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="a7784-132">Deverá ver uma página de início de sessão, conforme mostrado abaixo que pode iniciar sessão com as credenciais especificadas na fase de configuração VM Olá WAF.</span><span class="sxs-lookup"><span data-stu-id="a7784-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Página de início de sessão de gestão][ManagementLoginPage]

<span data-ttu-id="a7784-134">Uma vez que iniciar sessão, deverá ver um dashboard como Olá uma imagem de Olá abaixo que irá apresentar estatísticas básicas sobre Olá proteção WAF.</span><span class="sxs-lookup"><span data-stu-id="a7784-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Dashboard de gestão][ManagementDashboard]

<span data-ttu-id="a7784-136">Clicar no separador de serviços de Olá irá permitir-lhe configurar o seu WAF para serviços que está a proteger.</span><span class="sxs-lookup"><span data-stu-id="a7784-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="a7784-137">Para obter mais detalhes sobre como configurar a sua WAF Barracuda pode consultar [respetiva documentação](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="a7784-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="a7784-138">Exemplo de Olá abaixo de uma aplicação Web do Azure que serve o tráfego HTTP e HTTPS foi configurada.</span><span class="sxs-lookup"><span data-stu-id="a7784-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Gestão de adicionar serviços][ManagementAddServices]

> <span data-ttu-id="a7784-140">Nota: Dependendo do modo como estão configuradas as suas aplicações e quais as funcionalidades que estão a ser utilizadas no seu ambiente de serviço de aplicações, terá de tooforward tráfego para as portas TCP diferente 80 e 443, por exemplo, se tiver o programa de configuração de SSL de IP para uma aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="a7784-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="a7784-141">Para obter uma lista das portas de rede utilizados em ambientes do App Service, consulte demasiado[da documentação do tráfego de entrada do controlo](app-service-app-service-environment-control-inbound-traffic.md) secção de portas de rede.</span><span class="sxs-lookup"><span data-stu-id="a7784-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="a7784-142">Configurar o Gestor de tráfego do Microsoft Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="a7784-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="a7784-143">Se a aplicação está disponível em várias regiões, em seguida, seria aconselhável saldo tooload-las por trás [Traffic Manager do Azure](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7784-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="a7784-144">toodo, pelo que pode adicionar um ponto final de Olá [portal clássico do Azure](https://manage.azure.com) utilizando o nome de serviço em nuvem Olá para sua WAF no perfil do Gestor de tráfego de Olá conforme mostrado na imagem de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="a7784-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Ponto final do Gestor de tráfego][TrafficManagerEndpoint]

<span data-ttu-id="a7784-146">Se a sua aplicação requer autenticação, certifique-se de que tem alguns recursos que não requerem qualquer autenticação para o Gestor de tráfego tooping para disponibilidade Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="a7784-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="a7784-147">Pode configurar o URL de Olá em Olá secção Configurar no Olá [portal clássico do Azure](https://manage.azure.com) conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a7784-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configurar o Gestor de Tráfego][ConfigureTrafficManager]

<span data-ttu-id="a7784-149">tooforward pings de Gestor de tráfego de Olá da sua aplicação de tooyour WAF, terá de traduções toosetup site na sua Barracuda WAF tooforward tráfego tooyour aplicação conforme mostrado no exemplo Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="a7784-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Traduções de Web site][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="a7784-151">Proteger o tráfego tooApp serviço ambiente através de segurança de rede grupos (NSG)</span><span class="sxs-lookup"><span data-stu-id="a7784-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="a7784-152">Siga Olá [documentação de tráfego de entrada do controlo](app-service-app-service-environment-control-inbound-traffic.md) para obter detalhes sobre a restringir tráfego tooyour ambiente de serviço de aplicações de Olá WAF apenas utilizando endereços Olá VIP do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a7784-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="a7784-153">Eis um comando do Powershell de exemplo para efetuar esta tarefa para a porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="a7784-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="a7784-154">Substitua Olá SourceAddressPrefix Olá endereço de IP Virtual (VIP) do serviço de nuvem do seu WAF.</span><span class="sxs-lookup"><span data-stu-id="a7784-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="a7784-155">Nota: Olá VIP do seu serviço de nuvem será alterado quando eliminar e voltar a criar Olá serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a7784-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="a7784-156">Disponibilizar se tooupdate Olá endereço IP no grupo de recursos de rede de Olá depois de fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="a7784-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
