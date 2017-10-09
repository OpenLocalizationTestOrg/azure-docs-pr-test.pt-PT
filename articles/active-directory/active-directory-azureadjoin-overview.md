---
title: "dispositivos tooWindows 10 de capacidades de nuvem do aaaExtending através da associação do Azure Active Directory | Microsoft Docs"
description: "Fornece uma descrição detalhada do como dispositivos Windows 10 pode utilizar a associação do Azure AD tooget registado no Azure Active Directory."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Expandir nuvem dispositivos de tooWindows 10 capacidades através da associação do Azure Active Directory
## <a name="what-is-azure-active-directory-join"></a>O que é o Azure Active Directory Join?
Azure associação do Active Directory (associação do Azure AD) é a funcionalidade de Olá que regista um dispositivo propriedade da empresa no Azure Active Directory tooenable centralizada gestão de dispositivos de Olá. Este torna possível para utilizadores, tais como os funcionários e alunos tooconnect toohello enterprise cloud através do Azure Active Directory. Isto permite simplificada implementações do Windows e acesso tooorganizational aplicações e recursos a partir de qualquer dispositivo de Windows, tanto pertencentes à empresa e pessoais (BYOD).

A associação do Azure AD destina-se de que as empresas que estão apenas na nuvem primeiro/nuvem-– normalmente dimensionados de pequenas e médias empresas que não tenham uma infraestrutura do Windows Server Active Directory no local. Que referida, Azure AD a associação pode e também irá ser utilizada por organizações grandes em dispositivos que estão sem capacidade de fazer uma associação de domínio tradicional (dispositivos móveis, por exemplo), ou para utilizadores que necessitam de principalmente tooaccess do Office 365 ou outras aplicações de SaaS integradas com o Azure AD.

Apesar de associação a um domínio tradicional Olá ainda oferece Olá melhor no local de experiência em dispositivos que são capazes de associação de domínio, a associação do Azure AD é adequada para os dispositivos que não é possível a associação a um domínio. A associação do Azure AD também é adequada para a gestão de utilizadores na nuvem de Olá. Isto é feito utilizando as capacidades de gestão de dispositivos móveis em vez de utilizando as ferramentas de gestão do domínio tradicionais, como a política de grupo e o System Center Configuration Manager (SCCM).

