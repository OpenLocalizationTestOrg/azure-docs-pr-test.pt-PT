---
title: "aaaAzure DMZ exemplo – criar uma rede de Perímetro simples com NSGs | Microsoft Docs"
description: "Criar uma rede de Perímetro com grupos de segurança de rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Exemplo 1 – criar uma rede de Perímetro simple utilizando NSGs com um modelo Azure Resource Manager
[Devolver toohello segurança limites melhores práticas de página][HOME]

> [!div class="op_single_selector"]
> * [Modelo do Resource Manager](virtual-networks-dmz-nsg.md)
> * [Clássico - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Este exemplo cria uma rede de Perímetro primitivo com quatro servidores do Windows e grupos de segurança de rede. Este exemplo descreve cada um dos Olá modelo relevantes secções tooprovide uma compreensão mais aprofundada de cada passo. Há também um tooprovide da secção de cenário de tráfego uma visão passo a passo detalhada das como procede de tráfego através de camadas de Olá de defesa nas Olá DMZ. Por fim, na secção de referências de Olá é toobuild de código e as instruções do modelo completo de Olá este ambiente tootest e experiência com vários cenários. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![Rede de Perímetro entrada com o NSG][1]

## <a name="environment-description"></a>Descrição de ambiente
Neste exemplo, uma subscrição contém Olá os seguintes recursos:

* Um grupo de recursos única
* Uma rede Virtual com duas sub-redes; "FrontEnd" e "BackEnd"
* Um grupo de segurança de rede que é aplicado tooboth sub-redes
* Um servidor do Windows que representa um servidor de web de aplicação ("IIS01")
* Servidores de dois windows que representam servidores de back-end de aplicação ("AppVM01", "AppVM02")
* Um servidor do Windows que representa um servidor DNS ("DNS01")
* Um endereço IP público associado ao servidor de web de aplicação Olá

Na secção de referências de Olá, há um modelo Azure Resource Manager tooan de ligação que cria o ambiente de Olá descrito neste exemplo. Edifício Olá VMs e as redes virtuais, embora efetuada pelo modelo de exemplo de Olá, não são descritas em detalhe neste documento. 

**toobuild neste ambiente** (instruções detalhadas são Olá referências secção deste documento);

1. Implementar Olá modelo de Gestor de recursos do Azure em: [modelos de início rápido do Azure][Template]
2. Instalar a aplicação de exemplo de Olá em: [Script de aplicação de exemplo][SampleApp]

>[!NOTE]
>servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir". Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end. Em alternativa um IP público pode ser associado a cada servidor NIC para RDP mais fácil.
> 
>

Olá secções seguintes fornecem uma descrição detalhada do Olá grupo de segurança de rede e como funciona para este exemplo orientando através de chaves linhas de Olá modelo do Azure Resource Manager.

## <a name="network-security-groups-nsg"></a>Grupos de Segurança de Rede (NSG)
Para este exemplo, um grupo NSG está criado e, em seguida, carregar com regras de seis. 

>[!TIP]
>Um modo geral, deve primeiro criar as regras de "Permitir" específicas e, em seguida, hello mais genéricas "Deny" regras pela última vez. Olá prioridade atribuída determinam as regras são avaliadas primeiro. Assim que o tráfego for encontrado regras específicas de tooa tooapply, não existem regras adicionais são avaliadas. Podem aplicar regras do NSG no Olá direção de entrada ou de saída (perspetiva Olá da sub-rede Olá).
>
>

Forma declarativa, Olá seguintes regras está a ser criado para o tráfego de entrada:

1. O tráfego DNS interno (porta 53) é permitido
2. O tráfego RDP (porta 3389) do Olá Internet tooany VM é permitido
3. Tráfego HTTP (porta 80) do servidor de tooweb Olá Internet (IIS01) é permitido
4. Qualquer tráfego (todas as portas) de IIS01 tooAppVM1 é permitido
5. Qualquer tráfego (todas as portas) de Olá Internet toohello VNet completo (ambas as sub-redes) é negado
6. Qualquer tráfego (todas as portas) da sub-rede de back-end do Olá front-end sub-rede toohello é negado

Com a sub-rede de tooeach vinculada estas regras, se um pedido de HTTP foi recebido do servidor web do Olá Internet toohello, ambas as regras 3 (permitir) e 5 (negar) seria aplicada, mas uma vez que a regra 3 tem uma prioridade mais alta apenas seria aplicada e regra 5 não seria entrem em play. Deste modo, pedidos de HTTP Olá seriam permitido toohello servidor de web. Se esse mesmo tráfego estava a tentar servidor de DNS01 tooreach Olá, regra 5 (negar) seria Olá primeiro tooapply e Olá o tráfego seria não ser permitido toopass toohello servidor. Regra 6 (negar) blocos de sub-rede de front-end de Olá de falar com a sub-rede de back-end toohello (exceto para o tráfego permitido nas regras de 1 e 4), este conjunto de regras protege a rede de back-end Olá no caso de uma atacante compromissos Olá aplicação web no Olá front-end, atacante Olá seria limitada toohello acesso back-end "protegido" rede (apenas tooresources exposto no servidor de AppVM01 Olá).

Há uma regra de saída predefinida que lhe permite tráfego de saída toohello internet. Neste exemplo, vamos está a permitir o tráfego de saída e não modificar quaisquer regras de saída. tooapply tootraffic de política de segurança em ambas as direções, o utilizador definidas encaminhamento é necessário e é explorou "Exemplo 3" no Olá [segurança limites melhores práticas página][HOME].

Cada regra é abordada mais detalhadamente:

1. Um recurso do grupo de segurança de rede tem de ser toohold instanciadas Olá regras:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. primeira regra de Olá neste exemplo permite o tráfego DNS entre todas as redes internas toohello DNS o servidor na sub-rede de back-end Olá. regra de Olá tem alguns parâmetros importantes:
  * "destinationAddressPrefix" - regras podem utilizar um tipo especial de prefixo de endereço denominado um "etiqueta predefinida", estas etiquetas são identificadores fornecidos pelo sistema que permitem uma forma fácil tooaddress uma categoria superior dos prefixos de endereço. Esta regra utiliza Olá etiqueta predefinida "Internet" toosignify qualquer endereço fora Olá VNet. Outras etiquetas de prefixo são VirtualNetwork e AzureLoadBalancer.
  * "Direção" significa na direção do fluxo de tráfego esta regra entra em vigor. direção de Olá é a partir da perspetiva de Olá de Olá sub-redes ou máquinas virtuais (dependendo de onde está vinculado esta NSG). Deste modo, se direção "Entrada" e o tráfego está a entrar sub-rede Olá, seria aplicada a regra de Olá e tráfego que sai Olá sub-rede não seria afetado por esta regra.
  * "Prioridade" define a ordem de Olá avaliação de um fluxo de tráfego. Olá Olá número Olá superior Olá prioridade inferior. Quando uma regra aplica-se o fluxo de tráfego específico tooa, não existem regras adicionais são processadas. Deste modo, se uma regra com prioridade 1 permite que o tráfego e uma regra com prioridade 2 nega tráfego e ambas as regras aplicam-se tootraffic, em seguida, o tráfego de Olá seria permitido tooflow (uma vez que a regra 1 tinha uma prioridade mais alta demorou em vigor e não existem regras adicionais foram aplicadas).
  * "Acesso" significa tráfego afetado por esta regra estiver bloqueado ("Deny") ou permitido ("Permitir").

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Esta regra permite tooflow de tráfego RDP de porta RDP do Olá internet toohello em qualquer servidor na Olá vinculado sub-rede. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Esta regra permite entrada internet tráfego toohit Olá servidor web. Esta regra não altera o comportamento de encaminhamento Olá. regra de Olá permite apenas tráfego destinado IIS01 toopass. Deste modo, se o tráfego de Internet de Olá tinha o servidor de web de Olá como respectivo destino desta regra seria permitir que e param de processar mais regras. (Regra de Olá com a prioridade é bloqueado 140 todos os outro internet tráfego de entrada). Se apenas estiver a processar tráfego HTTP, esta regra pode ser mais restrito tooonly Permitir destino porta 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Esta regra permite tráfego toopass do servidor de IIS01 Olá toohello AppVM01 servidor, uma regra posterior bloqueia todo o restante front-end tooBackend tráfego. tooimprove esta regra, se a porta de Olá é conhecida que deve ser adicionada. Por exemplo, se o servidor IIS Olá é atingir apenas SQL Server em AppVM01, Olá intervalo de portas de destino deve ser alterado de "*" (Any) too1433 (Olá porta do SQL Server), permitindo assim que uma superfície de ataque de entrada inferior em AppVM01 aplicação web de Olá alguma vez comprometida.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Esta regra negar o tráfego de servidores de tooany Olá internet numa rede de Olá. Com regras de Olá em prioridade 110 e 120, o efeito de Olá é tooallow apenas internet tráfego toohello firewall de entrada e de portas RDP nos servidores e bloqueia tudo o resto. Esta regra é um "isento" regra tooblock todos os fluxos inesperados.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. regra final Olá nega o tráfego de sub-rede de back-end do Olá front-end sub-rede toohello. Uma vez que esta regra é uma regra de só de entrada, o tráfego inverso é permitido (a partir de Olá back-end toohello front-end).

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Cenários de tráfego
#### <a name="allowed-internet-tooweb-server"></a>(*Permitidos*) servidor da Internet tooweb
1. Um utilizador de internet solicita uma página HTTP de endereço IP público de Olá do Olá que NIC associada Olá IIS01 NIC
2. Olá endereço IP público transmite tráfego toohello VNet para IIS01 (servidor de web de Olá)
3. Sub-rede de front-end inicia o processamento da regra de entrada:
  1. Não aplicar regras de NSG 1 (DNS), mover toonext regra
  2. Regras de NSG 2 (RDP) não se aplica, mover toonext regra
  3. Aplicar regras de NSG 3 (Internet tooIIS01), o tráfego é o processamento da regra permitido, parar
4. O tráfego chega a um endereço IP do servidor de web de Olá IIS01 (10.0.1.5)
5. IIS01 está à escuta para o tráfego web, este pedido de recebe e inicia o processamento de pedido de Olá
6. IIS01 pede-lhe Olá do SQL Server no AppVM01 informações
7. Não existem regras de saída na sub-rede do front-end, o tráfego é permitido
8. sub-rede de back-end de Olá inicia o processamento da regra de entrada:
  1. Não aplicar regras de NSG 1 (DNS), mover toonext regra
  2. Regras de NSG 2 (RDP) não se aplica, mover toonext regra
  3. NSG regra 3 (Internet tooFirewall) não se aplica, mover toonext regra
  4. Aplicar regras de NSG 4 (IIS01 tooAppVM01), o tráfego é o processamento da regra permitido, parar
9. AppVM01 recebe Olá consulta SQL e responde
10. Uma vez que não existem quaisquer regras de saída na sub-rede de back-end Olá, resposta Olá é permitida
11. Sub-rede de front-end inicia o processamento da regra de entrada:
  1. Não há nenhuma regra NSG aplica-se tooInbound tráfego de Olá back-end sub-rede toohello front-end sub-rede, pelo que nenhuma das regras do NSG Olá são aplicáveis
  2. regra do sistema predefinido de Olá a permitir o tráfego entre sub-redes permitiria que este tráfego para que o tráfego de Olá é permitido.
12. servidor IIS Olá recebe a resposta SQL Olá conclui a resposta HTTP Olá e envia toohello autor do pedido
13. Uma vez que não existem quaisquer regras de saída na sub-rede do front-end de Olá, resposta Olá é permitida e Olá utilizador Internet recebe Olá web página pedida.

#### <a name="allowed-rdp-tooiis-server"></a>(*Permitidos*) servidor de tooIIS RDP
1. Um administrador do servidor na internet solicita um tooIIS01 de sessão do RDP no endereço IP público de Olá do Olá que NIC associada Olá NIC IIS01 (este endereço IP público pode ser encontrado através de Olá Portal ou o PowerShell)
2. Olá endereço IP público transmite tráfego toohello VNet para IIS01 (servidor de web de Olá)
3. Sub-rede de front-end inicia o processamento da regra de entrada:
  1. Não aplicar regras de NSG 1 (DNS), mover toonext regra
  2. Aplicar regras de NSG 2 (RDP), o tráfego é o processamento da regra permitido, parar
4. Não existem regras de saída, aplicam regras predefinidas e retorno tráfego é permitido
5. Sessão do RDP está ativado
6. Pedidos de IIS01 Olá nome de utilizador e palavra-passe

>[!NOTE]
>servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir". Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Permitidos*) pesquisar DNS de servidor Web num servidor DNS
1. Web necessidades de servidor, IIS01, dados de um feed em www.data.gov, mas tem de tooresolve Olá endereço.
2. Olá configuração de rede para as listas de VNet Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como servidor DNS primário do Olá, IIS01 envia Olá DNS pedido tooDNS01
3. Não existem regras de saída na sub-rede do front-end, o tráfego é permitido
4. Sub-rede de back-end inicia o processamento da regra de entrada:
  * Aplicar regras de NSG 1 (DNS), o tráfego é o processamento da regra permitido, parar
5. Servidor DNS recebe o pedido de Olá
6. Servidor DNS não tem endereços Olá em cache e pede-lhe um servidor DNS de raiz no Olá internet
7. Não existem regras de saída na sub-rede de back-end, o tráfego é permitido
8. Servidor DNS de Internet responde, uma vez que esta sessão foi iniciada internamente, resposta Olá é permitida
9. Servidor DNS coloca Olá resposta em cache e responde toohello pedido inicial back tooIIS01
10. Não existem regras de saída na sub-rede de back-end, o tráfego é permitido
11. Sub-rede de front-end inicia o processamento da regra de entrada:
  1. Não há nenhuma regra NSG aplica-se tooInbound tráfego de Olá back-end sub-rede toohello front-end sub-rede, pelo que nenhuma das regras do NSG Olá são aplicáveis
  2. regra do sistema predefinido de Olá a permitir o tráfego entre sub-redes permitiria que este tráfego para que o tráfego de Olá é permitido
12. IIS01 recebe resposta Olá de DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Permitidos*) ficheiro de acesso do servidor Web no AppVM01
1. IIS01 pede-lhe um ficheiro num AppVM01
2. Não existem regras de saída na sub-rede do front-end, o tráfego é permitido
3. sub-rede de back-end de Olá inicia o processamento da regra de entrada:
  1. Não aplicar regras de NSG 1 (DNS), mover toonext regra
  2. Regras de NSG 2 (RDP) não se aplica, mover toonext regra
  3. NSG regra 3 (Internet tooIIS01) não se aplica, mover toonext regra
  4. Aplicar regras de NSG 4 (IIS01 tooAppVM01), o tráfego é o processamento da regra permitido, parar
