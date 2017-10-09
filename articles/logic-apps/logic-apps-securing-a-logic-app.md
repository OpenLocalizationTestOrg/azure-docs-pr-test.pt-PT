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
# <a name="secure-access-tooyour-logic-apps"></a>Proteger o acesso tooyour logic apps

Existem toohelp disponíveis muitas do ferramentas, a proteger a sua aplicação lógica.

* Proteger o acesso tootrigger uma aplicação lógica (acionador de pedido de HTTP)
* Proteger o acesso toomanage, editar ou de leitura de uma aplicação lógica
* Proteger o acesso toocontents de entradas e saídas para uma execução
* Proteger parâmetros ou entradas dentro ações num fluxo de trabalho
* Proteger o acesso tooservices que receber pedidos de um fluxo de trabalho

## <a name="secure-access-tootrigger"></a>Acesso seguro tootrigger

Quando trabalha com uma aplicação lógica que é acionado um pedido de HTTP ([pedido](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), pode restringir o acesso, para que apenas os clientes autorizados podem acionados a aplicação de lógica de Olá. Todos os pedidos para uma aplicação lógica estão encriptados e protegidos por SSL.

### <a name="shared-access-signature"></a>Assinatura de acesso partilhado

Cada ponto final de pedido para uma aplicação lógica inclui um [assinatura de acesso partilhado (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) como parte do URL de Olá. Cada URL contém um `sp`, `sv`, e `sig` parâmetro de consulta. Permissões especificadas pelo `sp`, e correspondem métodos tooHTTP permitidos, `sv` é Olá versão utilizada toogenerate, e `sig` é utilizado tooauthenticate tootrigger de acesso. assinatura de Olá é gerada utilizando o algoritmo de Olá SHA256 com uma chave secreta em todos os caminhos do URL Olá e propriedades. a chave secreta Olá nunca está exposta e publicada e são mantidos encriptados e armazenados como parte da aplicação de lógica de Olá. A aplicação lógica autoriza apenas acionadores que contém uma assinatura válida criada com uma chave secreta Olá.

#### <a name="regenerate-access-keys"></a>Voltar a gerar chaves de acesso

Pode voltar a gerar uma nova chave segura em qualquer altura através do portal de REST API ou Azure Olá. Todos os URLs atuais que foram gerados anteriormente utilizando a chave de antiga Olá são aplicação de lógica de Olá toofire inválida e já não autorizados.

1. No portal do Azure Olá, abra a aplicação de lógica de Olá pretende tooregenerate uma chave
1. Clique em Olá **chaves de acesso** item de menu em **definições**
1. Escolha tooregenerate chave Olá e processo de Olá concluída

URLs que obter depois da regeneração da sessão com a nova chave de acesso Olá.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Criar URLs de chamada de retorno com uma data de expiração

Se estiver a partilhar Olá URL com outras entidades, pode gerar os URLs com chaves específicas e as datas de expiração conforme necessário. Pode, em seguida, perfeitamente reverta chaves ou certifique-se toofire de acesso de uma aplicação é restrito tooa determinada timespan. Pode especificar uma data de expiração de um URL através de Olá [aplicações lógicas REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

No corpo de Olá, incluir propriedade Olá `NotAfter` como uma cadeia de data JSON, que devolve um URL de chamada de retorno que só é válido até Olá `NotAfter` data e hora.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Criar os URLs com a chave secreta primária ou secundária

Ao gerar ou lista de URLs de chamada de retorno para acionadores baseado em pedidos, também pode especificar o URL de Olá toosign toouse chave.  Pode gerar um URL assinado por uma chave específica através de Olá [aplicações lógicas REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) da seguinte forma:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

No corpo de Olá, incluir propriedade Olá `KeyType` como `Primary` ou `Secondary`.  Esta ação devolve um URL assinado pela chave segura Olá especificada.

### <a name="restrict-incoming-ip-addresses"></a>Restringir os endereços recebidos de IP

Além disso toohello assinatura de acesso partilhado, pode ser útil toorestrict chamar uma aplicação lógica apenas a partir de clientes específicos.  Por exemplo, se gere o ponto final através da API Management do Azure, pode restringir a lógica de Olá aplicação tooonly aceitar o pedido de Olá, quando pedido Olá é proveniente de Olá endereço IP da instância de API Management.

Esta definição pode ser configurada nas definições de aplicação de lógica de Olá:

1. No portal do Azure Olá, abra a aplicação de lógica de Olá pretende tooadd restrições de endereço IP
1. Clique em Olá **configuração de controlo de acesso** item de menu em **definições**
1. Especificar lista Olá de toobe de intervalos de endereços IP aceite pelo acionador Olá

Um intervalo IP válido assume o formato de Olá `192.168.1.1/255`. Se quiser Olá logic app tooonly fire como uma aplicação lógica aninhados, selecione Olá **outras as logic apps** opção. Esta opção escreve um recurso de toohello matriz vazia, que significa que apenas as chamadas de Olá serviço próprio fire (as logic apps de principal) com êxito.

> [!NOTE]
> Pode continuar a executar uma aplicação lógica com um acionador de pedido através da REST API de Olá / gestão `/triggers/{triggerName}/run` independentemente do IP. Este cenário requer autenticação contra Olá API REST do Azure e todos os eventos aparecia na Olá registo de auditoria do Azure. Acesso de conjunto de políticas de controlo em conformidade.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>A definição de intervalos de IP na definição do recurso de Olá

Se estiver a utilizar um [modelo de implementação](logic-apps-create-deploy-template.md) tooautomate as implementações, as definições de intervalo IP Olá podem ser configuradas num modelo do resource Olá.  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>A adição do Azure Active Directory, OAuth ou outro administrativo

tooadd autorização mais protocolos por cima de uma aplicação lógica, [API Management do Azure](https://azure.microsoft.com/services/api-management/) oferece avançado monitorização, segurança, política e a documentação para qualquer ponto final com Olá capacidade tooexpose uma aplicação lógica como uma API. Gestão de API do Azure pode expor um ponto de final público ou privado para a aplicação de lógica de Olá, pode utilizar o Azure Active Directory, certificado, OAuth ou outras normas de segurança. Quando é recebido um pedido, a API Management do Azure reencaminha aplicação lógica Olá pedido toohello (efetuar quaisquer restrições em trânsito ou transformações necessárias). Pode utilizar o intervalo IP entrado Olá definições tooonly de aplicação de lógica de Olá permitem toobe de aplicação de lógica de Olá acionada da gestão de API.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Proteger o acesso toomanage ou editar as logic apps

Pode restringir o acesso toomanagement operações numa aplicação lógica, para que apenas utilizadores específicos ou grupos sejam tooperform capaz de operações no recurso de Olá. As Logic apps utilizam Olá Azure [controlo de acesso baseado em funções (RBAC)](../active-directory/role-based-access-control-configure.md) funcionalidade e podem ser personalizadas com Olá ferramentas mesmas.  Existem algumas funções incorporadas que pode atribuir os membros da sua subscrição tooas também:

* **Contribuinte de aplicação lógica** -fornece acesso tooview, editar e atualização de uma aplicação lógica.  Não é possível remover o recurso de Olá ou efetuar operações de admin.
* **Operador de aplicação lógica** - pode ver a aplicação de lógica de Olá e histórico de execução e ativar/desativar.  Não é possível editar ou atualizar a definição de Olá.

Também pode utilizar [bloqueio de recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent alterar ou eliminar as logic apps. Esta funcionalidade é útil tooprevent recursos de produção de alterações ou eliminações.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Acesso seguro toocontents de Olá histórico de execução

Pode restringir o acesso toocontents de entradas e saídas do anteriores intervalos de endereços do IP toospecific é executado.  

Todos os dados dentro de uma execução de fluxo de trabalho são encriptados em trânsito e rest. Quando é efetuado um histórico de toorun chamada, o serviço Olá autentica o pedido de Olá e fornece ligações toohello pedido e entradas de resposta e saídas. Esta ligação pode ser protegidos pedidos, por isso, apenas tooview conteúdo de um intervalo de endereços IP designado devolver o conteúdo de Olá. Pode utilizar esta capacidade para controlo de acesso adicionais. Pode ainda especificar um endereço IP, como `0.0.0.0` pelo que ninguém pode aceder a entradas/saídas. Apenas um utilizador com permissões de administrador foi possível remover esta restrição, fornecendo a possibilidade de Olá para conteúdos de tooworkflow acesso 'just-in-time'.

Esta definição pode ser configurada dentro de definições de recursos de Olá de Olá portal do Azure:

1. No portal do Azure Olá, abra a aplicação de lógica de Olá pretende tooadd restrições de endereço IP
1. Clique em Olá **configuração de controlo de acesso** item de menu em **definições**
1. Especificar lista Olá intervalos de endereços IP para toocontent de acesso

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>A definição de intervalos de IP na definição do recurso de Olá

Se estiver a utilizar um [modelo de implementação](logic-apps-create-deploy-template.md) tooautomate as implementações, as definições de intervalo IP Olá podem ser configuradas num modelo do resource Olá.  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Proteger os parâmetros e entradas num fluxo de trabalho

Pode querer tooparameterize alguns aspetos de uma definição de fluxo de trabalho para implementação em ambientes. Além disso, alguns parâmetros podem ser parâmetros segurados que não pretende tooappear ao editar um fluxo de trabalho, tais como um ID de cliente e o segredo do cliente para [autenticação do Azure Active Directory](../connectors/connectors-native-http.md#authentication) de uma ação de HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Utilizar parâmetros e parâmetros segurados

tooaccess Olá hello valor de um parâmetro de recurso no tempo de execução, [linguagem de definição de fluxo de trabalho](http://aka.ms/logicappsdocs) fornece um `@parameters()` operação. Além disso, pode [especificar parâmetros no modelo de implementação de recursos de Olá](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Porém, se especificar o tipo de parâmetro de Olá como `securestring`, parâmetro Olá não será devolvido com rest Olá Olá da definição de recurso e não estar acessível através da visualização dos recursos de Olá após a implementação.

> [!NOTE]
> Se o parâmetro é utilizado em nem corpo de um pedido de cabeçalhos de Olá, parâmetro Olá poderão ser visível ao aceder ao histórico de Olá executar e pedidos de HTTP de saída. Certifique-se de que tooset as políticas de acesso ao conteúdo em conformidade.
> Cabeçalhos de autorização nunca são visíveis através de entradas e saídas. Por isso, se está a ser utilizado o segredo de Olá existe, Olá segredo não é recuperável.

#### <a name="resource-deployment-template-with-secrets"></a>Modelo de implementação de recursos com segredos

Olá exemplo seguinte mostra uma implementação que faça referência a um parâmetro seguro do `secret` no tempo de execução. No ficheiro de parâmetros separados, pode especificar valor de ambiente de Olá para Olá `secret`, ou utilize [do Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve segredos no momento de implementar.

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

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Proteger o acesso tooservices pedidos de receção de um fluxo de trabalho

Existem muitas formas toohelp segura que tooaccess necessita de qualquer aplicação de lógica de Olá de ponto final.

### <a name="using-authentication-on-outbound-requests"></a>Utilizar a autenticação nos pedidos de saída

Ao trabalhar com um HTTP, HTTP + Swagger (API aberto) ou Webhook ação, pode adicionar o pedido de toohello de autenticação a ser enviado. Pode incluir a autenticação básica, autenticação de certificado ou a autenticação do Azure Active Directory. Detalhes sobre como tooconfigure esta autenticação pode ser encontrada [neste artigo](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Restringir o acesso toologic endereços IP aplicação

Todas as chamadas a partir das logic apps provenientes de um conjunto específico de endereços IP por região. Pode adicionar filtragem adicionais tooonly aceitar pedidos das designados de endereços IP. Para obter uma lista desses endereços IP, consulte [limites de aplicação de lógica e configuração](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Conectividade no local

As Logic apps fornecem integração com vários serviços tooprovide, segura e fiável no local comunicação.

#### <a name="on-premises-data-gateway"></a>Gateway de dados no local

Muitos conetores geridos para aplicações lógicas fornecem conectividade segura sistemas tooon local, incluindo o sistema de ficheiros, SQL Server, SharePoint, DB2 e muito mais. gateway de Olá transmite dados a partir de origens do local em canais encriptados através de Olá Service Bus do Azure. Todo o tráfego origina como tráfego de saída seguro de agente de gateway Olá. Saiba mais sobre [como funciona o gateway de dados de Olá](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>API Management do Azure

[Gestão de API do Azure](https://azure.microsoft.com/services/api-management/) tem opções de conectividade no local, incluindo a integração de ExpressRoute e de VPN de site a site para sistemas de tooon local de proxy e comunicação seguros. Olá Designer de aplicação lógica, pode rapidamente selecionar uma API exposta a partir de API Management do Azure dentro de um fluxo de trabalho, que fornece acesso rápido sistemas tooon local.

#### <a name="hybrid-connections-from-azure-app-service"></a>Ligações híbridas do App Service do Azure

Pode utilizar a funcionalidade de ligação híbrida do Olá no local para a API do Azure e Web apps toocommunicate no local.  Detalhes sobre as ligações híbridas e como pode ser encontrado tooconfigure [neste artigo](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Passos seguintes
[Criar um modelo de implementação](logic-apps-create-deploy-template.md)  
[Processamento de exceções](logic-apps-exception-handling.md)  
[Monitorizar as aplicações lógicas](logic-apps-monitor-your-logic-apps.md)  
[Diagnosticar problemas e falhas de aplicação lógica](logic-apps-diagnosing-failures.md)  
