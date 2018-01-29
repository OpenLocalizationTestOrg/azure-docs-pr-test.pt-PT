---
title: "Pacote de um serviço do Azure aplicação Fabric | Microsoft Docs"
description: "Como uma aplicação de Service Fabric antes de implementar um cluster do pacote."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 93c86f4805257aee8e04ef80e33b3cec0fd3c67d
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/11/2018
---
# <a name="package-an-application"></a>Pacote de uma aplicação
Este artigo descreve como uma aplicação de Service Fabric do pacote e torná-lo preparado para a implementação.

## <a name="package-layout"></a>Esquema do pacote
O manifesto da aplicação, um ou mais manifestos de serviço e outros ficheiros de pacote necessários tem sejam organizados de um esquema específico para a implementação para um cluster do Service Fabric. Os manifestos de exemplo neste artigo, seriam necessário sejam organizados da estrutura do diretório seguinte:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

As pastas são denominadas para fazer corresponder o **nome** atributos de cada elemento correspondente. Por exemplo, se o manifesto do serviço contidos dois pacotes de código com os nomes de **MyCodeA** e **MyCodeB**, em seguida, duas pastas com os mesmos nomes iriam conter os binários necessários para cada pacote do código.

## <a name="use-setupentrypoint"></a>Utilizar SetupEntryPoint
Cenários típicos de utilização **SetupEntryPoint** quando tiver de executar um executável antes do início do serviço ou necessitar de efetuar uma operação com privilégios elevados. Por exemplo:

* Configurar e inicializar as variáveis de ambiente que tem o executável do serviço. Não é limitado a apenas executáveis escritos através de modelos de programação do Service Fabric. Por exemplo, npm.exe tem algumas variáveis de ambiente configurados para implementar uma aplicação node.js.
* Configurar o controlo de acesso através da instalação de certificados de segurança.

