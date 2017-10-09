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
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="98519-103">Segurança de grelha de eventos e autenticação</span><span class="sxs-lookup"><span data-stu-id="98519-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="98519-104">Grelha de eventos do Azure tem três tipos de autenticação:</span><span class="sxs-lookup"><span data-stu-id="98519-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="98519-105">Subscrições de eventos</span><span class="sxs-lookup"><span data-stu-id="98519-105">Event subscriptions</span></span>
* <span data-ttu-id="98519-106">Publicação de eventos</span><span class="sxs-lookup"><span data-stu-id="98519-106">Event publishing</span></span>
* <span data-ttu-id="98519-107">Entrega de eventos do WebHook</span><span class="sxs-lookup"><span data-stu-id="98519-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="98519-108">Entrega de eventos do WebHook</span><span class="sxs-lookup"><span data-stu-id="98519-108">WebHook Event delivery</span></span>

<span data-ttu-id="98519-109">Webhooks são um dos muitos eventos de tooreceive formas em tempo real da grelha de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="98519-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="98519-110">Sempre que há um novo toobe pronto de evento entregue, grelha de eventos envia um pedido HTTP com tooyour WebHook com evento Olá no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="98519-111">Quando registar o próprio ponto final de WebHook a grelha de evento, envia a um pedido POST com um código de validação simples na propriedade de ponto final de tooprove de ordem.</span><span class="sxs-lookup"><span data-stu-id="98519-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="98519-112">A aplicação tem toorespond por echoing código de validação de Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="98519-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="98519-113">Grelha de evento não irá fornecer eventos pontos finais de tooWebHook que não passaram a validação de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="98519-114">Detalhes de validação:</span><span class="sxs-lookup"><span data-stu-id="98519-114">Validation details:</span></span>

* <span data-ttu-id="98519-115">Grelha de evento mensagens do momento Olá da subscrição de evento criação/atualização, um ponto final toohello "SubscriptionValidationEvent" eventos destino.</span><span class="sxs-lookup"><span data-stu-id="98519-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="98519-116">eventos de Olá contém um valor de cabeçalho "Tipo de evento: validação".</span><span class="sxs-lookup"><span data-stu-id="98519-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="98519-117">tem de corpo de evento Olá Olá mesmo esquema que outros eventos de grelha de eventos.</span><span class="sxs-lookup"><span data-stu-id="98519-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="98519-118">dados de eventos de Olá incluem uma propriedade de "ValidationCode" com uma cadeia gerada aleatoriamente, por exemplo "ValidationCode: acb13...".</span><span class="sxs-lookup"><span data-stu-id="98519-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="98519-119">Na propriedade de ponto final de tooprove ordem, por exemplo de código de validação de back-Olá de eco "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="98519-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="98519-120">Por fim, é importante toonote que a grelha de eventos do Azure suporta apenas pontos finais de webhook HTTPS.</span><span class="sxs-lookup"><span data-stu-id="98519-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="98519-121">Subscrição de evento</span><span class="sxs-lookup"><span data-stu-id="98519-121">Event subscription</span></span>

<span data-ttu-id="98519-122">evento de tooan toosubscribe, tem de ter Olá **Microsoft.EventGrid/EventSubscriptions/Write** necessária a permissão no Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="98519-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="98519-123">Tem esta permissão porque estiver a escrever uma nova subscrição no âmbito de Olá do recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="98519-124">Olá necessários recursos diferente com base em se estão subscrever tooa tópico de sistema ou um tópico personalizado.</span><span class="sxs-lookup"><span data-stu-id="98519-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="98519-125">Ambos os tipos são descritos nesta secção.</span><span class="sxs-lookup"><span data-stu-id="98519-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="98519-126">Tópicos de sistema (editores de serviço do Azure)</span><span class="sxs-lookup"><span data-stu-id="98519-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="98519-127">Tópicos de sistema, terá de permissão toowrite numa nova subscrição de eventos no âmbito de Olá do evento de Olá de publicação de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="98519-128">formato de Olá do recurso de Olá é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="98519-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="98519-129">Por exemplo, toosubscribe tooan evento de uma conta de armazenamento com o nome **myacct**, necessita de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="98519-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="98519-130">Tópicos personalizados</span><span class="sxs-lookup"><span data-stu-id="98519-130">Custom topics</span></span>

<span data-ttu-id="98519-131">Tópicos personalizado, terá de permissão toowrite numa nova subscrição de eventos no âmbito de Olá tópico da grelha de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="98519-132">formato de Olá do recurso de Olá é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="98519-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="98519-133">Por exemplo, toosubscribe tooa personalizado tópico com o nome **mytopic**, necessita de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="98519-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="98519-134">Publicação de tópico</span><span class="sxs-lookup"><span data-stu-id="98519-134">Topic publishing</span></span>

<span data-ttu-id="98519-135">Tópicos sobre utiliza a assinatura de acesso partilhado (SAS) ou autenticação de chave.</span><span class="sxs-lookup"><span data-stu-id="98519-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="98519-136">Recomendamos SAS, mas a autenticação de chave fornece programação simple, não sendo compatível com muitos editores de webhook existente.</span><span class="sxs-lookup"><span data-stu-id="98519-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="98519-137">Incluir o valor de autenticação de Olá no cabeçalho HTTP Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="98519-138">Para SAS, utilize **token de sas aeg** para o valor de cabeçalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="98519-139">Para autenticação de chave, utilize **chave de sas aeg** para o valor de cabeçalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="98519-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="98519-140">Autenticação de chave</span><span class="sxs-lookup"><span data-stu-id="98519-140">Key authentication</span></span>

