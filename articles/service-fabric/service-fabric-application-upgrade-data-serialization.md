---
title: "Atualização da aplicação: serialização de dados | Microsoft Docs"
description: "Melhores práticas para a serialização de dados e a forma como afeta a atualizações graduais de aplicação."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Como a serialização de dados afeta uma atualização da aplicação
Num [a atualização da aplicação](service-fabric-application-upgrade.md), atualização Olá é aplicado tooa subconjunto de nós, um domínio de atualização a uma hora. Durante este processo, alguns domínios de atualização são numa versão mais recente do Olá da sua aplicação e alguns domínios de atualização são numa versão mais antiga do Olá da sua aplicação. Durante a implementação de Olá, versão nova do Olá da sua aplicação tem de ser capaz de tooread versão antiga do Olá dos seus dados e versão antiga do Olá da sua aplicação tem de ser capaz de tooread Olá nova versão, dos seus dados. Formato de dados de Olá não esteja com versões anteriores e reencaminhar atualização Olá compatível, podem falhar, worse, dados ou pode ser perdido ou corrompido. Este artigo descreve o que constitui o formato de dados e oferece melhores práticas para se certificar de que os dados estão a reencaminhar e com versões anteriores compatível.

## <a name="what-makes-up-your-data-format"></a>O que constitui o formato de dados?
No Azure Service Fabric, os dados de Olá que é persistente e replicados provém das classes de c#. Para aplicações que utilizam [coleções fiável](service-fabric-reliable-services-reliable-collections.md), que dados são objetos Olá dicionários fiável Olá e pelas filas. Para aplicações que utilizam [Reliable Actors](service-fabric-reliable-actors-introduction.md), ou seja Olá fazer uma cópia de estado de ator Olá. Estas classes c# tem de ser serializáveis toobe persistência e replicação. Por conseguinte, o formato dos dados Olá é definido por campos de Olá e propriedades que estão a serializada, bem como a forma como estas são serializadas. Por exemplo, num `IReliableDictionary<int, MyClass>` dados Olá são um serializados `int` e um serializados `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Código de alterações que resultam numa alteração de formato de dados
Uma vez que o formato dos dados Olá é determinado pelo c# classes, classes de toohello de alterações que podem causar uma alteração de formato de dados. Deve ter cuidado tooensure que pode processar uma atualização sem interrupção dados Olá formatar a alteração. Exemplos que podem fazer com que as alterações de formato de dados:

* Adicionar ou remover propriedades ou campos
* Mudar o nome de campos ou propriedades
* A alteração Olá tipos de campos ou propriedades
* Alterar o nome da classe de Olá ou espaço de nomes

### <a name="data-contract-as-hello-default-serializer"></a>Contrato de dados como Olá serializador predefinido
o serializador de Olá é, geralmente, responsável pela leitura de dados de Olá e anular a serialização na versão atual do Olá, mesmo se dados Olá são mais antigo na ou *mais recente* versão. Olá serializador predefinido é Olá [serializador de contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx), que tem regras de controlo de versões bem definidos. Coleções fiáveis permitem Olá serializador toobe substituído, mas Reliable Actors atualmente não compatíveis. o serializador de dados de Olá desempenha um papel importante para ativar atualizações graduais. o serializador de contrato de dados de Olá é serializador Olá que recomendamos para aplicações de Service Fabric.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Como o formato dos dados Olá afeta uma atualização sem interrupção
Durante uma atualização sem interrupção, existem dois cenários principais onde o serializador de Olá poderá encontrar mais antigo ou *mais recente* versão dos dados:

1. Depois de um nó é atualizado e inicia a cópia de segurança, serializador novo Olá irá carregar os dados de Olá que foi toodisk persistente por versão antigo Olá.
2. Durante a atualização de Olá, cluster Olá irá conter uma combinação de versões de antigos e novos Olá do seu código. Uma vez que as réplicas podem ser colocadas em domínios de atualização diferentes e réplicas enviar dados tooeach outras hello novo e/ou antigo versão dos dados pode ser encontrado com a versão nova e/ou antigo Olá do seu serializador.

> [!NOTE]
> Olá "nova versão" e "versão antiga" aqui Consulte toohello versão do seu código que está em execução. Olá "novo serializador" refere-se o código de serializador toohello que está a executar a versão nova do Olá da sua aplicação. Olá "dados novos" refere-se toohello serializado c# classe da nova versão de Olá da sua aplicação.
> 
> 

Olá duas versões de código e o formato de dados tem de ser direta e com versões anteriores compatível. Se não forem compatíveis, Olá a atualização poderá falhar ou os dados poderão perder-se. Olá, a atualização poderá falhar porque o código de Olá ou serializador pode acionar exceções ou uma falha quando encontra Olá outra versão. Dados poderão perder-se se, por exemplo, foi adicionada uma nova propriedade mas serializador antigo Olá elimina-lo durante a desserialização.

Contrato de dados é Olá recomendado solução para se certificar de que os seus dados são compatíveis. Tem regras de controlo de versões definida especificamente para adicionar, remover e alteração dos campos. Também tem suporte para lidar com campos desconhecidos, hooking no processo de serialização e a anulação da serialização de Olá e lidar com a herança de classe. Para obter mais informações, consulte [através de contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Passos seguintes
[Atualizar a aplicação utilizando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta-o através de uma atualização da aplicação com o Visual Studio.

[Atualizar a sua aplicação através do Powershell](service-fabric-application-upgrade-tutorial-powershell.md) orienta-o através de uma atualização da aplicação através do PowerShell.

Controlar a forma como a aplicação atualiza utilizando [atualizar parâmetros](service-fabric-application-upgrade-parameters.md).

Saiba como toouse avançada funcionalidade ao atualizar a sua aplicação ao referir-se demasiado[tópicos avançados](service-fabric-application-upgrade-advanced.md).

Resolva problemas comuns nas atualizações de aplicações ao referir-se passos toohello [resolução de problemas de atualizações de aplicação ](service-fabric-application-upgrade-troubleshooting.md).

