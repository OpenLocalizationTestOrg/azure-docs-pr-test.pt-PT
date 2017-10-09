---
title: aaaUsing tooDev tooPublish de Scripts do Windows PowerShell e ambientes de teste | Microsoft Docs
description: Saiba como toouse do Windows PowerShell scripts de ambientes de toodevelopment e teste de toopublish do Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Com o Windows PowerShell scripts toopublish toodev e teste ambientes
Quando cria uma aplicação web no Visual Studio, pode gerar um script do Windows PowerShell que pode utilizar a publicação de Olá de tooautomate posterior do seu Web site tooAzure como uma aplicação Web no App Service do Azure ou uma máquina virtual. Pode editar e expandir os seus requisitos de script do Windows PowerShell Olá no toosuit de editor do Visual Studio Olá ou integrar o script de Olá compilação existente, teste e publicação de scripts.

Utilizar estes scripts, pode aprovisionar versões personalizadas (também conhecido como ambientes de desenvolvimento e teste) do seu site para utilização temporária. Por exemplo, poderá configurar uma versão específica do seu site numa máquina virtual do Azure ou num Olá ranhura toorun um Web site de teste um conjunto de teste, reproduzir de erros, teste uma correção de erros, versão de avaliação de uma alteração proposta ou configurar um ambiente personalizado para um demonstração ou apresentação. Depois de criar um script que publica o seu projeto, pode recriar ambientes idênticos, executando novamente o script Olá conforme necessário ou executar script de Olá com a seus próprios compilação do seu toocreate de aplicação web num ambiente personalizado para fins de teste.

## <a name="what-you-need"></a>Do que precisa
* Azure SDK 2.3 ou posterior. Consulte [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) para obter mais informações.

Não é necessário scripts de Olá toogenerate do Olá Azure SDK para projetos web. Esta funcionalidade destina-se a projetos web, não funções da web nos serviços em nuvem.

* O Azure PowerShell 0.7.4 ou posterior. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou posterior.

