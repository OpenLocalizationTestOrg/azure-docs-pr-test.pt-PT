---
title: "lista de compatibilidades de Federação aaaAzure AD"
description: "Esta página tem não Microsoft fornecedores de identidade que podem ser utilizado tooimplement único início de sessão."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a>Lista de compatibilidades de federação do Azure AD
Azure Active Directory fornece o início de sessão único em e modulação de segurança de acesso de aplicação para Office 365 e outros serviços Online da Microsoft para implementações de apenas na nuvem e de híbrida sem necessidade de qualquer solução de terceiros. Office 365, como a maioria dos Serviços Online da Microsoft, está integrado com o Azure Active Directory para serviços de diretório, autenticação e autorização. Azure Active Directory fornece também toothousands de início de sessão único de aplicações SaaS e no local as aplicações web. Consulte Galeria de aplicações do Azure Active Directory Olá para aplicações SaaS suportadas.

Nas organizações que tenham investido em soluções de Federação de terceiros, este tópico contém orientações para configurar início de sessão único para os respetivos utilizadores do Windows Server Active Directory com o Microsoft Online services utilizando fornecedores de identidade de terceiros Olá "do Azure Active Directory Federação compatibilidade lista" abaixo. 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
[Grupo de computadores Oxford](http://oxfordcomputergroup.com/), uma terceiros em nome da Microsoft, testada estes único início de sessão experiências utilizando fornecedores de identidade de terceiros em relação a um conjunto de casos de utilização comuns com o Azure Active Directory.

Para informações sobre como obter o seu fornecedor de identidade de terceiros listado aqui, contacte o grupo de computador do Oxford em [ idp@oxfordcomputergroup.com ](mailto:idp@oxfordcomputergroup.com).

> [!IMPORTANT]
> Grupo de computadores Oxford testado funcionalidade para Federação de Olá apenas um destes cenários de início de sessão único. Grupo de computadores Oxford não tiver sido executada qualquer teste de sincronização de Olá, autenticação de dois fatores, etc. os componentes destes cenários de início de sessão único.
> 
> Utilização de início de sessão por ID alternativo tooUPN também é testada não no programa.
> 
> 

* [Azure Active Directory](#azure-active-directory)
* [4.5 o início de sessão único AuthAnvil](#authanvil-single-sign-on-45)
* [BIG-IP com o Gestor de políticas de acesso BIG-IP ver. 11.3 x – 11, 6x](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [BitGlass](#bitglass)
* [Nuvem segura de AC](#ca-secure-cloud) 
* [AC SiteMinder 12.52](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [Centrify](#centrify) 
* [Dell um Gestor de acesso de nuvem de identidade v7.1](#dell-one-identity-cloud-access-manager-v71) 
* [Autenticação DigitalPersona compostos](#digitalpersona-composite-authentication)
* [IBM Tivoli federado 6.2.2 do Identity Manager](#ibm-tivoli-federated-identity-manager-622) 
* [IceWall Federação versão 3.0](#icewall-federation-version-30) 
* [Memority](#memority)
* [Gestor de acesso de NetIQ 4. x](#netiq-access-manager-4x) 
* [Okta](#okta) 
* [OneLogin](#onelogin) 
* [Serviços de Federação de servidor do Virtual identidade IDM ideal](#optimal-idm-virtual-identity-server-federation-services) 
* [PingFederate 6.11, 7.2, 8. x](#pingfederate-611-72-8x)
* [RadiantOne CFS 3.0](#radiantone-cfs-30) 
* [Sailpoint IdentityNow](#sailpoint-identitynow)
* [SecureAuth IdP 7.2.0](#secureauth-idp-720) 
* [Inicie sessão & go 5.3](#signgo-53) 
* [Porta de serviço Online da tecnologia de SoftBank](#softbank)
* [Área de trabalho VMware um](#vmware-workspace-one)



> [!IMPORTANT]
> Uma vez que estes são os produtos de terceiros, a Microsoft fornece suporte para implementação de Olá, configuração, resolução de problemas, melhores práticas, etc. problemas e perguntas sobre estes fornecedores de identidade. Para suporte e perguntas sobre estes fornecedores de identidade, contacte diretamente a terceiros Olá suportado.
> 
> Estes fornecedores de identidade de terceiros foram testados para interoperabilidade com a utilização de WS-Federation e apenas os protocolos de WS-Trust cloud services da Microsoft. A testar não incluiu através do protocolo SAML Olá.
> 


## <a name="azure-active-directory"></a>Azure Active Directory

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |
| Aplicações modernas utilizam a ADAL, tais como o Office 2016 |Suportado |Nenhuma |

Para obter mais informações sobre como utilizar o Azure Active Directory com o AD FS, consulte [serviços de Federação do Active Directory (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

Para obter mais informações sobre como utilizar o Azure Active Directory com sincronização de palavra-passe Consulte [do Azure AD Connect](active-directory-aadconnect.md).

## <a name="authanvil-single-sign-on-45"></a>4.5 o início de sessão único AuthAnvil

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações, consulte [AuthAnvil início de sessão único.](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a>BIG-IP com o Gestor de políticas de acesso BIG-IP ver. 11.3 x – 11, 6x

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Não suportado |Não suportado |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre o Gestor de políticas de acesso do BIG-IP, consulte [Gestor de políticas de acesso BIG-IP.](https://f5.com/products/modules/access-policy-manager) 

Para obter instruções de Gestor de políticas de acesso BIG-IP de Olá sobre como tooconfigure transferir este tooyour de experiência de início de sessão único de Olá STS tooprovide utilizadores do Active Directory, Olá pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).

## <a name="bitglass"></a>BitGlass

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre BitGlass consulte [BitGlass](http://www.bitglass.com).

## <a name="ca-secure-cloud"></a>Nuvem segura de AC

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre a nuvem de proteger a AC, consulte [AC Secure nuvem](http://www.ca.com/us/products/security-as-a-service.aspx).

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a>AC SiteMinder 12.52 SP1 cumulativa versão 4

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para mais informações sobre SiteMinder de AC, consulte [AC SiteMinder Federação](http://www.ca.com/us/products/ca-single-sign-on.html). 

## <a name="centrify"></a>Centrify

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Controlo de acesso de cliente não é suportado |

Para mais informações sobre Centrify, consulte [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).

## <a name="dell-one-identity-cloud-access-manager-v71"></a>Dell um Gestor de acesso de nuvem de identidade v7.1

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre Dell uma identidade de nuvem Gestor de acesso, consulte [Gestor de acesso para Dell uma identidade de nuvem](http://software.dell.com/products/cloud-access-manager).

 Para Olá obter instruções sobre como tooconfigure este tooyour de experiência de início de sessão único de Olá STS tooprovide utilizadores do Office 365, consulte o artigo [configurar utilizadores do Office 365](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365). 

## <a name="digitalpersona-composite-authentication"></a>Autenticação DigitalPersona compostos  

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows|
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows|
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações consulte [autenticação composta DigitalPersona](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).


## <a name="ibm-tivoli-federated-identity-manager-622"></a>IBM Tivoli federado 6.2.2 do Identity Manager

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre o IBM Tivoli federado Identity Manager, consulte [IBM Gestor de acesso de segurança para Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).

## <a name="icewall-federation-version-30"></a>IceWall Federação versão 3.0

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre IceWall Federação, consulte [IceWall Federação versão 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) e [IceWall federação com o Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).

## <a name="memority"></a>Memority

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre como utilizar Memority consulte [Memority](http://www.memority.com).


## <a name="netiq-access-manager-4x"></a>Gestor de acesso de NetIQ 4. x

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma|
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma|
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações, consulte [Gestor de acesso de NetIQ](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).

## <a name="okta"></a>Okta

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Autenticação integrada do Windows requer a configuração do servidor web adicional e aplicação de Okta. |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para mais informações sobre Okta, consulte [Okta](https://www.okta.com/).

## <a name="onelogin"></a>OneLogin

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para mais informações sobre OneLogin, consulte [OneLogin](https://www.onelogin.com/).

## <a name="optimal-idm-virtual-identity-server-federation-services"></a>Serviços de Federação de servidor do Virtual identidade IDM ideal

seguinte Olá é Olá matriz de suporte de cenário esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |

Para obter mais informações sobre o cliente Consulte de políticas de acesso [tooOffice de limitar o acesso a 365 serviços com base no Olá localização do cliente de Olá](https://technet.microsoft.com/library/hh526961.aspx).





## <a name="pingfederate-611-72-8x"></a>PingFederate 6.11, 7.2, 8. x

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para Olá PingFederate obter instruções sobre como tooconfigure este STS tooprovide Olá-início de sessão único experiência de utilizadores do Active Directory tooyour, consulte um dos seguintes Olá: 

- [PingFederate 6.11](http://go.microsoft.com/fwlink/?LinkID=266321)
- [PingFederate 7.2](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [PingFederate 8. x](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a>RadiantOne CFS 3.0

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre RadiantOne CFS, consulte [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).

## <a name="sailpoint-identitynow"></a>Sailpoint IdentityNow

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações, consulte [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).

## <a name="secureauth-idp-720"></a>SecureAuth IdP 7.2.0

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Nenhuma |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para mais informações sobre SecureAuth, consulte [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).














## <a name="signgo-53"></a>Inicie sessão & go 5.3

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Contratos de Kerberos suportada |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Nenhuma |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Início de sessão & go 5.3 suporta a autenticação Kerberos através da configuração de um contrato de Kerberos.  Para obter ajuda com esta configuração, contacte o guia de configuração de Olá Ilex ou vista [sessão & go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)

## <a name="softbank-technology-online-service-gate"></a>Porta de serviço Online da tecnologia de SoftBank

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre a porta de serviço Online do SoftBank tecnologia consulte [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)

## <a name="vmware-workspace-one"></a>Área de trabalho VMware um

Olá que se segue matriz de suporte de cenário Olá para esta experiência de início de sessão único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, tais como o acesso Web do Exchange e ao SharePoint Online |Suportado |Não é suportada a autenticação integrada do Windows |
| Aplicações de clientes avançados, tais como o Lync, a subscrição do Office, CRM |Suportado |Não é suportada a autenticação integrada do Windows |
| Clientes de e-mail Avançada, tais como o Outlook e ActiveSync |Suportado |Nenhuma |

Para obter mais informações sobre consulte [um de área de trabalho do VMware](http://www.vmware.com/pdf/vidm-office365-saml.pdf)

