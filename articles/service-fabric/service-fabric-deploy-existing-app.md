---
title: "aaaDeploy um tooAzure executável existente Service Fabric | Microsoft Docs"
description: "Obter instruções sobre como toopackage uma aplicação existente como um executável de convidado, pelo que pode ser implementado tooa cluster do Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Implementar um tooService executável convidado recursos de infraestrutura
Pode executar qualquer tipo de código, tal como o Node.js, Java ou C++ no Service Fabric do Azure como um serviço. Service Fabric refere-se os tipos de toothese de serviços como convidado executáveis.

Executáveis de convidado são tratadas pelo serviço de recursos de infraestrutura, como serviços sem monitorização de estado. Como resultado, são colocadas em nós num cluster, com base na disponibilidade e outras métricas. Este artigo descreve como toopackage e implementar um cluster de Service Fabric tooa executável do convidado, utilizando o Visual Studio ou um utilitário da linha de comandos.

Neste artigo, iremos abranger Olá passos toopackage um convidado executável e implementá-la tooService recursos de infraestrutura.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Benefícios da execução de um convidado executável no Service Fabric
Existem várias vantagens toorunning um convidado executável num cluster de Service Fabric:

* Elevada disponibilidade. Aplicações executadas no Service Fabric que são efetuadas altamente disponíveis. Service Fabric assegura que as instâncias de uma aplicação estão em execução.
* Monitorização de estado de funcionamento. Monitorização de estado de funcionamento do Service Fabric Deteta se uma aplicação está em execução e fornece informações de diagnóstico, se ocorrer uma falha.   
* Gestão de ciclo de vida de aplicações. Para além de fornecer atualizações sem período de indisponibilidade, Service Fabric fornece a versão anterior do toohello Reversão automática se ocorrer um evento de estado de funcionamento incorreto comunicado durante uma atualização.    
* Densidade. Pode executar várias aplicações num cluster, eliminando a necessidade de Olá de cada toorun de aplicação no seu próprio hardware.
* Capacidade de Deteção: Utilizar REST pode chamar Olá Service Fabric Naming service toofind outros serviços no cluster de Olá. 

