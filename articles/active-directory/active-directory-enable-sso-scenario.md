---
title: "aaaManaging aplicações com o Azure Active Directory | Microsoft Docs"
description: "Vantagens de Olá este artigo de integrar o Azure Active Directory no local, a nuvem e de aplicações SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Gestão de aplicações com o Azure Active Directory
Para além do fluxo de trabalho real Olá ou conteúdo, as empresas têm dois requisitos básicos para todas as aplicações:

1. tooincrease produtividade, as aplicações devem ser fácil toodiscover e acesso
2. segurança tooenable e governação, Olá organização necessita de controlo e supervisão em quem pode e, na verdade, está a aceder a cada aplicação

No mundo Olá das aplicações em nuvem isto melhor ser possível utilizar identidade toocontrol "*que é permitida toodo que*".

Na terminologia de computação:

* *Quem* é conhecido como *identidade* -Olá gestão de utilizadores e grupos
* *O que* é conhecido como *aceder à gestão* – Olá gestão de acesso a recursos tooprotected

Ambos os componentes em conjunto são conhecidos como *identidade e gestão de acesso (IAM)*, que é definido pela Olá [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) grupo como "*Olá disciplina de segurança que permite que o direito de Olá recursos corretos do indivíduos tooaccess Olá em Olá com o botão direito vezes por motivos de direito de Olá*".

Há problema, por isso, o que é o problema de Olá? Se for IAM *não gerido* num local com uma solução integrada:

* Os administradores de identidade têm tooindividually criar e atualizar as contas de utilizador em todas as aplicações em separado, uma atividade redundante e demorada.
* Os utilizadores têm toomemorize várias credenciais tooaccess Olá as aplicações que precisam toowork com. Como resultado, os utilizadores tendem toowrite baixo as palavras-passe ou utilizam outras soluções de gestão de palavra-passe que introduz outros riscos de segurança de dados.
* Redundante atividades demoradas reduzir a quantidade de Olá de tempo que os utilizadores e os administradores estão a funcionar em atividades de negócio que aumentam a linha de parte inferior da sua empresa.

Por isso, o que, geralmente, impede que as organizações de adotar integradas soluções IAM?

* As soluções mais técnicas baseiam-se em plataformas de software que precisam de toobe implementado e adaptada descritos por cada organização para as suas próprias aplicações.
* Aplicações em nuvem adotado uma larga maioria são, muitas vezes, uma taxa superior a organização de TI pode integrar com soluções IAM existentes.
* Ferramentas de monitorização e de segurança requerem personalização e integração tooachieve abrangentes E2E cenários adicionais.

## <a name="azure-active-directory-integrated-with-applications"></a>Azure Active Directory integrado em aplicações
Azure Active Directory é identidade da Microsoft como uma solução de serviço (IDaaS) que:

* Permite IAM como um serviço em nuvem 
* Fornece gestão de acesso central, início de sessão único (SSO) e relatórios 
* Suporta a gestão de acesso integrada para [milhares de aplicações](https://azure.microsoft.com/marketplace/active-directory/) na Galeria de aplicações de Olá, incluindo o Salesforce, Google Apps, caixa, Concur e muito mais. 

Com o Azure Active Directory, todas as aplicações publica para os parceiros e os clientes (ou empresariais consumidor) têm Olá mesmas capacidades de gestão de identidades e acessos.<br> Este permite toosignificantly reduzir os custos operacionais.

E se tem tooimplement uma aplicação que ainda não está listada na Galeria de aplicações de Olá? Apesar de ser um pouco mais morosa ao configurar o SSO para aplicações na Galeria de aplicações de Olá, Azure AD fornece um assistente que o ajuda a com a configuração de Olá.

valor de Olá do Azure AD vai mais além "apenas" as aplicações em nuvem. Também pode utilizá-lo com as aplicações no local ao fornecer o acesso remoto seguro. Com acesso remoto seguro, pode eliminar a necessidade de Olá Olá para as VPNs ou outras implementações de gestão de acesso remoto tradicional.

Ao fornecer gestão de acesso central e de início de sessão único (SSO) para todas as suas aplicações, o Azure AD fornece solução Olá toohello de problemas de produtividade e segurança de dados principal.

* Os utilizadores podem aceder a várias aplicações com um início de sessão dar mais tempo tooincome atividades de operações de negócio ou gerar causadas.
* Os administradores de identidade podem gerir o acesso tooapplications num único local.

benefício de Olá para utilizador Olá e para a sua empresa é óbvios. Vamos um olhar mais benefícios Olá para um administrador de identidades e organização Olá.

## <a name="integrated-application-benefits"></a>Vantagens de aplicação integrada
Olá processo SSO tem dois passos:

* Autenticação, o processo de Olá de validação de identidade do utilizador Olá.
* Autorização, Olá decisão tooenable ou bloquear o acesso tooa recursos com uma política de acesso.

Ao utilizar aplicações de toomanage do Azure AD e ativar SSO:

* A autenticação é efetuada no local (por exemplo, AD) ou a conta do Azure AD Olá utilizador.
* Autorização executa na Olá do Azure AD proteção e de atribuição de política de garantir que a experiência de utilizador final consistente e permitindo tooadd atribuição, localizações e condições MFA em qualquer aplicação, independentemente das respetivas capacidades de internas.

-Importante toounderstand Olá autorização Olá de forma é enacted na aplicação de destino Olá varia consoante a forma como a aplicação Olá foi integrada com o Azure AD.

* **Aplicações previamente integradas pelo fornecedor de serviço** como o Office 365 e o Azure, estes são criados diretamente no Azure AD e depender para as respetivas capacidades de gestão de identidades e acessos abrangentes de aplicações. Aceder às aplicações de toothese é ativada através da emissão de tokens e informações de diretório.
* **Aplicações previamente integradas pela Microsoft e aplicações personalizadas** são independentes da nuvem aplicações que dependem de um diretório de aplicação interna e podem funcionar independentemente do Azure AD. Aceder às aplicações de toothese é ativada através da emissão de uma aplicação credenciais específicas mapeado tooan aplicação conta. Consoante as capacidades das aplicações Olá, credencial de Olá poderá um token de Federação ou nome de utilizador e palavra-passe para uma conta que foi aprovisionada na aplicação Olá.
* **Aplicações no local** as aplicações publicadas através do proxy da aplicação Olá do Azure AD principalmente ativar aplicações de tooon local de acesso. Estas aplicações baseiam-se no diretório central no local, como o Windows Server Active Directory. Aceder às aplicações de toothese está ativado por acionar Olá proxy toodeliver Olá aplicação toohello conteúdo utilizador final para respeitar Olá local no início de sessão requisito.

Por exemplo, se um utilizador associa a sua organização, terá de toocreate uma conta de utilizador de Olá no Azure AD para Olá início de sessão operações primárias. Se este utilizador requer acesso tooa gerido aplicação, tais como o Salesforce, também tem de toocreate uma conta para este utilizador no Salesforce e ligá-lo trabalho SSO toomake do toohello conta do Azure. Quando o utilizador Olá deixa a sua organização, é aconselhável toodelete Olá conta do Azure AD e todas as contas de homólogo em Olá arquivos IAM das aplicações de Olá utilizador Olá tinha acesso.

## <a name="access-detection"></a>Deteção de acesso
Empresas moderna, departamentos de TI muitas vezes, não têm conhecimento de todas as aplicações de nuvem de Olá que estão a ser utilizadas. Em conjunto com a Cloud App Discovery, do Azure AD fornece uma solução toodetect estas aplicações.

## <a name="account-management"></a>Gestão de contas
Tradicionalmente, gestão de contas no Olá várias aplicações é um processo manual realizado IT ou suporta pessoais na organização de Olá. Do Azure AD totalmente automatizado gestão de contas em todas as aplicações de fornecedor integrado de serviço e as aplicações previamente integradas pela Microsoft que suportam o aprovisionamento automatizado do utilizador ou SAML JIT.

## <a name="automated-user-provisioning"></a>O aprovisionamento automatizado do utilizador
Algumas aplicações fornecem interfaces de automatização para criação e remoção (ou desativação) de contas. Se um fornecedor de oferecer dessa interface, é utilizado pelo Azure AD. Esta reduz os custos operacionais porque as tarefas administrativas ocorrem automaticamente e melhora a segurança de Olá do seu ambiente, porque o diminui a probabilidade de Olá de acesso não autorizado.

## <a name="access-management"></a>Gestão de acesso
Utilizar o Azure AD pode gerir o acesso tooapplications através de individuais ou a regra orientadas por atribuições. Também pode delegar o acesso gestão toohello direita pessoas Olá organização, garantindo que Olá melhor supervisão e reduzir a carga de Olá sobre o suporte técnico.

## <a name="on-premises-applications"></a>Aplicações no local
Olá incorporada do proxy de aplicações permite-lhe toopublish os utilizadores de tooyour de aplicações no local que resulta em ambos consistente aceder à experiência com vantagens de aplicação e Olá em nuvem modernas de monitorização do Azure AD, relatórios e as capacidades de segurança .

## <a name="reporting-and-monitoring"></a>Monitorização e relatórios
Azure AD fornece relatórios previamente integradas e capacidades que lhe permitem tooknow quem tem acesso tooapplications e quando, na verdade, utilizaram-los de monitorização.

## <a name="related-capabilities"></a>Funcionalidades relacionadas
Com o Azure AD pode proteger as suas aplicações com políticas de acesso granular e MFA previamente integrada. toolearn mais informações sobre o MFA do Azure, consulte [MFA do Azure](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Introdução
tooget iniciado integrar aplicações com o Azure AD, observe Olá [guia de introdução de integrar o Azure Active Directory com aplicações obter](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Consultar também
[Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)

