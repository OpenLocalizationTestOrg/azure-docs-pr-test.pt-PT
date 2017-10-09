---
title: aaaOverview do Azure Active Directory Domain Services | Microsoft Docs
description: "Descrição geral dos serviços de domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="overview"></a>Descrição geral
Serviços de infraestrutura do Azure permitem-lhe toodeploy uma vasta gama de soluções de computação de forma seja ágil. Com máquinas de virtuais do Azure, pode implementar quase instantaneamente e paga apenas por minuto Olá. Utilizar o suporte para Windows, Linux, SQL Server, Oracle, IBM, SAP e BizTalk, pode implementar qualquer carga de trabalho, qualquer idioma, em praticamente qualquer sistema operativo. Estas vantagens permitem-lhe tooAzure no toomigrate legado aplicações implementadas no local, toosave em despesas operacionais.

Um aspeto chave da migração no local tooAzure de aplicações está a processar necessidades de identidade Olá destas aplicações. Aplicações com suporte para o diretório poderão dependem de LDAP para o diretório de empresarial de acesso de escrita ou leitura toohello ou baseiam-se na autenticação integrada do Windows (autenticação Kerberos ou NTLM) tooauthenticate final utilizadores. Aplicações do linha de negócio (LOB) em execução no Windows Server, normalmente, são implementadas em computadores associados a um domínio, pelo que podem ser geridos em segurança através da política de grupo. too'lift e shift' nuvem de toohello de aplicações no local, tem destas dependências na infraestrutura de identidade empresarial Olá toobe resolvido.

Os administradores, muitas vezes, ativar tooone de Olá seguintes soluções toosatisfy Olá identidade às necessidades das respetivas aplicações implementadas no Azure:

* Implemente uma ligação de VPN de site a site entre as cargas de trabalho em execução nos serviços de infraestrutura do Azure e Olá empresarial diretório no local.
* Ampliar a infraestrutura de domínio/floresta de Olá AD empresarial ao configurar os controladores de domínio de réplica com máquinas virtuais do Azure.
* Implemente um domínio autónomo no Azure utilizando os controladores de domínio implementados como máquinas virtuais do Azure.

Todas estas abordagens sofrem do custo elevado e a sobrecarga administrativa. Os administradores são os controladores de domínio necessários toodeploy utilizar máquinas virtuais no Azure. Além disso, necessitam de monitor do patch do toomanage, segura, cópia de segurança e estas máquinas virtuais de resolução de problemas. dependência de Olá em toohello de ligações VPN no local diretório faz com que as cargas de trabalho implementadas no glitches de rede do Azure toobe tootransient vulnerável ou falhas. Estas falhas de rede por sua vez resultam num menor tempo de atividade e fiabilidade reduzida para estas aplicações.

Foi concebido tooprovide de serviços de domínio do Azure AD alternativa mais fácil.

## <a name="introducing-azure-ad-domain-services"></a>Introdução dos serviços de domínio do Azure AD
Serviços de domínio do AD do Azure fornece serviços de domínio geridos, tais como a associação a um domínio, autenticação de Kerberos/NTLM de política, LDAP, grupo são totalmente compatível com o Windows Server Active Directory. Pode consumir estes serviços de domínio sem necessidade de Olá para lhe toodeploy, gerir e corrigir os controladores de domínio na nuvem de Olá. Serviços de domínio do AD do Azure integra-se com o seu inquilino do Azure AD existente, deste modo, permitir que utilizadores toolog utilizando as respetivas credenciais empresariais. Além disso, pode utilizar grupos existentes e tooresources de acesso de toosecure de contas de utilizador, que garante uma smoother 'comparação de precisão-e-shift' de tooAzure de recursos no local dos serviços de infraestrutura.

