---
title: "aaaAzure reencaminhamento de autenticação e autorização | Microsoft Docs"
description: "Descrição geral da autenticação da assinatura de acesso partilhado (SAS) no reencaminhamento do Azure"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Autorização e autenticação de reencaminhamento do Azure
As aplicações podem autenticar tooAzure reencaminhamento através da autenticação da assinatura de acesso partilhado (SAS). Semelhante demasiado[mensagens do Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md), aplicações tooauthenticate toohello serviço de reencaminhamento do Azure com uma chave de acesso configurada no espaço de nomes de reencaminhamento de Olá permite a autenticação SAS. Em seguida, pode utilizar esta chave toogenerate um token de assinatura de acesso partilhado que os clientes podem utilizar o serviço de reencaminhamento de toohello tooauthenticate.

## <a name="shared-access-signature-authentication"></a>Autenticação da assinatura de acesso partilhada
[Autenticação de SAS](../service-bus-messaging/service-bus-sas.md) permite toogrant um utilizador aceder tooAzure reencaminhamento a recursos com direitos específicos. Autenticação de SAS envolve a configuração de Olá de uma chave criptográfica com direitos associados num recurso. Os clientes, em seguida, podem obter acesso toothat recursos através da apresentação de um token SAS, que consiste em Olá URI do recurso que está a ser acedido e uma expiração assinada com Olá configurado chave.

Pode configurar as chaves de SAS num espaço de nomes de reencaminhamento. Ao contrário das mensagens do Service Bus, [ligações híbridas de reencaminhamento](relay-hybrid-connections-protocol.md) suporta os remetentes não autorizados ou anonymous. Pode ativar o acesso anónimo para a entidade de Olá quando cria, conforme mostrado no Olá captura a partir do portal de Olá de ecrã a seguir:

![][0]

toouse SAS, pode configurar um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto de um espaço de nomes de reencaminhamento que consiste Olá seguinte:

* *KeyName* que identifica a regra de Olá.
* *PrimaryKey* é uma chave criptográfica utilizada toosign/validar os tokens SAS.
* *SecondaryKey* é uma chave criptográfica utilizada toosign/validar os tokens SAS.
* *Direitos* que representa a coleção de Olá de escuta, enviar ou faça a gestão de direitos concedidos.

Regras de autorização configuradas ao nível do espaço de nomes de Olá conceder acesso ligações de reencaminhamento tooall num espaço de nomes para os clientes com tokens assinados utilizando a chave de Olá correspondente. Cópia de segurança too12 dessas regras de autorização podem ser configuradas num espaço de nomes de reencaminhamento. Por predefinição, um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) com todos os direitos está configurado para cada espaço de nomes ao que está a ser aprovisionado pela primeira vez.

tooaccess uma entidade, Olá cliente necessita de um token SAS gerado utilizando específico [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token SAS de Olá é gerado com uma chave criptográfica associada de regra de autorização de Olá Olá HMAC-SHA256 de uma cadeia de recurso que constituem o recurso de Olá acesso de toowhich URI foi reclamado e uma expiração.

Suporte de autenticação SAS para o reencaminhamento do Azure é incluído em versões de SDK .NET da Azure Olá 2.0 e posterior. SAS inclui suporte para um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Todas as APIs que aceitam uma cadeia de ligação como um parâmetro incluem suporte para cadeias de ligação de SAS.

## <a name="next-steps"></a>Passos seguintes
- Continuar a ler [autenticação de Service Bus com assinaturas de acesso partilhado](../service-bus-messaging/service-bus-sas.md) para obter mais detalhes sobre SAS.
- Consulte Olá [guia de protocolo do Azure reencaminhamento híbrido ligações](relay-hybrid-connections-protocol.md) para obter informações detalhadas sobre Olá capacidade de ligações híbridas.
- Para obter informações correspondentes sobre mensagens do Service Bus autenticação e autorização, consulte [barramento de serviço de autenticação e autorização](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png