---
title: "Ligar uma rede virtual de computador tooa através da autenticação ponto a Site e o certificado: clássico do Azure Portal | Microsoft Docs"
description: "Ligar de forma segura tooyour clássico Virtual Network do Azure através da criação de uma ligação de gateway VPN de ponto a Site utilizando Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Configurar um tooa de ligação de ponto a Site VNet através da autenticação de certificado (clássica): portal do Azure

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artigo mostra como toocreate uma VNet com uma ligação ponto a Site utilizando de modelo de implementação clássica do Olá Olá portal do Azure. Esta configuração utilize Olá tooauthenticate de certificados a ligação de cliente. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Um gateway de VPN de ponto a Site (P2S) permite-lhe criar uma rede virtual de tooyour ligação segura a partir de um computador de cliente individuais. Ligações de VPN ponto a Site são úteis quando pretende tooconnect tooyour VNet a partir de uma localização remota, tal como quando são telecommuting casa ou numa conferência. Uma VPN P2S também é toouse uma excelente solução em vez de uma VPN de Site a Site quando tem apenas alguns clientes que necessitam de tooconnect tooa VNet. 

Utiliza P2S Olá Secure Socket Tunneling Protocol (SSTP), que é um protocolo VPN baseada em SSL. É estabelecida uma ligação de P2S VPN ao iniciá-lo a partir do computador de cliente Olá.


