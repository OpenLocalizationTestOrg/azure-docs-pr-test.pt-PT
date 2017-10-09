---
title: "aaaFAQs - serviços de domínio do Active Directory do Azure | Microsoft Docs"
description: "Perguntas mais frequentes sobre serviços de domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Serviços de domínio do Azure Active Directory: Perguntas mais frequentes (FAQ)
Esta página respostas a perguntas mais frequentes sobre Olá do Azure Active Directory Domain Services. Manter a verificação de volta para atualizações.

### <a name="troubleshooting-guide"></a>Guia de resolução de problemas
Consulte tooour [guia de resolução de problemas](active-directory-ds-troubleshooting.md) para problemas de toocommon soluções encontrou quando configurar ou administração dos serviços de domínio do Azure AD.

### <a name="configuration"></a>Configuração
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Posso criar vários domínios para um único diretório do Azure AD?
Não. Só pode criar um único domínio de manutenção pelos serviços de domínio do Azure AD para um único diretório do Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Pode ativar os serviços de domínio do Azure AD numa rede virtual do Azure Resource Manager?
Não. Serviços de domínio do AD do Azure só podem ser ativados numa rede virtual do Azure clássica. Pode ligar Olá rede virtual clássica tooa Resource Manager rede virtual utilização toouse peering de rede virtual do seu domínio gerido numa rede virtual do Gestor de recursos.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Posso ativar os serviços de domínio do Azure AD no Azure federado diretório AD? Utilizar o utilizadores do AD FS tooauthenticate para acesso tooOffice 365. Pode ativar os serviços de domínio do Azure AD para este diretório?
Não. Serviços de domínio do AD do Azure tem de aceder a toohello hashes de palavra-passe de contas de utilizador, os utilizadores de tooauthenticate através de NTLM ou Kerberos. Num diretório federado, os hashes de palavra-passe não são armazenados no diretório do Azure AD de Olá. Por conseguinte, os serviços de domínio do Azure AD não funciona com essas diretórios do Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Pode posso disponibilizar os serviços de domínio do Azure AD em várias redes virtuais na minha subscrição?
serviço de Olá propriamente dito não suporta diretamente neste cenário. Serviços de domínio do AD do Azure está disponível na rede virtual apenas uma de cada vez. No entanto, pode configurar a conectividade entre várias redes virtuais tooexpose serviços de domínio do Azure AD tooother redes virtuais. Este artigo descreve como pode [ligar redes virtuais no Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Pode ativar os serviços de domínio do Azure AD através do PowerShell?
Implementação automatizada/PowerShell dos serviços de domínio do Azure AD não está disponível atualmente.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Serviços de domínio do Azure AD está disponível no novo portal do Azure Olá?
Não. Serviços de domínio do Azure AD podem ser configurados apenas no Olá [portal clássico do Azure](https://manage.windowsazure.com). Esperamos tooextend suporte para Olá [portal do Azure](https://portal.azure.com) no Olá futura.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>Pode adicionar domínio gerido do domínio controladores tooan dos serviços de domínio do Azure AD?
Não. domínio Olá fornecido pelos serviços de domínio do Azure AD é um domínio gerido. Não é necessário tooprovision, configurar ou gerir os controladores de domínio para este domínio - estas atividades são fornecidas como um serviço pela Microsoft de gestão. Por conseguinte, não é possível adicionar controladores de domínio adicional (leitura / escrita ou só de leitura) para o domínio Olá de gerido.

### <a name="administration-and-operations"></a>Administração e operações
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Pode ligar o controlador de domínio toohello para o meu domínio gerido utilizando o ambiente de trabalho remoto?
Não. Não dispõe de controladores de toodomain tooconnect permissões para Olá domínio gerido através do ambiente de trabalho remoto. Os membros Olá ' AAD DC' do grupo de administradores podem administrar Olá domínio gerido utilizando ferramentas de administração do AD como Olá Centro de administração do Active Directory (ADAC) ou do AD do PowerShell. Estas ferramentas são instaladas utilizando o Olá 'Server ferramentas de administração remota' funcionalidade num servidor Windows associados a um domínio gerido toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Posso tiver ativado os serviços de domínio do Azure AD. Que conta de utilizador utilizar toodomain associar domínio de toothis máquinas?
Os membros do grupo administrativo de Olá 'AAD DC administradores' podem máquinas de associação de domínio. Além disso, os membros deste grupo recebem toomachines de acesso de ambiente de trabalho remoto que tenham sido toohello associado ao domínio.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Alguns têm privilégios de administrador de domínio para o domínio gerido Olá fornecida pelos serviços de domínio do Azure AD?
Não. Não são concedidos privilégios administrativos no domínio Olá de gerido. Privilégios de administrador de domínio e o administrador de empresa não estão disponíveis para toouse dentro do domínio Olá. Administrador de domínio existente ou grupos de administrador de empresa no seu diretório do Azure AD são também não concedidos privilégios de administrador empresarial/domínio no domínio Olá.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Pode modificar as associações de grupo utilizando outras ferramentas de administração do AD ou LDAP em domínios geridos?
Não. As associações de grupo não podem ser modificadas em domínios de manutenção pelos serviços de domínio do Azure AD. Olá que mesmo se aplica a atributos de utilizador. No entanto pode alterar as associações de grupo ou os atributos de utilizador no Azure AD ou no seu domínio no local. Essas alterações são automaticamente sincronizado tooAzure AD nos serviços de domínio.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Quanto tempo demora para que as alterações posso fazer com que toomy do Azure AD directory toobe visível no meu domínio gerido?
As alterações efetuadas no diretório do Azure AD utilizando o Olá IU do Azure AD ou o PowerShell são domínio gerido tooyour sincronizados. Este processo de sincronização é executado em segundo plano de Olá. Depois de concluída a Olá única a sincronização inicial do seu diretório,-normalmente demora cerca de 20 minutos para as alterações efetuadas no Azure AD toobe refletidas no seu domínio gerido.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Pode expandir o esquema de Olá de domínio geridos Olá fornecido pelos serviços de domínio do Azure AD?
Não. esquema de Olá é administrada pela Microsoft para o domínio Olá de gerido. Extensões de esquema não são suportadas pelos serviços de domínio do Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Pode modificar ou adicionar registos DNS no meu domínio gerido?
Sim. Os membros do grupo Olá 'AAD DC administradores' são concedidos privilégios de administrador de DNS, toomodify DNS regista no domínio Olá de gerido. Pode utilizarem a consola do Gestor de DNS Olá num computador em execução do Windows Server toohello associados a um domínio gerido, toomanage DNS. Olá toouse consola do Gestor de DNS, instale 'Ferramentas do servidor DNS', que faz parte da funcionalidade de opcional 'Ferramentas de administração de servidor remoto' Olá no servidor de Olá. Obter mais informações sobre [utilitários para administrar, monitorização e resolução de problemas de DNS](https://technet.microsoft.com/library/cc753579.aspx) está disponível no TechNet.

### <a name="billing-and-availability"></a>Disponibilidade e de faturação
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>É que um serviço pago dos serviços de domínio do Azure AD?
Sim. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Existe uma versão de avaliação gratuita para o serviço de Olá?
Este serviço está incluído na versão de avaliação gratuita do Olá para o Azure. Pode inscrever-se para obter um [avaliação de um mês do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Pode obter os serviços de domínio do Azure AD como parte do Enterprise Mobility Suite (EMS)? É necessário dos serviços de domínio do Azure AD Premium toouse do Azure AD?
Não. Serviços de domínio do AD do Azure é uma serviço do Azure pay as you go e não faz parte do EMS. Serviços de domínio do Azure AD pode ser utilizados com todas as edições do Azure AD (gratuita, básico e, Premium). São faturadas numa base horária, dependendo de utilização.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>As regiões do Azure está disponível no serviço de Olá?
Consulte toohello [serviços do Azure por região](https://azure.microsoft.com/regions/#services/) Olá de página toosee uma lista de regiões do Azure onde os serviços de domínio do Azure AD está disponível.
