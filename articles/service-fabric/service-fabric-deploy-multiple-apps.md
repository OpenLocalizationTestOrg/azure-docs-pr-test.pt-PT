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
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="55559-103">Implementar vários executáveis convidados</span><span class="sxs-lookup"><span data-stu-id="55559-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="55559-104">Este artigo mostra como toopackage e implementar vários tooAzure de executáveis convidado Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="55559-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="55559-105">Para criar e implementar um único pacote de Service Fabric, leia como demasiado[implementar um tooService executável convidado recursos de infraestrutura](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="55559-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="55559-106">Embora estas instruções mostram como toodeploy uma aplicação com um Node.js front-end que utiliza o MongoDB como arquivo de dados de Olá, pode aplicar Olá passos tooany aplicação que tiver dependências de outra aplicação.</span><span class="sxs-lookup"><span data-stu-id="55559-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="55559-107">Pode utilizar o Visual Studio tooproduce Olá pacote de aplicação que contém vários executáveis de convidado.</span><span class="sxs-lookup"><span data-stu-id="55559-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="55559-108">Consulte [utilizando o Visual Studio toopackage uma aplicação existente](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="55559-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="55559-109">Depois de ter adicionado executável de convidado primeiro Olá, com o botão direito clique no projeto de aplicação Olá e selecione Olá **adicionar -> serviço de recursos de infraestrutura de serviço novo** tooadd Olá segundo convidado executável projeto toohello solução.</span><span class="sxs-lookup"><span data-stu-id="55559-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="55559-110">Nota: Se optar por origem de Olá toolink no Olá projeto do Visual Studio, construir solução do Visual Studio Olá, será Certifique-se de que o pacote de aplicação é segurança toodate com alterações na origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="55559-111">Amostras</span><span class="sxs-lookup"><span data-stu-id="55559-111">Samples</span></span>
* [<span data-ttu-id="55559-112">Exemplo de empacotamento e implementação de um executável de convidado</span><span class="sxs-lookup"><span data-stu-id="55559-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="55559-113">Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST</span><span class="sxs-lookup"><span data-stu-id="55559-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="55559-114">Manualmente o pacote Olá vários aplicação executável de convidado</span><span class="sxs-lookup"><span data-stu-id="55559-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="55559-115">Em alternativa, pode manualmente o pacote convidado Olá executável.</span><span class="sxs-lookup"><span data-stu-id="55559-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="55559-116">Para empacotamento de manual Olá, este artigo utiliza a ferramenta de empacotamento do Olá Service Fabric, que está disponível em [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="55559-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="55559-117">Olá empacotamento aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="55559-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="55559-118">Este artigo pressupõe que o Node.js não está instalado em nós de Olá no cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="55559-119">Como consequence, terá de tooadd Node.exe toohello diretório de raiz da sua aplicação de nó antes de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="55559-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="55559-120">estrutura de diretórios Olá da aplicação de Node.js Olá (utilizando a estrutura do Express web e de motor de modelo Jade) deve ter um aspeto semelhante toohello um abaixo:</span><span class="sxs-lookup"><span data-stu-id="55559-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

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

<span data-ttu-id="55559-121">Como passo seguinte, criar um pacote de aplicação para Olá aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="55559-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="55559-122">código de Olá abaixo cria um pacote de aplicação de Service Fabric que contém a aplicação de Node.js Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="55559-123">Segue-se uma descrição dos parâmetros de Olá que estão a ser utilizado:</span><span class="sxs-lookup"><span data-stu-id="55559-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="55559-124">**/Source** pontos toohello diretório da aplicação Olá que deve ser empacotada.</span><span class="sxs-lookup"><span data-stu-id="55559-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="55559-125">**/ de destino** define diretório Olá num que Olá pacote deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="55559-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="55559-126">Este diretório tem toobe diferente do diretório de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="55559-127">**/appname** define o nome da aplicação Olá da aplicação existente Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="55559-128">É importante toounderstand que isto traduz-se toohello nome do serviço no manifesto de Olá e não toohello nome de aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="55559-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="55559-129">**/exe** define Olá executável que Service Fabric deveria toolaunch, neste caso `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="55559-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="55559-130">**/Ma** define argumento Olá que está a ser utilizado toolaunch Olá executável.</span><span class="sxs-lookup"><span data-stu-id="55559-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="55559-131">Como Node.js não estiver instalado, Service Fabric tem de servidor de web de Node.js de Olá toolaunch executando `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="55559-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="55559-132">`/ma:'bin/www'`indica Olá empacotamento ferramenta toouse `bin/ma` como argumento de Olá para node.exe.</span><span class="sxs-lookup"><span data-stu-id="55559-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="55559-133">**/ AppType** define o nome do tipo de aplicação de Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="55559-134">Se procurar o diretório de toohello que foi especificado no parâmetro de /target Olá, pode ver que essa ferramenta Olá criou um pacote ao funcionamento integral de Service Fabric, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="55559-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="55559-135">Olá ServiceManifest.xml gerado tem agora uma secção que descreve a forma como o servidor de web de Node.js Olá deve ser iniciado, conforme ilustrado no fragmento de código Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="55559-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

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
<span data-ttu-id="55559-136">Neste exemplo, servidor de web de Node.js Olá escuta tooport 3000, pelo que necessita de informações de ponto final de Olá tooupdate no ficheiro de ServiceManifest.xml Olá conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="55559-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="55559-137">Olá empacotamento MongoDB aplicação</span><span class="sxs-lookup"><span data-stu-id="55559-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="55559-138">Agora que tem empacotada aplicação Node.js de Olá, pode avançar e pacotes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55559-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="55559-139">Tal como mencionado anteriormente, os passos de Olá que passar por agora não estão tooNode.js específico e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55559-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="55559-140">Na verdade, aplicam-se aplicações de tooall que se destinam toobe agrupada como uma aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="55559-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="55559-141">toopackage MongoDB, deve certificar-se de que o pacote Mongod.exe e Mongo.exe toomake.</span><span class="sxs-lookup"><span data-stu-id="55559-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="55559-142">Ambos os binários estão localizados em Olá `bin` diretório do seu diretório de instalação do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55559-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="55559-143">estrutura de diretórios Olá procura toohello semelhante um abaixo.</span><span class="sxs-lookup"><span data-stu-id="55559-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="55559-144">Service Fabric tem toostart MongoDB com um toohello semelhante de comando um abaixo, por isso terá de toouse Olá `/ma` parâmetro quando empacotamento MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55559-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="55559-145">dados de Olá não estão a ser mantidos na Olá maiúsculas e minúsculas de uma falha de nó se colocar o diretório de dados de MongoDB Olá no diretório local do Olá do nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="55559-146">Deve utilizar o armazenamento durável ou implementar uma réplica de MongoDB definida em perda de dados de tooprevent de ordem.</span><span class="sxs-lookup"><span data-stu-id="55559-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="55559-147">Na shell de comandos do PowerShell ou Olá, iremos executar ferramenta de empacotamento de Olá com Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="55559-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="55559-148">Ordem tooadd MongoDB tooyour Service Fabric pacote de aplicação, terá de se esse parâmetro de /target Olá pontos toohello toomake mesmo diretório que já contém o manifesto da aplicação Olá, juntamente com a aplicação de Node.js Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="55559-149">Terá também de certificar-se de que está a utilizar toomake Olá mesmo ApplicationType nome.</span><span class="sxs-lookup"><span data-stu-id="55559-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="55559-150">Vamos procurar no diretório toohello e examine a ferramenta que Olá criou.</span><span class="sxs-lookup"><span data-stu-id="55559-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

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
<span data-ttu-id="55559-151">Como pode ver, a ferramenta Olá adicionado um novo diretório de toohello da pasta, MongoDB, que contém os binários de MongoDB Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="55559-152">Se abrir Olá `ApplicationManifest.xml` ficheiro, pode ver esse pacote Olá agora contém a aplicação de Node.js Olá e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55559-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="55559-153">código de Olá abaixo mostra Olá conteúdo Olá do manifesto de aplicação.</span><span class="sxs-lookup"><span data-stu-id="55559-153">hello code below shows hello content of hello application manifest.</span></span>

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

### <a name="publishing-hello-application"></a><span data-ttu-id="55559-154">Aplicação de Olá publicação</span><span class="sxs-lookup"><span data-stu-id="55559-154">Publishing hello application</span></span>
<span data-ttu-id="55559-155">último passo de Olá é toopublish Olá aplicação toohello Service Fabric cluster local com scripts do PowerShell de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="55559-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="55559-156">Assim que a aplicação Olá estiver cluster local toohello publicada com êxito, pode aceder a aplicações de Node.js Olá na porta Olá que foi introduzido no manifesto do serviço de Olá da aplicação de Node.js Olá – por exemplo http://localhost:3000.</span><span class="sxs-lookup"><span data-stu-id="55559-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="55559-157">Neste tutorial, constatou como tooeasily pacote duas aplicações existentes como uma aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="55559-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="55559-158">Também aprendeu como toodeploy-tooService recursos de infraestrutura, para que as TI podem beneficiar do algumas das Olá funcionalidades do Service Fabric, tais como a integração de sistema de estado de funcionamento e disponibilidade elevada.</span><span class="sxs-lookup"><span data-stu-id="55559-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="55559-159">Adicionar mais convidado executáveis tooan aplicação existente utilizando Yeoman no Linux</span><span class="sxs-lookup"><span data-stu-id="55559-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="55559-160">tooadd outra tooan aplicação de serviço já criadas utilizando `yo`, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="55559-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="55559-161">Alterar a raiz de toohello do diretório da aplicação existente Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="55559-162">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é aplicação Olá criada pelo Yeoman.</span><span class="sxs-lookup"><span data-stu-id="55559-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="55559-163">Executar `yo azuresfguest:AddService` e forneça os detalhes necessários Olá.</span><span class="sxs-lookup"><span data-stu-id="55559-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55559-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="55559-164">Next steps</span></span>
* <span data-ttu-id="55559-165">Saiba mais sobre a implementação de contentores com [descrição geral do Service Fabric e os contentores](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="55559-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="55559-166">Exemplo de empacotamento e implementação de um executável de convidado</span><span class="sxs-lookup"><span data-stu-id="55559-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="55559-167">Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST</span><span class="sxs-lookup"><span data-stu-id="55559-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