![Diagrama Ponto a Site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Ligações de autenticação de certificado de ponto a Site requerem seguinte Olá:

* Um gateway de VPN Dinâmico.
* Olá chave pública (ficheiro. cer) para um certificado de raiz, que é carregado tooAzure. Isto é considerado um certificado fidedigno e é utilizado para autenticação.
* Um certificado de cliente gerado a partir do certificado de raiz de Olá e instalado em cada computador cliente que irá estabelecer ligação. Este certificado é utilizado para autenticação de cliente.
* Um pacote de configuração de cliente VPN tem de estar gerado e instalado em todos os computadores cliente que estabelece ligação. pacote de configuração de cliente Olá configura o cliente VPN nativo Olá que já se encontra num sistema de operativo Olá com Olá informações necessárias tooconnect toohello VNet.

As ligações Ponto a Site não precisam de nenhum dispositivo VPN ou endereço IP destinado ao público no local. Olá ligação VPN é criado através de SSTP (Secure Socket Tunneling Protocol). No lado do servidor de Olá, suportamos versões SSTP 1.0, 1.1 e 1.2. cliente de Olá decide que toouse de versão. Para o Windows 8.1 e versões posteriores, o SSTP utiliza 1.2 por predefinição. 

Para obter mais informações sobre ligações ponto a Site, consulte Olá [ponto a Site FAQ](#faq) no fim de Olá deste artigo.

### <a name="example-settings"></a>Definições de exemplo

Pode utilizar os seguintes valores toocreate num ambiente de teste de Olá, ou consulte valores toothese toobetter compreender exemplos Olá neste artigo:

* **Nome: VNet1**
* **Espaço de endereços: 192.168.0.0/16**<br>Para este exemplo, utilizamos apenas um espaço de endereços. Pode ter mais do que um espaço de endereços para a sua VNet.
* **Nome da sub-rede: FrontEnd**
* **Intervalo de endereços da sub-rede: 192.168.1.0/24**
* **Subscrição:** se tiver mais do que uma subscrição, certifique-se de que está a utilizar Olá correto.
* **Grupo de Recursos: TestRG**
* **Localização: E.U.A. Leste**
* **Tipo de ligação: Ponto a site**
* **Espaço de Endereços do Cliente: 172.16.201.0/24**. Os clientes VPN que se ligam toohello VNet com esta ligação ponto a Site recebe um endereço IP de Olá conjunto especificado.
* **GatewaySubnet: 192.168.200.0/24**. sub-rede do Gateway Olá tem de utilizar Olá nome "GatewaySubnet".
* **Tamanho:** que pretende que o toouse SKU de gateway de Olá selecione.
* **Tipo de Encaminhamento: Dinâmico**

## <a name="vnetvpn"></a>1. Criar uma rede virtual e um gateway de VPN

Antes de começar, verifique se tem uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Parte 1: Criar uma rede virtual

Se ainda não tiver uma rede virtual, crie uma. As capturas de ecrã são disponibilizadas como exemplos. Ser se valores de Olá tooreplace com os seus próprios. Olá, toocreate uma VNet com o portal do Azure, Olá utilize os seguintes passos:

1. Num browser, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, inicie sessão com a sua conta do Azure.
2. Clique em **Novo**. No Olá **marketplace Olá de pesquisa** campo, escreva 'Rede Virtual'. Localizar **rede Virtual** de Olá devolvido lista e clique em tooopen Olá **rede Virtual** página.

  ![Página Procurar rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Perto Olá parte inferior da página Olá da rede Virtual, do Olá **selecionar um modelo de implementação** lista, selecione **clássico**e, em seguida, clique em **criar**.

  ![Selecionar modelo de implementação](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. No Olá **criar rede virtual** página, configurar definições da VNet Olá. Nesta página, deve adicionar o seu primeiro espaço de endereços e um único intervalo de endereços de sub-rede. Depois de concluir a criação Olá VNet, pode voltar atrás e adicionar sub-redes adicionais e espaços de endereços.

  ![Página Criar rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Certifique-se de que Olá **subscrição** é Olá correto. Pode alterar as subscrições utilizando Olá lista pendente.
6. Clique em **Grupo de recursos** e selecione um grupo de recursos existente ou crie um novo escrevendo um nome para o novo grupo de recursos. Se estiver a criar um novo grupo de recursos, o grupo de recursos nome Olá tooyour de acordo com planeada valores de configuração. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Em seguida, selecione Olá **localização** definições para a sua VNet. localização de Olá determina onde os recursos de Olá que implemente toothis VNet irão residir.
8. Selecione **Pin toodashboard** se pretende toofind capaz de toobe a VNet facilmente no dashboard de Olá e, em seguida, clique em **criar**.

  ![PIN toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Depois de clicar em criar, é apresentado um mosaico no dashboard que irá refletir o progresso de Olá da VNet. alterações de mosaico Olá como Olá VNet está a ser criado.

  ![Mosaico Criar rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Quando tiver sido criada a sua rede virtual, consulte **criado** listados na **estado** na página de redes de Olá do Olá portal clássico do Azure.
11. Adicione um servidor DNS (opcional). Depois de criar a rede virtual, pode adicionar endereço IP de Olá de um servidor DNS para resolução de nomes. Olá endereço IP de servidor DNS que especificar deve ser o endereço de Olá de um servidor DNS que pode resolver nomes de Olá dos recursos de Olá na sua VNet.<br>tooadd um servidor DNS, abra o Olá as definições para a rede virtual, clique em servidores DNS e adicionar Olá endereço IP do servidor DNS Olá que pretende que o toouse.

### <a name="gateway"></a>Parte 2: Criar a sub-rede de gateway e um gateway de encaminhamento dinâmico

Neste passo, vai criar uma sub-rede de gateway e um gateway de encaminhamento dinâmico. No portal do Azure para o modelo de implementação clássica Olá Olá, criação de sub-rede do gateway Olá e gateway Olá pode ser feito Olá mesmo as páginas de configuração.

1. No portal de Olá, navegue até toohello de rede virtual para o qual pretende toocreate um gateway.
2. Na página Olá na sua rede virtual, no Olá **descrição geral** página, na secção de ligações de VPN Olá, clique em **Gateway**.

  ![Clique em toocreate um gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. No Olá **nova ligação VPN** página, selecione **ponto a site**.

  ![Tipo de ligação Ponto a Site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Para **espaço de endereços de cliente**, adicione o intervalo de endereços IP Olá. Este é o intervalo de Olá partir da qual os clientes VPN de Olá recebem um endereço IP ao ligar. Utilize um intervalo de endereços IP privado que não se sobreponha a localização no local Olá que estabelecerão ligação através da ou com Olá VNet que pretende que sejam tooconnect para. Pode eliminar o intervalo de preenchimento automático Olá e depois adicione Olá privado intervalo de endereços IP que pretende que o toouse.

  ![Espaço de endereços do cliente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Selecione Olá **criar gateway de imediato** caixa de verificação.

  ![Criar gateway de imediato](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Clique em **configuração do gateway opcional** tooopen Olá **configuração do Gateway** página.

  ![Clique em configuração do gateway opcional](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Clique em **sub-rede configurar definições necessárias** tooadd Olá **sub-rede do gateway**. Embora seja possível toocreate uma sub-rede do gateway tão pequena como/29, recomendamos que crie uma sub-rede maior que inclua endereços mais ao selecionar, pelo menos, / 28 ou /27. Isto permitirá para suficiente endereços tooaccommodate possíveis configurações adicionais que poderá ser útil no Olá futuras. Ao trabalhar com as sub-redes de gateway, evite a associação de uma sub-rede de gateway toohello de grupo (NSG) de segurança de rede. Associar uma sub-rede de toothis de grupo de segurança de rede pode fazer com que o toostop de gateway VPN a funcionar conforme esperado.

  ![Adicionar GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Gateway de Olá selecione **tamanho**. o tamanho de Olá é a SKU de gateway Olá para o gateway de rede virtual. No portal de Olá, hello predefinido SKU é **básico**. Para obter mais informações sobre os SKUs de gateway, veja [About VPN Gateway Settings (Acerca das Definições do Gateway de VPN)](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Tamanho do gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Selecione Olá **encaminhamento tipo** para o seu gateway. As configurações P2S requerem o tipo de encaminhamento **Dinâmico**. Clique em **OK** quando concluir a configuração desta página.

  ![Configurar o tipo de encaminhamento](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. No Olá **nova ligação VPN** página, clique em **OK** na parte inferior de Olá de Olá página toobegin criar o gateway de rede virtual. Um gateway de VPN pode demorar até too45 toocomplete de minutos, consoante o sku de gateway Olá que selecionar.

## <a name="generatecerts"></a>2. Criar certificados

Certificados são utilizados por clientes VPN do Azure tooauthenticate para VPNs ponto a Site. Carregar informações chave pública de tooAzure de certificado de raiz de Olá Olá. chave pública Olá, em seguida, é considerado 'fidedigna'. Certificados de cliente tem de ser gerados a partir do certificado de raiz fidedigna Olá e, em seguida, instalados em cada computador cliente no arquivo de certificados do Olá atual de certificados de utilizador/pessoal. o certificado de Olá é o cliente de Olá tooauthenticate utilizado quando inicia a toohello uma ligação VNet. 

Se utilizar certificados autoassinados, eles têm de ser criados com parâmetros específicos. Pode criar um certificado autoassinado utilizando Olá instruções para [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), ou [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). É importante que segue Olá passos nestas instruções ao trabalhar com certificados de raiz autoassinados e de gerar os certificados de cliente de Olá certificado de raiz autoassinado. Caso contrário, não serão compatíveis com ligações P2S certificados Olá que criar e irá receber um erro de ligação.

### <a name="cer"></a>Parte 1: Obter a chave pública de Olá (. cer) para o certificado de raiz de Olá

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Parte 2: Gerar um certificado de cliente

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Carregar ficheiro. cer do certificado de raiz Olá

Depois de ter sido criado o gateway de Olá, pode carregar Olá ficheiro. cer (que contém informações de chaves públicas Olá) para um tooAzure de certificado de raiz fidedigna. Não carregue uma chave privada Olá para tooAzure de certificado de raiz de Olá. Assim que o ficheiro de a.cer é carregado, Azure pode utilizá-la tooauthenticate clientes que têm instalado um certificado de cliente gerado a partir do certificado de raiz fidedigna Olá. Pode carregar ficheiros de certificado de raiz fidedigna adicionais - cópia de segurança tooa total de 20, mais tarde, se necessário.  

1. No Olá **ligações VPN** secção da página Olá para a sua VNet, clique em Olá **clientes** tooopen gráfico Olá **ponto a site VPN ligação** página.

  ![Clientes](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. No Olá **ligaçãopontoasitede** página, clique em **gerir certificados** tooopen Olá **certificados** página.<br>

  ![Página Certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. No Olá **certificados** página, clique em **carregar** tooopen Olá **carregar certificado** página.<br>

    ![Página Carregar certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Clique em Olá pasta toobrowse gráfico para o ficheiro. cer de Olá. Selecione o ficheiro de Olá, em seguida, clique em **OK**. Atualização Olá página toosee Olá carregado certificado Olá **certificados** página.

  ![Carregar certificado](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Configurar cliente Olá

tooconnect tooa VNet com uma VPN ponto a Site, a cada cliente tem de instalar um cliente de VPN do Windows nativo do pacote tooconfigure Olá. pacote de configuração de Olá configura nativo cliente de VPN do Windows hello com a rede virtual do Olá definições necessárias tooconnect toohello.

Pode utilizar Olá a mesma configuração de cliente VPN do pacote em cada computador cliente, desde que a versão de Olá corresponde à arquitetura de Olá para cliente Olá. Para Olá obter lista de sistemas operativos cliente que são suportados, consulte Olá [ligaçõespontoaSitedeFAQ](#faq) no fim de Olá deste artigo.

### <a name="generateconfigpackage"></a>Parte 1: Gerar e instalar o pacote de configuração de cliente VPN Olá

1. No Olá portal do Azure, na Olá **descrição geral** página para a sua VNet em **ligações VPN**, clique em hello do Olá cliente tooopen gráfico **ponto a site VPN ligação** página.
2. Na parte superior de Olá de Olá **ponto a site VPN ligação** página, clique em pacote de transferência de Olá que corresponde ao sistema de operativo de cliente de toohello no qual será instalado:

  * Para clientes de 64 bits, selecione **Cliente VPN (64 bit)s**.
  * Para clientes de 32 bits, selecione **Cliente VPN (32 bit)s**.

  ![Transferir o pacote de configuração do cliente VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Depois de Olá empacotada gera, transfira e instale-o no seu computador cliente. Se vir um pop-up SmartScreen, clique em **Mais informações** e, em seguida, em **Executar mesmo assim**. Também pode guardar Olá pacote tooinstall noutros computadores cliente.

### <a name="installclientcert"></a>Parte 2: Instalar certificado de cliente Olá

Se pretender toocreate um P2S ligação de um computador cliente que não sejam Olá um utilizou certificados de cliente toogenerate Olá, precisa de tooinstall um certificado de cliente. Ao instalar um certificado de cliente, terá de palavra-passe de Olá que foi criada quando o certificado de cliente Olá foi exportado. Normalmente, isto é apenas um fim de duplo clique em certificado Olá e instale-o. Para obter mais informações, veja [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install)(Instalar um certificado de cliente exportado).

## <a name="connect"></a>5. Ligar tooAzure

### <a name="connect-tooyour-vnet"></a>Ligar tooyour VNet

1. tooconnect tooyour VNet, no computador de cliente Olá, navegue até tooVPN ligações e localize a ligação de VPN de Olá que criou. Tem o nome Olá mesmo nome que a rede virtual. Clique em **Ligar**. Pode apresentada uma mensagem de pop-up que referencia o certificado de Olá toousing. Se isto acontecer, clique em **continuar** toouse privilégios elevados.
2. No Olá **ligação** página de estado, clique em **Connect** ligação de Olá toostart. Se vir um **selecionar certificado** ecrã, certifique-se de que Olá certificado de cliente apresentado é Olá uma que pretenda toouse tooconnect. Se não for, utilize o certificado correto do Olá na seta pendente tooselect Olá e, em seguida, clique em **OK**.

  ![Ligação de cliente VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. A ligação é estabelecida.

  ![Ligação estabelecida](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Resolução de problemas com ligações P2S

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Certifique-se a ligação de VPN Olá

1. tooverify que a ligação VPN está ativa, abra uma linha de comandos elevada e execute *ipconfig/all*.
2. Ver os resultados de Olá. Tenha em atenção que o endereço IP de Olá recebeu é um dos endereços de Olá dentro do intervalo de endereços de conetividade de Olá ponto a Site que especificou quando criou a VNet. resultados de Olá devem ser semelhante toothis exemplo:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Ligar a máquina virtual de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Adicionar ou remover certificados de raiz fidedigna

Pode adicionar e remover certificados de raiz fidedigna do Azure. Quando remove um certificado de raiz, os clientes que tenham um certificado gerado a partir desse raiz, não será capaz de tooauthenticate e, por conseguinte, não será capaz de tooconnect. Se pretender um tooauthenticate de cliente e se liga, terá tooinstall um novo certificado de cliente gerado a partir de um certificado de raiz fidedigna tooAzure (carregado).

### <a name="addtrustedroot"></a>tooadd um certificado de raiz fidedigna

Pode adicionar segurança too20 fidedigna raiz certificado. cer ficheiros tooAzure. Para obter instruções, consulte [secção 3 - ficheiro de. cer do certificado de raiz do carregamento Olá](#upload).

### <a name="removetrustedroot"></a>tooremove um certificado de raiz fidedigna

1. No Olá **ligações VPN** secção da página Olá para a sua VNet, clique em Olá **clientes** tooopen gráfico Olá **ponto a site VPN ligação** página.

  ![Clientes](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. No Olá **ligaçãopontoasitede** página, clique em **gerir certificados** tooopen Olá **certificados** página.<br>

  ![Página Certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. No Olá **certificados** página, clique em Olá reticências seguinte toohello certificado que pretende tooremove e clique em **eliminar**.

  ![Eliminar certificado de raiz](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Revogar um certificado de cliente

Pode revogar certificados de cliente. certificado de Olá lista de revogação permite-lhe tooselectively negar conetividade ponto a Site com base em certificados de cliente individuais. Isto é diferente da remoção de um certificado de raiz fidedigna. Se remover um certificado de raiz fidedigna. cer do Azure, revoga acesso Olá para todos os certificados de cliente gerado/assinado pelo certificado de raiz revogados Olá. Revogar um certificado de cliente, em vez de certificado de raiz de Olá, permite Olá outros certificados que foram gerados a partir de Olá raiz certificado toocontinue toobe utilizado para autenticação da ligação de Olá ponto a Site.

prática comum Olá é acesso toomanage certificado de raiz de Olá de toouse níveis equipa ou organização, ao utilizar certificados de cliente revogados para controlo de acesso detalhada nos utilizadores individuais.

### <a name="revokeclientcert"></a>toorevoke um certificado de cliente

Pode revogar um certificado de cliente através da adição de lista de revogação Olá thumbprint toohello.

1. Obter o thumbprint do certificado de cliente de Olá. Para obter mais informações, consulte [como: obter Olá Thumbprint de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copie o editor de texto do Olá informações tooa e remova todos os espaços para que seja uma cadeia de carateres contínua.
3. Navegue toohello **'nome de rede virtual clássica' > ligação VPN ponto a site > certificados** página e, em seguida, clique em **lista de revogação** página de lista de revogação de Olá tooopen. 
4. No Olá **lista de revogação** página, clique em **+ adicionar certificado** tooopen Olá **lista do adicionar certificado toorevocation** página.
5. No Olá **lista do adicionar certificado toorevocation** página, cole o thumbprint do certificado Olá como uma linha contínua de texto, sem espaços. Clique em **OK** em Olá parte inferior da página Olá.
6. Uma vez concluída a atualização, o certificado de Olá já não pode ser utilizado tooconnect. Clientes que tentam tooconnect utilizando este certificado de recebem uma mensagem a indicar que se o certificado Olá já não é válido.

## <a name="faq"></a>FAQ Ponto a Site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Passos seguintes
Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Para obter mais informações, veja [Máquinas Virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand mais informações sobre o funcionamento em rede e máquinas virtuais, consulte [descrição geral da rede do Azure e a VM com Linux](../virtual-machines/linux/azure-vm-network-overview.md).
