### <a name="gwipnoconnection"></a>endereço IP de gateway de rede local de Olá toomodify - nenhuma ligação de gateway

Utilize o exemplo de Olá toomodify um gateway de rede local que não tem uma ligação de gateway. Quando modificar este valor, também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo.

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **configuração**.
2. No Olá **endereço IP** caixa, modifique o endereço IP Olá.
3. Clique em **guardar** definições de Olá toosave.

### <a name="gwipwithconnection"></a>toomodify Olá rede local gateway endereço IP do gateway - existente a ligação de gateway

toomodify um gateway de rede local que tenha uma ligação, terá de ligação de Olá toofirst remover. Depois de remover a ligação de Olá, pode modificar o endereço IP do gateway Olá e recriá-lo de uma nova ligação. Também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo. Este procedimento resulta num período de indisponibilidade da ligação VPN. Quando modificar o endereço IP do gateway Olá, não precisa de gateway de VPN de Olá toodelete. Só precisa de ligação de Olá tooremove.
 
#### <a name="1-remove-hello-connection"></a>1. Remova ligação Olá.

1. No Olá recurso de Gateway de rede Local, no Olá **definições** secção, clique em **ligações**.
2. Clique em Olá **...**  numa linha de Olá para ligação Olá, em seguida, clique em **eliminar**.
3. Clique em **guardar** toosave as suas definições.

#### <a name="2-modify-hello-ip-address"></a>2. Modificar o endereço IP Olá.

Também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo.

1. No Olá **endereço IP** caixa, modifique o endereço IP Olá.
2. Clique em **guardar** definições de Olá toosave.

#### <a name="3-recreate-hello-connection"></a>3. Recrie a ligação de Olá.

1. Navegue toohello Gateway de rede Virtual para a sua VNet. (Não a Olá Gateway de rede Local.)
2. No Olá Gateway de rede Virtual, no Olá **definições** secção, clique em **ligações**.
3. Clique em Olá **+ adicionar** tooopen Olá **adicionar ligação** painel.
4. Recrie a ligação.
5. Clique em **OK** ligação de Olá toocreate.
