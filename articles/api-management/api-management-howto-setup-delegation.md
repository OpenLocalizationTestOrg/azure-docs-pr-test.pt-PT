---
title: "aaaHow toodelegate utilizador produto e registo de subscrição"
description: "Saiba como toodelegate utilizador registo e o produto da subscrição tooa de terceiros na API Management do Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Como toodelegate de subscrição de produto e registo de utilizador
Delegação permite-lhe toouse seu Web site existente para processar tooproducts de início de sessão-na/sessão-up e uma subscrição de programador como opposed toousing Olá uma funcionalidade incorporada no portal de programador Olá. Isto permite que os dados de utilizador do Web site tooown Olá e efetuar a validação de Olá destes passos de uma forma personalizada.

## <a name="delegate-signin-up"></a>Delegating programador início de sessão e inscrição
toodelegate programador tooyour de início de sessão e inscrição Web site existente, terá de toocreate um ponto final de delegação especial no seu site que age como Olá ponto de entrada para esse pedido de iniciadas a partir do portal do programador Olá API Management.

fluxo de trabalho final Olá será o seguinte:

1. Programador clica na ligação de início de sessão ou inscrição de Olá em Olá portal do Programador de API Management
2. Browser é o ponto final de delegação toohello redirecionada
3. Ponto final de delegação no return redireciona tooor apresenta IU perguntar utilizador toosign ou no inscrição
4. Com êxito, o utilizador Olá é redirecionada toohello back-API Management programador portal página iniciadas a partir do

toobegin, vamos primeiro tooroute de gestão de API de configuração pedidos através do seu ponto final de delegação. No portal do publicador da API Management Olá, clique em **segurança** e, em seguida, clique em Olá **delegação** separador. Clique em Olá caixa de verificação tooenable 'Delegate início de sessão e inscrição'.

![Página de delegação][api-management-delegation-signin-up]

* Decidir que Olá URL do seu ponto final de delegação especial será e introduza-o no Olá **URL de ponto final de delegação** campo. 
* Dentro do Olá **chave de autenticação de delegação** campo introduza um segredo que será utilizado toocompute tooyou uma assinatura fornecida para verificação tooensure que Olá pedido realmente for proveniente de API Management do Azure. Pode clicar em Olá **gerar** botão toohave gestão de API gerar aleatoriamente uma chave para si.

Agora tem toocreate Olá **ponto final de delegação**. Tooperform é tem um número de ações:

1. Receba um pedido no Olá seguinte formato:
   
   > *http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {URL da página de origem} & salt = {cadeia} & sig = {cadeia}*
   > 
   > 
   
    Parâmetros de consulta para o caso de início de sessão / inscrição Olá:
   
   * **operação**: identifica o tipo de pedido de delegação é - só pode ser **SignIn** neste caso,
   * **returnUrl**: Olá URL da página olá onde o utilizador Olá clicado numa ligação de início de sessão ou inscrição
   * **Salt**: uma cadeia de salt especial utilizada para um hash de segurança de computação
   * **SIG**: um toobe de hash de segurança calculada utilizado para comparação tooyour própria hash calculado
