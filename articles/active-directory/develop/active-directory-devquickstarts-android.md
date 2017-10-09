---
title: "aaaAzure AD Android introdução | Microsoft Docs"
description: "Como toobuild uma aplicação Android que se integra com o Azure AD para início de sessão e chamadas do Azure AD protegido APIs através da utilização de OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Integrar o Azure AD para uma aplicação Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Experimentar a pré-visualização de Olá do nosso novo [portal do programador](https://identity.microsoft.com/Docs/Android), que irá ajudar a começar a trabalhar com o Azure AD em apenas alguns minutos. portal do programador Olá irá guiá-lo através do processo de Olá de registar uma aplicação e a integração do Azure AD para o seu código. Quando tiver terminado, terá uma aplicação simples que pode autenticar utilizadores no seu inquilino e um back-end que podem aceitar tokens e efetuar a validação.
>
>

Se estiver a desenvolver uma aplicação de ambiente de trabalho, do Azure Active Directory (Azure AD) permite simples e fácil para tooauthenticate os utilizadores através das respetivas contas do Active Directory no local. Também permite que a aplicação toosecurely consumir qualquer API web protegida pelo Azure AD, tal como Olá APIs do Office 365 ou Olá API do Azure.

Para Android clientes que necessitam de recursos de tooaccess protegido, o Azure AD fornece Olá Active Directory Authentication Library (ADAL). Olá único objetivo ADAL é toomake-lo mais fácil para os tokens de acesso de tooget de aplicação. toodemonstrate como fácil é, iremos irá criar uma aplicação Android lista de tarefas que:

* Obtém acesso tokens para chamar uma API da lista de tarefas utilizando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Obtém a lista de tarefas de um utilizador.
* Inicia os utilizadores.

