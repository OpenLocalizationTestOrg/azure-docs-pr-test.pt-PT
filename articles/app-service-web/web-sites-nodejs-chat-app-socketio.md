---
title: "aaaCreate uma aplicação de chat Node.js com Socket.IO no App Service do Azure"
description: "Um tutorial que demonstra com socket.io numa aplicação web node.js alojada no Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Criar uma aplicação de chat Node.js com o Socket.IO no App Service do Azure
Socket.IO fornece em tempo real comunicação entre o servidor de node.js e clientes que utilizam WebSockets. Também suporta transportes de contingência tooother (tais como a consulta muito) que funcionam com os browsers mais antigos. Este tutorial irá guiá-lo através de alojamento uma aplicação de chat Socket.IO com base em como uma aplicação web do Azure e mostrar-lhe como tooscale Olá a aplicação utilizar [a Cache de Redis do Azure]. Para obter mais informações sobre Socket.IO, consulte <http://socket.io/>.

> [!NOTE]
> procedimentos de Olá nesta tarefa aplicam-se demasiado[Web Apps do App Service]; para serviços em nuvem, consulte [compilar uma aplicação de Chat Node.js com Socket.IO num serviço em nuvem do Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Transferir o exemplo de chat de Olá
Para este projeto, utilizamos o exemplo de chat de Olá do Olá [repositório do Socket.IO GitHub]. Efetuar Olá seguinte o exemplo de Olá toodownload de passos e adicione-o projeto de toohello que criou anteriormente.

1. Transferir um [ZIP ou GZ arquivados versão] do projeto de Socket.IO Olá (versão 1.3.5 foi utilizado para este documento)
2. Extrair Olá de arquivo e copie Olá **exemplos\\chat** nova localização do diretório tooa. Por exemplo,  **\\nó\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modificar app.js e instalar os módulos
1. Mudar o nome Olá **index.js** ficheiro demasiado**app.js**. Isto permite toodetect do Azure que se trata de uma aplicação Node.js.
2. Abra Olá **app.js** ficheiro num editor de texto. Linha de Olá de alteração que contém `var io = require('../..')(server);` conforme mostrado abaixo:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Abra Olá **Package. JSON** de ficheiros e adicionar um toosocket.io de referência em `dependencies`, conforme mostrado abaixo:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Na Olá da linha de comandos, altere toohello  **\\nó\\chat** diretório e utilize npm tooinstall Olá módulos necessários para esta aplicação:
   
        npm install
   
    Esta ação instalará os módulos de Olá para uma subpasta denominada **node_modules**.

## <a name="create-an-azure-web-app"></a>Criar uma aplicação Web do Azure
Siga estes passos toocreate uma aplicação web do Azure, ativar a publicação de Git e, em seguida, ativar o suporte de WebSocket para a aplicação web de Olá.

> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Avaliação Gratuita do Azure</a>.
> 
> 

1. Instalar Olá Interface de linha de comandos do Azure (CLI do Azure) e ligar tooyour subscrição do Azure. Consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md).
2. Se esta for a primeira hora configurar um repositório no Azure, terá das credenciais de início de sessão toocreate. No Olá CLI do Azure, introduza Olá os seguintes comandos:
   
        azure site deployment user set [username] [password]
3. Alterar toohello  **\\node\chat** diretório e seguinte Olá de utilização de comandos toocreate uma nova aplicação web do Azure e um repositório de Git local. Este comando também cria um Git remoto nomeado 'azure'.
   
        azure site create mysitename --git
   
    Tem de substituir 'mysitename' com um nome exclusivo para a sua aplicação web.
4. Consolide Olá existente ficheiros toohello repositório local utilizando Olá os seguintes comandos:
   
        git add .
        git commit -m "Initial commit"
5. Emita o repositório de Web Apps do Azure Olá ficheiros toohello com Olá os seguintes comandos:
   
        git push azure master
   
    Quando lhe for pedido, introduza as credenciais do passo 2. Irá receber mensagens de estado conforme os módulos são importados no servidor de Olá. Após a conclusão deste processo, Olá aplicação será alojada na sua aplicação web do Azure.
   
   > [!NOTE]
   > Durante a instalação do módulo, poderá reparar erros que ' Olá projeto importado... não foi encontrado '. Estes podem ser ignorados.
   > 
   > 
