---
title: 'B2C do Azure AD: Proteger uma API Web utilizando Node.js | Microsoft Docs'
description: Como a API web de toobuild um Node.js que aceita tokens a partir de um inquilino do B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>B2C do Azure AD: Proteger uma API Web utilizando Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Com o Azure Active Directory (Azure AD) B2C, pode proteger uma API web utilizando tokens de acesso de OAuth 2.0. Estes tokens permitem que as aplicações de cliente que utilizam a API do Azure AD B2C tooauthenticate toohello. Este artigo mostra como toocreate uma API de "lista de tarefas" que permite aos utilizadores tooadd e a lista de tarefas. Olá web API está protegida com o Azure AD B2C e só permite que os utilizadores autenticados toomanage respetiva lista de tarefas.

> [!NOTE]
> Este exemplo foi escrito utilizando o tooby toobe ligado nosso [aplicação de exemplo de iOS B2C](active-directory-b2c-devquickstarts-ios.md). Olá passagem atual pela primeira vez e, em seguida, acompanhe com esse exemplo.
>
>

**Passport** é o middleware de autenticação do Node.js. Flexível e modular, o Passport pode ser instalado discretamente em qualquer aplicação Web baseada no Express ou Restify. Um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, o Facebook, o Twitter e muito mais. Desenvolvemos uma estratégia para o Azure Active Directory (Azure AD). Instalará este módulo e, em seguida, adicionar Olá do Azure AD `passport-azure-ad` Plug-in.

toodo neste exemplo, tem de:

1. Registar uma aplicação com o Azure AD.
2. Configurar a sua aplicação toouse Passport `azure-ad-passport` Plug-in.
3. Configure uma cliente aplicação toocall Olá "lista de tarefas" API web.

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório do Azure AD B2C
Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.  Um diretório é um contentor para todos os utilizadores, aplicações, grupos, etc.  Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.

## <a name="create-an-application"></a>Criar uma aplicação
Em seguida, terá de toocreate uma aplicação no diretório do B2C que dá ao Azure AD algumas informações que necessita de toosecurely comunicar com a sua aplicação. Neste caso, a aplicação de cliente Olá e web API são representadas por um único **ID da aplicação**, uma vez que compõem uma aplicação lógica. toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário:

* Incluir um **web app/web api** na aplicação Olá
* Introduzir `http://localhost/TodoListService` como um **URL de resposta**. É Olá predefinido URL para este exemplo de código.
* Criar um **Segredo de aplicação** para a aplicação e copiá-lo. Estes dados são necessários mais tarde. Tenha em atenção que este valor tem de toobe [XML de escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de o utilizar.
* Olá cópia **ID da aplicação** que é atribuído tooyour aplicação. Estes dados são necessários mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar as políticas
No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md). Esta aplicação contém duas experiências de identidade: registo e início de sessão. Tem toocreate uma política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Quando criar as três políticas, não se esqueça de:

* Escolha Olá **nome a apresentar** e outros atributos de inscrição na política de inscrição.
* Escolha Olá **nome a apresentar** e **ID de objeto** afirmações de aplicação em cada política.  Também pode escolher outras afirmações.
* Copie Olá **nome** de cada política depois de a criar. Deve ter o prefixo de Olá `b2c_1_`.  Vai necessitar destes nomes de política mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de criar as três políticas, está pronto toobuild a aplicação.

toolearn sobre como funcionam as políticas no Azure AD B2C, comece com Olá [.NET introdução à aplicação web tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Transferir o código de Olá
Olá código para este tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). exemplo de Olá toobuild como vá, pode [transferir um projeto de estrutura como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). Também pode clonar a estrutura de Olá:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

