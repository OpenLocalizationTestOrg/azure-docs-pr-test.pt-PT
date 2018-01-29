---
title: "Migrar do serviço de controlo de acesso do Azure Active Directory para autorização de assinatura de acesso partilhado | Microsoft Docs"
description: "Migrar aplicações de serviço de controlo de acesso a SAS"
services: service-bus-relay
documentationcenter: 
author: clemensv
manager: timlt
editor: 
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/20/2017
ms.author: sethm
ms.openlocfilehash: 7a2674ad4db9749b0a2d9342017a230797514763
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2017
---
# <a name="migrate-from-azure-active-directory-access-control-service-to-shared-access-signature-authorization"></a>Migrar do serviço de controlo de acesso do Azure Active Directory para autorização de assinatura de acesso partilhado

Aplicações de reencaminhamento do Azure historicamente tinham uma opção de utilizar dois modelos de autorização diferentes: o [assinatura de acesso partilhado (SAS)](../service-bus-messaging/service-bus-sas.md) modelo token fornecido diretamente pelo serviço de reencaminhamento e um modelo federado onde a gestão de regras de autorização é gerido dentro de, pela [do Azure Active Directory](/azure/active-directory/) serviço de controlo de acesso (ACS) e os tokens obtidos a partir de ACS são transmitidos para reencaminhamento para autorizar o acesso às funcionalidades pretendidos.

O modelo de autorização de ACS longa foi substituído pelas [autorização de SAS](../service-bus-messaging/service-bus-authentication-and-authorization.md) como o modelo preferencial e toda a documentação, exemplos e documentação de orientação exclusivamente utilizam SAS hoje. Além disso, já não é possível criar novos espaços de nomes de reencaminhamento que estão associados a ACS.

SAS tem a vantagem em que não é imediatamente depende de outro serviço, mas pode ser utilizado diretamente a partir de um cliente sem qualquer intermediários, concedendo acesso de cliente para a chave de regra e o nome da regra SAS. SAS também podem ser facilmente integrado com uma abordagem em que um cliente tem de passar pela primeira vez uma verificação de autorização com o serviço de outro e, em seguida, é emitido um token. A abordagem esta última opção é semelhante para o padrão de utilização de ACS, mas permite emissora tokens de acesso com base nas condições específicas de aplicações que são difíceis de express em ACS.

Para todas as aplicações que dependem dos ACS, recomendamos vivamente que migrar as respetivas aplicações de confiarem nos SAS em vez disso, os clientes.

## <a name="migration-scenarios"></a>Cenários de migração

ACS e reencaminhamento estão integradas através do conhecimento partilhado de um *chave de assinatura*. A chave de assinatura é utilizada por um espaço de nomes do ACS para assinar os tokens de autorização e é utilizado pelo Azure reencaminhamento para verificar que o token foi emitido por espaço de nomes de ACS emparelhado. O espaço de nomes do ACS contém identidades de serviço e as regras de autorização. Definem as regras de autorização que identidade de serviço ou o token emitido por um externo o fornecedor de identidade obtém o tipo de acesso a uma parte do espaço de nomes de reencaminhamento da graph, sob a forma de uma correspondência de prefixo mais longo.

Por exemplo, uma regra de ACS pode conceder a **enviar** de afirmação no prefixo do caminho `/` para uma identidade de serviço, o que significa que um token emitido por ACS com base nessa regra atribui o cliente direitos para enviar para todas as entidades no espaço de nomes. Se o prefixo do caminho é `/abc`, a identidade está restrita a enviar para entidades com o nome `abc` ou organizados sob esse prefixo. Presume-se que os leitores desta orientação de migração já estejam familiarizados com estes conceitos.

Os cenários de migração enquadram-se em três categorias amplas:

1.  **Não altere as predefinições**. Alguns clientes utilizam uma [SharedSecretTokenProvider](/dotnet/api/microsoft.servicebus.sharedsecrettokenprovider) objeto, passar automaticamente gerado **proprietário** identidade e a chave secreta para o espaço de nomes do ACS emparelhado com o espaço de nomes de reencaminhamento, serviço e fazer Não adicione regras de novo.

2.  **Identidades de serviço personalizado com regras simples**. Alguns clientes adicionar novas identidades de serviço e conceder cada nova identidade de serviço **enviar**, **escutar**, e **gerir** permissões para uma entidade específica.

3.  **Identidades de serviço personalizado com regras complexas**. Clientes muito poucos tem complexa regra define os tokens emitidos externamente estão mapeados para direitos no reencaminhamento ou onde é atribuída uma identidade de serviço única diferenciadas direitos sobre os vários caminhos de espaço de nomes através de várias regras.

Para obter ajuda com a migração de conjuntos de regras complexa, pode contactar [suporte do Azure](https://azure.microsoft.com/support/options/). Os outros dois cenários ative a migração simples.

### <a name="unchanged-defaults"></a>Predefinições não alteradas

Se a aplicação não tiver sido alterado as predefinições de ACS, pode substituir todas [SharedSecretTokenProvider](/dotnet/api/microsoft.servicebus.sharedsecrettokenprovider) utilização com um [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) de objeto e utilizar o espaço de nomes pré-configurada  **RootManageSharedAccessKey** em vez de ACS **proprietário** conta. Tenha em atenção que, mesmo com as ACS **proprietário** conta, esta configuração foi (e continua a ser) não, geralmente, recomendado, porque esta conta/regra fornece autoridade de gestão completo sobre o espaço de nomes, incluindo a permissão para eliminar qualquer entidades.

### <a name="simple-rules"></a>Regras simples

Se a aplicação utilizar identidades do serviço personalizado com regras simples, a migração é simples nos casos onde uma identidade de serviço ACS foi criada para fornecer controlo de acesso num reencaminhamento específico. Este cenário é muitas vezes o caso em soluções de SaaS estilo onde cada reencaminhamento é utilizado como uma ponte de um site de inquilino ou sucursal e a identidade de serviço é criada para esse site específico. Neste caso, a identidade de serviço correspondentes pode ser migrada para uma regra de assinatura de acesso partilhado, diretamente no reencaminhamento. O nome da identidade de serviço pode tornar-se o nome da regra SAS e a chave de identidade de serviço pode tornar-se a chave de regra SAS. Os direitos da regra SAS não estão configurado equivalente para ACS respetivamente aplicável regra para a entidade.

Pode fazer esta configuração de novo e adicional do SAS no local em qualquer espaço de nomes existente que está Federado com ACS e a migração dos ACS, subsequentemente, é efetuada utilizando [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) em vez de [SharedSecretTokenProvider](/dotnet/api/microsoft.servicebus.sharedsecrettokenprovider). O espaço de nomes não precisa de ser desassociado do ACS.

### <a name="complex-rules"></a>Regras complexas

Regras SAS não se destinam a ser contas, mas são denominadas associadas com direitos de chaves de assinatura. Como tal, cenários em que a aplicação cria várias identidades do serviço e lhes conceda direitos de acesso para várias entidades ou todo o espaço de nomes ainda requerem um intermediário de emissão de tokens. Pode obter orientações para essa intermediário por [contactar o suporte](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Passos Seguintes

Para saber mais sobre a autenticação de reencaminhamento do Azure, consulte os seguintes tópicos:

* [Autorização e autenticação de reencaminhamento do Azure](relay-authentication-and-authorization.md)
* [Autenticação de Service Bus com assinaturas de acesso partilhado](../service-bus-messaging/service-bus-sas.md)


