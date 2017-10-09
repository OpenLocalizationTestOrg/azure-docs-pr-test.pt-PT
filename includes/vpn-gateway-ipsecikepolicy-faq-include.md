### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>A política de IPsec/IKE personalizado é suportada em todos os SKU de Gateway de VPN do Azure?
A política de IPsec/IKE personalizada é suportada no Azure **VpnGw1, VpnGw2, VpnGw3, Standard** e nos gateways de VPN **HighPerformance**. O SKU **Básico** NÃO é suportado.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Quantas políticas posso especificar numa ligação?
Só pode especificar ***uma*** combinação de políticas para uma determinada ligação.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Posso especificar uma política parcial numa ligação? (Por exemplo, somente os algoritmos de IKE mas não IPsec)
Não, tem de especificar todos os parâmetros e algoritmos de IKE (modo principal) e IPsec (modo rápido). Não é permitida a especificação da política parcial.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Quais são os algoritmos de Olá e força da codificação chave suportada numa política personalizada do Olá?
tabela Olá abaixo apresenta uma lista de algoritmos criptográficos Olá suportado e chave força da codificação configuráveis por clientes de Olá. Tem de selecionar uma opção para cada campo.

| **IPsec/IKEv2**  | **Opções**                                                                   |
| ---              | ---                                                                           |
| Encriptação IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Integridade do IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Grupo DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, Nenhum |
| Encriptação do IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, Nenhum      |
| Integridade do IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Grupo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Nenhum                              |
| Duração de SA QM   | Segundos (número inteiro; **mín. 300** /predefinição de 27000 segundos)<br>KBytes (número inteiro; **mín. 1024** /predefinição de 102400000 KBytes)           |
| Seletor de tráfego | UsePolicyBasedTrafficSelectors ($True/$False; default $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 são Olá mesmo como grupo Diffie-Hellman **14** IKE e PFS de IPsec. Consulte [Diffie-Hellman grupos](#DH) para Olá conclua mapeamentos.
> 2. Algoritmos GCMAES, terá de especificar hello mesmo comprimento de algoritmo e a chave GCMAES para encriptação de IPsec e integridade.
> 3. Duração de SA de modo do IKEv2 principal é fixo no 28.800 segundos nos gateways de VPN do Azure Olá
> 4. As Durações de SA QM são parâmetros opcionais. Se “nenhum” tiver sido especificado, são utilizados os valores predefinidos dos segundos 27000 (7.5hrs) e 102400000 KBytes (102 GB).
> 5. UsePolicyBasedTrafficSelector é um parâmetro de opção numa ligação Olá. Consulte Olá FAQ sobre o seguinte item de "UsePolicyBasedTrafficSelectors"

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Tudo precisa toomatch entre Olá política do gateway de VPN do Azure e as minhas configurações de dispositivo VPN no local?
A configuração do dispositivo VPN no local tem de corresponder ou conter Olá seguir algoritmos e parâmetros que especificou no Olá política IPsec/IKE do Azure:

* Algoritmo de encriptação do IKE
* Algoritmo de integridade do IKE
* Grupo DH
* Algoritmo de encriptação do IPsec
* Algoritmo de integridade do IPsec
* Grupo PFS
* Seletor de tráfego (*)

durações de Olá SA apenas especificações locais, não precisa de toomatch.

Se ativar **UsePolicyBasedTrafficSelectors**, terá de tooensure o dispositivo VPN tem Olá correspondente definidos com todas as combinações dos seus prefixos de (gateway de rede local) de rede no local do Olá de seletores de tráfego Prefixos de rede virtual do Azure, em vez de qualquer a qualquer. Por exemplo, se os prefixos de rede no local são 10.1.0.0/16 e 10.2.0.0/16 e os prefixos de rede virtual são 192.168.0.0/16 e 172.16.0.0/16, terá de Olá toospecify seguir seletores de tráfego:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Consulte demasiado[ligar dispositivos VPN baseado na política vários locais](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter mais detalhes sobre como toouse esta opção.

### <a name ="DH"></a>Que Grupos de Diffie-Hellman são suportados?
tabela de Olá abaixo apresenta Olá suportado Diffie-Hellman grupos IKE (DHGroup) e para IPsec (PFSGroup):

| **Grupo Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Comprimento da chave** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP de 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP de 1024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP de 2048 bits  |
| 19                        | ECP256                   | ECP256       | ECP de 256 bits    |
| 20                        | ECP384                   | ECP284       | ECP de 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP de 2048 bits  |
|                           |                          |              |                |

Consulte demasiado[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) para obter mais detalhes.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Política personalizada do Olá substituir o Olá predefinido IPsec/IKE política conjuntos para gateways de VPN do Azure?
Sim, depois de uma política personalizada é especificada numa ligação, o gateway de VPN do Azure apenas utilizar política de Olá numa ligação Olá, tanto como iniciador de IKE e dispositivo de resposta do IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Se remover uma política personalizada do IPsec/IKE, ligação Olá tornar-se desprotegida?
Não, ligação Olá continuarão a estar protegida por IPsec/IKE. Depois de remover a política personalizada do Olá de uma ligação, o gateway de VPN do Azure Olá irá reverter back toohello [lista predefinida de propostas de IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) e iniciar novamente Olá handshake IKE novamente com o seu dispositivo VPN no local.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Adicionar ou atualizar uma política de IPsec/IKE pode atrapalhar a minha ligação VPN?
Sim, pode causar uma interrupção pequena (alguns segundos) como gateway de VPN do Azure Olá irá fechar as ligação existente Olá e iniciar novamente Olá IKE handshake toore-estabeleça o túnel IPsec de Olá com novos algoritmos criptográficos Olá e parâmetros. Certifique-se de que o dispositivo VPN no local também é configurado com algoritmos correspondente Olá e força da codificação chave toominimize Olá uma perturbação.

### <a name="can-i-use-different-policies-on-different-connections"></a>Posso usar políticas diferentes em ligações diferentes?
Sim. A política personalizada é aplicada consoante a ligação. Pode criar e aplicar diferentes políticas de IPsec/IKE em diferentes ligações. Também pode escolher tooapply políticas personalizadas num subconjunto de ligações. Olá restantes aqueles irá utilizar conjuntos de políticas de IPsec/IKE do Olá predefinido do Azure.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Pode utilizar a política personalizada do Olá, bem como a ligação VNet a VNet?
Sim, pode aplicar a política personalizada em ligações entre locais de IPsec ou em ligações VNet para VNet.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>É necessário toospecify Olá a mesma política em ambos os recursos de ligação de VNet a VNet?
Sim. Um túnel de VNet para VNet consiste em dois recursos de ligação no Azure, uma para cada direção. Terá de tooensure ambos os recursos de ligação ter Olá mesma política, não irão estabelecer othereise Olá ligação VNet a VNet.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>A política de IPsec/IKE personalizada funciona na ligação do ExpressRoute?
Não. Política do IPsec/IKE só funciona em S2S VPN e ligações VNet a VNet através de gateways de VPN do Azure Olá.
