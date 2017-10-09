---
title: "aaaAuthenticating identidades sem palavras-passe através do Windows Hello para empresas e o Azure AD | Microsoft Docs"
description: "Fornece uma descrição geral do Windows Hello para empresas e informações adicionais sobre como implementar o Windows Hello para empresas."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Autenticar identidades sem palavras-passe através do Windows Hello para empresas
os métodos de atual Olá de autenticação com palavras-passe por si só não são suficientes utilizadores tookeep seguros. Os utilizadores reutilizarem e se esqueça de palavras-passe. As palavras-passe são breachable, phishable, propensas ao toocracks e guessable. Também recebem tooremember difícil e tooattacks suscetíveis como "[passagem Olá hash](https://technet.microsoft.com/dn785092.aspx)".

## <a name="about-windows-hello-for-business"></a>Sobre o Windows Hello para empresas
Windows Hello para empresas é uma chave pública/privada ou uma abordagem de autenticação baseada em certificado para as organizações e os consumidores que vai mais além palavras-passe. Esta forma de autenticação baseia-se nas credenciais de par de chaves que podem substituir as palavras-passe e são resistentes toobreaches, thefts e phishing.

 Windows Hello para empresas permite que um utilizador autenticar tooa conta Microsoft, uma conta do Windows Server Active Directory, uma conta do Microsoft Azure Active Directory (Azure AD) ou um serviço de terceiros que suporta a autenticação rápido identidade Online (FIDO). Depois de uma verificação de dois passos iniciais durante o Windows Hello para inscrição de negócio, Windows Hello para empresas está configurada no dispositivo do utilizador Olá, e utilizador Olá define um gesto, que pode ser o Windows Hello ou um PIN. utilizador Olá fornece Olá gesto tooverify a sua identidade. Windows, em seguida, utiliza o Windows Hello para utilizador do negócio tooauthenticate Olá e ajudá-los tooaccess protegidos recursos e serviços.

chave privada Olá é disponibilizada apenas através de um "gesto de utilizador" como um PIN, biometria ou um dispositivo remoto como um smart card que Olá utilizador utiliza toosign toohello o dispositivo. Esta informação é ligado tooa certificado ou um par de chaves assimétrico. chave privada Olá é hardware atestado se o dispositivo de Olá tem um chip Trusted Platform Module (TPM). chave privada Olá nunca sai dispositivo Olá.

chave pública Olá está registado no Azure Active Directory e o Windows Server Active Directory (para no local). Fornecedores de identidade (IDPs) validar o utilizador Olá pelo mapeamento Olá chave pública da chave privada do Olá utilizador toohello e fornecem informações de início de sessão através de um tempo de palavra-passe (OTP), PhoneFactor ou um mecanismo de notificação diferentes.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Por que razão as empresas devem adotar o Windows Hello para empresas
Ao ativar a Windows Hello para empresas, o empresas podem efetuar os seus recursos ainda mais seguros por:

* Configurar o Windows Hello para empresas com uma opção preferencial de hardware. Isto significa que as chaves serão geradas no TPM 1.2 ou 2.0 quando disponível. Quando o TPM não estiver disponível, o software irá gerar chave Olá.
* Definição de Olá de complexidade e o comprimento de Olá PIN e, se a utilização de Olá está ativada na sua organização.
* Configurar o Windows Hello para cenários de smart card como toosupport empresariais através da utilização de confiança baseada em certificado.

## <a name="how-windows-hello-for-business-works"></a>Como Windows Hello para empresas funciona
1. As chaves são geradas no hardware de Olá por TPM ou software. Muitos dispositivos têm um chip TPM incorporado que protege o hardware de Olá por integrar as chaves criptográficas em dispositivos. TPM 1.2 ou 2.0 gera chaves nem certificados que são criados a partir das chaves de Olá gerado.
2. Olá TPM attests estas chaves de hardware vinculados.
3. Um gesto de desbloqueio único desbloqueia dispositivo Olá. Este gesto permite aceder a recursos toomultiple se o dispositivo de Olá não estiver associado a um domínio ou do Azure associado ao AD.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Como funciona o Olá Windows Hello para empresas ciclo de vida
![Windows Hello para empresas ciclo de vida](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Olá anterior diagrama ilustra o par de chaves do Olá público/privado e validação de Olá pelo fornecedor de identidade Olá. Cada um destes passos é explicada detalhadamente aqui:

1. Olá utilizador prove a sua identidade através de vários métodos de proofing incorporados (gestos, smart cards físicos, autenticação multifator) e envia esta tooan informações fornecedor de identidade (IDP), como o Azure Active Directory ou no local do Active Directory.
2. em seguida, o dispositivo de Olá cria chave Olá, attests chave Olá, demora Olá pública parte desta chave, anexa-lo com as instruções de estação, inicia sessão e envia-a chave de Olá toohello IDP tooregister.
3. Assim que Olá IDP regista Olá pública parte chave Olá, desafios de IDP Olá Olá toosign de dispositivo com parte da chave de Olá privada Olá.
4. Olá IDP, em seguida, valida e problemas Olá token de autenticação que permite ao utilizador Olá Olá acesso Olá protegido com recursos de dispositivos. IDPs pode escrever as aplicações da plataforma ou utilize toocreate de suporte (através de APIs de JavaScript/Webcrypto) do browser e utilizar o Windows Hello para empresas as credenciais para os seus utilizadores.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Olá, requisitos de implementação do Windows Hello para empresas
### <a name="at-hello-enterprise-level"></a>Nível de Olá enterprise
* enterprise Olá tem uma subscrição do Azure.

### <a name="at-hello-user-level"></a>Nível de utilizador de Olá
* computador do utilizador Olá executa o Windows 10 Professional ou Enterprise.

Para obter instruções de implementação detalhados, consulte [ativar o Windows Hello para empresas na organização de Olá](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para empresa Olá: dispositivos de toouse formas de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Expandir nuvem dispositivos de tooWindows 10 capacidades através da associação do Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Saiba mais sobre os cenários de utilização da Associação do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Associação do Azure AD](active-directory-azureadjoin-setup.md)