<span data-ttu-id="98519-141">Autenticação de chave é a forma mais simples de Olá de autenticação.</span><span class="sxs-lookup"><span data-stu-id="98519-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="98519-142">Utilize o formato de Olá:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="98519-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="98519-143">Por exemplo, transmitir uma chave com:</span><span class="sxs-lookup"><span data-stu-id="98519-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="98519-144">Tokens SAS</span><span class="sxs-lookup"><span data-stu-id="98519-144">SAS tokens</span></span>

<span data-ttu-id="98519-145">Tokens SAS de grelha de eventos incluem recursos Olá, uma hora de expiração e uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="98519-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="98519-146">Olá formato do token SAS de Olá é: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="98519-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="98519-147">Olá recurso for o caminho de Olá para Olá tópico toowhich está a enviar eventos.</span><span class="sxs-lookup"><span data-stu-id="98519-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="98519-148">Por exemplo, é um caminho de recurso válido:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="98519-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="98519-149">Gerar a assinatura Olá a partir de uma chave.</span><span class="sxs-lookup"><span data-stu-id="98519-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="98519-150">Por exemplo, um válido **token de sas aeg** valor é:</span><span class="sxs-lookup"><span data-stu-id="98519-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="98519-151">Olá seguinte exemplo cria um token SAS para utilização com grelha de evento:</span><span class="sxs-lookup"><span data-stu-id="98519-151">hello following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="98519-152">Controlo de acesso de gestão</span><span class="sxs-lookup"><span data-stu-id="98519-152">Management Access Control</span></span>

<span data-ttu-id="98519-153">Grelha de eventos do Azure permite-lhe toocontrol Olá nível de acesso fornecido toodifferent utilizadores toodo várias operações de gestão, tais como as subscrições de eventos de lista, criar novos e gerar as chaves.</span><span class="sxs-lookup"><span data-stu-id="98519-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="98519-154">Grelha de evento utiliza função de acesso baseado em verificar (RBAC do Azure) para este.</span><span class="sxs-lookup"><span data-stu-id="98519-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="98519-155">Tipos de operação</span><span class="sxs-lookup"><span data-stu-id="98519-155">Operation types</span></span>

<span data-ttu-id="98519-156">Grelha de eventos do Azure suporta Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="98519-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="98519-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="98519-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="98519-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="98519-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="98519-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="98519-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="98519-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="98519-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="98519-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="98519-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="98519-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="98519-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="98519-163">Olá últimas três operações retorno potencialmente informações secretas que obtém filtrados normais operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="98519-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="98519-164">É recomendado para que operações de toothese toorestrict acesso.</span><span class="sxs-lookup"><span data-stu-id="98519-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="98519-165">Funções personalizadas podem ser criadas utilizando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Interface de linha de comandos do Azure (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)e Olá [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="98519-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="98519-166">Impor a função com base em verificação de acesso (RBAC)</span><span class="sxs-lookup"><span data-stu-id="98519-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="98519-167">Utilize Olá os seguintes passos tooenforce RBAC para diferentes utilizadores:</span><span class="sxs-lookup"><span data-stu-id="98519-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="98519-168">Criar um ficheiro de definição de função personalizada (. JSON)</span><span class="sxs-lookup"><span data-stu-id="98519-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="98519-169">Olá seguem-se definições de funções de grelha de eventos de exemplo que permitem aos utilizadores tooperform diferentes conjuntos de ações.</span><span class="sxs-lookup"><span data-stu-id="98519-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="98519-170">**EventGridReadOnlyRole.json**: permitir apenas operações só de leitura.</span><span class="sxs-lookup"><span data-stu-id="98519-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="98519-171">**EventGridNoDeleteListKeysRole.json**: permitir ações post restrito, mas não o permitir ações de eliminação.</span><span class="sxs-lookup"><span data-stu-id="98519-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="98519-172">**EventGridContributorRole.json**: permite que todas as ações de grelha de eventos.</span><span class="sxs-lookup"><span data-stu-id="98519-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="98519-173">Instalação e início de sessão tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="98519-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="98519-174">CLI do Azure versão 0.8.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="98519-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="98519-175">versão mais recente do tooinstall Olá e associá-lo com a sua subscrição do Azure, consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="98519-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="98519-176">O Azure Resource Manager, na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="98519-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="98519-177">Aceda demasiado[Using Olá CLI do Azure com o Gestor de recursos de Olá](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="98519-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="98519-178">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="98519-178">Create a custom role</span></span>

<span data-ttu-id="98519-179">toocreate uma função personalizada, utilize:</span><span class="sxs-lookup"><span data-stu-id="98519-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="98519-180">Atribua Olá função tooa utilizador</span><span class="sxs-lookup"><span data-stu-id="98519-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="98519-181">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="98519-181">Next steps</span></span>

* <span data-ttu-id="98519-182">Para uma introdução tooEvent grelha, consulte [sobre eventos grelha](overview.md)</span><span class="sxs-lookup"><span data-stu-id="98519-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
