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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Atualizar as suas anteriores Java Service Fabric aplicação toofetch Java bibliotecas do Maven
Foi recentemente movido binários de Java de recursos de infraestrutura de serviço do SDK de Java do Service Fabric de Olá tooMaven que aloja. Agora, pode utilizar **mavencentral** dependências de Java de recursos de infraestrutura de serviço do toofetch Olá mais recentes. Isto ajuda início rápido a atualizar as suas aplicações de Java existentes, que criou anteriormente toobe utilizado com o SDK de Java de recursos de infraestrutura de serviço, utilizando o Yeoman modelo ou do Eclipse, toobe compatível com Olá compilação Maven com base.

## <a name="prerequisites"></a>Pré-requisitos
1. Primeiro tem de toouninstall Olá existente SDK de Java.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Seguinte mais recente de Service Fabric CLI do instalação Olá Olá passos mencionados [aqui](service-fabric-cli.md).

3. toobuild e trabalho em aplicações de Java de recursos de infraestrutura do serviço de Olá, terá de tooensure que tiver JDK 1.8 e Gradle instalado. Se ainda não está instalado, pode executar Olá seguintes tooinstall JDK 1.8 (openjdk-8-jdk) e Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Scripts de instalação/desinstalação a Olá da atualização da sua toouse aplicação Olá CLI de recursos de infraestrutura de serviço novo seguindo os passos de Olá mencionados [aqui](service-fabric-application-lifecycle-sfctl.md). Pode consultar tooour introdução [exemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) para referência.

>[!TIP]
> Após a desinstalação Olá SDK de Java do Service Fabric, Yeoman não funcionará. Siga os pré-requisitos de Olá mencionados [aqui](service-fabric-create-your-first-linux-application-with-java.md) toohave Java de Service Fabric Yeoman gerador de modelo de cópia de segurança e em funcionamento.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliotecas Java do Service Fabric no Maven
As bibliotecas Java do Service Fabric foram alojadas no Maven. Pode adicionar Olá dependências no Olá ``pom.xml`` ou ``build.gradle`` das suas bibliotecas de Service Fabric Java toouse projetos de **mavenCentral**.

### <a name="actors"></a>Atores

Suporte de Reliable Actor do Service Fabric para a sua aplicação.

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

### <a name="services"></a>Serviços

Suporte de Serviço sem Estado do Service Fabric para a sua aplicação.

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

### <a name="others"></a>Outros
#### <a name="transport"></a>Transporte

Suporte da camada de transporte para a aplicação Java do Service Fabric. Não é necessário adicionar tooexplicitly esta dependência tooyour Ator fiável ou aplicações de serviço, a menos que o programa na camada de transporte de Olá.

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

#### <a name="fabric-support"></a>Suporte para o Fabric

Suporte de nível de sistema para que a sua toonative Service Fabric runtime do Service Fabric. Não é necessário tooexplicitly adicionar esta dependência tooyour Ator fiável ou aplicações de serviço. Este obtém recuperado automaticamente do Maven, ao incluir Olá outras dependências acima.

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


## <a name="migrating-service-fabric-stateless-service"></a>Migrar Serviço sem Estado do Service Fabric

toobuild capaz de toobe o Service Fabric sem monitorização de estado Java serviço existente com as dependências do Service Fabric recuperadas do Maven, terá de tooupdate Olá ``build.gradle`` ficheiro dentro Olá serviço. Tenha utilizado da seguinte forma - toobe como
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
Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -
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
Em geral, tooget uma ideia geral sobre como Olá criar script teria aspeto para um serviço de Java sem monitorização de estado do Service Fabric, pode consultar tooany exemplo dos nossos exemplos de introdução. Eis Olá [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) para amostra de EchoServer Olá.

## <a name="migrating-service-fabric-actor-service"></a>Migrar o Serviço Actor do Service Fabric

toobe toobuild capacidade, a aplicação de Java de Ator de recursos de infraestrutura de serviço existente utilizando dependências de Service Fabric recuperadas do Maven, terá de tooupdate Olá ``build.gradle`` ficheiro no interior do pacote da interface de Olá e no pacote de serviço Olá. Se tiver um pacote de TestClient, terá de tooupdate que bem. Sim, para o seu ator ``Myactor``, seguinte Olá seria locais olá onde terá tooupdate -
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Atualizar o script de compilação do projeto de interface de Olá

Tenha utilizado da seguinte forma - toobe como
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -
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

#### <a name="updating-build-script-for-hello-actor-project"></a>Atualizar o script de compilação do projeto de ator Olá

Tenha utilizado da seguinte forma - toobe como
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
Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -
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

#### <a name="updating-build-script-for-hello-test-client-project"></a>Atualizar o script de compilação do projeto de cliente de teste de Olá

Alterações aqui são semelhantes alterações de toohello abordadas na secção anterior, ou seja, o projeto de ator Olá. Olá anteriormente Gradle toobe de script utilizada como forma-
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
Agora, as dependências de Olá toofetch do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá forma -
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

## <a name="next-steps"></a>Passos seguintes

* [Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Plug-in do Service Fabric para Eclipse](service-fabric-get-started-eclipse.md)
* [Interagir com clusters do Service Fabric através da Olá CLI de recursos de infraestrutura de serviço](service-fabric-cli.md)
