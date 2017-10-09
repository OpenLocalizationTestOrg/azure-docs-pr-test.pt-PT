---
title: "aaaSet a integração contínua para micro-serviços do Azure | Microsoft Docs"
description: "Obter uma descrição geral de como tooset integração contínua e implementação para uma aplicação de Service Fabric através dos serviços de equipa do Visual Studio (VSTS)."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Configurar a integração contínua de recursos de infraestrutura de serviço e a implementação com o Visual Studio Team Services
Este artigo descreve os passos de Olá tooset integração contínua e implementação para uma aplicação de Service Fabric do Azure utilizando os serviços de equipa do Visual Studio (VSTS).

Este documento reflete procedimento atual Olá e é toochange esperado ao longo do tempo.

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado, siga estes passos:

1. Certifique-se de que tem acesso tooa Team Services conta ou [criar um](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) por si.
2. Certifique-se de que tem o projeto de equipa de serviços da equipa do acesso tooa ou [criar um](https://www.visualstudio.com/docs/setup-admin/create-team-project) por si.
3. Certifique-se de que tem um toowhich de cluster do Service Fabric pode implementar a aplicação ou crie uma utilizando Olá [portal do Azure](service-fabric-cluster-creation-via-portal.md), um [modelo Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), ou [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Certifique-se de que já criou um projeto de aplicação de recursos de infraestrutura de serviço (.sfproj). Tem de ter um projeto que foi criado ou atualizado com o serviço de recursos de infraestrutura SDK 2.1 ou superior (o ficheiro de .sfproj Olá deve conter um valor de propriedade ProjectVersion de 1.1 ou superior).

> [!NOTE]
> Agentes de compilação personalizado já não são necessários. Equipa de serviços alojados agentes agora vêm pré-instaladas com software de gestão de cluster do Service Fabric, permitindo a implementação das suas aplicações diretamente a partir desses agentes.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Configurar e partilhe os ficheiros de origem
Olá primeira coisa que pretende é toodo preparar um perfil de publicação para utilização pelo processo de implementação de Olá que é executada num Team Services.  perfil de publicação de Olá deve ser o cluster de Olá tootarget configurado que já preparou anteriormente:

1. Escolha um perfil de publicação dentro do seu projeto de aplicação que pretende que toouse ao fluxo de trabalho de integração contínua. Siga Olá [publicar instruções](service-fabric-publish-app-remote-cluster.md) sobre toopublish um cluster remoto de tooa de aplicação. Não, na verdade, precisa de toopublish a aplicação apesar. Pode clicar em Olá **guardar** hiperligação no Olá caixa de diálogo Publicar depois de configurar devidamente coisas.
2. Se pretender que o seu toobe aplicação atualizado para cada implementação que ocorre dentro do Team Services, pretende tooconfigure Olá publicar atualização tooenable de perfil. Na caixa de diálogo utilizada mesmo publicar no passo 1 de Olá, certifique-se que Olá **Olá atualização aplicação** caixa de verificação está selecionada.  Saiba mais sobre [configurar definições de atualização adicionais](service-fabric-visualstudio-configure-upgrade.md). Clique em Olá **guardar** hyperlink toosave Olá definições toohello perfil de publicação.
3. Certifique-se de que tenha as alterações foram guardadas toohello publicar perfil e cancelar Olá caixa de diálogo Publicar.
4. Agora está na altura demasiado[partilhar os ficheiros de origem do projeto de aplicação](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) com a equipa de serviços. Depois dos ficheiros de origem estão acessíveis no Team Services, agora pode mover no passo seguinte toohello gerar compilações. 

## <a name="create-a-build-definition"></a>Criar uma definição de compilação
Uma definição de compilação Team Services descreve um fluxo de trabalho é composto por um conjunto de passos de compilação que são executados sequencialmente. objetivo de Olá da definição de compilação de Olá que está a criar é tooproduce um pacote de aplicação de Service Fabric e outros objetos, que podem ser utilizados toodeploy Olá aplicação. Saiba mais sobre os serviços da equipa [definições de compilação](https://www.visualstudio.com/docs/build/define/create).

### <a name="create-a-definition-from-hello-build-template"></a>Criar uma definição a partir do modelo de compilação de Olá
1. Abra o projeto de equipa no Visual Studio Team Services.
2. Selecione Olá **criar** separador.
3. Verde Olá selecione  **+**  assinar toocreate uma nova definição de compilação.
4. Olá caixa de diálogo que se abre, selecione **aplicação do Azure Service Fabric** dentro Olá **criar** categoria de modelo.
5. Selecione **seguinte**.
6. Selecione o repositório de Olá e ramo associada com a sua aplicação de Service Fabric.
7. Selecione a fila de agente Olá desejar toouse. Agentes alojados são suportados.
8. Selecione **Criar**.
9. Guardar a definição de compilação de Olá e forneça um nome.
10. Olá parágrafo seguinte é uma descrição dos passos de compilação de Olá gerado pelo modelo de Olá:

| Passo de compilação | Descrição |
| --- | --- |
| Restauro do NuGet |Restaura os pacotes de NuGet Olá para a solução de Olá. |
| Compilar solução \*. sln |Baseia-se a solução completa de Olá. |
| Compilar solução \*.sfproj |Gera o pacote de aplicação de Service Fabric Olá que é utilizado toodeploy Olá aplicação. localização de pacote de aplicação Olá é toobe especificada dentro do diretório de artefacto da compilação Olá. |
| Atualizar versões de aplicação do Service Fabric |Atualiza os valores da versão Olá contidos no tooallow de ficheiros de manifesto do pacote de aplicação Olá para suporte de atualização. Consulte Olá [página de documentação de tarefas](https://go.microsoft.com/fwlink/?LinkId=820529) para obter mais informações. |
| Copiar ficheiros |Olá cópias publicar perfil e toobe de artefactos do aplicação parâmetros ficheiros toohello compilação consumidos para implementação. |
| Publicar artefactos |Publica artefactos da compilação Olá. Permite que uma definição de versão artefactos de compilação de Olá a tooconsume. |

### <a name="verify-hello-default-set-of-tasks"></a>Verificar conjunto predefinido de Olá de tarefas
1. Certifique-se Olá **solução** campo entrada de Olá **NuGet restauro** e **construir solução** criar passos.  Por predefinição, estes passos de compilação executar após todos os ficheiros de solução que estão contidos no repositório de Olá associado.  Se pretender apenas Olá compilação definição toooperate desses ficheiros de solução, terá do ficheiro de toothat do tooexplicitly atualização Olá caminho.
2. Certifique-se Olá **solução** campo entrada de Olá **empacotar a aplicação** passo de compilação.  Por predefinição, este passo de compilação assume que apenas um projeto de aplicação de recursos de infraestrutura de serviço (.sfproj) existe no repositório de Olá.  Se tiver vários esses ficheiros no seu repositório e quiser tootarget apenas um para esta definição de compilação, é necessário o ficheiro de toothat do tooexplicitly atualização Olá caminho.  Se quiser toopackage projetos de várias aplicações no seu repositório, terá de toocreate adicionais **compilação do Visual Studio** os passos na definição de compilação de Olá que cada um projeto de aplicação de destino.  Em seguida, também terá de tooupdate Olá **argumentos de MSBuild** campo para cada um desses passos de compilação, para que a localização do pacote Olá seja exclusiva para cada um deles.
3. Verifique se o comportamento de controlo de versões de Olá definido no Olá **versões de aplicação de recursos de infraestrutura de serviço de atualização** passo de compilação.  Por predefinição, este passo de compilação acrescenta Olá compilação tooall versão valores numéricos nos ficheiros de manifesto do pacote de aplicação Olá. Consulte Olá [página de documentação de tarefas](https://go.microsoft.com/fwlink/?LinkId=820529) para obter mais informações. Isto é útil para suportar a atualização da sua aplicação, uma vez que os valores da versão diferente da implementação anterior Olá requer que cada implementação de atualização. Se não estiver a destinar toouse atualização da aplicação no seu fluxo de trabalho, pode considerar desativar este passo de compilação. Tem de ser desativada se a sua intenção é tooproduce uma compilação que pode ser utilizado toooverwrite uma aplicação de Service Fabric existente. Falha na implementação de Olá se versão Olá da aplicação Olá produzida por compilação de Olá não corresponde à versão de Olá da aplicação Olá num cluster de Olá.
4. Se a solução contiver um projeto de .NET Core, certifique-se de que a definição da compilação contiver um passo de compilação que restaura dependências Olá:
   1. Selecione **passo de compilação de adicionar...** .
   2. Localizar Olá **da linha de comandos** no separador de utilitário Olá de tarefas e clique o botão Adicionar.
   3. Para campos de entrada da tarefa de Olá, utilize Olá os seguintes valores:
   4. Ferramenta: dotnet
   5. Argumentos: restaurar
   6. Arraste tarefas Olá, para que seja imediatamente após Olá **NuGet restauro** passo.
5. Guarde as alterações efetuadas toohello compilação definição.

### <a name="try-it"></a>Experimente
Selecione **criar fila** toomanually iniciar uma compilação. Baseia-se também acionadores na emissão ou entrada. Depois de verificar que a compilação de Olá está a executar com êxito, pode agora passar toodefining uma definição de versão que implementa o cluster de tooa de aplicação.

## <a name="create-a-release-definition"></a>Criar uma definição de versão
Uma definição de versão Team Services descreve um fluxo de trabalho é composto por um conjunto de tarefas que são executados sequencialmente. objetivo Olá da definição da versão Olá que está a criar é tootake um pacote de aplicação e implementá-la tooa cluster. Quando utilizado em conjunto, Olá Criar definição e definição de versão pode executar o fluxo de trabalho completo Olá de carateres começadas tooending de ficheiros de origem com uma aplicação em execução no seu cluster. Saiba mais sobre os serviços da equipa [versão definições](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-definition-from-hello-release-template"></a>Criar uma definição do modelo da versão Olá
1. Abra o projeto no Visual Studio Team Services.
2. Selecione Olá **versão** separador.
3. Selecione Olá verde  **+**  iniciar sessão toocreate uma nova definição de versão e selecionar **criar versão definição** no menu de Olá.
4. Olá caixa de diálogo que se abre, selecione **implementação de recursos de infraestrutura do serviço de Azure** dentro Olá **implementação** categoria de modelo.
5. Selecione **seguinte**.
6. Selecione a definição de compilação de Olá pretende toouse como origem Olá esta definição de versão.  Olá versão definição referências Olá artefactos que foram produzidos pelo Olá selecionado Criar definição.
7. Verifique Olá **a implementação contínua** caixa de verificação se quiser toohave Team Services automaticamente criar uma nova versão e implementar a aplicação de Service Fabric Olá sempre que uma compilação for concluída.
8. Selecione a fila de agente Olá desejar toouse. Agentes alojados são suportados.
9. Selecione **Criar**.
10. Edite o nome de definição de Olá clicando no ícone lápis Olá em Olá parte superior da página Olá.
11. Selecione Olá toowhich de cluster deve ser implementada a sua aplicação Olá **ligação de Cluster** campo entrada de tarefa Olá. ligação de cluster Olá fornece informações necessárias Olá que permite que o cluster de toohello Olá implementação tarefas tooconnect. Se ainda não tiver uma ligação de cluster para o cluster, selecione Olá **gerir** hiperligação seguinte toohello campo tooadd um. Na página Olá que se abre, execute Olá os seguintes passos:
    1. Selecione **ponto final de serviço novo** e, em seguida, selecione **Azure Service Fabric** menu Olá.
    2. Selecione o tipo de Olá de autenticação a ser utilizado pelo cluster Olá visada por este ponto final.
    3. Defina um nome para a sua ligação no Olá **nome da ligação** campo.  Normalmente, seria utilizar Olá nome do cluster.
    4. Definir o URL de ponto final da ligação de cliente de Olá no Olá **ponto final de Cluster** campo.  Exemplo: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Para as credenciais do Azure Active Directory, definir credenciais Olá pretende toouse tooconnect toohello cluster Olá **Username** e **palavra-passe** campos.
    6. Para a autenticação baseada em certificado, defina Olá Base64 codificação de ficheiro de certificado de cliente Olá no Olá **certificado de cliente** campo.  Consulte o menu de pop-up Olá ajuda sobre esse campo para informações sobre como tooget valor.  Se o certificado é protegido por palavra-passe, definir palavra-passe de Olá Olá **palavra-passe** campo.
    7. Confirmar as alterações ao clicar em **OK**. Depois de navegar tooyour back-definição de versão, clique em ícone de atualização de Olá no Olá **ligação de Cluster** endpoint Olá toosee de campo acabou de adicionar.
12. Guarde a definição da versão de Olá.

> [!NOTE]
> Accounts da Microsoft (por exemplo, @hotmail.com ou @outlook.com) não são suportadas com a autenticação do Azure Active Directory.
> 
> 

definição de Olá criado é composta por uma tarefa do tipo **implementação de aplicação do serviço de recursos de infraestrutura**. Consulte Olá [página de documentação de tarefas](https://go.microsoft.com/fwlink/?LinkId=820528) para obter mais informações sobre esta tarefa.

### <a name="verify-hello-template-defaults"></a>Certifique-se as predefinições de modelo Olá
1. Certifique-se Olá **publicar perfil** campo entrada de Olá **implementar aplicações de recursos de infraestrutura de serviço** tarefas. Por predefinição, este campo faz referência a um perfil de publicação com o nome Cloud.xml contidas no artefactos da compilação Olá. Se pretender tooreference um perfil de publicação diferente ou se a compilação de Olá contém vários pacotes de aplicações os artefactos, terá de caminho de Olá tooupdate adequadamente.
2. Certifique-se Olá **pacote de aplicação** campo entrada de Olá **implementar aplicações de recursos de infraestrutura de serviço** tarefas. Por predefinição, este campo referencia Olá predefinido pacote caminho da aplicação utilizado num modelo de definição de compilação Olá.  Se tiver modificado o caminho de pacote de aplicação de predefinido Olá Olá Criar definição, tem de caminho de Olá tooupdate adequadamente aqui bem.

### <a name="try-it"></a>Experimente
Selecione **criar versão** de Olá **versão** toomanually de menu do botão de criar uma versão. Olá caixa de diálogo que se abre, selecione a compilação de Olá que pretende versão de Olá toobase em e, em seguida, clique em **criar**. Se ativou a implementação contínua, versões serão criadas automaticamente quando a definição de compilação de Olá associado conclui uma compilação.

## <a name="next-steps"></a>Passos seguintes
toolearn mais sobre a integração contínua com aplicações de Service Fabric, leia Olá seguintes artigos:

* [Equipa de documentação dos serviços de raiz](https://www.visualstudio.com/docs/overview)
* [Criar gestão nos serviços de equipa](https://www.visualstudio.com/docs/build/overview)
* [Gestão de versões nos serviços de equipa](https://www.visualstudio.com/docs/release/overview)

