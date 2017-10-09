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
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configurar uma Firewall de aplicação Web (WAF) para o ambiente de serviço de aplicações
## <a name="overview"></a>Descrição geral
Web firewalls de aplicação, como Olá [Barracuda WAF para o Azure](https://www.barracuda.com/programs/azure) que está disponível no Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ajuda a proteger as suas aplicações web através da inspeção de tráfego de entrada web tooblock SQL injections, processamento de scripts entre sites, software maligno carregamentos & aplicação DDoS e outros ataques. É também inspeciona respostas hello dos servidores de back-end web Olá para prevenção de perda de dados (DLP). Combinada com isolamento Olá e dimensionamento adicionais fornecidas pelo ambientes do App Service, esta opção fornece um ambiente ideal toohost empresariais críticos as aplicações web que necessitam de pedidos maliciosos toowithstand e o tráfego de elevado volume.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Configurar
Para este documento que irá configurar o nosso ambiente de serviço de aplicações por trás da carga de vários com balanceamento de instâncias de Barracuda WAF para que apenas o tráfego de Olá WAF pode alcançar Olá ambiente de serviço de aplicações e não estar acessível a partir do Olá DMZ. Também temos Traffic Manager do Azure à frente do nosso saldo de tooload de instâncias de Barracuda WAF entre centros de dados do Azure e regiões. Um diagrama de alto nível da configuração de Olá teria aspeto que é mostrado abaixo.

![Arquitetura][Architecture] 

> Nota: com a introdução de Olá das [ILB suporte para o ambiente de serviço de aplicações](app-service-environment-with-internal-load-balancer.md), pode configurar Olá ASE toobe inacessível de Olá DMZ e só ser rede privada toohello disponíveis. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configurar o ambiente de serviço de aplicações
tooconfigure um ambiente de serviço de aplicações Consulte demasiado[nossa documentação](app-service-web-how-to-create-an-app-service-environment.md) no assunto Olá. Assim que tiver um ambiente de serviço de aplicações criado, pode criar [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) e [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) neste ambiente que serão todas protegidos por trás Olá WAF iremos Configure na secção seguinte, Olá.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configurar o serviço de nuvem WAF Barracuda
Barracuda tem um [artigo detalhado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre como implementar o respetivo WAF numa máquina virtual no Azure. Mas uma vez que pretende redundância e introduz um ponto único de falha, pretende que a instância de WAF toodeploy, pelo menos, 2 VMs num Olá mesmo serviço em nuvem quando seguir estas instruções.

### <a name="adding-endpoints-toocloud-service"></a>Adicionar pontos finais tooCloud serviço
Assim que tiver 2 ou instâncias de VM de WAF mais no seu serviço em nuvem pode utilizar Olá [portal do Azure](https://portal.azure.com/) tooadd HTTP e HTTPS pontos finais que são utilizados pela sua aplicação, como mostrado na imagem de Olá abaixo.

![Configurar o ponto final][ConfigureEndpoint]

Se as suas aplicações utilizam outros pontos finais, certifique-se tooadd esses lista toothis bem. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configurar Barracuda WAF através do seu Portal de gestão
Barracuda WAF utiliza 8000 de porta de TCP para a configuração através do seu portal de gestão. Uma vez que temos várias instâncias de VMs de WAF Olá, terá de passos de Olá toorepeat aqui descritos para cada instância VM. 

> Nota: Depois de terminar com a configuração de WAF, remova Olá TCP/8000 ponto final de todos os seus tookeep WAF VMs sua WAF segura.
> 
> 

Adicione o ponto final de gestão de Olá conforme mostrado na imagem de Olá abaixo tooconfigure sua WAF Barracuda.

![Adicionar ponto final de gestão][AddManagementEndpoint]

Utilize um ponto de final de gestão de toohello de toobrowse do browser no seu serviço em nuvem. Se o seu serviço em nuvem é chamado test.cloudapp.net, seria aceder a este ponto final navegando toohttp://test.cloudapp.net:8000. Deverá ver uma página de início de sessão, conforme mostrado abaixo que pode iniciar sessão com as credenciais especificadas na fase de configuração VM Olá WAF.

![Página de início de sessão de gestão][ManagementLoginPage]

Uma vez que iniciar sessão, deverá ver um dashboard como Olá uma imagem de Olá abaixo que irá apresentar estatísticas básicas sobre Olá proteção WAF.

![Dashboard de gestão][ManagementDashboard]

Clicar no separador de serviços de Olá irá permitir-lhe configurar o seu WAF para serviços que está a proteger. Para obter mais detalhes sobre como configurar a sua WAF Barracuda pode consultar [respetiva documentação](https://techlib.barracuda.com/waf/getstarted1). Exemplo de Olá abaixo de uma aplicação Web do Azure que serve o tráfego HTTP e HTTPS foi configurada.

![Gestão de adicionar serviços][ManagementAddServices]

> Nota: Dependendo do modo como estão configuradas as suas aplicações e quais as funcionalidades que estão a ser utilizadas no seu ambiente de serviço de aplicações, terá de tooforward tráfego para as portas TCP diferente 80 e 443, por exemplo, se tiver o programa de configuração de SSL de IP para uma aplicação Web. Para obter uma lista das portas de rede utilizados em ambientes do App Service, consulte demasiado[da documentação do tráfego de entrada do controlo](app-service-app-service-environment-control-inbound-traffic.md) secção de portas de rede.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configurar o Gestor de tráfego do Microsoft Azure (opcional)
Se a aplicação está disponível em várias regiões, em seguida, seria aconselhável saldo tooload-las por trás [Traffic Manager do Azure](../traffic-manager/traffic-manager-overview.md). toodo, pelo que pode adicionar um ponto final de Olá [portal clássico do Azure](https://manage.azure.com) utilizando o nome de serviço em nuvem Olá para sua WAF no perfil do Gestor de tráfego de Olá conforme mostrado na imagem de Olá abaixo. 

![Ponto final do Gestor de tráfego][TrafficManagerEndpoint]

Se a sua aplicação requer autenticação, certifique-se de que tem alguns recursos que não requerem qualquer autenticação para o Gestor de tráfego tooping para disponibilidade Olá da sua aplicação. Pode configurar o URL de Olá em Olá secção Configurar no Olá [portal clássico do Azure](https://manage.azure.com) conforme mostrado abaixo.

![Configurar o Gestor de Tráfego][ConfigureTrafficManager]

tooforward pings de Gestor de tráfego de Olá da sua aplicação de tooyour WAF, terá de traduções toosetup site na sua Barracuda WAF tooforward tráfego tooyour aplicação conforme mostrado no exemplo Olá abaixo.

![Traduções de Web site][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Proteger o tráfego tooApp serviço ambiente através de segurança de rede grupos (NSG)
Siga Olá [documentação de tráfego de entrada do controlo](app-service-app-service-environment-control-inbound-traffic.md) para obter detalhes sobre a restringir tráfego tooyour ambiente de serviço de aplicações de Olá WAF apenas utilizando endereços Olá VIP do seu serviço de nuvem. Eis um comando do Powershell de exemplo para efetuar esta tarefa para a porta TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Substitua Olá SourceAddressPrefix Olá endereço de IP Virtual (VIP) do serviço de nuvem do seu WAF.

> Nota: Olá VIP do seu serviço de nuvem será alterado quando eliminar e voltar a criar Olá serviço em nuvem. Disponibilizar se tooupdate Olá endereço IP no grupo de recursos de rede de Olá depois de fazê-lo. 
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