## <a name="samples"></a>Amostras
* [Exemplo de empacotamento e implementação de um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Descrição geral da aplicação e ficheiros de manifesto do serviço
Como parte da implementação de um executável de convidado, é empacotamento de Service Fabric toounderstand útil Olá e modelo de implementação, tal como descrito no [modelo de aplicação](service-fabric-application-model.md). modelo de empacotamento de Service Fabric Olá baseia-se em dois ficheiros XML: Olá manifestos de aplicação e serviços. Olá definição de esquema para a hello ficheiros ApplicationManifest.xml e ServiceManifest.xml com Olá SDK de Service Fabric para *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **O manifesto da aplicação** manifesto da aplicação Olá é utilizado toodescribe Olá aplicação. Lista os serviços de Olá que compõem-lo e outros parâmetros que são utilizado toodefine devem ser implementados como um ou mais serviços, tais como o número de Olá de instâncias.

  No Service Fabric, uma aplicação é uma unidade de implementação e a atualização. É possível atualizar uma aplicação como uma única unidade em que é geridos os potenciais falhas e reverte potenciais. Service Fabric garante que os processo de atualização de Olá é efetuada com êxito, ou, se Olá atualização falhar, não deixe a Olá aplicação num Estado desconhecido ou instável.
* **O manifesto do serviço** manifesto do serviço de Olá descreve Olá os componentes de um serviço. Inclui dados, tais como o nome de Olá e tipo de serviço e o código e a configuração. Olá manifesto do serviço também inclui alguns parâmetros adicionais que podem ser utilizados o serviço de Olá tooconfigure assim que for implementado.

## <a name="application-package-file-structure"></a>Estrutura de ficheiros do pacote de aplicação
toodeploy tooService uma aplicação dos recursos de infraestrutura, aplicação Olá deve seguir a estrutura de diretórios predefinidos. Olá segue-se um exemplo dessa estrutura.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Olá ApplicationPackageRoot contém ficheiros de ApplicationManifest.xml Olá que define a aplicação Olá. Um subdiretório para cada serviço incluído na aplicação Olá é utilizado toocontain Olá todos os artefactos Olá serviço necessita. Estes subdiretórios são Olá ServiceManifest.xml e, normalmente, Olá seguintes:

* *Código*. Este diretório contém o código do serviço Olá.
* *Configuração*. Este diretório contém um ficheiro de Settings.xml (e outros ficheiros, se necessário) que o serviço de Olá consegue aceder às definições de configuração específicas de tooretrieve de tempo de execução.
* *Dados*. Este é um diretório adicional toostore local dados adicionais que poderá ter o serviço de Olá. Dados devem estar dados apenas efémeras toostore utilizados. Service Fabric efetua uma cópia não replicar as alterações toohello dados diretório ou se precisa de serviço Olá toobe relocalizada (por exemplo, durante a ativação pós-falha).

> [!NOTE]
> Não tem toocreate Olá `config` e `data` diretórios se não precisar deles.
>
>

## <a name="package-an-existing-executable"></a>Pacote de um executável existente
Quando empacotamento um executável de convidado, pode escolher qualquer toouse um modelo de projeto do Visual Studio ou demasiado[criar manualmente o pacote de aplicação Olá](#manually). Com o Visual Studio, Olá a estrutura do pacote de aplicação e ficheiros de manifesto são criados pelo modelo de projeto novo Olá para si.

> [!TIP]
> Olá toopackage da forma mais fácil um executável para um serviço existentes do Windows é toouse Visual Studio e em Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Utilizar o Visual Studio toopackage e implementar um executável existente
O Visual Studio fornece uma infraestrutura de serviço toohelp de modelo de serviço implementar um cluster convidado do Service Fabric tooa executável.

1. Escolha **ficheiro** > **novo projeto**e crie uma aplicação de Service Fabric.
2. Escolha **convidado executável** como modelo de serviço Olá.
3. Clique em **procurar** pasta de Olá tooselect com os seus executável e preencha rest Olá do serviço de Olá Olá parâmetros toocreate.
   * *Comportamento de pacote de código*. Pode ser conjunto toocopy todo o conteúdo de Olá do seu toohello pasta projeto do Visual Studio, que é útil se Olá executável não se altera. Se esperar toochange executável Olá e quiser Olá capacidade toopick cópias de segurança novas compilações dinamicamente, pode escolher toolink toohello pasta em vez disso. Pode utilizar as pastas de ligado ao criar o projeto de aplicação Olá no Visual Studio. Esta ação liga a localização de origem toohello de dentro do projeto de Olá, tornando possíveis para tooupdate Olá convidado executável no respetivo destino de origem. Essas atualizações passam a fazer parte do pacote de aplicação Olá na compilação.
   * *Programa* Especifica executável Olá que deve ser executado o serviço de Olá toostart.
   * *Argumentos* Especifica Olá argumentos que devem ser transmitidos toohello executável. Pode ser uma lista de parâmetros com argumentos.
   * *WorkingFolder* Especifica o diretório de trabalho de Olá para o processo de Olá que vai toobe foi iniciado. Pode especificar três valores:
     * `CodeBase`Especifica o diretório de trabalho que Olá vai toobe definir o diretório de código toohello no pacote de aplicação Olá (`Code` directory apresentados no Olá anterior a estrutura de ficheiros).
     * `CodePackage`Especifica o diretório de trabalho que Olá vai toobe definir toohello raiz Olá do pacote de aplicação (`GuestService1Pkg` mostrado na Olá anterior a estrutura de ficheiros).
     * `Work`Especifica que os ficheiros de Olá são colocados num subdiretório chamado trabalho.
4. Dê um nome ao serviço e clique em **OK**.
5. Se o serviço precisa de um ponto final para a comunicação, agora pode adicionar Olá protocolo, porta e ficheiros do tipo toohello ServiceManifest.xml. Por exemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Agora pode utilizar o pacote de Olá e publique ação contra o seu cluster local através da depuração solução Olá no Visual Studio. Quando estiver pronto, pode publicar cluster remoto do Olá aplicação tooa ou verifique no controlo de toosource Olá solução.
7. Aceda a fim de toohello do toosee artigo como tooview o serviço de executável de convidado em execução no Service Fabric Explorer.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Utilizar Yoeman toopackage e implementar um executável existente no Linux

procedimento Olá para criar e implementar um convidado executável no Linux é Olá igual ao implementar uma aplicação csharp ou java.

1. Num terminal, escreva `yo azuresfguest`.
2. Dê um nome à aplicação.
3. Nome do seu serviço e forneça detalhes Olá, incluindo o caminho de Olá executável e parâmetros de Olá que tem de ser invocado com.

Yeoman cria um pacote de aplicação com a aplicação apropriada Olá e ficheiros de manifesto juntamente com instalar e desinstalar scripts.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Manualmente o pacote e implementar um executável existente
processo de Olá de empacotamento manualmente um executável de convidado é baseado no Olá os seguintes passos gerais:

1. Crie a estrutura de diretórios do pacote de Olá.
2. Adicione ficheiros de código e a configuração da aplicação Olá.
3. Edite o ficheiro de manifesto do serviço de Olá.
4. Edite o ficheiro de manifesto da aplicação Olá.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Criar a estrutura de diretórios do pacote de Olá
Pode começar por criar a estrutura de diretórios Olá, conforme descrito em Olá anterior a secção, "Aplicação pacote estrutura de ficheiros."

### <a name="add-hello-applications-code-and-configuration-files"></a>Adicionar ficheiros de código e a configuração da aplicação Olá
Depois de ter criado a estrutura de diretórios Olá, pode adicionar os ficheiros de código e a configuração da aplicação Olá em diretórios Olá de configuração e de código. Também pode criar diretórios adicionais ou subdiretórios diretórios Olá de configuração ou de código.

Service Fabric um `xcopy` de conteúdo de Olá Olá aplicação raiz do diretório de, pelo que não existe nenhum toouse estrutura predefinidas que não sejam de criação de dois diretórios superiores, o código e definições. (Pode escolher nomes diferentes se pretender. Obter mais detalhes estão na secção seguinte, Olá).

> [!NOTE]
> Certifique-se de que inclui todos os ficheiros de Olá e dependências Olá necessidades de aplicação. Service Fabric copia Olá conteúdo do pacote de aplicação Olá em todos os nós no cluster de olá onde os serviços da aplicação Olá são toobe contínuo implementado. pacote de Olá deve conter todo o código Olá que aplicação Olá tem toorun. Não parta do princípio que dependências Olá já estão instaladas.
>
>

### <a name="edit-hello-service-manifest-file"></a>Editar o ficheiro de manifesto do serviço de Olá
Olá passo seguinte consiste nas Olá de tooinclude serviço de Olá do tooedit ficheiro de manifesto seguintes informações:

* nome de Olá Olá do tipo de serviço. Este é um ID que o Service Fabric utiliza tooidentify um serviço.
* Olá comando toouse toolaunch Olá aplicação (ExeHost).
* Qualquer script que necessita de tooset toobe executar cópias de segurança aplicação Olá (SetupEntrypoint).

Olá segue-se um exemplo de um `ServiceManifest.xml` ficheiro:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Olá secções a seguir abordar as diferentes partes Olá do ficheiro de Olá terá tooupdate.

#### <a name="update-servicetypes"></a>Atualizar ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Pode escolher qualquer nome que pretende para `ServiceTypeName`. valor de Olá é utilizado no Olá `ApplicationManifest.xml` tooidentify Olá serviço ficheiro.
* Especifique `UseImplicitHost="true"`. Este atributo indica ao Service Fabric que o serviço de Olá baseia-se numa aplicação autónomo, pelo que necessita de todos os recursos de infraestrutura de serviço toodo é toolaunch-o como um processo e monitorizar o estado de funcionamento.

#### <a name="update-codepackage"></a>Atualizar o CodePackage
elemento de CodePackage Olá Especifica a localização de Olá (e versão) de código do serviço de Olá.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Olá `Name` elemento é o nome de Olá de toospecify utilizado do diretório de Olá no pacote de aplicação Olá que contém o código do serviço de Olá. `CodePackage`Também tem Olá `version` atributo. Isto pode ser utilizado toospecify Olá versão de código Olá e potencialmente também pode ser utilizado o código do serviço de Olá tooupgrade utilizando a infraestrutura de gestão de ciclo de vida de aplicação Olá no Service Fabric.

#### <a name="optional-update-setupentrypoint"></a>Opcional: SetupEntrypoint de atualização
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
elemento de SetupEntryPoint Olá é toospecify utilizada qualquer ficheiro executável ou lote que deve ser executado antes do código do serviço de Olá for iniciado. Este passo é opcional, pelo que não é necessário toobe incluído se não houver nenhuma necessária inicialização. Olá SetupEntryPoint é executada sempre que o serviço de Olá for reiniciado.

Não há SetupEntryPoint apenas uma, por isso, scripts de configuração precisam toobe agrupada num ficheiro batch único se a configuração da aplicação Olá necessitar de vários scripts. Olá SetupEntryPoint pode executar qualquer tipo de ficheiro: ficheiros executáveis, ficheiros batch e cmdlets do PowerShell. Para obter mais detalhes, consulte [configurar SetupEntryPoint](service-fabric-application-runas-security.md).

No Olá anterior exemplo, Olá SetupEntryPoint executa um ficheiro batch chamado `LaunchConfig.cmd` que está localizado no Olá `scripts` subdiretório do diretório de código Olá (partindo do princípio de elemento de WorkingFolder Olá está definido tooCodeBase).

#### <a name="update-entrypoint"></a>Atualizar o ponto de entrada
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Olá `EntryPoint` elemento no ficheiro de manifesto do serviço de Olá é toospecify utilizado como serviço de Olá toolaunch. Olá `ExeHost` elemento Especifica Olá executável (e os argumentos) que deve ser utilizado o serviço de Olá toolaunch.

* `Program`Especifica o nome de Olá do executável de Olá que deve iniciar o serviço de Olá.
* `Arguments`Especifica os argumentos de Olá que devem ser transmitidos toohello executável. Pode ser uma lista de parâmetros com argumentos.
* `WorkingFolder`Especifica o diretório de trabalho de Olá para o processo de Olá que vai toobe foi iniciado. Pode especificar três valores:
  * `CodeBase`Especifica o diretório de trabalho que Olá vai toobe definir o diretório de código toohello no pacote de aplicação Olá (`Code` diretório no Olá anterior a estrutura de ficheiros).
  * `CodePackage`Especifica o diretório de trabalho que Olá vai toobe definir toohello raiz Olá do pacote de aplicação (`GuestService1Pkg` no Olá anterior a estrutura de ficheiros).
    * `Work`Especifica que os ficheiros de Olá são colocados num subdiretório chamado trabalho.

Olá WorkingFolder é o diretório de trabalho correto Olá tooset útil para que os caminhos relativos podem ser utilizados por qualquer um dos scripts de aplicação ou inicialização Olá.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Atualizar pontos finais e registar com o serviço de nomenclatura para comunicação
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
No Olá anterior exemplo, Olá `Endpoint` elemento Especifica pontos finais de Olá que aplicação Olá pode escutar. Neste exemplo, Olá aplicação Node.js escuta de http na porta 3000.

Além disso pode pedir ao Service Fabric toopublish este toohello ponto final de serviço de nomes para que outros serviços podem detetar o serviço de toothis de endereço de ponto final de Olá. Isto permite-lhe toobe toocommunicate capaz de entre os serviços convidados executáveis.
Olá endereço do ponto final publicada é de formulário Olá `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme`e `PathSuffix` são atributos opcionais. `IPAddressOrFQDN`é Olá endereço IP ou nome de domínio completamente qualificado do nó de Olá este ficheiro executável obtém colocado e esta é calculada para si.

No hello exemplo seguinte, uma vez serviço de Olá é implementado, no Service Fabric Explorer verá um ponto final semelhante demasiado`http://10.1.4.92:3000/myapp/` publicados para a instância de serviço Olá. Ou se se tratar de um computador local, consulte `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Pode utilizar estes endereços com [proxy inverso](service-fabric-reverseproxy.md) toocommunicate entre serviços.

### <a name="edit-hello-application-manifest-file"></a>Editar o ficheiro de manifesto da aplicação Olá
Assim que tiver configurado Olá `Servicemanifest.xml` ficheiro, terá de toomake toohello algumas alterações `ApplicationManifest.xml` ficheiro tooensure Olá são utilizados o tipo de serviço e o nome correto.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
No Olá `ServiceManifestImport` elemento, pode especificar um ou mais serviços que pretende que o tooinclude na aplicação Olá. Os serviços são referenciados com `ServiceManifestName`, que especifica o nome de Olá do diretório de olá onde hello `ServiceManifest.xml` está localizado o ficheiro.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Configurar o registo
Para executáveis de convidado, é útil toobe toosee capaz de consola registos toofind enviados se scripts de configuração e aplicação Olá mostram erros.
Redirecionamento de consola pode ser configurado no Olá `ServiceManifest.xml` ficheiro utilizando Olá `ConsoleRedirection` elemento.

> [!WARNING]
> Nunca utilize a política de redirecionamento de consola Olá numa aplicação que é implementada na produção porque isto pode afetar Olá ativação pós-falha de aplicação. *Apenas* utilizá-lo para o desenvolvimento local e fins de depuração.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`pode ser o diretório de trabalho de tooa de saída (stdout e stderr) consola tooredirect utilizados. Esta opção fornece Olá capacidade tooverify se não existirem erros durante a configuração de Olá ou execução da aplicação Olá no cluster do Service Fabric Olá.

`FileRetentionCount`Determina quantos ficheiros são guardados no diretório de trabalho de Olá. Um valor de 5, por exemplo, significa que os ficheiros de registo de Olá para execuções de cinco anterior Olá são armazenados no diretório de trabalho de Olá.

`FileMaxSizeInKb`Especifica o tamanho máximo do Olá Olá dos ficheiros de registo.

Ficheiros de registo são guardados dos diretórios de trabalho do serviço de Olá. toodetermine onde estão localizados, ficheiros de Olá utilizar toodetermine de Service Fabric Explorer, o serviço de Olá do nó está em execução e o diretório de trabalho está a ser utilizado. Este processo é descrito neste artigo.

## <a name="deployment"></a>Implementação
último passo de Olá é demasiado[implementar a sua aplicação](service-fabric-deploy-remove-applications.md). Olá a seguir mostra de script do PowerShell como toodeploy o cluster de desenvolvimento local toohello de aplicação e inicie um novo serviço de Service Fabric.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Comprimir pacote Olá](service-fabric-package-apps.md#compress-a-package) antes de copiar o arquivo de imagens toohello se o pacote Olá é grande ou tem vários ficheiros. Leia mais [aqui](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Um serviço do Service Fabric pode ser implementado em várias "configurações". Por exemplo, pode ser implementado como únicas ou várias instâncias, ou podem ser implementada de forma a que não há uma instância do serviço de Olá em cada nó do cluster do Service Fabric Olá.

Olá `InstanceCount` parâmetro de Olá `New-ServiceFabricService` cmdlet é utilizado toospecify quantas instâncias do serviço de Olá devem ser iniciadas no cluster do Service Fabric Olá. Pode definir Olá `InstanceCount` valor, dependendo do tipo de Olá de aplicação que estiver a implementar. Olá dois os cenários mais comuns são:

* `InstanceCount = "1"`. Neste caso, apenas uma instância do serviço de Olá for implementada num cluster de Olá. Programador de Service Fabric determina o serviço de Olá nó vai toobe implementado em.
* `InstanceCount ="-1"`. Neste caso, uma instância do serviço de Olá é implementada em cada nó do cluster do Service Fabric Olá. resultado de Olá está a ter um (e apenas um) instância do serviço de Olá para cada nó no cluster de Olá.

Esta é uma configuração útil para aplicações de front-end (por exemplo, um ponto final do REST), porque as aplicações de cliente precisam de demasiado "ligar" tooany de nós de Olá num ponto final do Olá cluster toouse Olá. Esta configuração também pode ser utilizada quando, por exemplo, todos os nós do cluster do Service Fabric Olá tooa ligado Balanceador de carga. O tráfego de cliente, em seguida, pode ser distribuído por serviço Olá que está a ser executado em todos os nós no cluster de Olá.

## <a name="check-your-running-application"></a>Verifique a sua aplicação em execução
No Service Fabric Explorer, identifique o nó de olá onde o serviço de Olá está em execução. Neste exemplo, é executada no Nó1:

![Nó onde o serviço está a ser executado](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Se navegar nó toohello e procurar toohello aplicação, consulte as informações de nó essencial Olá, incluindo a localização no disco.

![Localização do disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Se procurar diretório toohello utilizando o Explorador de servidores, pode encontrar o diretório de trabalho de Olá e pasta de registo do serviço de Olá, conforme mostrado na seguinte captura de ecrã de Olá: 

![Localização do registo](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu como toopackage um executável de convidado e implementá-la tooService recursos de infraestrutura. Consulte Olá seguintes artigos para tarefas e informações relacionadas.

* [Exemplo de empacotamento e implementação de um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluindo uma pré-lançamento toohello de ligação da ferramenta de empacotamento de Olá
* [Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Implementar vários executáveis convidados](service-fabric-deploy-multiple-apps.md)
* [Criar a primeira aplicação de Service Fabric com o Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
