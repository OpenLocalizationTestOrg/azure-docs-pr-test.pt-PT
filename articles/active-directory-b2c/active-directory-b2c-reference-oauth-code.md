---
title: "Fluxo de código de autorização - Azure AD B2C | Microsoft Docs"
description: "Saiba como toobuild aplicações web através do protocolo de autenticação do Azure AD B2C e o OpenID Connect."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Do Azure Active Directory B2C: Fluxo de código de autorização de OAuth 2.0
Pode utilizar a concessão do código de autorização de Olá OAuth 2.0 em aplicações instaladas num dispositivo toogain acesso tooprotected recursos, tais como as APIs web. Ao utilizar a implementação de (Azure AD B2C) Olá Azure Active Directory B2C de OAuth 2.0, pode adicionar inscrição, início de sessão e tarefas de outra gestão de identidades tooyour aplicações de ambiente de trabalho e móveis. Este artigo é independente de idioma. Artigo de Olá, vamos descrever como toosend e receber mensagens HTTP sem utilizar quaisquer bibliotecas de open source.

<!-- TODO: Need link toolibraries -->

Olá fluxo de código de autorização do OAuth 2.0 está descrita em [secção 4.1 de especificação de Olá OAuth 2.0](http://tools.ietf.org/html/rfc6749). Pode utilizá-lo para autenticação e autorização na maioria dos tipos de aplicação, incluindo [aplicações web](active-directory-b2c-apps.md#web-apps) e [instalado nativamente aplicações](active-directory-b2c-apps.md#mobile-and-native-apps). Pode utilizar Olá adquirir toosecurely de fluxo de código de autorização do OAuth 2.0 *tokens de acesso* para as suas aplicações, que pode ser utilizado tooaccess recursos que estão protegidos por um [servidor autorização](active-directory-b2c-reference-protocols.md#the-basics).

Este artigo incida no Olá **clientes públicos** fluxo de código de autorização do OAuth 2.0. Um cliente público é qualquer aplicação cliente que não pode ser fidedigno toosecurely manter a integridade do Olá de uma palavra-passe secreta. Isto inclui as aplicações móveis, as aplicações de ambiente de trabalho e essencialmente qualquer aplicação que é executado num dispositivo e tem de tooget tokens de acesso. 

> [!NOTE]
> aplicação web tooa de gestão de identidade de tooadd utilizando o Azure AD B2C, utilize [OpenID Connect](active-directory-b2c-reference-oidc.md) em vez de OAuth 2.0.

O Azure AD B2C expande o padrão de Olá que flui de OAuth 2.0 toodo mais do que simples autenticação e autorização. Introduz Olá [parâmetro política](active-directory-b2c-reference-policies.md). Com as políticas incorporadas, pode utilizar o OAuth 2.0 tooadd utilizador experiências tooyour aplicação, tal como inscrição, início de sessão e gestão de perfis. Neste artigo, vamos mostrar-lhe como tooimplement de OAuth 2.0 e as políticas de toouse cada um destes experiências nas suas aplicações nativas. Podemos também mostram-lhe como tooget tokens de acesso para aceder a APIs web.

Pedidos HTTP de exemplo de Olá neste artigo, utilizamos diretório do Azure AD B2C nosso exemplo, **fabrikamb2c.onmicrosoft.com**. Também utilizamos a nossa aplicação de exemplo e as políticas. Pode tentar Olá pedidos utilizando estes valores, ou pode substituí-los com os seus próprios valores.
Saiba como demasiado[obter os seus próprios diretório do Azure AD B2C, aplicações e políticas](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Obtenha um código de autorização
fluxo de código de autorização de Olá começa com o cliente de Olá instruir Olá utilizador toohello `/authorize` ponto final. Este é Olá interativa parte fluxo Olá, onde o utilizador Olá executa a ação. Este pedido de cliente Olá indica em Olá `scope` permissões de Olá de parâmetro que necessita de tooacquire de utilizador de Olá. No Olá `p` parâmetro, ele indica Olá tooexecute de política. Olá três exemplos seguintes (com quebras de linha para legibilidade) cada utilizarem uma política diferente.

### <a name="use-a-sign-in-policy"></a>Utilizar uma política de início de sessão
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Utilizar uma política de inscrição
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Utilizar uma política de perfil de edição
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parâmetro | Necessário? | Descrição |
| --- | --- | --- |
| client_id |Necessário |ID da aplicação Olá atribuído aplicação tooyour no Olá [portal do Azure](https://portal.azure.com). |
| response_type |Necessário |tipo de resposta de Olá, tem de incluir `code` para o fluxo de código de autorização de Olá. |
| redirect_uri |Necessário |Olá redireciona o URI da sua aplicação, onde as respostas de autenticação são enviadas e recebidas pela sua aplicação. Este deve corresponder exatamente um redirecionamento Olá URIs registados no portal de Olá, exceto que tem de ser codificados de URL. |
| Âmbito |Necessário |Uma lista separada por espaço de âmbitos. Um valor único âmbito indica tooAzure do Active Directory (Azure AD) ambas as permissões de Olá que estão a ser solicitada. Olá, utilizando o cliente de Olá ID como âmbito de Olá indica que a aplicação tem um token de acesso que pode ser utilizado contra o seu próprio serviço ou a API, web representado pelo mesmo ID de cliente.  Olá `offline_access` âmbito indica que a aplicação tem um token de atualização para tooresources de acesso de longa duração. Também pode utilizar Olá `openid` âmbito toorequest um token de ID do Azure AD B2C. |
| response_mode |Recomendado |método de Olá que utilize toosend Olá resultante autorização código back tooyour aplicação. Pode ser `query`, `form_post`, ou `fragment`. |
| state |Recomendado |Um valor incluído no pedido de Olá que é devolvido em resposta token Olá. Pode ser uma cadeia de qualquer conteúdo que pretende que o toouse. Normalmente, é utilizado um valor exclusivo gerado aleatoriamente, tooprevent ataques de falsificação de pedidos entre sites. Estado de Olá é também utilizada tooencode informações sobre o estado do utilizador Olá na aplicação Olá antes do pedido de autenticação de Olá ocorreu. Por exemplo, o utilizador do Olá página Olá estava no ou Olá política que estava a ser executada. |
| P |Necessário |política de Olá que é executada. De Olá nome de uma política que é criado no diretório do Azure AD B2C. o valor de nome de política de Olá deve iniciar com **b2c\_1\_**. toolearn mais informações sobre políticas, consulte [políticas incorporadas do Azure AD B2C](active-directory-b2c-reference-policies.md). |
| linha de comandos |Opcional |tipo de Olá da interação do utilizador que é necessário. Atualmente, Olá único valor válido é `login`que força Olá utilizador tooenter as respetivas credenciais desse pedido. O início de sessão único não entrarão em vigor. |

Neste momento, Olá é pedido ao utilizador fluxo de trabalho da política de Olá toocomplete. Isto poderá envolver o utilizador Olá introduzir o respetivo nome de utilizador e palavra-passe, início de sessão com uma identidade de redes social, inscrever-se para o diretório de Olá ou qualquer outro número de passos. Ações de utilizador dependem como política Olá está definida.

Após a conclusão da política de Olá utilizador Olá, Azure AD devolve uma aplicação de tooyour de resposta no valor de Olá utilizado para `redirect_uri`. Utiliza o método de Olá especificado em Olá `response_mode` parâmetro. resposta Olá é exatamente hello mesmo para cada um dos Olá ação cenários de utilizador, independentemente da política de Olá que foi executada.

Uma resposta com êxito que utiliza `response_mode=query` se parece com isto:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parâmetro | Descrição |
| --- | --- |
| código |código de autorização de Olá que Olá aplicação pedida. aplicação Olá pode utilizar Olá autorização código toorequest um token de acesso para um recurso de destino. Códigos de autorização são muito curta duração. Normalmente, estas expiram após cerca de 10 minutos. |
| state |Ver descrição completa do Olá na tabela de Olá no Olá anterior a secção. Se um `state` parâmetro está incluído no pedido de Olá, hello mesmo valor deve aparecer na resposta Olá. Olá aplicação deve verificar que Olá `state` valores existentes na Olá pedido e resposta são idênticos. |

As respostas de erro também podem ser enviadas URI de redirecionamento toohello para que hello aplicação pode processá-los corretamente:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parâmetro | Descrição |
| --- | --- |
| erro |Uma cadeia de código de erro que pode utilizar tooclassify Olá tipos de erros que ocorrem. Também pode utilizar Olá cadeia tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar causas raiz Olá um erro de autenticação. |
| state |Ver descrição completa do Olá no Olá anterior a tabela. Se um `state` parâmetro está incluído no pedido de Olá, hello mesmo valor deve aparecer na resposta Olá. Olá aplicação deve verificar que Olá `state` valores existentes na Olá pedido e resposta são idênticos. |

## <a name="2-get-a-token"></a>2. Obter um token
Agora que já obteve um código de autorização, pode resgatar Olá `code` para um token toohello que se destina a recursos através do envio de um toohello de pedido POST `/token` ponto final. No Azure AD B2C, hello apenas os recursos que pode pedir um token para é o web de back-end da aplicação API. Convenção de Olá que é utilizada para pedir um token tooyourself é toouse o ID de cliente da sua aplicação como âmbito de Olá:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Parâmetro | Necessário? | Descrição |
| --- | --- | --- |
| P |Necessário |Olá política que foi utilizado tooacquire Olá autorização código. Não é possível utilizar uma política diferente neste pedido. Tenha em atenção que adicionar este parâmetro toohello *cadeia de consulta*e não na Olá corpo da mensagem. |
| client_id |Necessário |ID da aplicação Olá atribuído aplicação tooyour no Olá [portal do Azure](https://portal.azure.com). |
| grant_type |Necessário |tipo de Olá de concessão. Fluxo de código de autorização de Olá, Olá conceder tipo tem de ser `authorization_code`. |
| Âmbito |Recomendado |Uma lista separada por espaço de âmbitos. Um valor único âmbito indica tooAzure AD ambas as permissões de Olá que estão a ser solicitada. Olá, utilizando o cliente de Olá ID como âmbito de Olá indica que a aplicação tem um token de acesso que pode ser utilizado contra o seu próprio serviço ou a API, web representado pelo mesmo ID de cliente.  Olá `offline_access` âmbito indica que a aplicação tem um token de atualização para tooresources de acesso de longa duração.  Também pode utilizar Olá `openid` âmbito toorequest um token de ID do Azure AD B2C. |
| código |Necessário |código de autorização de Olá que obteve na fase de primeiro Olá do fluxo de Olá. |
| redirect_uri |Necessário |Olá redireciona o URI da aplicação olá onde recebido o código de autorização de Olá. |

Uma resposta com êxito de token tem o seguinte aspeto:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parâmetro | Descrição |
| --- | --- |
| not_before |tempo de Olá no qual Olá token é considerado válido, no tempo de época. |
| token_type |valor de tipo de token de Olá. Olá escreva apenas que o suporte do Azure AD é portador. |
| access_token |Olá assinado JSON Web tokens (JWT) que pediu. |
| Âmbito |âmbitos de Olá Olá token é válido para. Também pode utilizar os tokens de toocache âmbitos para utilização posterior. |
| expires_in |Olá período de tempo que Olá token é válido (em segundos). |
| refresh_token |Um token de atualização de OAuth 2.0. aplicação Olá pode utilizar este token tooacquire os tokens adicionais depois de token atual Olá expira. Os tokens de atualização são longa duração. Pode utilizá-los tooretain acesso tooresources para períodos de tempo prolongados. Para obter mais informações, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). |

As respostas de erro tem o seguinte aspeto:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parâmetro | Descrição |
| --- | --- |
| erro |Uma cadeia de código de erro que pode utilizar tooclassify Olá tipos de erros que ocorrem. Também pode utilizar Olá cadeia tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar causas raiz Olá um erro de autenticação. |

## <a name="3-use-hello-token"></a>3. Utilizar token Olá
Agora que já obteve com êxito um token de acesso, pode utilizar o token de Olá APIs web de back-end de tooyour pedidos, incluindo-o no Olá `Authorization` cabeçalho:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Atualizar o token de Olá
Os tokens de acesso e tokens de ID são curta duração. Depois de expirarem, deve atualizá-las toocontinue tooaccess recursos. toodo, Submeter outro toohello de pedido POST `/token` ponto final. Este tempo, fornecer Olá `refresh_token` em vez de Olá `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Parâmetro | Necessário? | Descrição |
| --- | --- | --- |
| P |Necessário |política de Olá que foi token de atualização do tooacquire utilizados Olá original. Não é possível utilizar uma política diferente neste pedido. Tenha em atenção que adicionar este parâmetro toohello *cadeia de consulta*e não na Olá corpo da mensagem. |
| client_id |Recomendado |ID da aplicação Olá atribuído aplicação tooyour no Olá [portal do Azure](https://portal.azure.com). |
| grant_type |Necessário |tipo de Olá de concessão. Para esta parte do fluxo de código de autorização de Olá, Olá conceder tipo tem de ser `refresh_token`. |
| Âmbito |Recomendado |Uma lista separada por espaço de âmbitos. Um valor único âmbito indica tooAzure AD ambas as permissões de Olá que estão a ser solicitada. Olá, utilizando o cliente de Olá ID como âmbito de Olá indica que a aplicação tem um token de acesso que pode ser utilizado contra o seu próprio serviço ou a API, web representado pelo mesmo ID de cliente.  Olá `offline_access` âmbito indica que a aplicação irá precisar de um token de atualização para tooresources de acesso de longa duração.  Também pode utilizar Olá `openid` âmbito toorequest um token de ID do Azure AD B2C. |
| redirect_uri |Opcional |Olá redireciona o URI da aplicação olá onde recebido o código de autorização de Olá. |
| refresh_token |Necessário |Olá original token de atualização que obteve na fase de segundo Olá do fluxo de Olá. |

Uma resposta com êxito de token tem o seguinte aspeto:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parâmetro | Descrição |
| --- | --- |
| not_before |tempo de Olá no qual Olá token é considerado válido, no tempo de época. |
| token_type |valor de tipo de token de Olá. Olá escreva apenas que o suporte do Azure AD é portador. |
| access_token |Olá assinado JWT que pediu. |
| Âmbito |âmbitos de Olá Olá token é válido para. Também pode utilizar tokens de toocache hello âmbitos para utilização posterior. |
| expires_in |Olá período de tempo que Olá token é válido (em segundos). |
| refresh_token |Um token de atualização de OAuth 2.0. aplicação Olá pode utilizar este token tooacquire os tokens adicionais depois de token atual Olá expira. Atualizar tokens são longa duração e podem ser utilizados tooretain acesso tooresources para períodos de tempo prolongados. Para obter mais informações, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). |

As respostas de erro tem o seguinte aspeto:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parâmetro | Descrição |
| --- | --- |
| erro |Uma cadeia de código de erro que pode utilizar tooclassify tipos de erros que ocorrem. Também pode utilizar Olá cadeia tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar causas raiz Olá um erro de autenticação. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Utilizar os seus próprios diretórios do Azure AD B2C
tootry estes pedidos por si, Olá concluir os seguintes passos. Substitua os valores de exemplo de Olá que utilizámos neste artigo com os seus próprios valores.

1. [Criar um diretório do Azure AD B2C](active-directory-b2c-get-started.md). Utilize o nome de Olá do seu diretório no Olá pedidos.
2. [Criar uma aplicação](active-directory-b2c-app-registration.md) tooobtain uma ID da aplicação e um URI de redirecionamento. Incluem um cliente nativo na sua aplicação.
3. [Criar as políticas](active-directory-b2c-reference-policies.md) tooobtain os nomes de política.

