---
title: "Ligar o seu tooan de rede no local rede virtual do Azure: VPN de Site para Site (clássica): Portal | Microsoft Docs"
description: "Uma ligação de IPsec do seu local de rede tooan rede virtual do Azure através de toocreate de passos Olá Internet pública. Estes passos irão ajudá-lo a criar uma ligação de Gateway de VPN de Site para Site em vários locais através do portal Olá."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Criar uma ligação Site a Site utilizando Olá portal do Azure (clássica)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artigo mostra como toouse Olá toocreate portal do Azure uma ligação de gateway VPN de Site para Site da sua toohello de rede no local VNet. passos de Olá neste artigo aplicam-se o modelo de implementação clássica toohello. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Uma ligação de gateway VPN de Site a Site é utilizado tooconnect tooan rede virtual do Azure de rede no local através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Este tipo de ligação requer uma VPN dispositivos localizado no local que tenha um tooit de atribuída de endereço IP público com acesso exterior. Para obter mais informações sobre o gateways de VPN, veja [About VPN gateway (Acerca do gateway de VPN)](vpn-gateway-about-vpngateways.md).

![Diagrama da ligação de Gateway de Rede de VPNs em vários sites](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de começar

Certifique-se de que cumpriu Olá os seguintes critérios antes de iniciar a configuração:

* Certifique-se de que pretende que o toowork no modelo de implementação clássica Olá. Se pretender toowork no modelo de implementação do Resource Manager Olá, veja [criar uma ligação Site a Site (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Sempre que possível, recomendamos que utilize o modelo de implementação do Resource Manager Olá.
* Certifique-se de um dispositivo VPN compatível e alguém que seja capaz de tooconfigure-lo. Para obter mais informações sobre os dispositivos VPN compatíveis e a configuração do dispositivo, consulte [About VPN Devices (Acerca dos Dispositivos VPN)](vpn-gateway-about-vpn-devices.md).
* Verifique se tem um endereço IP IPv4 público com acesso exterior para o seu dispositivo VPN. Este endereço IP não pode estar localizado atrás de um NAT.
* Se não estiver familiarizado com intervalos de endereços IP Olá localizados na configuração de rede no local, tem de toocoordinate com alguém que consiga fornecer esses detalhes. Ao criar esta configuração, tem de especificar que o Azure irá encaminhar localização no local de tooyour dos prefixos de intervalo de endereços para IP Olá. Nenhuma das sub-redes Olá da sua rede no local pode através de lap com sub-redes da rede virtual Olá que pretende que sejam tooconnect para.
* Atualmente, o PowerShell é necessário toospecify Olá partilhado chave e criar a ligação de gateway VPN Olá. Instale a versão mais recente do Olá do Olá cmdlets do PowerShell de gestão de serviço do Azure (SM). Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Ao trabalhar com o PowerShell para esta configuração, certifique-se de que está a executar como administrador. 

### <a name="values"></a>Valores de configuração de exemplo para este exercício

Exemplos de Olá neste artigo utilizam Olá os seguintes valores. Pode utilizar estes toocreate de valores num ambiente de teste, ou consulte toothem toobetter compreender exemplos Olá neste artigo.

* **Nome da VNet:** TestVNet1
* **Espaço de Endereços:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcional para este exercício)
* **Sub-redes:**
  * Front-End: 10.11.0.0/24
  * Back-End: 10.12.0.0/24 (opcional para este exercício)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupo de Recursos:** TestRG1
* **Localização:** E.U.A. Leste
* **Servidor DNS:** 10.11.0.3 (opcional para este exercício)
* **Nome do site local:** Site2
* **Espaço de endereços de cliente:** Olá espaço de endereços que está localizado no seu site no local.

## <a name="CreatVNet"></a>1. Criar uma rede virtual

Quando cria um toouse de rede virtual para uma ligação S2S, tem de certificar-se de que os espaços de endereços Olá que especificou não se sobrepõem qualquer um dos espaços de endereços de cliente Olá para sites locais Olá que pretende que sejam tooconnect para toomake. Se tiver sub-redes sobrepostas, a ligação não funcionará corretamente.

* Se já tiver uma VNet, certifique-se de que as definições de Olá são compatíveis com a estrutura do gateway VPN. Preste especial atenção tooany sub-redes que se possam sobrepor com outras redes. 

* Se ainda não tiver uma rede virtual, crie uma. As capturas de ecrã são disponibilizadas como exemplos. Ser se valores de Olá tooreplace com os seus próprios.

### <a name="toocreate-a-virtual-network"></a>toocreate uma rede virtual

1. Num browser, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, inicie sessão com a sua conta do Azure.
2. Clique em **+**. No Olá **marketplace Olá de pesquisa** campo, escreva 'Rede Virtual'. Localizar **rede Virtual** de Olá devolvido lista e clique em tooopen Olá **rede Virtual** página.

  ![Página Procurar rede virtual](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Perto Olá parte inferior da página Olá da rede Virtual, do Olá **selecionar um modelo de implementação** na lista pendente, selecione **clássico**e, em seguida, clique em **criar**.

  ![Selecionar modelo de implementação](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. No Olá **criar virtual network(classic)** página, configurar definições da VNet Olá. Nesta página, deve adicionar o seu primeiro espaço de endereços e um único intervalo de endereços de sub-rede. Depois de concluir a criação Olá VNet, pode voltar atrás e adicionar sub-redes adicionais e espaços de endereços.

  ![Página Criar rede virtual](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Página Criar rede virtual")
5. Certifique-se de que Olá **subscrição** é Olá correto. Pode alterar as subscrições utilizando Olá lista pendente.
6. Clique em **Grupo de recursos** e selecione um grupo de recursos existente ou crie um novo grupo ao escrever um nome para o mesmo. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Em seguida, selecione Olá **localização** definições para a sua VNet. localização de Olá determina onde os recursos de Olá que implemente toothis VNet irão residir.
8. Se pretender toofind capaz de toobe a VNet facilmente no dashboard de Olá, selecione **Pin toodashboard**. Clique em **criar** toocreate sua VNet.

  ![PIN toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "toodashboard de Pin")
9. Depois de clicar em "Criar", é apresentado um mosaico no dashboard de Olá que reflete o progresso de Olá da VNet. alterações de mosaico Olá como Olá VNet está a ser criado.

  ![Mosaico A criar a rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "A criar a rede virtual")

Assim que for criada a sua rede virtual, consulte **criado** listados na **estado** na página de redes de Olá do Olá portal clássico do Azure.

## <a name="additionaladdress"></a>2. Adicionar espaço de endereços adicional

Depois de criar a rede virtual, pode adicionar espaço de endereços adicional. Adicionar espaço de endereços adicionais não é uma parte de uma configuração de S2S necessária, mas se necessitar de vários espaços de endereços, utilize Olá os seguintes passos:

1. Localize redes virtuais Olá no portal de Olá.
2. Na página Olá na sua rede virtual, em Olá **definições** secção, clique em **espaço de endereços**.
3. Na página de espaço de endereço Olá, clique em **+ adicionar** e introduza o espaço de endereços adicionais.

## <a name="dns"></a>3. Especificar um servidor DNS

As definições de DNS não são uma parte obrigatória de uma configuração de S2S, mas o DNS é necessário se quiser resolução de nomes. A especificação de um valor não cria um novo servidor DNS. Olá endereço IP de servidor DNS que especificar deve ser um servidor DNS que pode resolver nomes de Olá dos recursos de Olá que está a ligar. Para as definições de exemplo de Olá, é utilizado um endereço IP privado. endereço IP de Olá que utilizamos provavelmente, não é o endereço IP hello do servidor DNS. Ser toouse se os seus próprios valores.

Depois de criar a rede virtual, pode adicionar endereço IP Olá uma resolução de nomes do DNS server toohandle. Abra o Olá as definições para a rede virtual, clique em servidores DNS e adicionar Olá endereço IP do servidor DNS Olá que pretende que toouse para resolução de nomes.

1. Localize redes virtuais Olá no portal de Olá.
2. Na página Olá na sua rede virtual, em Olá **definições** secção, clique em **servidores DNS**.
3. Adicione um servidor DNS.
4. toosave as definições, clique em **guardar** em Olá parte superior da página Olá.

## <a name="localsite"></a>4. Configurar o site local Olá

site local Olá refere-se normalmente localização do tooyour no local. Endereço IP Olá toowhich de dispositivo VPN de Olá que irá criar uma ligação e intervalos de endereços IP Olá serão encaminhados através de um dispositivo VPN do Olá VPN gateway toohello nele contidos.

1. No portal de Olá, navegue até toohello de rede virtual para o qual pretende toocreate um gateway.
2. Na página Olá na sua rede virtual, no Olá **descrição geral** página, na secção de ligações de VPN Olá, clique em **Gateway** tooopen Olá **nova ligação VPN** página.

  ![Clique em definições do gateway tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "clique em definições do gateway tooconfigure")
3. No Olá **nova ligação VPN** página, selecione **Site para site**.
4. Clique em **Local do site - configurar as definições necessárias** tooopen Olá **Local site** página. Configurar definições de Olá e, em seguida, clique em **OK** definições de Olá toosave.
  - **Nome:** criar um nome para o local site toomake-lo mais fácil para tooidentify.
  - **Endereço IP do gateway de VPN:** este é o endereço IP público Olá do dispositivo VPN Olá para a sua rede no local. dispositivo VPN Olá requer um endereço IP público de IPv4. Especifique um endereço IP público válido para Olá toowhich do dispositivo VPN que pretende tooconnect. Este não pode ser protegido por NAT e tem toobe acessível pelo Azure. Se não souber Olá endereço IP do seu dispositivo VPN que pode colocar sempre um valor do marcador de posição (enquanto este estiver no formato de Olá de um endereço IP público válido) e, em seguida, alterá-la mais tarde.
  - **Espaço de endereços de cliente:** lista Olá intervalos de endereços IP que pretende que sejam encaminhados toohello local rede no local através deste gateway. Pode adicionar vários intervalos de espaço de endereços. Certifique-se de que intervalos Olá que especificar aqui se sobreponha a intervalos de outras redes que estabelece ligação à rede virtual para ou com intervalos de endereços de Olá da rede virtual de Olá próprio.

  ![Site local](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configurar o site local")

## <a name="gatewaysubnet"></a>5. Configurar Olá sub-rede de gateway

Tem de criar uma sub-rede de gateway para o gateway de VPN. sub-rede do gateway Olá contém os endereços IP Olá que utilizam serviços de gateway VPN Olá.

1. No Olá **nova ligação VPN** página, selecione de Olá caixa de verificação **criar gateway de imediato**. é apresentada a página Olá 'opcional configuração do gateway'. Se não selecionar a caixa de verificação Olá, não verão a sub-rede do gateway Olá página tooconfigure Olá.

  ![Configuração do gateway - Sub-rede, tamanho, tipo de encaminhamento](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Configuração do gateway - Sub-rede, tamanho, tipo de encaminhamento")
2. Olá tooopen **configuração do Gateway** página, clique em **configuração do gateway opcional - sub-rede, tamanho e tipo de encaminhamento**.
3. No Olá **configuração do Gateway** página, clique em **sub-rede - configurar as definições necessárias** tooopen Olá **adicionar sub-rede** página.

  ![Configuração do gateway - sub-rede do gateway](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Configuração do gateway - sub-rede do gateway")
4. No Olá **adicionar sub-rede** página, adicione a sub-rede do gateway Olá. tamanho de Olá da sub-rede do gateway Olá que especificar depende da configuração do gateway VPN de Olá que pretende que o toocreate. Embora seja possível toocreate uma sub-rede do gateway tão pequena como/29, recomendamos que utilize/27 ou /28. Desta forma, estará a criar uma sub-rede maior que inclui mais endereços. Utilizar uma sub-rede do gateway maior permite suficiente endereços tooaccommodate possíveis futuras configurações de IP.

  ![Adicionar sub-rede do gateway](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Adicionar sub-rede do gateway")

## <a name="sku"></a>6. Especifique Olá SKU e tipo de VPN

1. Gateway de Olá selecione **tamanho**. Este é o gateway de Olá SKU que utilize toocreate gateway da rede virtual. No portal de Olá, Olá 'SKU predefinido' = **básico**. Gateways de VPN clássicos utilizam Olá antigo (Legado) SKUs de gateway. Para obter mais informações sobre SKUs de gateway de legado Olá, consulte [trabalhar com o gateway de rede virtual SKUs (SKUs antigos)](vpn-gateway-about-skus-legacy.md).

  ![Selecionar o SKU e o tipo de VPN](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Selecionar o SKU e o tipo de VPN")
2. Selecione Olá **encaminhamento tipo** para o seu gateway. Isto também é conhecido como tipo de VPN Olá. É importante tooselect Olá gateway correto tipo porque não é possível converter o gateway de Olá de um tipo tooanother. O dispositivo VPN tem de ser compatível com o tipo de encaminhamento Olá que selecionar. Para obter mais informações sobre o tipo de VPN, veja [About VPN Gateway (Acerca do Gateway de VPN)](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Poderá ver artigos que faça referência too'RouteBased' e 'PolicyBased' VPN tipos. ' Dinâmico 'corresponde ao too'RouteBased', e 'Estático' corresponde a 'PolicyBased'.
3. Clique em **OK** definições de Olá toosave.
4. No Olá **nova ligação VPN** página, clique em **OK** na parte inferior de Olá de Olá página toobegin criar o gateway de rede virtual. Dependendo do SKU selecionar Olá, pode demorar até too45 minutos toocreate um gateway de rede virtual.

## <a name="vpndevice"></a>7. Configurar o dispositivo VPN

Rede do ligações site a Site tooan no local requer um dispositivo VPN. Neste passo, configure o seu dispositivo VPN. Quando configurar o seu dispositivo VPN, terá de seguinte Olá:

- Uma chave partilhada. Isto é Olá mesmo partilhado chave que especificar ao criar a ligação de VPN de Site para Site. Nos nossos exemplos, iremos utilizar uma chave partilhada básica. Recomendamos que geram um toouse chave mais complexa.
- Olá endereço IP público do gateway da rede virtual. Pode ver o endereço IP público Olá utilizando Olá portal do Azure, PowerShell ou a CLI.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Criar ligação Olá
Neste passo, defina a chave partilhada Olá e criar a ligação de Olá. definir a chave de Olá é tem de ser Olá mesma chave que foi utilizado na sua configuração de dispositivo VPN.

> [!NOTE]
> Atualmente, este passo não está disponível no Olá portal do Azure. Tem de utilizar Olá gestão de serviço (SM) versão Olá cmdlets Azure PowerShell.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Passo 1. Ligar tooyour conta do Azure

1. Abra a consola do PowerShell com direitos elevados e ligue tooyour conta. Utilize Olá toohelp de exemplo, ligar os seguintes:

  ```powershell
  Add-AzureAccount
  ```
2. Verifique Olá subscrições para a conta de Olá.

  ```powershell
  Get-AzureSubscription
  ```
3. Se tiver mais do que uma subscrição, selecione a subscrição de Olá que pretende que o toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Passo 2. Defina a chave partilhada Olá e criar ligação Olá

Ao trabalhar com o modelo de implementação clássica do PowerShell e Olá, por vezes, Olá os nomes de recursos no portal de Olá não são Olá nomes Olá Azure espera toosee quando utilizar o PowerShell. Olá passos seguintes ajudá-lo exportar Olá rede ficheiro tooobtain Olá exato valores de configuração para nomes de Olá.

1. Crie um diretório no seu computador e, em seguida, exporte o diretório de toohello do ficheiro de configuração de rede da Olá. Neste exemplo, o ficheiro de configuração de rede Olá é tooC:\AzureNet exportado.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Abra o ficheiro de configuração de rede Olá com um editor de xml e verifique os valores Olá 'LocalNetworkSite name' e 'VirtualNetworkSite name'. Modificar Olá tooreflect Olá os valores de exemplo que precisa. Quando especificar um nome que contenha espaços, utilize único entre aspas à volta de valor de Olá.

3. Defina a chave partilhada Olá e criar ligação Olá. Olá '-SharedKey' é um valor que geram e especificar. Exemplo de Olá, utilizámos 'abc123', mas pode gerar (e deve) utilizar algo mais complexo. Olá importante é que o valor Olá que especificar aqui tem de ser Olá que mesmo valor que especificou quando configurar o seu dispositivo VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Quando é criada a ligação de Olá, o resultado de Olá é: **Estado: bem-sucedida**.

## <a name="verify"></a>9. Verificar a ligação

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Se estiver a ter problemas em ligar, consulte Olá **Troubleshoot** secção da tabela de Olá de conteúdo no painel esquerdo Olá.

## <a name="reset"></a>Como tooreset um gateway de VPN

Repor o gateway de VPN do Azure é útil se perder a conectividade VPN em vários locais num ou mais túneis de rede de VPNs. Nesta situação, os dispositivos VPN no local estão todos os a funcionar corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure Olá. Para obter os passos, veja [Reset a VPN gateway](vpn-gateway-resetgw-classic.md) (Repor um gateway de VPN).

## <a name="changesku"></a>Como toochange um SKU de gateway

Para obter Olá passos toochange um SKU de gateway, consulte [redimensionar um SKU de gateway](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Passos seguintes

* Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Para obter mais informações, veja [Máquinas Virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para obter informações sobre o Túnel Forçado, veja [Acerca do Túnel Forçado](vpn-gateway-about-forced-tunneling.md).