tooget iniciada, é necessário um inquilino do Azure AD, onde pode criar utilizadores e registar uma aplicação. Se ainda não tiver um inquilino, [Saiba como tooget um](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Passo 1: Transferir e executar o servidor de exemplo Olá TODO de API de REST do Node.js
exemplo de TODO de API de REST do Node.js Olá é escrito especificamente toowork no nosso exemplo existente para criar um API de REST de itens pendentes de único inquilino do Azure AD. Este é um pré-requisito para Olá início rápido.

Para obter informações sobre como tooset esta cópia de segurança, consulte o artigo nossos exemplos existentes no [serviço Microsoft Azure Active Directory exemplo REST API para Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Passo 2: Registar a API web no inquilino do Azure AD
Active Directory suporta a adição de dois tipos de aplicações:

- As APIs que oferecem toousers de serviços Web
- As aplicações (executado na web Olá ou num dispositivo) que aceder às APIs web

Neste passo, que está a registar Olá web API que estiver a executar localmente para este exemplo de teste. Normalmente, esta API web é um serviço REST que é a funcionalidade de oferta de que pretende que um tooaccess de aplicação. Azure AD pode ajudar a proteger qualquer ponto final.

Partimos do princípio que está a registar Olá API de REST de TODO referenciado anteriormente. Mas isto funciona para qualquer web API que pretende que o Azure Active Directory toohelp proteger.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior Olá, clique em sua conta. No Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.
3. Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.
4. Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.
5. Introduza um nome amigável para aplicação Olá (por exemplo, **TodoListService**), selecione **aplicação Web e/ou Web API**e clique em **seguinte**.
6. Para Olá início de sessão no URL, introduza o URL de base de Olá de exemplo de Olá. Por predefinição, este é `https://localhost:8080`.
7. Clique em **OK** registo de Olá toocomplete.
8. Enquanto ainda Olá portal do Azure, visite a página da aplicação tooyour, localizar o valor de ID de aplicação Olá e copiá-lo. Irá precisar deste mais tarde quando configurar a sua aplicação.
9. De Olá **definições** -> **propriedades** página, atualizar a aplicação Olá ID URI - introduza `https://<your_tenant_name>/TodoListService`. Substitua `<your_tenant_name>` com o nome de Olá do seu inquilino do Azure AD.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Passo 3: Registar a aplicação de cliente nativo Android de exemplo de Olá
Tem de registar a aplicação web neste exemplo. Isto permite que o seu toocommunicate de aplicação com Olá just-registado API web do. Azure AD irá refuse tooeven permitir tooask a aplicação de início de sessão, a menos que está registado. Que faz parte de segurança de Olá do modelo de Olá.

Partimos do princípio que está a registar a aplicação de exemplo de Olá referenciada anteriormente. Mas este procedimento funciona para qualquer aplicação que estiver a desenvolver.

> [!NOTE]
> Poderá wonder por que motivo está a colocar uma aplicação e uma API web no um inquilino. Como o poderá ter adivinhado, pode criar uma aplicação que acede a uma API externa que está registada no Azure AD a partir de outro inquilino. Se, fazê-lo, os seus clientes será solicitado tooconsent toohello utilização Olá API na aplicação Olá. Biblioteca de autenticação do Active Directory para iOS encarrega-se deste consentimento para si. Como podemos explorar as funcionalidades mais avançadas, verá que se trata de uma parte importante da suite Olá do Olá trabalho tooaccess necessárias das APIs do Microsoft Azure e Office, bem como qualquer outro fornecedor de serviços. Por agora, porque registado web API e a aplicação Olá mesmo inquilino, não verão qualquer pede consentimento. Isto é normalmente o caso de Olá se estiver a desenvolver uma aplicação apenas para sua própria toouse da empresa.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior Olá, clique em sua conta. No Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.
3. Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.
4. Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.
5. Introduza um nome amigável para aplicação Olá (por exemplo, **TodoListClient Android**), selecione **aplicação cliente nativa**e clique em **seguinte**.
6. Para Olá URI de redirecionamento, introduza `http://TodoListClient`. Clique em **Concluir**.
7. A partir da página da aplicação Olá, localize o valor de ID de aplicação Olá e copiá-lo. Irá precisar deste mais tarde quando configurar a sua aplicação.
8. De Olá **definições** página, selecione **permissões obrigatórias** e selecione **adicionar**.  Localize e selecione TodoListService, adicione Olá **acesso TodoListService** permissão em **permissões delegadas**e clique em **feito**.

toobuild com o Maven, pode utilizar pom.xml no nível superior Olá:

1. Este repositório do clone para um diretório da sua preferência:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Siga os passos de Olá Olá [pré-requisitos tooset configurar o ambiente de Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Configure o emulador de Olá com 19 de SDK.
4. Aceda toohello a pasta raiz onde clonou o repositório de Olá.
5. Execute este comando:`mvn clean install`
6. Alterar o exemplo Olá diretório toohello início rápido:`cd samples\hello`
7. Execute este comando:`mvn android:deploy android:run`

   Deverá ver a iniciar a aplicação Olá.
8. Introduza tootry de credenciais de utilizador de teste.

Pacotes JAR irão ser submetidos para além do pacote de AAR Olá.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Passo 4: Transferir Olá Android ADAL e adicione-a área de trabalho do tooyour Eclipse
Fizemos-lo mais fácil para toohave tem várias opções toouse ADAL no seu projeto Android:

* Pode utilizar tooimport de código de origem Olá nesta biblioteca na aplicação de tooyour Eclipse e a ligação.
* Se estiver a utilizar o Android Studio, pode utilizar Olá AAR pacote formato e referência Olá binários.

### <a name="option-1-source-zip"></a>Opção 1: Origem Zip
Clique em toodownload uma cópia do código de origem Olá, **transferir ZIP** no lado direito de Olá da página Olá. Ou pode [transferir a partir do GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Opção 2: Origem via Git
código de origem Olá tooget de Olá SDK através de Git, escreva:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Opção 3: Binários através do Gradle
Pode obter os binários de Olá do repositório central do Olá Maven. pacote de AAR Olá pode ser incluído forma no seu projeto no Android Studio:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Opção 4: AAR através do Maven
Se estiver a utilizar Olá M2Eclipse Plug-in, pode especificar a dependência de Olá no seu ficheiro pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Opção 5: Pacote JAR Olá libs pasta
Pode obter o ficheiro JAR de Olá do repositório de Maven Olá e solte-o no Olá **libs** pasta no seu projeto. Terá de projeto, de tooyour do toocopy Olá recursos necessários porque não incluem pacotes JAR Olá-los.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Passo 5: Adicionar o projeto do referências tooAndroid ADAL tooyour
1. Adicione um projeto de tooyour de referência e especificá-la como uma biblioteca do Android. Se estiver incerto como toodo, pode obter mais informações sobre Olá [site do Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Adicione dependência do projeto de Olá de depuração para as definições do projeto.
3. Atualize tooinclude de ficheiro do seu projeto AndroidManifest.xml:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Crie uma instância de AuthenticationContext a atividade principal. detalhes de Olá desta chamada estejam fora do âmbito Olá deste tópico, mas pode obter um bom ponto de partida ao observar Olá [exemplo Android Native Client](https://github.com/AzureADSamples/NativeClient-Android). No seguinte exemplo de Olá, SharedPreferences é cache predefinido de Olá e autoridade está no formato Olá `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Copie este código bloco toohandle Olá final AuthenticationActivity depois de recebe um código de autorização e introduz credenciais de utilizador de Olá:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask para obter um token, definir uma chamada de retorno:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Por fim, voltar a pedir um token utilizando esse chamada de retorno:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Eis uma explicação dos parâmetros de Olá:

* *recurso* é necessário e é recurso Olá que está a tentar tooaccess.
* *ClientID* é necessário e provém do Azure AD.
* *RedirectUri* não é necessário toobe fornecido para a chamada de acquireToken Olá. Pode configurar, como o nome do pacote.
* *PromptBehavior* ajuda tooask para cache de Olá tooskip de credenciais e o cookie.
* *chamada de retorno* for chamado depois do código de autorização de Olá é trocado para obter um token. Tem um objeto do AuthenticationResult, que tem um token de acesso, data expirou e ID as informações do token.
* *acquireTokenSilent* é opcional. Pode chamá-lo toohandle colocação em cache e atualização do token. Também fornece versão da sincronização Olá. Aceita *userId* como parâmetro.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Ao utilizar estas instruções, deve ter o que precisa de toosuccessfully integrar com o Azure Active Directory. Para obter mais exemplos de como este trabalhar, visite Olá AzureADSamples / repositório no GitHub.

## <a name="important-information"></a>Informações importantes
### <a name="customization"></a>Personalização
Os recursos de aplicação podem substituir os recursos do projeto de biblioteca. Isto acontece quando a aplicação está a ser criada. Por este motivo, pode personalizar autenticação atividade esquema Olá gosta. Ser se tookeep Olá ID controlos Olá esse ADAL utiliza (WebView).

### <a name="broker"></a>Mediador
aplicação de Portal da empresa do Microsoft Intune Olá fornece o componente de Mediador de Olá. é criada a conta de Olá na AccountManager. tipo de conta de Olá é "workaccount." AccountManager permite apenas uma única conta SSO. Cria um cookie SSO para utilizador Olá depois de concluir o desafio de dispositivo Olá para uma das aplicações de Olá.

ADAL utiliza a conta de Mediador de Olá se uma conta de utilizador é criada neste autenticador e optar por não tooskip-lo. Pode ignorar o utilizador de Mediador de Olá com:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

É necessário tooregister um RedirectUri especial para utilização do Mediador. RedirectUri está num formato de Olá de `msauth://packagename/Base64UrlencodedSignature`. Pode obter o RedirectUri para a sua aplicação através da utilização de Olá script brokerRedirectPrint.ps1 ou Olá API chamada mContext.getBrokerRedirectUri. a assinatura de Olá é tooyour relacionadas com certificados de assinatura.

modelo de Mediador atual Olá destina-se um utilizador. AuthenticationContext fornece utilizador de Mediador de Olá método tooget Olá API.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

O manifesto da aplicação deve ter Olá seguintes contas de AccountManager toouse de permissões. Para obter mais informações, consulte Olá [AccountManager informações no site do Android Olá](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>URL de autoridade e o AD FS
Serviços de Federação do Active Directory (AD FS) não é reconhecido como produção STS, para que precisa de tooturn da deteção de instância e transmita o valor false no construtor de AuthenticationContext Olá.

URL de autoridade de Olá necessita de uma instância de STS e um [nome do inquilino](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Consultar os itens da cache
ADAL fornece uma cache de predefinição na SharedPreferences com a cache de algumas simple funções de consulta. Pode aproveitar cache atual Olá AuthenticationContext utilizando:

    ITokenCacheStore cache = mContext.getCache();

Também pode fornecer a implementação de cache, se quiser toocustomize-lo.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Comportamento de aviso
ADAL fornece um comportamento de aviso de toospecify opção. PromptBehavior.Auto mostrará Olá IU se o token de atualização de Olá é inválido e são necessárias credenciais de utilizador. PromptBehavior.Always irá ignorar a utilização da cache de Olá e Mostrar sempre Olá IU.

### <a name="silent-token-request-from-cache-and-refresh"></a>Pedido de token automática da cache e atualizar
Um pedido de token automática não utiliza Olá IU pop-up e não necessita de uma atividade. Devolve um token da cache de Olá, se disponível. Se o token de Olá expirou, este método tenta toorefresh-lo. Se o token de atualização de Olá expirou ou falha, devolve AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Também pode efetuar uma sincronização chamar através deste método. Pode definir toocallback nulo ou utilizar acquireTokenSilentSync.

### <a name="diagnostics"></a>Diagnóstico
Estes são origens principais de Olá de informações para diagnosticar problemas:

* Exceções
* Registos
* Rastreios de rede

Tenha em atenção que os IDs de correlação são diagnóstico central toohello na biblioteca de Olá. Pode definir os IDs de correlação numa base por pedido, se quiser toocorrelate um ADAL pedido com outras operações no seu código. Se não definir um ID de correlação, ADAL irá gerar um aleatório. Registar todas as mensagens e chamadas de rede serão, em seguida, ser carimbo de data / com o ID de correlação Olá. Olá geradas automaticamente ID as alterações em cada pedido.

#### <a name="exceptions"></a>Exceções
Exceções são Olá primeiro diagnóstico. Vamos tentar tooprovide mensagens de erro úteis. Se encontrar um que não seja útil, ficheiro, um problema e informe-nos. Inclua informações de dispositivo como modelo e número SDK.

#### <a name="logs"></a>Registos
Pode configurar Olá biblioteca toogenerate mensagens de registo que pode utilizar toohelp diagnosticar problemas. Configurar o registo efetuando o seguinte Olá chamar tooconfigure uma chamada de retorno que ADAL utilizará toohand desativar cada mensagem do registo como é gerada.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

As mensagens podem ser escritas tooa o ficheiro de registo personalizado, conforme mostrado no Olá seguinte código. Infelizmente, não é possível padrão recuperá registos a partir de um dispositivo. Existem alguns serviços que podem ajudá-lo com esta. Também pode invent o suas próprias, tal como servidor de envio tooa de ficheiros de Olá.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Estes são os níveis de registo de Olá:
* Erro (exceções)
* Avisar (aviso)
* Informações (fins informações)
* Verboso (obter mais detalhes)

Definir o nível de registo de Olá como esta:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Todas as mensagens de registo são enviadas toologcat, em chamadas de retorno de registo personalizado de tooany de adição.
Pode obter um ficheiro de registo de tooa do logcat da seguinte forma:

    adb logcat > "C:\logmsg\logfile.txt"

 Para obter mais informações sobre os comandos adb, consulte Olá [logcat informações no site do Android Olá](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Rastreios de rede
Pode utilizar várias ferramentas toocapture Olá tráfego HTTP que gera ADAL.  Isto é mais útil se estiver familiarizado com Olá protocolo de OAuth ou se precisar de tooprovide informações de diagnóstico tooMicrosoft ou outros canais de suporte.

Fiddler é Olá ferramenta de rastreio de HTTP mais fácil. Seguinte de Olá utilize liga tooset-cópia de segurança toocorrectly registo ADAL tráfego de rede. Para obter uma ferramenta de rastreio, como o Fiddler ou Charles toobe útil, tem de configurá-lo toorecord não encriptada SSL tráfego.  

> [!NOTE]
> Os rastreios gerados desta forma poderão conter informações privilegiadas como tokens de acesso, nomes de utilizador e palavras-passe. Se estiver a utilizar contas de produção, não deve partilhe estes rastreios com terceiros. Se precisar de toosupply toosomeone um rastreio no suporte de tooget ordem, reproduza o problema de Olá utilizando uma conta temporária com nomes de utilizador e palavras-passe que não atenção a partilha.

* A partir do site de Telerik Olá: [definição de cópia de segurança Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* A partir do GitHub: [configurar regras de Fiddler da ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>Modo de caixa de diálogo
método de acquireToken Olá sem atividade suporta uma linha de comandos de caixa de diálogo.

### <a name="encryption"></a>Encriptação
ADAL encripta tokens Olá e arquivo na SharedPreferences por predefinição. Pode ver detalhes da Olá toosee Olá StorageHelper classe. Android introduzida Android Keystore 4.3 (18 de API) de armazenamento seguro de chaves privadas. ADAL utiliza esse para 18 de API e superiores. Se pretender toouse ADAL para versões do SDK inferiores, terá de tooprovide uma chave secreta no AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Desafio de portador do OAuth2
Olá AuthenticationParameters classe fornece funcionalidade tooget authorization_uri de Olá desafio de portador do OAuth2.

### <a name="session-cookies-in-webview"></a>Cookies de sessão no WebView
Android WebView não limpa cookies de sessão após a aplicação Olá está fechada. Pode processar que ao utilizar este código de exemplo:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Para obter mais informações sobre os cookies, consulte Olá [CookieSyncManager informações no site do Android Olá](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Substituições de recursos
biblioteca da ADAL Olá inclui cadeias inglês ProgressDialog mensagens. A aplicação deve substituí-los se pretender que as cadeias localizadas.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Caixa de diálogo NTLM
Versão da ADAL 1.1.0 suporta uma caixa de diálogo NTLM é processada através do evento onReceivedHttpAuthRequest Olá WebViewClient. Pode personalizar o esquema de Olá e cadeias de caixa de diálogo Olá.

### <a name="cross-app-sso"></a>SSO em várias aplicações
Saiba [como tooenable SSO em várias aplicações no Android utilizando ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
