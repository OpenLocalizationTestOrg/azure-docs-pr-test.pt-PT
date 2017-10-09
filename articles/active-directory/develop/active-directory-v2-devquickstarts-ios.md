---
title: "utilizando a aplicação aaaAdd início de sessão tooan iOS Olá ponto final de v 2.0 do Azure AD | Microsoft Docs"
description: "Como toobuild uma aplicação iOS que inicia sessão utilizadores com ambos os conta pessoal da Microsoft e contas profissionais ou escolares através da utilização de bibliotecas de terceiros."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Adicionar a aplicação do iOS de início de sessão tooan utilizando uma biblioteca de terceiros com Graph API utilizando o ponto final de v 2.0 Olá
plataforma de identidade do Microsoft Olá utiliza as normas de abertura, como o OAuth2 e o OpenID Connect. Os programadores podem utilizar qualquer biblioteca que pretendem toointegrate aos nossos serviços. os programadores de toohelp utilizam nossa plataforma com outras bibliotecas, escrevemos algumas instruções como esta um toodemonstrate como plataforma de identidade do Microsoft tooconnect toohello tooconfigure bibliotecas de terceiros. A maioria das bibliotecas que implementam [spec Olá especificação RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) pode ligar-se a plataforma de identidade do Microsoft toohello.

Com a aplicação Olá que cria esta explicação passo a passo, os utilizadores podem iniciar sessão tootheir organização e, em seguida, procure outras pessoas na sua organização utilizando Olá Graph API.

Se tiver tooOAuth2 novo ou o OpenID Connect, muito este exemplo de configuração poderá não fazer sentido tooyou. Recomendamos que leia [protocolos de v 2.0 - fluxo de código do OAuth 2.0 autorização](active-directory-v2-protocols-oauth-code.md) para em segundo plano.

> [!NOTE]
> Algumas funcionalidades da nossa plataforma que têm uma expressão num Olá OAuth2 ou o OpenID Connect normas, como o acesso condicional e gestão de políticas do Intune, requerem toouse nosso bibliotecas de identidade do Microsoft Azure de código aberto.
> 
> 

ponto final de v 2.0 Olá não suporta todos os cenários do Azure Active Directory e funcionalidades.

