## <a name="create-a-ruby-application"></a>Criar uma aplicação Ruby
Para obter instruções, consulte [criar uma aplicação Ruby no Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Configurar o seu tooUse aplicação de Service Bus
toouse Service Bus, transfira e utilize o pacote de Azure Ruby Olá, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilize o pacote de Olá RubyGems tooobtain
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).
2. Escreva "gem instalar azure" gem do Olá comando janela tooinstall Olá e as dependências.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Utilizando o editor de texto favorito, adicionar Olá toohello superior de Olá Ruby os seguintes ficheiros no qual pretende toouse armazenamento:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Configurar uma ligação de barramento de serviço
Seguinte de Olá de utilização código valores de Olá tooset de espaço de nomes, nome de Olá chave, chave, signatário e anfitrião:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Definir o valor toohello Olá espaço de nomes valor que criou em vez do URL completo Olá. Por exemplo, utilizar **"yourexamplenamespace"**, não "yourexamplenamespace.servicebus.windows.net".
