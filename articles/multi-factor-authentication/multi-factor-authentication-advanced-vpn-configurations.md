---
title: "cenários de aaaAdvanced MFA do Azure e VPNs de terceiros"
description: "Guias de configuração passo a passo para toointegrate de MFA do Azure com o Cisco, Citrix e Juniper."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Cenários avançados com multi-factor Authentication do Azure e soluções VPN de terceiros
Multi-factor Authentication do Azure podem ser utilizado tooseamlessly ligar com várias soluções VPN de terceiros. Este artigo incida no dispositivo de VPN do Cisco® ASA, aplicação Citrix NetScaler SSL VPN e Olá Juniper redes proteger o acesso/Pulse Secure ligar seguro SSL dispositivo de VPN. Criámos tooaddress de guias de configuração estes três aplicações comuns, mas o servidor multi-factor Authentication pode integrar com a maior parte dos sistemas que utilizam o RADIUS, o LDAP, o IIS ou autenticação baseada em afirmações tooAD FS. Pode encontrar mais detalhes em [configurações de servidor MFA](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Dispositivo de VPN do ASA da Cisco e a multi-factor Authentication do Azure
Multi-factor Authentication do Azure integra-se a sua® de Cisco ASA VPN aplicação tooprovide adicional de segurança para inícios de sessão do Cisco AnyConnect® VPN e acesso ao portal.  Isto pode ser feito utilizando qualquer um dos Olá protocolo RADIUS ou LDAP.  Selecione uma das Olá seguir configuração passo a passo detalhadas toodownload Olá orienta.

| Guia de configuração | Descrição |
| --- | --- |
| [Cisco ASA com Anyconnect VPN e o Azure MFA de configuração para o LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Integrar o seu dispositivo de Cisco ASA VPN com a MFA do Azure através de LDAP |
| [Cisco ASA com a configuração de MFA Anyconnect VPN e o Azure para RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Integrar o seu dispositivo de Cisco ASA VPN com a MFA do Azure com o RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>Citrix NetScaler SSL VPN e o Azure multi-factor Authentication
Multi-factor Authentication do Azure integra-se a sua Citrix NetScaler SSL VPN aplicação tooprovide adicional de segurança para inícios de sessão do Citrix NetScaler SSL VPN e acesso ao portal.  Isto pode ser feito utilizando qualquer um dos Olá protocolo RADIUS ou LDAP.  Selecione uma das Olá seguir configuração passo a passo detalhadas toodownload Olá orienta.

| Guia de configuração | Descrição |
| --- | --- |
| [Citrix NetScaler SSL VPN e o Azure MFA de configuração para o LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Integrar a VPN do Citrix NetScaler SSL com o dispositivo de MFA do Azure através de LDAP |
| [Configuração de MFA de VPN do Citrix NetScaler SSL e o Azure para RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Integrar o seu dispositivo de VPN do Citrix NetScaler SSL com a MFA do Azure com o RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Dispositivo de VPN do Juniper/Pulse Secure SSL e o Azure multi-factor Authentication
Multi-factor Authentication do Azure integra-se a sua Juniper/Pulse Secure SSL VPN aplicação tooprovide adicional de segurança para inícios de sessão Juniper/Pulse Secure SSL VPN e acesso ao portal.  Isto pode ser feito utilizando qualquer um dos Olá protocolo RADIUS ou LDAP.  Selecione uma das Olá seguir configuração passo a passo detalhadas toodownload Olá orienta.

| Guia de configuração | Descrição |
| --- | --- |
| [Juniper/Pulse Secure de VPN SSL e o Azure MFA de configuração para o LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Integrar o Juniper/Pulse Secure de VPN SSL com o dispositivo de MFA do Azure através de LDAP |
| [Configuração de MFA Juniper/Pulse Secure de VPN SSL e o Azure para RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Integrar o seu dispositivo Juniper/Pulse Secure SSL VPN com a MFA do Azure com o RADIUS |

## <a name="next-steps"></a>Passos seguintes

- [Aumentar a sua infraestrutura de autenticação existente com Olá extensão NPS para o multi-factor Authentication do Azure](multi-factor-authentication-nps-extension.md)

- [Configurar Definições do Multi-Factor Authentication do Azure](multi-factor-authentication-whats-next.md)