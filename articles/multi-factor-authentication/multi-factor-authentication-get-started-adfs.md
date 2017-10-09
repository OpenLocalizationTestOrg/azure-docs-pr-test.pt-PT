---
title: "verificação de aaaTwo passo e o AD FS - MFA do Azure | Microsoft Docs"
description: "Esta é a página de autenticação do Olá multi-factor do Azure que descreve como tooget utilizar a MFA do Azure e o AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Introdução ao Multi-Factor Authentication do Azure e aos Serviços de Federação do Active Directory
<center>![Nuvem](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Se a sua organização tiver federado o seu Active Directory no local com o Azure Active Directory através do AD FS, existem duas opções para utilizar o Multi-Factor Authentication do Azure.

* Proteger recursos da nuvem com o Multi-Factor Authentication do Azure ou os Serviços de Federação do Active Directory
* Proteger recursos na nuvem e no local com o Servidor Multi-Factor Authentication do Azure

Olá, a tabela seguinte resume a experiência de verificação de Olá entre proteger recursos com o Azure multi-factor Authentication e o AD FS

| Experiência de Verificação - Aplicações baseadas no browser | Experiência de Verificação - Aplicações não baseadas no browser |
|:--- |:--- |:--- |
| Proteger recursos do Azure AD com o Multi-Factor Authentication do Azure |<li>primeiro passo de verificação Olá é efetuado no local utilizando o AD FS.</li> <li>Step-by-Olá segundo passo é um método baseado em telefone efetuado através da autenticação em nuvem.</li> |
| Proteger recursos do Azure AD com os Serviços de Federação do Active Directory |<li>primeiro passo de verificação Olá é efetuado no local utilizando o AD FS.</li><li>Step-by-Olá segundo passo é executado no local honrando a afirmação Olá.</li> |

Advertências com palavras-passe de aplicação para utilizadores federados:

* As palavras-passe da aplicação são verificadas com a autenticação na nuvem, para que possam ignorar a federação. A federação apenas é utilizada ativamente ao definir uma palavra-passe de aplicação.
* As definições de Controlo de Acesso de Cliente no local não são honradas pelas palavras-passe de aplicações.
* Perde a capacidade de registos de autenticação no local para as palavras-passe de aplicações.
* A desativação/eliminação da conta pode demorar horas toothree para sincronização de diretórios, atrasando a desativação/eliminação de palavras-passe de aplicação na identidade de nuvem Olá.

## <a name="next-steps"></a>Passos seguintes
Para informações sobre como configurar o Azure multi-factor Authentication ou Olá Azure multi-factor Authentication Server com o AD FS, consulte Olá seguintes artigos:

* [Proteger recursos da nuvem com o Multi-Factor Authentication do Azure e o AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Proteger recursos na nuvem e no local utilizando o Servidor Multi-Factor Authentication do Azure com o Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Proteger recursos na nuvem e no local utilizando o Servidor Multi-Factor Authentication do Azure com o AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
