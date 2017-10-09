---
title: "ocorre no aaaConnect dispositivos associados a domínios tooAzure AD para o Windows 10 | Microsoft Docs"
description: "Explica como os administradores podem configurar a rede empresarial de associados a um domínio toohello toobe política de grupo tooenable dispositivos."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10
Associação a um domínio é que as organizações de forma tradicional Olá ligou dispositivos for work para Olá últimos 15 anos e muito mais. Ativou toosign de utilizadores nos dispositivos tootheir utilizando o respetivo trabalho do Windows Server Active Directory (Active Directory) ou contas profissional e permitido IT toofully gerirem estes dispositivos. As organizações dependem normalmente imaging métodos tooprovision dispositivos toousers e geralmente, utilizar o System Center Configuration Manager (SCCM) ou de política de grupo toomanage-los.


Associação a um domínio no Windows 10 fornece-lhe Olá depois de ligar dispositivos tooAzure do Active Directory (Azure AD) os seguintes benefícios:

* Único início de sessão (SSO) tooAzure AD recursos a partir de qualquer lugar
* Aceder à empresa toohello loja Windows através da utilização de trabalho ou escola contas (não existe nenhuma conta Microsoft necessária)
* Empresarial compatível roaming de definições de utilizador em todos os dispositivos através da utilização de contas profissionais ou escolares (não existe nenhuma conta Microsoft necessária)
* Autenticação forte e conveniente início de sessão para contas profissionais ou escolares com o Windows Hello para empresas e o Windows Hello
* Capacidade toorestrict aceder apenas toodevices que estão em conformidade com as definições de política de grupo organizacional do dispositivo

## <a name="prerequisites"></a>Pré-requisitos
Associação a um domínio continua toobe útil. No entanto, tooget vantagens de Olá do Azure AD do SSO, roaming das definições com ou escola contas e aceder à loja de tooWindows com trabalho profissional ou escolar contas, é necessário Olá seguintes:

* Subscrição do Azure AD
* Azure AD Connect tooextend Olá no local diretório tooAzure AD
* Política de que definiu tooconnect dispositivos associados a domínios tooAzure AD
* Compilação do Windows 10 (compilação 10551 ou mais recente) para dispositivos

tooenable Windows Hello para empresas e o Windows Hello, também terá de seguinte Olá:

- **Infraestrutura de chaves públicas (PKI)** para emissão de certificados de utilizador.

- **System Center Configuration Manager Current Branch** -terá tooinstall versão 1606 ou melhor.  
Para obter mais informações, consulte: 
    - [Documentação do System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blogue da equipa do System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Windows Hello para definições da empresa no System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Como um requisito de implementação de PKI toohello alternativa, pode fazê-lo seguinte Olá:

* Ter alguns controladores de domínio com o Windows Server 2016 Active Directory Domain Services.

acesso condicional tooenable, pode criar definições de política de grupo que permitem o acesso a dispositivos associados a toodomain com sem implementações adicionais. controlo de acesso de toomanage com base na conformidade de dispositivo Olá, terá de seguinte Olá:

* System Center Configuration Manager Current Branch (1606 ou posterior) para Windows Hello para cenários de negócios

## <a name="deployment-instructions"></a>Instruções de implementação

toodeploy, siga passos de Olá apresentados na [como tooconfigure o registo automático do Windows associados a um domínio dispositivos com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Passo seguinte
* [Windows 10 para empresa Olá: dispositivos de toouse formas de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Expandir nuvem dispositivos de tooWindows 10 capacidades através da associação do Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Saiba mais sobre os cenários de utilização da Associação do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Associação do Azure AD](active-directory-azureadjoin-setup.md)

