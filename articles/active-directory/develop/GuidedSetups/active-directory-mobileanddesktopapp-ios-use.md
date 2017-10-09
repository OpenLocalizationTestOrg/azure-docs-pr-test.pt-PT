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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilizar Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API

Abra `ViewController.swift` e substitua o código de Olá com:

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
### <a name="more-information"></a>Mais Informações
#### <a name="getting-a-user-token-interactively"></a>A obter um utilizador token interativamente
Chamar Olá `acquireToken` resultados do método na janela de browser pedir confirmação Olá toosign de utilizador no. Aplicações normalmente necessitam de um utilizador toosign no interativamente Olá pela primeira vez que precisam tooaccess um recurso protegido ou quando uma operação automática tooacquire um token de falha (por exemplo, palavra-passe do utilizador Olá expirou).

#### <a name="getting-a-user-token-silently"></a>A obter um utilizador token automaticamente
Olá `acquireTokenSilent` método processa aquisições token e a renovação sem qualquer interação do utilizador. Depois de `acquireToken` é executado para Olá pela primeira vez, `acquireTokenSilent` Olá método utilizado normalmente tooobtain tokens utilizados tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.

Eventualmente, `acquireTokenSilent` falhará – por exemplo, o utilizador Olá foi terminada, ou foi alterada a palavra-passe noutro dispositivo. Quando MSAL Deteta que é possível resolver o problema de Olá exigindo uma ação interativa, é acionado um `MSALErrorCode.interactionRequired` exceção. A aplicação pode processar esta exceção de duas formas:

1.  Efetuar uma chamada contra `acquireToken` imediatamente, resultando num pedir Olá toosign de utilizador no. Este padrão é normalmente utilizado nas aplicações online em que não existe nenhum conteúdo offline na aplicação Olá disponíveis para Olá utilizador. aplicação de exemplo de Olá gerada por esta configuração orientada utiliza este padrão: pode vê-lo na Olá ação pela primeira vez que executar a aplicação Olá. Porque nenhum utilizador alguma vez utilizado a aplicação Olá, `applicationContext.users().first` irá conter um valor nulo e um ` MSALErrorCode.interactionRequired ` exceção será emitida. Olá, código de exemplo de Olá, em seguida, identificadores Olá exceção ao chamar `acquireToken` resultavam pedir Olá utilizador toosign no.

2.  Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `acquireTokenSilent` numa altura posterior. Isto é normalmente utilizado quando o utilizador Olá pode utilizar outras funcionalidades da aplicação Olá sem ser interrompidos, por exemplo, não há conteúdo offline na aplicação Olá. Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess, toorefresh Olá desatualizada informações ou para a aplicação pode decidir tooretry `acquireTokenSilent` quando a rede é restaurada após está temporariamente indisponível.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve

Adicionar Olá novo método abaixo demasiado`ViewController.swift`. Este método é toomake utilizado um `GET` pedido contra a utilização de Microsoft Graph API Olá um *cabeçalho de autorização de HTTP*:

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
### <a name="making-a-rest-call-against-a-protected-api"></a>Efetuar uma chamada REST em relação a uma API protegida

Esta aplicação de exemplo Olá `getContentWithToken()` método é utilizado toomake um HTTP `GET` pedido contra um recurso protegido que necessita de um autor da chamada do token e, em seguida, retorno Olá toohello conteúdo. Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*. Para este exemplo, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Configurar a fim de sessão

Adicionar Olá seguinte método demasiado`ViewController.swift` toosign saída utilizador Olá:

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
### <a name="more-info-on-sign-out"></a>Obter mais informações sobre o fim de sessão

Olá `signoutButton` método Remove o utilizador Olá Olá cache de utilizador MSAL – isto eficazmente informará o utilizador atual do MSAL tooforget Olá para um pedido futuras tooacquire um token apenas terá êxito se este for efetuada toobe interativo.

Embora a aplicação Olá neste exemplo suporta um único utilizador, MSAL suporta cenários em que várias contas podem ter sessão iniciadas em Olá simultâneo – um exemplo é uma aplicação de e-mail em que um utilizador tem várias contas.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Registar a chamada de retorno Olá

Assim que autentica o utilizador Olá, o browser Olá redireciona Olá aplicação de back-toohello do utilizador. Siga os passos de Olá abaixo tooregister esta chamada de retorno:

1.  Abra `AppDelegate.swift` e importar MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Adicionar Olá seguinte método tooyour <code>AppDelegate</code> toohandle chamadas de retorno de classe:
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

