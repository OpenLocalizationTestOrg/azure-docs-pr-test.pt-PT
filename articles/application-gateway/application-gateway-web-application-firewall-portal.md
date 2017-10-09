---
title: "aaaCreate ou Atualize um Gateway de aplicação do Azure com firewall de aplicações web | Microsoft Docs"
description: "Saiba como um Gateway de aplicação com firewall de aplicações web através da utilização de toocreate Olá portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Criar um gateway de aplicação com firewall de aplicações web através do portal Olá

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI do Azure](application-gateway-web-application-firewall-cli.md)

Saiba como toocreate uma firewall de aplicação web ativado o gateway de aplicação.

Olá firewall de aplicações web (WAF) no Gateway de aplicação do Azure protege as aplicações web de ataques baseados na web comuns, como a injeção de SQL, ataques de scripts entre sites e hijacks de sessão. Aplicação Web protege contra muitas das Olá OWASP superiores 10 comuns web vulnerabilidades.

## <a name="scenarios"></a>Cenários

Neste artigo, existem dois cenários:

No primeiro cenário Olá, saiba demasiado[criar um gateway de aplicação com firewall de aplicações web](#create-an-application-gateway-with-web-application-firewall)

No segundo cenário Olá, saiba demasiado[adicionar web firewall tooan existente application gateway de aplicação](#add-web-application-firewall-to-an-existing-application-gateway).

![Exemplo de cenário][scenario]

> [!NOTE]
> Pesquisas de configuração adicional do gateway de aplicação Olá, incluindo o estado de funcionamento personalizado, os endereços do conjunto de back-end e regras adicionais são configurados após a configuração do gateway de aplicação Olá e não durante a implementação inicial.

## <a name="before-you-begin"></a>Antes de começar

Gateway de aplicação do Azure requer a sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que deixe suficiente toohave de espaço de endereço várias sub-redes. Depois de implementar uma sub-rede de tooa do gateway de aplicação, os gateways de aplicação apenas adicionais são toobe capaz de adicionado toohello sub-rede.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Adicionar web firewall tooan existente application gateway de aplicação

Neste exemplo de atualizações de uma existente application gateway toosupport firewall de aplicação web no modo de prevenção.

1. No portal do Azure de Olá **Favoritos** painel, clique em **todos os recursos**. Clique em Olá Gateway de aplicação existente na Olá **todos os recursos** painel. Se a subscrição de Olá que selecionou já tem vários recursos na mesma, pode introduzir o nome Olá no Olá **filtrar por nome...** zona DNS do caixa tooeasily acesso Olá.

   ![Criar Gateway de aplicação][1]

1. Clique em **firewall de aplicações Web** e atualizar as definições do gateway de aplicação Olá. Quando concluir clique **guardar**

    Olá definições tooupdate um existente application gateway toosupport firewall de aplicações web são:

   | **Definição** | **Valor** | **Detalhes**
   |---|---|---|
   |**Atualizar tooWAF camada**| Assinalado | Isto define a camada de Olá de Olá gateway toohello WAF a camada da aplicação.|
   |**Estado da firewall**| Ativado | Esta definição permite que a firewall Olá Olá WAF.|
   |**Modo de firewall** | Prevenção | Esta definição é a forma como a firewall de aplicações web lida com tráfego malicioso. **Deteção** modo apenas os registos de eventos de Olá, onde **prevenção** modo regista eventos de Olá e deixa de Olá tráfego malicioso.|
   |**Conjunto de regras**|3.0|Esta definição determina Olá [principal conjunto de regras](application-gateway-web-application-firewall-overview.md#core-rule-sets) que é utilizado tooprotect Olá back-end membros do agrupamento.|
   |**Configurar regras desativadas**|varia|tooprevent falsos positivos possíveis, esta definição permite-lhe toodisable determinadas [regras e grupos de regra](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Ao atualizar um toohello do gateway de aplicação existentes WAF SKU, Olá SKU tamanho alterações demasiado**média**. Isto pode ser reconfigurado após a conclusão da configuração.

    ![definições básicas do painel que mostra][2-1]

    > [!NOTE]
    > registos de firewall de aplicação web tooview, diagnóstico tem de estar ativados e ApplicationGatewayFirewallLog selecionado. Uma contagem de instâncias de 1 pode ser escolhida para fins de teste. É importante tooknow qualquer instância contagem de instâncias em dois não é abrangido por Olá SLA e, por conseguinte, não recomendado. Gateways pequenos não estão disponíveis ao utilizar a firewall de aplicações web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Criar um gateway de aplicação com firewall de aplicações web

Neste cenário irão:

* Crie um gateway de aplicação de firewall de aplicação web médias com duas instâncias.
* Crie uma rede virtual denominada AdatumAppGatewayVNET com um bloco CIDR reservado de 10.0.0.0/16.
* Criar uma sub-rede denominada Appgatewaysubnet que utiliza 10.0.0.0/28 como bloco CIDR.
* Configure um certificado para a descarga de SSL.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com). Se ainda não tiver uma conta, pode inscrever-se para obter um [um mês avaliação gratuita](https://azure.microsoft.com/free)
1. No painel de Favoritos Olá do portal de Olá, clique em **novo**
1. No Olá **novo** painel, clique em **redes**. No Olá **redes** painel, clique em **Gateway de aplicação**, conforme apresentado na Olá seguinte imagem:
1. Navegue toohello portal do Azure, clique em **novo** > **redes** > **Gateway de aplicação**

    ![Criar Gateway de aplicação][1]

1. No Olá **Noções básicas** painel apresentado, introduza os seguintes valores de Olá, em seguida, clique em **OK**:

   | **Definição** | **Valor** | **Detalhes**
   |---|---|---|
   |**Nome**|AdatumAppGateway|nome de Olá Olá do gateway de aplicação|
   |**Camada**|WAF|Os valores disponíveis são padrão e WAF. Visite [firewall de aplicações web](application-gateway-web-application-firewall-overview.md) toolearn mais informações sobre WAF.|
   |**Tamanho do SKU**|Médio|Opções de quando escolher o escalão padrão são pequeno, médio e grande. Quando escolher o escalão de WAF, as opções médio e grande apenas estão.|
   |**Contagem de instâncias**|2|Número de instâncias de gateway de aplicação Olá para elevada disponibilidade. Contagens de instâncias de 1 só devem ser utilizadas para fins de teste.|
   |**Subscrição**|[A sua subscrição]|Selecione um gateway de aplicação de Olá toocreate subscrição no.|
   |**Grupo de recursos**|**Criar um novo:** AdatumAppGatewayRG|Crie um grupo de recursos. nome do grupo de recursos de Olá têm de ser exclusivo dentro da subscrição Olá que selecionou. mais informações sobre grupos de recursos, leia Olá toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artigo de descrição geral.|
   |**Localização**|EUA Oeste||

   ![definições básicas do painel que mostra][2-2]

1. No Olá **definições** painel que é apresentado em **rede Virtual**, clique em **escolha uma rede virtual**. Este passo é aberto o introduza Olá **escolha de rede virtual** painel.  Clique em **criar nova** tooopen Olá **criar rede virtual** painel.

   ![Escolha uma rede virtual][2]

1. No Olá **painel de rede virtual criar** introduza Olá valores a seguir, em seguida, clique em **OK**. Este passo fecha Olá **criar rede virtual** e **escolha de rede virtual** painéis. Desta forma é preenchida Olá **sub-rede** campo no Olá **definições** painel com sub-rede Olá escolhido.

   |**Definição** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|AdatumAppGatewayVNET|Nome do gateway de aplicação Olá|
   |**Espaço de endereços**|10.0.0.0/16| Este valor é o espaço de endereços de Olá para a rede virtual Olá|
   |**Nome da sub-rede**|AppGatewaySubnet|Nome da sub-rede Olá Olá gateway de aplicação|
   |**Intervalo de endereços da sub-rede**|10.0.0.0/28 | Esta sub-rede permite mais sub-redes adicionais na rede virtual Olá para os membros do conjunto de back-end|

1. No Olá **definições** painel em **configuração de IP de front-end**, escolha **pública** como Olá **tipo de endereço IP**

1. No Olá **definições** painel em **endereço IP público**, clique em **escolher um endereço IP público**, este passo abre Olá **escolher endereço IP público**painel, clique em **criar nova**.

   ![Escolha o ip público][3]

1. No Olá **Criar endereço IP público** painel, aceite o valor predefinido de Olá e clique em **OK**. Este passo fecha Olá **escolher endereço IP público** painel, Olá **Criar endereço IP público** painel e preencher **endereço IP público** com endereço IP público Olá escolhido.

1. No Olá **definições** painel em **configuração do serviço de escuta**, clique em **HTTP** em **protocolo**. toouse **https**, é necessário um certificado. Olá privada do certificado de Olá é necessária para que uma exportação. pfx do certificado de Olá tem toobe fornecida e Olá palavra-passe para o ficheiro de Olá.

1. Configurar Olá **WAF** definições específicas.

   |**Definição** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Estado da firewall**| Ativado| Esta definição desativa WAF ou desativar.|
   |**Modo de firewall** | Prevenção| Esta definição determina as ações de Olá que WAF demora no tráfego malicioso. Se **deteção** é escolhido tráfego só com sessão iniciado.  Se **prevenção** é escolhido registado e parado com uma resposta não autorizado 403 tráfego.|


1. Reveja a página de resumo de Olá e clique em **OK**.  Agora o gateway de aplicação Olá é colocado em fila cópias de segurança e criado.

1. Assim que tiver sido criado o gateway de aplicação Olá, navegue tooit na configuração do portal toocontinue Olá Olá do gateway de aplicação.

    ![Vista de recurso do Gateway de aplicação][10]

Estes passos criar um gateway de aplicação básico com as predefinições para o serviço de escuta de Olá, conjunto back-end, as definições http de back-end e regras. Pode modificar estas definições toosuit a implementação depois de aprovisionamento de Olá é efetuada com êxito

> [!NOTE]
> Gateways de aplicação criados com a configuração de firewall de aplicação de web básico Olá estão configurados com CR 3.0 para proteção.

## <a name="next-steps"></a>Passos seguintes

Em seguida, pode saber como tooconfigure um alias de domínio personalizado para Olá [endereço IP público](../dns/dns-custom-domain.md#public-ip-address) através de DNS do Azure ou de outro fornecedor DNS.

Saiba como registo de diagnóstico tooconfigure, toolog Olá eventos são detetados ou impedidos com firewall de aplicações web, visitando [diagnóstico do Gateway de aplicação](application-gateway-diagnostics.md)

Saiba como o estado de funcionamento personalizado toocreate sondas, visitando [criar uma sonda do Estado de funcionamento personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarga de SSL e de desencriptação de SSL dispendiosa do tirar Olá desativado seus servidores web, visitando [configurar a descarga de SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
