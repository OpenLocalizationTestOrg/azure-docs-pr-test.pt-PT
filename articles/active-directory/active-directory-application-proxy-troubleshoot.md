---
title: "aaaTroubleshoot Proxy de aplicações | Microsoft Docs"
description: "Abrange como tootroubleshoot erros no Proxy de aplicações do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Resolver problemas de Proxy de aplicações e as mensagens de erro
Se ocorrerem erros ao aceder a uma aplicação publicada ou numa publicação de aplicações, verifique Olá seguir toosee opções, se o Proxy de aplicações do Microsoft Azure AD está a funcionar corretamente:

* Serviços do Windows hello abrir consola e certifique-se de que Olá **conector do Proxy de aplicações do Microsoft AAD** serviço está ativado e em execução. Também poderá toolook na página de propriedades de serviço de Proxy da aplicação Olá, conforme mostrado no Olá seguinte imagem:  
  ![Captura de ecrã de janela de propriedades de conector do Proxy de aplicações do Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Abra o Visualizador de eventos e procure eventos do conector de Proxy de aplicações no **registos de serviços e aplicações** > **Microsoft** > **AadApplicationProxy** > **conector** > **Admin**.
* Se for necessário, registos mais detalhados estão disponíveis por [ativar Olá registos de sessão do conector de Proxy de aplicações](application-proxy-understand-connectors.md#under-the-hood).

Para obter mais informações sobre a ferramenta de resolução de problemas de Olá do Azure AD, consulte [ferramenta toovalidate conector rede pré-requisitos de resolução de problemas](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>página Olá não é composta corretamente
Poderá ter problemas com a sua aplicação de composição ou está a funcionar incorretamente sem receber mensagens de erro específicas. Isto pode ocorrer se publicou o caminho de artigo Olá, mas Olá aplicação requer o conteúdo que existe fora nesse caminho.

Por exemplo, se publicar Olá caminho https://yourapp/app mas aplicação Olá chama imagens em https://yourapp/media, podem não ser compostos. Certifique-se de que pode publicar a aplicação Olá utilizando Olá de caminho nível mais elevado terá tooinclude todo o conteúdo relevante. Neste exemplo, seria possível http://yourapp/.

Se alterar o conteúdo do caminho tooinclude referenciada, mas continua a precisar tooland de utilizadores de uma ligação de mais profunda no caminho de Olá, consulte a mensagem de blogue de Olá [ligação de direita de Olá de definição para aplicações de Proxy de aplicações no painel de acesso de Olá do Azure AD e a aplicação do Office 365 iniciador](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Erros de conector

Olá utilize [do Azure AD aplicação Proxy portas teste ferramenta do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que o conector pode contactar o serviço de Proxy da aplicação Olá. No mínimo, certifique-se de que a região EUA Central de Olá e Olá região mais próxima tooyou têm todas as marcas de verificação verdes. Para além disso, as marcas de verificação verde mais significa maior resiliência. 

Se o registo falhar durante a instalação de assistente do conector de Olá, existem duas formas tooview motivo Olá falha Olá. O procure no registo de eventos de Olá em **aplicações e serviços Logs\Microsoft\AadApplicationProxy\Connector\Admin**, ou Olá executar seguinte comando do Windows PowerShell:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Depois de localizar o erro de conector Olá do registo de eventos de Olá, utilize esta tabela de problema de Olá de tooresolve erros comuns:

| Erro | Passos recomendados |
| ----- | ----------------- |
| Falha no registo do conector: Certifique-se de que ativou o Proxy de aplicações no Olá Azure Management Portal e que introduziu corretamente o nome de utilizador do Active Directory e a palavra-passe. Erro: 'ocorreram um ou mais erros.' | Se tiver fechado janela de registo Olá sem iniciar sessão no tooAzure AD, execute novamente o Assistente do conector Olá e registe Olá conector. <br><br> Se a janela de registo de Olá abre e, em seguida, fecha imediatamente sem permitindo-lhe toolog no, provavelmente, irá obter este erro. Este erro ocorre quando existe um erro de rede no seu sistema. Certifique-se de que é possível tooconnect do browser tooa Web site público e que as portas de Olá estão abertas conforme especificado no [pré-requisitos do Proxy de aplicações](active-directory-application-proxy-enable.md). |
| Limpar erro é apresentado na janela de registo Olá. Não é possível continuar | Se vir este erro e, em seguida, fecha a janela de Olá, introduziu errado Olá de nome de utilizador ou palavra-passe. Tente novamente. |
| Falha no registo do conector: Certifique-se de que ativou o Proxy de aplicações no Olá Azure Management Portal e que introduziu corretamente o nome de utilizador do Active Directory e a palavra-passe. Erro: ' AADSTS50059: não existem informações de identificação de inquilino encontradas o pedido de Olá ou implícito por qualquer fornecido as credenciais e pesquisa por serviço principal URI falhou. | Está a tentar toosign utilizando uma Account Microsoft e não um domínio que faz parte do ID de organização Olá do diretório de Olá que está a tentar tooaccess. Certifique-se de que o administrador Olá faz parte de Olá mesmo nome de domínio como Olá domínio de inquilino, por exemplo, se o domínio de Olá do Azure AD for contoso.com, Olá, admin deve ser admin@contoso.com. |
| Falha na política de execução de atual de Olá do tooretrieve para executar scripts do PowerShell. | Se Olá instalação do conector falhar, verifique toomake certificar-se de que a política de execução do PowerShell não está desativada. <br><br>1. Abra Olá Editor de políticas de grupo.<br>2. Aceda demasiado**configuração do computador** > **modelos administrativos** > **componentes do Windows**  >   **Windows PowerShell** e faça duplo clique **ativar a execução do Script**.<br>3. política de execução de Olá pode ser definida tooeither **não configurado** ou **ativado**. Se definido demasiado**ativado**, certifique-se de que em Opções, Olá política de execução é definida tooeither **permitir scripts locais e remotos scripts assinados** ou demasiado**permitir todos os scripts**. |
| Configuração de Olá toodownload falha do conector. | certificado de cliente do conector de Olá, que é utilizado para autenticação, expirou. Isto pode também ocorrer se tiver Olá que conector instalado atrás de um proxy. Neste caso, Olá conector não é possível aceder Olá Internet e não será capaz de tooprovide aplicações tooremote utilizadores. Renovar a confiança manualmente utilizando Olá `Register-AppProxyConnector` cmdlet no Windows PowerShell. Se o seu conector estiver atrás de um proxy, é necessário toogrant Internet toohello conector as contas de acesso "serviços de rede" e "sistema local." Isto pode ser conseguido, concedendo-lhes aceder toohello Proxy ou definindo-los toobypass Olá proxy. |
| Falha no registo do conector: Certifique-se de que um Administrador Global do seu Olá tooregister de Active Directory Connector. Erro: ' Olá registo requisição foi negada.' | alias de Olá que está a tentar toolog com não é administrador neste domínio. O conector é sempre instalado para o diretório de Olá que pertence o domínio do utilizador Olá. Certifique-se de que a conta de administrador de Olá que está a tentar toosign com tem inquilino toohello do Azure AD de permissões global. |

## <a name="kerberos-errors"></a>Erros de Kerberos

Esta tabela aborda Olá mais comum erros que vêm da configuração de Kerberos e a configuração e incluem sugestões para resolução.

| Erro | Passos recomendados |
| ----- | ----------------- |
| Falha na política de execução de atual de Olá do tooretrieve para executar scripts do PowerShell. | Se Olá instalação do conector falhar, verifique toomake certificar-se de que a política de execução do PowerShell não está desativada.<br><br>1. Abra Olá Editor de políticas de grupo.<br>2. Aceda demasiado**configuração do computador** > **modelos administrativos** > **componentes do Windows**  >   **Windows PowerShell** e faça duplo clique **ativar a execução do Script**.<br>3. política de execução de Olá pode ser definida tooeither **não configurado** ou **ativado**. Se definido demasiado**ativado**, certifique-se de que em Opções, Olá política de execução é definida tooeither **permitir scripts locais e remotos scripts assinados** ou demasiado**permitir todos os scripts**. |
| 12008 - as do azure AD excedido Olá número máximo de autenticação do Kerberos permitido tenta toohello servidor de back-end. | Este erro pode indicar uma configuração incorreta entre o Azure AD e Olá back-end servidor de aplicações, ou um problema na configuração de data e hora em ambas as máquinas. servidor de back-end Olá recusado permissão de Kerberos Olá criado pelo Azure AD. Certifique-se de que o Azure AD e o servidor de aplicação de back-end Olá estão configuradas corretamente. Certifique-se de que a configuração a hora e data Olá no Olá do Azure AD e o servidor de aplicação de back-end de Olá estão sincronizadas. |
| 13016 - as do azure AD não é possível obter uma permissão de Kerberos em nome de utilizador de Olá porque não existe nenhum UPN no edge Olá token ou no cookie de acesso de Olá. | Não há um problema com a configuração de STS Olá. Corrija Olá de afirmação UPN configuração Olá STS. |
| 13019 - as do azure AD não é possível obter uma permissão de Kerberos em nome de utilizador de Olá devido ao seguinte erro geral de API de Olá. | Este evento pode indicar uma configuração incorreta entre o Azure AD e servidor de controlador de domínio Olá, ou um problema na configuração de data e hora em ambas as máquinas. controlador de domínio Olá recusado permissão de Kerberos Olá criado pelo Azure AD. Certifique-se de que o Azure AD e o servidor de aplicação de back-end Olá estão configurados corretamente, especialmente Olá SPN configuração. Certifique-se Olá do Azure AD está associado a um domínio toohello mesmo domínio como Olá tooensure de controlador de domínio que o controlador de domínio de Olá estabelece a fidedignidade com o Azure AD. Certifique-se de que a configuração a hora e data Olá no Olá do Azure AD e o controlador de domínio de Olá estão sincronizadas. |
| 13020 - as do azure AD não é possível obter uma permissão de Kerberos em nome de utilizador de Olá porque o servidor de back-end de Olá SPN não está definido. | Este evento pode indicar uma configuração incorreta entre o Azure AD e servidor de controlador de domínio Olá, ou um problema na configuração de data e hora em ambas as máquinas. controlador de domínio Olá recusado permissão de Kerberos Olá criado pelo Azure AD. Certifique-se de que o Azure AD e o servidor de aplicação de back-end Olá estão configurados corretamente, especialmente Olá SPN configuração. Certifique-se Olá do Azure AD está associado a um domínio toohello mesmo domínio como Olá tooensure de controlador de domínio que o controlador de domínio de Olá estabelece a fidedignidade com o Azure AD. Certifique-se de que a configuração a hora e data Olá no Olá do Azure AD e o controlador de domínio de Olá estão sincronizadas. |
| 13022 - as do azure AD não consegue autenticar o utilizador de Olá porque o servidor de back-end Olá responde tooKerberos tentativas de autenticação com um erro de HTTP 401. | Este evento pode indicar uma configuração incorreta entre o Azure AD e Olá back-end servidor de aplicações, ou um problema na configuração de data e hora em ambas as máquinas. servidor de back-end Olá recusado permissão de Kerberos Olá criado pelo Azure AD. Certifique-se de que o Azure AD e o servidor de aplicação de back-end Olá estão configuradas corretamente. Certifique-se de que a configuração a hora e data Olá no Olá do Azure AD e o servidor de aplicação de back-end de Olá estão sincronizadas. |

## <a name="end-user-errors"></a>Erros de utilizador final

Esta lista inclui os erros que os utilizadores finais podem surgir quando tentar tooaccess Olá aplicação e falhar. 

| Erro | Passos recomendados |
| ----- | ----------------- |
| Web site de Olá não é possível apresentar a página Olá. | O utilizador pode obter este erro quando tenta tooaccess Olá aplicação publicada se Olá aplicação é uma aplicação de IWA. Olá definido SPN para esta aplicação pode estar incorreta. Para aplicações IWA, certifique-se de que Olá SPN configurada para esta aplicação está correto. |
| Web site de Olá não é possível apresentar a página Olá. | O utilizador pode obter este erro quando tenta tooaccess Olá aplicação publicados se a aplicação de Olá é uma aplicação do OWA. Isto pode ser causado por um dos seguintes Olá:<br><li>Olá definido SPN para esta aplicação está incorreta. Certifique-se de que Olá SPN configurada para esta aplicação está correto.</li><li>Olá utilizador tentou a aplicação de Olá tooaccess está a utilizar uma conta Microsoft em vez de Olá toosign de conta empresarial adequada no, ou utilizador Olá é um utilizador convidado. Disponibilizar se Olá utilizador inicia sessão utilizando a respetiva conta empresarial, que corresponde ao hello domínio de Olá publicado a aplicação. Os utilizadores da Microsoft Account e de convidado não é possível aceder a aplicações de IWA.</li><li>Olá utilizador tentou a aplicação de Olá tooaccess não está definido corretamente para esta aplicação no lado do Olá no local. Certifique-se de que este utilizador tem permissões adequadas Olá, tal como definido para esta aplicação de back-end na máquina no local de Olá. |
| Não é possível aceder esta aplicação empresarial. São tooaccess não autorizados esta aplicação. Falha de autorização. Certifique-se de que utilizador de Olá tooassign com a aplicação de toothis de acesso. | Os utilizadores poderão obter este erro quando tenta tooaccess Olá aplicação publicada se utilizarem contas Microsoft, em vez dos respetivos toosign de conta empresarial no. Os utilizadores convidados também poderão obter este erro. Os utilizadores da Microsoft Account e nos convidados não podem aceder a aplicações IWA. Disponibilizar se Olá utilizador inicia sessão utilizando a respetiva conta empresarial, que corresponde ao hello domínio de Olá publicado a aplicação.<br><br>Poderá não ter atribuído utilizador Olá para esta aplicação. Aceda toohello **aplicação** separador e, em **utilizadores e grupos**, atribua este utilizador ou a aplicação de toothis de grupo do utilizador. |
| Esta aplicação empresarial não pode ser acedida neste momento. Tente novamente mais tarde... conector Olá ultrapassou o tempo limite. | Os utilizadores poderão obter este erro quando tenta tooaccess Olá aplicação publicada se não estão corretamente definidos para esta aplicação no lado do Olá no local. Certifique-se de que os utilizadores têm permissões adequadas Olá, tal como definido para esta aplicação de back-end na máquina no local de Olá. |
| Não é possível aceder esta aplicação empresarial. São tooaccess não autorizados esta aplicação. Falha de autorização. Certifique-se de que o utilizador Olá tenha uma licença para o Azure Active Directory Premium ou Basic. | Os utilizadores poderão obter este erro quando tenta tooaccess Olá aplicação publicada se não foram atribuídos explicitamente com uma licença de Premium/básica pelo administrador do subscritor Olá. Aceda do Active Directory do subscritor toohello **licenças** separador e certifique-se de que este utilizador ou grupo de utilizadores é atribuído uma licença Premium ou Basic. |

## <a name="my-error-wasnt-listed-here"></a>A minha erro não listado aqui

Se ocorrer um erro ou problema com o Proxy da aplicação AD do Azure que não está listado neste guia de resolução de problemas, gostaríamos toohear acerca do mesmo. Enviar um e-mail tooour [equipa comentários](mailto:aadapfeedback@microsoft.com) com Olá os detalhes do erro Olá que encontrou.

## <a name="see-also"></a>Consultar também
* [Ativar o Proxy de aplicações do Azure Active Directory](active-directory-application-proxy-enable.md)
* [Publicar aplicações com o Proxy de aplicações](active-directory-application-proxy-publish.md)
* [Ativar o início de sessão único](active-directory-application-proxy-sso-using-kcd.md)
* [Ativar o acesso condicional](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
