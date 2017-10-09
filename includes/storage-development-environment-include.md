## <a name="set-up-your-development-environment"></a>Configurar o ambiente de desenvolvimento
Configure o ambiente de desenvolvimento no Visual Studio, em seguida, pelo que pode exemplos de código Olá tootry preparado neste guia.

### <a name="create-a-windows-console-application-project"></a>Criar um projeto de aplicação de consola do Windows
No Visual Studio, crie uma nova aplicação de consola do Windows. Olá, os passos seguintes mostra como toocreate uma aplicação de consola no Visual Studio 2017, no entanto, os passos de Olá são semelhantes noutras versões do Visual Studio.

1. Selecione **Ficheiro** > **Novo** > **Projeto**
2. Selecione **Instalado** > **Modelos** > **Visual C#** > **Ambiente de Trabalho Clássico do Windows**
3. Selecione **Aplicação da Consola (.NET Framework)**
4. Introduza um nome para a sua aplicação no Olá **Name:** campo
5. Selecione **OK**

![Caixa de diálogo de criação de projetos no Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Todos os exemplos de código deste tutorial podem ser adicionados toohello `Main()` método da sua aplicação de consola `Program.cs` ficheiro.

Pode utilizar Olá biblioteca de clientes do Storage do Azure em qualquer tipo de aplicações .NET, incluindo uma aplicação de web ou serviço de nuvem do Azure e aplicações de ambiente de trabalho e dispositivos móveis. Neste guia, utilizamos uma aplicação de consola pela simplicidade.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Utilizar pacotes do NuGet tooinstall Olá necessário
Existem dois pacotes necessita tooreference no seu projeto toocomplete neste tutorial:

* [Biblioteca do cliente de armazenamento do Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): Este pacote fornece acesso programático toodata recursos na sua conta de armazenamento.
* [Biblioteca do Gestor de Configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este pacote fornece uma classe para analisar uma cadeia de ligação num ficheiro de configuração, independentemente de onde a sua aplicação estiver a ser executada.

Pode utilizar o NuGet tooobtain ambos os pacotes. Siga estes passos.

1. Clique com o botão direito do rato no projeto no **Explorador de Soluções** e escolha **Gerir Pacotes NuGet**.
2. Procure online "Windowsazure" e clique em **instalar** tooinstall Olá biblioteca de clientes de armazenamento e as respetivas dependências.
3. Procure online por "WindowsAzure.ConfigurationManager" e clique em **instalar** tooinstall Olá Azure Configuration Manager.

> [!NOTE]
> pacote de biblioteca de clientes de armazenamento de Olá também está incluído no Olá [Azure SDK para .NET](https://azure.microsoft.com/downloads/). No entanto, recomendamos que instale também Olá biblioteca de clientes de armazenamento a partir de tooensure NuGet que tenham sempre a versão mais recente do Olá da biblioteca de clientes de Olá.
> 
> as dependências ODataLib de Olá no Olá biblioteca de clientes de armazenamento para .NET são resolvidas através da pacotes ODataLib de Olá disponíveis no NuGet, não a partir do WCF Data Services. bibliotecas de ODataLib Olá podem ser transferidas diretamente ou referenciadas pelo seu projeto de código através do NuGet. Olá pacotes ODataLib específicos utilizados pelo Olá biblioteca de clientes de armazenamento são [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), e [Spatial](http://nuget.org/packages/System.Spatial/). Embora estas bibliotecas sejam utilizadas pelas classes de armazenamento de Azure Table Olá, são dependências necessárias para a programação com Olá biblioteca de clientes de armazenamento.
> 
> 

### <a name="determine-your-target-environment"></a>Determinar o ambiente de destino
Tem duas opções de ambiente para executar os exemplos de Olá neste guia:

* Pode executar o código uma conta de armazenamento do Azure na nuvem de Olá. 
* Pode executar o código no emulador do storage do Azure de Olá. emulador do storage Olá é um ambiente local que emula uma conta de armazenamento do Azure na nuvem de Olá. emulador Olá é uma opção gratuita para testar e depurar o seu código enquanto a aplicação está em desenvolvimento. emulador de Olá utiliza uma conta bem conhecida e a chave. Para obter mais informações, consulte [Olá utilizar emulador do Storage do Azure para desenvolvimento e teste](../articles/storage/common/storage-use-emulator.md)

Se estiver a filtrar uma conta de armazenamento na nuvem de Olá, copie Olá chave de acesso primária para a sua conta de armazenamento Olá portal do Azure. Para obter mais informações, veja [Ver e copiar chaves de acesso do armazenamento](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> Pode visar tooavoid de emulador de armazenamento de Olá incorrer em custos associados ao Storage do Azure. No entanto, se optar por tootarget uma conta de armazenamento do Azure na nuvem de Olá, os custos para efetuar este tutorial serão negligenciável.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Configurar a cadeia de ligação de armazenamento
Olá biblioteca de clientes do Storage do Azure para .NET suporta a utilização de um armazenamento cadeia tooconfigure pontos finais da ligação e as credenciais para aceder aos serviços de armazenamento. Olá melhor forma toomaintain a cadeia de ligação de armazenamento é num ficheiro de configuração. 

Para mais informações sobre cadeias de ligação, consulte [configurar uma cadeia de ligação de tooAzure armazenamento](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> A chave de conta de armazenamento é semelhante toohello raiz palavra-passe para a sua conta de armazenamento. Tenha sempre tooprotect cuidado a chave de conta de armazenamento. Evite distribuição dos mesmos utilizadores tooother, pré-programá-lo ou guardá-lo num ficheiro de texto simples que seja acessível tooothers. Regenere a chave utilizando Olá portal do Azure se considerar que poderá ter sido comprometida.
> 
> 

tooconfigure a cadeia de ligação, abra Olá `app.config` ficheiro a partir do Explorador de soluções no Visual Studio. Adicionar conteúdo Olá Olá `<appSettings>` elemento mostrado abaixo. Substitua `account-name` com o nome de Olá da sua conta do storage e `account-key` com a chave de acesso da conta:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Por exemplo, a definição de configuração é semelhante a:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

emulador de armazenamento do tootarget Olá, pode utilizar um atalho que mapeia o nome de conta conhecidos toohello e a chave. Nesse caso, a definição da cadeia de ligação é:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

