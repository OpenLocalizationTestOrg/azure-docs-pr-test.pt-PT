---
title: "Azure Active Directory B2C: Token, sessão e a configuração de início de sessão único | Microsoft Docs"
description: "Token, a sessão e a configuração do início de sessão único no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: Token, sessão e a configuração de início de sessão único
Esta funcionalidade fornece um controlo detalhado, num [base por política](active-directory-b2c-reference-policies.md), de:

1. Durações de tokens de segurança emitidos pelo Azure Active Directory (Azure AD) B2C.
2. Durações de sessões de aplicação web geridas pelo Azure AD B2C.
3. Formatos de afirmações importantes em tokens de segurança de Olá emitidos pelo Azure AD B2C.
4. Comportamento início de sessão único (SSO) em várias aplicações e políticas no seu inquilino do B2C.

Pode utilizar esta funcionalidade no seu inquilino do B2C da seguinte forma:

1. Siga estes passos demasiado[navegue painel de funcionalidades de toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no Olá portal do Azure.
2. Clique em **políticas de início de sessão**. *Nota: Pode utilizar esta funcionalidade em qualquer tipo de política, não apenas no **políticas de início de sessão***.
3. Abra uma política clicando nela. Por exemplo, clique em **B2C_1_SiIn**.
4. Clique em **editar** , Olá parte superior do painel de Olá.
5. Clique em **Token, a sessão e a configuração de início de sessão único**.
6. Efetue as alterações pretendidas. Saiba mais sobre as propriedades disponíveis nas secções subsequentes.
7. Clique em **OK**.
8. Clique em **guardar** no Olá parte superior do painel de Olá.

## <a name="token-lifetimes-configuration"></a>Configuração de durações de token
Azure AD B2C suporta Olá [protocolo de autorização do OAuth 2.0](active-directory-b2c-reference-protocols.md) para ativar a proteger o acesso a recursos de tooprotected. tooimplement este suporte, Azure AD B2C emite várias [tokens de segurança](active-directory-b2c-reference-tokens.md). Estes são propriedades Olá, que pode utilizar toomanage durações de tokens de segurança emitidos pelo Azure AD B2C:

* **Durações (minutos) de token de acesso & ID**: recurso protegido ao duração Olá tooa de acesso de toogain utilizados token de portador Olá OAuth 2.0. B2C do Azure AD emite apenas tokens de ID neste momento. Este valor seria aplicada tooaccess tokens bem, iremos adicionar suporte para os mesmos.
  * Predefinição = 60 minutos.
  * Mínimo (inclusive) = 5 minutos.
  * Máximo (inclusive) = 1440 minutos.
* **Atualize a duração do token (dias)**: Olá período de tempo máximo antes do qual um token de atualização pode ser utilizado tooacquire um token de ID de acesso novo ou (e, opcionalmente, um novo token de atualização, se a aplicação tivesse sido concedida Olá `offline_access` âmbito).
  * Predefinição = 14 dias.
  * Mínimo (inclusive) = 1 dia.
  * Máximo (inclusive) = 90 dias.
* **Atualizar o token duração de janela deslizante (dias)**: depois deste utilizador de Olá de período decorrer do tempo toore forçada-autenticar, independentemente do período de validade de Olá do token atualização mais recente Olá adquirido pela aplicação Olá. Só pode ser fornecido se comutador Olá estiver definido demasiado**Bounded**. Necessita de toobe maior que ou igual toohello **duração do token de atualização (dias)** valor. Se o comutador de Olá estiver definido demasiado**Unbounded**, não é possível fornecer um valor específico.
  * Predefinição = 90 dias.
  * Mínimo (inclusive) = 1 dia.
  * Máximo (inclusive) = 365 dias.

Estes são alguns casos de utilização que pode ativar a utilizar estas propriedades:

* Permitir que um toostay de utilizador que iniciou a sessão na aplicação móvel indefinidamente, desde que ele for continuamente ativa na aplicação Olá. Pode fazê-lo ao definir Olá **atualização deslizante janela duração do token (dias)** comutador demasiado**Unbounded** na sua política de início de sessão.
* Cumpre os requisitos de segurança e conformidade da indústria, definindo durações de token de acesso adequados Olá.

    > [!NOTE]
    > Estas definições não estão disponíveis para as políticas de reposição de palavra-passe.
    > 
    > 

## <a name="token-compatibility-settings"></a>Definições de compatibilidade de token
Tornamos a formatação afirmações de tooimportant alterações em tokens de segurança emitidos pelo Azure AD B2C. Isto foi feito tooimprove nosso suporte de protocolos padrão e interoperabilidade melhor com bibliotecas de identidade de terceiros. No entanto, tooavoid quebra as aplicações existentes, criámos Olá seguintes propriedades tooallow clientes tooopt-em conforme necessário:

* **O emissor (iss) afirmação**: esta identifica inquilino Olá, Azure AD B2C que emitiu o token de Olá.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Este é o valor predefinido de Olá.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Este valor inclui os IDs para o inquilino Olá B2C e política de Olá utilizada no pedido de token de Olá. Se a aplicação ou biblioteca necessita do Azure AD B2C toobe em conformidade com Olá [OpenID Connect 1.0 deteção spec](http://openid.net/specs/openid-connect-discovery-1_0.html), utilize este valor.
* **O requerente (sub) afirmação**: identifica esta entidade hello, ou seja, de utilizador de Olá, para que Olá token asserções informações.
  * **ObjectID**: Este é o valor predefinido de Olá. Preenche Olá o ID de objeto de utilizador de Olá no diretório de Olá para Olá `sub` de afirmações num token de Olá.
  * **Não suportado**: Isto é fornecido apenas para compatibilidade com versões anteriores e recomendamos que comutador demasiado**ObjectID** assim conseguir.
* **Que representa o ID de política de afirmações**: esta identifica o tipo de afirmação de Olá no qual Olá ID de política utilizada no pedido de token de Olá é preenchido.
  * **tfp**: Este é o valor predefinido de Olá.
  * **Acr**: Isto é fornecido apenas para compatibilidade com versões anteriores e recomendamos que comutador demasiado`tfp` assim conseguir.

## <a name="session-behavior"></a>Comportamento de sessão
Azure AD B2C suporta Olá [protocolo de autenticação OpenID Connect](active-directory-b2c-reference-oidc.md) para ativar aplicações de tooweb de início de sessão segura. Estes são propriedades Olá, que pode utilizar sessões de aplicação web de toomanage:

* **Aplicação Web duração de sessão (minutos)**: duração Olá de cookie de sessão do Azure AD B2C armazenado no browser do utilizador Olá após a autenticação com êxito.
  * Predefinição = 1440 minutos.
  * Mínimo (inclusive) = 15 minutos.
  * Máximo (inclusive) = 1440 minutos.
* **Tempo limite de sessão de aplicação Web**: se este parâmetro estiver definido demasiado**absoluto**, Olá. o utilizador é forçado toore-autenticar após Olá período de tempo especificado pelo **aplicação Web duração de sessão (minutos)** decorrida. Se este parâmetro estiver definido demasiado**Rolling** (hello definição predefinida), utilizador de Olá permanecer com sessão iniciada, desde que o utilizador de Olá é continuamente Active Directory na sua aplicação web.

Estes são alguns casos de utilização que pode ativar a utilizar estas propriedades:

* Cumpre os requisitos de segurança e conformidade da indústria, definindo a sessão de aplicação web adequada de Olá durações.
* Força nova autenticação após um período de tempo definido durante a interação de um utilizador com uma parte de alta segurança da sua aplicação web. 

    > [!NOTE]
    > Estas definições não estão disponíveis para as políticas de reposição de palavra-passe.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Configuração início de sessão único (SSO)
Se tiver várias aplicações e políticas no seu inquilino do B2C, pode gerir interações do utilizador através da-los utilizando Olá **configuração de início de sessão único** propriedade. Pode definir Olá propriedade tooone de Olá seguintes definições:

* **Inquilino**: Esta é a predefinição de Olá. Utilizar esta definição permite que várias aplicações e políticas no seu inquilino do B2C tooshare Olá mesma sessão de utilizador. Por exemplo, depois de um utilizador inicia sessão numa aplicação, compras de Contoso, ele ou ela pode também perfeitamente inicie sessão no outro Contoso Pharmacy um, após a aceder ao mesmo.
* **Aplicação**: Isto permite que toomaintain uma sessão de utilizador exclusivamente para uma aplicação, independente de outras aplicações. Por exemplo, se pretender que o utilizador de Olá toosign no tooContoso Pharmacy (com Olá mesmas credenciais), mesmo que ele ou já esteja assinada para compras de Contoso, outra aplicação nos Olá mesmo inquilino do B2C. 
* **Política**: Isto permite que toomaintain uma sessão de utilizador exclusivamente para uma política, independentemente das aplicações de Olá utilizá-la. Por exemplo, se já tem sessão iniciada e foi concluído um passo de authentication (MFA) do fator de várias utilizador Olá, ele ou ela pode ser especificada acesso toohigher segurança partes de várias aplicações, desde que não expire Olá sessão associada toohello política.
* **Desativado**: Isto força o Olá utilizador toorun através de journey de utilizador completo Olá cada a execução da política de Olá. Por exemplo, isto permitirá vários utilizadores toosign segurança tooyour aplicação (num partilhado ambiente de trabalho cenário), mesmo enquanto um único utilizador permanece com sessão iniciada durante o tempo de todo Olá.

    > [!NOTE]
    > Estas definições não estão disponíveis para as políticas de reposição de palavra-passe.
    > 
    > 

