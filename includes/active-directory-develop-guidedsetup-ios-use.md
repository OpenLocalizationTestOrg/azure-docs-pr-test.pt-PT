## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a>Utilizar a biblioteca de autenticação da Microsoft (MSAL) para obter um token para a Microsoft Graph API

Abra `ViewController.swift` e substitua o código com:

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
Chamar o `acquireToken` método resulta numa janela do browser pedir ao utilizador para iniciar sessão. Aplicações normalmente necessitam de um utilizador iniciar sessão interativamente na primeira vez que necessitam para aceder a recursos protegidos, ou quando uma operação automática ao adquirir um token falhar (por exemplo, palavra-passe do utilizador expirou).

#### <a name="getting-a-user-token-silently"></a>A obter um utilizador token automaticamente
O `acquireTokenSilent` método processa aquisições token e a renovação sem qualquer interação do utilizador. Depois de `acquireToken` é executado pela primeira vez, `acquireTokenSilent` é o método costuma ser utilizado para obter os tokens utilizados para aceder a recursos protegidos para chamadas subsequentes - como as chamadas para pedir ou renovar tokens são efetuadas automaticamente.

Eventualmente, `acquireTokenSilent` falhará – por exemplo, o utilizador foi terminada, ou foi alterada a palavra-passe noutro dispositivo. Quando MSAL Deteta que é possível resolver o problema, exigindo que uma ação interativa, é acionado um `MSALErrorCode.interactionRequired` exceção. A aplicação pode processar esta exceção de duas formas:

1.  Efetuar uma chamada contra `acquireToken` imediatamente, o que resulta numa pedir ao utilizador para iniciar sessão. Este padrão é normalmente utilizado nas aplicações online em que não existe nenhum conteúdo offline na aplicação disponível para o utilizador. O exemplo de aplicação gerado por esta configuração orientada utiliza este padrão: pode vê-lo no prazo de ação primeiro executar a aplicação. Porque nenhum utilizador alguma vez utilizado a aplicação, `applicationContext.users().first` irá conter um valor nulo e um ` MSALErrorCode.interactionRequired ` exceção será emitida. O código no exemplo, em seguida, processa a exceção ao chamar `acquireToken` resultavam pedir ao utilizador para iniciar sessão.

2.  Aplicações também podem efetuar uma indicação de visual para o utilizador que um interativa início de sessão é necessário, para que o utilizador pode seleccionar no momento certo para iniciar sessão ou a aplicação pode tentar novamente `acquireTokenSilent` numa altura posterior. Isto é normalmente utilizado quando o utilizador pode utilizar outras funcionalidades da aplicação sem ser interrompidos - por exemplo, não há conteúdo offline na aplicação. Neste caso, o utilizador pode decidir quando pretende iniciar sessão para aceder ao recurso protegido ou para atualizar as informações Desatualizadas ou a aplicação pode decidir repetir `acquireTokenSilent` quando a rede é restaurada após está temporariamente indisponível.

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a>Chamar o Microsoft Graph API utilizando o token obtido apenas

Adicione o método novo abaixo para `ViewController.swift`. Este método é utilizado para efetuar um `GET` pedido contra a utilização de Microsoft Graph API um *cabeçalho de autorização de HTTP*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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

Nesta aplicação de exemplo, o `getContentWithToken()` método é utilizado para efetuar um HTTP `GET` contra um recurso protegido que necessita de um token de pedido e, em seguida, devolver o conteúdo para o autor da chamada. Este método adiciona o token adquirido no *cabeçalho de autorização de HTTP*. Para este exemplo, o recurso é o Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Configurar a fim de sessão

Adicione o seguinte método para `ViewController.swift` para terminar sessão de utilizador:

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Obter mais informações sobre o fim de sessão

O `signoutButton` método Remove o utilizador da cache de utilizador MSAL – isto eficazmente informará MSAL para se esqueça do utilizador atual para um pedido futuro para adquirir um token apenas terá êxito se for efetuada para ser interativo.

Apesar da aplicação neste exemplo suporta um único utilizador, MSAL suporta cenários em que várias contas podem ter sessão iniciadas em simultâneo – um exemplo é uma aplicação de e-mail em que um utilizador tem várias contas.
<!--end-collapse-->

## <a name="register-the-callback"></a>Registar a chamada de retorno

Depois do utilizador efetua a autenticação, o browser redireciona o utilizador novamente para a aplicação. Siga os passos abaixo para registar esta chamada de retorno:

1.  Abra `AppDelegate.swift` e importar MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Adicione o método seguinte à sua <code>AppDelegate</code> classe para processar as chamadas de retorno:
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

