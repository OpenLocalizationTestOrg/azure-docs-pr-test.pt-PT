---
title: "aaaAzure AD v2 JS SPA orientado o programa de configuração - configurar | Microsoft Docs"
description: "Como aplicações de JavaScript SPA podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Registar a sua aplicação

Existem várias formas toocreate uma aplicação, selecione um dos atributos:

### <a name="option-1-register-your-application-express-mode"></a>Opção 1: Registar a sua aplicação (modo Express)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:

1.  Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Introduza um nome para a aplicação e o seu correio eletrónico
3.  Certifique-se de que opção de Olá *orientado configuração* está marcada
4.  Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código

### <a name="option-2-register-your-application-advanced-mode"></a>Opção 2: Registar a sua aplicação (modo avançado)

1. Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação
2. Introduza um nome para a aplicação e o seu correio eletrónico 
3. Certifique-se de que opção de Olá *orientado configuração* está desmarcada
4.  Clique em `Add Platform`, em seguida, selecione`Web`
5. Adicionar Olá `Redirect URL` que correspondem o URL da aplicação toohello com base no seu servidor web. Consulte as secções de Olá abaixo para obter instruções sobre como tooset / obter o URL de redirecionamento Olá no Visual Studio e Python.
6. Clique em *guardar*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio instruções para obter o URL de redirecionamento
> Siga o seu URL de redirecionamento de Olá instruções tooobtain:
> 1.    No *Explorador de soluções*, selecione o projeto de Olá e observe Olá `Properties` janela (se não for apresentada uma janela de propriedades, prima `F4`)
> 2.    Copie o valor Olá `URL` toohello área de transferência:<br/> ![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Comutador back toohello *Portal de registo de aplicação* e cole o valor de Olá como um `Redirect URL` e clique em 'Guardar'

<p/>

> #### <a name="setting-redirect-url-for-python"></a>URL de redirecionamento de definição para Python
> Para o Python, pode definir a porta do servidor web Olá através de linha de comandos. Esta configuração orientada utiliza a porta de Olá 8080 para referência, mas pode toouse livre qualquer porta disponível. Em qualquer caso, siga instruções Olá abaixo tooset configurar um URL de redirecionamento nas informações de registo de aplicação Olá:<br/>
> - Comutador toohello back- *Portal de registo de aplicação* e defina `http://localhost:8080/` como um `Redirect URL`, ou utilize `http://localhost:[port]/` se estiver a utilizar uma porta TCP personalizada (onde *[porta]* Olá é a porta TCP personalizado número) e clique em 'Guardar'


#### <a name="configure-your-javascript-spa"></a>Configurar o JavaScript SPA

1.  Crie um ficheiro denominado `msalconfig.js` que contém as informações de registo de aplicação Olá. Se estiver a utilizar o Visual Studio, o projeto de Olá selecione (pasta raiz do projeto), clique com botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`. Nome`msalconfig.js`
2.  Adicionar Olá seguinte código tooyour `msalconfig.js` ficheiro:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Substitua <code>Enter_the_Application_Id_here</code> com Olá Id da aplicação que acabou de ser registado
</li>
</ol>
