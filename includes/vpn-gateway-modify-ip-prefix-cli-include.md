### <a name="noconnection"></a>prefixos de endereços IP de gateway de rede local toomodify - nenhuma ligação de gateway

Se não tiver uma ligação de gateway e pretende tooadd ou remover prefixos de endereço IP, utilize Olá mesmo comando que utilize o gateway de rede local do toocreate Olá, [az local-gateway de rede criar](https://docs.microsoft.com/cli/azure/network/local-gateway#create). Também pode utilizar este endereço IP do comando tooupdate Olá gateway para o dispositivo VPN Olá. toooverwrite Olá as definições atuais, utilize o nome existente do Olá do seu gateway de rede local. Se utilizar um nome diferente, criar um novo gateway de rede local, em vez de substituir Olá já existente.

Sempre que efetuar uma alteração, a lista completa de Olá dos prefixos tem de ser especificado, não apenas Olá prefixos que pretende que o toochange. Especificar apenas Olá prefixos que pretende que o tookeep. Neste caso, 10.0.0.0/24 e 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify rede local gateway prefixos de endereços IP - existente a ligação de gateway

Se tiver uma ligação de gateway e pretender tooadd ou remover prefixos de endereço IP, pode atualizar os prefixos de Olá utilizando [atualização de gateway do local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Este procedimento resulta num período de indisponibilidade da ligação VPN. Quando modificar o endereço IP Olá prefixos, não precisa de gateway de VPN de Olá toodelete.

Sempre que efetuar uma alteração, a lista completa de Olá dos prefixos tem de ser especificado, não apenas Olá prefixos que pretende que o toochange. Neste exemplo, 10.0.0.0/24 e 20.0.0.0/24 já estão presentes. Vamos adicionar Olá prefixos 30.0.0.0/24 e 40.0.0.0/24 e especifique todos os 4 de prefixos Olá ao atualizar.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```