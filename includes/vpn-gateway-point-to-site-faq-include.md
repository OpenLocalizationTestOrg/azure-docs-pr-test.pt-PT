### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Que sistemas operativos cliente posso utilizar com a ligação Ponto a Site?

é suportado Olá os seguintes sistemas operativos cliente:

* Windows 7 (32 e 64 bits)
* Windows Server 2008 R2 (apenas 64 bits)
* Windows 8 (32 e 64 bits)
* Windows 8.1 (32 e 64 bits)
* Windows Server 2012 (apenas 64 bits)
* Windows Server 2012 R2 (apenas 64 bits)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Posso utilizar qualquer cliente VPN de software para a ligação Ponto a Site que suporte SSTP?

Não. O suporte está limitadas apenas toohello Windows versões do sistema operativo listadas acima.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Quantos pontos finais de cliente VPN posso ter na minha configuração Ponto a Site?

Fornecemos suporte de cópia de segurança too128 VPN clientes toobe tooconnect capaz de tooa rede virtual no Olá mesmo tempo.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Posso utilizar AC de raiz de PKI interna para a conetividade Ponto a Site?

Sim. Anteriormente, só podiam ser utilizados os certificados de raiz autoassinados. Ainda pode carregar 20 certificados de raiz.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Posso atravessar proxies e firewalls com a capacidade Ponto a Site?

Sim. Utilizamos o SSTP (Secure Socket Tunneling Protocol) tootunnel através de firewalls. Este túnel aparece como uma ligação HTTPs.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Se reiniciar o computador cliente configurado para ponto a Site, será hello VPN restabelece ligação automaticamente?

Por predefinição, computador de cliente Olá não restabelece ligação de VPN Olá automaticamente.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Ponto a Site suporta restabelecimento de ligação automático e DDNS nos Olá clientes VPN?

Atualmente, o restabelecimento de ligação automático e DDNS não são suportados nas VPNs Ponto a Site.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Posso ter Site a Site e configurações ponto a Site coexistem para Olá mesma rede virtual?

Sim. Ambas as soluções funcionarão se tiver um tipo de VPN RouteBased para o gateway. Para o modelo de implementação clássica Olá, é necessário um gateway dinâmico. Fazemos não suporte ponto a Site para gateways de VPN de encaminhamento estático ou gateways que utilizem Olá `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Pode configurar um ponto a Site cliente tooconnect toomultiple redes virtuais no Olá mesmo tempo?

Sim, é possível. Mas redes virtuais Olá não podem ter prefixos IP sobrepostos e espaços de endereços de Olá ponto a Site não pode sobrepor entre redes virtuais Olá.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Que débito posso esperar através das ligações Site a Site ou Ponto a Site?

É difícil toomaintain débito exato de Olá de túneis VPN de Olá. O IPsec e SSTP são protocolos VPN extremamente encriptados. O débito também é limitado pela latência Olá e largura de banda entre o local e Olá Internet.
