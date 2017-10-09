---
title: Atributos sincronizados pelo Azure AD Connect | Microsoft Docs
description: "Apresenta uma lista de atributos de Olá que são sincronizados tooAzure do Active Directory."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Sincronização do Azure AD Connect: atributos sincronizados tooAzure do Active Directory
Este tópico apresenta uma lista de atributos de Olá que estão sincronizados com a sincronização do Azure AD Connect.  
Olá atributos estão agrupados por Olá relacionadas com a aplicação Azure AD.

## <a name="attributes-toosynchronize"></a>Toosynchronize de atributos
Uma pergunta comum é *Novidades lista Olá de atributos mínimo toosynchronize*. predefinição de Olá e a abordagem recomendada é atributos do tookeep Olá predefinidos para que um total GAL (lista de endereços Global) pode ser construído numa Olá nuvem e tooget todas as funcionalidades em cargas de trabalho do Office 365. Em alguns casos, existem alguns atributos que sua organização pretende toohello sincronizados nuvem, uma vez que estes atributos contêm confidenciais ou dados do PII (informação identificativa), como neste exemplo:  
![atributos incorretos](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

Neste caso, iniciar com a lista de Olá de atributos neste tópico e identificar os atributos que deveria conter confidenciais ou dados PII e não não possível sincronizar. Em seguida, desmarque esses atributos durante a instalação utilizando [aplicação Azure AD e filtragem de atributos](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Quando desmarcando atributos, deve tenha cuidado e desmarque apenas esses toosynchronize absolutamente não é possível de atributos. Unselecting outros atributos pode ter um impacto negativo sobre funcionalidades.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Nome do atributo | Utilizador | Comentário |
| --- |:---:| --- |
| accountEnabled |X |Define se a uma conta estiver ativada. |
| CN |X | |
| displayName |X | |
| Sidobjeto |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| pwdLastSet |X |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| sourceAnchor |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| usageLocation |X |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |

## <a name="exchange-online"></a>Exchange Online
| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| Assistente de |X |X | | |
| altRecipient |X | | |Requer o Azure AD Connect compilação 1.1.552.0 ou após. |
| authOrig |X |X |X | |
| C |X |X | | |
| CN |X | |X | |
| Co |X |X | | |
| Empresa |X |X | | |
| Indicativo do país |X |X | | |
| Departamento |X |X | | |
| descrição |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| HomePhone |X |X | | |
| informações |X |X |X |Atualmente, este atributo é consumido não para grupos. |
| iniciais |X |X | | |
| l |X |X | | |
| LegacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| Gestor |X |X | | |
| Membro | | |X | |
| Mobile |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Disponível no Azure AD Connect versão 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Este atributo é atualmente não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Este atributo é atualmente não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Este atributo é atualmente não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Este atributo é atualmente não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Este atributo é atualmente não é consumido pelo Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg IsOrganizational | | |X | |
| Sidobjeto |X | |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| Pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| PostalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Derivado groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Título |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| authOrig |X |X |X | |
| C |X |X | | |
| CN |X | |X | |
| Co |X |X | | |
| Empresa |X |X | | |
| Indicativo do país |X |X | | |
| Departamento |X |X | | |
| descrição |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homephone |X |X | | |
| informações |X |X |X | |
| iniciais |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| capacidade de correio |X |X |X | |
| mailNickname |X |X |X | |
| Está | | |X | |
| Gestor |X |X | | |
| Membro | | |X | |
| middleName |X |X | | |
| Mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| Sidobjeto |X | |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| OtherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| Pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| PostalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Derivado groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Título |X |X | | |
| unauthOrig |X |X |X | |
| URL |X |X | | |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X | | |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| C |X |X | | |
| CN |X | |X | |
| Co |X |X | | |
| Empresa |X |X | | |
| Departamento |X |X | | |
| descrição |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homephone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| capacidade de correio |X |X |X | |
| mailNickname |X |X |X | |
| Está | | |X | |
| Gestor |X |X | | |
| Membro | | |X | |
| Mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-linha |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| Sidobjeto |X | |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| PostalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| securityEnabled | | |X |Derivado groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Título |X |X | | |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X | | |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>O Azure RMS
| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| CN |X | |X |Nome ou alias comum. Mais frequentemente Olá prefixo do valor de [correio]. |
| displayName |X |X |X |Uma cadeia que representa o nome de Olá, muitas vezes, são apresentada como nome amigável do Olá (Apelido Nome próprio). |
| capacidade de correio |X |X |X |endereço de e-mail completo. |
| Membro | | |X | |
| Sidobjeto |X | |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| proxyAddresses |X |X |X |propriedade mechanical. Utilizada pelo Azure AD. Contém todos os endereços de e-mail secundário para o utilizador Olá. |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. |
| securityEnabled | | |X |Derivado groupType. |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X | | |Este UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |

## <a name="intune"></a>Intune
| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| C |X |X | | |
| CN |X | |X | |
| descrição |X |X |X | |
| displayName |X |X |X | |
| capacidade de correio |X |X |X | |
| mailNickname |X |X |X | |
| Membro | | |X | |
| Sidobjeto |X | |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| securityEnabled | | |X |Derivado groupType |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X | | |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| C |X |X | | |
| CN |X | |X | |
| Co |X |X | | |
| Empresa |X |X | | |
| Indicativo do país |X |X | | |
| descrição |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| Está | | |X | |
| Gestor |X |X | | |
| Membro | | |X | |
| Mobile |X |X | | |
| Sidobjeto |X | |X |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| physicalDeliveryOfficeName |X |X | | |
| PostalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| securityEnabled | | |X |Derivado groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| telephoneNumber |X |X | | |
| Título |X |X | | |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X | | |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |

## <a name="3rd-party-applications"></a>aplicações de terceiros 3rd
Este grupo é um conjunto de atributos utilizado como Olá atributos mínimo necessários para uma carga de trabalho genérica ou aplicação. Pode ser utilizado para uma carga de trabalho não listado no outra secção ou para uma aplicação de terceiros. Explicitamente é utilizado para seguinte Olá:

* Yammer (apenas o utilizador é consumido)
* [Cenários colaboração híbridos empresa-empresa (B2B) entre org oferecidos pelos recursos como o SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Este grupo é um conjunto de atributos que pode ser utilizado se o diretório do Azure AD de Olá não for utilizado toosupport do Office 365, Dynamics, ou o Intune. Tem um pequeno conjunto de atributos principais.

| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se a uma conta estiver ativada. |
| CN |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| capacidade de correio |X | |X | |
| Está | | |X | |
| mailNickName |X |X |X | |
| Membro | | |X | |
| Sidobjeto |X | | |propriedade mechanical. Identificador de utilizador do AD utilizado toomaintain sincronização entre o Azure AD e AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mechanical. Utilizado tooknow quando tooinvalidate já os tokens emitidos. Utilizado pela sincronização de palavra-passe e a Federação. |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mechanical. Relação de toomaintain identificador imutável entre ADDS e o Azure AD. |
| usageLocation |X | | |propriedade mechanical. país do utilizador Olá. Utilizado para a atribuição de licença. |
| userPrincipalName |X | | |UPN é Olá ID de início de sessão do utilizador Olá. Mais frequentemente Olá igual ao valor de [correio]. |

## <a name="windows-10"></a>Windows 10
Um computer(device) do Windows 10 associados a um domínio sincroniza tooAzure alguns atributos AD. Para obter mais informações sobre os cenários de Olá, consulte [ligar dispositivos associados a domínios tooAzure AD para experiências do Windows 10](../active-directory-azureadjoin-devices-group-policy.md). Estes atributos sempre sincronizar e Windows 10 não aparece como uma aplicação que pode anular a seleção. Um computador associado a um domínio do Windows 10 é identificado por ter Olá atributo userCertificate preenchido.

| Nome do atributo | Dispositivo | Comentário |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |Valor de codificado para computadores associados a um domínio. |
| displayName |X | |
| MS-DS-CreatorSID |X |Também denominado registeredOwnerReference. |
| objectGUID |X |Também denominado deviceID. |
| Sidobjeto |X |Também denominado onPremisesSecurityIdentifier. |
| sistema operativo |X |Também denominado deviceOSType. |
| operatingSystemVersion |X |Também denominado deviceOSVersion. |
| userCertificate |X | |

Estes atributos para **utilizador** é Ademais toohello que outras aplicações que selecionou.  

| Nome do atributo | Utilizador | Comentário |
| --- |:---:| --- |
| domainFQDN |X |Também denominado dnsDomainName. Por exemplo, contoso.com. |
| domainNetBios |X |Também denominado netBiosName. Por exemplo, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Repetição de escrita do Exchange híbrida
Estes atributos são gravados do Azure AD tooon local do Active Directory quando seleciona tooenable **híbrida do Exchange**. Dependendo da versão do Exchange, poderão estar sincronizados menos atributos.

| Nome do atributo | Utilizador | Contacto | Grupo | Comentário |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Derivado cloudAnchor no Azure AD. Este atributo é novo no Exchange 2016 e AD do Windows Server 2016. |
| msExchArchiveStatus |X | | |Arquivo online: Correio tooarchive permite que os clientes. |
| msExchBlockedSendersHash |X | | |Filtragem: Escreve novamente no local de filtragem e os dados de remetente seguro e bloqueadas online dos clientes. |
| msExchSafeRecipientsHash |X | | |Filtragem: Escreve novamente no local de filtragem e os dados de remetente seguro e bloqueadas online dos clientes. |
| msExchSafeSendersHash |X | | |Filtragem: Escreve novamente no local de filtragem e os dados de remetente seguro e bloqueadas online dos clientes. |
| msExchUCVoiceMailSettings |X | | |Ativar Unified Messaging (UM) - correio de voz Online: utilizadas pelo Microsoft Lync Server integração tooindicate tooLync Server no local que o utilizador Olá tem o correio de voz nos serviços online. |
| msExchUserHoldPolicies |X | | |Suspensão de litígio: Permite toodetermine de serviços em nuvem que os utilizadores estão em litígio conter. |
| proxyAddresses |X |X |X |É inserido apenas para endereço Olá x500 do Exchange Online. |
| publicDelegates |X | | |Permite que um Exchange Online toobe de caixa de correio concedido SendOnBehalfTo direitos toousers com caixa de correio do Exchange no local. Requer o Azure AD Connect compilação 1.1.552.0 ou após. |

## <a name="exchange-mail-public-folder"></a>Pasta de público de correio do Exchange
Estes atributos são sincronizados entre no local do Active Directory tooAzure AD Quando seleciona tooenable **pasta pública de correio eletrónico Exchange**.

| Nome do atributo | PublicFolder | Comentário |
| --- | :---:| --- |
| displayName | X |  |
| capacidade de correio | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Repetição de escrita do dispositivo
Objetos de dispositivo são criados no Active Directory. Estes objetos podem ser dispositivos associados tooAzure AD ou a computadores associados a domínios do Windows 10.

| Nome do atributo | Dispositivo | Comentário |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| DN |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Apenas com o esquema do AD do Windows Server 2016 |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Notas
* Quando utilizar um ID alternativo, hello no local atributo userPrincipalName é sincronizado com onPremisesUserPrincipalName de atributo Olá do Azure AD. Olá, o atributo ID alternativo, por exemplo correio, está sincronizado com Olá do Azure AD atributo userPrincipalName.
* Nas listas de Olá acima, Olá tipo de objeto **utilizador** também se aplica o tipo de objeto toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