> [!NOTE]
> toodetermine se deve utilizar o ponto final de v 2.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Transferir o código a partir do GitHub
código Olá deste tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow ao longo, pode [transferir a estrutura da aplicação Olá como um. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou estrutura de Olá do clone:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

Pode também simplesmente transferir exemplo Olá e começar imediatamente:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Registar uma aplicação
Criar uma nova aplicação Olá [portal de registo de aplicação](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga Olá os passos detalhados em [como tooregister uma aplicação com o ponto final de v 2.0 Olá](active-directory-v2-app-registration.md).  Certifique-se de que:

* Olá cópia **Id da aplicação** que é atribuído tooyour aplicação porque irá precisar das mesmas em breve.
* Adicionar Olá **Mobile** plataforma para a sua aplicação.
* Olá cópia **URI de redirecionamento** do portal de Olá. Tem de utilizar o valor predefinido Olá `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Transferir Olá terceiros NXOAuth2 biblioteca e criar uma área de trabalho
Nestas instruções, irá utilizar Olá OAuth2Client do GitHub, o que é uma biblioteca OAuth2 para Mac OS X e iOS (Cocoa e Cocoa touch). Esta biblioteca é baseada no rascunho 10 da especificação do OAuth2 de Olá. Implementa o perfil de aplicação nativa Olá e suporta o ponto final de autorização de Olá do utilizador Olá. Estes são todos os aspetos de Olá, terá de toointegrate com a plataforma de identidade do Microsoft hello.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Adicione o projeto de tooyour da biblioteca de Olá utilizando o CocoaPods
O CocoaPods é um gestor de dependência para projetos do Xcode. Gere automaticamente os passos de instalação anterior Olá.

```
$ vi Podfile
```
1. Adicione Olá toothis podfile os seguintes:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Carregue o podfile Olá utilizando o CocoaPods. Isto irá criar uma área de trabalho Xcode nova que irá carregar.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Explorar a estrutura de Olá do projeto de Olá
Olá seguir a estrutura está configurado para o nosso projeto na estrutura de Olá:

* Uma vista principal com uma pesquisa UPN
* Uma vista de detalhes para os dados de Olá sobre o utilizador selecionado Olá
* Uma vista de início de sessão em que um utilizador pode iniciar sessão no gráfico de Olá toohello aplicação tooquery

Iremos irá mover ficheiros toovarious na autenticação de estrutura tooadd Olá. Outras partes do código Olá, tais como o código visual Olá, não dizem respeito tooidentity mas são fornecidas por si.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Configurar o ficheiro de settings.plst Olá na biblioteca de Olá
* No projeto de início rápido de Olá, abra Olá `settings.plist` ficheiro. Substitua os valores de Olá de elementos Olá Olá secção tooreflect Olá os valores que utilizou na Olá portal do Azure. O código será referenciar estes valores, sempre que utiliza Olá biblioteca de autenticação do Active Directory.
  * Olá `clientId` é Olá ID de cliente da aplicação que copiou do portal de Olá.
  * Olá `redirectUri` é o URL de redirecionamento Olá desse portal Olá fornecido.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Configurar a biblioteca NXOAuth2Client de Olá no seu LoginViewController
biblioteca de NXOAuth2Client Olá requer tooget alguns valores de multimédia. Depois de concluir essa tarefa, pode utilizar Olá de adquiridas toocall token Olá Graph API. Porque `LoginView` será chamado sempre que precisamos tooauthenticate, faz sentido tooput valores de configuração no ficheiro toothat.

* Vamos adicionar alguns valores toohello `LoginViewController.m` contexto de Olá ficheiro tooset para autenticação e autorização. Detalhes sobre os valores de Olá siga código Olá.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Vamos ver detalhes sobre o código de Olá.

destina-se a primeira cadeia de Olá `scopes`.  Olá `User.Read` valor permite-lhe tooread Olá básico perfil Olá sessão do utilizador.

Pode saber mais sobre todos os âmbitos disponíveis Olá em [âmbitos de permissões de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Para `authURL`, `loginURL`, `bhh`, e `tokenURL`, deve utilizar valores de Olá fornecidos anteriormente. Se utilizar a open source para Olá bibliotecas de identidade do Microsoft Azure, iremos importar estes dados para si através do nosso ponto final de metadados. Iremos tiver terminado Olá trabalho de extrair estes valores para si.

Olá `keychain` valor é o contentor de Olá Olá biblioteca NXOAuth2Client irá utilizar toocreate toostore um keychain os tokens. Se quiser tooget-início de sessão único (SSO) em várias aplicações, pode especificar Olá mesmo keychain em cada uma das suas aplicações e solicitar a utilização de Olá desse keychain na elegibilidade do Xcode. Isto é explicado no Olá documentação da Apple.

rest Olá destes valores são biblioteca de Olá toouse necessária e criar locais para si contexto de toohello toocarry valores.

### <a name="create-a-url-cache"></a>Criar uma cache de URL
Dentro de `(void)viewDidLoad()`, sempre que é chamado após o carregamento da vista de Olá, hello seguinte código primes uma cache para utilização.

Adicione Olá seguinte código:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Criar um WebView para início de sessão
Um WebView pode pedir ao utilizador Olá fatores adicionais, como mensagem de texto SMS (se configurada) ou utilizador de toohello de mensagens de erro de retorno. Aqui configure Olá WebView e, em seguida, posterior escrita Olá código toohandle Olá chamadas de retorno que irão surgir no WebView do Olá dos serviços de identidade Olá.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Ignorar a autenticação de toohandle de métodos de WebView Olá
Olá tootell WebView o que acontece quando um utilizador precisa toosign no, tal como abordado anteriormente, pode colar Olá seguinte código.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Resultado do pedido de OAuth2 Olá Olá da toohandle do código de escrita
Olá seguinte código irá processar o redirectURL Olá devolve de Olá WebView. Se a autenticação não foi concluída com êxito, o código Olá tentará novamente. Entretanto, a biblioteca de Olá fornecerá erro Olá que pode ver na consola de Olá ou processar de forma assíncrona.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Configurar Olá contexto OAuth (denominada conta arquivo)
Aqui pode chamar `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` no arquivo de conta partilhada Olá para cada serviço que quiser Olá aplicação toobe capaz de tooaccess. tipo de conta Olá é uma cadeia que é utilizada como um identificador para um determinado serviço. Porque estão a aceder Olá Graph API, o código de Olá refere-se tooit como `"myGraphService"`. Em seguida, configure um observador que informará quando ocorrem alterações com o token de Olá. Depois de obter o token de Olá, devolver Olá utilizador back toohello `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Configurar Olá toosearch vista principal e apresentar utilizadores Olá Olá Graph API
Uma aplicação Master-View-Controller (MVC) que apresenta Olá devolvida dados na grelha de Olá ultrapassa o âmbito de Olá destas instruções e muitos tutoriais online explicam como toobuild um. Todos os este código é no ficheiro de estrutura de Olá. No entanto, terá de toodeal com algumas coisas nesta aplicação MVC:

* Intercetar quando um utilizador tipos algo no campo de pesquisa de Olá
* Fornecer um objeto de dados back-toohello MasterView para poder apresentar os resultados de Olá na grelha de Olá

Iremos executará as abaixo.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Adicionar um toosee de verificação se estiver a ser iniciado a sessão
aplicação Olá efetua pouco se utilizador Olá não está assinada, pelo que é toocheck inteligente se já existir um token na cache de Olá. Se não, redireciona toohello LoginView para Olá utilizador toosign no. Se recorda, Olá melhor forma toodo ações quando carrega uma vista é toouse Olá `viewDidLoad()` método Apple fornece-nos.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Atualizar Olá vista em tabela quando são recebidos dados
Quando Olá Graph API devolve dados, terá de dados de Olá toodisplay. De simplicidade, segue-se todos os tabela de Olá do Olá código tooupdate. Apenas pode colar valores direita Olá no seu código automático MVC.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Fornecer um Olá toocall de forma Graph API quando alguém tipos de campo de procura Olá
Quando um utilizador tipos uma pesquisa na caixa de Olá, terá de tooshove que através de toohello Graph API. Olá `GraphAPICaller` classe, que se compilam Olá código a seguir, separa a funcionalidade de pesquisa de Olá da apresentação de Olá. Por agora, vamos escrever código Olá feeds qualquer toohello de carateres de pesquisa Graph API. Podemos fazê-lo, fornecendo um método chamado `lookupInGraph`, que demora a cadeia de Olá que queremos toosearch para.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Escrever um Olá de tooaccess de classe de programa auxiliar Graph API
Este é o principal de Olá da nossa aplicação. Enquanto o resto Olá foi inserir o código no padrão MVC Olá predefinido da Apple, aqui é escrever gráfico do código tooquery Olá como utilizador Olá tipos e, em seguida, devolver os dados. Eis o código de Olá e uma explicação detalhada seguinte.

### <a name="create-a-new-objective-c-header-file"></a>Criar um novo ficheiro de cabeçalho de Objective C
Ficheiro de Olá nome `GraphAPICaller.h`e adicione Olá seguinte código.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Aqui pode ver que um método especificado demora uma cadeia e devolve um completionBlock. Este completionBlock, como o poderá ter adivinhado, irá atualizar Olá tabela, fornecendo um objeto com a dados preenchidos em tempo real como Olá pesquisas de utilizador.

### <a name="create-a-new-objective-c-file"></a>Criar um novo ficheiro de Objective C
Ficheiro de Olá nome `GraphAPICaller.m`e adicione Olá seguinte método.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

Passemos através deste método em detalhe.

núcleo de Olá deste código é no Olá `NXOAuth2Request`, método que utiliza parâmetros de Olá que que já definiu no ficheiro de settings.plist Olá.

Step-by-Olá primeiro passo é tooconstruct Olá direita gráfico na chamada à API. Porque está a chamar `/users`, especificar que acrescentando-resource de Graph API toohello juntamente com a versão de Olá. Faz sentido tooput estes num ficheiro de definições externo porque estes podem alterar-se à medida que evolui de Olá API.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Em seguida, terá de parâmetros de toospecify que também irá fornecer toohello chamada de API de gráfico. É *muito importante* que coloque os parâmetros de Olá num ponto final de recursos de Olá porque que é removida de todos os carateres conforming não URI no tempo de execução. Todo o código de consulta tem de ser fornecido nos parâmetros de Olá.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

É possível que repare isto chama um `convertParamsToDictionary` método que ainda não escritas ainda. Vamos fazer agora, por isso, no fim de Olá do ficheiro de Olá:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Em seguida, vamos utilizar Olá `NXOAuth2Request` fazer uma cópia de dados do método tooget de Olá API no formato JSON.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Por fim, vamos ver como regressar Olá dados toohello MasterViewController. dados de Olá devolve conforme serializado e tem de anular a serialização de toobe e carregar um objeto que Olá MainViewController pode consumir. Para esta finalidade, a estrutura de Olá tem um `User.m/h` ficheiro que cria um objeto de utilizador. Preencher esse objeto de utilizador com as informações de gráfico de Olá.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Executar o exemplo de Olá
Se tiver utilizado a estrutura de Olá ou seguidas juntamente com instruções de Olá que agora deve ser executada a sua aplicação. Iniciar o simulador de Olá e clique em **sessão** aplicação de Olá toouse.

## <a name="get-security-updates-for-our-product"></a>Obter as atualizações de segurança para o nosso produto
Aconselhamo-lo tooget notificações de quando os incidentes de segurança ocorrem, visitando Olá [TechCenter de segurança](https://technet.microsoft.com/security/dd252948) e subscrever tooSecurity SUBSCREVENDO os alertas.

