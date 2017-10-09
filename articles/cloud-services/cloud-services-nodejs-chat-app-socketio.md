---
title: "aplicação de aaaNode.js utilizando Socket.io | Microsoft Docs"
description: "Saiba como toouse socket.io numa aplicação node.js alojada no Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Criar uma aplicação de Node.js Chat com Socket.IO num serviço em nuvem do Azure
Socket.IO fornece em tempo real comunicação entre o entre o servidor de node.js e clientes. Este tutorial irá guiá-lo através de alojamento um socket. E/s baseado em aplicações de chat no Azure. Para obter mais informações sobre Socket.IO, consulte <http://socket.io/>.

Abaixo é uma captura de ecrã da aplicação Olá concluída:

![Uma janela de browser a apresentar serviço Olá alojado no Azure][completed-app]  

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que Olá seguintes produtos e versões são instalados toosuccessfully exemplo de Olá concluída neste artigo:

* Instalar o [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* Instalar o [Node. js](https://nodejs.org/download/)
* Instalar [Python versão 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Criar um projeto de serviço em nuvem
Olá passos seguintes criar projeto do serviço de nuvem Olá que irá alojar a aplicação de Socket.IO Olá.

1. De Olá **Menu Iniciar** ou **ecrã Iniciar**, procure **do Windows PowerShell**. Por fim, clique com botão direito **do Windows PowerShell** e selecione **executar como administrador**.
   
    ![Ícone do PowerShell do Azure][powershell-menu]
2. Criar um diretório denominado **c:\\nó**. 
   
        PS C:\> md node
3. Altere os diretórios toohello **c:\\nó** diretório
   
        PS C:\> cd node
4. Introduza os seguintes comandos toocreate uma nova solução com o nome de Olá **chatapp** e uma função de trabalho com o nome **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Verá Olá seguinte resposta:
   
    ![saída de Olá do novo Olá-azureservice e azurenodeworkerrolecmdlets adicionar](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Transferir Olá Chat exemplo
Para este projeto, utilizamos o exemplo de chat de Olá do Olá [repositório do Socket.IO GitHub]. Efetuar Olá seguinte o exemplo de Olá toodownload de passos e adicione-o projeto de toohello que criou anteriormente.

1. Criar uma cópia local do repositório de Olá utilizando Olá **Clone** botão. Também pode utilizar Olá **ZIP** projeto do botão toodownload Olá.
   
   ![Uma janela do browser ver https://github.com/LearnBoost/socket.io/tree/master/examples/chat, com ícone de transferência Olá ZIP realçado][chat-example-view]
2. Navegue de estrutura de diretórios Olá do repositório local Olá até chegar à Olá **exemplos\\chat** diretório. Copie Olá conteúdo neste diretório toothe **c:\\nó\\chatapp\\WorkerRole1** diretório que criou anteriormente.
   
   ![Explorador, apresentando conteúdo Olá exemplos Olá\\diretório de chat extraído de arquivo de Olá][chat-contents]
   
   Olá itens realçados na captura de ecrã Olá acima são ficheiros Olá copiados Olá **exemplos\\chat** diretório
3. No Olá **c:\\nó\\chatapp\\WorkerRole1** diretório, eliminar Olá **server.js** de ficheiros e, em seguida, renomeie Olá **app.js**ficheiro demasiado**server.js**. Esta ação remove predefinido Olá **server.js** ficheiro criado anteriormente pela Olá **adicionar AzureNodeWorkerRole** cmdlet e substitui-lo com a aplicação Olá de ficheiros de exemplo de chat de Olá.

### <a name="modify-serverjs-and-install-modules"></a>Modificar Server.js e instalar os módulos
Antes de aplicação Olá teste no Olá emulador do Azure, podemos tem de se algumas alterações secundárias. Execute Olá ficheiro de server.js toothe passos a seguir:

1. Abra Olá **server.js** ficheiro no Visual Studio ou num editor de texto.
2. Determinar Olá **dependências de módulo** secção início Olá de server.js e altere a linha de Olá que contém **sio = require('.. //.. lib//socket.IO')** demasiado**sio = require('socket.io')** conforme mostrado abaixo:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. aplicação de Olá tooensure escuta a porta correta de Olá, abra server.js no bloco de notas ou o seu editor favorito e, em seguida, altere a linha seguinte, substituindo **3000** com **process.env** conforme mostrado abaixo:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Depois de guardar as alterações de Olá demasiado**server.js**, utilize Olá os seguintes passos para instalar os módulos necessários e, em seguida, testar a aplicação Olá no emulador do Azure:

1. Utilizar **Azure PowerShell**, altere os diretórios toohello **c:\\nó\\chatapp\\WorkerRole1** Olá diretório e utilize a seguinte Olá tooinstall de comando módulos necessários para esta aplicação:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Esta ação instalará os módulos de Olá indicados no ficheiro de Package. JSON Olá. Após a conclusão do comando de Olá, deverá ver a seguinte de toothe semelhante de saída:
   
   ![comando de instalação de npm Olá resultado Olá][The-output-of-the-npm-install-command]
2. Uma vez que este exemplo foi originalmente parte de Olá repositório do Socket.IO GitHub e diretamente referenciada biblioteca de Socket.IO Olá pelo caminho relativo, Socket.IO não foi referenciado no ficheiro de Package. JSON Olá, pelo que, deve instalá-lo através da emissão Olá os seguintes comandos:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Testar e implementar
1. Inicie o emulador de Olá emitindo Olá os seguintes comandos:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Se ocorrerem problemas com iniciar emulador, ex.: início AzureEmulator: Ocorreu uma falha inesperada.  Detalhes: Foi encontrado um objeto de comunicação de Olá um erro inesperado, System.ServiceModel.Channels.ServiceChannel, não pode ser utilizado para comunicação porque está a ser Olá estado falhado.
   
      reinstalar AzureAuthoringTools v 2.7.1 e AzureComputeEmulator v 2.7 - Certifique-se de que a versão corresponde.
   >
   >


2. Abra um browser e navegue demasiado**http://127.0.0.1**.
3. Quando abre a janela do browser Olá, introduza uma alcunha e, em seguida, clique em enter.
   Isto irá permitir mensagens toopost como uma alcunha específica. funcionalidade de multiutilizador tootest, abra janelas do browser adicionais utilizando o mesmo URL e introduza nicknames diferentes.
   
   ![Duas janelas do browser que apresenta as mensagens de chat de Utilizador1 e o Utilizador2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Após a aplicação de Olá teste, pare o emulador de Olá ao emitir o comando seguinte:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. tooAzure de aplicação de Olá toodeploy, utilize o **Publish-AzureServiceProject** cmdlet. Por exemplo:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Ser toouse se um nome exclusivo, caso contrário Olá publicar processo irá falhar. Depois de concluída a implementação de Olá, browser Olá irá abrir e navegue serviço toohello implementado.
   > 
   > Se receber um erro a indicar que Olá fornecido o nome da subscrição não existe na Olá importado o perfil de publicação, tem de transferir e importar o perfil de publicação Olá para a sua subscrição antes de implementar tooAzure. Consulte Olá **implementar Olá aplicação tooAzure** secção [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Uma janela de browser a apresentar serviço Olá alojado no Azure][completed-app]
   
   > [!NOTE]
   > Se receber um erro a indicar que Olá fornecido o nome da subscrição não existe na Olá importado o perfil de publicação, tem de transferir e importar o perfil de publicação Olá para a sua subscrição antes de implementar tooAzure. Consulte Olá **implementar Olá aplicação tooAzure** secção [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

A aplicação está agora em execução no Azure e pode reencaminhar mensagens de chat entre diferentes clientes com o Socket.IO.

> [!NOTE]
> Para uma simplicidade este exemplo está limitado toochatting entre toohello ligado utilizadores mesma instância. Isto significa que se o serviço em nuvem Olá cria duas instâncias de função de trabalho, os utilizadores só conseguirão toochat com outros utilizadores ligados toohello mesma instância de função de trabalho. tooscale Olá toowork de aplicação com várias instâncias de função, pode utilizar uma tecnologia, como o estado de arquivo do Service Bus tooshare Olá Socket.IO em instâncias. Para obter exemplos, consulte exemplos de utilização de tópicos e filas do Service Bus Olá no Olá [Azure SDK para o repositório do Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, aprendeu como toocreate uma aplicação de chat básico alojada num serviço em nuvem do Azure. toolearn como toohost esta aplicação num Web site do Azure, consulte o artigo [compilar uma aplicação de Chat Node.js com Socket.IO no Web Site um Azure][chatwebsite].

Para obter mais informações, consulte também Olá [Centro para programadores do Node.js](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repositório do Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


