---
title: "Ligar uma rede virtual de computador tooa através da autenticação ponto a Site e o certificado: Portal do Azure | Microsoft Docs"
description: "Liga de forma segura tooyour um computador Virtual Network do Azure através da criação de uma ligação de gateway VPN de ponto a Site utilizando a autenticação de certificado. Este artigo aplica-se do modelo de implementação do Resource Manager toohello e utiliza Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Configurar um tooa de ligação de ponto a Site VNet através da autenticação de certificado: portal do Azure

Este artigo mostra como toocreate uma VNet com uma ligação ponto a Site utilizando modelo de implementação de Gestor de recursos do Olá Olá portal do Azure. Esta configuração utilize Olá tooauthenticate de certificados a ligação de cliente. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Um gateway de VPN de ponto a Site (P2S) permite-lhe criar uma rede virtual de tooyour ligação segura a partir de um computador de cliente individuais. Ligações de VPN ponto a Site são úteis quando pretende tooconnect tooyour VNet a partir de uma localização remota, tal como quando são telecommuting casa ou numa conferência. Uma VPN P2S também é toouse uma excelente solução em vez de uma VPN de Site a Site quando tem apenas alguns clientes que necessitam de tooconnect tooa VNet. 

Utiliza P2S Olá Secure Socket Tunneling Protocol (SSTP), que é um protocolo VPN baseada em SSL. É estabelecida uma ligação de P2S VPN ao iniciá-lo a partir do computador de cliente Olá.