Funcionalidade de serviços de domínio do AD do Azure funciona na perfeição independentemente se o seu inquilino do Azure AD é só de nuvem ou sincronizado com o Active Directory no local.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Serviços de domínio do Azure AD para organizações apenas na nuvem
Um apenas na nuvem do Azure AD de inquilino (frequentemente referidos tooas ' gerido inquilinos') não tem quaisquer requisitos de espaço de identidade no local. Por outras palavras, contas de utilizador, as respetivas palavras-passe e as associações de grupo são todos os, toohello nativa na nuvem - ou seja, criado e gerido no Azure AD. Considere para um momento que a Contoso é um apenas na nuvem inquilino do Azure AD. Conforme mostrado na seguinte ilustração de Olá, o administrador da Contoso tiver configurado uma rede virtual nos serviços de infraestrutura do Azure. Aplicações e cargas de trabalho do servidor são implementadas na rede virtual em virtual machines do Azure. Uma vez que a Contoso é um inquilino apenas na nuvem, todas as identidades de utilizador, as suas credenciais e associações a grupos são criadas e geridas no Azure AD.

![Descrição geral de serviços de domínio do Azure AD](./media/active-directory-domain-services-overview/aadds-overview.png)

Do contoso administrador de TI pode ativar os serviços de domínio do Azure AD para o seu inquilino do Azure AD e escolha toomake dos serviços de domínio disponíveis nesta rede virtual. Depois disso, os serviços de domínio do Azure AD aprovisiona um domínio gerido e torna disponível na rede virtual Olá. Todas as contas de utilizador, associações a grupos e credenciais de utilizador disponíveis no inquilino do Azure AD da Contoso também estão disponíveis neste domínio recentemente criado. Esta funcionalidade permite aos utilizadores na organização de Olá toosign no domínio toohello utilizando as respetivas credenciais empresariais - por exemplo, ao ligar remotamente toodomain computadores associados a um através do ambiente de trabalho remoto. Os administradores podem aprovisionar acesso tooresources no domínio Olá utilizando as associações de grupo existente. As aplicações implementadas em máquinas virtuais na rede virtual Olá podem utilizar funcionalidades como a associação a um domínio, LDAP leitura, LDAP bind, a autenticação NTLM e Kerberos e política de grupo.

Alguns aspetos salientes Olá domínio gerido que está aprovisionado pelos serviços de domínio do Azure AD são os seguintes:

* Do contoso administrador de TI não precisa de toomanage, patches ou para monitorizar este domínio ou quaisquer controladores de domínio para este domínio gerido.
* Não há nenhuma replicação de toomanage AD necessário para este domínio. Contas de utilizador, as associações de grupo e as credenciais de inquilino do Azure AD da Contoso estão automaticamente disponíveis dentro deste domínio gerido.
* Uma vez que o domínio de Olá é gerido pelo Azure AD nos serviços de domínio Contoso administrador de TI não tem privilégios de administrador do domínio ou de administrador de empresa neste domínio.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Serviços de domínio do Azure AD para organizações híbrida
As organizações com uma versão híbrida a infraestrutura de TI consumam uma combinação de recursos de nuvem e de recursos no local. Estas organizações sincronizam informações de identidade do seu inquilino do Azure AD de tootheir de diretório no local. Como as organizações a híbrida parecer toomigrate mais os respetivos nuvem toohello de aplicações no local, especialmente legadas com suporte para o diretório de aplicações, serviços de domínio do Azure AD podem ser útil toothem.

Implementou litware Corporation [do Azure AD Connect](../active-directory/active-directory-aadconnect.md), informações de identidade toosynchronize do respetivo inquilino de tootheir do Azure AD de diretório no local. incluem informações de identidade Olá que são sincronizadas a contas de utilizador, os hashes de credencial de autenticação (sincronização de palavra-passe) e as associações de grupo.

> [!NOTE]
> **Sincronização de palavra-passe é obrigatória para as organizações de híbrida toouse dos serviços de domínio do Azure AD**. Este requisito é porque são necessárias credenciais dos utilizadores no Olá gerido domínio fornecida pelos serviços de domínio do Azure AD, tooauthenticate estes utilizadores através de métodos de autenticação de NTLM ou Kerberos.
>
>

