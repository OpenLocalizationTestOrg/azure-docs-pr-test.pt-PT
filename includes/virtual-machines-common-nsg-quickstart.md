Abrir uma porta ou criar um ponto final, tooa máquina virtual (VM) no Azure através da criação de um filtro de rede numa sub-rede ou interface de rede VM. Colocar estes filtros que controlam o tráfego de entrada e saído, num grupo de segurança de rede ligado toohello recurso que recebe o tráfego de Olá.

Vamos utilizar um exemplo comum de tráfego da web na porta 80. Assim que tiver uma VM que está configurado tooserve web pedidos Olá padrão TCP na porta 80 (Lembre-se de serviços adequado do toostart Olá e abrir quaisquer regras de firewall de SO em Olá VM bem),:

1. Crie um grupo de segurança de rede.
2. Crie uma regra de entrada permitir o tráfego com:
   * intervalo de portas de destino Olá "80"
   * Olá, intervalo de portas de origem de "*" (permitir que qualquer porta de origem)
   * um valor de prioridade de menos 65,500 (toobe superior numa prioridade de Olá predefinido catch-all regra de negação de entrada)
3. Associe Olá grupo de segurança de rede a interface de rede VM Olá ou sub-rede.

Pode criar toosecure de configurações de rede complexa ambiente utilizando grupos de segurança de rede e regras. O nosso exemplo utiliza apenas uma ou duas regras que permitam o tráfego HTTP ou de gestão remota. Para obter mais informações, consulte o artigo seguinte Olá ['Informação mais'](#more-information-on-network-security-groups) secção ou [que é um grupo de segurança de rede?](../articles/virtual-network/virtual-networks-nsg.md)

