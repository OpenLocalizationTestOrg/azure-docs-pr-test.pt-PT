---
title: "considerações de design do aaaAzure do Active Directory híbrida identidade - determinar os requisitos de identidade | Microsoft Docs"
description: "Identifica necessidades de negócio da empresa Olá que direciona os requisitos de Olá toodefine para o design da identidade híbrida Olá."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Determinar os requisitos de identidade para a sua solução de identidade híbrida
Olá primeiro passo para conceber uma solução de identidade híbrida é requisitos de Olá toodetermine da organização de negócio de Olá que irá tirar partido desta solução.  Identidade híbrida é iniciada como uma função de suporte (suporta todas as outras soluções de nuvem, fornecer autenticação) e entra nas capacidades de novas e interessantes tooprovide que desbloquear novas cargas de trabalho para os utilizadores.  Estas cargas de trabalho ou serviços que pretende tooadopt para os seus utilizadores vai ditar os requisitos de Olá para o design da identidade híbrida Olá.  Estes serviços e cargas de trabalho tem de identidade híbrida de tooleverage no local e na nuvem de Olá.  

Terá de toogo estes aspetos-chave de Olá negócio toounderstand o que é um requisito agora e planos de empresa que Olá para Olá futura. Se não tiver visibilidade Olá da estratégia de longo prazo Olá para o design da identidade híbrida, possibilidades são de que a solução não será dimensionável à medida que necessidades de negócio Olá mudam.   T ele diagrama abaixo mostra um exemplo de um híbrida identidade arquitetura e Olá cargas de trabalho que estão a ser desbloqueada para os utilizadores. Esta é apenas um exemplo de todas as possibilidades de nova Olá que podem ser desbloqueadas e entregue com uma estratégia de identidade híbrida sólida. 

