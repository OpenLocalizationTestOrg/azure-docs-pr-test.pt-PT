---
title: "aaaAzure AD Cordova introdução | Microsoft Docs"
description: "Como toobuild uma aplicação Cordova que se integra com o Azure AD para início de sessão e chama APIs do Azure AD protegida utilizando OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Integrar o Azure AD com um Apache aplicação Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Pode utilizar o Apache Cordova toodevelop HTML5/JavaScript as aplicações que podem ser executadas em dispositivos móveis, como aplicações nativas totalmente funcional. Com o Azure Active Directory (Azure AD), pode adicionar aplicações de Cordova de tooyour de capacidades de autenticação de nível empresarial.

Um plug-in de Cordova encapsula num wrapper do Azure AD SDKs nativas no iOS, Android, Loja Windows e Windows Phone. Ao utilizar que Plug-in, pode melhorar a sua aplicação toosupport início de sessão com contas do Windows Server Active Directory dos utilizadores, obter acesso tooOffice 365 e APIs do Azure e, inclusivamente ajudar a proteger chamadas tooyour própria personalizado API web.

Neste tutorial, iremos utilizar Olá Apache Cordova Plug-in para o Active Directory Authentication Library (ADAL) tooimprove uma aplicação simples adicionando Olá seguintes funcionalidades:

* Com apenas alguns linhas de código, autenticar um utilizador e obter um token.
* Utilize essa tooquery de Graph API do token tooinvoke Olá nesse diretório e apresentar resultados de Olá.  
* Utilize a autenticação de toominimize de cache de token ADAL Olá pede ao utilizador Olá.

toomake essas melhorias, tem de:

1. Registar uma aplicação com o Azure AD.
2. Adicione tokens de toorequest do código tooyour aplicação.
3. Adicionar código toouse Olá token para consultas Olá Graph API e ver os resultados.
4. Criar o projeto de implementação de Cordova Olá com todas as plataformas de Olá pretende tootarget, adicionar Olá Cordova ADAL Plug-in e testar a solução de Olá emuladores.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, precisa de:

* Um inquilino do Azure AD em que tenha uma conta com direitos de desenvolvimento de aplicações.
* Ambiente de desenvolvimento que tenha configurado toouse Apache Cordova.  

Se ainda tiver ambos configurar, avançar diretamente toostep 1.

Se não tiver um inquilino do Azure AD, utilize Olá [instruções sobre como tooget um](active-directory-howto-tenant.md).

Se não tiver Apache Cordova configurar no seu computador, instale o seguinte Olá:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (pode ser facilmente instalado através do Gestor de pacote NPM: `npm install -g cordova`)

Olá precedente instalações deverão funcionar tanto no Olá PC na Olá Mac.

Cada plataforma de destino apresenta diferentes pré-requisitos:

