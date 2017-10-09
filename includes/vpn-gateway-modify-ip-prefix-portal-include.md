### <a name="noconnection"></a>prefixos de endereços IP de gateway de rede local toomodify - nenhuma ligação de gateway

#### <a name="tooadd-additional-address-prefixes"></a>tooadd prefixos de endereços adicionais:

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **configuração**.
2. Adicionar espaço de endereços IP Olá Olá *adicionar intervalo de endereços adicionais* caixa.
3. Clique em **guardar** toosave as suas definições.

#### <a name="tooremove-address-prefixes"></a>prefixos de endereço tooremove:

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **configuração**.
2. Clique em Olá **'...'** na linha de Olá que contém o prefixo de Olá pretende tooremove.
3. Clique em **remover**.
4. Clique em **guardar** toosave as suas definições.

### <a name="withconnection"></a>toomodify rede local gateway prefixos de endereços IP - existente a ligação de gateway

Se tiver uma ligação de gateway e pretender tooadd ou remover prefixos de endereço IP do Olá contidos no gateway de rede local, terá de Olá toodo os seguintes passos, por ordem. Este procedimento resulta num período de indisponibilidade da ligação VPN. Ao modificar os prefixos de endereços IP, não precisa de gateway de VPN de Olá toodelete. Só precisa de ligação de Olá tooremove.

#### <a name="1-remove-hello-connection"></a>1. Remova ligação Olá.

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **ligações**.
2. Clique em Olá **...**  numa linha de Olá para cada ligação, em seguida, clique em **eliminar**.
3. Clique em **guardar** toosave as suas definições.

#### <a name="2-modify-hello-address-prefixes"></a>2. Modificar os prefixos de endereço Olá.

tooadd prefixos de endereços adicionais:

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **configuração**.
2. Adicione espaço de endereços IP Olá.
3. Clique em **guardar** toosave as suas definições.

prefixos de endereço tooremove:

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **configuração**.
2. Clique em Olá **...**  na linha de Olá que contém o prefixo de Olá pretende tooremove.
3. Clique em **remover**.
4. Clique em **guardar** toosave as suas definições.

#### <a name="3-recreate-hello-connection"></a>3. Recrie a ligação de Olá.

1. Navegue toohello Gateway de rede Virtual para a sua VNet. (Não a Olá Gateway de rede Local.)
2. No Olá Gateway de rede Virtual, no Olá **definições** secção, clique em **ligações**.
3. Clique em Olá **+ adicionar** tooopen Olá **adicionar ligação** painel.
4. Recrie a ligação.
5. Clique em **OK** ligação de Olá toocreate.
