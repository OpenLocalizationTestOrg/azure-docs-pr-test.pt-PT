---
title: "aaaCreate uma aplicação de contentor do Azure Service Fabric no Linux | Microsoft Docs"
description: "Crie a sua primeira aplicação de contentor do Linux no Azure Service Fabric.  Construir uma imagem do Docker com a sua aplicação, push o registo de contentor do Olá imagem tooa, criar e implementar uma aplicação de contentor do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Criar a sua primeira aplicação de contentor do Service Fabric no Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Executar uma aplicação existente num contentor Linux num cluster de Service Fabric não necessita de qualquer aplicação tooyour de alterações. Este artigo explica como criar uma imagem de Docker que contém um Python [Flask](http://flask.pocoo.org/) web de aplicação e implementar a política tooa cluster do Service Fabric.  Também vai partilhar a sua aplicação contentorizada através do [Azure Container Registry](/azure/container-registry/).  Este artigo pressupõe uma compreensão básica do Docker. Pode saber mais sobre o Docker por ler Olá [descrição geral do Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Pré-requisitos
* Um computador de programação com:
  * [SDK e ferramentas do Service Fabric](service-fabric-get-started-linux.md).
  * [Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [CLI do Service Fabric](service-fabric-cli.md)

* Um registo no Azure Container Registry - [Criar um registo de contentor](../container-registry/container-registry-get-started-portal.md) na sua subscrição do Azure. 

## <a name="define-hello-docker-container"></a>Definir o contentor de Docker Olá
Criar uma imagem com base no Olá [imagem Python](https://hub.docker.com/_/python/) localizado no Hub de Docker. 

Defina o contentor do Docker num Dockerfile. Olá Dockerfile contém instruções para configurar o ambiente de Olá no interior do contentor, carregar a aplicação Olá pretende toorun e mapeamento de portas. Olá Dockerfile é toohello entrada Olá `docker build` comando, que cria Olá imagem. 

Criar um diretório vazio e criar o ficheiro de Olá *Dockerfile* (com nenhuma extensão de ficheiro). Adicionar Olá seguir demasiado*Dockerfile* e guarde as alterações:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Olá leitura [Dockerfile referência](https://docs.docker.com/engine/reference/builder/) para obter mais informações.

## <a name="create-a-simple-web-application"></a>Criar uma aplicação Web simples
Crie uma aplicação web Flask que escute na porta 80 e que devolva "Hello World!".  No mesmo diretório de Olá, criar ficheiro de Olá *requirements.txt*.  Adicione o seguinte Olá e guardar as alterações:
```
Flask
```

Também criar Olá *app.py* de ficheiros e adicione Olá seguinte:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a>Compilar Olá imagem
Executar Olá `docker build` comando toocreate Olá imagem, que executa a aplicação web. Abra uma janela do PowerShell e navegue demasiado*c:\temp\helloworldapp*. Execute Olá os seguintes comandos:

```bash
docker build -t helloworldapp .
```

Este comando compilações Olá nova imagem utilizando instruções Olá no seu Dockerfile nomenclatura (-t etiquetagem) imagem Olá "helloworldapp". Criar uma imagem obtém a imagem base Olá para baixo do Docker Hub e cria uma nova imagem que adiciona a sua aplicação em cima da imagem base Olá.  

Após a conclusão do comando de compilação de Olá, execute Olá `docker images` toosee sobre a nova imagem de Olá de comando:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Executar a aplicação Olá localmente
Certifique-se de que a sua aplicação de é executada localmente antes de enviar-registo de contentor Olá.  

Executar a aplicação Olá, mapeamento do contentor do seu computador, porta 4000 toohello expostos a porta 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*nome* fornece toohello um nome com o contentor (em vez do ID de contentor Olá).

Ligar toohello com o contentor.  Abra um browser apontar toohello endereço IP devolvido na porta 4000, por exemplo "http://localhost:4000". Deverá ver Olá cabeçalho "Olá mundo!" apresentar num browser de Olá.

![Hello World!][hello-world]

toostop o contentor, execute:

```bash
docker stop my-web-site
```

Elimine o contentor de Olá a partir do seu computador de desenvolvimento:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Registo de contentor do push Olá imagem toohello
Depois de verificar que a aplicação Olá é executada no Docker, emitir o registo de tooyour Olá imagem no registo de contentor do Azure.

Executar `docker login` toolog no registo de contentor tooyour com seu [credenciais do registo](../container-registry/container-registry-authentication.md).

Olá seguinte exemplo, passa Olá ID e palavra-passe de um Azure Active Directory [principal de serviço](../active-directory/active-directory-application-objects.md). Por exemplo, poderá ter atribuído um registo de principal tooyour de serviço para um cenário de automatização.  Em alternativa, pode iniciar sessão com o nome de utilizador e a palavra-passe do registo.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Olá comando seguinte cria uma etiqueta, ou alias, da imagem de Olá, com um registo de tooyour caminho completamente qualificado. Neste exemplo locais Olá imagem no Olá `samples` espaço de nomes tooavoid clutter na raiz de Olá do registo de Olá.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registo de contentor do push Olá imagem tooyour:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>O pacote de imagem de Docker Olá com Yeoman
Olá para Linux SDK de Service Fabric inclui um [Yeoman](http://yeoman.io/) gerador que torna mais fácil toocreate a aplicação e adicionar uma imagem de contentor. Vamos utilizar Yeoman toocreate chamada de uma aplicação com um único contentor de Docker *SimpleContainerApp*.

toocreate uma aplicação de contentor do Service Fabric, abra uma janela de terminal e execute `yo azuresfcontainer`.  

Dê um nome à aplicação (por exemplo, “mycontainer”). 

Fornecer Olá URL para a imagem de contentor Olá no registo de contentor (por exemplo, ""). 

Esta imagem tem uma carga de trabalho ponto de entrada definido, por isso, tem de tooexplicitly especifique comandos de entrada (executados no interior do contentor de Olá, que irá manter o contentor de Olá executar após o arranque de comandos). 

Especifique uma contagem de instâncias de "1".

![Gerador Yeoman do Service Fabric para contentores][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Configurar o mapeamento de portas e a autenticação do repositório de contentores
O seu serviço contentorizado precisa de um ponto final para comunicação.  Agora adicione Olá protocolo, porta e tipo tooan `Endpoint` no ficheiro de ServiceManifest.xml Olá. Para este artigo, o serviço de Olá de escuta na porta 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Fornecer Olá `UriScheme` automaticamente regista Olá ponto final de contentor com Olá Service Fabric Naming service para deteção. Um ficheiro de exemplo ServiceManifest.xml completo é fornecido no fim de Olá deste artigo. 

Configurar o mapeamento de porta de anfitrião de porta do contentor de Olá, especificando um `PortBinding` política no `ContainerHostPolicies` do ficheiro de ApplicationManifest.xml Olá.  Para este artigo, `ContainerPort` é 80 (contentor de Olá expõe a porta 80, como especificado no Olá Dockerfile) e `EndpointRef` é "myserviceTypeEndpoint" (Olá ponto final definido no manifesto do serviço de Olá).  Os pedidos recebidos toohello serviço na porta 4000 estão mapeados tooport 80 no contentor de Olá.  Se o contentor tem tooauthenticate com um repositório privado, em seguida, adicione `RepositoryCredentials`.  Para este artigo, adicione nome Olá da conta e palavra-passe para Olá myregistry.azurecr.io contentor de registo. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Compilação e pacote de aplicação de Service Fabric Olá
modelos de serviço Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que pode utilizar a aplicação Olá toobuild Olá terminal. toobuild e pacote Olá aplicação, execute Olá seguinte:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Implementar a aplicação Olá
Uma vez que é criada a aplicação Olá, pode implementá-la toohello cluster local com Olá CLI de recursos de infraestrutura de serviço.

Ligue o cluster do Service Fabric local toohello.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Olá utilize instalar o script fornecido no Olá modelo toocopy aplicação Olá arquivo de imagens do cluster toohello do pacote, registar o tipo de aplicação Olá e criar uma instância da aplicação Olá.

```bash
./install.sh
```

Abra um browser e navegue tooService Explorador de recursos de infraestrutura em http://localhost:19080/Explorer (substituir localhost com Olá IP privado de Olá VM se utilizar Vagrant no Mac OS X). Expanda o nó de aplicações de Olá e observe que não existe agora uma entrada para o tipo de aplicação e outro para Olá primeira instância desse tipo.

Ligar toohello com o contentor.  Abra um browser apontar toohello endereço IP devolvido na porta 4000, por exemplo "http://localhost:4000". Deverá ver Olá cabeçalho "Olá mundo!" apresentar num browser de Olá.

![Hello World!][hello-world]

## <a name="clean-up"></a>Limpeza
Utilizar script de desinstalação de Olá fornecido na instância da aplicação de Olá modelo toodelete Olá do cluster de desenvolvimento local Olá e anular o registo do tipo de aplicação Olá.

```bash
./uninstall.sh
```

Depois de push o registo de contentor do Olá imagem toohello pode eliminar imagem local Olá do seu computador de desenvolvimento:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Exemplo completo da aplicação do Service Fabric e dos manifestos do serviço
Seguem-se o serviço concluído Olá e os manifestos da aplicação utilizados neste artigo.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Adicionar mais serviços tooan aplicação existente

executar a aplicação de tooan de serviço de contentor outro já criada utilizando yeoman, tooadd Olá os seguintes passos:

1. Alterar a raiz de toohello do diretório da aplicação existente Olá.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é aplicação Olá criada pelo Yeoman.
2. Execute `yo azuresfcontainer:AddService`

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a>Configurar o intervalo de tempo antes do contentor ser forçado a terminar

Pode configurar um intervalo de tempo para Olá runtime toowait antes do contentor de Olá é removida após hello eliminação do serviço (ou um nó de tooanother mover) foi iniciado. Intervalo de tempo de Olá configurar envia Olá `docker stop <time in seconds>` contentor toohello de comando.   Para obter mais detalhes, veja [paragem do docker](https://docs.docker.com/engine/reference/commandline/stop/). toowait de intervalo de tempo de Olá especificado nas Olá `Hosting` secção. Olá fragmento de manifesto do cluster a seguir mostra como tooset Olá Aguarde intervalo:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Olá intervalo de tempo predefinido estiver definido too10 segundos. Uma vez que esta configuração for dinâmica, uma configuração atualizar-se apenas no tempo limite do Olá cluster atualizações Olá. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Configurar Olá runtime tooremove imagens do contentor não utilizadas

Pode configurar tooremove de cluster do Service Fabric Olá imagens do contentor não utilizado a partir do nó de Olá. Esta configuração permite toobe de espaço em disco recaptured se estiverem presentes no nó de Olá demasiados de contentor de imagens.  tooenable desta funcionalidade, a atualização Olá `Hosting` secção manifesto do cluster Olá conforme mostrado no Olá seguinte fragmento: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Para imagens que não devem ser eliminadas, pode especificá-las em Olá `ContainerImagesToSkip` parâmetro. 


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre como executar [contentores no Service Fabric](service-fabric-containers-overview.md).
* Olá leitura [implementar uma aplicação .NET num contentor](service-fabric-host-app-in-a-container.md) tutorial.
* Saiba mais sobre Olá Service Fabric [ciclo de vida de aplicação](service-fabric-application-lifecycle.md).
* Olá finalizar [exemplos de código do contentor de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) no GitHub.

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