## <a name="additional-tools"></a>Ferramentas adicionais
Ferramentas adicionais e recursos para trabalhar com o PowerShell no Visual Studio para desenvolvimento do Azure estão disponíveis. Consulte [PowerShell Tools para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Gerar Olá publicar scripts
Pode gerar Olá publicar scripts para uma máquina virtual que aloja o seu Web site quando criar um novo projeto seguindo [estas instruções](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Também pode [gerar publicar scripts para as web apps no App Service do Azure](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Scripts que gera o Visual Studio
Visual Studio gera uma pasta de nível de solução denominada **PublishScripts** que contém dois ficheiros do Windows PowerShell, um script de publicar para a máquina virtual ou Web site e um módulo que contém as funções que pode utilizar Olá scripts. Visual Studio também gera um ficheiro no formato JSON Olá que especifica os detalhes de Olá do projeto de Olá que estiver a implementar.

### <a name="windows-powershell-publish-script"></a>Script de publicar do Windows PowerShell
Olá publicar o script contém específico publicar os passos para implementar tooa site ou a máquina virtual. O Visual Studio fornece sintaxe coloração para desenvolvimento do Windows PowerShell. Ajuda para as funções de Olá está disponível e livremente pode editar funções de Olá no Olá script toosuit os requisitos de alteração.

### <a name="windows-powershell-module"></a>Módulo do Windows PowerShell
Olá do Windows PowerShell módulo gera do Visual Studio contém funções que Olá publicar utiliza de script. Estas são as funções do Azure PowerShell e não são toobe pretendido modificado. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.

### <a name="json-configuration-file"></a>Ficheiro de configuração JSON
ficheiro JSON Olá é criado na Olá **configurações** pasta e contém dados de configuração que especifica exatamente qual tooAzure toodeploy de recursos. Olá o nome do ficheiro de Olá que gera o Visual Studio é projeto-nome-WAWS-dev.json se tiver criado um Web site ou o nome de projeto-VM-dev.json se tiver criado uma máquina virtual. Eis um exemplo de um ficheiro de configuração JSON que é gerado quando criar um Web site. A maioria dos valores de Olá são facilmente compreensíveis. nome do Web site Olá é gerado pelo Azure, pelo que não poderá corresponder ao nome do seu projeto.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Quando cria uma máquina virtual, o ficheiro de configuração JSON Olá procura semelhante toohello seguinte. Tenha em atenção que um serviço em nuvem foi criado como um contentor para a máquina virtual de Olá. máquina virtual de Olá contém Olá habitual os pontos finais para o acesso web através de HTTP e HTTPS, bem como pontos finais para o Web Deploy, que lhe permite publicar Web site de toohello do seu computador local, o ambiente de trabalho remoto e o Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Pode editar Olá JSON configuração toochange o que acontece quando executar Olá publicar scripts. Olá `cloudService` e `virtualMachine` secções são necessárias, mas pode eliminar Olá `databases` secção se não o tiver. Propriedades de Olá que estão vazios no ficheiro de configuração predefinida do Olá que gera o Visual Studio são opcionais; que têm valores no ficheiro de configuração predefinido Olá são necessários.

Se tiver um site que tenha vários ambientes de implementação (conhecidos como ranhuras) em vez de um site de produção único no Azure, pode incluir nome de ranhura Olá no nome de Olá do Web site de Olá no ficheiro de configuração do Olá JSON. Por exemplo, se tiver um site com o nome **mysite** e uma ranhura para o mesmo nome **testar** , em seguida, Olá URI é mysite test.cloudapp.net, mas Olá toouse de nome correto no ficheiro de configuração de Olá mysite(test) . Só pode fazer isto, se o Web site de Olá e ranhuras já existem na sua subscrição. Se não existirem, criar site Olá executando o script de Olá sem especificar ranhura Olá, em seguida, criar ranhura Olá no Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), e após executar o script de Olá com o nome de Web site modificado Olá. Para obter mais informações sobre as ranhuras de implementação para aplicações web, consulte [configurar ambientes para web apps no App Service do Azure de teste](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Como toorun Olá publicar scripts
Se nunca tiver executado um script do Windows PowerShell antes, primeiro tem de definir Olá execução política tooenable scripts toorun. Esta é a segurança funcionalidade tooprevent os utilizadores executem scripts do Windows PowerShell se não estiverem toomalware vulnerável ou vírus que envolvam a execução de scripts.

### <a name="run-hello-script"></a>Executar script de Olá
1. Crie pacote Olá Web Deploy para o seu projeto. Um pacote do Web Deploy é um arquivo comprimido (ficheiro. zip) que contêm ficheiros que pretende que o Web site de tooyour toocopy ou máquina virtual. Pode criar pacotes Web Deploy no Visual Studio para qualquer aplicação web.

![Criar Web implementar o pacote](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Para obter mais informações, consulte [como: criar um pacote de implementação Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Também pode automatizar criação Olá do pacote do Web Deploy, conforme descrito na secção de Olá **Customizing e expandir Olá publicar scripts** mais adiante neste tópico.

1. No **Explorador de soluções**, abra o menu de contexto de Olá para script Olá e, em seguida, escolha **abra o ISE do PowerShell**.
2. Se este for Olá pela primeira vez que executar scripts do Windows PowerShell no computador, abra uma janela de linha de comandos com privilégios de administrador e Olá tipo os seguintes comandos:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Inicie sessão tooAzure com Olá os seguintes comandos.

    ```powershell
    Add-AzureAccount
    ```

    Quando lhe for pedido, forneça o nome de utilizador e palavra-passe.

    Tenha em atenção que, ao automatizar o script de Olá, este método de fornecer credenciais do Azure não irão funcionar. Em vez disso, deve utilizar as credenciais do Olá. publishsettings ficheiro tooprovide. Uma vez, pode utiliza apenas comandos Olá **Get-AzurePublishSettingsFile** Olá toodownload de ficheiros a partir do Azure e utilizar após **importação AzurePublishSettingsFile** ficheiros de Olá tooimport. Para obter instruções detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

4. (Opcional) Se quiser toocreate Azure recursos, tais como máquina virtual de Olá, a base de dados e o Web site sem a publicação da sua aplicação web, utilizam Olá **publicar WebApplication.ps1** comando com Olá **-configuração** argumento definido toohello ficheiro de configuração de JSON. Esta linha de comandos utiliza toodetermine de ficheiro de configuração do Olá JSON que toocreate de recursos. Porque utiliza as predefinições de Olá para outros argumentos da linha de comandos, cria Olá recursos, mas não publicar a sua aplicação web. Olá – opção verbosa dá-lhe obter mais informações sobre o que acontece.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Olá utilize **publicar WebApplication.ps1** conforme mostrado dos Olá seguinte script de Olá tooinvoke de exemplos de comandos e publicar a aplicação web. Se precisar de predefinições de Olá toooverride para qualquer uma das Olá outros argumentos, tais como o nome da subscrição Olá, publicar o nome do pacote, credenciais de máquina virtual ou as credenciais do servidor de base de dados, pode especificar os parâmetros. Olá utilize **– verboso** opção toosee mais informações sobre o progresso de Olá de Olá processo de publicação.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Se estiver a criar uma máquina virtual, o comando de Olá aspeto Olá seguinte. Este exemplo mostra também como toospecify Olá credenciais para várias bases de dados. Para máquinas de virtuais Olá que criar estes scripts, certificado SSL Olá não é de uma autoridade de raiz fidedigna. Por conseguinte, terá de toouse Olá **– AllowUntrusted** opção.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    script de Olá pode criar bases de dados, mas não criar servidores de base de dados. Se quiser toocreate um servidor de base de dados, pode utilizar Olá **New-AzureSqlDatabaseServer** funcionar em Olá módulo do Azure.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Personalizar e expandir Olá publicar scripts
Pode personalizar Olá publicar script e o ficheiro de configuração JSON. Olá funções no módulo do Windows PowerShell Olá **AzureWebAppPublishModule.psm1** não são toobe pretendido modificado. Se apenas pretender toospecify uma base de dados diferente ou alterar algumas das propriedades de Olá da máquina virtual de Olá, edite o ficheiro de configuração do Olá JSON. Se pretender que a funcionalidade de Olá tooextend de Olá script tooautomate criar e testar o projeto, pode implementar os stubs de função no **publicar WebApplication.ps1**.

tooautomate compilar o projeto, adicione o código que chama MSBuild demasiado`New-WebDeployPackage` conforme mostrado neste exemplo de código. Olá caminho toohello MSBuild comando é diferente consoante a versão de Olá do Visual Studio que instalou. caminho correto do Olá tooget, pode utilizar a função de Olá **Get-MSBuildCmd**, conforme mostrado neste exemplo.

### <a name="tooautomate-building-your-project"></a>tooautomate compilar o projeto
1. Adicionar Olá `$ProjectFile` parâmetro na secção de global param Olá.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copiar a função de Olá `Get-MSBuildCmd` no seu ficheiro de script.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Substitua `New-WebDeployPackage` com Olá seguinte código e substitua Olá marcadores de posição no Olá linha construir `$msbuildCmd`. Este código é para o Visual Studio 2015. Se estiver a utilizar o Visual Studio 2013, altere Olá **VisualStudioVersion** propriedade abaixo demasiado`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild a aplicação web, utilize MsBuild.exe. Para obter ajuda, consulte a referência da linha de comandos MSBuild: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Iniciar a execução do comando de compilação de Olá

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Chamar Olá `New-WebDeployPackage` função antes desta linha: `$Config = Read-ConfigFile $Configuration` para aplicações web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para máquinas virtuais.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Invocar script Olá personalizada de linha de comandos utilizando a transmissão Olá `$Project` argumento, tal como em Olá linha de comandos de exemplo a seguir.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate testar da sua aplicação, adicione o código demasiado`Test-WebApplication`. Ser toouncomment se linhas Olá **publicar WebApplication.ps1** onde estas funções são denominadas. Se não fornecer uma implementação, pode criar manualmente o projeto com o Visual Studio e, em seguida, execute Olá publicar script toopublish tooAzure.

## <a name="publishing-function-summary"></a>Função publicação resumo
Ajuda tooget para funções que pode utilizar Olá linha de comandos do Windows PowerShell, utilize o comando de Olá `Get-Help function-name`. Ajuda Olá inclui ajuda de parâmetro e exemplos. Olá texto de ajuda do mesmo é também nos ficheiros de origem do script de Olá, **AzureWebAppPublishModule.psm1** e **publicar WebApplication.ps1**. script de Olá e ajuda está localizada no seu idioma de Visual Studio.

**AzureWebAppPublishModule**

| Nome de função | Descrição |
| --- | --- |
| Adicionar-AzureSQLDatabase |Cria uma nova base de dados SQL do Azure. |
| AzureSQLDatabases adicionar |Cria bases de dados SQL do Azure a partir de valores de Olá num ficheiro de configuração de JSON Olá que gera o Visual Studio. |
| Adicionar-AzureVM |Cria uma máquina virtual do Azure e devolve o que URL de Olá de Olá implementado VM. Olá função configura os pré-requisitos de Olá e, em seguida, Olá chamadas **New-AzureVM** funcionar (módulo do Azure) toocreate uma nova máquina virtual. |
| AzureVMEndpoints adicionar |Adiciona a nova máquina de virtual de tooa pontos finais de entrada e devolve Olá máquina de virtual com o novo ponto de final Olá. |
| AzureVMStorage adicionar |Cria uma nova conta de armazenamento do Azure na subscrição atual Olá. nome de Olá da conta de Olá começa com "devtest" seguido de uma cadeia alfanumérica exclusiva. a função Olá devolve o nome de Olá Olá novo da conta de armazenamento. Tem de especificar uma localização ou um grupo de afinidades Olá nova conta de armazenamento. |
| AzureWebsite adicionar |Cria um Web site com o nome especificado Olá e localização. Esta função chama Olá **New-AzureWebsite** funcionar em Olá módulo do Azure. Se a subscrição de Olá já não incluir um Web site com o nome especificado Olá, esta função cria o Web site de Olá e devolve um objeto de Web site. Caso contrário, devolve `$null`. |
| Subscrição de cópia de segurança |Guarda Olá atual subscrição do Azure no Olá `$Script:originalSubscription` variável no âmbito de script. Esta função guarda a subscrição do Azure atual de Olá (tal como obtidas pelo `Get-AzureSubscription -Current`) e a conta do storage e subscrição Olá que é alterada por este script (armazenado na variável Olá `$UserSpecifiedSubscription`) e a respetiva conta de armazenamento, no âmbito de script. Ao guardar os valores de Olá, pode utilizar uma função, como `Restore-Subscription`, toorestore Olá original atual subscrição e o armazenamento toocurrent estado da conta se tiver alterado o estado atual do Olá. |
| Localizar-AzureVM |Obtém Olá especificado máquina virtual do Azure. |
| Formato DevTestMessageWithTime |Prepends mensagem de saudação data e hora tooa. Esta função foi concebida para mensagens escritas toohello erro e Verbose fluxos. |
| Get-AzureSQLDatabaseConnectionString |Monta uma ligação cadeia tooconnect tooan SQL database do Azure. |
| Get-AzureVMStorage |Devolve Olá nome Olá primeiro da conta de armazenamento com o padrão de nome de Olá "devtest*" (sensível) no grupo de afinidade ou a localização especificado no Olá. Se Olá "devtest*" conta de armazenamento não corresponde à localização de Olá ou o grupo de afinidade, função Olá ignora-lo. Tem de especificar uma localização ou um grupo de afinidade. |
| Get-MSDeployCmd |Devolve uma ferramenta do comando toorun Olá MsDeploy.exe. |
| Novo AzureVMEnvironment |Localiza ou cria uma máquina virtual na subscrição Olá que corresponda a valores de Olá no ficheiro de configuração do Olá JSON. |
| WebPackage publicar |Uma web e utiliza MsDeploy.exe publicou o pacote. Zip ficheiro toodeploy recursos tooa site. Esta função não gera qualquer saída. Se Olá chamada tooMSDeploy.exe falhar, a função de Olá emite uma exceção. tooget mais detalhadas de saída, utilize Olá **-Verbose** opção. |
| WebPackageToVM publicar |Verifica os valores de parâmetros de Olá e, em seguida, chama Olá **publicar WebPackage** função. |
| Leitura ConfigFile |Valida o ficheiro de configuração JSON Olá e devolve uma tabela hash de valores selecionados. |
| Subscrição de restauro |Repõe Olá subscrição toohello original subscrição atual. |
| Teste AzureModule |Devolve `$true` se Olá instalada a versão de módulo do Azure é 0.7.4 ou posterior. Devolve `$false` se o módulo Olá não está instalado ou uma versão anterior. Esta função não tem parâmetros. |
| Teste AzureModuleVersion |Devolve `$true` se versão Olá Olá módulo Azure for 0.7.4 ou posterior. Devolve `$false` se o módulo Olá não está instalado ou uma versão anterior. Esta função não tem parâmetros. |
| Teste HttpsUrl |Converte o objeto de URI de tooa Olá entrada URL. Devolve `$True` se Olá URL absoluto e a esquema é https. Devolve `$false` se Olá URL é relativo, a esquema não é HTTPS ou cadeia de entrada Olá não pode ser convertida tooa URL. |
| Membro de teste |Devolve `$true` se uma propriedade ou método é um membro do objeto de Olá. Caso contrário, devolve `$false`. |
| Escrita ErrorWithTime |Escreve uma mensagem de erro o prefixo Olá hora atual. Esta função chama Olá **formato DevTestMessageWithTime** tempo de Olá tooprepend função antes de escrever o fluxo de erro do Olá mensagens toohello. |
| Escrita HostWithTime |Escreve um programa de anfitrião de toohello de mensagem (**escrita anfitrião**) o prefixo Olá hora atual. efeito Olá de escrever o programa de anfitrião toohello varia. A maioria dos programas nesse anfitrião do Windows PowerShell escrever estas mensagens toostandard saída. |
| Escrita VerboseWithTime |Escreve uma mensagem verbosa prefixo Olá hora atual. Uma vez que chama **Write-Verbose**, mensagem de saudação apresenta apenas quando Olá script é executado com Olá **verboso** parâmetro ou quando Olá **VerbosePreference** preferência é Definir demasiado**continuar**. |

**Publicar-WebApplication**

| Nome de função | Descrição |
| --- | --- |
| Novo AzureWebApplicationEnvironment |Cria recursos do Azure, tais como um Web site ou a máquina virtual. |
| Novo WebDeployPackage |Esta função não está implementada. Pode adicionar comandos no toobuild função seu projeto. |
| AzureWebApplication publicar |Publica um tooAzure de aplicação web. |
| Publicar-WebApplication |Cria e implementa as aplicações Web, as máquinas virtuais, bases de dados SQL e contas de armazenamento para um projeto web do Visual Studio. |
| Teste-WebApplication |Esta função não está implementada. Pode adicionar comandos no tootest função da aplicação. |

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre os scripts do PowerShell através da leitura [Scripting com o Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e ver outros scripts do PowerShell do Azure em Olá [Centro de scripts](https://azure.microsoft.com/documentation/scripts/).
