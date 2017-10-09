---
title: aaaSet configurar o ambiente de desenvolvimento no Linux | Microsoft Docs
description: "Instalar o runtime Olá e SDK e criar um cluster de desenvolvimento local no Linux. Depois de concluir esta configuração, estará pronto toobuild aplicações."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Preparar o ambiente de desenvolvimento no Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy e execute [aplicações do Azure Service Fabric](service-fabric-application-model.md) no seu computador de desenvolvimento do Linux, instalar o runtime de Olá e SDK comuns. Também pode instalar SDKs opcionais para Java e .NET Core.

## <a name="prerequisites"></a>Pré-requisitos

Olá seguintes versões do sistema operativo é suportada para desenvolvimento:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Atualizar as origens do APT
tooinstall Olá SDK e Olá runtime associados pacote através da ferramenta de linha de comandos Olá apt get, tem primeiro de atualizar as origens de ferramenta de empacotamento avançadas (APT).

1. Abra um terminal.
2. Adicione a lista de origens do Olá Service Fabric repositório tooyour.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Adicionar Olá `dotnet` lista de origens de tooyour do repositório.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Adicionar Olá tooyour APT porta-chaves da chave nova proteção de privacidade Gnu (o GnuPG ou GPG).

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Adicione Olá oficial Docker GPG tooyour chave APT porta-chaves.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Configure o repositório de Docker Olá.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Atualizar o pacote listas com base no Olá recentemente adicionado repositórios.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Instalar e configurar Olá SDK para a configuração de local cluster

Depois de atualizar as origens, pode instalar Olá SDK. Instalar pacote do SDK de Service Fabric de Olá, confirmar instalação Olá e aceitar o contrato de licença toohello.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Olá seguintes comandos automatizar aceitar Olá licença para pacotes de Service Fabric:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Configurar um cluster local
  Se a instalação de Olá for bem-sucedida, deve ser capaz de toostart um cluster local.

  1. Execute script de configuração de cluster Olá.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Abra um browser e aceda demasiado[Service Fabric Explorer](http://localhost:19080/Explorer). Se tiver iniciado o cluster Olá, deverá ver o dashboard de Service Fabric Explorer Olá.

      ![Service Fabric Explorer no Linux][sfx-linux]

  Nesta fase, pode implementar pacotes de aplicações do Service Fabric pré-configurados ou novos com base em contentores convidados ou em executáveis convidados. toobuild novos serviços utilizando Java Olá ou .NET Core SDKs, siga os passos de configuração opcional Olá que são fornecidos nas secções subsequentes.


  > [!NOTE]
  > O Linux não suporta clusters autónomos. Olá preview suporta apenas uma caixa e clusters de múltiplos computadores Linux do Azure.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Configurar Olá CLI de recursos de infraestrutura de serviço

Olá [CLI de recursos de infraestrutura de serviço](service-fabric-cli.md) tem comandos para interagir com entidades do Service Fabric, incluindo clusters e aplicações. Se baseia no python, por isso tenha se toohave python e pip instalado antes de continuar com Olá os seguintes comandos:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Instalar e configurar generators Olá para contentores e executáveis de convidado
O Service Fabric fornece ferramentas estruturais que irão ajudá-lo a criar aplicações do Service Fabric a partir do terminal, através do gerador de modelos Yeoman. Siga os passos de Olá abaixo tooensure que tiver o gerador de modelo yeoman Olá Service Fabric para trabalhar no seu computador.

1. Instalar nodejs e NPM no seu computador

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) no seu computador a partir do NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar o gerador de contentor do serviço Fabric Yeo Olá e gerador de execuatble de convidado de NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Depois de ter instalado Olá acima generators, deve ser capaz de toocreate aplicações com serviços de convidados executável ou contentor executando `yo azuresfguest` ou `yo azuresfcontainer` respetivamente.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Instalar Olá necessários Java artefactos (opcionais, se quiser toouse Olá Java modelos de programação)

