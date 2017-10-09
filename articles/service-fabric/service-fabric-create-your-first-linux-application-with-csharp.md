---
title: "aaaCreate sua primeira aplicação do Azure micro-serviços no Linux utilizando c# | Microsoft Docs"
description: "Criar e implementar uma aplicação do Service Fabric com C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Criar a sua primeira aplicação do Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

O Service Fabric disponibiliza SDKs para criar serviços no Linux em .NET Core e Java. Neste tutorial, vamos ver como toocreate uma aplicação para Linux e compilação um serviço com a c# (.NET Core).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, certifique-se de que [configurou o seu ambiente de desenvolvimento do Linux](service-fabric-get-started-linux.md). Se estiver a utilizar o Mac OS X, pode [configurar um ambiente de uma caixa do Linux numa máquina virtual com Vagrant](service-fabric-get-started-mac.md).

Também convém tooinstall Olá [CLI de recursos de infraestrutura de serviço](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Instalar e configurar generators Olá para CSharp
O Service Fabric fornece ferramentas estruturais que irão ajudá-lo a criar uma aplicação CSharp do Service Fabric a partir do terminal, através do gerador de modelos Yeoman. Siga os passos de Olá abaixo tooensure que tiver o gerador de modelo yeoman Olá Service Fabric para CSharp trabalhar no seu computador.
1. Instalar nodejs e NPM no seu computador

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) no seu computador a partir do NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar o gerador de aplicação de Service Fabric Yeo Java Olá de NPM

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Criar aplicação Olá
Uma aplicação de Service Fabric pode conter um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade da aplicação Olá. Olá Service Fabric [Yeoman](http://yeoman.io/) gerador do CSharp, que instalou no último passo, torna mais fácil toocreate seu próprio serviço e tooadd mais mais tarde. Vamos utilizar Yeoman toocreate uma aplicação com um único serviço.

1. Num terminal, escreva Olá toostart comando Criar andaime Olá os seguintes:`yo azuresfcsharp`
2. Dê um nome à aplicação.
3. Escolha o tipo de Olá do seu primeiro serviço e nome. Para efeitos de Olá deste tutorial, vamos escolher um serviço de Atores fiável.

   ![Gerador Yeoman do Service Fabric para C#][sf-yeoman]

> [!NOTE]
> Para obter mais informações sobre as opções de Olá, consulte [descrição geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Criar aplicação Olá
os modelos de serviço Fabric Yeoman Olá incluem um script de compilação que pode utilizar a aplicação de Olá toobuild de Olá terminal (após navegar toohello pasta da aplicação).

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a>Implementar a aplicação Olá

Uma vez que é criada a aplicação Olá, pode implementá-la toohello cluster local.

1. Ligue o cluster do Service Fabric local toohello.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Script de instalação de execução Olá fornecida Olá modelo toocopy Olá arquivo de imagens do cluster de aplicação, pacote toohello, registar o tipo de aplicação Olá e criar uma instância da aplicação Olá.

    ```bash
    ./install.sh
    ```

Implementação da aplicação Olá incorporado é Olá mesmo como qualquer outra aplicação de Service Fabric. Consulte a documentação de Olá no [gerir uma aplicação de Service Fabric com Olá CLI de recursos de infraestrutura de serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.

Comandos de toothese parâmetros podem ser encontrados em manifestos Olá gerado no interior do pacote de aplicação Olá.

Assim que tiver sido implementada a aplicação Olá, abra um browser e navegue para [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer). Em seguida, expanda Olá **aplicações** nós e tenha em atenção que está agora uma entrada para o tipo de aplicação e outro para Olá primeira instância desse tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Iniciar o cliente de teste de Olá e efetuar uma ativação pós-falha
Os projetos de ator não fazem nada só por si. Necessitam de outro toosend de serviço ou cliente mensagens-las. modelo de ator Olá inclui um script de teste simples que pode utilizar toointeract com o serviço de atores Olá.

1. Execute script de Olá utilizando Olá veja utilitário toosee Olá saída do serviço de atores Olá.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. No Service Fabric Explorer, localize o nó que aloja a réplica primária do Olá para o serviço de atores Olá. Olá captura de ecrã abaixo, é nó 3.

    ![Localizar a réplica primária Olá no Service Fabric Explorer][sfx-primary]
3. Clique com o nó de Olá encontrado no passo anterior Olá, em seguida, selecione **desativar (reiniciar)** no menu de Olá ações. Esta ação reinicia um nó do cluster local forçar uma réplica secundária de ativação pós-falha tooa em execução no outro nó. Como efetuar esta ação, paga saída de toohello atenção do cliente de teste de Olá e tenha em atenção que contador Olá continua tooincrement, apesar de ativação pós-falha de Olá.

## <a name="adding-more-services-tooan-existing-application"></a>Adicionar mais serviços tooan aplicação existente

tooadd outra tooan aplicação de serviço já criadas utilizando `yo`, efetuar Olá os seguintes passos:
1. Alterar a raiz de toohello do diretório da aplicação existente Olá.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é aplicação Olá criada pelo Yeoman.
2. Execute `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>Migrar do project.json too.csproj
1. Executar 'dotnet migrar' no diretório de raiz do projeto irá migrar todos os formato de toocsproj de project.json Olá.
2. Projeto de Olá de atualização em conformidade referencia toocsproj ficheiros nos ficheiros de projeto.
3. Atualize ficheiros toocsproj nomes de ficheiro de projeto de Olá no build.sh.

## <a name="next-steps"></a>Passos seguintes

* [Saiba mais sobre os Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interagir com clusters do Service Fabric através da Olá CLI de recursos de infraestrutura de serviço](service-fabric-cli.md)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
