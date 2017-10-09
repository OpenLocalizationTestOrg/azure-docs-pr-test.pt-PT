---
title: "aaaAzure AD Connect e a Federação | Microsoft Docs"
description: "Esta página é uma localização central de Olá para toda a documentação relativas à operações do AD FS que utilizam o Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect e a federação
Azure Connect do Active Directory (Azure AD) permite ao configurar a Federação com o local Serviços de Federação do Active Directory (AD FS) e o Azure AD. Com Federação início de sessão, pode ativar utilizadores toosign nos tooAzure baseada em AD serviços com as palavras-passe no local – e, enquanto na rede empresarial Olá, sem ter tooenter as palavras-passe novamente. Utilizando a opção de Federação Olá com o AD FS, pode implementar uma nova instalação do AD FS ou pode especificar uma instalação existente num farm do Windows Server 2012 R2.

Este tópico é Olá inicial para obter informações sobre as funcionalidades relacionadas com a Federação para o Azure AD Connect. Apresenta uma lista ligações tooall relacionadas com tópicos. Para ligações tooAzure AD Connect, consulte [integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Do Azure AD Connect: tópicos de Federação
| Tópico | O que abrange e quando tooread-la |
|:--- |:--- |
| **Opções do Azure AD Connect utilizador iniciar sessão** | |
| [Compreender as opções de início de sessão do utilizador](active-directory-aadconnect-user-signin.md) |Saiba mais sobre as várias opções de início de sessão do utilizador e como afetam a experiência de utilizador Olá o início de sessão do Azure. |
| **Instalar o AD FS utilizando o Azure AD Connect** | |
| [Pré-requisitos](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Consulte Olá pré-requisitos para uma instalação do AD FS com êxito através do Azure AD Connect. |
| [Configurar um farm do AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Instale um novo farm do AD FS utilizando o Azure AD Connect. |
| [Federar com o Azure AD utilizando o ID de início de sessão alternativo](active-directory-aadconnect-federation-management.md#alternateid) | Configurar a Federação com o ID de início de sessão alternativo  |
| **Modificar a configuração do Olá AD FS** | |
| [Reparação Olá confiança](active-directory-aadconnect-federation-management.md#repairthetrust) |Reparação Olá atual confiança no local do AD FS e o Office 365/Azure. |
| [Adicionar um novo servidor do AD FS](active-directory-aadconnect-federation-management.md#addadfsserver) |Expanda um farm do AD FS com um servidor do AD FS adicional após a instalação inicial. |
| [Adicionar um novo servidor do WAP do AD FS](active-directory-aadconnect-federation-management.md#addwapserver) |Expanda um farm do AD FS com um servidor de Proxy de aplicações Web (WAP) adicionais após a instalação inicial. |
| [Adicionar um novo domínio federado](active-directory-aadconnect-federation-management.md#addfeddomain) |Adicionar outro domínio toobe, federada com o Azure AD. |
| [Atualizar o certificado SSL Olá](active-directory-aadconnectfed-ssl-update.md)| Atualize o certificado SSL de Olá para um farm do AD FS. |
| **Outra configuração de Federação** | |
| [Federar várias instâncias do Azure AD com uma instância única do AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Federar vários do Azure AD com única farm do AD FS| 
| [Adicionar uma ilustração/logótipo de empresa personalizado](active-directory-aadconnect-federation-management.md#customlogo) |Modificar a experiência de início de sessão Olá especificando Olá personalizado do logótipo do que é apresentado no AD FS início de sessão página Olá. |
| [Adicione uma descrição de início de sessão](active-directory-aadconnect-federation-management.md#addsignindescription) |Alterar Olá início de sessão descrição na página de início de sessão Olá do AD FS. |
| [Modificar as regras de afirmações do AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Modificar ou adicionar regras de afirmação no AD FS que correspondem a configuração da sincronização tooAzure AD Connect. |


## <a name="additional-resources"></a>Recursos adicionais
* [Federação duas do Azure AD com o único do AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Implementação do AD FS no Azure](active-directory-aadconnect-azure-adfs.md)
* [Implementação do elevada disponibilidade em vários locais geográfica AD FS no Azure com o Gestor de tráfego do Azure](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
