## <a name="load-balancer-differences"></a>Diferenças do Balanceador de Carga

Existem tráfego de rede diferentes opções toodistribute utilizar o Microsoft Azure. Estas opções funcionam de forma diferente entre si, tendo um conjunto de funcionalidades diferente e suportando diferentes cenários. Podem todos ser utilizados em isolamento ou em conjunto.

* **Balanceador de carga do Azure** funciona na camada de transporte de Olá (camada 4 na pilha de referência do Olá OSI rede). Fornece ao nível da rede de distribuição de tráfego em instâncias de uma aplicação em execução no Olá mesmo centro de dados do Azure.
* **Gateway de aplicação** funciona na camada de aplicação Olá (camada 7 na pilha de referência do Olá OSI rede). Atua como um serviço de proxy inverso, terminar a ligação de cliente Olá e pedidos de reencaminhamento pontos finais de tooback-end.
* **Gestor de tráfego** funciona em Olá nível DNS.  Utiliza DNS respostas toodirect pelo utilizador final tráfego tooglobally distribuída pontos finais. Os clientes ligam, em seguida, pontos finais de toothose diretamente.

Olá a tabela seguinte resume as funcionalidades de Olá oferecidas pelo cada serviço:

| Serviço | Azure Load Balancer | Gateway de Aplicação | Gestor de Tráfego |
| --- | --- | --- | --- |
| Tecnologia |Nível de transporte (Camada 4) |Nível de aplicação (Camada 7) |Nível de DNS |
| Protocolos de aplicação suportados |Qualquer |HTTP, HTTPS e WebSockets |Qualquer (É preciso um ponto final HTTP para a monitorização de ponto final) |
| Pontos Finais |Instâncias da função de VMs do Azure e Serviços Cloud |Qualquer endereço de IP interno do Azure, endereço IP de Internet pública, VM do Azure ou Serviço Cloud do Azure |VMs do Azure, Serviços Cloud, Aplicações Web do Azure e os pontos finais externos |
| Suporte de Vnet |Serve para ambas as aplicações (Vnet) internas e com acesso à Internet |Serve para ambas as aplicações (Vnet) internas e com acesso à Internet |Suporta apenas aplicações de acesso à Internet |
| Monitorização de Pontos Finais |Suportado através de sondas |Suportado através de sondas |Suportado através de HTTP/HTTPS GET |

Azure Balanceador de carga e tooendpoints de tráfego de rede de rota de Gateway de aplicação, mas tem toohandle de tráfego de toowhich de cenários de utilização diferentes. Olá seguinte tabela ajuda a diferença de Olá compreender entre balanceadores de carga dois Olá:

| Tipo | Azure Load Balancer | Gateway de Aplicação |
| --- | --- | --- |
| Protocolos |UDP/TCP |HTTP, HTTPS e WebSockets |
| Reserva de IP |Suportado |Não suportado |
| Modo de balanceamento de carga |5 cadeias de identificação (IP de origem, porta de origem, IP de destino, porta de destino, tipo de protocolo) |Round Robin<br>Encaminhamento com base no URL |
| Modo de balanceamento de carga (IP de origem/sessões temporárias) |duas cadeias de identificação (IP de origem e destino IP),três cadeias de identificação (IP de origem, IP de destino e porta). Pode aumentar ou reduzir verticalmente com base no número de Olá de máquinas virtuais |Afinidade com base no cookie<br>Encaminhamento com base no URL |
| Sondas do estado de funcionamento |Predefinido: intervalo da sonda - 15 seg. Retiradas da rotação: duas falhas contínuas. Suporta sondas definidas pelo utilizador |Intervalo da sonda inativo 30 seg. Retirado depois de cinco falhas consecutivas de tráfego em direto ou uma falha de sonda única no modo inativo. Suporta sondas definidas pelo utilizador |
| Descarga de SSL |Não suportado |Suportado |
| Com base no URL de encaminhamento | Não suportado | Suportado|
| Política SSL | Não suportado | Suportado|
