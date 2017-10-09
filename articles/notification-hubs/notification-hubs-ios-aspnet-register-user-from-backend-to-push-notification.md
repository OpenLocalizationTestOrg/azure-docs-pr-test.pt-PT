---
title: "utilizador atual de Olá aaaRegister para notificações push utilizando a Web API | Microsoft Docs"
description: "Saiba como toorequest registo da notificação push numa aplicação iOS com Notification Hubs do Azure quando o registo é efetuado através da API Web do ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="9527c-103">Registar o utilizador atual do Olá para notificações push utilizando o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9527c-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9527c-104">iOS</span><span class="sxs-lookup"><span data-stu-id="9527c-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9527c-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="9527c-105">Overview</span></span>
<span data-ttu-id="9527c-106">Este tópico mostra como toorequest registo da notificação push com Notification Hubs do Azure quando o registo é efetuado através da API Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9527c-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="9527c-107">Este tópico expande tutorial Olá [notificar os utilizadores com os Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="9527c-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="9527c-108">Tem já tiver concluído os passos de Olá necessário no serviço móvel tutorial toocreate Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="9527c-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="9527c-109">Para obter mais informações sobre Olá notificar o cenário de utilizadores, consulte [notificar os utilizadores com os Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="9527c-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="9527c-110">Atualizar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="9527c-110">Update your app</span></span>
1. <span data-ttu-id="9527c-111">No seu MainStoryboard_iPhone.storyboard, adicione Olá seguintes componentes de biblioteca de objetos de Olá:</span><span class="sxs-lookup"><span data-stu-id="9527c-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="9527c-112">**Etiqueta**: "TooUser com os Hubs de notificação Push"</span><span class="sxs-lookup"><span data-stu-id="9527c-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="9527c-113">**Etiqueta**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="9527c-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="9527c-114">**Etiqueta**: "Utilizador"</span><span class="sxs-lookup"><span data-stu-id="9527c-114">**Label**: "User"</span></span>
   * <span data-ttu-id="9527c-115">**Campo de texto**: "Utilizador"</span><span class="sxs-lookup"><span data-stu-id="9527c-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="9527c-116">**Etiqueta**: "Password"</span><span class="sxs-lookup"><span data-stu-id="9527c-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="9527c-117">**Campo de texto**: "Password"</span><span class="sxs-lookup"><span data-stu-id="9527c-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="9527c-118">**Botão**: "Início de sessão"</span><span class="sxs-lookup"><span data-stu-id="9527c-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="9527c-119">Neste momento, o seu guião gráfico aparente ser Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9527c-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="9527c-120">No editor do Assistente de Olá, criar saídas para todos os controlos de Olá mudada-los, ligar os campos de texto de Olá com Olá controlador de vista (delegado) e criar um **ação** para Olá **início de sessão** botão.</span><span class="sxs-lookup"><span data-stu-id="9527c-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="9527c-121">Crie uma classe com o nome **DeviceInfo**, e Olá cópia seguinte código na secção de interface de Olá do ficheiro de Olá DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="9527c-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="9527c-122">Copie Olá código na secção de implementação de Olá do ficheiro de DeviceInfo.m Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9527c-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="9527c-123">No PushToUserAppDelegate.h, adicione Olá singleton de propriedade os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9527c-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="9527c-124">No Olá **didFinishLaunchingWithOptions** método PushToUserAppDelegate.m, adicionar Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="9527c-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="9527c-125">primeira linha de Olá inicializa Olá **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="9527c-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="9527c-126">Olá segundo linha começa Olá registo para as notificações push, que já está presente é já tiver concluído Olá [introdução aos Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="9527c-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="9527c-127">No PushToUserAppDelegate.m, implementa o método de Olá **didRegisterForRemoteNotificationsWithDeviceToken** no seu AppDelegate e adicione Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="9527c-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="9527c-128">Isto define o token do dispositivo Olá para o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="9527c-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9527c-129">Neste momento, não existe não deve ser quaisquer outras código neste método.</span><span class="sxs-lookup"><span data-stu-id="9527c-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="9527c-130">Se já tiver um toohello chamada **registerNativeWithDeviceToken** método que tenha sido adicionado aquando da conclusão Olá [introdução aos Hubs de notificação](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, tem comente ou remover que a chamada.</span><span class="sxs-lookup"><span data-stu-id="9527c-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="9527c-131">No ficheiro de PushToUserAppDelegate.m Olá, adicione Olá seguinte método do processador:</span><span class="sxs-lookup"><span data-stu-id="9527c-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="9527c-132">aplicação (nulo):(UIApplication *) aplicação didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", userInfo);   UIAlertView * alerta = [[UIAlertView alocação] initWithTitle:@"Notification" mensagem: [userInfo objectForKey:@"inAppMessage"] delegado: nil cancelButtonTitle: @ otherButtonTitles:nil "OK", nil];   [alerta Mostrar]; }</span><span class="sxs-lookup"><span data-stu-id="9527c-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="9527c-133">Este método apresenta um alerta no Olá IU quando a aplicação recebe notificações enquanto estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="9527c-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="9527c-134">Abrir Olá PushToUserViewController.m ficheiro e teclado Olá retorno em Olá implementação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9527c-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="9527c-135">No Olá **viewDidLoad** inicializar o método no ficheiro de PushToUserViewController.m Olá, etiqueta de installationId Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="9527c-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="9527c-136">Adicione Olá seguintes propriedades na interface na PushToUserViewController.m:</span><span class="sxs-lookup"><span data-stu-id="9527c-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="9527c-137">Em seguida, adicione Olá implementação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9527c-137">Then, add hello following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="9527c-138">Código seguinte Olá de cópia para Olá **início de sessão** método do processador criado pelo XCode:</span><span class="sxs-lookup"><span data-stu-id="9527c-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="9527c-139">Este método obtém um ID de instalação e o canal para notificações push e envia-, juntamente com o tipo de dispositivo Olá, toohello autenticado método Web API que cria um registo dos Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="9527c-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="9527c-140">Esta API Web foi definido na [notificar os utilizadores com os Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="9527c-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="9527c-141">Agora que hello aplicação de cliente foi atualizada, devolver toohello [notificar os utilizadores com os Notification Hubs] e atualizar as notificações de toosend do serviço móvel Olá com os Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="9527c-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificar os utilizadores com os Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet

[introdução aos Hubs de notificação]: /manage/services/notification-hubs/get-started-notification-hubs-ios