4. AppVM01 recebe o pedido de Olá e responde com o ficheiro (partindo do princípio de acesso é autorizado)
5. Uma vez que não existem quaisquer regras de saída na sub-rede de back-end Olá, resposta Olá é permitida
6. Sub-rede de front-end inicia o processamento da regra de entrada:
  1. Não há nenhuma regra NSG aplica-se tooInbound tráfego de Olá back-end sub-rede toohello front-end sub-rede, pelo que nenhuma das regras do NSG Olá são aplicáveis
  2. regra do sistema predefinido de Olá a permitir o tráfego entre sub-redes permitiria que este tráfego para que o tráfego de Olá é permitido.
7. servidor IIS Olá recebe um ficheiro de Olá

#### <a name="denied-rdp-toobackend"></a>(*Negado*) RDP toobackend
1. Um utilizador de internet tenta tooRDP tooserver AppVM01
2. Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá
3. No entanto se foi ativado um endereço IP público por algum motivo, a regra NSG 2 (RDP) permitiria que este tráfego

>[!NOTE]
>servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir". Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Negado*) servidor de toobackend Web
1. Um utilizador de internet tenta tooaccess um ficheiro num AppVM01
2. Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá
3. Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueariam este tráfego

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Negado*) pesquisar Web DNS num servidor DNS
1. Um utilizador de internet tenta toolook se um registo DNS interno no DNS01
2. Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá
3. Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueariam este tráfego (Nota: se regra 1 (DNS) não seriam aplicadas porque Olá pede o endereço de origem são Olá internet e a regra 1 aplica-se apenas toohello VNet local como origem Olá)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Negado*) acesso do SQL Server no servidor de web de Olá
1. Um utilizador de internet solicita dados SQL IIS01
2. Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá
3. Se um endereço IP público foi ativado por algum motivo, a sub-rede do front-end de Olá começa processamento da regra de entrada:
  1. Não aplicar regras de NSG 1 (DNS), mover toonext regra
  2. Regras de NSG 2 (RDP) não se aplica, mover toonext regra
  3. Aplicar regras de NSG 3 (Internet tooIIS01), o tráfego é o processamento da regra permitido, parar
