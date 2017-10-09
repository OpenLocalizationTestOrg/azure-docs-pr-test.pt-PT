---
title: "Do Azure Active Directory Connect: FAQ – | Microsoft Docs"
description: "Esta página tem perguntas mais frequentes sobre o Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Perguntas mais frequentes sobre Azure Active Directory Connect

## <a name="general-installation"></a>Instalação geral
**P: instalação funcionará se Olá Administrador Global do AD do Azure tiver 2FA ativado?**  
Com Olá compilações de Fevereiro de 2016, isto é suportado.

**P: existe uma forma tooinstall do Azure AD Connect automático?**  
É apenas suportado tooinstall do Azure AD Connect utilizando o Assistente de instalação de Olá. Não é suportada uma instalação automática e silenciosa.

**P: Tenho uma floresta em que um domínio não pode ser contactado. Como instalar o Azure AD Connect?**  
Com Olá compilações de Fevereiro de 2016, isto é suportado.

**P: Olá o trabalho de agente de estado de funcionamento de AD DS no server core?**  
Sim. Depois de instalar o agente de Olá, pode concluir o processo de registo de Olá utilizando Olá seguinte cmdlet do PowerShell: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Rede
**P: Posso tem uma firewall, o dispositivo de rede ou outra coisa que limita a ligações de tempo máximo de Olá pode permanecer aberta na minha rede. Quanto tempo os meus limiar de tempo limite de lado do cliente estará ao utilizar o Azure AD Connect?**  
Todo o software de rede, dispositivos físicos ou há mais alguma coisa que os limites de tempo máximo de Olá ligações podem permanecer abertas deve utilizar um limiar de, pelo menos, 5 minutos (300 segundos) para conetividade entre Olá servidor onde hello do Azure AD Connect cliente está instalado e o Azure Active Directory. Isto também se aplica as ferramentas de sincronização do Microsoft Identity tooall anteriormente lançada.

**P: são SLDs (domínios de etiqueta única) suportada?**  
Não, do Azure AD Connect não suporta local florestas/domínios SLDs a utilizar.

**P: são "separada por pontos" com o nome de NetBios suportado?**  
Não, do Azure AD Connect não suporta florestas/domínios de no local onde o nome de NetBios Olá contenha um ponto final "." no nome de Olá.

## <a name="federation"></a>Federação
**P: o que devo fazer se receber uma mensagem de e-mail que perguntar-me toorenew meu certificado do Office 365**  
Utilize as orientações de Olá que está destacada em Olá [renovar certificados](active-directory-aadconnect-o365-certs.md) tópico sobre como toorenew Olá certificado.

**P: Posso ter "Atualizar automaticamente da entidade confiadora" definido para da entidade confiadora do Office 365. É necessário tootake qualquer ação quando faz o meu automaticamente o certificado de assinatura de token através de?**  
Utilize as orientações de Olá que é descrita no artigo Olá [renovar certificados](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Ambiente
**P: é it suportado toorename Olá servidor após a instalação do Azure AD Connect?**  
Não. Alterar o nome do servidor Olá toonot de motor de sincronização de Olá causa será tooconnect capaz de base de dados SQL de toohello e serviço Olá não será capaz de toostart.

## <a name="identity-data"></a>Dados de identidade
**P: Olá UPN (userPrincipalName) atributo no Azure AD não corresponde ao hello UPN no local - por que motivo?**  
Consulte estes artigos:

* [Olá, os nomes de utilizador no Office 365, Azure ou Intune não correspondem ao UPN no local ou o ID de início de sessão alternativo](https://support.microsoft.com/en-us/kb/2523192)
* [As alterações não são sincronizadas pela ferramenta de sincronização de diretórios do Azure Active Directory Olá depois de alterar Olá UPN de um toouse de conta de utilizador outro domínio federado](https://support.microsoft.com/en-us/kb/2669550)

Também pode configurar userPrincipalName de Olá ao tooupdate do motor de sincronização do Azure AD tooallow Olá conforme descrito em [funcionalidades do serviço de sincronização do Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**P: for it suportado toosoft correspondência no local objetos de AD grupo/contacte com o objetos existentes do grupo/contacte do Azure AD?**  
Não, isto não é atualmente suportado.

**P: é it suportado toomanually definir o atributo de ImmutableId no existente do Azure AD grupo/contacte objetos toohard correspondência tooon local objetos de AD grupo/contacto?**  
Não, isto não é atualmente suportado.



## <a name="custom-configuration"></a>Configuração personalizada
**P: onde estão Olá cmdlets do PowerShell do Azure AD Connect documentado?**  
Com exceção de Olá dos cmdlets de Olá documentados neste site, os outros cmdlets do PowerShell encontrados no Azure AD Connect não são suportados para utilização do cliente.

**P: Posso utilizar "Servidor de exportação/importação do servidor" encontrada no *Synchronization Service Manager* toomove configuração entre servidores?**  
Não. Esta opção não irá obter todas as definições de configuração e não deve ser utilizada. Em vez disso, deve utilizar configuração base do Olá assistente toocreate Olá no segundo servidor de Olá e utilizar Olá sincronização regra editor toogenerate PowerShell scripts toomove qualquer regra personalizada entre servidores. Consulte [Swing migração](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**P: as palavras-passe ser colocadas em cache para a página Olá o início de sessão do Azure e pode isto impedida porque contém um elemento de entrada de palavra-passe com Olá autocomplete = "false" atributo?**</br>
Atualmente não suportamos modificação Olá HTML atributos Olá campo palavra-passe entrado, incluindo a tag de conclusão automática de Olá. Estamos atualmente uma funcionalidade que vai permitir Javascript personalizada que lhe permitirá tooadd qualquer campo de palavra-passe de toohello de atributo. Deve ser posterior disponível parte de 2017.

**P: na página de início de sessão do Azure Olá, são apresentados os nomes de utilizador para os utilizadores que tenham anteriormente sessão iniciada com êxito.  Este comportamento pode ser ativado?**</br>
Atualmente não suportamos atributos HTML Olá modificação da página de início de sessão Olá. Estamos atualmente uma funcionalidade que vai permitir Javascript personalizada que lhe permitirá tooadd qualquer campo de palavra-passe de toohello de atributo. Deve ser posterior disponível parte de 2017.

**P: existe uma forma tooprevent sessões simultâneas?**</br>
Não.



## <a name="troubleshooting"></a>Resolução de problemas
**P: como posso obter ajuda com o Azure AD Connect?**

[Procurar Olá Base de dados de Conhecimento Microsoft (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Procure Olá Base de dados de Conhecimento Microsoft (KB) para problemas de break-fix toocommon soluções técnicas sobre o suporte do Azure AD Connect.

[Fóruns do Microsoft Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Pode pesquisar e navegue para a technical questões e respostas da Comunidade Olá ou peça ao seu próprio pergunta clicando [aqui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Suporte ao cliente do Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Utilize este suporte de tooget ligação através de Olá portal do Azure.

