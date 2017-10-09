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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="b1273-104">Os Notification Hubs do Azure Notificam Utilizadores do iOS com back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="b1273-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="b1273-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="b1273-105">Overview</span></span>
<span data-ttu-id="b1273-106">Suporte de notificação push no Azure permite-lhe tooaccess uma fácil de utilizar, multiplatform e infraestrutura push ampliada, o que simplifica bastante a implementação de Olá de notificações push para aplicações de consumidor e enterprise Mobile plataformas.</span><span class="sxs-lookup"><span data-stu-id="b1273-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="b1273-107">Este tutorial mostra como toouse Notification Hubs do Azure toosend push utilizador de aplicação específica tooa de notificações num dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="b1273-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="b1273-108">Um back-end de ASP.NET WebAPI end é utilizado tooauthenticate clientes e notificações de toogenerate, conforme mostrado no tópico de documentação de orientação Olá [registar de back-end da aplicação](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="b1273-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="b1273-109">Este tutorial parte do princípio de que criou e configurado o notification hub, conforme descrito em [introdução aos Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b1273-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="b1273-110">Este tutorial também é toohello pré-requisitos Olá [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1273-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="b1273-111">Se quiser toouse Mobile Apps como o serviço de back-end, consulte Olá [Mobile Apps introdução Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="b1273-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="b1273-112">Modificar a sua aplicação iOS</span><span class="sxs-lookup"><span data-stu-id="b1273-112">Modify your iOS app</span></span>
1. <span data-ttu-id="b1273-113">Aplicação de vista de página única Olá aberto que criou no Olá [introdução aos Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1273-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b1273-114">Nesta secção partimos do pressuposto que o projeto está configurado com um nome de organização vazio.</span><span class="sxs-lookup"><span data-stu-id="b1273-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="b1273-115">Caso contrário, terá de tooprepend os nomes de classe de tooall de nome de organização.</span><span class="sxs-lookup"><span data-stu-id="b1273-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="b1273-116">No seu Main.storyboard adicione componentes Olá mostrados Olá o captura de ecrã abaixo a partir da biblioteca de objetos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="b1273-117">**Nome de utilizador**: UITextField de A com o texto do marcador de posição, *introduza o nome de utilizador*, imediatamente abaixo Olá enviar etiqueta de resultados e toohello restrita à esquerda e com o botão direito margens e abaixo Olá enviar etiqueta de resultados.</span><span class="sxs-lookup"><span data-stu-id="b1273-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="b1273-118">**Palavra-passe**: UITextField de A com o texto do marcador de posição, *introduza a palavra-passe*, imediatamente beneath Olá campo de texto do nome de utilizador e toohello restrita à esquerda e o botão direito do rato margens e por baixo do campo de texto do nome de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="b1273-119">Verifique Olá **seguro de entrada de texto** opção em Olá atributo Inspector, *devolver chave*.</span><span class="sxs-lookup"><span data-stu-id="b1273-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="b1273-120">**Inicie sessão no**: A UIButton etiqueta imediatamente por baixo do campo de texto de palavra-passe Olá e desmarque Olá **ativado** opção em Olá atributos Inspector, *conteúdo de controlo*</span><span class="sxs-lookup"><span data-stu-id="b1273-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="b1273-121">**WNS**: etiqueta e o envio do comutador tooenable Olá notificação de serviço de notificação do Windows se foi a configuração num hub de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="b1273-122">Consulte Olá [Windows introdução](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1273-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="b1273-123">**GCM**: etiqueta e o envio do comutador tooenable Olá tooGoogle notificação Cloud Messaging se foi a configuração num hub de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="b1273-124">Consulte [Android introdução](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1273-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="b1273-125">**APNS**: etiqueta e o envio do comutador tooenable Olá notificação toohello serviço de notificação de plataforma Apple.</span><span class="sxs-lookup"><span data-stu-id="b1273-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="b1273-126">**Nome de utilizador Recipent**: UITextField de A com o texto do marcador de posição, *etiqueta de nome de utilizador de destinatário*, imediatamente abaixo Olá GCM etiqueta e toohello restrita à esquerda e direita margens e abaixo Olá GCM etiqueta.</span><span class="sxs-lookup"><span data-stu-id="b1273-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="b1273-127">Foram adicionados alguns componentes no Olá [introdução aos Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1273-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="b1273-128">**CTRL** arrastar dos componentes de Olá no Olá vista tooViewController.h e adicione estes saídas de novo.</span><span class="sxs-lookup"><span data-stu-id="b1273-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
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
2. <span data-ttu-id="b1273-129">No viewcontroller. H, adicione o seguinte de Olá `#define` imediatamente por baixo declarações de importação.</span><span class="sxs-lookup"><span data-stu-id="b1273-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="b1273-130">Olá Substitute *< introduzir o ponto final de back-end\>*  marcador Olá URL de destino que utilizou toodeploy back-end da aplicação na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="b1273-131">Por exemplo, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="b1273-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="b1273-132">No seu projeto, crie um novo **Cocoa Touch classe** denominado **RegisterClient** toointerface com Olá back-end ASP.NET que criou.</span><span class="sxs-lookup"><span data-stu-id="b1273-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="b1273-133">Criar a classe de Olá herdar `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="b1273-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="b1273-134">Em seguida, adicione o seguinte código no Olá RegisterClient.h de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="b1273-135">Olá RegisterClient.m atualizar Olá `@interface` secção:</span><span class="sxs-lookup"><span data-stu-id="b1273-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="b1273-136">Substitua Olá `@implementation` secção Olá RegisterClient.m com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="b1273-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="b1273-137">código de Olá acima implementa lógica Olá explicada no artigo de documentação de orientação Olá [registar de back-end da aplicação](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) utilizando NSURLSession tooperform REST chama tooyour back-end de aplicação e NSUserDefaults toolocally arquivo Olá registrationId devolvido pelo hub de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1273-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="b1273-138">Tenha em atenção que esta classe requer a respetiva propriedade **authorizationHeader** toobe na ordem toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="b1273-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="b1273-139">Esta propriedade é definida por Olá **ViewController** após o início de sessão de Olá de classe.</span><span class="sxs-lookup"><span data-stu-id="b1273-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="b1273-140">No viewcontroller. H, adicione um `#import` declaração para RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="b1273-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="b1273-141">Em seguida, adicione uma declaração de token do dispositivo Olá e referenciar tooa `RegisterClient` instância no Olá `@interface` secção:</span><span class="sxs-lookup"><span data-stu-id="b1273-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="b1273-142">No ViewController.m, adicione uma declaração de método private Olá `@interface` secção:</span><span class="sxs-lookup"><span data-stu-id="b1273-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="b1273-143">Olá fragmento seguinte não é um esquema de autenticação segura, deve substituir implementação Olá Olá **createAndSetAuthenticationHeaderWithUsername:AndPassword:** com o mecanismo de autenticação específicas. que gera um toobe de token de autenticação consumido por Olá register classe de cliente, por exemplo, OAuth, do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b1273-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="b1273-144">Em seguida, no Olá `@implementation` secção ViewController.m adicionar Olá seguinte código que adiciona a implementação de Olá para definição Olá dispositivo token e a autenticação de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="b1273-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="b1273-145">Tenha em atenção a como o token do dispositivo definição Olá permite Olá botão de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="b1273-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="b1273-146">Isto acontece porque como parte da ação de início de sessão de Olá, controlador de vista de Olá regista para notificações push com Olá back-end de aplicação.</span><span class="sxs-lookup"><span data-stu-id="b1273-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="b1273-147">Por conseguinte, não pretendemos início de sessão ação toobe acessível até o token do dispositivo Olá está corretamente configurada.</span><span class="sxs-lookup"><span data-stu-id="b1273-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="b1273-148">Pode desemparelhar Olá de início de sessão do registo de push Olá, desde que anterior Olá ocorre antes de Olá anterior será ignorada.</span><span class="sxs-lookup"><span data-stu-id="b1273-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="b1273-149">ViewController.m, utilizar Olá seguinte método da ação de fragmentos tooimplement Olá para sua **início de sessão** botão e um método toosend Olá notificação mensagem utilizando Olá back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b1273-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="b1273-150">(IBAction) LogInAction: remetente (id) {/ / criar o cabeçalho de autenticação e defina-o cliente NSString * nome de utilizador de registo = autónoma. UsernameField.text;   Palavra-passe NSString * = autónoma. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="b1273-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="b1273-151">[auto createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="b1273-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="b1273-152">__weak ViewController * selfie = Self;   [self.registerClient registerWithDeviceToken:self.deviceToken etiquetas: nil andCompletion:^(NSError* error) {Se (! erro) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered com êxito!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="b1273-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="b1273-153">-SendNotificationASPNETBackend (nulo): (NSString*) pns UsernameTag: (NSString*) usernameTag mensagem: (NSString*) mensagem {NSURLSession* sessão = [NSURLSession sessionWithConfiguration: [NSURLSessionConfiguration defaultSessionConfiguration] delegado: nil delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="b1273-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="b1273-154">Etiqueta de Olá pns e o nome de utilizador de passar como parâmetros com Olá REST URL toohello ASP.NET back-end nsurl que * requestURL = [nsurl que URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="b1273-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="b1273-155">NSMutableURLRequest * pedido = [NSMutableURLRequest requestWithURL:requestURL];    [setHTTPMethod:@"POST"pedido];</span><span class="sxs-lookup"><span data-stu-id="b1273-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="b1273-156">Obter hello mock authenticationheader do cliente de registar Olá NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"pedido];</span><span class="sxs-lookup"><span data-stu-id="b1273-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="b1273-157">Adicionar o corpo de mensagem de notificação de Olá [pedido setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [setHTTPBody do pedido: [mensagem dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="b1273-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="b1273-158">Executar a notificação de envio de Olá REST API no Olá ASP.NET back-end NSURLSessionDataTask * dataTask = [sessão dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *erro) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) resposta;        Se (erro | | httpResponse.statusCode! = 200) {NSString* Estado = [NSString stringWithFormat:@"Error estado para % @: % d\nError: %@\n", pns, httpResponse.statusCode, erro];            dispatch_async(dispatch_get_main_queue(), ^ {/ / acrescentar texto porque todos os 3 chamadas PNS podem também ter informações tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="b1273-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="b1273-159">}];    [dataTask retomar]; }</span><span class="sxs-lookup"><span data-stu-id="b1273-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="b1273-160">Atualizar a ação de Olá da Olá **Enviar notificação** botão toouse Olá ASP.NET back-end e enviar tooany PNS ativada por um comutador.</span><span class="sxs-lookup"><span data-stu-id="b1273-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="b1273-161">Na função **ViewDidLoad**, adicione Olá seguir a instância do tooinstantiate Olá RegisterClient e defina o delegado de Olá para os campos de texto.</span><span class="sxs-lookup"><span data-stu-id="b1273-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="b1273-162">Agora no **Appdelegate**, remova todos os conteúdos de Olá do método Olá **aplicação: didRegisterForPushNotificationWithDeviceToken:** e substitua-o com Olá seguir toomake Certifique-se que Olá vista controlador contém Olá mais recente token do dispositivo obtido a partir do APNs:</span><span class="sxs-lookup"><span data-stu-id="b1273-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="b1273-163">Por fim no **Appdelegate**, certifique-se de Olá método os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b1273-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="b1273-164">Olá teste aplicação</span><span class="sxs-lookup"><span data-stu-id="b1273-164">Test hello Application</span></span>
1. <span data-ttu-id="b1273-165">No XCode, execute a aplicação Olá num dispositivo iOS físico (emitir notificações não irão funcionar no simulador de Olá).</span><span class="sxs-lookup"><span data-stu-id="b1273-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="b1273-166">Na aplicação para iOS Olá IU, introduza um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="b1273-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="b1273-167">Estes podem ser qualquer cadeia, mas têm ambos de ser Olá mesmo valor da cadeia.</span><span class="sxs-lookup"><span data-stu-id="b1273-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="b1273-168">Em seguida, clique em **início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="b1273-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="b1273-169">Deverá ver um pop-up que o informa da êxito de registo.</span><span class="sxs-lookup"><span data-stu-id="b1273-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="b1273-170">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1273-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="b1273-171">No Olá **etiqueta de nome de utilizador de destinatário* texto campo, introduza a etiqueta de nome de utilizador de Olá utilizada com o registo de Olá a partir de outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1273-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="b1273-172">Introduza uma mensagem de notificação e clique em **Enviar notificação**.</span><span class="sxs-lookup"><span data-stu-id="b1273-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="b1273-173">Apenas os dispositivos de Olá que tem um registo com etiqueta de nome de utilizador destinatário Olá recebem a mensagem de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1273-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="b1273-174">É enviada apenas toothose utilizadores.</span><span class="sxs-lookup"><span data-stu-id="b1273-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
