

Existem dois níveis de balanceamento de carga disponíveis para os serviços de infraestrutura do Azure:

* **Nível de DNS**: balanceamento de carga para serviços de nuvem do tráfego toodifferent localizado nos dados de diferentes centros, toodifferent Web sites do Azure localizados em data centers diferentes ou tooexternal pontos finais. Isto é feito com o Gestor de tráfego do Azure e método de balanceamento de carga de Olá Round Robin.
* **Nível de rede**: de entrada Internet tráfego toodifferent máquinas virtuais de um serviço em nuvem de balanceamento de carga ou de tráfego entre máquinas virtuais numa rede virtual ou serviço em nuvem de balanceamento de carga. Isto é feito com Balanceador de carga do Azure de Olá.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Gestor de tráfego balanceamento de carga para serviços em nuvem e Web sites
Gestor de tráfego permite-lhe toocontrol distribuição Olá tooendpoints de tráfego do utilizador, que pode incluir serviços em nuvem, Web sites, sites externos e outros perfis do Traffic Manager. Gestor de tráfego funciona ao aplicar uma política inteligente motor tooDomain Name System (DNS) as consultas para nomes de domínio Olá dos seus recursos de Internet. Os serviços em nuvem ou Web sites podem estar em execução em datacenters diferentes em Olá mundo.

Tem de utilizar REST ou o Windows PowerShell tooconfigure pontos finais externos ou perfis do Traffic Manager como pontos finais.

Gestor de tráfego utiliza três tráfego de toodistribute de métodos de balanceamento de carga:

* **Ativação pós-falha**: Utilize este método quando pretender toouse um ponto final principal para todo o tráfego, mas fornecem as cópias de segurança no caso de Olá primário fica indisponível.
* **Desempenho**: Utilize este método se tiver pontos finais em localizações geográficas diferentes e pretender que os clientes toouse Olá "mais próximo" ponto final em termos de latência mais baixa Olá a pedir.
* **O Round Robin:** Utilize este método quando pretender que a carga de toodistribute através de um conjunto de nuvem dos serviços de no Olá mesmo datacenter ou em serviços em nuvem ou Web sites em datacenters diferentes.

Para obter mais informações, consulte [sobre tráfego Manager carga balanceamento métodos](../articles/traffic-manager/traffic-manager-routing-methods.md).

Olá diagrama a seguir mostra um exemplo de Olá método de balanceamento de carga Round Robin para distribuir o tráfego entre os serviços de nuvem diferente.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

processo de básico Olá é seguinte Olá:

1. Um cliente de Internet consulta um serviço de web de tooa correspondente do domínio nome.
2. DNS reencaminha Olá nome consulta pedido tooTraffic Manager.
3. Gestor de tráfego escolhe o serviço em nuvem seguinte Olá no Olá lista o Round Robin e envia novamente Olá nome DNS. servidor DNS do cliente de Internet Olá resolve o endereço IP do Olá nome tooan e envia-a clientes de Internet toohello.
4. cliente de Internet Olá liga ao serviço de nuvem Olá escolhido pelo Gestor de tráfego.

Para obter mais informações, consulte [Gestor de tráfego](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Azure balanceamento de carga para as máquinas virtuais
Olá, máquinas virtuais no mesmo serviço em nuvem ou de rede virtual pode comunicar entre si diretamente com os respetivos endereços IP privados. Computadores e serviços fora Olá serviço em nuvem ou de rede virtual só pode comunicar com máquinas virtuais de um serviço em nuvem ou a rede virtual com um ponto final configurado. Um ponto final é um mapeamento de um endereço IP público e o endereço IP privado toothat porta e a porta de uma máquina virtual ou a função da web dentro de um serviço em nuvem do Azure.

Olá, Azure Load Balancer distribui aleatoriamente um tipo específico de tráfego de entrada entre várias máquinas virtuais ou serviços numa configuração conhecido como um conjunto com balanceamento de carga. Por exemplo, pode propagar-se de carga do tráfego de pedido web Olá em vários servidores web ou funções da web.

Olá diagrama seguinte mostra um ponto final com balanceamento de carga para o tráfego web (sem encriptação) padrão que é partilhado entre três máquinas virtuais para Olá pública e privada a porta TCP 80. Estas três máquinas virtuais estão num conjunto com balanceamento de carga.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Para obter mais informações, consulte [Balanceador de carga do Azure](../articles/load-balancer/load-balancer-overview.md). Para obter Olá passos toocreate um conjunto com balanceamento de carga, consulte [configurar um conjunto com balanceamento de carga](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure pode também o balanceamento de carga dentro de um serviço em nuvem ou de rede virtual. Isto é conhecido como balanceamento de carga interna e pode ser utilizado em Olá seguintes formas:

* Saldo tooload entre servidores em diferentes escalões de uma aplicação multicamada (por exemplo, entre escalões web e a base de dados).
* tooload saldo linha de negócio (LOB) aplicações alojadas no Azure, sem necessidade de software ou hardware de Balanceador de carga adicional.
* tooinclude servidores no local no conjunto de Olá de computadores cujo tráfego está com balanceamento de carga.

Semelhante tooAzure balanceamento de carga, balanceamento de carga interna é facilitada ao configurar um conjunto com balanceamento de carga interno.

Olá diagrama a seguir mostra um exemplo de um endpoint com balanceamento de carga interno para uma aplicação de linha de negócio (LOB) que é partilhada entre três máquinas virtuais numa rede virtual em vários locais.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Considerações de Balanceador de carga
Um balanceador de carga está configurado por predefinição tootimeout uma sessão inativa em 4 minutos. Se a aplicação por trás de um balanceador de carga deixa uma ligação inativa durante mais de 4 minutos e não tem uma configuração de ligação Keep-Alive, ligação Olá será ignorada. Pode alterar tooallow de comportamento de Balanceador de carga Olá um [definição de tempo limite de tempo para o Balanceador de carga do Azure](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Outra consideração é o tipo de Olá de modo de distribuição suportado pelo balanceador de carga do Azure. Pode configurar a afinidade do IP de origem (IP de origem, IP de destino) ou protocolo IP de origem (IP de origem, IP de destino e protocolo). Veja [modo de distribuição do Balanceador de carga do Azure (afinidade do IP de origem)](../articles/load-balancer/load-balancer-distribution-mode.md) para obter mais informações.

## <a name="next-steps"></a>Passos seguintes
Para obter Olá passos toocreate um conjunto com balanceamento de carga, consulte [configurar um conjunto com balanceamento de carga interno](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Para mais informações sobre o Balanceador de carga, consulte [balanceamento de carga interna](../articles/load-balancer/load-balancer-internal-overview.md).