![Descrição geral dos dispositivos empresariais e dispositivos pessoais com o Active Directory no local e o Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Por que motivo devem que as empresas adotar a associação do Azure AD?
* **Olá, as empresas que estão em grande parte nos nuvem**: se movido ou se estiver a mover tooa modelo no qual estão a reduzir os requisitos de espaço no local e pretende toooperate mais na nuvem de Olá, associação do Azure AD foi beneficiar. Pode ser criada com contas do Azure AD manualmente ou através de sincronizar o Active Directory no local. Qualquer forma, tem de ter uma conta no Azure AD e pode utilizá-lo toosign em tooWindows 10. Os utilizadores podem associar os seus tooAzure computadores AD através de uma experiência de out-of-box Olá (OOBE) ou através do menu de definições de Olá. Após a associação, os utilizadores serão desfrutar único início de sessão (SSO) acesso toocloud recursos como o Office 365, nos seus browsers ou nas aplicações do Office.
* **Instituições Educational**: um dos cenários de Olá recebemos sobre, muitas vezes, é que instituições educational têm dois tipos de utilizador: corpo docente e alunos. Os membros do corpo docente são considerados duração mais longa membros da organização Olá, pelo que a criação de contas no local para os mesmos é desejável. Mas estudantes são shorter-term membros da organização Olá e, por conseguinte, podem ser geridos no Azure AD. Isto significa que a escala de diretório pode ser enviada toohello nuvem em vez de armazenada no local. Também significa que os estudantes que estejam podem iniciar sessão tooWindows com as respetivas contas do Azure AD e obter acesso tooOffice 365 recursos nos seus browsers ou nas aplicações do Office.
* **Revenda empresas**: outro cenário que já conhecemos de clientes é os funcionários de sazonais toomanage desire mais facilmente.  Novamente, as contas para os funcionários a tempo inteiro, duração mais longa são normalmente criadas no local contas em computadores associados a um domínio. Mas trabalhadores sazonais são membros shorter-term org Olá, pelo que é preferível toomanage-los onde licenças de utilizador podem ser mais facilmente movidas à volta. Criar estas contas de utilizador na nuvem de Olá com licenças do Office 365 permite que os benefícios do Olá utilizadores tooget Olá do início de sessão tooWindows e aplicações do Office com uma conta do Azure AD. Entretanto, manter uma maior flexibilidade com as respetivas licenças depois de serem saírem.
* **Outras empresas**:, apesar de manter os utilizadores no Active Directory no local, ainda pode beneficiar de ter os utilizadores sejam associados-Azure AD. Isto acontece porque o Azure AD oferece uma experiência simplificada associar, gestão de dispositivos eficiente, inscrição da gestão de dispositivos móveis automática e capacidade de início de sessão único para o Azure AD e recursos no local.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Associação do Azure AD oferecem que capacidades?
Com a associação do Azure AD, obter seguinte Olá:

* **Aprovisionamento automático de dispositivos pertencentes à empresa**: com o Windows 10, os utilizadores podem configurar um dispositivo novo, shrink-wrapped na experiência de out-of-box Olá, sem o envolvimento de IT.
* **Suporte para fatores de forma moderna**: associação do Azure AD funciona nos dispositivos que não tenham o domínio tradicional Olá associar capacidades.  
* **Suporte para as contas organizacionais existentes**: os utilizadores já não precisar toocreate e manter um um tooget de conta Microsoft pessoal Olá melhor experiência em dispositivos emitidos pela empresa, como o fizeram com o Windows 8. Em vez disso, podem utilizar as respetivas contas de trabalho existentes no Azure AD. Para muitas organizações, basicamente significa que os utilizadores podem configurar e iniciar sessão tooWindows com Olá mesmas credenciais que utilizam tooaccess do Office 365.
* **Inscrição de gestão de dispositivos móveis automática**: dispositivos podem ser automaticamente inscritos na gestão de dispositivos móveis quando ligado tooAzure AD. Este processo funciona com soluções de gestão de dispositivos móveis do Microsoft Intune e o parceiro. Quando a gestão de dispositivos é efetuada com o Intune, os administradores de TI podem monitorizar/gerir dispositivos associados a um AD do Azure em conjunto com dispositivos associados a um domínio na consola de gestão do SCCM Olá.
* **Único recursos de início de sessão toocompany**: os utilizadores desfrutar início de sessão único de tooapps ambiente de trabalho do Windows hello e de recursos na nuvem de Olá, tais como o Office 365 e milhares de aplicações de empresas que dependem do Azure AD para autenticação através de [Do azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Dispositivos pertencentes à empresa que estão associados a um tooAzure AD também Desfrute mais recursos do SSO tooon local quando o dispositivo de Olá estiver numa rede empresarial e, em qualquer lugar, quando estes recursos estão expostos através de Olá [Proxy de aplicações do Azure AD](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **Roaming de estado de SO**: definições de acessibilidade, Web sites, palavras-passe de Wi-Fi e outras definições são sincronizadas em todos os dispositivos pertencentes à empresa sem necessidade de uma conta Microsoft pessoal.
* **Loja Windows de preparada para empresa**: Olá loja Windows suporta a aquisição de aplicação e licenciamento com contas do Azure AD. As organizações podem aplicações de licença de volume e torná-los toohello disponíveis utilizadores na sua organização.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Como funcionam com a associação do Azure AD diferentes dispositivos?
| Dispositivos de empresa (domínio local tooon associado) | Dispositivos de empresa (toohello associados nuvem) | Dispositivo pessoal |
| --- | --- | --- |
| Os utilizadores podem iniciar sessão no Windows com credenciais de trabalho (tal como estes hoje em dia). |Os utilizadores podem iniciar sessão tooWindows com credenciais de trabalho que são geridas no Azure AD. Este aspeto é relevante para dispositivos da empresa em três casos: <ol><li>organização de Olá não tiver o Active Directory no local (por exemplo, uma pequena empresa).</li><li>organização Olá não cria todas as contas de utilizador no Active Directory (por exemplo, as contas para estudantes, consultores ou trabalhadores sazonais não são criadas no Active Directory).</li><li>organização de Olá tiver dispositivos empresariais que não podem ser o domínio associado ao tooan (no local), como telemóveis ou tablets com um SKU de móvel (por exemplo, um dispositivo secundário tomado tooa fábrica/revenda piso).</li></ol> A associação do Azure AD suporta a associação de dispositivos da empresa para organizações federadas e não geridos. |Os utilizadores iniciarem sessão tooWindows com as credenciais da conta Microsoft pessoais (não alterar). |
| Os utilizadores têm acesso tooroaming definições e enterprise Olá loja Windows. Estes serviços funcionam com contas de trabalho e não necessitam de uma conta Microsoft pessoal. Isto requer as organizações tooconnect os respetivos tooAzure do Active Directory no local AD. |Os utilizadores podem efetuar a configuração do self-service. Podem aceder através de experiência de primeira execução Olá (FRX) através da respetiva conta profissional como uma alternativa toohaving IT Olá de aprovisionar dispositivos, embora ambos os métodos são suportados. |Os utilizadores podem facilmente adicionar uma conta profissional, que é gerida no Active Directory ou do Azure AD. |
| Os utilizadores têm capacidade SSO de aplicações de ambiente de trabalho toowork Olá, Web sites e de recursos – incluindo recursos no local e aplicações em nuvem que utilizam o Azure AD para autenticação. |Os dispositivos são registados automaticamente no diretório de enterprise Olá (Azure AD) e automaticamente inscritos na gestão de dispositivos móveis. (Funcionalidade do azure AD Premium). |Os utilizadores têm capacidade SSO em aplicações e toowebsites/recursos, com esta conta profissional. |
| Os utilizadores podem adicionar as respetivas contas tooaccess pessoal do Microsoft os seus ficheiros e imagens pessoais sem afetar os dados empresariais. (As definições de roaming continuam toowork com a conta profissional.) Olá conta Microsoft permite SSO e já não unidades Olá roaming das definições. |Os utilizadores podem efetuar uma reposição de palavra-passe self-service (SSPR) no winlogon, o que significa que poderem repor uma palavra-passe esquecida. (Funcionalidade do azure AD Premium). |Os utilizadores têm acesso toohello enterprise Windows Store para que estes possam adquirir e utilizar aplicações de linha de negócio nos respetivos dispositivos pessoais. |

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para empresa Olá: dispositivos de toouse formas de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Expandir nuvem dispositivos de tooWindows 10 capacidades através da associação do Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Autenticar identidades sem palavras-passe através do Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre os cenários de utilização da Associação do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Associação do Azure AD](active-directory-azureadjoin-setup.md)