serviços do Service Fabric toobuild utilizando Java, certifique-se de que tem 1.8 JDK instalados juntamente com o Gradle que é utilizada para executar tarefas de compilação. Olá seguinte fragmento instala abra JDK 1.8 juntamente com o Gradle. bibliotecas de Service Fabric Java Olá são solicitadas do Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Instalar Olá Eclipse Neon Plug-in (opcional)

Pode instalar Olá Plug-in do Eclipse para o Service Fabric do dentro Olá **IDE Eclipse para programadores de Java**. Pode utilizar aplicações executável do Eclipse toocreate do Service Fabric convidado e aplicações de contentor em aplicações de Java de recursos de infraestrutura de tooService de adição.

1. No Eclipse, certifique-se de que dispõe de mais recente Eclipse Neon e Olá a versão mais recente do Buildship (1.0.17 ou posterior) instalado. Pode verificar as versões de Olá componentes instalados selecionando **ajudar** > **detalhes da instalação**. Pode atualizar Buildship utilizando instruções Olá em [Eclipse Buildship: Eclipse Plug-ins para Gradle][buildship-update].

2. tooinstall Olá, selecione de plug-in do Service Fabric **ajudar** > **instalar novo Software**.

3. No Olá **trabalhar com** caixa, escreva **http://dl.microsoft.com/eclipse**.

4. Clique em **Adicionar**.

    ![página de Software disponíveis Olá][sf-eclipse-plugin]

5. Selecione Olá **ServiceFabric** Plug-in e, em seguida, clique em **seguinte**.

6. Conclua os passos de instalação de Olá e, em seguida, aceite o contrato de licença de utilizador final de Olá.

Se já tiver Olá Service Fabric Eclipse Plug-in instalado, certifique-se de que tem a versão mais recente Olá. Pode verificar selecionando **ajudar** > **detalhes da instalação** e, em seguida, procura na lista de Olá de Service Fabric instalado plug-ins. Se estiver disponível uma versão mais recente, selecione **Atualizar**.

Para obter mais informações, veja [Plug-in do Service Fabric para desenvolvimento de aplicações Java de Eclipse](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Instalar Olá .NET Core SDK (opcional, se pretender que os modelos de programação do .NET Core toouse Olá)
Olá .NET Core SDK fornece bibliotecas Olá e modelos que são necessárias toobuild aos serviços do Service Fabric com .NET Core. Instalar o pacote de SDK do .NET Core Olá seguindo em execução Olá-

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Olá atualização SDK e tempo de execução

tooupdate toohello versão mais recente de Olá SDK e tempo de execução, execute os seguintes comandos de Olá (desselecione Olá SDKs que não pretende):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
binários de Java SDK do Olá tooupdate do Maven, terá de tooupdate Olá versão detalhes binário correspondente do Olá no Olá ``build.gradle`` versão mais recente do ficheiro toopoint toohello. tooknow exatamente onde necessita de versão de Olá tooupdate, pode consultar tooany ``build.gradle`` ficheiro nos exemplos de introdução do Service Fabric [aqui](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Atualizar pacotes de Olá poderá causar a toostop de cluster de desenvolvimento local em execução. Reinicie o seu cluster local após uma atualização ao seguir as instruções de Olá nesta página.

## <a name="next-steps"></a>Passos seguintes

* [Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Plug-in do Service Fabric para Eclipse](service-fabric-get-started-eclipse.md)
* [Create your first CSharp application on Linux (Criar a sua primeira aplicação CSharp no Linux)](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Prepare your development environment on OSX (Preparar o ambiente de desenvolvimento no OSX)](service-fabric-get-started-mac.md)
* [Utilizar Olá CLI de recursos de infraestrutura de serviço toomanage as suas aplicações](service-fabric-application-lifecycle-sfctl.md)
* [Diferenças do Service Fabric no Windows/Linux](service-fabric-linux-windows-differences.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