* toobuild e executar uma aplicação para Windows Tablet/PC ou Windows Phone:
  * Instalar [Visual Studio 2013 para Windows com a atualização 2 ou posterior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (rápida ou outra versão) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild e execute uma aplicação para iOS:

  * Instalar Xcode 6. x ou posterior. Transferência a partir da Olá [site Apple Developer](http://developer.apple.com/downloads) ou Olá [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Instalar [ios-sim](https://www.npmjs.org/package/ios-sim). Pode utilizá-lo aplicações de iOS toostart no simulador iOS Olá linha de comandos. (Pode instalá-lo facilmente através de Olá terminal: `npm install -g ios-sim`.)
* toobuild e executar uma aplicação para Android:

  * Instalar [Kit de desenvolvimento Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou posterior. Certifique-se `JAVA_HOME` (variável de ambiente) está corretamente definida de acordo com caminho de instalação do JDK toohello (por exemplo, c:\Programas\Microsoft Files\Java\jdk1.7.0_75).
  * Instalar [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) e adicione Olá `<android-sdk-location>\tools` localização (por exemplo, C:\tools\Android\android-sdk\tools) tooyour `PATH` variável de ambiente.
  * Abra o Gestor do Android SDK (por exemplo, através de Olá terminal: `android`) e instalar:
    * *Android 5.0.1 (API 21)* plataforma SDK
    * *Ferramentas de criação de SDK Android* versão 19.1.0 ou posterior
    * *Suporte Android repositório* (Extras)

  Olá Android SDK não fornece qualquer instância de emulador predefinido. Crie um executando `android avd` Olá terminal e, em seguida, selecionar **criar**, se pretender toorun Olá aplicação Android num emulador. Recomendamos um nível de API de 19 ou superior. Para mais informações sobre opções de emulador e a criação de Android no Olá, consulte [Gestor de AVD](http://developer.android.com/tools/help/avd-manager.html) no site do Android Olá.

## <a name="step-1-register-an-application-with-azure-ad"></a>Passo 1: Registar uma aplicação com o Azure AD
Este passo é opcional. Este tutorial fornece pré-aprovisionada valores que pode utilizar toosee Olá exemplo na ação sem efetuar qualquer aprovisionamento no seu próprio inquilino. No entanto, recomendamos que execute este passo e se familiarize com o processo de Olá, porque irá ser necessário quando criar as suas próprias aplicações.

O Azure AD emite tooonly de tokens conhecidos aplicações. Antes de poder utilizar o Azure AD da sua aplicação, terá de toocreate uma entrada para o mesmo no seu inquilino. tooregister uma nova aplicação no seu inquilino:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior Olá, clique em sua conta. No Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.
3. Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.
4. Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.
5. Siga as instruções de Olá e criar um **aplicação cliente nativa**. (Embora aplicações Cordova HTML com base, estamos a criar uma aplicação cliente nativa aqui. Olá **aplicação cliente nativa** tem de selecionar a opção ou aplicação Olá não funcionará.)
  * **Nome** descreve toousers sua aplicação.
  * **URI de redirecionamento** é Olá URI que tenha utilizado tooreturn tokens tooyour aplicação. Introduza **http://MyDirectorySearcherApp**.

Depois de concluir o registo, o Azure AD atribui uma aplicação de tooyour de ID de aplicação único. Irá precisar deste valor nas secções seguintes Olá. Pode encontrá-lo no separador de aplicação Olá de Olá aplicação criada recentemente.

toorun `DirSearchClient Sample`, conceder Olá recém-criado aplicação permissão tooquery Olá AD Graph API do Azure:

1. De Olá **definições** página, selecione **permissões obrigatórias**e, em seguida, selecione **adicionar**.  
2. Para Olá aplicação Azure Active Directory, selecione **Microsoft Graph** como Olá API e adicione Olá **acesso ao diretório de Olá como utilizador com sessão iniciada Olá** permissão em **delegados Permissões**.  Isto permite que o seu Olá tooquery da aplicação Graph API para os utilizadores.

## <a name="step-2-clone-hello-sample-app-repository"></a>Passo 2: Clonar o repositório de aplicação de exemplo de Olá
A partir da shell ou a linha de comandos, escreva Olá os seguintes comandos:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Passo 3: Criar a aplicação Cordova de Olá
Existem várias formas o toocreate Cordova aplicações. Neste tutorial, iremos utilizar o interface de linha de comandos do Olá Cordova (CLI).

1. A partir da shell ou a linha de comandos, escreva Olá os seguintes comandos:

        cordova create DirSearchClient

   Este comando cria estrutura de pastas de Olá e andaime para o projeto Cordova de Olá.

2. Mova toohello nova DirSearchClient pasta:

        cd .\DirSearchClient

3. Copie o conteúdo de Olá do projeto de arranque Olá na subpasta de www Olá utilizando um Gestor de ficheiros ou Olá seguinte comando na sua shell:

  * Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * MAC:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Adicione a lista branca Olá Plug-in. Isto é necessário para invocar Olá Graph API.

        cordova plugin add cordova-plugin-whitelist

5. Adicione todas as plataformas de Olá que pretende que o toosupport. toohave uma amostra de trabalho, terá de tooexecute pelo menos um dos seguintes comandos de Olá. Tenha em atenção que não ser capaz de tooemulate iOS no Windows ou emular Windows num Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Adicione Olá ADAL para o projeto de tooyour Plug-in Cordova:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Passo 4: Adicionar código tooauthenticate utilizadores e obter os tokens do Azure AD
aplicação Olá que estiver a desenvolver neste tutorial, irá fornecer uma funcionalidade de pesquisa de diretório simples. utilizador Olá pode, em seguida, escreva o alias de Olá de qualquer utilizador no diretório de Olá e visualizar alguns atributos básicos. projeto de arranque Olá contém uma definição de Olá da interface de utilizador básico Olá da aplicação Olá (em www/index.html) e andaime Olá que cablagem um evento de aplicações básica ciclos, enlaces de interface de utilizador e apresentar lógica (www/js/index.js) de resultados. Olá apenas restantes para a tarefa está lógica de Olá tooadd que implementa as tarefas de identidade.

Olá primeira coisa que precisa de toodo no seu código é introduzir os valores de protocolo de Olá que utiliza o Azure AD para identificar a sua aplicação e Olá recursos que o destino. Esses valores serão utilizados tooconstruct Olá pedidos de token mais tarde. Inserir Olá fragmento, Olá parte superior do ficheiro de index.js Olá os seguintes:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Olá `redirectUri` e `clientId` valores devem corresponder ao valores Olá que descrevem a sua aplicação no Azure AD. Pode encontrar as do Olá **configurar** separador Olá portal do Azure, como descrito no passo 1, anteriormente neste tutorial.

> [!NOTE]
> Se tiver optado por não registar uma nova aplicação no seu próprio inquilino, pode colar simplesmente valores Olá pré-configurada como está. Em seguida, pode ver que executar o exemplo Olá, embora sempre deve criar sua própria entrada para as aplicações que se destinam para produção.

Em seguida, adicione o código de pedido de token de Olá. Inserir Olá seguinte fragmento entre Olá `search` e `renderData` definições:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Vamos examinar essa função ao eliminar-a para baixo em duas partes principais.
Este exemplo está concebida toowork com nenhum inquilino, como toobeing oposição ao associada tooa um determinado. Utiliza Olá "/ comuns" ponto final, que permite Olá utilizador tooenter qualquer conta no momento de autenticação e direciona o inquilino de toohello Olá pedido onde pertence.

Esta primeira parte do método Olá inspeciona Olá ADAL cache toosee se um token já está armazenado. Se Sim, o método de Olá utiliza inquilinos olá onde o token de Olá provém para reinicializar ADAL. Isto é necessário tooavoid pedidos adicionais, porque Olá utilização de "/ comuns" sempre resulta num perguntar Olá utilizador tooenter uma nova conta.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
Olá segunda parte método Olá efetua o pedido de token adequada Olá. Olá `acquireTokenSilentAsync` método pede-lhe ADAL tooreturn um token Olá especificado recurso sem qualquer UX. a mostrar Que pode acontecer se a cache de Olá já tem um token de acesso adequado armazenado, ou se um token de atualização pode ser utilizados tooget um novo token de acesso sem que mostra a qualquer linha de comandos. Se que a tentativa falhar, iremos reverter `acquireTokenAsync`– que irá solicitar visibly Olá tooauthenticate de utilizador.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Agora que temos o token de Olá, iremos finally pode invocar Olá Graph API e executar a consulta de pesquisa de Olá que queremos. Inserir Olá seguinte fragmento abaixo Olá `authenticate` definição:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
ficheiros do ponto inicial de Olá indicado um UX simple para introduzir o alias do utilizador na caixa de texto. Este método utiliza esse valor tooconstruct uma consulta, combiná-la com o token de acesso de Olá, envia-as tooMicrosoft gráfico e analisar os resultados de Olá. Olá `renderData` método, já está presente no ficheiro de ponto inicial de Olá, trata-se de visualizar os resultados de Olá.

## <a name="step-5-run-hello-app"></a>Passo 5: Executar a aplicação Olá
A aplicação está toorun finally pronto. Funcionamento é simple: quando inicia a aplicação Olá, introduza alias Olá do utilizador Olá pretende toolook cópias de segurança e, em seguida, clique no botão de Olá. Lhe for pedida a autenticação. Após a autenticação com êxito e êxito pesquisa, são apresentados Olá os atributos de utilizador de Olá procurado.

Execuções subsequentes irão efetuar a pesquisa de Olá sem que mostra a qualquer linha de comandos, thanks presença toohello Olá anteriormente adquirir token na cache.

passos concreto de Olá para executar a aplicação Olá variam consoante a plataforma.

### <a name="windows-10"></a>Windows 10
   Tablet/PC:`cordova run windows --archs=x64 -- --appx=uap`

   Dispositivo móvel (requer um tooa de dispositivo ligado do Windows 10 Mobile PC):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Durante a Olá executar pela primeira vez, ser pedido toosign numa licença de programador. Para obter mais informações, consulte [licença de programador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Windows 8.1 Tablet/PC
   `cordova run windows`

   > [!NOTE]
   > Durante a Olá executar pela primeira vez, ser pedido toosign numa licença de programador. Para obter mais informações, consulte [licença de programador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun num dispositivo ligado:`cordova run windows --device -- --phone`

   toorun no emulador do Olá predefinido:`cordova emulate windows -- --phone`

   Utilize `cordova run windows --list -- --phone` toosee todos os destinos disponíveis e `cordova run windows --target=<target_name> -- --phone` aplicação de Olá toorun num dispositivo específico ou emulador (por exemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun num dispositivo ligado:`cordova run android --device`

   toorun no emulador do Olá predefinido:`cordova emulate android`

   Certifique-se de que criou uma instância de emulador utilizando o Gestor de AVD, como descrito anteriormente Olá secção "Pré-requisitos".

   Utilize `cordova run android --list` toosee todos os destinos disponíveis e `cordova run android --target=<target_name>` aplicação de Olá toorun num dispositivo específico ou emulador (por exemplo, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun num dispositivo ligado:`cordova run ios --device`

   toorun no emulador do Olá predefinido:`cordova emulate ios`

   > [!NOTE]
   > Certifique-se de que tem Olá `ios-sim` toorun pacote instalado no emulador Olá. Para obter mais informações, consulte Olá "pré-requisitos" secção.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Passos seguintes
Para referência, está disponível no exemplo de Olá concluído (sem os valores de configuração) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Pode agora os cenários de movimentação em toomore avançadas (e mais interessante). É aconselhável tootry: [proteger uma API Web do Node.js com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