Alguns componentes que fazem parte da arquitetura de identidade híbrida de Olá![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Determinar as necessidades de negócio
Cada empresa tem requisitos diferentes, mesmo que essas empresas façam parte de Olá mesma indústria, os requisitos comerciais reais de Olá podem variar. Ainda pode tirar partido das melhores práticas da indústria Olá, mas, em última análise é necessidades comerciais da empresa de Olá que direciona os requisitos de Olá toodefine para o design da identidade híbrida Olá. 

Certifique-se a seguinte de Olá tooanswer questões tooidentify sua empresa precisa de:

* É da sua empresa está à procura o toocut IT operacional custo?
* É da sua empresa está à procura o toosecure recursos de nuvem (aplicações SaaS, infraestrutura)?
* É a sua empresa está à procura toomodernize o departamento de TI?
  * Os seus utilizadores estão mais pedir o seu trabalho e móveis IT toocreate exceções no seu DMZ tooallow outro tipo de recursos diferentes do tráfego tooaccess?
  * A sua empresa tem aplicações legadas que necessários toobe publicado toothese moderna, mas não são toorewrite fácil?
  * Da sua empresa precisa de tooaccomplish todas estas tarefas e colocá-lo sob controlo ao hello mesmo tempo?
* É da sua empresa está à procura as identidades dos utilizadores toosecure e reduzir o risco ao colocar novas ferramentas que tiram partido conhecimentos Olá da segurança do Azure conhecimentos no local da Microsoft?
* É da sua empresa ao tentar tooget rid de Olá dreaded "externas" contas no local e movê-los na nuvem toohello onde estiverem já não é uma ameaça dormant no interior do seu ambiente no local?

## <a name="analyze-on-premises-identity-infrastructure"></a>Analisar a infraestrutura de identidade no local
Agora que tem uma ideia sobre os requisitos de negócio da empresa, terá de tooevaluate a infraestrutura de identidade no local. Esta avaliação é importante para definir Olá requisitos técnicos toointegrate o atual solução toohello cloud identity gestão sistema de identidade. Certifique-se tooanswer Olá, seguintes perguntas:

* Que solução de autenticação e autorização da sua empresa utilizar no local? 
* A sua empresa tem atualmente qualquer serviços de sincronização no local?
* A sua empresa utiliza quaisquer fornecedores de identidade (IdP) de terceiros?

Também precisa de toobe conhecimento dos serviços em nuvem Olá que poderão ter a sua empresa. Efetuar uma avaliação toounderstand Olá atual integração com o SaaS, os modelos de IaaS ou PaaS no seu ambiente é muito importante. Certifique-se de que tooanswer Olá, seguintes perguntas durante esta avaliação:

* A sua empresa tem qualquer integração com um fornecedor de serviços na nuvem?
* Se Sim, quais os serviços estão a ser utilizados?
* É esta integração atualmente na produção ou é um piloto?

> [!NOTE]
> Se não tiver um mapeamento exata de todas as suas aplicações e serviços em nuvem, pode utilizar a ferramenta de Cloud App Discovery Olá. Esta ferramenta pode fornecer o seu departamento de TI com visibilidade para empresa todos os seus da sua e aplicações em nuvem de consumidor. Que torna mais fácil de alguma vez toodiscover sombra IT na sua organização, incluindo detalhes sobre os padrões de utilização e todos os utilizadores aceder as aplicações em nuvem. Consulte tooget iniciado [o Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Avaliar requisitos de integração de identidade
Em seguida, terá de requisitos de integração de identidade de Olá tooevaluate. Esta avaliação é importante toodefine requisitos técnicos do Olá para como irão autenticar os utilizadores, como a presença de organização Olá será apresentada na nuvem de Olá, como organização Olá permitirá autorização e experiência de utilizador que Olá está curso toobe. Certifique-se tooanswer Olá, seguintes perguntas:

* Organização utilizará Federação, autenticação padrão ou ambos?
* É um requisito de Federação?  Devido ao seguinte Olá:
  * Com base em Kerberos SSO
  * A sua empresa tenha um aplicações no local (um criada interna ou 3rd) que utiliza o SAML ou semelhantes funcionalidades de Federação.
  * MFA através de Smart Cards. RSA SecurID, etc.
  * Regras de acesso de cliente que resolvem perguntas Olá abaixo:
    1. Pode bloquear todos os acesso externo tooOffice 365 com base no endereço IP hello do cliente de Olá?
    2. Pode bloquear todos os tooOffice acesso externo 365, exceto Exchange ActiveSync?
    3. Pode bloquear todos os tooOffice acesso externo 365, exceto aplicações baseadas no browser (OWA, SPO)
    4. Pode bloquear todos os acesso externo tooOffice 365 para membros de grupos do AD designados
* Auditoria de segurança/preocupações
* Já investimento em autenticação federada
* O nome o nosso organização utiliza para o nosso domínio na nuvem de Olá?
* A organização Olá tem um domínio personalizado?
  1. É o domínio público e facilmente verificável através de DNS?
  2. Se não for, em seguida, tem um domínio público que pode ser utilizado tooregister um UPN alternativo no AD?
* São identificadores de utilizador Olá consistentes para representação da nuvem? 
* A organização Olá tem aplicações requerem integração com serviços em nuvem?
* A organização Olá tem vários domínios e utilizarão todos eles autenticação federada ou padrão?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Avaliar as aplicações que são executadas no seu ambiente
Agora que tem uma ideia sobre no local e a infraestrutura de nuvem, terá de aplicações de Olá tooevaluate com estes ambientes. Esta avaliação é importante toodefine Olá requisitos técnicos toointegrate sistema de gestão de identidade estas aplicações toohello na nuvem. Certifique-se tooanswer Olá, seguintes perguntas:

* Onde serão as nossas aplicações em direto?
* Os utilizadores acederão aplicações no local?  Na nuvem de Olá? Ou ambos?
* Existem planos de cargas de trabalho das aplicações existentes do tootake Olá e movê-los toohello nuvem?
* Existem planos toodevelop novas aplicações que irão residir no local ou na Olá na nuvem que irão utilizar a autenticação na nuvem?

## <a name="evaluate-user-requirements"></a>Avaliar requisitos de utilizador
Também tem os requisitos de utilizador do tooevaluate Olá. Esta avaliação é passos de Olá toodefine importantes que serão necessária para Dependency e os utilizadores a prestar assistência como estes transição toohello nuvem. Certifique-se tooanswer Olá, seguintes perguntas:

* Os utilizadores acederão aplicações no local?
* Os utilizadores acederão aplicações na nuvem de Olá?
* Como fazer os utilizadores normalmente tootheir de início de sessão local ambiente?
* Como irão os utilizadores início de sessão toohello na nuvem?

> [!NOTE]
> Certifique-se de que tootake notas de cada resposta e compreender a lógica por detrás de Olá atrás de resposta de Olá. [Determinar os requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) abordará as opções de Olá disponíveis e os profissionais de TI/contras de cada opção.  Ao responder a estas questões, vai selecionar que opções melhor se adapta às sua empresa precisa.
> 
> 

## <a name="next-steps"></a>Passos seguintes
[Determinar os requisitos de sincronização de diretórios](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Consultar também
[Descrição geral das considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

