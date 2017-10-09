---
title: "aaaMigrate do SDK de Java tooMaven - atualizar antigo aplicações de Java do Azure Service Fabric toouse Maven | Microsoft Docs"
description: "Atualize Olá mais antigas aplicações Java que utilizado toouse Olá SDK de Java do Service Fabric, dependências do Service Fabric Java toofetch do Maven. Depois de concluir esta configuração, as aplicações mais antigas do Java seria capaz de toobuild."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="293fe-104">Atualizar as suas anteriores Java Service Fabric aplicação toofetch Java bibliotecas do Maven</span><span class="sxs-lookup"><span data-stu-id="293fe-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="293fe-105">Foi recentemente movido binários de Java de recursos de infraestrutura de serviço do SDK de Java do Service Fabric de Olá tooMaven que aloja.</span><span class="sxs-lookup"><span data-stu-id="293fe-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="293fe-106">Agora, pode utilizar **mavencentral** dependências de Java de recursos de infraestrutura de serviço do toofetch Olá mais recentes.</span><span class="sxs-lookup"><span data-stu-id="293fe-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="293fe-107">Isto ajuda início rápido a atualizar as suas aplicações de Java existentes, que criou anteriormente toobe utilizado com o SDK de Java de recursos de infraestrutura de serviço, utilizando o Yeoman modelo ou do Eclipse, toobe compatível com Olá compilação Maven com base.</span><span class="sxs-lookup"><span data-stu-id="293fe-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="293fe-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="293fe-108">Prerequisites</span></span>
1. <span data-ttu-id="293fe-109">Primeiro tem de toouninstall Olá existente SDK de Java.</span><span class="sxs-lookup"><span data-stu-id="293fe-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="293fe-110">Seguinte mais recente de Service Fabric CLI do instalação Olá Olá passos mencionados [aqui](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="293fe-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="293fe-111">toobuild e trabalho em aplicações de Java de recursos de infraestrutura do serviço de Olá, terá de tooensure que tiver JDK 1.8 e Gradle instalado.</span><span class="sxs-lookup"><span data-stu-id="293fe-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="293fe-112">Se ainda não está instalado, pode executar Olá seguintes tooinstall JDK 1.8 (openjdk-8-jdk) e Gradle -</span><span class="sxs-lookup"><span data-stu-id="293fe-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="293fe-113">Scripts de instalação/desinstalação a Olá da atualização da sua toouse aplicação Olá CLI de recursos de infraestrutura de serviço novo seguindo os passos de Olá mencionados [aqui](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="293fe-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="293fe-114">Pode consultar tooour introdução [exemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) para referência.</span><span class="sxs-lookup"><span data-stu-id="293fe-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="293fe-115">Após a desinstalação Olá SDK de Java do Service Fabric, Yeoman não funcionará.</span><span class="sxs-lookup"><span data-stu-id="293fe-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="293fe-116">Siga os pré-requisitos de Olá mencionados [aqui](service-fabric-create-your-first-linux-application-with-java.md) toohave Java de Service Fabric Yeoman gerador de modelo de cópia de segurança e em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="293fe-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="293fe-117">Bibliotecas Java do Service Fabric no Maven</span><span class="sxs-lookup"><span data-stu-id="293fe-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="293fe-118">As bibliotecas Java do Service Fabric foram alojadas no Maven.</span><span class="sxs-lookup"><span data-stu-id="293fe-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="293fe-119">Pode adicionar Olá dependências no Olá ``pom.xml`` ou ``build.gradle`` das suas bibliotecas de Service Fabric Java toouse projetos de **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="293fe-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="293fe-120">Atores</span><span class="sxs-lookup"><span data-stu-id="293fe-120">Actors</span></span>

<span data-ttu-id="293fe-121">Suporte de Reliable Actor do Service Fabric para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="293fe-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="293fe-122">Serviços</span><span class="sxs-lookup"><span data-stu-id="293fe-122">Services</span></span>

<span data-ttu-id="293fe-123">Suporte de Serviço sem Estado do Service Fabric para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="293fe-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="293fe-124">Outros</span><span class="sxs-lookup"><span data-stu-id="293fe-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="293fe-125">Transporte</span><span class="sxs-lookup"><span data-stu-id="293fe-125">Transport</span></span>

<span data-ttu-id="293fe-126">Suporte da camada de transporte para a aplicação Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="293fe-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="293fe-127">Não é necessário adicionar tooexplicitly esta dependência tooyour Ator fiável ou aplicações de serviço, a menos que o programa na camada de transporte de Olá.</span><span class="sxs-lookup"><span data-stu-id="293fe-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="293fe-128">Suporte para o Fabric</span><span class="sxs-lookup"><span data-stu-id="293fe-128">Fabric support</span></span>

<span data-ttu-id="293fe-129">Suporte de nível de sistema para que a sua toonative Service Fabric runtime do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="293fe-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="293fe-130">Não é necessário tooexplicitly adicionar esta dependência tooyour Ator fiável ou aplicações de serviço.</span><span class="sxs-lookup"><span data-stu-id="293fe-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="293fe-131">Este obtém recuperado automaticamente do Maven, ao incluir Olá outras dependências acima.</span><span class="sxs-lookup"><span data-stu-id="293fe-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="293fe-132">Migrar Serviço sem Estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="293fe-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="293fe-133">toobuild capaz de toobe o Service Fabric sem monitorização de estado Java serviço existente com as dependências do Service Fabric recuperadas do Maven, terá de tooupdate Olá ``build.gradle`` ficheiro dentro Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="293fe-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="293fe-134">Tenha utilizado da seguinte forma - toobe como</span><span class="sxs-lookup"><span data-stu-id="293fe-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="293fe-135">Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -</span><span class="sxs-lookup"><span data-stu-id="293fe-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="293fe-136">Em geral, tooget uma ideia geral sobre como Olá criar script teria aspeto para um serviço de Java sem monitorização de estado do Service Fabric, pode consultar tooany exemplo dos nossos exemplos de introdução.</span><span class="sxs-lookup"><span data-stu-id="293fe-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="293fe-137">Eis Olá [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) para amostra de EchoServer Olá.</span><span class="sxs-lookup"><span data-stu-id="293fe-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="293fe-138">Migrar o Serviço Actor do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="293fe-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="293fe-139">toobe toobuild capacidade, a aplicação de Java de Ator de recursos de infraestrutura de serviço existente utilizando dependências de Service Fabric recuperadas do Maven, terá de tooupdate Olá ``build.gradle`` ficheiro no interior do pacote da interface de Olá e no pacote de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="293fe-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="293fe-140">Se tiver um pacote de TestClient, terá de tooupdate que bem.</span><span class="sxs-lookup"><span data-stu-id="293fe-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="293fe-141">Sim, para o seu ator ``Myactor``, seguinte Olá seria locais olá onde terá tooupdate -</span><span class="sxs-lookup"><span data-stu-id="293fe-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="293fe-142">Atualizar o script de compilação do projeto de interface de Olá</span><span class="sxs-lookup"><span data-stu-id="293fe-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="293fe-143">Tenha utilizado da seguinte forma - toobe como</span><span class="sxs-lookup"><span data-stu-id="293fe-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="293fe-144">Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -</span><span class="sxs-lookup"><span data-stu-id="293fe-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="293fe-145">Atualizar o script de compilação do projeto de ator Olá</span><span class="sxs-lookup"><span data-stu-id="293fe-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="293fe-146">Tenha utilizado da seguinte forma - toobe como</span><span class="sxs-lookup"><span data-stu-id="293fe-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="293fe-147">Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -</span><span class="sxs-lookup"><span data-stu-id="293fe-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="293fe-148">Atualizar o script de compilação do projeto de cliente de teste de Olá</span><span class="sxs-lookup"><span data-stu-id="293fe-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="293fe-149">Alterações aqui são semelhantes alterações de toohello abordadas na secção anterior, ou seja, o projeto de ator Olá.</span><span class="sxs-lookup"><span data-stu-id="293fe-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="293fe-150">Olá anteriormente Gradle toobe de script utilizada como forma-</span><span class="sxs-lookup"><span data-stu-id="293fe-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="293fe-151">Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -</span><span class="sxs-lookup"><span data-stu-id="293fe-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="293fe-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="293fe-152">Next steps</span></span>

* [<span data-ttu-id="293fe-153">Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Yeoman</span><span class="sxs-lookup"><span data-stu-id="293fe-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="293fe-154">Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Plug-in do Service Fabric para Eclipse</span><span class="sxs-lookup"><span data-stu-id="293fe-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="293fe-155">Interagir com clusters do Service Fabric através da Olá CLI de recursos de infraestrutura de serviço</span><span class="sxs-lookup"><span data-stu-id="293fe-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
