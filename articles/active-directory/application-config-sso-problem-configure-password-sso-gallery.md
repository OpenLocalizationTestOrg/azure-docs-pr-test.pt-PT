---
title: "aaaProblem configurar palavra-passe-início de sessão único para uma aplicação de galeria do Azure AD | Microsoft Docs"
description: "Compreender a letra de pessoas de problemas comuns Olá quando configurar a palavra-passe-início de sessão único para aplicações que já estão listadas no Olá Galeria de aplicações do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problema de configuração de palavra-passe-início de sessão único para uma aplicação de galeria do Azure AD

Este artigo ajudá-lo toounderstand Olá comuns problemas pessoas enfrentam reside quando configurar **palavra-passe-início de sessão único** com uma aplicação de galeria do Azure AD.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>As credenciais são preenchidas, mas a extensão de Olá não submetê-las

Normalmente, isto acontece se o fornecedor da aplicação Olá foi alterado o início de sessão recentemente página tooadd um campo, alterar um identificador subjacente utilizámos toodetect de campos de nome de utilizador e palavra-passe de Olá ou modificar como início de sessão Olá experiência funciona para a respetiva aplicação. Felizmente, em muitos casos, Microsoft pode trabalhar com aplicações fornecedores toorapidly resolva estes problemas.

Embora a Microsoft tem tooautomatically tecnologias detetar quando estes integrações interromper, mas por vezes, mas não é possível toofind estes problemas direito away ou demorar algum tempo toofix. No caso de Olá quando um destes integrações não funcione corretamente, agradecemos se tiver aberto um incidente de suporte para que possamos corrigi-lo mais rapidamente possível.

