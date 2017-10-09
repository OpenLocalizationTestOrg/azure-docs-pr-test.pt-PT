## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Como toocreate uma VNet clássica a utilizar a CLI do Azure
Pode utilizar Olá CLI do Azure toomanage os recursos do Azure a partir da linha de comandos Olá partir de qualquer computador com Windows, Linux ou OSX. toocreate uma VNet utilizando Olá CLI do Azure, siga os passos de Olá abaixo.

1. Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../articles/cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.
2. Executar Olá **criar rede azure vnet** comando toocreate uma VNet e uma sub-rede, como mostrado abaixo. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Resultado esperado:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **-- vnet**. Nome do Olá VNet toobe criado. Para o nosso cenário *TestVNet*.
   * **-e (ou - espaço de endereços)**. Espaço de endereços da VNet. Para o nosso cenário *192.168.0.0*
   * **-i (ou - cidr)**. Máscara de rede no formato CIDR. Para o nosso cenário *16*.
   * **-n (ou - nome de sub-rede**). Nome da sub-rede primeiro Olá. Para o nosso cenário *FrontEnd*.
   * **-p (ou - ip de início de sub-rede)**. Endereço IP inicial para a sub-rede ou espaço de endereços de sub-rede. Para o nosso cenário *192.168.1.0*.
   * **-r (ou - sub-rede cidr)**. Máscara de rede no formato CIDR para a sub-rede. Para o nosso cenário *24*.
   * **-l (ou --location)**. Região do Azure onde será criada Olá VNet. Para o nosso cenário *EUA Central*.
3. Executar Olá **sub-rede da vnet de rede do azure crie** comando toocreate uma sub-rede, como mostrado abaixo. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    O resultado para o comando de Olá acima Olá esperado é:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (ou -- vnet-name**. Nome da VNet onde será criada a sub-rede de Olá de Olá. Para o nosso cenário *TestVNet*.
   * **-n (ou --name)**. Nome da nova sub-rede Olá. Para o nosso cenário *back-end*.
   * **-a (or --address-prefix)**. Bloco CIDR da sub-rede. Quatro nosso cenário, *192.168.2.0/24*.
4. Executar Olá **mostrar de vnet de rede do azure** comando Propriedades de Olá tooview de Olá nova vnet, como mostrado abaixo.
   
            azure network vnet show
   
    O resultado para o comando de Olá acima Olá esperado é:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

