---
title: "aaaAzure AD v2 Android introdução - utilização | Microsoft Docs"
description: "Como uma aplicação Android pode obter um token de acesso e chamar Graph API do Microsoft ou de APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2"
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
ms.custom: aaddev
ms.openlocfilehash: 4480d89eb7638fe7d588c8cebd2b1e3c9d4c6e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilizar Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API

1.  Abra: `MainActivity` (em `app`  >  `java`  >  `{domain}.{appname}`)
2.  Adicione Olá seguintes importações:

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Substitua Olá `MainActivity` classe com abaixo:
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter hello application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt tooget a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined toohandle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined toohandle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in hello cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need toodo an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store hello authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use hello access
         * token toocall hello Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store hello auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set hello UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL tooacquireToken for hello end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles hello redirect from hello System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a>Mais Informações
#### <a name="getting-a-user-token-interactive"></a>Obter um token de utilizador interativa
Chamar Olá `AcquireTokenAsync` resultados de método numa janela solicitando Olá toosign de utilizador no. Aplicações normalmente necessitam de um utilizador toosign no interativamente Olá pela primeira vez que precisam tooaccess um recurso protegido ou quando uma operação automática tooacquire um token de falha (por exemplo, palavra-passe do utilizador Olá expirou).

#### <a name="getting-a-user-token-silently"></a>A obter um utilizador token automaticamente
`AcquireTokenSilentAsync`processa aquisições token e a renovação sem qualquer interação do utilizador. Depois de `AcquireTokenAsync` é executado para Olá pela primeira vez, `AcquireTokenSilentAsync` Olá método utilizado normalmente tooobtain tokens tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.
Eventualmente, `AcquireTokenSilentAsync` falhará – por exemplo, o utilizador Olá foi terminada, ou foi alterada a palavra-passe noutro dispositivo. Quando MSAL Deteta que é possível resolver o problema de Olá exigindo uma ação interativa, é acionado um `MsalUiRequiredException`. A aplicação pode processar esta exceção de duas formas:

1.  Efetuar uma chamada contra `AcquireTokenAsync` imediatamente, que resulta num utilizador Olá toosign-na pedir. Este padrão é normalmente utilizado nas aplicações online em que não existe nenhum conteúdo offline na aplicação Olá disponíveis para Olá utilizador. Olá exemplo gerado por esta configuração orientada utiliza este padrão: pode vê-lo na Olá ação pela primeira vez que executar o exemplo de Olá: porque nenhum utilizador alguma vez utilizado a aplicação Olá, `PublicClientApp.Users.FirstOrDefault` irá conter um valor nulo e um `MsalUiRequiredException` exceção será emitida. Olá, código de exemplo de Olá, em seguida, identificadores Olá exceção ao chamar `AcquireTokenAsync` resultando num utilizador Olá toosign-na pedir.
2.  Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `AcquireTokenSilentAsync` numa altura posterior. Isto é normalmente utilizado quando o utilizador Olá tooaccess capaz de funcionalidade da aplicação Olá sem ser interrompidos - por exemplo, não há conteúdo offline na aplicação Olá. Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess, toorefresh Olá desatualizada informações ou para a aplicação pode decidir tooretry `AcquireTokenSilentAsync` quando a rede é restaurada após está temporariamente indisponível.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve
1.  Adicionar Olá os seguintes métodos para Olá `MainActivity` classe:

```java
/* Use Volley toomake an HTTP request toohello /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request toograph");

    /* Make sure we have a token toosend toograph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed tooput parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send tooUI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET tooQueue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets hello Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a>Mais informações sobre como efetuar uma chamada REST em relação a uma API protegida

Nesta aplicação de exemplo, `callGraphAPI` chamadas `getAccessToken` e, em seguida, faz com que um HTTP `GET` pedido contra um recurso que necessita de um token e devolve o conteúdo de Olá. Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*. Para este exemplo, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.
<!--end-collapse-->

## <a name="setup-sign-out"></a>Configuração do início de sessão

1.  Adicionar Olá os seguintes métodos para Olá `MainActivity` classe:

```java
/* Clears a user's tokens from hello cache.
 * Logically similar too"sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt tooget a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set hello UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a>Mais informações

`onSignOutClicked`acima remove hello utilizador da cache de utilizador MSAL – isto eficazmente informará o utilizador atual do MSAL tooforget Olá para que um pedido futuras tooacquire um token apenas terá êxito se este for efetuada toobe interativo.
Embora a aplicação Olá neste exemplo suporta um único utilizador, MSAL suporta cenários em que várias contas podem ser com sessão iniciada em Olá simultâneo – um exemplo é uma aplicação de e-mail em que um utilizador tem várias contas.
<!--end-collapse-->
