---
title: "aplicações com suporte para aaaClaims - Proxy de aplicações do Azure AD | Microsoft Docs"
description: "Como toopublish no local as aplicações de ASP.NET que aceitam afirmações do ADFS para acesso remoto seguro pelos seus utilizadores."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Trabalhar com aplicações com suporte para afirmações no Proxy de aplicações
[Aplicações com suporte para afirmações](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) efetuar um toohello redirecionamento serviço de Token de segurança (STS). Olá STS os pedidos de credenciais de utilizador de Olá in exchange for um token e redireciona, em seguida, a aplicação de toohello Olá utilizador. Existem algumas formas tooenable Proxy de aplicações toowork com estes redirecionamentos. Utilize este artigo tooconfigure a implementação para aplicações com suporte para afirmações. 

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que Olá STS Olá aplicação com suporte para afirmações redireciona toois disponíveis fora da rede no local. É possível disponibilizar Olá STS pela sua exposição através de um proxy ou permitindo fora ligações. 

## <a name="publish-your-application"></a>Publicar a aplicação

1. Publicar a aplicação de acordo com as instruções de toohello descritas em [publicar aplicações com o Proxy de aplicações](application-proxy-publish-azure-portal.md).
2. Navegue até a página de aplicação toohello no Olá portal e selecione **de sessão único-**.
3. Se tiver escolhido **do Azure Active Directory** como seu **método de pré-autenticação**, selecione **do Azure AD-início de sessão único desativada** como o **método de autenticação interno**. Se tiver escolhido **Passthrough** como seu **método de pré-autenticação**, não precisa de toochange qualquer caráter.

## <a name="configure-adfs"></a>A configuração do ADFS

Pode configurar o AD FS para aplicações com suporte para afirmações de uma das duas formas. Olá pela primeira vez é através da utilização de domínios personalizados. segundo é Olá com WS-Federation. 

### <a name="option-1-custom-domains"></a>Opção 1: Domínios personalizados

Se todos os URLs internos de Olá para as aplicações são completamente qualificadas (FQDN) de nomes de domínio, em seguida, pode configurar [domínios personalizados](active-directory-application-proxy-custom-domains.md) para as suas aplicações. Utilize Olá domínios personalizados toocreate URLs externos que são Olá igual ao hello URLs internos. Quando os URLs externos corresponder ao seu URLs internos, em seguida, redirecionamentos de STS Olá funcionam se os seus utilizadores estão no local ou remoto. 

### <a name="option-2-ws-federation"></a>Opção 2: WS-Federation

1. Abra a gestão do AD FS.
2. Aceda demasiado**confianças da entidade Confiadora**, faça duplo clique na aplicação Olá com o Proxy da aplicação que está a publicar e escolha **propriedades**.  

   ![Confianças da entidade confiadora faça duplo clique no nome da aplicação – captura de ecrã](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. No Olá **pontos finais** separador em **tipo de ponto final**, selecione **WS-Federation**.
4. Em **fidedigna URL**, introduza o URL de Olá que introduziu no Olá Proxy de aplicações em **URL externo** e clique em **OK**.  

   ![Adicionar um ponto final - defina o valor do URL fidedigna - captura de ecrã](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Passos seguintes
* [Ativar o início de sessão único em](application-proxy-sso-overview.md) para aplicações que não suporte para afirmações
* [Ativar aplicações de cliente nativo toointeract com aplicações de proxy](active-directory-application-proxy-native-client.md)


