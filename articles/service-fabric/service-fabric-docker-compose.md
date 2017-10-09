---
title: "aaaAzure Docker Compose pré-visualização do serviço de recursos de infraestrutura"
description: "Azure Service Fabric aceita o Docker Compose toomake de formato-contentores existente mais fácil do tooorchestrate, utilizando o Service Fabric. Este suporte está atualmente em pré-visualização."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Suporte de aplicações do docker Compose no Service Fabric do Azure (pré-visualização)

Docker utiliza Olá [docker-Compose.yml](https://docs.docker.com/compose) ficheiro para definir o contentor várias aplicações. toomake-lo mais fácil para os clientes familiarizados com o Docker tooorchestrate contentor as aplicações existentes no Azure Service Fabric, incluímos suporte de pré-visualização para o Docker Compose nativamente na plataforma de Olá. Service Fabric pode aceitar a versão 3 e posterior do `docker-compose.yml` ficheiros. 

Porque este suporte está em pré-visualização, apenas um subconjunto de diretivas de Compose é suportado. Por exemplo, as atualizações de aplicações não são suportadas. No entanto, pode sempre remover e implementar aplicações em vez de atualização-los.

toouse esta pré-visualização, criar o cluster com a versão 5.7 ou superior do tempo de execução do Olá Service Fabric através de Olá portal do Azure, juntamente com Olá correspondente SDK. 

> [!NOTE]
> Esta funcionalidade está em pré-visualização e não é suportada na produção.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Implementar um ficheiro de Docker Compose no Service Fabric

Olá os comandos seguintes criam uma aplicação de Service Fabric (com o nome `fabric:/TestContainerApp` no Olá anterior exemplo), que pode monitorizar e gerir como qualquer outra aplicação de Service Fabric. Pode utilizar o nome de aplicação especificada Olá para consultas de estado de funcionamento.

### <a name="use-powershell"></a>Utilizar o PowerShell

Crie uma aplicação de Service Fabric compor a partir de um ficheiro docker-Compose.yml executando o seguinte comando do PowerShell de Olá:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`e `RegistryPassword` Consulte nome de utilizador de registo de contentor de toohello e a palavra-passe. Após concluir aplicação Olá, pode verificar o estado utilizando Olá os seguintes comandos:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete Olá Compose aplicação através do PowerShell, utilize Olá os seguintes comandos:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Utilizar a CLI do Azure Service Fabric (sfctl)

Em alternativa, pode utilizar Olá os seguintes comandos da CLI de recursos de infraestrutura de serviço:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Depois de criar aplicação Olá, pode verificar o estado utilizando Olá os seguintes comandos:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Olá toodelete Compose aplicação, utilize Olá os seguintes comandos:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Diretivas de Compose suportadas

Esta pré-visualização suporta um subconjunto das opções de configuração de Olá Olá Compose versão 3 o formato, incluindo Olá primitivos os seguintes:

* Serviços > Implementar > réplicas
* Serviços > Implementar > colocação > restrições
* Serviços > Implementar > recursos > limites
    * -cpu partilhas
    * -memória
    * -memória-troca
* Serviços > comandos
* Serviços > ambiente
* Serviços > portas
* Serviços > imagem
* Serviços > isolamento (apenas para o Windows)
* Serviços > registo > controladores
* Serviços > registo > controladores > Opções
* Volume & implementar > Volume

Configurar o cluster Olá para impor limites de recursos, conforme descrito em [governação de recursos do Service Fabric](service-fabric-resource-governance.md). Todos os outras diretivas Docker Compose não são suportadas para esta pré-visualização.

## <a name="servicednsname-computation"></a>Cálculo ServiceDnsName

Se o nome de serviço Olá que especificou num ficheiro Compose é um nome de domínio completamente qualificado (ou seja, contém um ponto [.]), o nome DNS Olá registado pelo Service Fabric é `<ServiceName>` (incluindo o ponto de Olá). Caso contrário, cada segmento de caminho no nome da aplicação Olá torna-se uma etiqueta de domínio no nome de DNS do serviço Olá, com Olá primeiro segmento de caminho tornar-se a etiqueta de Olá de domínio de nível superior.

Por exemplo, se Olá especificado o nome da aplicação é `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` seria Olá nome DNS registado.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Diferenças entre Compose (definição de instância) e o modelo de aplicação de Service Fabric (definição de tipo)

Um ficheiro docker-Compose.yml descreve um conjunto implementável de contentores, incluindo as respetivas propriedades e configurações.
Por exemplo, o ficheiro de Olá pode conter variáveis de ambiente e portas. Também pode especificar parâmetros de implementação, tais como restrições de posicionamento, limites de recursos e nomes DNS no ficheiro de docker-Compose.yml Olá.

Olá [modelo de aplicação de Service Fabric](service-fabric-application-model.md) Olá, utiliza tipos de serviço e tipos de aplicações, onde pode ter várias instâncias da aplicação do mesmo tipo. Por exemplo, pode ter uma instância da aplicação por cliente. Este modelo baseado no tipo suporta várias versões do Olá mesmo tipo de aplicação que está registado com Olá tempo de execução.

Por exemplo, cliente um pode ter uma aplicação com instâncias com tipo 1.0 do AppTypeA e cliente B pode ter outra aplicação instanciada com Olá mesmo tipo e versão. Definir os tipos de aplicação Olá em manifestos da aplicação Olá e especificar parâmetros de nome e a implementação da aplicação Olá quando criar aplicação Olá.

Embora este modelo oferece flexibilidade, iremos também estiver a planear toosupport um modelo de implementação mais simples, instância baseada em onde tipos são implícitos de ficheiro de manifesto Olá. Neste modelo, cada aplicação obtém o seu próprio manifesto independente. Iremos são pré-visualização deste esforço adicionando suporte para docker-Compose.yml, que é um formato de implementação com base na instância.

## <a name="next-steps"></a>Passos seguintes

* Ler sobre Olá [modelo de aplicação de Service Fabric](service-fabric-application-model.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