2. Certifique-se de que esse pedido Olá for proveniente de API Management do Azure (opcional, mas vivamente recomendado de segurança)
   
   * Computação um hash HMAC SHA512 de uma cadeia com base no Olá **returnUrl** e **salt** parâmetros de consulta ([código de exemplo fornecido abaixo]):
     
     > HMAC (**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Comparar Olá acima-hash calculado toohello valor Olá **sig** parâmetro de consulta. Se correspondem aos hashes de dois Olá, mover no passo seguinte toohello, caso contrário negar o pedido de Olá.
3. Certifique-se de que estão a receber um pedido de início de sessão na/início de sessão-cópia de segurança: Olá **operação** parâmetro de consulta será definido demasiado "**SignIn**".
4. Presente Olá utilizador com IU toosign ou no inscrição
5. Se o utilizador Olá é a assinatura de segurança tem toocreate uma conta correspondente para os mesmos na API Management. [Criar um utilizador] com Olá API de REST de gestão de API. Ao fazê-lo, certifique-se de que definiu toohello de ID de utilizador Olá mesmo está no arquivo de utilizador ou ID de tooan pode manter controlar dos.
6. Quando o utilizador de Olá é autenticado com êxito:
   
   * [pedir um token de sessão único (SSO)] através de Olá API de REST de gestão de API
   * acrescente um toohello de parâmetro de consulta returnUrl URL SSO recebidos da chamada de API de Olá acima:
     
     > Por exemplo, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * Olá utilizador toohello acima foram produzido URL de redirecionamento

Na adição toohello **SignIn** operação, também pode efetuar a gestão de conta ao seguir os passos anteriores Olá e utilizando um dos Olá seguintes operações.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

Tem de passar Olá seguir os parâmetros de consulta para operações de gestão de conta.

* **operação**: identifica o tipo de pedido de delegação é (ChangePassword, ChangeProfile ou CloseAccount)
* **userId**: id de utilizador de Olá de Olá conta toomanage
* **Salt**: uma cadeia de salt especial utilizada para um hash de segurança de computação
* **SIG**: um toobe de hash de segurança calculada utilizado para comparação tooyour própria hash calculado

## <a name="delegate-product-subscription"></a>Delegar a subscrição do produto
Delegar a subscrição de produto funciona da mesma forma toodelegating utilizador início de sessão/cópia de segurança. fluxo de trabalho final Olá seria o seguinte:

1. Programador seleciona um produto no portal de Programador de API Management Olá e clica no botão de subscrever Olá
2. Browser é o ponto final de delegação toohello redirecionada
3. Ponto final de delegação efetua os passos de subscrição necessário produto - esta é a cópia de segurança tooyou e poderá entail redirecionar informações de faturação, colocar questões adicionais, ou simplesmente armazenar informações de Olá e que não requerem qualquer ação do utilizador o toorequest da página de tooanother

tooenable Olá funcionalidade, Olá **delegação** página clique **delegar a subscrição de produto**.

Em seguida, certifique-se de ponto final de delegação Olá efetua Olá seguintes ações:

1. Receba um pedido no Olá seguinte formato:
   
   > *http://www.yourwebsite.com/apimdelegation?Operation= {operação} & productId = {toosubscribe de produto para} & userId = {efetuar o pedido de utilizador} & salt = {cadeia} & sig = {cadeia}*
   > 
   > 
   
    Parâmetros de consulta para o caso de subscrição de produto Olá:
   
   * **operação**: identifica o tipo de pedido de delegação é. Para a subscrição de produto pedidos Olá válido opções são:
     * "Subscrever": fornecidos de um pedido toosubscribe Olá utilizador tooa fornecido produto com o ID (ver abaixo)
     * "Anular a subscrição": toounsubscribe um pedido um utilizador de um produto
     * "Renovar": uma toorenew requst uma subscrição (por exemplo, que pode ser expira)
   * **productId**: Olá ID de utilizador do Olá produto Olá pedida toosubscribe para
   * **userId**: Olá ID de utilizador de Olá para o qual o pedido de Olá é efetuado
   * **Salt**: uma cadeia de salt especial utilizada para um hash de segurança de computação
   * **SIG**: um toobe de hash de segurança calculada utilizado para comparação tooyour própria hash calculado
2. Certifique-se de que esse pedido Olá for proveniente de API Management do Azure (opcional, mas vivamente recomendado de segurança)
   
   * Computação um SHA512 HMAC de uma cadeia com base no Olá **productId**, **userId** e **salt** parâmetros de consulta:
     
     > HMAC (**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * Comparar Olá acima-hash calculado toohello valor Olá **sig** parâmetro de consulta. Se correspondem aos hashes de dois Olá, mover no passo seguinte toohello, caso contrário negar o pedido de Olá.
3. Efetuar qualquer processamento de subscrição de produto com base no tipo de Olá da operação pedida no **operação** -por exemplo, de faturação, mais perguntas, etc.
4. Com êxito subscrever o produto de toohello Olá utilizador no seu lado, subscrever produtos de gestão de API do Olá utilizador toohello por [Olá chamar a REST API para a subscrição de produto].

## <a name="delegate-example-code"></a> Código de exemplo
Estes exemplos mostram de código como tootake Olá *chave de validação de delegação*, que está definido no ecrã de delegação de Olá do portal do publicador Olá, toocreate um HMAC que, em seguida, é utilizada a assinatura de Olá toovalidate, comprovar a respetiva validade Olá Olá returnUrl transmitido. Olá mesmo código funciona para Olá productId e userId com ligeiras modificação.

**C# hash de código toogenerate do returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**NodeJS código hash toogenerate de returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre delegação, consulte Olá seguir as vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[pedir um token de sessão único (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[criar um utilizador]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[Olá chamar a REST API para a subscrição de produto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[código de exemplo fornecido abaixo]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
