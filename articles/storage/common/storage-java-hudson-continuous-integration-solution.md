---
title: aaaHow toouse Hudson com o Blob storage | Microsoft Docs
description: "Descreve como toouse Hudson Blob Storage do Azure como um repositório de artefactos de compilação."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 119becdd-72c4-4ade-a439-070233c1e1ac
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 196b5d014b0318c5972a052f7822b568cfcc23df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-hudson-continuous-integration-solution"></a>Utilizar o Armazenamento do Azure com uma solução Hudson de Integração Contínua
## <a name="overview"></a>Descrição geral
Olá informações seguintes mostram como o armazenamento de BLOBs de toouse como um repositório de artefactos de compilação criado por uma solução de integração contínua Hudson (CI) ou como uma origem de ficheiros transferível toobe utilizadas num processo de compilação. Um dos cenários de olá onde que seria útil isto é quando estiver a codificação num ambiente de desenvolvimento seja ágil (utilizando Java ou outros idiomas), baseiam-se em execução com base na integração contínua e necessitam de um repositório de artefactos da compilação, para que lhe foi , por exemplo, partilhá-los com outros membros da organização, os seus clientes, ou manter um arquivo.  Outro cenário é quando a tarefa de compilação próprio requer outros ficheiros, por exemplo, toodownload de dependências, como parte da Olá Criar entrada.

Neste tutorial, irá utilizar Olá Plug-in de armazenamento do Azure para CI Hudson disponibilizados pela Microsoft.

## <a name="introduction-toohudson"></a>Introdução tooHudson
Hudson permite integração contínua de um projeto de software ao permitir que os programadores tooeasily integrar as alterações de código e ter baseia-se produzidos automaticamente e com frequência, deste modo, aumentar a produtividade Olá de programadores Olá. Compilações são com versão e compilação artefactos podem ser carregados toovarious repositórios. Este artigo irá mostrar como toouse Blob storage do Azure como repositório Olá Olá criar artefactos. Esta operação também irá mostrar como dependências toodownload do Blob storage do Azure.

Obter mais informações sobre Hudson podem ser encontradas em [cumprir Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson).

## <a name="benefits-of-using-hello-blob-service"></a>Vantagens da utilização Olá serviço Blob
Vantagens da utilização Olá Blob serviço toohost seus artefactos de compilação de desenvolvimento seja ágil incluem:

* Elevada disponibilidade dos seus artefactos de compilação e/ou transferíveis dependências.
* Desempenho quando a sua solução de Hudson CI carrega os seus artefactos de compilação.
* Desempenho quando os clientes e os parceiros de transferir os seus artefactos de compilação.
* Controlar através de políticas de acesso de utilizador, com uma opção entre acesso anónimo, acesso de assinatura de acesso partilhado com base em expiração, privada acesso, etc.

## <a name="prerequisites"></a>Pré-requisitos
Será necessário Olá seguintes toouse Olá serviço Blob com a sua solução de Hudson CI:

* Uma solução de integração contínua Hudson.
  
    Se não tem atualmente uma solução de Hudson CI, pode executar uma solução de Hudson CI utilizando Olá técnica os seguintes:
  
  1. Numa máquina preparados para Java, transferência Olá Hudson WAR de <http://hudson-ci.org/>.
  2. Na linha de comandos que é aberta toohello pasta que contém Olá Hudson WAR, execute Olá Hudson WAR. Por exemplo, se tiver transferido versão 3.1.2:
     
      `java -jar hudson-3.1.2.war`

  3. No seu browser, abra `http://localhost:8080/`. Esta ação irá abrir Olá Hudson dashboard.
  4. Após a primeira utilização da Hudson, conclua a configuração inicial do Olá em `http://localhost:8080/`.
  5. Depois de concluir a configuração inicial Olá, Cancelar Olá a executar a instância de Olá Hudson WAR, iniciar Olá Hudson WAR novamente e volte a abrir Olá Hudson dashboard, `http://localhost:8080/`, que irá utilizar tooinstall e configurar o plug-in do Olá Storage do Azure.
     
      Enquanto seria possível definir uma solução de Hudson CI típica toorun como um serviço, executar Olá Hudson war na linha de comandos Olá será suficiente para este tutorial.
