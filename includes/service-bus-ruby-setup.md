## <a name="create-a-ruby-application"></a><span data-ttu-id="836f0-101">Criar uma aplicação Ruby</span><span class="sxs-lookup"><span data-stu-id="836f0-101">Create a Ruby application</span></span>
<span data-ttu-id="836f0-102">Para obter instruções, consulte [criar uma aplicação Ruby no Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="836f0-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="836f0-103">Configurar o seu tooUse aplicação de Service Bus</span><span class="sxs-lookup"><span data-stu-id="836f0-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="836f0-104">toouse Service Bus, transfira e utilize o pacote de Azure Ruby Olá, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="836f0-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="836f0-105">Utilize o pacote de Olá RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="836f0-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="836f0-106">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="836f0-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="836f0-107">Escreva "gem instalar azure" gem do Olá comando janela tooinstall Olá e as dependências.</span><span class="sxs-lookup"><span data-stu-id="836f0-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="836f0-108">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="836f0-108">Import hello package</span></span>
<span data-ttu-id="836f0-109">Utilizando o editor de texto favorito, adicionar Olá toohello superior de Olá Ruby os seguintes ficheiros no qual pretende toouse armazenamento:</span><span class="sxs-lookup"><span data-stu-id="836f0-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="836f0-110">Configurar uma ligação de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="836f0-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="836f0-111">Seguinte de Olá de utilização código valores de Olá tooset de espaço de nomes, nome de Olá chave, chave, signatário e anfitrião:</span><span class="sxs-lookup"><span data-stu-id="836f0-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="836f0-112">Definir o valor toohello Olá espaço de nomes valor que criou em vez do URL completo Olá.</span><span class="sxs-lookup"><span data-stu-id="836f0-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="836f0-113">Por exemplo, utilizar **"yourexamplenamespace"**, não "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="836f0-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
