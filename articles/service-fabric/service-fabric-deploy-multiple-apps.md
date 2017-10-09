---
title: "aaaDeploy uma aplicação Node.js que utiliza o MongoDB | Microsoft Docs"
description: "Instruções sobre como toopackage vários executáveis toodeploy tooan Azure Service Fabric cluster de convidados"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a>Implementar vários executáveis convidados
Este artigo mostra como toopackage e implementar vários tooAzure de executáveis convidado Service Fabric. Para criar e implementar um único pacote de Service Fabric, leia como demasiado[implementar um tooService executável convidado recursos de infraestrutura](service-fabric-deploy-existing-app.md).

Embora estas instruções mostram como toodeploy uma aplicação com um Node.js front-end que utiliza o MongoDB como arquivo de dados de Olá, pode aplicar Olá passos tooany aplicação que tiver dependências de outra aplicação.   

Pode utilizar o Visual Studio tooproduce Olá pacote de aplicação que contém vários executáveis de convidado. Consulte [utilizando o Visual Studio toopackage uma aplicação existente](service-fabric-deploy-existing-app.md). Depois de ter adicionado executável de convidado primeiro Olá, com o botão direito clique no projeto de aplicação Olá e selecione Olá **adicionar -> serviço de recursos de infraestrutura de serviço novo** tooadd Olá segundo convidado executável projeto toohello solução. Nota: Se optar por origem de Olá toolink no Olá projeto do Visual Studio, construir solução do Visual Studio Olá, será Certifique-se de que o pacote de aplicação é segurança toodate com alterações na origem de Olá. 

