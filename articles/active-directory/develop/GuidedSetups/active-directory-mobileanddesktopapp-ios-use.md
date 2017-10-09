---
title: "aaaAzure AD v2 iOS introdução - utilização | Microsoft Docs"
description: "Como as aplicações do iOS (Swift) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="9c328-103">Utilizar Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="9c328-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="9c328-104">Abra `ViewController.swift` e substitua o código de Olá com:</span><span class="sxs-lookup"><span data-stu-id="9c328-104">Open `ViewController.swift` and replace hello code with:</span></span>

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="9c328-105">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="9c328-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="9c328-106">A obter um utilizador token interativamente</span><span class="sxs-lookup"><span data-stu-id="9c328-106">Getting a user token interactively</span></span>
<span data-ttu-id="9c328-107">Chamar Olá `acquireToken` resultados do método na janela de browser pedir confirmação Olá toosign de utilizador no.</span><span class="sxs-lookup"><span data-stu-id="9c328-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="9c328-108">Aplicações normalmente necessitam de um utilizador toosign no interativamente Olá pela primeira vez que precisam tooaccess um recurso protegido ou quando uma operação automática tooacquire um token de falha (por exemplo, palavra-passe do utilizador Olá expirou).</span><span class="sxs-lookup"><span data-stu-id="9c328-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="9c328-109">A obter um utilizador token automaticamente</span><span class="sxs-lookup"><span data-stu-id="9c328-109">Getting a user token silently</span></span>
<span data-ttu-id="9c328-110">Olá `acquireTokenSilent` método processa aquisições token e a renovação sem qualquer interação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="9c328-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="9c328-111">Depois de `acquireToken` é executado para Olá pela primeira vez, `acquireTokenSilent` Olá método utilizado normalmente tooobtain tokens utilizados tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c328-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="9c328-112">Eventualmente, `acquireTokenSilent` falhará – por exemplo, o utilizador Olá foi terminada, ou foi alterada a palavra-passe noutro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c328-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="9c328-113">Quando MSAL Deteta que é possível resolver o problema de Olá exigindo uma ação interativa, é acionado um `MSALErrorCode.interactionRequired` exceção.</span><span class="sxs-lookup"><span data-stu-id="9c328-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="9c328-114">A aplicação pode processar esta exceção de duas formas:</span><span class="sxs-lookup"><span data-stu-id="9c328-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="9c328-115">Efetuar uma chamada contra `acquireToken` imediatamente, resultando num pedir Olá toosign de utilizador no.</span><span class="sxs-lookup"><span data-stu-id="9c328-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="9c328-116">Este padrão é normalmente utilizado nas aplicações online em que não existe nenhum conteúdo offline na aplicação Olá disponíveis para Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="9c328-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="9c328-117">aplicação de exemplo de Olá gerada por esta configuração orientada utiliza este padrão: pode vê-lo na Olá ação pela primeira vez que executar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9c328-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="9c328-118">Porque nenhum utilizador alguma vez utilizado a aplicação Olá, `applicationContext.users().first` irá conter um valor nulo e um ` MSALErrorCode.interactionRequired ` exceção será emitida.</span><span class="sxs-lookup"><span data-stu-id="9c328-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="9c328-119">Olá, código de exemplo de Olá, em seguida, identificadores Olá exceção ao chamar `acquireToken` resultavam pedir Olá utilizador toosign no.</span><span class="sxs-lookup"><span data-stu-id="9c328-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="9c328-120">Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `acquireTokenSilent` numa altura posterior.</span><span class="sxs-lookup"><span data-stu-id="9c328-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="9c328-121">Isto é normalmente utilizado quando o utilizador Olá pode utilizar outras funcionalidades da aplicação Olá sem ser interrompidos, por exemplo, não há conteúdo offline na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9c328-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="9c328-122">Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess, toorefresh Olá desatualizada informações ou para a aplicação pode decidir tooretry `acquireTokenSilent` quando a rede é restaurada após está temporariamente indisponível.</span><span class="sxs-lookup"><span data-stu-id="9c328-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="9c328-123">Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve</span><span class="sxs-lookup"><span data-stu-id="9c328-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="9c328-124">Adicionar Olá novo método abaixo demasiado`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="9c328-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="9c328-125">Este método é toomake utilizado um `GET` pedido contra a utilização de Microsoft Graph API Olá um *cabeçalho de autorização de HTTP*:</span><span class="sxs-lookup"><span data-stu-id="9c328-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="9c328-126">Efetuar uma chamada REST em relação a uma API protegida</span><span class="sxs-lookup"><span data-stu-id="9c328-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="9c328-127">Esta aplicação de exemplo Olá `getContentWithToken()` método é utilizado toomake um HTTP `GET` pedido contra um recurso protegido que necessita de um autor da chamada do token e, em seguida, retorno Olá toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9c328-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="9c328-128">Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*.</span><span class="sxs-lookup"><span data-stu-id="9c328-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="9c328-129">Para este exemplo, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="9c328-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="9c328-130">Configurar a fim de sessão</span><span class="sxs-lookup"><span data-stu-id="9c328-130">Set up sign-out</span></span>

<span data-ttu-id="9c328-131">Adicionar Olá seguinte método demasiado`ViewController.swift` toosign saída utilizador Olá:</span><span class="sxs-lookup"><span data-stu-id="9c328-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="9c328-132">Obter mais informações sobre o fim de sessão</span><span class="sxs-lookup"><span data-stu-id="9c328-132">More info on sign-out</span></span>

<span data-ttu-id="9c328-133">Olá `signoutButton` método Remove o utilizador Olá Olá cache de utilizador MSAL – isto eficazmente informará o utilizador atual do MSAL tooforget Olá para um pedido futuras tooacquire um token apenas terá êxito se este for efetuada toobe interativo.</span><span class="sxs-lookup"><span data-stu-id="9c328-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="9c328-134">Embora a aplicação Olá neste exemplo suporta um único utilizador, MSAL suporta cenários em que várias contas podem ter sessão iniciadas em Olá simultâneo – um exemplo é uma aplicação de e-mail em que um utilizador tem várias contas.</span><span class="sxs-lookup"><span data-stu-id="9c328-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="9c328-135">Registar a chamada de retorno Olá</span><span class="sxs-lookup"><span data-stu-id="9c328-135">Register hello callback</span></span>

<span data-ttu-id="9c328-136">Assim que autentica o utilizador Olá, o browser Olá redireciona Olá aplicação de back-toohello do utilizador.</span><span class="sxs-lookup"><span data-stu-id="9c328-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="9c328-137">Siga os passos de Olá abaixo tooregister esta chamada de retorno:</span><span class="sxs-lookup"><span data-stu-id="9c328-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="9c328-138">Abra `AppDelegate.swift` e importar MSAL:</span><span class="sxs-lookup"><span data-stu-id="9c328-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="9c328-139">Adicionar Olá seguinte método tooyour <code>AppDelegate</code> toohandle chamadas de retorno de classe:</span><span class="sxs-lookup"><span data-stu-id="9c328-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

