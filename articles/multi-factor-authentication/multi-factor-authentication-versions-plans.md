---
title: "versões do MFA aaaAzure e o consumo de planos | Microsoft Docs"
description: "Informações sobre o cliente de multi-factor Authentication Olá e métodos diferentes Olá e versões disponíveis. Detalhes sobre cada plano de consumo"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Como tooget multi-factor Authentication do Azure

Quando se trata tooprotecting as suas contas, a verificação deve ser standard na sua organização. Esta funcionalidade é especialmente importante para as contas administrativas com privilegiado tooresources de acesso. Por este motivo, a Microsoft oferece tooOffice de funcionalidades de verificação de dois passos básicos 365 e administradores do Azure. Se pretende funcionalidades de Olá tooupgrade para os seus administradores, ou expandir rest toohello de verificação de dois passos dos seus utilizadores, pode comprar o Azure multi-factor Authentication. 

Este artigo abrange explica a diferença de Olá entre versões Olá oferecidas tooadministrators e Olá versão de MFA do Azure completa e especifica que funcionalidades estão disponíveis em cada um. Se estiver pronto toodeploy Olá concluir oferta do MFA do Azure, Olá posteriores opções de implementação de bastidores secções e como o Microsoft calcula consumo.

>[!IMPORTANT]
>Este artigo destina-se toobe toohelp um guia compreender Olá diferentes formas toobuy Azure multi-factor Authentication. Para obter detalhes específicos sobre preços e faturação, sempre devem consultar toohello [multi-factor Authentication página de preços](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Versões disponíveis de multi-factor Authentication do Azure

Olá tabela seguinte descreve as diferenças de Olá entre três versões da multi-factor authentication:

| Versão | Descrição |
| --- | --- |
| Multi-Factor Authentication para Office 365 |Esta versão funciona exclusivamente com aplicações do Office 365 e é gerida a partir do portal de Olá do Office 365. Os administradores podem [proteger recursos do Office 365 com verificação de dois passos](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Esta versão faz parte de uma subscrição do Office 365. |
| Autenticação Multifator para os administradores do Azure | Os administradores globais de inquilinos do Azure podem ativar a verificação de dois passos para as contas de administrador global sem custos adicionais.|
| Multi-Factor Authentication do Azure | Versão de "completa" Olá, muitas vezes, referidos tooas, Azure multi-factor Authentication oferece conjunto richest de Olá de capacidades. Fornece opções de configuração adicionais através de Olá [portal clássico do Azure](https://manage.windowsazure.com), avançadas de relatórios e suporte para um intervalo de no local e as aplicações em nuvem. Multi-factor Authentication do Azure está incluído no Azure Active Directory Premium (planos P1 e P2) e o Enterprise Mobility + segurança (planos E3 e E5) e pode ser implementado um [na nuvem de Olá ou no local](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Comparação de funcionalidades das versões
Olá tabela seguinte fornece uma lista das funcionalidades de Olá que estão disponíveis no Olá diversas versões do Azure multi-factor Authentication.

> [!NOTE]
> Esta tabela de comparação aborda funcionalidades de Olá que fazem parte de cada versão do multi-factor Authentication. Se tiver o serviço de multi-factor Authentication do Azure completo Olá, algumas funcionalidades poderão não estar disponíveis consoante utilize ou [MFA na nuvem de Olá ou MFA no local](multi-factor-authentication-get-started.md).


| Funcionalidade | Multi-Factor Authentication para Office 365 | Autenticação Multifator para os administradores do Azure | Multi-Factor Authentication do Azure |
| --- |:---:|:---:|:---:|
| Proteger contas de administrador com a MFA |● |● (apenas para contas de Administrador Global) |● |
| Aplicação móvel como um segundo fator |● |● |● |
| Chamada telefónica como segundo fator de |● |● |● |
| SMS como um segundo fator |● |● |● |
| Palavras-passe de aplicação para clientes que não suportam MFA |● |● |● |
| Controlo de administração sobre métodos de verificação |● |● |● |
| Modo PIN | | |● |
| Alerta de fraudes | | |● |
| Relatórios do MFA | | |● |
| Omissão de Uso Individual | | |● |
| Saudações personalizadas para chamadas telefónicas | | |● |
| ID do autor da chamada personalizadas para chamadas telefónicas | | |● |
| IPs Fidedignos | | |● |
| Memorizar MFA para dispositivos fidedignos |● |● |● |
| MFA SDK | | |● (fornecedor de multi-Factor Auth requer e subscrição do Azure completo) |
| MFA para aplicações no local | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Como tooget multi-factor Authentication do Azure
Se pretender que a funcionalidade completa de Olá oferecida pelo Azure multi-factor Authentication, existem várias opções:

### <a name="option-1---mfa-licenses"></a>Opção 1 - licenças MFA

Comprar licenças de Azure multi-factor Authentication e atribuir-lhes tooyour utilizadores no Azure Active Directory. 

Se utilizar esta opção, deve criar um fornecedor de autenticação do multi-factor do Azure apenas se também precisa de verificação de dois passos tooprovide para alguns utilizadores que não têm licenças. Caso contrário, poderá ser-lhe faturado duas vezes.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Licenças de opção 2 - incluída que incluem o MFA

Comprar licenças que incluem a multi-factor Authentication do Azure, como o Azure Active Directory Premium (P1 ou P2) ou o Enterprise Mobility + segurança (E3 ou E5) e atribuir-lhes tooyour utilizadores no Azure Active Directory. 

Se utilizar esta opção, deve criar um fornecedor de autenticação do multi-factor do Azure apenas se também precisa de verificação de dois passos tooprovide para alguns utilizadores que não têm licenças. Caso contrário, poderá ser-lhe faturado duas vezes. 

### <a name="option-3---mfa-consumption-based-model"></a>Opção 3 - modelo baseada no consumo de MFA

Crie um fornecedor de autenticação do multi-factor do Azure dentro de uma subscrição do Azure. Fornecedores de MFA do Azure são recursos do Azure que são faturados contra o Enterprise Agreement, um compromisso monetário do Azure ou um cartão de crédito como todos os outros recursos do Azure. Estes fornecedores só podem ser criados em subscrições Azure completo, não se limitando subscrições do Azure que tenham um 0 $ limite de gastos. Limitado subscrições são criadas quando ativar licenças, como nas opções de 1 e 2. 

Quando utilizar um fornecedor de autenticação do multi-factor do Azure, existem dois modelos de utilização disponíveis que são faturadas através da sua subscrição do Azure:  

1. **Por utilizador** - para que as empresas que pretendem tooenable a verificação de dois passos para um número fixo de empregados que necessitem regularmente de autenticação. Faturação por utilizador é baseada no número de Olá dos utilizadores ativados para a MFA no seu inquilino do Azure AD e/ou o servidor MFA do Azure. Se os utilizadores estão ativados para o MFA em ambas do Azure AD e o servidor do MFA do Azure e a sincronização de domínio (Azure AD Connect) está ativada, em seguida, iremos contagem conjunto maior de Olá de utilizadores. Se a sincronização de domínio não está ativada, então, contagem de soma de Olá de todos os utilizadores ativados para a MFA no Azure AD e o servidor MFA do Azure. Faturação é proporcional e comunicados toohello sistema de comércio diariamente. 

  > [!NOTE]
  > Exemplo de faturação 1: tiver 5000 utilizadores ativados para a MFA hoje. Olá sistema MFA divide esse número 31 e 161.29 utilizadores relatórios para esse dia. Amanhã ativa 15 mais utilizadores para que Olá sistema MFA 161.77 utilizadores de relatórios para esse dia. Por final Olá Olá ciclo de faturação, o número total de Olá de utilizadores com faturação contra a sua subscrição do Azure adiciona segurança tooaround 5000. 
  >
  > Exemplo de faturação 2: tem uma mistura de utilizadores com licenças e os utilizadores sem, pelo que tem um toomake de fornecedor de MFA do Azure por utilizador segurança diferença Olá. Existem 4,500 Enterprise Mobility + licenças de segurança no seu inquilino, mas 5000 utilizadores ativados para a MFA. A subscrição do Azure é faturada por 500 utilizadores, proporcional e reportada 16.13 utilizadores diariamente. 

2. **Por autenticação** - para que as empresas que pretendem tooenable a verificação de um grupo grande de utilizadores que raramente necessitam de autenticação. Faturação é com base no número de Olá de pedidos de verificação de dois passos recebidos pelo Olá serviço de nuvem do MFA do Azure, independentemente se esses verificações êxito ou são negadas. Este é apresentado na sua declaração de utilização do Azure em pacotes de 10 autenticações e faturação é comunicado toohello comércio sistema diariamente. 

  > [!NOTE]
  > Exemplo de faturação 3: hoje em dia, Olá serviço MFA do Azure recebido 3,105 pedidos de verificação de dois passos. A subscrição do Azure é faturada 310.5 pacotes de autenticação. 

É importante toonote pode tem licenças de MFA do Azure, mas ainda obter cobrados com base no consumo de configuração. Se configurar um fornecedor de MFA do Azure por autenticação, é-lhe faturado para cada pedido de verificação de dois passos, incluindo os feito por utilizadores que possuem licenças. Se configurar um fornecedor de MFA do Azure por utilizador no domínio que não está ligado tooyour inquilino do Azure AD, é-lhe faturado por utilizador ativado, mesmo se os utilizadores têm de licenças no Azure AD. 

## <a name="next-steps"></a>Passos seguintes

- Para obter mais detalhes de preços, consulte [preços do Azure MFA](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Escolha se toodeploy MFA do Azure [na nuvem de Olá ou no local](multi-factor-authentication-get-started.md)
