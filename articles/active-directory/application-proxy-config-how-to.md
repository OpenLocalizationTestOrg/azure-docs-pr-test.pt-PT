---
title: "aaaHow tooconfigure uma aplicação de Proxy de aplicações | Microsoft Docs"
description: "Saiba como toocreate um configurar uma aplicação de Proxy de aplicações em alguns passos simples"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Como tooconfigure uma aplicação de Proxy de aplicações

Este artigo ajudá-lo toounderstand como tooconfigure uma aplicação de Proxy de aplicações dentro do Azure AD tooexpose sua toohello de aplicações no local na nuvem.

## <a name="recommended-documents"></a>Documentos recomendados 

toolearn sobre configurações inicial Olá e criação de uma aplicação de Proxy de aplicações através do Portal de administração de Olá siga Olá [publicar aplicações através do Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Para obter mais informações sobre como configurar conectores, consulte [ativar o Proxy da aplicação no portal do Azure de Olá](active-directory-application-proxy-enable.md).

Para informações sobre como carregar certificados e a utilização de domínios personalizados, consulte [trabalhar com domínios personalizados no Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Criar Olá/definição da aplicação Olá URLs

Se estiver a seguir os passos de Olá em Olá [publicar aplicações através do Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) tem e a documentação de obter um erro ao criar a aplicação Olá, consulte os detalhes do erro Olá para informações e sugestões sobre como aplicação de Olá toofix. A maioria das mensagens de erro incluem uma correção sugerida. erros comuns tooavoid, certifique-se:

-   É um administrador com permissão toocreate uma aplicação de Proxy de aplicações

-   URL interno Olá é exclusivo

-   URL externo Olá é exclusivo

-   Olá URLs início com http ou https e terminar com um "/"

-   URL de Olá deve ser um nome de domínio, não um endereço IP

mensagem de erro de saudação deve apresentar no canto superior direito Olá quando criar aplicação Olá. Também pode selecionar Olá notificação ícone toosee Olá as mensagens de erro.

   ![Pedido de notificação](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Configurar grupos de conectores/conector

Se estiver a ter dificuldade em configurar a sua aplicação devido a aviso sobre conectores Olá e grupos de conector, consulte as instruções sobre como ativar o Proxy da aplicação para obter detalhes sobre como conectores toodownload. Se pretender mais informações sobre conectores toolearn, veja Olá [documentação de conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Se os conectores estão inativos, isto significa que estão serviço de Olá tooreach não é possível. Isto é, muitas vezes, porque todas as portas de Olá necessárias não estão abertas. toosee uma lista de portas necessárias, consulte a secção de pré-requisitos de Olá de Olá ativar a documentação do Proxy de aplicações.

## <a name="upload-certificates-for-custom-domains"></a>Carregar certificados para domínios personalizados

Domínios personalizados permitem-lhe domínio de Olá toospecify do seu URLs externos. domínios personalizados toouse, precisa de tooupload Olá certificado desse domínio. Para obter informações sobre como utilizar domínios e certificados personalizados, consulte [trabalhar com domínios personalizados no Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Se tiver problemas com a carregar o certificado, procure mensagens de erro Olá no portal de Olá para obter informações adicionais sobre o problema de Olá com certificado Olá. Problemas de certificado comuns incluem:

-   Certificado expirado

-   O certificado é autoassinado

-   Certificado não tem chave privada Olá

apresentação de mensagem de erro de Olá no Olá canto superior direito, tente o certificado de Olá tooupload. Também pode selecionar Olá notificação ícone toosee Olá as mensagens de erro.

   ![Pedido de notificação](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Passos seguintes
[Publicar aplicações através do Proxy de aplicações do Azure AD](application-proxy-publish-azure-portal.md)
