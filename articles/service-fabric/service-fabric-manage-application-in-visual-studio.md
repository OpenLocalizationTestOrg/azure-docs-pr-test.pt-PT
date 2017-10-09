---
title: "aaaManage as suas aplicações no Visual Studio | Microsoft Docs"
description: "Utilizar o Visual Studio toocreate, desenvolver, pacote, implementar e depurar os seus serviços e aplicações de Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Utilize a escrita de toosimplify do Visual Studio e a gestão das suas aplicações de Service Fabric
Pode gerir as suas aplicações do Azure Service Fabric e serviços através do Visual Studio. Assim que tiver [configurar o ambiente de desenvolvimento](service-fabric-get-started.md), pode utilizar as aplicações de Service Fabric do Visual Studio toocreate, adicionar serviços, ou o pacote, registar e implementar aplicações no seu cluster de desenvolvimento local.

## <a name="deploy-your-service-fabric-application"></a>Implementar a aplicação de Service Fabric
Por predefinição, a implementar uma aplicação combina Olá os seguintes passos para uma operação simple:

1. Criar o pacote de aplicação Olá
2. Carregamento Olá pacote toohello imagem loja de aplicações
3. Registar o tipo de aplicação Olá
4. Remover quaisquer instâncias de aplicações em execução
5. Criar uma instância de aplicação

No Visual Studio, premindo **F5** implementa a aplicação e anexar instâncias da aplicação Olá depurador tooall. Pode utilizar **Ctrl + F5** toodeploy uma aplicação sem depuração, ou pode publicar tooa local ou perfil de publicação de clusters remotos utilizando Olá. Para obter mais informações, consulte [publicar um cluster de remoto tooa aplicação utilizando o Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Modo de depuração de aplicações
Visual Studio fornecem uma propriedade denominada **modo de depuração da aplicação**, que controla a forma como pretende que a implementação de aplicação do Visual estúdios toohandle como parte de depuração.

#### <a name="tooset-hello-application-debug-mode-property"></a>Olá tooset propriedade do modo de depuração de aplicações
1. No Olá Service Fabric aplicação do projeto (*.sfproj) menu de atalho, escolha **propriedades** (ou prima Olá **F4** chave).
2. No Olá **propriedades** janela, conjunto Olá **modo de depuração da aplicação** propriedade.

![Definir a propriedade de modo de depuração de aplicações][debugmodeproperty]

#### <a name="application-debug-modes"></a>Modos de depuração de aplicações

1. **Atualizar aplicação** este modo permite-lhe alterar tooquickly e depurar o seu código e suporta a edição de ficheiros estáticos web durante a depuração. Este modo só funciona se o cluster de desenvolvimento local está a ser [1 nó modo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Remover aplicação** causas Olá toobe aplicação removido quando termina a sessão de depuração Olá.
3. **Auto atualização** aplicação Olá continua toorun quando termina a sessão de depuração Olá. Olá próxima sessão de depuração irão tratar implementação Olá como uma atualização. processo de atualização de Olá preserva todos os dados que introduziu numa sessão de depuração anterior.
4. **Manter aplicações** Olá mantém de aplicação em execução no cluster de Olá quando hello terminar sessão de depuração. Olá início do Olá próxima sessão de depuração, a aplicação Olá será removida.

Para **automática atualizar** os dados são preservados aplicando Olá atualização as capacidades das aplicações de Service Fabric. Para obter mais informações sobre como atualizar aplicações e como pode executar uma atualização num ambiente real, consulte [atualização da aplicação de Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Adicionar uma aplicação de Service Fabric de tooyour de serviço
Pode adicionar novos serviços o tooyour aplicação tooextend sua funcionalidade.  tooensure que o serviço de Olá está incluído no seu pacote de aplicação, adicione o serviço de Olá através de Olá **novo serviço de recursos de infraestrutura...**  item de menu.

![Adicionar um novo serviço de Service Fabric][newservice]

Selecione uma aplicação de tooyour tooadd de tipo de projeto de Service Fabric e especifique um nome para o serviço de Olá.  Consulte [escolher uma estrutura para o seu serviço](service-fabric-choose-framework.md) toohelp decidir qual serviço escreva toouse.

![Selecionar uma aplicação do Service Fabric serviço projeto tipo tooadd tooyour][addserviceproject]

é adicionado o novo serviço de Olá tooyour solução e pacote de aplicação existente. Olá referências de serviço e uma instância de serviço predefinido será adicionado toohello o manifesto da aplicação, que provocou toobe de serviço Olá criado e iniciado Olá próxima vez que implementa a aplicação Olá.

![o manifesto da aplicação tooyour está a ser adicionado por Olá novo serviço][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Pacote da aplicação de Service Fabric
aplicação de Olá toodeploy e o cluster de tooa serviços, terá de toocreate um pacote de aplicação.  pacote de Olá organiza manifesto da aplicação Olá, manifestos de serviço e outros ficheiros necessários num esquema específico.  Visual Studio configura e gere Olá pacote na pasta do projeto de aplicação Olá, no diretório do Olá 'pkg'.  Ao clicar em **pacote** de Olá **aplicação** cria do menu de contexto ou atualizações Olá pacote de aplicação.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Remover aplicações e tipos de aplicação utilizando o Explorador de nuvem
Pode efetuar operações de gestão de cluster básico a partir do Visual Studio através do Explorador de nuvem, o que pode iniciar a partir de Olá **vista** menu. Por exemplo, pode eliminar as aplicações e anular o aprovisionamento de tipos de aplicações em clusters locais ou remotos.

![Remover uma aplicação][removeapplication]

> [!TIP]
> Para mais rica funcionalidades de gestão de cluster, consulte [visualizar o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passos seguintes
* [Modelo de aplicação de Service Fabric](service-fabric-application-model.md)
* [Implementação de aplicação de Service Fabric](service-fabric-deploy-remove-applications.md)
* [Gerir aplicações parâmetros para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md)
* [Depurar a aplicação de Service Fabric](service-fabric-debugging-your-application.md)
* [Visualizar o cluster utilizando o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png