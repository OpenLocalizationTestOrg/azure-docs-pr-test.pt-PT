---
title: aaaAzure notificar utilizadores dos Notification Hubs para iOS com back-end .NET
description: "Saiba como toosend push toousers de notificações no Azure. Exemplos de código escrito em Objective-C e Olá .NET API de back-end de Olá."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Os Notification Hubs do Azure Notificam Utilizadores do iOS com back-end do .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Descrição geral
Suporte de notificação push no Azure permite-lhe tooaccess uma fácil de utilizar, multiplatform e infraestrutura push ampliada, o que simplifica bastante a implementação de Olá de notificações push para aplicações de consumidor e enterprise Mobile plataformas. Este tutorial mostra como toouse Notification Hubs do Azure toosend push utilizador de aplicação específica tooa de notificações num dispositivo específico. Um back-end de ASP.NET WebAPI end é utilizado tooauthenticate clientes e notificações de toogenerate, conforme mostrado no tópico de documentação de orientação Olá [registar de back-end da aplicação](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> Este tutorial parte do princípio de que criou e configurado o notification hub, conforme descrito em [introdução aos Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). Este tutorial também é toohello pré-requisitos Olá [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.
> Se quiser toouse Mobile Apps como o serviço de back-end, consulte Olá [Mobile Apps introdução Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Modificar a sua aplicação iOS
1. Aplicação de vista de página única Olá aberto que criou no Olá [introdução aos Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.
   
   > [!NOTE]
   > Nesta secção partimos do pressuposto que o projeto está configurado com um nome de organização vazio. Caso contrário, terá de tooprepend os nomes de classe de tooall de nome de organização.
   > 
   > 
2. No seu Main.storyboard adicione componentes Olá mostrados Olá o captura de ecrã abaixo a partir da biblioteca de objetos de Olá.
   
    ![][1]
   
   * **Nome de utilizador**: UITextField de A com o texto do marcador de posição, *introduza o nome de utilizador*, imediatamente abaixo Olá enviar etiqueta de resultados e toohello restrita à esquerda e com o botão direito margens e abaixo Olá enviar etiqueta de resultados.
   * **Palavra-passe**: UITextField de A com o texto do marcador de posição, *introduza a palavra-passe*, imediatamente beneath Olá campo de texto do nome de utilizador e toohello restrita à esquerda e o botão direito do rato margens e por baixo do campo de texto do nome de utilizador Olá. Verifique Olá **seguro de entrada de texto** opção em Olá atributo Inspector, *devolver chave*.
   * **Inicie sessão no**: A UIButton etiqueta imediatamente por baixo do campo de texto de palavra-passe Olá e desmarque Olá **ativado** opção em Olá atributos Inspector, *conteúdo de controlo*
   * **WNS**: etiqueta e o envio do comutador tooenable Olá notificação de serviço de notificação do Windows se foi a configuração num hub de Olá. Consulte Olá [Windows introdução](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.
   * **GCM**: etiqueta e o envio do comutador tooenable Olá tooGoogle notificação Cloud Messaging se foi a configuração num hub de Olá. Consulte [Android introdução](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.
   * **APNS**: etiqueta e o envio do comutador tooenable Olá notificação toohello serviço de notificação de plataforma Apple.
   * **Nome de utilizador Recipent**: UITextField de A com o texto do marcador de posição, *etiqueta de nome de utilizador de destinatário*, imediatamente abaixo Olá GCM etiqueta e toohello restrita à esquerda e direita margens e abaixo Olá GCM etiqueta.

    Foram adicionados alguns componentes no Olá [introdução aos Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.

1. **CTRL** arrastar dos componentes de Olá no Olá vista tooViewController.h e adicione estes saídas de novo.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. No viewcontroller. H, adicione o seguinte de Olá `#define` imediatamente por baixo declarações de importação. Olá Substitute *< introduzir o ponto final de back-end\>*  marcador Olá URL de destino que utilizou toodeploy back-end da aplicação na secção anterior Olá. Por exemplo, *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. No seu projeto, crie um novo **Cocoa Touch classe** denominado **RegisterClient** toointerface com Olá back-end ASP.NET que criou. Criar a classe de Olá herdar `NSObject`. Em seguida, adicione o seguinte código no Olá RegisterClient.h de Olá.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Olá RegisterClient.m atualizar Olá `@interface` secção:
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Substitua Olá `@implementation` secção Olá RegisterClient.m com Olá seguinte código.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    código de Olá acima implementa lógica Olá explicada no artigo de documentação de orientação Olá [registar de back-end da aplicação](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) utilizando NSURLSession tooperform REST chama tooyour back-end de aplicação e NSUserDefaults toolocally arquivo Olá registrationId devolvido pelo hub de notificação de Olá.

    Tenha em atenção que esta classe requer a respetiva propriedade **authorizationHeader** toobe na ordem toowork corretamente. Esta propriedade é definida por Olá **ViewController** após o início de sessão de Olá de classe.

1. No viewcontroller. H, adicione um `#import` declaração para RegisterClient.h. Em seguida, adicione uma declaração de token do dispositivo Olá e referenciar tooa `RegisterClient` instância no Olá `@interface` secção:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. No ViewController.m, adicione uma declaração de método private Olá `@interface` secção:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Olá fragmento seguinte não é um esquema de autenticação segura, deve substituir implementação Olá Olá **createAndSetAuthenticationHeaderWithUsername:AndPassword:** com o mecanismo de autenticação específicas. que gera um toobe de token de autenticação consumido por Olá register classe de cliente, por exemplo, OAuth, do Active Directory.
> 
> 

1. Em seguida, no Olá `@implementation` secção ViewController.m adicionar Olá seguinte código que adiciona a implementação de Olá para definição Olá dispositivo token e a autenticação de cabeçalho.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    Tenha em atenção a como o token do dispositivo definição Olá permite Olá botão de início de sessão. Isto acontece porque como parte da ação de início de sessão de Olá, controlador de vista de Olá regista para notificações push com Olá back-end de aplicação. Por conseguinte, não pretendemos início de sessão ação toobe acessível até o token do dispositivo Olá está corretamente configurada. Pode desemparelhar Olá de início de sessão do registo de push Olá, desde que anterior Olá ocorre antes de Olá anterior será ignorada.
2. ViewController.m, utilizar Olá seguinte método da ação de fragmentos tooimplement Olá para sua **início de sessão** botão e um método toosend Olá notificação mensagem utilizando Olá back-end do ASP.NET.
   
       - (IBAction) LogInAction: remetente (id) {/ / criar o cabeçalho de autenticação e defina-o cliente NSString * nome de utilizador de registo = autónoma. UsernameField.text;   Palavra-passe NSString * = autónoma. PasswordField.text;
   
           [auto createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = Self;   [self.registerClient registerWithDeviceToken:self.deviceToken etiquetas: nil andCompletion:^(NSError* error) {Se (! erro) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered com êxito!"];});}}];}

        -SendNotificationASPNETBackend (nulo): (NSString*) pns UsernameTag: (NSString*) usernameTag mensagem: (NSString*) mensagem {NSURLSession* sessão = [NSURLSession sessionWithConfiguration: [NSURLSessionConfiguration defaultSessionConfiguration] delegado: nil delegateQueue:nil];

            Etiqueta de Olá pns e o nome de utilizador de passar como parâmetros com Olá REST URL toohello ASP.NET back-end nsurl que * requestURL = [nsurl que URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            NSMutableURLRequest * pedido = [NSMutableURLRequest requestWithURL:requestURL];    [setHTTPMethod:@"POST"pedido];

            Obter hello mock authenticationheader do cliente de registar Olá NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"pedido];

            Adicionar o corpo de mensagem de notificação de Olá [pedido setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [setHTTPBody do pedido: [mensagem dataUsingEncoding:NSUTF8StringEncoding]];

            Executar a notificação de envio de Olá REST API no Olá ASP.NET back-end NSURLSessionDataTask * dataTask = [sessão dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *erro) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) resposta;        Se (erro | | httpResponse.statusCode! = 200) {NSString* Estado = [NSString stringWithFormat:@"Error estado para % @: % d\nError: %@\n", pns, httpResponse.statusCode, erro];            dispatch_async(dispatch_get_main_queue(), ^ {/ / acrescentar texto porque todos os 3 chamadas PNS podem também ter informações tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask retomar]; }


1. Atualizar a ação de Olá da Olá **Enviar notificação** botão toouse Olá ASP.NET back-end e enviar tooany PNS ativada por um comutador.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. Na função **ViewDidLoad**, adicione Olá seguir a instância do tooinstantiate Olá RegisterClient e defina o delegado de Olá para os campos de texto.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Agora no **Appdelegate**, remova todos os conteúdos de Olá do método Olá **aplicação: didRegisterForPushNotificationWithDeviceToken:** e substitua-o com Olá seguir toomake Certifique-se que Olá vista controlador contém Olá mais recente token do dispositivo obtido a partir do APNs:
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Por fim no **Appdelegate**, certifique-se de Olá método os seguintes:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Olá teste aplicação
1. No XCode, execute a aplicação Olá num dispositivo iOS físico (emitir notificações não irão funcionar no simulador de Olá).
2. Na aplicação para iOS Olá IU, introduza um nome de utilizador e palavra-passe. Estes podem ser qualquer cadeia, mas têm ambos de ser Olá mesmo valor da cadeia. Em seguida, clique em **início de sessão**.
   
    ![][2]
3. Deverá ver um pop-up que o informa da êxito de registo. Clique em **OK**.
   
    ![][3]
4. No Olá **etiqueta de nome de utilizador de destinatário* texto campo, introduza a etiqueta de nome de utilizador de Olá utilizada com o registo de Olá a partir de outro dispositivo.
5. Introduza uma mensagem de notificação e clique em **Enviar notificação**.  Apenas os dispositivos de Olá que tem um registo com etiqueta de nome de utilizador destinatário Olá recebem a mensagem de notificação de saudação.  É enviada apenas toothose utilizadores.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
