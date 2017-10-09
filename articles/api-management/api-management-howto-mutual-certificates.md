---
title: "Serviços de back-end aaaSecure utilizando a autenticação de certificado de cliente - API Management do Azure | Microsoft Docs"
description: "Saiba como serviços de back-end toosecure utilizando o cliente de certificado de autenticação na API Management do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Como serviços de back-end toosecure utilizando o cliente de certificado de autenticação na API Management do Azure
A API Management fornece Olá capacidade toosecure toohello back-end serviço de acesso de uma API utilizando certificados de cliente. Este guia mostra como toomanage certificados no portal do publicador Olá API e como tooconfigure uma API toouse tooaccess um certificado respetivo serviço de back-end.

Para obter informações sobre como gerir certificados Olá API de REST de gestão de API a utilizar, consulte [entidade de certificado de API do REST de gestão do Azure API][Azure API Management REST API Certificate entity].

## <a name="prerequisites"></a>Pré-requisitos
Este guia mostra como tooconfigure as API Management service instância toouse cliente certificado autenticação tooaccess Olá serviço de back-end para uma API. Antes de os passos seguinte Olá neste tópico, deve ter o seu serviço de back-end configurado para autenticação de certificados de cliente ([certificado tooconfigure autenticação em sites Web do Azure consulte o artigo toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), e ter acesso toohello certificado e Olá palavra-passe para o certificado de Olá para carregar no portal do publicador da API Management Olá.

## <a name="step1"></a>Carregar um certificado de cliente
tooget iniciado, clique em **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management. Isto leva-o portal do publicador da API Management toohello.

![Portal do publicador da API][api-management-management-console]

> Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **segurança** de Olá **API Management** menu Olá esquerda e clique em **certificados de cliente**.

![Certificados de cliente][api-management-security-client-certificates]

tooupload um novo certificado, clique em **carregar certificado**.

![Carregar certificado][api-management-upload-certificate]

Procurar tooyour certificado e, em seguida, introduza a palavra-passe de Olá certificado Olá.

> tem de estar no certificado Olá **. pfx** formato. Certificados autoassinados são permitidos.
> 
> 

![Carregar certificado][api-management-upload-certificate-form]

Clique em **carregar** certificado de Olá tooupload.

> palavra-passe do Olá certificado é validado neste momento. Se estiver incorreto é apresentada uma mensagem de erro.
> 
> 

![Certificado carregado][api-management-certificate-uploaded]

Depois do certificado de Olá é carregado, é apresentado no Olá **certificados de cliente** separador. Se tiver vários certificados, tome nota do requerente Olá ou Olá últimos quatro carateres do thumbprint Olá, que são certificados de Olá tooselect utilizada quando configurar um toouse API certificados, conforme descritas na íntegra no seguinte Olá [configurar um API toouse um certificado de cliente para autenticação de gateway] [ Configure an API toouse a client certificate for gateway authentication] secção.

> tooturn desativar validação da cadeia de certificados quando utilizar, por exemplo, um certificado autoassinado, siga os passos de Olá descritos neste FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"></a>Eliminar um certificado de cliente
toodelete um certificado, clique em **eliminar** ao lado do certificado pretendido Olá.

![Eliminar o certificado][api-management-certificate-delete]

Clique em **Sim, elimine-o** tooconfirm.

![Confirmar eliminação][api-management-confirm-delete]

Se o certificado de Olá está a ser utilizado por uma API, um ecrã de aviso é apresentado. certificado de Olá toodelete tem de remover primeiro Olá de certificado a partir de qualquer APIs que estão configurado toouse-lo.

![Confirmar eliminação][api-management-confirm-delete-policy]

## <a name="step2"></a>Configurar toouse uma API um certificado de cliente para autenticação de gateway
Clique em **APIs** de Olá **API Management** Olá menu à esquerda, clique no nome de Olá da API de Olá pretendida e clique Olá **segurança** separador.

![Segurança de API][api-management-api-security]

Selecione **certificados de cliente** de Olá **com credenciais** na lista pendente.

![Certificados de cliente][api-management-mutual-certificates]

Selecione Olá certificado pretendido Olá **certificado de cliente** na lista pendente. Se existirem vários certificados pode observar o requerente Olá ou Olá últimos quatro carateres do thumbprint Olá conforme indicado no Olá anterior secção toodetermine Olá certificado correto.

![Selecione o certificado][api-management-select-certificate]

Clique em **guardar** toohello de alteração de configuração do toosave Olá API.

> Esta alteração tem efeita imediato e chamadas toooperations essa API utilizará Olá tooauthenticate de certificado no servidor de back-end Olá.
> 
> 

![Guardar as alterações de API][api-management-save-api]

> Quando é especificado um certificado para autenticação de gateway para o serviço de back-end de Olá de uma API, este torna-se parte da política de Olá para essa API e pode ser visualizado no editor de políticas de Olá.
> 
> 

![Política de certificado][api-management-certificate-policy]

## <a name="next-steps"></a>Passos seguintes
Para mais informações sobre outra formas toosecure o serviço de back-end, tal como HTTP autenticação básica ou partilhado secreta, consulte Olá seguir as vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