aplicação Olá concluída está também [disponível como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou Olá `complete` ramo do Olá mesmo repositório.

## <a name="download-nodejs-for-your-platform"></a>Transferir Node.js para a plataforma
toosuccessfully utilizar este exemplo, precisa de uma instalação do Node.js.

Instalar Node.js de [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Instalar MongoDB para a plataforma
toosuccessfully utilizar este exemplo, precisa de uma instalação do MongoDB. Utilizamos o MongoDB toomake a API REST persistente em instâncias de servidor.

Instalar MongoDB de [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Esta passagem parte do princípio de que usa Olá servidor e a instalação pontos finais predefinidos para o MongoDB, que a hora de Olá desta redação é `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Instalar os módulos do Restify Olá na API web
Utilizamos o Restify toobuild a API REST. O Restify é uma estrutura de aplicação Node.js mínima e flexível derivada do Express. Tem um conjunto robusto de funcionalidades para a criação de APIs REST por cima do Connect.

### <a name="install-restify"></a>Instalação do Restify
Olá linha de comandos, altere o diretório demasiado`azuread`. Se hello `azuread` diretório não existe, criá-la.

`cd azuread` ou `mkdir azuread;`

Introduza Olá os seguintes comandos:

`npm install restify`

Este comando instala o Restify.

#### <a name="did-you-get-an-error"></a>Obteve um erro?
Em alguns sistemas operativos, quando utiliza `npm`, poderá receber o erro de Olá `Error: EPERM, chmod '/usr/local/bin/..'` e um pedido para que execute conta Olá como administrador. Se o problema ocorrer, utilize Olá `sudo` comando toorun `npm` a um nível de privilégio mais elevado.

#### <a name="did-you-get-a-dtrace-error"></a>Obteve um erro de DTrace?
Quando instalar o Restify, pode aparecer o seguinte texto:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

O Restify fornece um mecanismo poderoso para rastreio de chamadas REST utilizando o DTrace. No entanto, muitos sistemas operativos não tem o DTrace disponível. Pode ignorar com segurança estes erros.

saída de Olá do comando de Olá deve aparecer semelhante toothis texto:

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Instalar o Passport na API Web
Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá.

Instale o Passport utilizando Olá os seguintes comandos:

`npm install passport`

saída de Olá do comando de Olá deve ser semelhante toothis texto:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Adicionar passport-azuread tooyour web API
Em seguida, adicione a estratégia de OAuth Olá utilizando `passport-azuread`, um conjunto de estratégias que ligam o Azure AD com o Passport. Utilize esta estratégia para os tokens de portador no exemplo de REST API de Olá.

> [!NOTE]
> Embora o OAuth2 forneça uma estrutura onde pode ser emitido qualquer tipo de token conhecido, apenas alguns tipos de tokens passaram a ser amplamente utilizados. tokens de Olá para proteger os pontos finais são tokens de portador. Estes tipos de tokens são Olá amplamente emitido no OAuth2. Várias implementações partem do princípio de que os tokens de portador são o único tipo de Olá de token emitido.
>
>

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá.

Instalar Olá Passport `passport-azure-ad` módulo Olá os seguintes comandos a utilizar:

`npm install passport-azure-ad`

saída de Olá do comando de Olá deve ser semelhante toothis texto:

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Adicionar API web do MongoDB módulos tooyour
Este exemplo utiliza o MongoDB como arquivo de dados. Para tal, instale o Mongoose, um plug-in de gestão de modelos e esquemas muito utilizado.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Instalar módulos adicionais
Em seguida, instale Olá restantes módulos necessários.

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

Instalar módulos Olá no seu `node_modules` diretório:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Crie um ficheiro de server.js com as suas dependências
Olá `server.js` ficheiro fornece maioria Olá da funcionalidade de Olá para o servidor de Web API.

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

Crie um ficheiro `server.js` num editor. Adicione Olá seguintes informações:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Guarde o ficheiro de Olá. Devolver tooit mais tarde.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Criar um toostore do ficheiro de config.js as definições do Azure AD
Este ficheiro de código transmite os parâmetros de configuração de Olá do seu Portal do Azure AD toohello `Passport.js` ficheiro. Criou estes valores de configuração quando adicionou o portal de toohello Olá web API na Olá primeira parte passagem Olá. Vamos explicar que tooput valores Olá destes parâmetros depois de copiar o código de Olá.

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

Crie um ficheiro `config.js` num editor. Adicione Olá seguintes informações:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Valores necessários
`clientID`: Olá ID de cliente da aplicação Web API.

`IdentityMetadata`: Aqui é onde `passport-azure-ad` procura dos seus dados de configuração para o fornecedor de identidade Olá. Procura também para Olá chaves toovalidate Olá JSON web de tokens.

`audience`: Olá identificador de recurso uniforme (URI) do portal de Olá que identifica a sua aplicação de chamada.

`tenantName`: o nome do seu inquilino (por exemplo, **contoso.onmicrosoft.com**).

`policyName`: Olá política que pretende que os tokens de Olá toovalidate futuras do servidor de tooyour. Esta política deve ser Olá a mesma política que utiliza numa aplicação de cliente Olá para início de sessão.

> [!NOTE]
> Por agora, utilize Olá mesmo políticas em toda a configuração de cliente e servidor. Se já tiver concluído uma passagem e criado estas políticas, não precisa de toodo, por isso, novamente. Uma vez concluída a passagem de Olá, não deverá ser preciso tooset configurar novas políticas para passagens de cliente no site de Olá.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Adicione o ficheiro de server.js tooyour de configuração
valores de Olá tooread de Olá `config.js` de ficheiros que criou, adicione Olá `.config` ficheiro como um recurso necessário na sua aplicação e, em seguida, defina Olá variáveis globais toothose no Olá `config.js` documento.

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

Abra Olá `server.js` ficheiro num editor. Adicione Olá seguintes informações:

```Javascript
var config = require('./config');
```
Adicionar uma nova secção demasiado`server.js` que inclua Olá seguinte código:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Em seguida, vamos adicionar alguns marcadores de posição para os utilizadores Olá recebido do nosso aplicações chamadas.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Vamos avançar e criar também o nosso registo.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Adicionar informações de esquema e modelo do MongoDB de Olá utilizando o Mongoose
Olá preparação pays como colocar estes três ficheiros num serviço REST API.

Para esta passagem, utilize MongoDB toostore as suas tarefas, conforme debatido anteriormente.

No Olá `config.js` ficheiro, chamado a base de dados **tasklist**. Esse nome foi também o que colocou no final Olá Olá `mongoose_auth_local` URL de ligação. Não precisa de toocreate esta base de dados previamente no MongoDB. Cria a base de dados de Olá para si na execução de primeiro Olá da aplicação de servidor.

Depois de indicar servidor Olá que toouse de base de dados de MongoDB, terá de toowrite algumas modelo do código adicional toocreate Olá e o esquema para as tarefas de servidor.

### <a name="expand-hello-model"></a>Expanda o modelo de Olá
Este modelo de esquema é simples. Pode expandi-lo conforme necessário.

`owner`: Quem é atribuído toohello tarefas. Este objeto é uma **cadeia**.  

`Text`: tarefa Olá propriamente dita. Este objeto é uma **cadeia**.

`date`: data de Olá essa tarefa Olá deve ser concluída. Este objeto é uma **datetime**.

`completed`: Se a tarefa de Olá está concluída. Este objeto é um **Booleano**.

### <a name="create-hello-schema-in-hello-code"></a>Criar o esquema de Olá no código Olá
Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

Abra Olá `server.js` ficheiro num editor. Adicione Olá seguindo as informações abaixo entrada de configuração de Olá:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Cria o esquema de Olá pela primeira vez e, em seguida, criar um objeto de modelo que utilize toostore os dados em todo o Olá code quando definir o **rotas**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Adicionar rotas ao seu servidor de tarefas da API REST
Agora que tem um toowork de modelo de base de dados com, adicione rotas de Olá que utilizar para o servidor de REST API.

### <a name="about-routes-in-restify"></a>Sobre rotas no Restify
As rotas funcionam no Restify Olá mesma maneira que funcionam quando utilizarem a pilha de Express de Olá. Definir rotas utilizando Olá URI que espera toocall de aplicações de cliente Olá.

Um padrão normal para uma rota do Restify é:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

O Restify e o Express podem fornecer funcionalidades muito mais aprofundada, tais como, definir tipos de aplicações e efetuar encaminhamentos complexos para diferentes pontos finais. Para efeitos de Olá deste tutorial, iremos manter estas rotas simples.

#### <a name="add-default-routes-tooyour-server"></a>Adicionar servidor de tooyour de rotas predefinidas
Agora a adicionar rotas CRUD básicas Olá de **criar** e **lista** para a nossa API REST. Podem encontrar outras rotas de Olá `complete` ramo do exemplo Olá.

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

Abra Olá `server.js` ficheiro num editor. Abaixo entradas da base de dados de Olá efetuadas acima adicionar Olá seguintes informações:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}
```


#### <a name="add-error-handling-for-hello-routes"></a>Adicionar tratamento de erro para rotas de Olá
Adicione alguns processamento de erros para que possa comunicar quaisquer problemas que encontre toohello back-cliente de forma a que possa compreender.

Adicione Olá seguinte código:

```Javascript
///--- Errors for communicating something interesting back toohello client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="create-your-server"></a>Criar o seu servidor
Agora definiu a base de dados e colocou as rotas. Olá coisa toodo é a instância do servidor de Olá tooadd que gere as chamadas.

O restify e o Express fornecem personalização avançada para um servidor de REST API, mas vamos utilizar a configuração mais básica do Olá aqui.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Adicionar Olá rotas toohello servidor (sem autenticação)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Adicionar o servidor de REST API de tooyour de autenticação
Agora que um servidor de API REST está em execução, pode torná-lo útil em relação ao Azure AD.

Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Utilizar Olá OIDCBearerStrategy que está incluído no passport-azure-ad
> [!TIP]
> Quando escreve APIs, deve ligar sempre Olá dados toosomething exclusivo a partir do token de Olá que Olá utilizador não pode falsificar. Quando o servidor de Olá armazena itens ToDo, aparece, por isso, com base no Olá **oid** de utilizador de Olá no token de Olá (chamado através de token.oid), que passa no campo de proprietário"Olá". Este valor garante que apenas esse utilizador pode aceder aos próprios itens ToDo. Não há nenhuma exposição na Olá API de "proprietário", pelo que um utilizador externo pode pedir dos outros itens ToDo, mesmo que estejam autenticados.
>
>

Em seguida, utilize a estratégia de portador Olá que vem com `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

O Passport utiliza Olá mesmo padrão para todas as respetivas estratégias. Passe-o como uma `function()` que tem `token` e `done` como parâmetros. estratégia de Olá volta a tooyou depois-tem de fazer todo o trabalho. Deve armazenar o utilizador Olá e guardar o token de Olá, de modo que não seja necessário tooask-lo novamente.

> [!IMPORTANT]
> código de Olá acima aceita qualquer utilizador que tooauthenticate tooyour servidor. Este processo é conhecido como registo automático. Em servidores de produção, não permita que qualquer API de Olá de acesso de utilizadores sem primeiro passá-los através de um processo de registo. Este processo é normalmente padrão de Olá normal que vemos nas aplicações de consumidor que lhe permitem tooregister utilizando o Facebook, mas, em seguida, pedir-lhe que toofill informações adicionais. Se este programa não era um programa da linha de comandos, poderíamos extrair o e-mail de Olá do objeto de token de Olá que é devolvido e, em seguida, mais frequentes utilizadores toofill informações adicionais. Porque se trata de uma amostra, iremos adicioná-los tooan dentro da memória da base de dados.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Execute o tooverify de aplicação de servidor que as TI a rejeita
Pode utilizar `curl` toosee se tem agora proteção do OAuth2 nos seus pontos finais. Olá cabeçalhos devolvidos devem ser suficiente tootell que estão no caminho certo Olá.

Certifique-se de que a instância do MongoDB está em execução:

    $sudo mongodb

Alterar o diretório de toohello e o servidor de execução Olá:

    $ cd azuread
    $ node server.js

Numa nova janela de terminal, execute `curl`

Tente um POST básico:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Um erro 401 é resposta Olá que quiser. Indica que camada do Passport Olá está a tentar tooredirect toohello autorizar o ponto final.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Agora tem um serviço de API REST que utiliza o OAuth2
Tem implementada uma API REST utilizando o Restify e o OAuth! Tem agora código suficiente para que possam continuar toodevelop o serviço e criar neste exemplo. Fez tudo o que podia com este servidor sem utilizar um cliente compatível com o OAuth2. Para esse passo seguinte, utilize uma passagem adicional, como o nosso [ligar tooa web API utilizando o iOS com o B2C](active-directory-b2c-devquickstarts-ios.md) explicação passo a passo.

## <a name="next-steps"></a>Passos seguintes
Agora pode mover tópicos toomore avançada, tais como:

[Ligar tooa web API utilizando o iOS com o B2C](active-directory-b2c-devquickstarts-ios.md)
