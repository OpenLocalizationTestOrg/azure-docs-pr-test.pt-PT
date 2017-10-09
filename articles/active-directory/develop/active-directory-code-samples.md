---
title: "aaaAzure exemplos de código do Active Directory | Microsoft Docs"
description: "Um índice dos exemplos de código do Azure Active Directory, organizados por cenário."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Exemplos de código do Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Pode utilizar o Microsoft Azure Active Directory (Azure AD) tooadd autenticação e autorização tooyour aplicações web e web APIs. Esta secção contém ligações toosamples que mostram como é efetuada e de fragmentos de código que pode utilizar nas suas aplicações. Na página de exemplo de código Olá, encontrará detalhada Leia-me tópicos de ajudam com requisitos, instalação e configuração. E código de Olá é comentado toohelp compreender secções críticos Olá.

cenário de básico Olá toounderstand para cada tipo de exemplo, consulte os cenários de autenticação para o Azure AD.

Contribuir tooour exemplos em GitHub: [e documentação do Microsoft Azure Active Directory Samples](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>Web Browser tooWeb aplicação
Estes exemplos mostram como toowrite uma aplicação web que direciona Olá toosign de browser do utilizador-las no tooAzure AD.

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| C# / .NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Utilize o OpenID Connect (ASP.Net OpenID Connect OWIN middleware) tooauthenticate os utilizadores de um inquilino do Azure AD. |
| C# / .NET |[WebApp-multi-inquilino-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Uma aplicação de web de MVC do .NET do multi-inquilino utiliza OpenID Connect (ASP.Net OpenID Connect OWIN middleware) tooauthenticate os utilizadores de vários inquilinos do Azure AD. |
| C# / .NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Utilize os utilizadores de tooauthenticate de WS-Federation (ASP.Net WS-Federation OWIN middleware) de um inquilino do Azure AD. |

## <a name="single-page-application-spa"></a>Aplicação de página única (SPA)
Este exemplo mostra como toowrite uma aplicação de página única protegidos com o Azure AD.  

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| JavaScript, c# / .NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Utilizam a ADAL para JavaScript e o Azure AD toosecure um AngularJS com base em única página aplicação implementada com um ASP.NET web API de back-end. |

## <a name="native-application-tooweb-api"></a>Nativo tooWeb de aplicação API
Estes exemplos de código mostram como as aplicações de cliente nativo de toobuild chamar as APIs web que são protegidas pelo Azure AD. Utilizarem [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) e [OAuth 2.0 no Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| Javascript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Utilize Olá ADAL Plug-in para Apache Cordova toobuild uma aplicação Apache Cordova que chama uma API web e utiliza o Azure AD para autenticação. |
| C# / .NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Uma aplicação .NET WPF que chama uma API web que está protegida por utilizar o Azure AD. |
| C# / .NET |[NativeClient WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Uma aplicação da loja Windows que chama uma API web que está protegida com o Azure AD. |
| C# / .NET |[NativeClient-end WebAPI multi-inquilino WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Uma aplicação da loja Windows chamar uma API que está protegida com o Azure AD de web do multi-inquilino. |
| C# / .NET |[End WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Uma aplicação de cliente nativo que chama uma API web do, que obtém um token tooact em nome de utilizador original Olá e, em seguida, utiliza um Olá token toocall API web do outro. |
| C# / .NET |[NativeClient WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Uma aplicação da loja Windows para Windows Phone 8.1 que chama uma API web que está protegida pelo Azure AD. |
| ObjC |[NativeClient iOS](https://github.com/Azure-Samples/active-directory-ios) |Uma aplicação iOS que chama uma API web que requer o Azure AD para autenticação. |
| C# / .NET |[End WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Uma aplicação de cliente nativo que inclui lógica tooprocess um token JWT uma API, web em vez de utilizar o OWIN middleware. |
| C# / Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Um Xamarin enlace toohello nativo do Azure AD Authentication Library (ADAL) para Olá biblioteca do Android. |
| C# / Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Um toohello de enlace de Xamarin nativo do Azure AD Authentication Library (ADAL) para iOS. |
| C# / Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Um projeto Xamarin que visa cinco plataformas e chama uma API web que está protegido pelo Azure AD. |
| C# / .NET |[NativeClient sem interface DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Uma aplicação nativa que efetua a autenticação não interativa e chama uma API web que está protegida pelo Azure AD. |

## <a name="web-application-tooweb-api"></a>TooWeb de aplicação Web API
Estes exemplos de código mostram como utilizar [OAuth 2.0 no Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild aplicações web às quais chamar as APIs web que estão protegidos pelo Azure AD.

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| C# / .NET |[WebApp-end WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Chame uma API web Olá com sessão iniciada as permissões de utilizador. |
| C# / .NET |[WebApp-end WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Chame uma API web permissões da aplicação Olá. |
| C# / .NET |[WebApp-end WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Adicionar autorização com [OAuth 2.0 no Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan aplicação de web existente para que possa chamar uma API web. |
| JavaScript |[End WebAPI Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Configure um serviço de REST API que está integrado com o Azure AD para proteção de API. Inclui um servidor de Node.js com uma API Web. |
| C# / .NET |[WebApp-end WebAPI-multi-inquilino-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Um multi-inquilino MVC web de aplicação que utiliza o OpenID Connect (ASP.Net OpenID Connect OWIN middleware) tooauthenticate os utilizadores de um inquilino do Azure AD. Utiliza um Olá de tooinvoke de código de autorização Graph API. |

## <a name="server-or-daemon-application-tooweb-api"></a>Servidor ou aplicação Daemon tooWeb API
Estes exemplos de código mostram como toobuild um daemon ou aplicações de servidor que obtém recursos de uma API web utilizando [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) e [OAuth 2.0 no Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| C# / .NET |[O daemon de DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Uma aplicação de consola chama uma API web. credencial de cliente Olá é uma palavra-passe. |
| C# / .NET |[O daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Uma aplicação de consola que chama uma API web. credencial de cliente Olá é um certificado. |

## <a name="calling-azure-ad-graph-api"></a>Chamar do Azure AD Graph API
Nestes exemplo de código mostram como toobuild aplicações que chamam Olá dados de diretório de tooread e de escrita do AD Graph API do Azure.

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Uma aplicação web que utiliza Olá Graph API tooaccess dados de diretório do Azure AD. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Uma aplicação web que utiliza Olá Graph API tooaccess dados de diretório do Azure AD. |
| C# / .NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Uma aplicação web que utiliza Olá Graph API tooaccess dados de diretório do Azure AD. |
| C# / .NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Esta aplicação de consola demonstra comuns leitura e escrita chamadas toohello Graph API e mostra como o utilizador tooexecute atribuição de licenças e atualizar fotografia em miniatura e ligações de um utilizador. |
| C# / .NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Uma aplicação de consola que utiliza consulta diferencial Olá no Olá Graph API tooget periódica alterações de objetos toouser um inquilino do Azure AD. |
| C# / .NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Uma aplicação MVC utiliza Graph API consultas toogenerate um gráfico de organizacional simples da empresa. |
| PHP |[WebApp GraphAPI-DirectoryExtensions PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Uma aplicação PHP que chama Olá Graph API tooregister uma extensão e, em seguida, ler, atualizar e eliminar os valores do atributo de extensão de Olá. |

## <a name="authorization"></a>Autorização
Estes exemplos mostram de código como toouse do Azure AD para autorização.

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| C# / .NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Efetue o controlo de acesso baseado em funções (RBAC) utilizando afirmações de grupo do Active Directory do Azure numa aplicação que está integrada com o Azure AD. |
| C# / .NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Efetue o controlo de acesso baseado em funções (RBAC) utilizando as funções do Azure Active Directory da aplicação numa aplicação que está integrada com o Azure AD. |

## <a name="legacy-walkthroughs"></a>Instruções legadas
Estas instruções utilizam a tecnologia ligeiramente mais antiga, mas ainda podem ser de interesse.

| Idioma/plataforma | Exemplo | Descrição |
| --- | --- | --- |
| C# / .NET |[Autorização baseada em funções e baseada no ACL numa aplicação do Microsoft Azure AD](http://go.microsoft.com/fwlink/?LinkId=331694) |Efetue autorização baseada em funções (RBAC) e de autorização baseada em ACL numa aplicação que está integrada com o Azure AD. |
| C# / .NET |[AAL - loja Windows tooREST do serviço de aplicações - autenticação](http://go.microsoft.com/fwlink/?LinkId=330605) |Utilize [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) (anteriormente AAL) para Windows Store Beta tooadd utilizador autenticação capacidades tooa aplicação da loja Windows. |
| C# / .NET |[Autenticação ADAL - nativo tooREST do serviço de aplicações - com o AAD através do diálogo do Browser](http://go.microsoft.com/fwlink/?LinkId=259814) |Utilize [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) cliente WPF de tooa capacidades tooadd utilizador autenticação. |
| C# / .NET |[Autenticação ADAL - nativo tooREST do serviço de aplicações - com ACS através do diálogo do Browser](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Utilize [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) e [2.0 de serviço de controlo de acesso (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) cliente WPF de tooa capacidades tooadd utilizador autenticação. |
| C# / .NET |[ADAL - servidor tooServer autenticação](http://go.microsoft.com/fwlink/?LinkId=259816) |Utilize [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) toosecure chamadas de serviço a partir de um tooan de processo do lado do servidor serviço MVC4 Web API REST. |
| C# / .NET |[Adicionar início de sessão tooYour Web aplicação utilizar o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Configure um .NET aplicação tooperform web-início de sessão único contra o diretório de empresa do Azure AD. |
| C# / .NET |[Desenvolver aplicações Web do multi-inquilino com o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Utilizar o Azure AD tooadd toohello-início de sessão único e capacidades de acesso de diretório de um toowork de aplicações de .NET em várias organizações. |
| JAVA |[Aplicação de exemplo de Java para o Azure AD Graph API](http://go.microsoft.com/fwlink/?LinkId=263969) |Utilize Olá Graph API tooaccess dados de diretório do Azure AD. |
| PHP |[Aplicação de exemplo do PHP para o Azure AD Graph API](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Utilize Olá Graph API tooaccess dados de diretório do Azure AD. |
| C# / .NET |[Aplicação de exemplo para o Azure AD Graph API](http://go.microsoft.com/fwlink/?LinkID=262648) |Utilize Olá Graph API tooaccess dados de diretório do Azure AD. |
| C# / .NET |[Aplicação de exemplo para consulta diferencial do Azure AD Graph](http://go.microsoft.com/fwlink/?LinkId=275398) |Utilize consulta diferencial Olá Olá Graph API tooget alterações periódica toouser objetos um inquilino do Azure AD. |
| C# / .NET |[Aplicação de exemplo para integrar a aplicação multi-inquilino de nuvem do Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Integre uma aplicação multi-inquilino do Azure AD. |
| C# / .NET |[Proteger uma aplicação da loja Windows e o serviço Web REST utilizar o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Criar um recurso web simples API e uma aplicação de cliente da loja Windows através do Azure AD e Olá [do Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md). |
| C# / .NET |[Utilizar Olá tooQuery de Graph API do Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Configure um Olá de toouse de aplicação do Microsoft .NET dados do Azure AD Graph API tooaccess a partir de um diretório de inquilino do Azure AD. |

## <a name="see-also"></a>Consultar também
##### <a name="other-resources"></a>Outros Recursos
[Guia para programadores do Azure Active Directory](active-directory-developers-guide.md)

[Azure AD Graph API Conceptual e de referência](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Biblioteca do Azure AD Graph API do programa auxiliar](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
