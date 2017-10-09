---
title: 'O Azure AD Connect: Resolver problemas de conectividade | Microsoft Docs'
description: Explica como problemas de conectividade tootroubleshoot com o Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Resolver problemas de conectividade com o Azure AD Connect
Este artigo explica como funciona a conectividade entre o Azure AD Connect e o Azure AD e como problemas de conectividade tootroubleshoot. Estes problemas são toobe provavelmente visto num ambiente com um servidor proxy.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Resolver problemas de conectividade no Assistente de instalação de Olá
O Azure AD Connect é que utilizam autenticação moderna (utilizando a biblioteca ADAL Olá) para autenticação. Assistente de instalação de Olá e de motor de sincronização de Olá adequada requerem toobe de Machine. config está corretamente configurada, uma vez que estes dois são aplicações de .NET.

Neste artigo, mostramos como Fabrikam liga tooAzure AD através do respetivo proxy. servidor de proxy de Olá é denominado fabrikamproxy e está a utilizar a porta 8080.

Primeiro é preciso toomake se [ **Machine. config** ](active-directory-aadconnect-prerequisites.md#connectivity) está corretamente configurada.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> Em alguns blogues de terceiros, são documentado que devem ser feitas alterações toomiiserver.exe.config em vez disso. No entanto, este ficheiro é substituído em cada atualização, por isso, mesmo se funciona durante a instalação inicial, sistema Olá deixa de funcionar actualização primeiro. Por esse motivo, Olá recomendação é tooupdate config em vez disso.
>
>

servidor de proxy de Olá também tem de ter URLs Olá necessárias abertos. lista de oficial Olá está documentada na [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

URLs, Olá a tabela seguinte é Olá absoluto toobe mínimo bare tooconnect capaz de tooAzure AD de todo. Esta lista não inclui quaisquer funcionalidades opcionais, tais como a repetição de escrita de palavras-passe ou o Azure AD Connect Health. É toohelp aqui documentado na resolução de problemas para a configuração inicial do Olá.

| URL | Porta | Descrição |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Apresenta uma lista de toodownload utilizado CRL. |
| \*. verisign.com |HTTP/80 |Apresenta uma lista de toodownload utilizado CRL. |
| \*. entrust.com |HTTP/80 |Toodownload utilizada listas de CRL para a MFA. |
| \*.windows.net |HTTPS/443 |Toosign utilizado no tooAzure AD. |
| Secure.aadcdn.microsoftonline p.com |HTTPS/443 |Utilizado para a MFA. |
| \*.microsoftonline.com |HTTPS/443 |Utilizado tooconfigure os dados de diretório e importar/exportar do Azure AD. |

## <a name="errors-in-hello-wizard"></a>Erros no Assistente de Olá
Assistente de instalação de Olá está a utilizar dois contextos de segurança diferentes. Na página Olá **ligar tooAzure AD**, está a utilizar Olá tem sessão iniciada no utilizador. Na página Olá **configurar**, está a alterar toohello [conta que executa o serviço de Olá para o motor de sincronização de Olá](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Se existir um problema, é apresentada mais provável já em Olá **ligar tooAzure AD** página no Assistente de Olá, uma vez que a configuração de proxy Olá global.

os seguintes problemas de Olá é erros mais comuns Olá que encontrar no Assistente de instalação de Olá.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>Assistente de instalação de Olá não foi corretamente configurado
Este erro ocorre quando o Assistente de Olá propriamente dito não é possível aceder a proxy Olá.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Se vir este erro, certifique-se Olá [Machine. config](active-directory-aadconnect-prerequisites.md#connectivity) foi configurado corretamente.
* Se o que procura correto, siga os passos de Olá no [verificar a conectividade de proxy](#verify-proxy-connectivity) toosee se o problema de Olá encontra-se fora do Assistente de Olá bem.

### <a name="a-microsoft-account-is-used"></a>É utilizada uma conta Microsoft
Se utilizar um **conta Microsoft** em vez de um **escolares ou organização** conta, verá um erro genérico.  
![É utilizada uma Account da Microsoft](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>Não é possível contactar o ponto final MFA Olá
Este erro ocorre se hello endpoint **https://secure.aadcdn.microsoftonline-p.com** não é possível aceder e o administrador global tiver a MFA ativada.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Se vir este erro, verifique se esse ponto final Olá **secure.aadcdn.microsoftonline p.com** toohello proxy foi adicionado.

### <a name="hello-password-cannot-be-verified"></a>Não é possível verificar a palavra-passe de Olá
Se o Assistente de instalação de Olá for bem sucedido no ligar tooAzure AD, mas a palavra-passe de Olá propriamente dito não é possível verificar a que ver este erro:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* É uma palavra-passe temporária de palavra-passe de Olá e tem de ser alterada? É-Olá, na verdade, palavra-passe correta? Tente toosign no toohttps://login.microsoftonline.com (num computador de outro servidor do Azure AD Connect Olá) e certifique-se de que a conta de Olá é utilizável.

### <a name="verify-proxy-connectivity"></a>Verifique a conectividade do proxy
tooverify se hello servidor do Azure AD Connect tem conectividade real com Olá Proxy e de Internet, utilize algumas toosee PowerShell se o proxy de Olá está a permitir pedidos web ou não. Na linha de comandos do PowerShell, execute `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Tecnicamente hello primeira chamada é toohttps://login.microsoftonline.com e este URI funciona bem, mas hello outro URI toorespond mais rápido.)

PowerShell utiliza a configuração de Olá no proxy de Olá toocontact de Machine. config. definições de Olá no winhttp/netsh não devem afetar estes cmdlets.

Se o proxy de Olá está configurada corretamente, deve obter um Estado de êxito: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Se receber **servidor remoto do tooconnect não é possível toohello**, em seguida, PowerShell está a tentar toomake uma chamada direta sem utilizar o proxy de Olá ou DNS não está corretamente configurado. Certifique-se de que Olá **Machine. config** ficheiro está corretamente configurado.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Se o proxy de Olá não está corretamente configurada, receberá um erro: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Erro | Texto de erro | Comentário |
| --- | --- | --- |
| 403 |Proibido |proxy de Olá não foi aberta para o URL de pedido de Olá. Revê a configuração de proxy Olá e certifique-se de que Olá [URLs](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) tenham sido abertos. |
| 407 |Autenticação de proxy necessária |servidor de proxy de Olá necessário um início de sessão e não foi fornecido nenhum. Se o servidor proxy requer autenticação, certifique-se de que toohave esta definição configurada em Machine. config de Olá. Certifique-se também que estiver a utilizar as contas de domínio para o utilizador Olá a executar o Assistente de Olá e para a conta de serviço Olá. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>padrão de comunicação de Olá entre o Azure AD Connect e o Azure AD
Se seguiu todos estes passos anteriores e ainda não é possível ligar-se, poderá começar neste momento observar os registos de rede. Esta secção é documentar um padrão de conectividade normal e com êxito. -Também é listagem herrings red comuns que pode ser ignorados ao ler a Olá registos de rede.

* Existem toohttps://dc.services.visualstudio.com chamadas. Não é necessário toohave que este URL abrir no proxy Olá para Olá instalação toosucceed e destas chamadas pode ser ignorado.
* Pode ver que a resolução de dns lista Olá real de anfitriões toobe nsatc.net de espaço de nome DNS Olá e outros espaços de nomes não em microsoftonline.com. No entanto, não existem quaisquer pedidos de serviço web nos nomes de servidor real Olá e não tiver tooadd proxy de toohello estes URLs.
* Olá pontos finais adminwebservice provisioningapi fazem pontos finais de deteção e utilizado toofind Olá ponto final real toouse. Estes pontos finais são diferentes consoante a sua região.

### <a name="reference-proxy-logs"></a>Registos de proxy de referência
Eis uma captura de um proxy real registo e Olá instalação página do assistente a partir de onde foi colocado (toohello de entradas duplicadas foram removidas mesmo ponto final). Nesta secção pode ser utilizada como uma referência para os seus próprios registos de proxy e de rede. pontos finais de real Olá poderão ser diferentes no seu ambiente (em particular esses URLs *itálico*).

**Ligar tooAzure AD**

| Hora | URL |
| --- | --- |
| 1/11/2016 8:31 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |ligar: / /*bba800 âncora*. microsoftonline.com:443 |
| 1/11/2016 8:32 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |ligar: / /*bwsc02 reencaminhamento*. microsoftonline.com:443 |

**Configurar**

| Hora | URL |
| --- | --- |
| 1/11/2016 8:43 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |ligar: / /*bba800 âncora*. microsoftonline.com:443 |
| 1/11/2016 8:43 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |ligar: / /*bba900 âncora*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |ligar: / /*bba800 âncora*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |ligar: / /*bwsc02 reencaminhamento*. microsoftonline.com:443 |

**Sincronização inicial**

| Hora | URL |
| --- | --- |
| 1/11/2016 8:48 |Connect://login.Windows.NET:443 |
| 1/11/2016 8:49 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |ligar: / /*bba900 âncora*. microsoftonline.com:443 |
| 1/11/2016 8:49 |ligar: / /*bba800 âncora*. microsoftonline.com:443 |

## <a name="authentication-errors"></a>Erros de autenticação
Esta secção abrange erros que podem ser devolvidos a partir da ADAL (biblioteca de autenticação de Olá utilizada pelo Azure AD Connect) e o PowerShell. Erro de Olá explicado deverá ajudá-lo a compreender os passos seguintes.

### <a name="invalid-grant"></a>Conceder inválido
Nome de utilizador ou palavra-passe inválidos. Para obter mais informações, consulte [não é possível verificar a palavra-passe de Olá](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Tipo de utilizador desconhecido
Diretório do Azure AD não é possível localizar ou resolvido. Talvez tente toologin com um nome de utilizador num domínio não verificado?

### <a name="user-realm-discovery-failed"></a>Falha na deteção de Realm de utilizador
Problemas de configuração de rede ou proxy. Não é possível aceder a rede de Olá. Consulte [resolver problemas de conectividade no Assistente de instalação de Olá](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Palavra-passe do utilizador expirado
As suas credenciais expiraram. Altere a palavra-passe.

### <a name="authorizationfailure"></a>AuthorizationFailure
Problema desconhecido.

### <a name="authentication-cancelled"></a>Autenticação cancelada
desafio de autenticação multifator (MFA) Olá foi cancelado.

### <a name="connecttomsonline"></a>ConnectToMSOnline
A autenticação foi efetuada com êxito, mas o Azure AD PowerShell tiver um problema de autenticação.

### <a name="azurerolemissing"></a>AzureRoleMissing
A autenticação foi efetuada com êxito. Não é um administrador global.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
A autenticação foi efetuada com êxito. Depois de ativar a gestão de identidades privilegiadas e atualmente não é um administrador global. Para obter mais informações, consulte [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
A autenticação foi efetuada com êxito. Não foi possível obter as informações da empresa a partir do Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
A autenticação foi efetuada com êxito. Não foi possível obter as informações do domínio do Azure AD.

### <a name="unexpected-exception"></a>Exceção inesperada
Mostrado como erro inesperado no Assistente de instalação de Olá. Pode ocorrer se tentar toouse um **Account Microsoft** em vez de um **conta profissional ou organização**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Passos de resolução de problemas para as versões anteriores.
Com as versões começando com o número de compilação 1.1.105.0 (lançadas Fevereiro de 2016), o Assistente de início de sessão Olá foi extinguido. Esta configuração de secção e Olá já não deve ser necessária, mas é mantida como referência.

Para Olá início de sessão único no assistente toowork, winhttp tem de ser configurado. Esta configuração pode ser feita com [ **netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Assistente de início de sessão Olá não foi corretamente configurada
Este erro ocorre quando o Assistente de início de sessão Olá é possível alcançar o proxy de Olá ou proxy Olá não está a permitir o pedido de Olá.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Se vir este erro, consulte Configuração do proxy de Olá no [netsh](active-directory-aadconnect-prerequisites.md#connectivity) e certifique-se de que está correto.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Se o que procura correto, siga os passos de Olá no [verificar a conectividade de proxy](#verify-proxy-connectivity) toosee se o problema de Olá encontra-se fora do Assistente de Olá bem.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
