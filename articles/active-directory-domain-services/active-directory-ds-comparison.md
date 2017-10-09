---
title: "Serviços de domínio do Azure AD: Controladores de domínio serviços de domínio do AD de Azure comparar tooDIY | Microsoft Docs"
description: "Comparar os controladores de domínio do Azure Active Directory Domain Services tooDIY"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Como é adequada para o caso de utilização toodecide se os serviços de domínio do Azure AD
Com os serviços de domínio do Azure AD pode implementar as cargas de trabalho nos serviços de infraestrutura do Azure, sem ter tooworry sobre a manutenção da infraestrutura de identidade no Azure. Este serviço gerido é diferente de uma implementação típica do Windows Server Active Directory que implementar e administrar por si. serviço de Olá é fácil toodeploy e oferece monitorização de estado de funcionamento automático e remediação. Estamos constantemente são evolução Olá serviço tooadd o suporte para cenários comuns de implementação.

toodecide se os serviços de domínio do Azure AD toouse Recomendamos Olá material de ler os seguintes:

* Ver lista de Olá de [funcionalidades oferecidas pelos serviços de domínio do Azure AD](active-directory-ds-features.md).
* Reveja comuns [cenários de implementação de serviços de domínio do Azure AD](active-directory-ds-scenarios.md).
* Por fim, [comparar a opção de tooa do-it-yourself AD de serviços de domínio do Azure AD](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Comparar o domínio de tooDIY AD de serviços de domínio do Azure AD no Azure
Olá seguinte tabela ajuda-o a decidir entre utilizando os serviços de domínio do Azure AD e gerir a sua própria infraestrutura de AD no Azure.

| **Funcionalidade** | **Serviços de domínio do Azure AD** | **'Do-it-yourself' AD em VMs do Azure** |
| --- |:---:|:---:|
| [**Serviço gerido**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**& #x 2715;** |
| [**Implementações seguras**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |Administrador tem de implementação de Olá toosecure. |
| [**Servidor DNS**](active-directory-ds-comparison.md#dns-server) |**& #x 2713;**  (serviço gerido) |**&#x2713;** |
| [**Privilégios de administrador de domínio ou Enterprise**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**& #x 2715;** |**&#x2713;** |
| [**Associação a um domínio**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**Autenticação de domínio utilizando NTLM e Kerberos**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Delegação restringida de Kerberos**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|baseada em recursos|baseada em recursos & com base em conta|
| [**Estrutura de UO personalizada**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**Extensões de esquema**](active-directory-ds-comparison.md#schema-extensions) |**& #x 2715;** |**&#x2713;** |
| [**Confianças de floresta e domínio AD**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**& #x 2715;** |**&#x2713;** |
| [**LDAP de leitura**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**LDAP seguro (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**Escrita LDAP**](active-directory-ds-comparison.md#ldap-write) |**& #x 2715;** |**&#x2713;** |
| [**Política de grupo**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**Geo-distribuição implementações**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**& #x 2715;** |**&#x2713;** |

#### <a name="managed-service"></a>Serviço gerido
Domínios de serviços de domínio do AD do Azure são geridos pela Microsoft. Não dispõe de tooworry sobre a aplicação de patches, atualizações, monitorização, cópias de segurança e garantir a disponibilidade do seu domínio. Estas tarefas de gestão são disponibilizadas como um serviço pelo Microsoft Azure para os domínios geridos.

#### <a name="secure-deployments"></a>Implementações seguras
domínio Olá de gerido em segurança bloqueado de acordo com as recomendações de segurança da Microsoft para implementações do AD. Estas recomendações stem de decades da equipa de produto Olá AD de experiência de engenharia e implementações de AD de suporte. Para implementações do-it-yourself, terá de implementação específico tootake passos toolock baixo/proteger a implementação.

#### <a name="dns-server"></a>Servidor DNS
Um domínio gerido dos serviços de domínio do Azure AD inclui serviços DNS geridos. Membros Olá ' AAD DC' do grupo de administradores podem gerir o DNS no domínio Olá gerido. Os membros deste grupo recebem privilégios completos de administração de DNS para o domínio Olá de gerido. Gestão de DNS pode ser efetuada utilizando Olá 'Consola de administração de DNS' incluída no pacote de ferramentas de administração remota de servidor (FARS) Olá.
[Obter mais informações](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Privilégios de administrador de empresa ou de domínio
Estes privilégios elevados não são disponibilizados num domínio gerido AAD DS. As aplicações que necessitam destas privilégios elevados não não possível implementar contra AAD DS Domínios geridos. Um subconjunto mais pequeno de privilégios administrativos é toomembers disponível do grupo de administração delegada Olá chamado 'AAD DC administradores'. Esses privilégios incluem privilégios tooconfigure DNS, configurar a política de grupo, obterem privilégios de administrador em computadores associados a um domínio etc.

#### <a name="domain-join"></a>Associação a um domínio
Pode associar máquinas virtuais toohello geridos toohow semelhante domínio associar o domínio de tooan AD de computadores.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Autenticação de domínio utilizando NTLM e Kerberos
Com os serviços de domínio do Azure AD, pode utilizar o seu tooauthenticate de credenciais da empresa com o domínio Olá de gerido. As credenciais são mantidas em sincronização com o seu inquilino do Azure AD. Para inquilinos sincronizados, o Azure AD Connect assegura que as alterações toocredentials efetuadas no local é sincronizado tooAzure AD. Com uma configuração de domínio do-it-yourself, poderá ser necessário tooset cópias de segurança num domínio AD fidedignidade com o ambiente AD para utilizadores tooauthenticate com as respetivas credenciais empresariais. Em alternativa, poderá ser necessário tooset segurança tooensure de replicação do AD que as palavras-passe do utilizador sincronizar as máquinas virtuais do controlador de domínio do Azure do tooyour.

#### <a name="kerberos-constrained-delegation"></a>Delegação restringida de Kerberos
Não dispõe de privilégios de administrador de domínio num domínio gerido dos serviços de domínio do Active Directory. Por conseguinte, não é possível configurar a delegação restringida de Kerberos (tradicional) com base na conta. No entanto, pode configurar Olá mais segura delegação restrita baseada em recursos.
[Obter mais informações](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Estrutura de UO personalizada
Os membros Olá ' AAD DC' do grupo de administradores podem criar UOs personalizados dentro do domínio Olá gerido. Os utilizadores que criar UOs personalizados são concedidos privilégios administrativos completos sobre Olá UO.
[Obter mais informações](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Extensões de esquema
Não é possível expandir o esquema de base de Olá de um domínio gerido dos serviços de domínio do Azure AD. Por conseguinte, as aplicações que dependem do esquema de tooAD extensões (por exemplo, novos atributos no objeto de utilizador Olá) não podem ser lifted e desviado domínios tooAAD DS.

#### <a name="ad-domain-or-forest-trusts"></a>Domínio do AD ou fidedignidades de floresta
Domínios geridos não podem ser configurado tooset se as relações de confiança (entrada/saída) com outros domínios. Por conseguinte, os cenários de implementação de floresta de recursos não é possível utilizar os serviços de domínio do Azure AD. Da mesma forma, implementações em que preferir não toosynchronize palavras-passe tooAzure AD não é possível utilizar os serviços de domínio do Azure AD.

#### <a name="ldap-read"></a>Leitura LDAP
Olá geridos domínio suporta LDAP leitura cargas de trabalho. Por conseguinte, pode implementar aplicações que executam operações contra o domínio gerido Olá de leitura de LDAP.

#### <a name="secure-ldap"></a>LDAP seguro
Pode configurar os serviços de domínio do Azure AD tooprovide segura LDAP acesso tooyour gerido Olá de domínio, incluindo através de internet.
[Obter mais informações](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>Escrita LDAP
domínio gerido Olá é só de leitura para objetos de utilizador. Por conseguinte, as aplicações que executam operações de escrita LDAP contra os atributos de objeto de utilizador Olá não funcionam num domínio gerido. Além disso, palavras-passe do utilizador não podem ser alteradas a partir do domínio gerido Olá. Outro exemplo seria modificação de membros do grupo ou os atributos de grupo no domínio gerido Olá, que não é permitido. No entanto, quaisquer alterações toouser atributos ou as palavras-passe efetuadas no Azure AD (através do portal do PowerShell/Azure) ou no local são sincronizados AD toohello AAD DS geridos domínio.

#### <a name="group-policy"></a>Política de grupo
Não há um incorporada GPO cada para contentores de Olá "AADDC computadores" e "AADDC utilizadores". Pode personalizar estas política de grupo de tooconfigure GPOs incorporada. Os membros Olá ' AAD DC' do grupo de administradores também podem criar GPOs personalizados e ligá-las UOs tooexisting (incluindo UOs personalizados).
[Obter mais informações](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Georreplicação-dispersos implementações
Domínios geridos de serviços de domínio do AD do Azure estão disponíveis numa única rede virtual no Azure. Para cenários que requerem o domínio controladores toobe disponível em várias regiões do Azure em Olá mundo, a configurar os controladores de domínio em VMs do IaaS do Azure pode ser alternativa melhor Olá.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>Opções de implementação (DIY) AD 'Do-it-yourself'
Poderá ter casos de utilização de implementação em que precisa de algumas das capacidades de Olá oferecidas por uma instalação do Windows Server AD. Nestes casos, considere uma das Olá do-it-yourself (DIY) opções a seguir:

* **Domínio de nuvem autónomo:** que pode configurar uma autónoma 'domínio cloud' utilizar máquinas virtuais do Azure que tenham sido configuradas como controladores de domínio. Esta infraestrutura não integrar no local com o ambiente do AD. Esta opção precisaria que um conjunto diferente de 'na nuvem credenciais' toologin/administrar VMs na nuvem de Olá.
* **Implementação de floresta de recursos:** pode configurar um domínio na topologia de floresta de recursos de Olá, utilizando configurados como controladores de domínio virtual machines do Azure. Em seguida, pode configurar uma relação de fidedignidade do AD no local com o ambiente do AD. Pode floresta de associação de domínio computadores (as VMs do Azure) toothis recursos na nuvem de Olá. Autenticação de utilizador ocorre através de qualquer um diretório no local do VPN/ExpressRoute ligação tooyour.
* **Expandir a sua tooAzure de domínio no local:** pode ligar uma rede no local do tooyour de rede virtual do Azure a utilizar uma ligação VPN/ExpressRoute. Esta configuração permite que as VMs do Azure toobe tooyour associados a um AD no local. Outra alternativa é toopromote controladores de domínio de réplica do seu domínio no local no Azure como uma VM. Pode, em seguida, configurar-tooreplicate através de um diretório no local do VPN/ExpressRoute ligação tooyour. Neste modo de implementação eficaz expande o tooAzure de domínio no local.

> [!NOTE]
> Pode determinar que opção de DIY melhor é adequada para os casos de utilização de implementação. Considere [partilha comentários](active-directory-ds-contact-us.md) toohelp-na compreender o que iriam ajudar funcionalidades dos serviços de domínio do Azure AD que escolheu no Olá futura. Estes comentários ajudam-na evoluir suit de toobetter Olá serviço que tem da implementação e casos de utilização.
>
>

Iremos tiver publicado [diretrizes para implementar o Windows Server Active Directory em Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp facilitar DIY instalações.

## <a name="related-content"></a>Conteúdo relacionado
* [Funcionalidades - Serviços de domínio do Azure AD](active-directory-ds-features.md)
* [Cenários de implementação - serviços de domínio do Azure AD](active-directory-ds-scenarios.md)
* [Diretrizes para a implementação do Windows Server Active Directory em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
