---
title: "aaaAccess Cofre de chaves atrás de uma firewall | Microsoft Docs"
description: "Saiba como tooaccess chave do Azure do cofre a partir de uma aplicação atrás de uma firewall"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Aceder ao Cofre de Chaves do Azure protegido por firewall
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>P: a minha aplicação de cliente do Cofre de chaves tem toobe atrás de uma firewall. As portas, anfitriões ou IP endereços deve abro Cofre de chaves tooenable acesso tooa?
tooaccess um cofre de chaves, a aplicação de cliente do Cofre de chaves tem tooaccess vários pontos finais para várias funcionalidades:

* Autenticação através do Azure Active Directory (Azure AD).
* Gestão do Cofre de Chaves do Azure. Isto inclui criar, ler, atualizar, eliminar e definir políticas de acesso através do Azure Resource Manager.
* Aceder e gerir objetos (chaves e segredos) armazenados no Cofre de chaves em si, passar Olá endpoint específicos de Cofre de chave (por exemplo, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Dependendo da configuração e do ambiente, existem algumas variações.   

## <a name="ports"></a>Portas
Todos os tráfego tooa Cofre de chaves para todos os três funções (autenticação, gestão e dados acesso plane) passa através de HTTPS: porta 443. No entanto, existirá ocasionalmente tráfego HTTP (porta 80) para CRL. Os clientes que suportem OCSP, não devem atingir o CRL, mas, ocasionalmente, poderão alcançar [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Autenticação
Aplicações de cliente do Cofre de chaves serão necessário tooaccess pontos finais do Azure Active Directory para autenticação. ponto final de Olá utilizado depende Olá configuração de inquilinos do Azure AD, o tipo de Olá de principal (principal de utilizador ou principal de serviço) e Olá tipo de conta – por exemplo, uma conta Microsoft ou de um trabalho conta escolar ou profissional.  

| Tipo de principal | Ponto final:porta |
| --- | --- |
| Utilizador com conta Microsoft<br> (por exemplo, user@hotmail.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure US Government:**<br> login-us.microsoftonline.com:443<br><br>**Azure Alemanha:**<br> login.microsoftonline.de:443<br><br> e <br>login.live.com:443 |
| Utilizador ou principal de serviço com uma conta escolar ou profissional com o Azure AD (por exemplo, user@contoso.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure US Government:**<br> login-us.microsoftonline.com:443<br><br>**Azure Alemanha:**<br> login.microsoftonline.de:443 |
| Utilizador ou principal de serviço com um ou conta profissional, e os serviços de Federação do Active Directory (AD FS) ou outro ponto final da Federado (por exemplo, user@contoso.com) |Todos os pontos finais para uma conta escolar ou profissional, mais AD FS ou outros pontos finais federados |

Existem outros cenários possíveis complexos. Consulte demasiado[do Azure Active Directory Authentication fluxo](/documentation/articles/active-directory-authentication-scenarios/), [integrar aplicações com o Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), e [protocolos de autenticação do Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Para obter informações adicionais.  

## <a name="key-vault-management"></a>Gestão do Cofre de Chaves
Para a gestão de Cofre de chaves (CRUD e definição de política de acesso), a aplicação de cliente do Cofre de chaves Olá tem tooaccess um ponto final do Azure Resource Manager.  

| Tipo de operação | Ponto final:porta |
| --- | --- |
| Operações do painel de controlo do Cofre de Chaves<br> através do Azure Resource Manager |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure US Government:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> management.microsoftazure.de:443 |
| Graph API do Azure Active Directory |**Global:**<br> graph.windows.net:443<br><br> **Azure China:**<br> graph.chinacloudapi.cn:443<br><br> **Azure US Government:**<br> graph.windows.net:443<br><br> **Azure Alemanha:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Operações do Cofre de Chaves
Para todos os gestão de objeto (chaves e segredos) do Cofre de chaves e operações de criptografia, o cliente do Cofre de chaves de Olá tem ponto final do tooaccess Olá Cofre de chaves. sufixo DNS do ponto final de Olá varia dependendo da localização de Olá do seu Cofre de chaves. ponto final do Cofre de chaves de Olá tem um formato Olá *nome do cofre*. *região---o sufixo dns específico*, conforme descrito nas Olá a tabela seguinte.  

| Tipo de operação | Ponto final:porta |
| --- | --- |
| Operações, incluindo operações criptográficas em chaves; criar, ler, atualizar e eliminar chaves e segredos; definir ou obter etiquetas e outros atributos de objetos de cofre de chaves (chaves ou segredos) |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure US Government:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Intervalos de endereços IP
Olá serviço Cofre de chaves utiliza outros recursos do Azure, como a infraestrutura de PaaS. Para que não seja possível tooprovide um específico intervalo de endereços IP que o Cofre de chaves tem pontos finais do serviço em qualquer altura específica. Se a firewall suporta apenas os intervalos de endereços IP, consulte toohello [intervalos de IP de centro de dados do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653) documento. Para autenticação e identidade (Azure Active Directory), a aplicação tem de ser pontos finais de toohello tooconnect capaz de descrito [endereços de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Passos seguintes
Se tiver dúvidas sobre o Cofre de chaves, visite Olá [nos fóruns do Cofre de chaves do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