6. Socket.IO utiliza WebSockets, que não estão ativados por predefinição no Azure. tooenable os sockets web, utilize Olá os seguintes comandos:
   
        azure site set -w
   
    Se lhe for solicitado, introduza o nome de Olá da aplicação web de Olá.
   
   > [!NOTE]
   > Olá, será de comando 'do azure site set -w' funcionam apenas com a versão 0.7.4 ou superior do Olá Interface de linha de comandos do Azure. Também pode ativar o suporte de WebSocket utilizando Olá [Portal do Azure](https://portal.azure.com).
   > 
   > tooenable WebSockets utilizando Olá Portal do Azure, clique em Olá web aplicação a partir do painel de aplicações Web Olá, clique em **todas as definições** > **definições da aplicação**. Em **Web Sockets**, clique em **no**. Em seguida, clique em **Guardar**.
   > 
   > 
7. aplicação de web de Olá tooview no seguinte de Olá do Azure, utilize comando toolaunch o browser e navegue toohello alojado web app:
   
        azure site browse

A aplicação está agora em execução no Azure e pode reencaminhar mensagens de chat entre diferentes clientes com o Socket.IO.

## <a name="scale-out"></a>Aumentar horizontalmente
Podem ser ampliadas Socket.IO aplicações utilizando um **adaptador** toodistribute eventos entre várias instâncias de aplicações e as mensagens. Enquanto existem vários adaptadores disponíveis, Olá [socket.io redis] adaptador pode ser utilizado facilmente com funcionalidade de Cache de Redis do Azure Olá.

> [!NOTE]
> Um requisito adicional para aumentar horizontalmente uma solução de Socket.IO é suporte para sessões temporária. Sessões temporária estão ativadas por predefinição para Web Apps do Azure através do encaminhamento de pedidos do Azure. Para obter mais informações, consulte [afinidade de instância de Web Sites no Azure].
> 
> 

### <a name="create-a-redis-cache"></a>Criar uma cache de Redis
Efetue os passos de Olá em [criar uma cache na Cache de Redis do Azure] toocreate uma nova cache.

> [!NOTE]
> Guardar Olá **nome de anfitrião** e **chave primária** para a sua cache, como estes serão necessários no Olá próximos passos.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Adicionar redis Olá e módulos socket.io redis
1. De uma linha de comandos, altere toohello  **\\nó\\chat** Olá de diretório e utilize os seguintes comandos.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > versões de Olá especificadas neste comando são versões Olá utilizadas ao testar este artigo.
   > 
   > 
2. Modificar Olá **app.js** seguinte do ficheiro tooadd Olá linhas imediatamente após`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Substitua **redishostname** e **rediskey** com o nome de anfitrião Olá e a chave para a sua cache de Redis.
   
    Este procedimento cria um publicar e subscrever toohello de cliente criada anteriormente a cache de Redis. os clientes de Olá, em seguida, são utilizados com Olá adaptador tooconfigure cache de Redis Socket.IO toouse Olá para passar os eventos e as mensagens entre instâncias da aplicação
   
   > [!NOTE]
   > Ao hello **socket.io redis** adaptador pode comunicar diretamente tooRedis, a versão atual do Olá não suporta a autenticação de Olá necessária para a cache de Redis do Azure. Para que a ligação inicial Olá é criada utilizando o Olá **redis** módulo, o cliente de Olá, em seguida, é passada toohello **socket.io redis** adaptador.
   > 
   > Enquanto a Cache de Redis do Azure suporta ligações seguras através da porta 6380, módulos de Olá utilizados neste exemplo não suportam ligações seguras a partir de 14/7/2014. Olá acima código utiliza Olá, porta não segura do 6379.
   > 
   > 
3. Olá guardar modificado **app.js**

### <a name="commit-changes-and-redeploy"></a>Consolidar as alterações e volte a implementar
Na linha de comandos no Olá Olá  **\\nó\\chat** diretório, utilize Olá seguintes alterações de toocommit de comandos e volte a implementar aplicações de Olá.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Depois das alterações de Olá tem sido feito o Push toohello servidor, pode dimensionar o seu site em múltiplas instâncias utilizando Olá os seguintes comandos.

    azure site scale instances --instances #

Onde  **#**  é o número de Olá de toocreate de instâncias.

Pode ligar aplicação web de tooyour de vários tooverify browsers ou computadores clientes tooall corretamente são enviadas as mensagens.

## <a name="troubleshooting"></a>Resolução de problemas
### <a name="connection-limits"></a>Limites de ligação
As aplicações Web do Azure está disponível em vários SKUs, que determinam o site do Olá recursos tooyour disponíveis. Isto inclui o número de Olá de ligações de WebSocket permitido. Para obter mais informações, consulte Olá [página de preços de aplicações Web].

### <a name="messages-arent-being-sent-using-websockets"></a>As mensagens não são enviadas utilizando WebSockets
Se os browsers cliente mantém reverter toolong consulta em vez de utilizar WebSockets, poderá ser devido a um dos seguintes Olá.

* **Tente limitar Olá transporte toojust WebSockets**
  
    Por ordem para Socket.IO toouse WebSockets como Olá mensagens transporte tanto o servidor de Olá como o cliente tem de suportar WebSockets. Se um ou Olá outro não, Socket.IO negociará transporte outro, tais como a consulta longa. lista de predefinição Olá de transportes utilizado pelo Socket.IO é ` websocket, htmlfile, xhr-polling, jsonp-polling`. Pode forçar-tooonly utilize WebSockets adicionando Olá seguinte código toohello **app.js** ficheiro, após Olá linha contendo `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Tenha em atenção que browsers antigos que não suporta WebSockets não será capaz de tooconnect toohello site enquanto Olá acima código está ativo, como restringe apenas tooWebSockets de comunicação.
  > 
  > 
* **Utilizar SSL**
  
    Os WebSockets baseia-se em algum menor utilizados cabeçalhos de HTTP, tais como Olá **atualizar** cabeçalho. Alguns dispositivos de rede intermédio, por exemplo, web proxies, podem remover estes cabeçalhos. tooavoid este problema, pode estabelecer ligação de WebSocket Olá através de SSL.
  
    Uma forma fácil tooaccomplish é demasiado tooconfigure Socket.IO`match origin protocol`. Isto dá instruções ao hello comunicação Socket.IO toosecure WebSockets igual Olá originadas HTTP/HTTPS pedido Olá da página web. Se um browser utiliza um HTTPS URL toovisit seu Web site, subsequentes comunicações de WebSocket através de Socket.IO esteja protegidas através de SSL.
  
    toomodify tooenable este exemplo nesta configuração, adicionar Olá seguinte código toohello **app.js** ficheiro após Olá linha contendo `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Verifique as definições da Web. config**
  
    Aplicações web do Azure que alojam aplicações Node.js utilizam Olá **Web. config** tooroute de ficheiros recebido pedidos de aplicação de Node.js toohello. Para WebSockets toofunction corretamente com aplicações Node.js, Olá **Web. config** tem de conter Olá seguir entrada.
  
        <webSocket enabled="false"/>
  
    Isto desativa o módulo de IIS WebSockets Olá, que inclui a sua própria implementação de WebSockets e entra em conflito com o Node.js módulos de WebSocket específicos, tais como Socket.IO. Se esta linha não está presente ou está definida demasiado`true`, isto pode dever-razão de Olá transporte de WebSocket Olá não está a trabalhar para a sua aplicação.
  
    Normalmente, aplicações Node.js não incluem um **Web. config** de ficheiros, para Web sites do Azure irá gerar automaticamente um para as aplicações Node.js quando estão implementadas. Uma vez que este ficheiro é gerado automaticamente no servidor de Olá, tem de utilizar Olá, FTP ou FTPS URL para o Web site tooview este ficheiro. Pode encontrar Olá FTP e FTPS URLs para o seu site no portal clássico Olá ao selecionar a sua aplicação web e, em seguida, Olá **Dashboard** ligação. Olá URLs são apresentados no Olá **leitura rápida** secção.
  
  > [!NOTE]
  > Olá **Web. config** ficheiro só é gerado por Web sites do Azure, se a aplicação não fornecer um. Se fornecer um **Web. config** ficheiro na raiz de Olá do seu projeto de aplicação, será utilizado pelo Web Apps do Azure.
  > 
  > 
  
    Se a entrada Olá não está presente ou é definir o valor de tooa da `true`, em seguida, deve criar um **Web. config** no Olá raiz da sua aplicação Node.js e especifique um valor de `false`.  Para referência, Olá abaixo está um predefinido **Web. config** para uma aplicação que utiliza **app.js** como ponto de entrada Olá.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Se a sua aplicação utiliza um ponto de entrada diferente de **app.js**, tem de substituir todas as ocorrências de **app.js** com Olá corrigir o ponto de entrada. Por exemplo, substituindo **app.js** com **server.js**.

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service], onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, aprendeu como toocreate uma aplicação de chat alojada numa aplicação web do Azure. Também pode alojar esta aplicação como um serviço em nuvem do Azure. Para obter os passos sobre como tooaccomplish esta, consulte [compilar uma aplicação de Chat Node.js com Socket.IO num serviço em nuvem do Azure].

Para obter mais informações, consulte também Olá [Centro para programadores do Node.js].

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes].

<!-- URL List -->

[a Cache de Redis do Azure]: /documentation/services/redis-cache/
[Web Apps do App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[página de preços de aplicações Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[compilar uma aplicação de Chat Node.js com Socket.IO num serviço em nuvem do Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[App Service do Azure e o respetivo impacto nos serviços do Azure existentes]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro para programadores do Node.js]: /develop/nodejs/
[experimentar o App Service]: https://azure.microsoft.com/try/app-service/
[afinidade de instância de Web Sites no Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[criar uma cache na Cache de Redis do Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[repositório do Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP ou GZ arquivados versão]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
