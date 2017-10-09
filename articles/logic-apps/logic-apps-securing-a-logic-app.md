---
title: aaaSecure aceder tooAzure Logic Apps | Microsoft Docs
description: "Adicione a segurança para proteger o acesso tootriggers, entradas e saídas, parâmetros de ação e serviços utilizado com fluxos de trabalho no Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="158e1-103">Proteger o acesso tooyour logic apps</span><span class="sxs-lookup"><span data-stu-id="158e1-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="158e1-104">Existem toohelp disponíveis muitas do ferramentas, a proteger a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="158e1-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="158e1-105">Proteger o acesso tootrigger uma aplicação lógica (acionador de pedido de HTTP)</span><span class="sxs-lookup"><span data-stu-id="158e1-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="158e1-106">Proteger o acesso toomanage, editar ou de leitura de uma aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="158e1-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="158e1-107">Proteger o acesso toocontents de entradas e saídas para uma execução</span><span class="sxs-lookup"><span data-stu-id="158e1-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="158e1-108">Proteger parâmetros ou entradas dentro ações num fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="158e1-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="158e1-109">Proteger o acesso tooservices que receber pedidos de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="158e1-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="158e1-110">Acesso seguro tootrigger</span><span class="sxs-lookup"><span data-stu-id="158e1-110">Secure access tootrigger</span></span>