Na adição toothis, **se forem in contact with fornecedor desta aplicação,** **envie-os nossa forma** para que possa trabalhar com os mesmos toonatively integrar a sua aplicação no Azure Active Directory. Pode enviar Olá fornecedor toohello [listar a aplicação na Galeria de aplicações do Azure Active Directory Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los foi iniciadas.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>As credenciais estão preenchidas e submetidas, mas a página Olá indica Olá credenciais estão incorretas

tooresolve este problema, primeiro seguinte de Olá de verificação:

-   Possui utilizador de Olá primeiro tente demasiado**inicie sessão no Web site de aplicação toohello diretamente** com as credenciais de Olá armazenadas para os mesmos.

  * Se funciona, em seguida, ter utilizador Olá, clique em Olá **atualizar as credenciais** botão Olá **aplicação mosaico** no Olá **aplicações** secção Olá [aplicação Aceder ao painel](https://myapps.microsoft.com/) tooupdate-los toohello conhecida mais recentes a funcionar de nome de utilizador e palavra-passe.

   * Se lhe ou outro credenciais de Olá de administrador atribuída para este utilizador, Localizar utilizador Olá ou a atribuição do grupo de aplicações, navegando toohello **utilizadores e grupos** separador da aplicação Olá, selecionando a atribuição de Olá e ao clicar em Olá **credenciais de atualização** botão.

-   Se o utilizador Olá atribuídas as suas próprias credenciais, ter utilizador Olá **verifique toobe certificar-se de que a palavra-passe expirou não numa aplicação Olá** e se assim for, **atualizar a palavra-passe expirada** ao iniciar sessão toohello aplicação diretamente.

   * Depois de palavra-passe de Olá tiver sido atualizado na aplicação Olá, pedir Olá do Olá utilizador tooclick **atualizar as credenciais** botão Olá **aplicação mosaico** no Olá **aplicações** secção de Olá [painel de acesso de aplicação](https://myapps.microsoft.com/) tooupdate-los toohello conhecida mais recentes a funcionar de nome de utilizador e palavra-passe.

   * Se lhe ou outro credenciais de Olá de administrador atribuída para este utilizador, Localizar utilizador Olá ou a atribuição do grupo de aplicações, navegando toohello **utilizadores e grupos** separador da aplicação Olá, selecionando a atribuição de Olá e ao clicar em Olá **credenciais de atualização** botão.

-   Tem a extensão de browser ao painel do acesso de Olá Olá utilizador atualização seguindo os passos Olá abaixo Olá [como tooinstall Olá extensão de Browser do painel de acesso](#how-to-install-the-access-panel-browser-extension) secção.

-   Certifique-se de que a extensão de browser de painel de acesso de Olá está em execução e ativado no browser do utilizador.

-   Certifique-se de que os utilizadores não estão a tentar toosign na aplicação toohello do painel de acesso de Olá no **modo privado, inPrivate ou incognito**. extensão de painel de acesso de Olá não é suportada nestes modos.

No caso de este não funciona, poderia ser caso Olá que tiver ocorrido uma alteração no lado de aplicação Olá que temporariamente tem quebrada integração da aplicação Olá com o Azure AD. Por exemplo, isto pode ocorrer quando o fornecedor da aplicação Olá introduz um script na respetiva página que funciona de forma diferente para manuais vs automatizada de entrada, o que faz com que a atribuição de integração, como o nosso própria, toobreak. Felizmente, em muitos casos, Microsoft pode trabalhar com aplicações fornecedores toorapidly resolva estes problemas.

Embora a Microsoft tem tooautomatically tecnologias detetar quando estes integrações interromper, mas por vezes, mas não é possível toofind estes problemas direito away ou demorar algum tempo toofix. No caso de Olá quando um destes integrações não funcione corretamente, agradecemos se tiver aberto um incidente de suporte para que possamos corrigi-lo mais rapidamente possível.

Na adição toothis, **se forem in contact with fornecedor desta aplicação,** **envie-os nossa forma** para que possa trabalhar com os mesmos toonatively integrar a sua aplicação no Azure Active Directory. Pode enviar Olá fornecedor toohello [listar a aplicação na Galeria de aplicações do Azure Active Directory Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los foi iniciadas.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>extensão de Olá funciona no Chrome e Firefox, mas não no Internet Explorer

Existem duas causas principais toothis problema:

-   Dependendo das definições de segurança de Olá ativadas no Internet Explorer, se o Web site de Olá não é parte de um **zona fidedigna**, por vezes, nosso script ser impedidos de execução para a aplicação Olá.

  *  tooresolve, instruir o utilizador Olá demasiado**adicionar Web site da aplicação Olá** toohello **Sites fidedignos** lista dentro do respetivo **definições de segurança do Internet Explorer**. Pode enviar o toohello utilizadores [como tooadd toomy um site fidedigno sites lista](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) artigo para obter instruções detalhadas.

-   Em circunstâncias raras, validação de segurança do Internet Explorer pode, por vezes, originar tooload de página Olá mais lentamente do que a execução de Olá do nosso script.

   * Infelizmente, esta situação pode variar consoante a versão do browser Olá, velocidade do computador ou site visitada. Neste caso, sugerimos que contacte o suporte para que possamos corrigir integração Olá para esta aplicação específica.

Na adição toothis, **se forem in contact with fornecedor desta aplicação,** **envie-os nossa forma** para que possa trabalhar com os mesmos toonatively integrar a sua aplicação no Azure Active Directory. Pode enviar Olá fornecedor toohello [listar a aplicação na Galeria de aplicações do Azure Active Directory Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los foi iniciadas.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Verifique se hello página de início de sessão da aplicação foi recentemente alterada ou necessita de um campo adicional

Se a página de início de sessão da aplicação Olá mudou significativamente, por vezes, isto faz com que a nossa toobreak integrações. Um exemplo desta situação é quando um fornecedor da aplicação adiciona um início de sessão no campo, uma captcha ou experiências tootheir de autenticação multifator. Felizmente, em muitos casos, Microsoft pode trabalhar com aplicações fornecedores toorapidly resolva estes problemas.

Embora a Microsoft tem tooautomatically tecnologias detetar quando estes integrações interromper, mas por vezes, mas não é possível toofind estes problemas de imediato. Caso contrário, execute toofix algum tempo. No caso de Olá quando um destes integrações não funcione corretamente, agradecemos abrir um incidente de suporte para que possamos corrigi-lo mais rapidamente possível.

Na adição toothis, **se forem in contact with fornecedor desta aplicação,** **envie-os nossa forma** para que possa trabalhar com os mesmos toonatively integrar a sua aplicação no Azure Active Directory. Pode enviar Olá fornecedor toohello [listar a aplicação na Galeria de aplicações do Azure Active Directory Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los foi iniciadas.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de Browser do painel de acesso

Olá tooinstall extensão de Browser do painel de acesso, siga os passos de Olá abaixo:

1.  Abra Olá [painel de acesso](https://myapps.microsoft.com) dos browsers Olá suportado e inicie sessão como um **utilizador** no seu Azure AD.

2.  Clique num **aplicação de palavra-passe SSO** no Olá painel de acesso.

3.  Olá prompt perguntar tooinstall Olá software, selecione **instalar agora**.

4.  Com base no seu browser ser toohello direcionados hiperligação de transferência. **Adicionar** browser de tooyour Olá extensão.

5.  Se o browser pede-lhe, selecione tooeither **ativar** ou **permitir** Olá extensão.

6.  Uma vez instalado, **reiniciar** a sessão do browser.

7.  Inicie sessão no painel de acesso de Olá e veja se pode **iniciar** as aplicações de SSO de palavra-passe

Também pode transferir a extensão de Olá para Chrome e Firefox de hiperligações diretas Olá abaixo:

-   [Extensão de painel de acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão de painel de acesso de Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Passos seguintes
[Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação](active-directory-application-proxy-sso-using-kcd.md)

