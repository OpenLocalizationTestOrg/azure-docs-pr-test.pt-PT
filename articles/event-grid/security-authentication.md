---
title: "segurança de grelha de evento aaaAzure e autenticação"
description: Descreve os conceitos e grelha de eventos do Azure.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Segurança de grelha de eventos e autenticação 

Grelha de eventos do Azure tem três tipos de autenticação:

* Subscrições de eventos
* Publicação de eventos
* Entrega de eventos do WebHook

## <a name="webhook-event-delivery"></a>Entrega de eventos do WebHook

Webhooks são um dos muitos eventos de tooreceive formas em tempo real da grelha de eventos do Azure.

Sempre que há um novo toobe pronto de evento entregue, grelha de eventos envia um pedido HTTP com tooyour WebHook com evento Olá no corpo de Olá.

Quando registar o próprio ponto final de WebHook a grelha de evento, envia a um pedido POST com um código de validação simples na propriedade de ponto final de tooprove de ordem. A aplicação tem toorespond por echoing código de validação de Olá anterior. Grelha de evento não irá fornecer eventos pontos finais de tooWebHook que não passaram a validação de Olá.
 
### <a name="validation-details"></a>Detalhes de validação:

* Grelha de evento mensagens do momento Olá da subscrição de evento criação/atualização, um ponto final toohello "SubscriptionValidationEvent" eventos destino.
* eventos de Olá contém um valor de cabeçalho "Tipo de evento: validação".
* tem de corpo de evento Olá Olá mesmo esquema que outros eventos de grelha de eventos.
* dados de eventos de Olá incluem uma propriedade de "ValidationCode" com uma cadeia gerada aleatoriamente, por exemplo "ValidationCode: acb13...".

Na propriedade de ponto final de tooprove ordem, por exemplo de código de validação de back-Olá de eco "ValidationResponse: acb13...".

Por fim, é importante toonote que a grelha de eventos do Azure suporta apenas pontos finais de webhook HTTPS.
## <a name="event-subscription"></a>Subscrição de evento

evento de tooan toosubscribe, tem de ter Olá **Microsoft.EventGrid/EventSubscriptions/Write** necessária a permissão no Olá recursos. Tem esta permissão porque estiver a escrever uma nova subscrição no âmbito de Olá do recurso de Olá. Olá necessários recursos diferente com base em se estão subscrever tooa tópico de sistema ou um tópico personalizado. Ambos os tipos são descritos nesta secção.

### <a name="system-topics-azure-service-publishers"></a>Tópicos de sistema (editores de serviço do Azure)

Tópicos de sistema, terá de permissão toowrite numa nova subscrição de eventos no âmbito de Olá do evento de Olá de publicação de recursos de Olá. formato de Olá do recurso de Olá é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Por exemplo, toosubscribe tooan evento de uma conta de armazenamento com o nome **myacct**, necessita de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Tópicos personalizados

Tópicos personalizado, terá de permissão toowrite numa nova subscrição de eventos no âmbito de Olá tópico da grelha de eventos de Olá. formato de Olá do recurso de Olá é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Por exemplo, toosubscribe tooa personalizado tópico com o nome **mytopic**, necessita de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Publicação de tópico

Tópicos sobre utiliza a assinatura de acesso partilhado (SAS) ou autenticação de chave. Recomendamos SAS, mas a autenticação de chave fornece programação simple, não sendo compatível com muitos editores de webhook existente. 

Incluir o valor de autenticação de Olá no cabeçalho HTTP Olá. Para SAS, utilize **token de sas aeg** para o valor de cabeçalho de Olá. Para autenticação de chave, utilize **chave de sas aeg** para o valor de cabeçalho de Olá.

### <a name="key-authentication"></a>Autenticação de chave

Autenticação de chave é a forma mais simples de Olá de autenticação. Utilize o formato de Olá:`aeg-sas-key: <your key>`

Por exemplo, transmitir uma chave com: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Tokens SAS

Tokens SAS de grelha de eventos incluem recursos Olá, uma hora de expiração e uma assinatura. Olá formato do token SAS de Olá é: `r={resource}&e={expiration}&s={signature}`.

Olá recurso for o caminho de Olá para Olá tópico toowhich está a enviar eventos. Por exemplo, é um caminho de recurso válido:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Gerar a assinatura Olá a partir de uma chave.

Por exemplo, um válido **token de sas aeg** valor é:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Olá seguinte exemplo cria um token SAS para utilização com grelha de evento:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Controlo de acesso de gestão

Grelha de eventos do Azure permite-lhe toocontrol Olá nível de acesso fornecido toodifferent utilizadores toodo várias operações de gestão, tais como as subscrições de eventos de lista, criar novos e gerar as chaves. Grelha de evento utiliza função de acesso baseado em verificar (RBAC do Azure) para este.

### <a name="operation-types"></a>Tipos de operação

Grelha de eventos do Azure suporta Olá seguintes ações:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Olá últimas três operações retorno potencialmente informações secretas que obtém filtrados normais operações de leitura. É recomendado para que operações de toothese toorestrict acesso. Funções personalizadas podem ser criadas utilizando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Interface de linha de comandos do Azure (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)e Olá [REST API](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Impor a função com base em verificação de acesso (RBAC)

Utilize Olá os seguintes passos tooenforce RBAC para diferentes utilizadores:

#### <a name="create-a-custom-role-definition-file-json"></a>Criar um ficheiro de definição de função personalizada (. JSON)

Olá seguem-se definições de funções de grelha de eventos de exemplo que permitem aos utilizadores tooperform diferentes conjuntos de ações.

**EventGridReadOnlyRole.json**: permitir apenas operações só de leitura.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: permitir ações post restrito, mas não o permitir ações de eliminação.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: permite que todas as ações de grelha de eventos.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Instalação e início de sessão tooAzure CLI

* CLI do Azure versão 0.8.8 ou posterior. versão mais recente do tooinstall Olá e associá-lo com a sua subscrição do Azure, consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md).
* O Azure Resource Manager, na CLI do Azure. Aceda demasiado[Using Olá CLI do Azure com o Gestor de recursos de Olá](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.

#### <a name="create-a-custom-role"></a>Criar uma função personalizada

toocreate uma função personalizada, utilize:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Atribua Olá função tooa utilizador


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Passos seguintes

* Para uma introdução tooEvent grelha, consulte [sobre eventos grelha](overview.md)
