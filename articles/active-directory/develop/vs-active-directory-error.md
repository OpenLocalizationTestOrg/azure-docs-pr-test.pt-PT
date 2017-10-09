---
title: "erros de toodiagnose aaaHow Olá Assistente de ligação do Azure Active Directory"
description: "Assistente de ligação do Active Directory Olá detetou um tipo de autenticação incompatível"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Diagnosticar erros com Olá Assistente de ligação do Azure Active Directory
Ao detetar o código de autenticação anterior, o Assistente de Olá detetou um tipo de autenticação incompatível.   

## <a name="what-is-being-checked"></a>O que está a ser modificado?
**Nota:** toocorrectly detetar anterior código de autenticação num projeto, projeto Olá tem de ser criado.  Se encontrou o erro e não tiver um código de autenticação anterior no seu projeto, reconstruir e tente novamente.

### <a name="project-types"></a>Tipos de projeto
Assistente de Olá verifica tipo Olá do projeto que está a desenvolver, de modo que pode inserir lógica de autenticação direita Olá no projeto Olá.  Se não houver qualquer controlador que derive `ApiController` no projeto Olá, projeto Olá é considerado um projeto de end WebAPI.  Se existirem apenas os controladores que derivem de `MVC.Controller` no projeto Olá, projeto Olá é considerado um projeto MVC.  Tudo o resto não é suportado pelo Assistente de Olá.

### <a name="compatible-authentication-code"></a>Código de autenticação compatível
Assistente de Olá também verifica a existência de definições de autenticação que foram anteriormente configuradas com o Assistente de Olá ou que são compatíveis com o Assistente de Olá.  Se todas as definições estiverem presentes, é considerada um caso re-entrant e será apresentado o assistente Olá apresenta as definições de Olá.  Se apenas algumas das definições de Olá estiverem presentes, é considerada um caso de erro.

Num projeto MVC, o Assistente de Olá verifica a existência de qualquer um dos Olá definições, o que resultam da utilização anterior do Assistente de Olá os seguintes:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Além disso, o Assistente de Olá verifica a existência de qualquer um dos Olá definições num projeto Web API, que resultam da utilização anterior do Assistente de Olá os seguintes:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Código de autenticação incompatível
Por fim, o Assistente de Olá tenta versões de toodetect do código de autenticação que foram configuradas com versões anteriores do Visual Studio. Se receber este erro, significa que projecto contém um tipo de autenticação incompatível. Assistente de Olá Deteta Olá seguintes tipos de autenticação de versões anteriores do Visual Studio:

* Autenticação do Windows 
* Contas de utilizador individuais 
* Contas organizacionais 

toodetect autenticação do Windows num projeto MVC, o Assistente de Olá procura Olá `authentication` elemento a partir do seu **Web. config** ficheiro.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect autenticação do Windows num projeto Web API, o Assistente de Olá procura Olá `IISExpressWindowsAuthentication` elemento a partir do seu projeto **. csproj** ficheiro:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

autenticação de contas de utilizador individuais toodetect, assistente Olá procura do elemento de pacote Olá a partir do seu **Packages** ficheiro.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect um formulário antigo de autenticação da conta institucional, o Assistente de Olá procura Olá seguinte elemento a partir do **Web. config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

tipo de autenticação do toochange Olá, remova o tipo de autenticação incompatível Olá e execute novamente o Assistente de Olá.

Para obter mais informações, consulte [cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Passos seguintes
- [Cenários de autenticação do Azure AD](active-directory-authentication-scenarios.md)