## <a name="samples"></a>Amostras
* [Exemplo de empacotamento e implementação de um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Manualmente o pacote Olá vários aplicação executável de convidado
Em alternativa, pode manualmente o pacote convidado Olá executável. Para empacotamento de manual Olá, este artigo utiliza a ferramenta de empacotamento do Olá Service Fabric, que está disponível em [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Olá empacotamento aplicação Node.js
Este artigo pressupõe que o Node.js não está instalado em nós de Olá no cluster do Service Fabric Olá. Como consequence, terá de tooadd Node.exe toohello diretório de raiz da sua aplicação de nó antes de empacotamento. estrutura de diretórios Olá da aplicação de Node.js Olá (utilizando a estrutura do Express web e de motor de modelo Jade) deve ter um aspeto semelhante toohello um abaixo:

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

Como passo seguinte, criar um pacote de aplicação para Olá aplicação Node.js. código de Olá abaixo cria um pacote de aplicação de Service Fabric que contém a aplicação de Node.js Olá.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Segue-se uma descrição dos parâmetros de Olá que estão a ser utilizado:

* **/Source** pontos toohello diretório da aplicação Olá que deve ser empacotada.
* **/ de destino** define diretório Olá num que Olá pacote deve ser criado. Este diretório tem toobe diferente do diretório de origem Olá.
* **/appname** define o nome da aplicação Olá da aplicação existente Olá. É importante toounderstand que isto traduz-se toohello nome do serviço no manifesto de Olá e não toohello nome de aplicação de Service Fabric.
* **/exe** define Olá executável que Service Fabric deveria toolaunch, neste caso `node.exe`.
* **/Ma** define argumento Olá que está a ser utilizado toolaunch Olá executável. Como Node.js não estiver instalado, Service Fabric tem de servidor de web de Node.js de Olá toolaunch executando `node.exe bin/www`.  `/ma:'bin/www'`indica Olá empacotamento ferramenta toouse `bin/ma` como argumento de Olá para node.exe.
* **/ AppType** define o nome do tipo de aplicação de Service Fabric Olá.

Se procurar o diretório de toohello que foi especificado no parâmetro de /target Olá, pode ver que essa ferramenta Olá criou um pacote ao funcionamento integral de Service Fabric, conforme mostrado abaixo:

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Olá ServiceManifest.xml gerado tem agora uma secção que descreve a forma como o servidor de web de Node.js Olá deve ser iniciado, conforme ilustrado no fragmento de código Olá abaixo:

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
Neste exemplo, servidor de web de Node.js Olá escuta tooport 3000, pelo que necessita de informações de ponto final de Olá tooupdate no ficheiro de ServiceManifest.xml Olá conforme mostrado abaixo.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Olá empacotamento MongoDB aplicação
Agora que tem empacotada aplicação Node.js de Olá, pode avançar e pacotes MongoDB. Tal como mencionado anteriormente, os passos de Olá que passar por agora não estão tooNode.js específico e MongoDB. Na verdade, aplicam-se aplicações de tooall que se destinam toobe agrupada como uma aplicação de Service Fabric.  

toopackage MongoDB, deve certificar-se de que o pacote Mongod.exe e Mongo.exe toomake. Ambos os binários estão localizados em Olá `bin` diretório do seu diretório de instalação do MongoDB. estrutura de diretórios Olá procura toohello semelhante um abaixo.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric tem toostart MongoDB com um toohello semelhante de comando um abaixo, por isso terá de toouse Olá `/ma` parâmetro quando empacotamento MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> dados de Olá não estão a ser mantidos na Olá maiúsculas e minúsculas de uma falha de nó se colocar o diretório de dados de MongoDB Olá no diretório local do Olá do nó de Olá. Deve utilizar o armazenamento durável ou implementar uma réplica de MongoDB definida em perda de dados de tooprevent de ordem.  
>
>

Na shell de comandos do PowerShell ou Olá, iremos executar ferramenta de empacotamento de Olá com Olá os seguintes parâmetros:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

Ordem tooadd MongoDB tooyour Service Fabric pacote de aplicação, terá de se esse parâmetro de /target Olá pontos toohello toomake mesmo diretório que já contém o manifesto da aplicação Olá, juntamente com a aplicação de Node.js Olá. Terá também de certificar-se de que está a utilizar toomake Olá mesmo ApplicationType nome.

Vamos procurar no diretório toohello e examine a ferramenta que Olá criou.

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Como pode ver, a ferramenta Olá adicionado um novo diretório de toohello da pasta, MongoDB, que contém os binários de MongoDB Olá. Se abrir Olá `ApplicationManifest.xml` ficheiro, pode ver esse pacote Olá agora contém a aplicação de Node.js Olá e MongoDB. código de Olá abaixo mostra Olá conteúdo Olá do manifesto de aplicação.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a>Aplicação de Olá publicação
último passo de Olá é toopublish Olá aplicação toohello Service Fabric cluster local com scripts do PowerShell de Olá abaixo:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Assim que a aplicação Olá estiver cluster local toohello publicada com êxito, pode aceder a aplicações de Node.js Olá na porta Olá que foi introduzido no manifesto do serviço de Olá da aplicação de Node.js Olá – por exemplo http://localhost:3000.

Neste tutorial, constatou como tooeasily pacote duas aplicações existentes como uma aplicação de Service Fabric. Também aprendeu como toodeploy-tooService recursos de infraestrutura, para que as TI podem beneficiar do algumas das Olá funcionalidades do Service Fabric, tais como a integração de sistema de estado de funcionamento e disponibilidade elevada.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Adicionar mais convidado executáveis tooan aplicação existente utilizando Yeoman no Linux

tooadd outra tooan aplicação de serviço já criadas utilizando `yo`, efetuar Olá os seguintes passos: 
1. Alterar a raiz de toohello do diretório da aplicação existente Olá.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é aplicação Olá criada pelo Yeoman.
2. Executar `yo azuresfguest:AddService` e forneça os detalhes necessários Olá.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre a implementação de contentores com [descrição geral do Service Fabric e os contentores](service-fabric-containers-overview.md)
* [Exemplo de empacotamento e implementação de um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