Para obter mais informações sobre como configurar o **SetupEntryPoint**, consulte [Configure a política para um ponto de entrada de configuração de serviço](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Configurar
### <a name="build-a-package-by-using-visual-studio"></a>Criar um pacote com o Visual Studio
Se utilizar o Visual Studio 2015 para criar a sua aplicação, pode utilizar o comando de pacote para criar automaticamente um pacote que corresponda ao esquema descrito acima.

Para criar um pacote, clique com o botão direito no projeto de aplicação no Explorador de soluções e escolha o comando de pacote, conforme mostrado abaixo:

![Empacotamento uma aplicação com o Visual Studio][vs-package-command]

Quando empacotamento estiver concluído, pode encontrar a localização do pacote no **saída** janela. O passo de empacotamento ocorre automaticamente quando implementar ou depurar a aplicação no Visual Studio.

### <a name="build-a-package-by-command-line"></a>Criar um pacote pela linha de comandos
Também é possível através de programação empacotar a aplicação utilizar `msbuild.exe`. Os bastidores, Visual Studio está em execução, pelo que o resultado é o mesmo.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a>O pacote de teste
Pode verificar a estrutura do pacote localmente através do PowerShell utilizando o [teste ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.
Este comando verifica a existência de problemas de analisar o manifesto e verifique se todas as referências. Este comando só verifica a correção estrutural dos diretórios e ficheiros no pacote.
Não verificar qualquer um do conteúdo do pacote de dados ou de código para além de verificar se todos os ficheiros necessários estão presentes.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Este erro mostra que o *MySetup.bat* ficheiro referenciado no manifesto de serviço **SetupEntryPoint** está em falta o pacote do código. Depois do ficheiro em falta é adicionado, passa a verificação da aplicação:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

Se a sua aplicação tiver [parâmetros da aplicação](service-fabric-manage-multiple-environment-app-configuration.md) definida, pode passá-las no [teste ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para validação adequada.

Se souber o cluster onde a aplicação será implementada, recomenda-se que passa a `ImageStoreConnectionString` parâmetro. Neste caso, o pacote também é validado com versões anteriores da aplicação que já estão em execução no cluster. Por exemplo, a validação pode detetar se um pacote com a mesma versão, mas um conteúdo diferente já foi implementado.  

Depois da aplicação é empacotada corretamente e ser aprovado na validação, considere a compressão do pacote para operações de implementação mais rápidas.

## <a name="compress-a-package"></a>Comprimir um pacote
Quando um pacote é grande ou tem vários ficheiros, pode comprimi-los para a implementação mais rápida. Compressão reduz o número de ficheiros e o tamanho do pacote.
Para um pacote de aplicação comprimido [carregar o pacote de aplicação](service-fabric-deploy-remove-applications.md#upload-the-application-package) poderá demorar mais tempo em comparação com a carregar o pacote descomprimido, especialmente se a compressão é efetuada como parte da cópia. Com compressão, [registar](service-fabric-deploy-remove-applications.md#register-the-application-package) e [anular o registo do tipo de aplicação](service-fabric-deploy-remove-applications.md#unregister-an-application-type) são mais rápidas.

O mecanismo de implementação é a mesmo para pacotes comprimidos e descomprimidos. Se o pacote está comprimido, é armazenada como tal no arquivo de imagem do cluster e descomprimido no nó antes da aplicação é executada.
A compressão substitui o pacote de Service Fabric válido com a versão comprimida. A pasta têm de permitir permissões de escrita. A compressão em execução um pacote comprimido já gera sem alterações.

Pode comprimir um pacote, executando o comando do Powershell [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com `CompressPackage` mudar. Pode descomprimir o pacote com o mesmo comando, utilizando `UncompressPackage` mudar.

O seguinte comando comprime o pacote sem copiar para o arquivo de imagens. Pode copiar um pacote comprimido para um ou mais clusters de Service Fabric, conforme necessário, utilizando [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sem o `SkipCopy` sinalizador.
O pacote inclui agora zipped ficheiros para o `code`, `config`, e `data` pacotes. O manifesto da aplicação e os manifestos de serviço não são zipados, porque são necessários para muitas operações internas. Por exemplo, a partilha de pacote, extração de nome e versão do tipo de aplicação para determinados todas as validações devem ter acesso os manifestos. Zipping manifestos iria tornar estas operações ineficaz.

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

Em alternativa, pode comprimir e copiar o pacote com [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) num único passo.
Se o pacote é grande, fornece um tempo limite suficientemente elevado para dar tempo para a compressão de pacote e o carregamento para o cluster.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Internamente, o Service Fabric calcula as somas de verificação para os pacotes de aplicações para a validação. Quando utiliza a compressão, as somas de verificação são calculadas nas versões zipped de cada pacote. Gerar um novo zip no mesmo pacote de aplicação cria as somas de verificação diferentes. Para evitar erros de validação, utilize [diff aprovisionamento](service-fabric-application-upgrade-advanced.md). Com esta opção, não incluem os pacotes não alterados na nova versão. Em vez disso, referencia diretamente a partir do manifesto de serviço novo.

Se o aprovisionamento de diferenciação não é uma opção e tem de incluir os pacotes, gerar novas versões para o `code`, `config`, e `data` pacotes para evitar discrepância de soma de verificação. É necessário gerar novas versões de pacotes inalterados quando é utilizado um pacote comprimido, independentemente se a versão anterior utiliza a compressão ou não.

O pacote é agora embalado corretamente, validado e comprimido (se necessário), para que fique pronta para [implementação](service-fabric-deploy-remove-applications.md) para um ou mais clusters de Service Fabric.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Comprimir pacotes durante a implementação com o Visual Studio
Pode instruir o Visual Studio para comprimir os pacotes de implementação, adicionando o `CopyPackageParameters` elemento para que o perfil de publicação e defina o `CompressPackage` atributo para `true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="create-an-sfpkg"></a>Criar um sfpkg
A partir da versão 6.1, Service Fabric permite o aprovisionamento de um arquivo de externo.
Com esta opção, o pacote de aplicação não tem de ser copiados para o arquivo de imagens. Em vez disso, pode criar um `sfpkg` e carregá-la para um armazenamento externo, em seguida, forneça o URI de transferência para o Service Fabric quando o aprovisionamento. O mesmo pacote pode ser aprovisionado para vários clusters. Aprovisionamento a partir da loja externa guarda o tempo necessário para copiar o pacote para cada cluster.

O `sfpkg` ficheiro é um zip que contém o pacote de aplicação inicial e tem a extensão ". sfpkg".
Dentro do zip, o pacote de aplicações pode ser comprimido ou descomprimido. A compressão do pacote de aplicação no interior do zip é realizada ao código, configuração e níveis de pacote de dados, como [mencionado anteriormente](service-fabric-package-apps.md#compress-a-package).

Para criar um `sfpkg`, começar com uma pasta que contém o pacote de aplicação original, comprimido ou não. Em seguida, utilize qualquer utilitário para zip a pasta com a extensão ". sfpkg". Por exemplo, utilizar [ZipFile.CreateFromDirectory](https://msdn.microsoft.com/library/hh485721(v=vs.110).aspx).

```csharp
ZipFile.CreateFromDirectory(appPackageDirectoryPath, sfpkgFilePath);
```

O `sfpkg` tem de ser carregado para o arquivo de externo fora de banda, fora do Service Fabric. O arquivo de externo pode ser qualquer armazenamento que expõe um ponto final de http ou https REST. Durante o aprovisionamento, o Service Fabric executa uma operação GET para transferir o `sfpkg` pacote de aplicação para o arquivo tem de permitir acesso de leitura para o pacote.

Para aprovisionar o pacote, utilize aprovisionar externo, o que requer o URI de transferência e as informações de tipo de aplicação.

>[!NOTE]
> Aprovisionamento com base na imagem guardar o caminho relativo não suporta atualmente `sfpkg` ficheiros. Por conseguinte, o `sfpkg` não deve ser copiado para o arquivo de imagens.

## <a name="next-steps"></a>Passos Seguintes
[Implementar e remover aplicações] [ 10] descreve como utilizar o PowerShell para gerir instâncias da aplicação

[Gerir parâmetros de aplicação para vários ambientes] [ 11] descreve como configurar os parâmetros e variáveis de ambiente para instâncias de aplicações diferentes.

[Configurar políticas de segurança para a sua aplicação] [ 12] descreve como executar os serviços de políticas de segurança para restringir o acesso.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
