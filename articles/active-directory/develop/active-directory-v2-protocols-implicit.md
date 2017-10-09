---
title: "aplicações de página única aaaSecure utilizando o fluxo implícito de v 2.0 Olá do Azure AD | Microsoft Docs"
description: "Criar aplicações web utilizando a implementação de v 2.0 do Azure AD de fluxo implícito Olá para aplicações de página única."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# v 2.0 protocolos - SPAs utilizando o fluxo implícito Olá
Com o ponto final de v 2.0 Olá, pode iniciar a sessão de utilizadores para as aplicações de página única com contas pessoais e trabalho/profissional da Microsoft.  Página única e outras aplicações de JavaScript que execute principalmente na enfrentam browser algumas interessantes desafia quando vem tooauthentication:

* características de segurança de Olá destas aplicações forem significativamente diferentes de aplicações do servidor tradicional baseado em web.
* Muitos servidores de autorização & fornecedores de identidade não suportam pedidos CORS.
* Página completa browser redireciona para fora da aplicação Olá ficar toohello particularmente INVASIVO experiência de utilizador.

Para estas aplicações (pensar: AngularJS, Ember.js, React.js, etc.) do Azure AD suporta o fluxo de concessão implícita do OAuth 2.0 Olá.  fluxo implícito Olá está descrito em Olá [especificação do OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.2).  A principal vantagem é que permite que os tokens de tooget de aplicação Olá do Azure AD sem efetuar uma troca de credencial de servidor de back-end.  Isto permite Olá aplicação toosign utilizador Olá, manter a sessão e obter tokens tooother web APIs tudo isto no código de JavaScript de cliente Olá.  Existem alguns tootake de considerações de segurança importantes em consideração ao utilizar o fluxo implícito Olá - especificamente cerca [cliente](http://tools.ietf.org/html/rfc6749#section-10.3) e [representação de utilizadores](http://tools.ietf.org/html/rfc6749#section-10.3).

Se pretender que o fluxo implícito de Olá toouse e a aplicação do Azure AD tooadd autenticação tooyour JavaScript, recomendamos que utilize a nossa biblioteca de JavaScript de código aberto, [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Existem alguns AngularJS tutoriais disponíveis [aqui](active-directory-appmodel-v2-overview.md#getting-started) toohelp começar.  

No entanto, se preferir não toouse uma biblioteca nas mensagens de protocolo de aplicação e enviar única página por si, siga Olá geral os passos abaixo.

> [!NOTE]
> Nem todos os cenários do Azure Active Directory e funcionalidades são suportadas pelo ponto final de v 2.0 Olá.  toodetermine se deve utilizar o ponto final de v 2.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).
> 
> 

## Diagrama de protocolo
Olá todo implícito início de sessão fluxo aspeto semelhante ao seguinte isto - cada um dos passos de Olá descritas detalhadamente abaixo.

![OpenId Connect pistas de diagrama](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Enviar o pedido de início de sessão Olá
início de sessão tooinitially hello utilizador na sua aplicação, pode enviar um [OpenID Connect](active-directory-v2-protocols-oidc.md) pedido de autorização e obter um `id_token` do ponto final de v 2.0 Olá:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Clique neste pedido de ligação de Olá abaixo tooexecute! Depois de iniciarem sessão, o browser deve ser redirecionado demasiado`https://localhost/myapp/` com um `id_token` na barra de endereço Olá.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parâmetro |  | Descrição |
| --- | --- | --- |
| Inquilino |Necessário |Olá `{tenant}` valor no caminho de Olá de pedido de Olá pode ser utilizado toocontrol quem pode iniciar sessão na aplicação Olá.  Olá os valores permitidos são `common`, `organizations`, `consumers`e inquilinos identificadores.  Para obter mais detalhes, consulte [Noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |Necessário |Olá Id da aplicação do portal de registo que Olá ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a sua aplicação. |
| response_type |Necessário |Tem de incluir `id_token` para OpenID Connect início de sessão.  Também podem incluir a Olá response_type `token`. Utilizar `token` aqui permitirá tooreceive a aplicação um token de acesso imediato a partir de Olá autorizar o ponto final sem ter toomake autorizar um toohello pedido segundo ponto final.  Se utilizar Olá `token` response_type, Olá `scope` parâmetro tem de conter um âmbito que indica que o token de Olá tooissue de recursos para. |
| redirect_uri |recomendado |Olá redirect_uri da sua aplicação, onde as respostas de autenticação podem ser enviadas e recebidas pela sua aplicação.  Este deve corresponder exatamente um dos redirect_uris Olá registado no portal de Olá, exceto tem de ser codificados de url. |
| Âmbito |Necessário |Uma lista separada por espaço de âmbitos.  Para OpenID Connect, tem de incluir o âmbito de Olá `openid`, que converte toohello permissão de "Iniciar sessão" em consentimento Olá IU.  Opcionalmente, também poderá tooinclude Olá `email` ou `profile` [âmbitos](active-directory-v2-scopes.md) para obter dados de utilizador de tooadditional de acesso.  Também pode incluir outros âmbitos neste pedido para pedir consentimento toovarious recursos. |
| response_mode |recomendado |Especifica o método de Olá que deve ser utilizados toosend Olá resultante tooyour back-token aplicação.  Deve ser `fragment` fluxo implícito Olá. |
| state |recomendado |Um valor incluído no pedido de Olá que também vai ser devolvido em resposta token Olá.  Pode ser uma cadeia de todos os conteúdos que pretende.  Um valor exclusivo gerado aleatoriamente é normalmente utilizado para [impedir ataques de falsificação de pedidos entre sites](http://tools.ietf.org/html/rfc6749#section-10.12).  Estado de Olá também é utilizado tooencode informações sobre o estado do utilizador Olá na aplicação Olá antes do pedido de autenticação de Olá ocorreu, como a página Olá ou vista estivessem nas suas. |
| nonce |Necessário |Um valor incluído no pedido de Olá, gerado pela aplicação Olá, que será incluída em Olá id_token resultante como uma afirmação.  aplicação Olá, em seguida, pode verificar a que ataques de repetição de token de toomitigate este valor.  valor de Olá, normalmente, é uma cadeia de aleatório, exclusiva que pode ser utilizados tooidentify Olá origem do pedido de Olá. |
| linha de comandos |Opcional |Indica o tipo de Olá de interação do utilizador que é necessário.  Olá, apenas os valores válidos neste momento, são 'início de sessão', 'none' e 'consentimento'.  `prompt=login`irá forçar Olá tooenter utilizador as suas credenciais nesse pedido, a negação de início de sessão único em.  `prompt=none`é Olá oposta – -irá garantir que o utilizador Olá não é apresentado com qualquer linha de comandos interativa contratutal.  Se não é possível concluir o pedido de Olá automaticamente através de início de sessão único, o ponto final de v 2.0 Olá devolverá um erro.  `prompt=consent`será Olá acionador OAuth consentimento diálogo após Olá utilizador iniciar sessão, solicitando Olá utilizador toogrant permissões toohello aplicação. |
| login_hint |Opcional |Pode ser campo do endereço de e-mail/nome de utilizador do preenchimento de toopre utilizados Olá de Olá iniciar sessão na página de utilizador de Olá, se souber o nome de utilizador antecedência.  Muitas vezes, as aplicações irão utilizar este parâmetro durante a reautenticação, já ter extraídos Olá nome de utilizador de um anterior início de sessão utilizando Olá `preferred_username` de afirmação. |
| domain_hint |Opcional |Pode ser um dos `consumers` ou `organizations`.  Caso, irá ignorar o processo de deteção baseada em e-mail Olá esse utilizador passa através de início de sessão do Olá v 2.0 na página, esquerda tooa está mais simples ligeiramente mais experiência de utilizador.  Muitas vezes, aplicações, irão utilizar este parâmetro durante a reautenticação, extraindo Olá `tid` Olá id_token de afirmação.  Se hello `tid` é o valor de afirmação `9188040d-6c67-4c5b-b112-36a304b66dad`, deve utilizar `domain_hint=consumers`.  Caso contrário, utilize `domain_hint=organizations`. |

Neste momento, o utilizador de Olá será pedido tooenter as respetivas credenciais e autenticação Olá concluída.  Olá ponto final v 2.0 também vai assegurar que o utilizador Olá consentiu permissões toohello indicadas Olá `scope` parâmetro de consulta.  Se o utilizador Olá não consentiu tooany essas permissões, irá pedir-Olá utilizador tooconsent toohello necessárias permissões.  Detalhes de [permissões, consentimento e aplicações de multi-inquilinos são fornecidas aqui](active-directory-v2-scopes.md).

Depois do utilizador Olá efetua a autenticação e atribui o consentimento, o ponto final de v 2.0 Olá irá devolver uma aplicação de tooyour de resposta no Olá indicado `redirect_uri`, utilizando o método de Olá especificado em Olá `response_mode` parâmetro.

#### Resposta com êxito
Uma resposta com êxito utilizando `response_mode=fragment` e `response_type=id_token+token` se parece com Olá seguinte, com as quebras de linha para melhorar a legibilidade:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Parâmetro | Descrição |
| --- | --- |
| access_token |Se incluídos `response_type` inclui `token`. token de acesso de Olá Olá aplicação solicitada, neste caso, para Olá Microsoft Graph.  o token de acesso de Olá não deve estar descodificar ou inspecionado caso contrário, pode ser tratado como uma cadeia opaco. |
| token_type |Se incluídos `response_type` inclui `token`.  Será sempre `Bearer`. |
| expires_in |Se incluídos `response_type` inclui `token`.  Indica o número de Olá de segundos que o token de Olá for válido, para efeitos de colocação em cache. |
| Âmbito |Se incluídos `response_type` inclui `token`.  Indica os âmbitos que se a Olá para que Olá access_token será válido. |
| id_token |Olá id_token Olá aplicação pedida. Pode utilizar Olá id_token tooverify Olá identidade do utilizador e iniciar uma sessão de utilizador de Olá.  Obter mais detalhes sobre id_tokens e os respetivos conteúdos está incluído no Olá [referência de token de ponto final v 2.0](active-directory-v2-tokens.md). |
| state |Se um parâmetro de estado está incluído no pedido de Olá, hello mesmo valor deve aparecer na resposta Olá. aplicação Olá deverá certificar-se de que os valores do Estado de Olá no Olá pedido e resposta são idênticos. |

#### Resposta de erro
As respostas de erro também podem ser enviadas toohello `redirect_uri` para aplicação Olá pode processar corretamente:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| erro |Uma cadeia de código de erro que pode ser utilizados tooclassify tipos de erros ocorridos e pode ser utilizados tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar um programador a identificar causas raiz Olá um erro de autenticação. |

## Validar Olá id_token
Apenas receber uma id_token não é suficiente utilizador de Olá tooauthenticate; tem de validar a assinatura do Olá id_token e certifique-se Olá afirmações num token de Olá por requisitos da sua aplicação.  o ponto final v 2.0 Olá utiliza [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e público tokens toosign de criptografia de chave e certifique-se de que são válidas.

Pode escolher toovalidate Olá `id_token` no código de cliente, mas uma prática comum é toosend Olá `id_token` tooa servidor de back-end e efetuar a validação de Olá não existe.  Depois de ter confirmado a assinatura de Olá id_token Olá, existem alguns afirmações que será tooverify necessária.  Consulte Olá [referência de token de v 2.0](active-directory-v2-tokens.md) para obter mais informações, incluindo [validar os Tokens](active-directory-v2-tokens.md#validating-tokens) e [importantes informações sobre como assinar Rollover de chave](active-directory-v2-tokens.md#validating-tokens).  Recomendamos que efetuar utilização de uma biblioteca para analisar e a validar a tokens - há, pelo menos, um disponível para a maioria dos idiomas e plataformas.
<!--TODO: Improve hello information on this-->

Também pode desejar toovalidate afirmações adicionais dependendo do seu cenário.  Alguns validações comuns incluem:

* Garantir que a organização e utilizador Olá assinou cópias de segurança da aplicação Olá.
* Utilizador de Olá, garantindo que tem autorização adequados/privilégios
* Garantir que um determinada força de autenticação tiver ocorrido, tais como a autenticação multifator.

Para obter mais informações sobre afirmações Olá numa id_token, consulte Olá [referência de token de ponto final v 2.0](active-directory-v2-tokens.md).

Depois de validar completamente id_token Olá, pode iniciar uma sessão de utilizador de Olá e utilizar afirmações de Olá Olá id_token tooobtain sobre utilizador Olá na sua aplicação.  Estas informações podem ser utilizadas para apresentar, registos, autorizações, etc.

## Obter os tokens de acesso
Agora que já iniciou a sessão de utilizador Olá na sua aplicação de página única, pode obter os tokens de acesso para chamadas das APIs protegidas pelo Azure AD, como Olá web [Microsoft Graph](https://graph.microsoft.io).  Mesmo que já foi recebido um token com Olá `token` response_type, pode utilizar este método tooacquire tokens tooadditional recursos sem ter tooredirect Olá utilizador toosign novamente.

No fluxo de OpenID Connect/OAuth normal Olá, isto seria feito ao tornar um v 2.0 toohello de pedido `/token` ponto final.  No entanto, o ponto final de v 2.0 Olá não não suporte CORS pedidos, para efetuar AJAX chama tooget e atualização de tokens está fora do pergunta Olá.  Em vez disso, pode utilizar fluxo implícito Olá um iframe oculta tooget novos tokens para outras APIs web: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Tente copiar e colar Olá abaixo pedido para um separador do browser! (Não se esqueça tooreplace Olá `domain_hint` e Olá `login_hint` valores com Olá corrigir valores para os seus utilizadores)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| Inquilino |Necessário |Olá `{tenant}` valor no caminho de Olá de pedido de Olá pode ser utilizado toocontrol quem pode iniciar sessão na aplicação Olá.  Olá os valores permitidos são `common`, `organizations`, `consumers`e inquilinos identificadores.  Para obter mais detalhes, consulte [Noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |Necessário |Olá Id da aplicação do portal de registo que Olá ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a sua aplicação. |
| response_type |Necessário |Tem de incluir `id_token` para OpenID Connect início de sessão.  Poderão incluir outras response_types, tais como `code`. |
| redirect_uri |recomendado |Olá redirect_uri da sua aplicação, onde as respostas de autenticação podem ser enviadas e recebidas pela sua aplicação.  Este deve corresponder exatamente um dos redirect_uris Olá registado no portal de Olá, exceto tem de ser codificados de url. |
| Âmbito |Necessário |Uma lista separada por espaço de âmbitos.  Para obter os tokens, incluir todos os [âmbitos](active-directory-v2-scopes.md) precisa para o recurso de Olá de interesse. |
| response_mode |recomendado |Especifica o método de Olá que deve ser utilizados toosend Olá resultante tooyour back-token aplicação.  Pode ser um dos `query`, `form_post`, ou `fragment`. |
| state |recomendado |Um valor incluído no pedido de Olá que também vai ser devolvido em resposta token Olá.  Pode ser uma cadeia de todos os conteúdos que pretende.  Um valor exclusivo gerado aleatoriamente é normalmente utilizado para impedir ataques de falsificação de pedidos entre sites.  Estado de Olá também é utilizado tooencode informações sobre o estado do utilizador Olá na aplicação Olá antes do pedido de autenticação de Olá ocorreu, como a página Olá ou vista estivessem nas suas. |
| nonce |Necessário |Um valor incluído no pedido de Olá, gerado pela aplicação Olá, que será incluída em Olá id_token resultante como uma afirmação.  aplicação Olá, em seguida, pode verificar a que ataques de repetição de token de toomitigate este valor.  valor de Olá, normalmente, é uma cadeia de aleatório, exclusiva que pode ser utilizados tooidentify Olá origem do pedido de Olá. |
| linha de comandos |Necessário |Para atualizar e obter os tokens um iframe oculta, deve utilizar `prompt=none` tooensure Olá iframe bloquear não na página de início de sessão v 2.0 Olá e devolve imediatamente. |
| login_hint |Necessário |Para atualizar e obter os tokens um iframe oculta, tem de incluir nome de utilizador de Olá do utilizador Olá desta sugestão na ordem toodistinguish entre várias sessões de utilizador de Olá pode ter um determinado ponto no tempo. Pode extrair Olá nome de utilizador a partir de um anterior início de sessão utilizando Olá `preferred_username` de afirmação. |
| domain_hint |Necessário |Pode ser um dos `consumers` ou `organizations`.  Para atualizar e obter os tokens um iframe oculta, tem de incluir Olá domain_hint no pedido de Olá.  Deve extrair Olá `tid` de afirmação que toouse de valor de Olá id_token de um toodetermine de início de sessão anterior.  Se hello `tid` é o valor de afirmação `9188040d-6c67-4c5b-b112-36a304b66dad`, deve utilizar `domain_hint=consumers`.  Caso contrário, utilize `domain_hint=organizations`. |

Obrigado toohello `prompt=none` parâmetro, este pedido é concluída com êxito ou falharão imediatamente e devolver tooyour aplicação.  Uma resposta com êxito será enviada tooyour aplicação em Olá indicado `redirect_uri`, utilizando o método de Olá especificado em Olá `response_mode` parâmetro.

#### Resposta com êxito
Uma resposta com êxito utilizando `response_mode=fragment` parece ser:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Parâmetro | Descrição |
| --- | --- |
| access_token |token de Olá Olá aplicação pedida. |
| token_type |Será sempre `Bearer`. |
| state |Se um parâmetro de estado está incluído no pedido de Olá, hello mesmo valor deve aparecer na resposta Olá. aplicação Olá deverá certificar-se de que os valores do Estado de Olá no Olá pedido e resposta são idênticos. |
| expires_in |Quanto o token de acesso de Olá é válido (em segundos). |
| Âmbito |âmbitos de Olá Olá token de acesso é válido para. |

#### Resposta de erro
As respostas de erro também podem ser enviadas toohello `redirect_uri` para aplicação Olá pode processar corretamente.  No caso de Olá de `prompt=none`, será um erro esperado:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parâmetro | Descrição |
| --- | --- |
| erro |Uma cadeia de código de erro que pode ser utilizados tooclassify tipos de erros ocorridos e pode ser utilizados tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar um programador a identificar causas raiz Olá um erro de autenticação. |

Se receber este erro no pedido de iframe Olá, Olá utilizador tem interativamente iniciar sessão novamente tooretrieve um novo token.  Pode escolher toohandle neste caso, forma que achar mais faz sentido para a sua aplicação.

## Atualizar tokens
Ambos `id_token`s e `access_token`s irá expirar após um curto período de tempo, pelo que a aplicação tem de ser preparada toorefresh estes tokens periodicamente.  toorefresh um tipo de token, pode realizar Olá mesmo pedido iframe oculta from above utilizando Olá `prompt=none` parâmetro comportamento toocontrol do Azure AD.  Se quiser tooreceive um novo `id_token`, ser toouse se `response_type=id_token` e `scope=openid`, bem como um `nonce` parâmetro.

## Enviar um pedido de terminar
Olá OpenIdConnect `end_session_endpoint` permite a um pedido toohello v 2.0 endpoint tooend sessão e limpar os cookies de um utilizador definidos pelo ponto final de v 2.0 Olá toosend a aplicação.  toofully assinar um utilizador fora de uma aplicação web, a aplicação deve terminar a sua própria sessão com o utilizador Olá (normalmente, ao limpar a cache de tokens ou remover cookies) e, em seguida, redireciona o browser Olá para:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| Inquilino |Necessário |Olá `{tenant}` valor no caminho de Olá de pedido de Olá pode ser utilizado toocontrol quem pode iniciar sessão na aplicação Olá.  Olá os valores permitidos são `common`, `organizations`, `consumers`e inquilinos identificadores.  Para obter mais detalhes, consulte [Noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | recomendado | URL de Olá Olá utilizador deve ser devolvido tooafter fim de sessão for concluída. Este valor tem de corresponder a um redirecionamento Olá que URIs registados para aplicação Olá. Se não incluído, utilizador de Olá será apresentada uma mensagem genérica pelo ponto final de v 2.0 Olá. |