* Uma conta do Azure. Pode inscrever-se numa conta do Azure em <http://www.azure.com>.
* Uma conta de armazenamento do Azure. Se ainda não tiver uma conta de armazenamento, pode criar um utilizando os passos de Olá em [criar uma conta de armazenamento](../common/storage-create-storage-account.md#create-a-storage-account).
* Familiaridade com a solução de Hudson CI Olá é recomendada, mas não é necessária, como hello seguinte conteúdo irá utilizar tooshow um exemplo básico Olá passos necessários ao utilizar o serviço de Blob de Olá como um repositório para Hudson CI criar artefactos.

## <a name="how-toouse-hello-blob-service-with-hudson-ci"></a>Como toouse Olá serviço Blob com Hudson CI
serviço de Blob do Olá toouse com Hudson, terá de tooinstall Olá Plug-in do Storage do Azure, Olá toouse de plug-in de configurar a conta de armazenamento e, em seguida, crie uma ação de compilação de pós-implementação que carrega a sua conta de armazenamento de tooyour de artefactos de compilação. Estes passos são descritos nas Olá secções a seguir.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Como tooinstall Olá Plug-in do Storage do Azure
1. No dashboard de Hudson Olá, clique em **gerir Hudson**.
2. No Olá **gerir Hudson** página, clique em **gerir plug-ins**.
3. Clique em Olá **disponível** separador.
4. Clique em **outros**.
5. No Olá **artefactos Uploaders** secção, selecione **Plug-in do armazenamento do Microsoft Azure**.
6. Clique em **Instalar**.
7. Depois de concluída a instalação de Olá, reinicie Hudson.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Como tooconfigure Olá toouse de plug-in de armazenamento do Azure a conta de armazenamento
1. No dashboard de Hudson Olá, clique em **gerir Hudson**.
2. No Olá **gerir Hudson** página, clique em **Configurar sistema**.
3. No Olá **configuração de conta de armazenamento do Microsoft Azure** secção:
   
    a. Introduza o nome de conta do storage, pode obter de Olá [Portal do Azure](https://portal.azure.com).
   
    b. Introduza a chave de conta de armazenamento, também obtainable de Olá [Portal do Azure](https://portal.azure.com).
   
    c. Utilize o valor predefinido Olá **URL de ponto final de serviço Blob** se estiver a utilizar nuvem pública do Azure de Olá. Se estiver a utilizar uma nuvem do Azure diferente, utilize o ponto final de Olá como Olá especificado no [Portal do Azure](https://portal.azure.com) para a sua conta de armazenamento.
   
    d. Clique em **validar as credenciais do armazenamento** toovalidate sua conta do storage.
   
    e. [Opcional] Se tiver contas de armazenamento adicional que pretende que o tooyour disponível efetuada Hudson CI, clique em **adicionar mais contas de armazenamento**.
   
    f. Clique em **guardar** toosave as suas definições.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Como toocreate uma ação de compilação de pós-implementação que carrega a sua conta de armazenamento de tooyour de artefactos de compilação
Para efeitos de instrução, primeiro precisamos toocreate uma tarefa que irá criar vários ficheiros e, em seguida, adicione na Olá ação de pós-compilação de tooupload Olá ficheiros tooyour conta do storage.

1. No dashboard de Hudson Olá, clique em **nova tarefa**.
2. Tarefa de Olá nome **MyJob**, clique em **criar uma tarefa de estilo livre software**e, em seguida, clique em **OK**.
3. No Olá **criar** secção de configuração da tarefa de Olá, clique em **Adicionar passo de compilação** e escolha **comando batch do Windows de executar**.
4. No **comando**, utilize Olá os seguintes comandos:

    ```   
        md text
        cd text
        echo Hello Azure Storage from Hudson > hello.txt
        date /t > date.txt
        time /t >> date.txt
    ```

5. No Olá **ações de pós-compilação de** secção de configuração da tarefa de Olá, clique em **carregar artefactos tooMicrosoft Blob storage do Azure**.
6. Para **nome da conta de armazenamento**, selecione Olá toouse de conta de armazenamento.
7. Para **nome do contentor**, especifique o nome do contentor Olá. (contentor de Olá será criado se já existir quando artefactos de compilação de Olá são carregados.) Pode utilizar variáveis de ambiente, por isso, para este exemplo introduza **${JOB_NAME}** como nome do contentor Olá.
   
    **Sugestão**
   
    Abaixo Olá **comando** secção onde introduziu um script para **comando batch do Windows de executar** é uma ligação de variáveis de ambiente de toohello reconhecidas pelo Hudson. Clique em ligar nomes de variáveis de ambiente do toolearn Olá e descrições. Tenha em atenção que ambiente variáveis que contêm carateres especiais, como Olá **BUILD_URL** variável de ambiente, não são permitidos como um nome de contentor ou o caminho virtual comum.
8. Clique em **tornar o novo contentor público por predefinição** para este exemplo. (Se pretender toouse um contentor privado, terá de toocreate um acesso de tooallow de assinatura de acesso partilhado. Que ultrapassa o âmbito Olá deste artigo. Pode saber mais sobre assinaturas de acesso partilhado no [utilizando partilhado acesso assinaturas (SAS)](../storage-dotnet-shared-access-signature-part-1.md).)
9. [Opcional] Clique em **contentor limpa antes de carregar** se quiser Olá contentor toobe limpo de conteúdo antes de compilação artefactos são carregados (deixe a opção desmarcada se não pretender que o conteúdo de Olá tooclean do contentor de Olá).
10. Para **tooupload de lista de artefactos**, introduza  **texto /*. txt**.
11. Para **caminho virtual comuns para os artefactos carregados**, introduza **${criar\_ID} / ${criar\_número}**.
12. Clique em **guardar** toosave as suas definições.
13. No dashboard de Hudson Olá, clique em **compilar agora** toorun **MyJob**. Examine o resultado da consola Olá para o estado. Mensagens de estado de armazenamento do Azure serão incluídas em resultado da consola Olá quando inicia a ação de pós-compilação de Olá artefactos de compilação tooupload.
14. Após a conclusão bem-sucedida da tarefa de Olá, pode examinar os artefactos de compilação Olá abrindo blob público Olá.
    
    a. Inicie sessão no toohello [Portal do Azure](https://portal.azure.com).
    
    b. Clique em **armazenamento**.
    
    c. Clique no nome de conta de armazenamento Olá que utilizou para Hudson.
    
    d. Clique em **contentores**.
    
    e. Clique com o nome de contentor de Olá **myjob**, que é a versão em minúsculas do Olá do nome da tarefa Olá que atribuiu quando criou Olá tarefa Hudson. Os nomes dos contentores e BLOBs nomes estão em minúsculas (e maiúsculas e minúsculas) no Storage do Azure. Na lista de Olá de blobs para com o nome de contentor de Olá **myjob** deverá ver **hello.txt** e **date.txt**. Copie o URL de Olá para qualquer uma destes itens e abri-lo no seu browser. Irá ver o ficheiro de texto de Olá que foi carregado como um artefacto de compilação.

Apenas uma ação de compilação pós-implementação que carrega artefactos tooAzure armazenamento de BLOBs pode ser criada por tarefa. Tenha em atenção que o armazenamento de BLOBs de tooAzure tooupload artefactos Olá única ação de pós-compilação de pode especificar ficheiros diferentes (incluindo os carateres universais) e caminhos toofiles dentro **tooupload de lista de artefactos** utilizando um ponto e vírgula como separador. Por exemplo, se criar a sua Hudson produz JAR e ficheiros TXT na sua área de trabalho **criar** pasta e pretender tooupload ambas tooAzure armazenamento de BLOBs, utilize o seguinte Olá para Olá **tooupload de lista de artefactos** valor: **criar /\*. JAR; compilação /\*. txt**. Também pode utilizar a sintaxe do valor de duplo vírgula toospecify toouse um caminho no nome do blob Olá. Por exemplo, se quiser Olá v7 tooget carregado utilizando **binários** no caminho do blob Olá e Olá TXT ficheiros tooget carregado utilizando **avisos** no caminho de blob Olá, utilize o seguinte de Olá para Olá  **Lista de tooupload artefactos** valor: **criar /\*. jar::binaries; compilação /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Como toocreate um passo de compilação que transfere a partir do Blob storage do Azure
Olá, os passos seguintes mostra como tooconfigure uma compilação passo itens toodownload do Blob storage do Azure. Isto é útil se pretender tooinclude itens na sua compilação, por exemplo, V7 manter no Blob storage do Azure.

1. No Olá **criar** secção de configuração da tarefa de Olá, clique em **Adicionar passo de compilação** e escolha **transferir a partir do Blob storage do Azure**.
2. Para **nome da conta de armazenamento**, selecione Olá toouse de conta de armazenamento.
3. Para **nome do contentor**, especifique Olá nome do contentor de Olá com blobs Olá pretende toodownload. Pode utilizar variáveis de ambiente.
4. Para **nome do Blob**, especifique o nome do blob Olá. Pode utilizar variáveis de ambiente. Além disso, pode utilizar um asterisco como caráter universal depois de especificar Olá letter(s) inicial do nome do blob Olá. Por exemplo, **projeto\***  especificar todos os blobs cujos nomes começar a utilizar **projeto**.
5. [Opcional] Para **caminho de transferência**, especifique o caminho de Olá em Olá máquina Hudson onde pretende que os ficheiros de toodownload do Blob storage do Azure. Também podem ser utilizadas a variáveis de ambiente. (Se não fornecer um valor para **caminho de transferência**, ficheiros de Olá do Blob storage do Azure será área de trabalho da tarefa toohello transferido.)

Se tiver itens adicionais que pretende toodownload do Blob storage do Azure, pode criar passos adicionais de compilação.

Depois de executar uma compilação, pode verificar o resultado da consola de histórico de compilação de Olá ou vista de olhos a localização de transferência, toosee se Olá blobs destinados foram transferidos com êxito.

## <a name="components-used-by-hello-blob-service"></a>Componentes utilizados pelo Olá serviço Blob
seguinte Olá fornece uma descrição geral Olá Blob de componentes do serviço.

* **Conta de armazenamento**: todas as acesso tooAzure armazenamento é feito através de uma conta de armazenamento. Este é o nível mais elevado de Olá de espaço de nomes de Olá para aceder aos blobs. Uma conta pode conter um número ilimitado de contentores, desde que o tamanho total é em 100 TB.
* **Contentor**: um contentor fornece um agrupamento de um conjunto de blobs. Todos os blobs tem de estar num contentor. Uma conta pode conter um número ilimitado de contentores. Um contentor pode armazenar um número ilimitado de blobs.
* **Blob**: um ficheiro de qualquer tipo e tamanho. Existem dois tipos de blobs que podem ser armazenados no Storage do Azure: blobs de blocos e de página. A maioria dos ficheiros são blobs de blocos. Pode ser um blob de bloco única cópia de segurança too200 GB de tamanho. Este tutorial utiliza os blobs de blocos. Os blobs de páginas, outro tipo de blob, podem ser segurança too1 TB de tamanho e são mais eficiente quando intervalos de bytes num ficheiro são modificados com frequência. Para obter mais informações sobre os blobs, consulte [compreender os Blobs de blocos, os Blobs de acréscimo e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Formato de URL**: Blobs são endereçáveis utilizando Olá segue o formato de URL:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (formato Olá acima aplica-se toohello de nuvem do Azure público. Se estiver a utilizar uma nuvem do Azure diferente, utilize Olá ponto final dentro Olá [Portal do Azure](https://portal.azure.com) toodetermine o ponto final do URL.)
  
    No formato de Olá acima, `storageaccount` representa Olá nome da sua conta de armazenamento, `container_name` representa Olá nome do seu contentor e `blob_name` representa Olá nome do seu blob, respetivamente. No nome do contentor Olá, pode ter vários caminhos, separados por uma barra,  **/** . nome do contentor de exemplo Olá neste tutorial foi **MyJob**, e **${criar\_ID} / ${criar\_número}** foi utilizado para Olá comuns caminho virtual, resultando em Olá blob ter um URL de Olá seguinte formato:
  
    `http://example.blob.core.windows.net/myjob/2014-05-01_11-56-22/1/hello.txt`

## <a name="next-steps"></a>Passos seguintes
* [Cumprir Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)
* [Armazenamento do Azure SDK para Java](https://github.com/azure/azure-storage-java)
* [Referência do SDK de cliente de armazenamento do Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST dos Serviços do Armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blogue da Equipa de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)

Para obter mais informações, visite [Azure para programadores Java](/java/azure).