4. O tráfego chega a um endereço IP de Olá IIS01 (10.0.1.5)
5. IIS01 não está a escutar na porta 1433, por isso, não toohello um pedido de resposta

## <a name="conclusion"></a>Conclusão
Neste exemplo é uma forma avançar diretamente e relativamente simple de isolar a sub-rede de back-end Olá do tráfego de entrada.

Obter mais exemplos e uma descrição geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].

## <a name="references"></a>Referências
### <a name="azure-resource-manager-template"></a>Modelo Azure Resource Manager
Este exemplo utiliza um modelo Azure Resource Manager predefinidos num repositório GitHub mantido pela Microsoft e abrir toohello Comunidade. Este modelo pode ser implementado diretamente do GitHub ou transferiu e alterou toofit às suas necessidades. 

modelo de principais de Olá esteja num ficheiro Olá com o nome "azuredeploy. JSON". Este modelo pode ser submetido através do PowerShell ou o CLI (com o ficheiro de associado "azuredeploy.parameters.json" Olá) toodeploy este modelo. Posso encontrar Olá mais fácil é forma toouse Olá "Implementar tooAzure" botão na página de README.md Olá no GitHub.

modelo de Olá toodeploy que cria este exemplo a partir do GitHub e Olá portal do Azure, siga estes passos:

1. Num browser, navegue toohello [modelo][Template]
2. Clique no botão de "Implementar tooAzure" hello (ou Olá "Visualizar" botão toosee uma representação gráfica deste modelo)
3. Introduza Olá conta de armazenamento, nome de utilizador e palavra-passe no painel de parâmetros de Olá, em seguida, clique em **OK**
5. Criar um grupo de recursos para esta implementação (pode utilizar um existente, mas recomendada a um novo para obter os melhores resultados)
6. Se necessário, altere as definições de subscrição e localização Olá para a sua VNet.
7. Clique em **consultar termos legais**, Olá termos de licenciamento e clique em **Compra** tooagree.
8. Clique em **criar** toobegin implementação Olá deste modelo.
9. Após a conclusão com êxito da implementação de Olá, navegue toohello criado para esta implementação toosee Olá os recursos configurados no interior do grupo de recursos.

>[!NOTE]
>Este modelo permite RDP toohello IIS01 apenas servidor (Olá localizar um IP público para IIS01 no Olá Portal). servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir". Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.
>
>

tooremove esta implementação, Olá eliminar grupo de recursos e todos os recursos subordinados também serão eliminados.

#### <a name="sample-application-scripts"></a>Scripts de aplicação de exemplo
Assim que o modelo de Olá é executada com êxito, pode configurar Olá servidor web e servidor de aplicações com um tooallow de aplicação web simples testar com esta configuração de rede de Perímetro. tooinstall uma aplicação de exemplo para isto e outros exemplos de rede de Perímetro, um tiver sido fornecido no Olá seguinte hiperligação: [Script de aplicação de exemplo][SampleApp]

## <a name="next-steps"></a>Passos seguintes

* Implementar neste exemplo
* Criar aplicação de exemplo de Olá
* Testar os fluxos de tráfego diferentes através desta rede de Perímetro

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Rede de Perímetro entrada com o NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md