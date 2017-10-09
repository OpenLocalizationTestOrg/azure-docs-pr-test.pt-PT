---
title: "aplicações do Azure Service Fabric aaaManage a utilizar o Azure CLI 2.0"
description: "Saiba como toodeploy e remover aplicações a partir de um Azure Service Fabric cluster utilizando o Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Gerir uma aplicação de Service Fabric do Azure utilizando o Azure CLI 2.0

Saiba como toocreate e eliminar aplicações em execução num cluster do Azure Service Fabric.

## <a name="prerequisites"></a>Pré-requisitos

* Instale a CLI do Azure 2.0. Em seguida, selecione o cluster do Service Fabric. Para obter mais informações, consulte [introdução ao Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

* Ter uma Service Fabric aplicação pacote pronto toobe implementado. Para obter mais informações sobre como tooauthor e pacote de aplicação, leia sobre Olá [modelo de aplicação de Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Descrição geral

toodeploy uma nova aplicação, conclua estes passos:

1. Carregar um arquivo de imagem de Service Fabric de toohello de pacote de aplicação.
2. Aprovisione um tipo de aplicação.
3. Especificar e criar uma aplicação.
4. Especifique e criação de serviços.

tooremove uma aplicação existente, conclua estes passos:

1. Elimine aplicação Olá.
2. Olá de não aprovisionamento associadas ao tipo de aplicação.
3. Elimine o conteúdo da loja Olá imagem.

## <a name="deploy-a-new-application"></a>Implementar uma nova aplicação

toodeploy uma nova aplicação Olá concluída seguintes tarefas.

### <a name="upload-a-new-application-package-toohello-image-store"></a>Carregar um arquivo de imagens do toohello de pacote de aplicação nova

Antes de criar uma aplicação, carregue o arquivo de imagens de Service Fabric pacote toohello Olá aplicação. 

Por exemplo, se o pacote de aplicação está a ser Olá `app_package_dir` diretório, Olá utilize os seguintes diretórios de Olá tooupload de comandos:

```azurecli
az sf application upload --path ~/app_package_dir
```

Para pacotes de aplicações grandes, pode especificar Olá `--show-progress` opção toodisplay progresso Olá carregamento Olá.

### <a name="provision-hello-application-type"></a>Tipo de aplicação Olá aprovisionar

Quando o carregamento de Olá estiver concluído, Aprovisione aplicação Olá. tooprovision Olá aplicação Olá utilize os seguintes comandos:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Olá valor para `application-type-build-path` é Olá nome do diretório de olá onde o seu pacote de aplicação que carregou.

### <a name="create-an-application-from-an-application-type"></a>Criar uma aplicação a partir de um tipo de aplicação

Depois de aprovisionar aplicação Olá, utilize Olá tooname de comando a seguir e criar a sua aplicação:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`é o nome de Olá que pretende que toouse para a instância da aplicação Olá. Pode obter os parâmetros adicionais do manifesto de aplicação aprovisionados anteriormente Olá.

nome da aplicação Olá tem de começar com o prefixo de Olá `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Criar serviços para a nova aplicação de Olá

Depois de criar uma aplicação, crie serviços da aplicação Olá. No seguinte exemplo de Olá, vamos criar um novo serviço sem monitorização de estado da nossa aplicação. Serviços de Olá que pode criar a partir de uma aplicação estão definidos num manifesto de serviço no pacote de aplicação aprovisionados anteriormente Olá.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Verifique o estado de funcionamento e implementação de aplicação

tooverify que uma aplicação e do serviço foram implementados com êxito, verifique se estão listados Olá aplicação e do serviço:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

tooverify que o serviço de Olá está em bom estado, utilize semelhante comandos tooretrieve Olá estado de funcionamento do serviço de Olá e aplicação Olá:

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Bom estado de funcionamento dos serviços e aplicações têm um `HealthState` valor `Ok`.

## <a name="remove-an-existing-application"></a>Remover uma aplicação existente

tooremove uma aplicação completa Olá seguintes tarefas.

### <a name="delete-hello-application"></a>Eliminar a aplicação Olá

toodelete Olá aplicação Olá utilize os seguintes comandos:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Anular o aprovisionamento de tipo de aplicação Olá

Depois de eliminar aplicação Olá, pode anular o aprovisionamento de tipo de aplicação Olá se já não precisar dele. tipo de aplicação Olá toounprovision, Olá utilize os seguintes comandos:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

versão de nome e tipo do tipo de Olá tem de corresponder ao nome de Olá e a versão no manifesto de aplicação aprovisionados anteriormente Olá.

### <a name="delete-hello-application-package"></a>Eliminar o pacote de aplicação Olá

Depois de ter anulou o aprovisionamento tipo de aplicação Olá, pode eliminar o pacote de aplicação Olá Olá do arquivo de imagens se já não precisar dele. Eliminação de pacotes de aplicações ajuda-o reclamar espaço em disco. 

pacote de aplicação do Olá toodelete Olá do arquivo de imagens, Olá utilize os seguintes comandos:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`deve ser Olá nome do diretório de Olá que carregou quando criou a aplicação Olá.

## <a name="related-articles"></a>Artigos relacionados

* [Introdução ao Service Fabric e à CLI 2.0 do Azure](service-fabric-azure-cli-2-0.md)
* [Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Introdução ao XPlat CLI do Service Fabric)