![Diagrama Ponto a Site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Ligações de autenticação de certificado de ponto a Site requerem seguinte Olá:

* Um gateway de VPN RouteBased.
* Olá chave pública (ficheiro. cer) para um certificado de raiz, que é carregado tooAzure. Depois do certificado de Olá é carregado, é considerada um certificado fidedigno e é utilizado para autenticação.
* Um certificado de cliente que é gerado a partir do certificado de raiz de Olá e instalado em cada computador cliente que irão ligar toohello VNet. Este certificado é utilizado para autenticação de cliente.
* Um pacote de configuração do cliente VPN. pacote de configuração de cliente VPN Olá contém informações necessárias do Olá para Olá cliente tooconnect toohello VNet. pacote de Olá configura o cliente VPN existente Olá que é nativo toohello sistema operativo Windows. Cada cliente que estabelece ligação tem de ser configurado utilizando o pacote de configuração de Olá.

As ligações Ponto a Site não precisam de nenhum dispositivo VPN ou endereço IP destinado ao público no local. Olá ligação VPN é criado através de SSTP (Secure Socket Tunneling Protocol). No lado do servidor de Olá, suportamos versões SSTP 1.0, 1.1 e 1.2. cliente de Olá decide que toouse de versão. Para o Windows 8.1 e versões posteriores, o SSTP utiliza 1.2 por predefinição.

Para obter mais informações sobre ligações ponto a Site, consulte Olá [ponto a Site FAQ](#faq) no fim de Olá deste artigo.

#### <a name="example"></a>Valores de exemplo

Pode utilizar os seguintes valores toocreate num ambiente de teste de Olá, ou consulte valores toothese toobetter compreender exemplos Olá neste artigo:

* **Nome da VNet:** VNet1
* **Espaço de endereços:** 192.168.0.0/16<br>Para este exemplo, utilizamos apenas um espaço de endereços. Pode ter mais do que um espaço de endereços para a sua VNet.
* **Nome da sub-rede:** FrontEnd
* **Intervalo de endereços da sub-rede:** 192.168.1.0/24
* **Subscrição:** se tiver mais do que uma subscrição, certifique-se de que está a utilizar Olá correto.
* **Grupo de Recursos:** TestRG
* **Localização:** E.U.A. Leste
* **GatewaySubnet:** 192.168.200.0/24<br>
* **Servidor DNS:** (opcional) endereço IP do servidor DNS de Olá que pretende que toouse para resolução de nomes.
* **Nome do gateway de rede virtual:** VNet1GW
* **Tipo de gateway:** VPN
* **Tipo de VPN:** baseado na rota
* **Nome do endereço IP público:** VNet1GWpip
* **Tipo de ligação:** Ponto a site
* **Conjunto de endereços do cliente:** 172.16.201.0/24<br>Os clientes VPN que se ligam toohello VNet com esta ligação ponto a Site recebem um endereço IP do conjunto de endereços de cliente Olá.

## <a name="createvnet"></a>1. Criar uma rede virtual

Antes de começar, verifique se tem uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Adicionar uma sub-rede do gateway

Antes de ligar o gateway de tooa da rede virtual, terá primeiro de sub-rede do gateway toocreate Olá Olá toowhich de rede virtual pretende tooconnect. os serviços de gateway Olá utilizar endereços IP de Olá especificados na sub-rede do gateway Olá. Se for possível, crie uma sub-rede de gateway utilizando um bloco CIDR de/28 ou /27 tooprovide suficiente IP endereços tooaccommodate requisitos de configuração futuras adicionais.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Especificar um servidor DNS (opcional)

Depois de criar a rede virtual, pode adicionar endereço IP Olá uma resolução de nomes do DNS server toohandle. servidor DNS Olá é opcional para esta configuração, mas necessário se pretender que a resolução do nome. A especificação de um valor não cria um novo servidor DNS. Olá endereço IP de servidor DNS que especificar deve ser um servidor DNS que pode resolver nomes de Olá dos recursos de Olá que está a ligar. Neste exemplo, é utilizado um endereço IP privado, mas é provável que não se trata de endereço IP hello do servidor DNS. Ser toouse se os seus próprios valores.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Criar um gateway de rede virtual

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Gerar certificados

Certificados são utilizados por clientes de tooauthenticate do Azure que se ligam tooa VNet através de uma ligação VPN ponto a Site. Depois de obter um certificado de raiz, [carregar](#uploadfile) Olá tooAzure de informações de chaves públicas. certificado de raiz de Olá, em seguida, é considerado 'considerado confiável' pelo Azure para ligação através de rede virtual do P2S toohello. Também gerar os certificados de cliente de certificado de raiz fidedigna Olá e, em seguida, instalá-los em cada computador cliente. certificado de cliente Olá é cliente de Olá tooauthenticate utilizado quando inicia a toohello uma ligação VNet. 

### <a name="getcer"></a>1. Obter o ficheiro. cer de Olá para certificado de raiz de Olá

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Gerar um certificado de cliente

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Adicionar o conjunto de endereços de cliente Olá

conjunto de endereços de cliente Olá é um intervalo de endereços IP privados que especificar. os clientes de Olá que ligam através de uma VPN ponto a Site recebem um endereço IP de neste intervalo. Utilize um intervalo de endereços IP privado que não se sobreponha a com a localização no local Olá que ligue a partir de ou Olá VNet que pretende que sejam tooconnect para.

1. Assim que tiver sido criado o gateway de rede virtual Olá, navegue até toohello **definições** secção da página de gateway de rede virtual Olá. No Olá **definições** secção, clique em **configuraçãoponto a site** tooopen Olá **ponto-a-Site-configuração** página.

  ![Página Ponto a Site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. No Olá **ponto-a-Site-configuração** página, pode eliminar o intervalo de preenchimento automático Olá, em seguida, adicionar Olá privado intervalo de endereços IP que pretende que o toouse. Clique em **guardar** toovalidate e guardar a definição de Olá.

  ![Conjunto de endereços de cliente](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Carregar dados de certificado pública do certificado de raiz Olá

Depois de ter sido criado o gateway de Olá, carregue as informações de chaves públicas Olá para tooAzure de certificado de raiz de Olá. Assim que são carregados dados de certificado público de Olá, Azure pode utilizá-la tooauthenticate clientes que têm instalado um certificado de cliente gerado a partir do certificado de raiz fidedigna Olá. Pode carregar total de tooa de cópia de segurança de certificados de raiz fidedigna adicionais de 20.

1. Certificados são adicionados em Olá **configuraçãoponto a site** página Olá **certificado de raiz** secção.  
2. Certifique-se de que exportou o certificado de raiz de Olá como uma Base-64 codificado ficheiro x. 509 (. cer). Precisa de certificado de Olá tooexport este formato, para abrir o certificado de Olá com o editor de texto.
3. Abra o certificado de Olá com um editor de texto, como o bloco de notas. Quando copiar dados de certificado Olá, certifique-se que copie o texto de Olá como uma linha contínua sem mudanças ou avanços de linha. Poderá ser necessário toomodify vista em too'Show de editor de texto Olá símbolo/Mostrar avanço do todos os carateres toosee Olá devolve e feeds de linha. Copie Olá apenas secção como uma linha contínua os seguintes:

  ![Dados de certificado](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Cole os dados de certificado de Olá Olá **dados de certificado pública** campo. **Nome** Olá certificado e, em seguida, clique em **guardar**. Pode adicionar configurar certificados de raiz too20 fidedigna.

  ![Carregamento de certificados](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Gerar e instalar o pacote de configuração de cliente VPN Olá

tooconnect tooa VNet com uma VPN ponto a Site, cada cliente tem de instalar um pacote de configuração de cliente que configura o cliente VPN nativo do Olá com definições de Olá e ficheiros de rede virtual do toohello tooconnect necessário. Configura o pacote de configuração de cliente VPN Olá nativo cliente de VPN do Windows hello, não instala um cliente VPN novo ou diferente.

Pode utilizar Olá a mesma configuração de cliente VPN do pacote em cada computador cliente, desde que a versão de Olá corresponde à arquitetura de Olá para cliente Olá. Para Olá obter lista de sistemas operativos cliente que são suportados, consulte Olá [ligaçõespontoaSitedeFAQ](#faq) no fim de Olá deste artigo.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Passo 1 – gerar e transferir o pacote de configuração de cliente Olá

1. No Olá **configuraçãoponto a site** página, clique em **cliente VPN transferir** tooopen Olá **cliente VPN transferir** página. Demorará um minuto ou dois para Olá toogenerate de pacote.

  ![transferência do cliente VPN 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Selecione o pacote correto Olá para o cliente e, em seguida, clique em **transferir**. Guarde o ficheiro de pacote de configuração de Olá. Instalar o pacote de configuração de cliente VPN Olá em cada computador cliente que liga toohello de rede virtual.

  ![transferência do cliente VPN 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Passo 2 - pacote de configuração de cliente de Olá de instalação

1. Cópia de ficheiros de configuração de Olá localmente toohello computador de que pretende que a rede virtual do tooconnect tooyour. 
2. Faça duplo clique em pacote de Olá .exe ficheiros tooinstall Olá no computador de cliente Olá. Uma vez criado o pacote de configuração de Olá, não tem sessão iniciada e poderá ver um aviso. Se obtiver um pop-up do Windows SmartScreen, clique em **obter mais informações** (no lado esquerdo Olá), em seguida, **executar mesmo assim** pacote de Olá tooinstall.
3. Instale o pacote de Olá no computador de cliente Olá. Se obtiver um pop-up do Windows SmartScreen, clique em **obter mais informações** (no lado esquerdo Olá), em seguida, **executar mesmo assim** pacote de Olá tooinstall.
4. No computador de cliente Olá, navegue demasiado**as definições de rede** e clique em **VPN**. Olá ligação VPN mostra o nome de Olá da rede virtual Olá que este se liga a.

## <a name="installclientcert"></a>9. Instalar um certificado de cliente exportado

Se pretender toocreate um P2S ligação de um computador cliente que não sejam Olá um utilizou certificados de cliente toogenerate Olá, precisa de tooinstall um certificado de cliente. Ao instalar um certificado de cliente, terá de palavra-passe de Olá que foi criada quando o certificado de cliente Olá foi exportado. Normalmente, é apenas um fim de duplo clique em certificado Olá e instale-o.

Certifique-se de que o certificado de cliente Olá foi exportado como um ficheiro. pfx, juntamente com a cadeia de certificados inteira Olá (que é a predefinição de Olá). Caso contrário, as informações do certificado de raiz Olá não estão presentes no computador de cliente Olá e cliente Olá não será capaz de tooauthenticate corretamente. Para obter mais informações, veja [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install)(Instalar um certificado de cliente exportado).

## <a name="connect"></a>10. Ligar tooAzure

1. tooconnect tooyour VNet, no computador de cliente Olá, navegue até tooVPN ligações e localize a ligação de VPN de Olá que criou. Tem o nome Olá mesmo nome que a rede virtual. Clique em **Ligar**. Pode apresentada uma mensagem de pop-up que referencia o certificado de Olá toousing. Clique em **continuar** toouse privilégios elevados.

2. No Olá **ligação** página de estado, clique em **Connect** ligação de Olá toostart. Se vir um **selecionar certificado** ecrã, certifique-se de que Olá certificado de cliente apresentado é Olá uma que pretenda toouse tooconnect. Se não for, utilize o certificado correto do Olá na seta pendente tooselect Olá e, em seguida, clique em **OK**.

  ![Cliente VPN liga tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. A ligação é estabelecida.

  ![Ligação estabelecida](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Resolução de problemas com ligações P2S

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Verificar a ligação

1. tooverify que a ligação VPN está ativa, abra uma linha de comandos elevada e execute *ipconfig/all*.
2. Ver os resultados de Olá. Tenha em atenção que o endereço IP de Olá recebeu é um dos endereços Olá Olá ponto a Site VPN cliente conjunto de endereços que especificou na configuração. resultados de Olá são semelhantes toothis exemplo:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Ligar a máquina virtual de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Adicionar ou remover certificados de raiz fidedigna

Pode adicionar e remover certificados de raiz fidedigna do Azure. Quando remove um certificado de raiz, os clientes que tenham um certificado gerado a partir desse raiz, não será capaz de tooauthenticate e, por conseguinte, não será capaz de tooconnect. Se pretender um tooauthenticate de cliente e se liga, terá tooinstall um novo certificado de cliente gerado a partir de um certificado de raiz fidedigna tooAzure (carregado).

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd um certificado de raiz fidedigna

Pode adicionar segurança too20 fidedigna raiz certificado. cer ficheiros tooAzure. Para obter instruções, consulte a secção de Olá [carregar um certificado de raiz fidedigna](#uploadfile) neste artigo.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove um certificado de raiz fidedigna

1. tooremove um certificado de raiz fidedigna, navegue toohello **configuraçãoponto a site** página para o gateway de rede virtual.
2. No Olá **certificado de raiz** secção da página Olá, localize o certificado de Olá que pretende que o tooremove.
3. Clique Olá reticências seguinte toohello certificado e, em seguida, clique em 'Remover'.

## <a name="revokeclient"></a>Revogar um certificado de cliente

Pode revogar certificados de cliente. certificado de Olá lista de revogação permite-lhe tooselectively negar conetividade ponto a Site com base em certificados de cliente individuais. Isto é diferente da remoção de um certificado de raiz fidedigna. Se remover um certificado de raiz fidedigna. cer do Azure, revoga acesso Olá para todos os certificados de cliente gerado/assinado pelo certificado de raiz revogados Olá. Revogar um certificado de cliente, em vez de certificado de raiz de Olá, permite Olá outros certificados que foram gerados a partir de Olá raiz certificado toocontinue toobe utilizado para autenticação.

prática comum Olá é acesso toomanage certificado de raiz de Olá de toouse níveis equipa ou organização, ao utilizar certificados de cliente revogados para controlo de acesso detalhada nos utilizadores individuais.

### <a name="toorevoke-a-client-certificate"></a>toorevoke um certificado de cliente

Pode revogar um certificado de cliente através da adição de lista de revogação Olá thumbprint toohello.

1. Obter o thumbprint do certificado de cliente de Olá. Para obter mais informações, consulte [como tooretrieve Olá Thumbprint de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copie o editor de texto do Olá informações tooa e remova todos os espaços para que seja uma cadeia de carateres contínua.
3. Navegue até o gateway de rede virtual toohello **ponto-a-site-configuração** página. Este é Olá mesma página que utilizou demasiado[carregar um certificado de raiz fidedigna](#uploadfile).
4. No Olá **certificados revogados** secção, introduza um nome amigável para o certificado de Olá (não tem CN do certificado de Olá toobe).
5. Copie e cole Olá thumbprint cadeia toohello **Thumbprint** campo.
6. thumbprint Olá valida e é adicionado automaticamente a lista de revogação toohello. É apresentada uma mensagem no ecrã de Olá esse Olá lista está a atualizar. 
7. Uma vez concluída a atualização, o certificado de Olá já não pode ser utilizado tooconnect. Clientes que tentam tooconnect utilizando este certificado de recebem uma mensagem a indicar que se o certificado Olá já não é válido.

## <a name="faq"></a>FAQ Ponto a Site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Passos seguintes
Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Para obter mais informações, veja [Máquinas Virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand mais informações sobre o funcionamento em rede e máquinas virtuais, consulte [descrição geral da rede do Azure e a VM com Linux](../virtual-machines/linux/azure-vm-network-overview.md).