![Serviços de domínio do Azure AD para Litware Corporation](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Olá ilustração anterior mostra como as organizações com uma versão híbrida a infraestrutura de TI, tais como Litware Corporation, podem utilizar os serviços de domínio do Azure AD. Aplicações e cargas de trabalho do servidor que requerem os serviços de domínio da litware são implementadas numa rede virtual nos serviços de infraestrutura do Azure. Do litware administrador de TI pode ativar os serviços de domínio do Azure AD para o seu inquilino do Azure AD e escolha toomake um domínio gerido disponível nesta rede virtual. Uma vez que Litware organização com uma versão híbrida a infraestrutura de TI, contas de utilizador, grupos e as credenciais são sincronizados tootheir do Azure AD de inquilino do seu diretório no local. Esta funcionalidade permite que os utilizadores toosign no domínio toohello utilizando as respetivas credenciais empresariais - por exemplo, ao ligar remotamente toomachines associados a um domínio toohello através do ambiente de trabalho remoto. Os administradores podem aprovisionar acesso tooresources no domínio Olá utilizando as associações de grupo existente. As aplicações implementadas em máquinas virtuais na rede virtual Olá podem utilizar funcionalidades como a associação a um domínio, LDAP leitura, LDAP bind, a autenticação NTLM e Kerberos e política de grupo.

Alguns aspetos salientes Olá domínio gerido que está aprovisionado pelos serviços de domínio do Azure AD são os seguintes:

* domínio Olá de gerido é um domínio autónomo. Não é uma extensão de domínio da Litware no local.
* Do litware administrador de TI não precisa de toomanage, correção ou controladores de domínio do monitor para este domínio gerido.
* Não há nenhum domínio de toothis necessidade toomanage AD replicação. Contas de utilizador, as associações de grupo e as credenciais de diretório no local da Litware são sincronizado tooAzure AD através do Azure AD Connect. Estas contas de utilizador, as associações de grupo e as credenciais estão automaticamente disponíveis no domínio Olá de gerido.
* Uma vez que o domínio de Olá é gerido pelo Azure AD nos serviços de domínio Litware administrador de TI não tem privilégios de administrador do domínio ou de administrador de empresa neste domínio.

## <a name="benefits"></a>Benefícios
Com os serviços de domínio do Azure AD, possam desfrutar Olá seguintes vantagens:

* **Simples** – pode satisfazer necessidades de identidade Olá de máquinas virtuais implementadas tooAzure serviços de infraestrutura com alguns cliques. Não precisa de toodeploy e gerir a infraestrutura de identidade no Azure ou a configuração infraestrutura de identidade conectividade back tooyour no local.
* **Integrada** – os serviços de domínio do Azure AD está profundamente integrado com o seu inquilino do Azure AD. Agora pode utilizar o Azure AD como um diretório de enterprise integrada baseada na nuvem que caters toohello necessidades da sua aplicações modernas e de aplicações com suporte para o diretório tradicionais.
* **Compatível** – os serviços de domínio do Azure AD baseia-se na infraestrutura de nível empresarial comprovado Olá do Windows Server Active Directory. Por conseguinte, as aplicações podem dependem de um maior nível de compatibilidade com as funcionalidades do Windows Server Active Directory. Nem todas as funcionalidades disponíveis no Windows Server AD estão atualmente disponíveis nos serviços de domínio do Azure AD. No entanto, as funcionalidades disponíveis são compatíveis com funcionalidades do Windows Server AD correspondentes Olá que dependem na sua infraestrutura no local. Olá LDAP, capacidades de associação de Kerberos, NTLM, política de grupo e domínio constituem uma oferta madura que tem sido testada e foi refinada através de várias versões do Windows Server.
* **Económica** – com os serviços de domínio do Azure AD, pode evitar o fardo de gestão e infraestrutura Olá que estão associado com gestão de identidade infraestrutura toosupport tradicional diretório com suporte para aplicações. Pode mover estes tooAzure de aplicações dos serviços de infraestrutura e beneficiar de maiores reduções em despesas operacionais.