<span data-ttu-id="158e1-111">Quando trabalha com uma aplicação lógica que é acionado um pedido de HTTP ([pedido](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), pode restringir o acesso, para que apenas os clientes autorizados podem acionados a aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="158e1-112">Todos os pedidos para uma aplicação lógica estão encriptados e protegidos por SSL.</span><span class="sxs-lookup"><span data-stu-id="158e1-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="158e1-113">Assinatura de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="158e1-113">Shared Access Signature</span></span>

<span data-ttu-id="158e1-114">Cada ponto final de pedido para uma aplicação lógica inclui um [assinatura de acesso partilhado (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) como parte do URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="158e1-115">Cada URL contém um `sp`, `sv`, e `sig` parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="158e1-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="158e1-116">Permissões especificadas pelo `sp`, e correspondem métodos tooHTTP permitidos, `sv` é Olá versão utilizada toogenerate, e `sig` é utilizado tooauthenticate tootrigger de acesso.</span><span class="sxs-lookup"><span data-stu-id="158e1-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="158e1-117">assinatura de Olá é gerada utilizando o algoritmo de Olá SHA256 com uma chave secreta em todos os caminhos do URL Olá e propriedades.</span><span class="sxs-lookup"><span data-stu-id="158e1-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="158e1-118">a chave secreta Olá nunca está exposta e publicada e são mantidos encriptados e armazenados como parte da aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="158e1-119">A aplicação lógica autoriza apenas acionadores que contém uma assinatura válida criada com uma chave secreta Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="158e1-120">Voltar a gerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="158e1-120">Regenerate access keys</span></span>

<span data-ttu-id="158e1-121">Pode voltar a gerar uma nova chave segura em qualquer altura através do portal de REST API ou Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="158e1-122">Todos os URLs atuais que foram gerados anteriormente utilizando a chave de antiga Olá são aplicação de lógica de Olá toofire inválida e já não autorizados.</span><span class="sxs-lookup"><span data-stu-id="158e1-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="158e1-123">No portal do Azure Olá, abra a aplicação de lógica de Olá pretende tooregenerate uma chave</span><span class="sxs-lookup"><span data-stu-id="158e1-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="158e1-124">Clique em Olá **chaves de acesso** item de menu em **definições**</span><span class="sxs-lookup"><span data-stu-id="158e1-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="158e1-125">Escolha tooregenerate chave Olá e processo de Olá concluída</span><span class="sxs-lookup"><span data-stu-id="158e1-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="158e1-126">URLs que obter depois da regeneração da sessão com a nova chave de acesso Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="158e1-127">Criar URLs de chamada de retorno com uma data de expiração</span><span class="sxs-lookup"><span data-stu-id="158e1-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="158e1-128">Se estiver a partilhar Olá URL com outras entidades, pode gerar os URLs com chaves específicas e as datas de expiração conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="158e1-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="158e1-129">Pode, em seguida, perfeitamente reverta chaves ou certifique-se toofire de acesso de uma aplicação é restrito tooa determinada timespan.</span><span class="sxs-lookup"><span data-stu-id="158e1-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="158e1-130">Pode especificar uma data de expiração de um URL através de Olá [aplicações lógicas REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="158e1-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="158e1-131">No corpo de Olá, incluir propriedade Olá `NotAfter` como uma cadeia de data JSON, que devolve um URL de chamada de retorno que só é válido até Olá `NotAfter` data e hora.</span><span class="sxs-lookup"><span data-stu-id="158e1-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="158e1-132">Criar os URLs com a chave secreta primária ou secundária</span><span class="sxs-lookup"><span data-stu-id="158e1-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="158e1-133">Ao gerar ou lista de URLs de chamada de retorno para acionadores baseado em pedidos, também pode especificar o URL de Olá toosign toouse chave.</span><span class="sxs-lookup"><span data-stu-id="158e1-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="158e1-134">Pode gerar um URL assinado por uma chave específica através de Olá [aplicações lógicas REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="158e1-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="158e1-135">No corpo de Olá, incluir propriedade Olá `KeyType` como `Primary` ou `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="158e1-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="158e1-136">Esta ação devolve um URL assinado pela chave segura Olá especificada.</span><span class="sxs-lookup"><span data-stu-id="158e1-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="158e1-137">Restringir os endereços recebidos de IP</span><span class="sxs-lookup"><span data-stu-id="158e1-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="158e1-138">Além disso toohello assinatura de acesso partilhado, pode ser útil toorestrict chamar uma aplicação lógica apenas a partir de clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="158e1-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="158e1-139">Por exemplo, se gere o ponto final através da API Management do Azure, pode restringir a lógica de Olá aplicação tooonly aceitar o pedido de Olá, quando pedido Olá é proveniente de Olá endereço IP da instância de API Management.</span><span class="sxs-lookup"><span data-stu-id="158e1-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="158e1-140">Esta definição pode ser configurada nas definições de aplicação de lógica de Olá:</span><span class="sxs-lookup"><span data-stu-id="158e1-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="158e1-141">No portal do Azure Olá, abra a aplicação de lógica de Olá pretende tooadd restrições de endereço IP</span><span class="sxs-lookup"><span data-stu-id="158e1-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="158e1-142">Clique em Olá **configuração de controlo de acesso** item de menu em **definições**</span><span class="sxs-lookup"><span data-stu-id="158e1-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="158e1-143">Especificar lista Olá de toobe de intervalos de endereços IP aceite pelo acionador Olá</span><span class="sxs-lookup"><span data-stu-id="158e1-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="158e1-144">Um intervalo IP válido assume o formato de Olá `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="158e1-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="158e1-145">Se quiser Olá logic app tooonly fire como uma aplicação lógica aninhados, selecione Olá **outras as logic apps** opção.</span><span class="sxs-lookup"><span data-stu-id="158e1-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="158e1-146">Esta opção escreve um recurso de toohello matriz vazia, que significa que apenas as chamadas de Olá serviço próprio fire (as logic apps de principal) com êxito.</span><span class="sxs-lookup"><span data-stu-id="158e1-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="158e1-147">Pode continuar a executar uma aplicação lógica com um acionador de pedido através da REST API de Olá / gestão `/triggers/{triggerName}/run` independentemente do IP.</span><span class="sxs-lookup"><span data-stu-id="158e1-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="158e1-148">Este cenário requer autenticação contra Olá API REST do Azure e todos os eventos aparecia na Olá registo de auditoria do Azure.</span><span class="sxs-lookup"><span data-stu-id="158e1-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="158e1-149">Acesso de conjunto de políticas de controlo em conformidade.</span><span class="sxs-lookup"><span data-stu-id="158e1-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="158e1-150">A definição de intervalos de IP na definição do recurso de Olá</span><span class="sxs-lookup"><span data-stu-id="158e1-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="158e1-151">Se estiver a utilizar um [modelo de implementação](logic-apps-create-deploy-template.md) tooautomate as implementações, as definições de intervalo IP Olá podem ser configuradas num modelo do resource Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="158e1-152">A adição do Azure Active Directory, OAuth ou outro administrativo</span><span class="sxs-lookup"><span data-stu-id="158e1-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="158e1-153">tooadd autorização mais protocolos por cima de uma aplicação lógica, [API Management do Azure](https://azure.microsoft.com/services/api-management/) oferece avançado monitorização, segurança, política e a documentação para qualquer ponto final com Olá capacidade tooexpose uma aplicação lógica como uma API.</span><span class="sxs-lookup"><span data-stu-id="158e1-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="158e1-154">Gestão de API do Azure pode expor um ponto de final público ou privado para a aplicação de lógica de Olá, pode utilizar o Azure Active Directory, certificado, OAuth ou outras normas de segurança.</span><span class="sxs-lookup"><span data-stu-id="158e1-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="158e1-155">Quando é recebido um pedido, a API Management do Azure reencaminha aplicação lógica Olá pedido toohello (efetuar quaisquer restrições em trânsito ou transformações necessárias).</span><span class="sxs-lookup"><span data-stu-id="158e1-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="158e1-156">Pode utilizar o intervalo IP entrado Olá definições tooonly de aplicação de lógica de Olá permitem toobe de aplicação de lógica de Olá acionada da gestão de API.</span><span class="sxs-lookup"><span data-stu-id="158e1-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="158e1-157">Proteger o acesso toomanage ou editar as logic apps</span><span class="sxs-lookup"><span data-stu-id="158e1-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="158e1-158">Pode restringir o acesso toomanagement operações numa aplicação lógica, para que apenas utilizadores específicos ou grupos sejam tooperform capaz de operações no recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="158e1-159">As Logic apps utilizam Olá Azure [controlo de acesso baseado em funções (RBAC)](../active-directory/role-based-access-control-configure.md) funcionalidade e podem ser personalizadas com Olá ferramentas mesmas.</span><span class="sxs-lookup"><span data-stu-id="158e1-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="158e1-160">Existem algumas funções incorporadas que pode atribuir os membros da sua subscrição tooas também:</span><span class="sxs-lookup"><span data-stu-id="158e1-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="158e1-161">**Contribuinte de aplicação lógica** -fornece acesso tooview, editar e atualização de uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="158e1-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="158e1-162">Não é possível remover o recurso de Olá ou efetuar operações de admin.</span><span class="sxs-lookup"><span data-stu-id="158e1-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="158e1-163">**Operador de aplicação lógica** - pode ver a aplicação de lógica de Olá e histórico de execução e ativar/desativar.</span><span class="sxs-lookup"><span data-stu-id="158e1-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="158e1-164">Não é possível editar ou atualizar a definição de Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="158e1-165">Também pode utilizar [bloqueio de recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent alterar ou eliminar as logic apps.</span><span class="sxs-lookup"><span data-stu-id="158e1-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="158e1-166">Esta funcionalidade é útil tooprevent recursos de produção de alterações ou eliminações.</span><span class="sxs-lookup"><span data-stu-id="158e1-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="158e1-167">Acesso seguro toocontents de Olá histórico de execução</span><span class="sxs-lookup"><span data-stu-id="158e1-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="158e1-168">Pode restringir o acesso toocontents de entradas e saídas do anteriores intervalos de endereços do IP toospecific é executado.</span><span class="sxs-lookup"><span data-stu-id="158e1-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="158e1-169">Todos os dados dentro de uma execução de fluxo de trabalho são encriptados em trânsito e rest.</span><span class="sxs-lookup"><span data-stu-id="158e1-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="158e1-170">Quando é efetuado um histórico de toorun chamada, o serviço Olá autentica o pedido de Olá e fornece ligações toohello pedido e entradas de resposta e saídas.</span><span class="sxs-lookup"><span data-stu-id="158e1-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="158e1-171">Esta ligação pode ser protegidos pedidos, por isso, apenas tooview conteúdo de um intervalo de endereços IP designado devolver o conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="158e1-172">Pode utilizar esta capacidade para controlo de acesso adicionais.</span><span class="sxs-lookup"><span data-stu-id="158e1-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="158e1-173">Pode ainda especificar um endereço IP, como `0.0.0.0` pelo que ninguém pode aceder a entradas/saídas.</span><span class="sxs-lookup"><span data-stu-id="158e1-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="158e1-174">Apenas um utilizador com permissões de administrador foi possível remover esta restrição, fornecendo a possibilidade de Olá para conteúdos de tooworkflow acesso 'just-in-time'.</span><span class="sxs-lookup"><span data-stu-id="158e1-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="158e1-175">Esta definição pode ser configurada dentro de definições de recursos de Olá de Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="158e1-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="158e1-176">No portal do Azure Olá, abra a aplicação de lógica de Olá pretende tooadd restrições de endereço IP</span><span class="sxs-lookup"><span data-stu-id="158e1-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="158e1-177">Clique em Olá **configuração de controlo de acesso** item de menu em **definições**</span><span class="sxs-lookup"><span data-stu-id="158e1-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="158e1-178">Especificar lista Olá intervalos de endereços IP para toocontent de acesso</span><span class="sxs-lookup"><span data-stu-id="158e1-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="158e1-179">A definição de intervalos de IP na definição do recurso de Olá</span><span class="sxs-lookup"><span data-stu-id="158e1-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="158e1-180">Se estiver a utilizar um [modelo de implementação](logic-apps-create-deploy-template.md) tooautomate as implementações, as definições de intervalo IP Olá podem ser configuradas num modelo do resource Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="158e1-181">Proteger os parâmetros e entradas num fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="158e1-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="158e1-182">Pode querer tooparameterize alguns aspetos de uma definição de fluxo de trabalho para implementação em ambientes.</span><span class="sxs-lookup"><span data-stu-id="158e1-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="158e1-183">Além disso, alguns parâmetros podem ser parâmetros segurados que não pretende tooappear ao editar um fluxo de trabalho, tais como um ID de cliente e o segredo do cliente para [autenticação do Azure Active Directory](../connectors/connectors-native-http.md#authentication) de uma ação de HTTP.</span><span class="sxs-lookup"><span data-stu-id="158e1-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="158e1-184">Utilizar parâmetros e parâmetros segurados</span><span class="sxs-lookup"><span data-stu-id="158e1-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="158e1-185">tooaccess Olá hello valor de um parâmetro de recurso no tempo de execução, [linguagem de definição de fluxo de trabalho](http://aka.ms/logicappsdocs) fornece um `@parameters()` operação.</span><span class="sxs-lookup"><span data-stu-id="158e1-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="158e1-186">Além disso, pode [especificar parâmetros no modelo de implementação de recursos de Olá](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="158e1-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="158e1-187">Porém, se especificar o tipo de parâmetro de Olá como `securestring`, parâmetro Olá não será devolvido com rest Olá Olá da definição de recurso e não estar acessível através da visualização dos recursos de Olá após a implementação.</span><span class="sxs-lookup"><span data-stu-id="158e1-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="158e1-188">Se o parâmetro é utilizado em nem corpo de um pedido de cabeçalhos de Olá, parâmetro Olá poderão ser visível ao aceder ao histórico de Olá executar e pedidos de HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="158e1-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="158e1-189">Certifique-se de que tooset as políticas de acesso ao conteúdo em conformidade.</span><span class="sxs-lookup"><span data-stu-id="158e1-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="158e1-190">Cabeçalhos de autorização nunca são visíveis através de entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="158e1-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="158e1-191">Por isso, se está a ser utilizado o segredo de Olá existe, Olá segredo não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="158e1-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="158e1-192">Modelo de implementação de recursos com segredos</span><span class="sxs-lookup"><span data-stu-id="158e1-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="158e1-193">Olá exemplo seguinte mostra uma implementação que faça referência a um parâmetro seguro do `secret` no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="158e1-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="158e1-194">No ficheiro de parâmetros separados, pode especificar valor de ambiente de Olá para Olá `secret`, ou utilize [do Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve segredos no momento de implementar.</span><span class="sxs-lookup"><span data-stu-id="158e1-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="158e1-195">Proteger o acesso tooservices pedidos de receção de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="158e1-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="158e1-196">Existem muitas formas toohelp segura que tooaccess necessita de qualquer aplicação de lógica de Olá de ponto final.</span><span class="sxs-lookup"><span data-stu-id="158e1-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="158e1-197">Utilizar a autenticação nos pedidos de saída</span><span class="sxs-lookup"><span data-stu-id="158e1-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="158e1-198">Ao trabalhar com um HTTP, HTTP + Swagger (API aberto) ou Webhook ação, pode adicionar o pedido de toohello de autenticação a ser enviado.</span><span class="sxs-lookup"><span data-stu-id="158e1-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="158e1-199">Pode incluir a autenticação básica, autenticação de certificado ou a autenticação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="158e1-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="158e1-200">Detalhes sobre como tooconfigure esta autenticação pode ser encontrada [neste artigo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="158e1-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="158e1-201">Restringir o acesso toologic endereços IP aplicação</span><span class="sxs-lookup"><span data-stu-id="158e1-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="158e1-202">Todas as chamadas a partir das logic apps provenientes de um conjunto específico de endereços IP por região.</span><span class="sxs-lookup"><span data-stu-id="158e1-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="158e1-203">Pode adicionar filtragem adicionais tooonly aceitar pedidos das designados de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="158e1-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="158e1-204">Para obter uma lista desses endereços IP, consulte [limites de aplicação de lógica e configuração](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="158e1-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="158e1-205">Conectividade no local</span><span class="sxs-lookup"><span data-stu-id="158e1-205">On-premises connectivity</span></span>

<span data-ttu-id="158e1-206">As Logic apps fornecem integração com vários serviços tooprovide, segura e fiável no local comunicação.</span><span class="sxs-lookup"><span data-stu-id="158e1-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="158e1-207">Gateway de dados no local</span><span class="sxs-lookup"><span data-stu-id="158e1-207">On-premises data gateway</span></span>

<span data-ttu-id="158e1-208">Muitos conetores geridos para aplicações lógicas fornecem conectividade segura sistemas tooon local, incluindo o sistema de ficheiros, SQL Server, SharePoint, DB2 e muito mais.</span><span class="sxs-lookup"><span data-stu-id="158e1-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="158e1-209">gateway de Olá transmite dados a partir de origens do local em canais encriptados através de Olá Service Bus do Azure.</span><span class="sxs-lookup"><span data-stu-id="158e1-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="158e1-210">Todo o tráfego origina como tráfego de saída seguro de agente de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="158e1-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="158e1-211">Saiba mais sobre [como funciona o gateway de dados de Olá](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="158e1-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="158e1-212">API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="158e1-212">Azure API Management</span></span>

<span data-ttu-id="158e1-213">[Gestão de API do Azure](https://azure.microsoft.com/services/api-management/) tem opções de conectividade no local, incluindo a integração de ExpressRoute e de VPN de site a site para sistemas de tooon local de proxy e comunicação seguros.</span><span class="sxs-lookup"><span data-stu-id="158e1-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="158e1-214">Olá Designer de aplicação lógica, pode rapidamente selecionar uma API exposta a partir de API Management do Azure dentro de um fluxo de trabalho, que fornece acesso rápido sistemas tooon local.</span><span class="sxs-lookup"><span data-stu-id="158e1-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="158e1-215">Ligações híbridas do App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="158e1-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="158e1-216">Pode utilizar a funcionalidade de ligação híbrida do Olá no local para a API do Azure e Web apps toocommunicate no local.</span><span class="sxs-lookup"><span data-stu-id="158e1-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="158e1-217">Detalhes sobre as ligações híbridas e como pode ser encontrado tooconfigure [neste artigo](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="158e1-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="158e1-218">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="158e1-218">Next steps</span></span>
[<span data-ttu-id="158e1-219">Criar um modelo de implementação</span><span class="sxs-lookup"><span data-stu-id="158e1-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="158e1-220">Processamento de exceções</span><span class="sxs-lookup"><span data-stu-id="158e1-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="158e1-221">Monitorizar as aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="158e1-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="158e1-222">Diagnosticar problemas e falhas de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="158e1-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
