---
title: "aaaUse tooaccess de autenticação do Azure AD API de serviços de suporte de dados do Azure com o resto | Microsoft Docs"
description: "Saiba como tooaccess API de serviços de suporte de dados do Azure com a autenticação do Azure Active Directory utilizando REST."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Utilização do Azure AD authentication tooaccess Olá API de serviços de suporte de dados do Azure com REST

equipa de Media Services do Azure Olá lançou suporte de autenticação do Azure Active Directory (Azure AD) para acesso de Media Services do Azure. Anunciou também a autenticação do serviço de planos toodeprecate controlo de acesso do Azure para o acesso de Media Services. Uma vez cada subscrição do Azure e cada conta de Media Services, são inquilino tooan ligado do Azure AD, o suporte de autenticação do Azure AD tem muitas vantagens de segurança. Para obter detalhes sobre esta alteração e a migração (se utilizar Olá SDK .NET dos Media Services para a sua aplicação), consulte o artigo seguinte Olá blogue mensagens e os artigos:

- [Media Services do Azure announces suporte para o Azure AD e descontinuação de autenticação de controlo de acesso](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation)
- [API dos serviços de suporte de dados de Azure do acesso através da autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md)
- [Utilizar o Azure AD authentication tooaccess API de serviços de suporte de dados do Azure com o Microsoft .NET](media-services-dotnet-get-started-with-aad.md)
- [Introdução à autenticação do Azure AD utilizando Olá portal do Azure](media-services-portal-get-started-with-aad.md)

Alguns clientes necessário toodevelop as soluções de Media Services em Olá seguintes restrições:

*   Utilizam uma linguagem de programação que não é o Microsoft .NET ou c# ou ambiente de tempo de execução de Olá não é Windows.
*   Azure AD bibliotecas, tais como bibliotecas de autenticação do Active Directory não estão disponíveis para Olá linguagem de programação ou não podem ser utilizadas para o respetivo ambiente de tempo de execução.

Alguns clientes tem programado aplicações utilizando a REST API para autenticação de controlo de acesso e acesso de Media Services do Azure. Para estes clientes, é necessário um Olá-apenas de toouse de forma REST API para a autenticação do Azure AD e aceder a subsequentes Media Services do Azure. Terá de toonot baseiam-se em qualquer uma das bibliotecas de Olá do Azure AD ou Olá SDK .NET dos Media Services. Neste artigo, vamos descrevem uma solução e forneça o código de exemplo para este cenário. Porque o código de Olá é todas as chamadas da REST API, com nenhuma dependência em qualquer do Azure AD ou biblioteca de Media Services do Azure, código de Olá pode facilmente ser tooany traduzida outra linguagem de programação.

> [!IMPORTANT]
> Atualmente, os Media Services suportam o modelo de autenticação de serviços de controlo de acesso do Azure Olá. No entanto, vai ser preterida a autenticação de controlo de acesso 1 de Junho de 2018. Recomendamos que migre o modelo de autenticação toohello do Azure AD logo que possível.


## <a name="design"></a>Design

Neste artigo, utilizamos Olá seguir a estrutura de autenticação e autorização:

*  Protocolo de autorização: OAuth 2.0. OAuth 2.0 é uma norma de segurança de web que abrange a autenticação e autorização. É suportada pela Google, Microsoft, Facebook e PayPal. -Foi ratified Outubro de 2012. Microsoft corretas oferece suporte a OAuth 2.0 e o OpenID Connect. Ambos estes padrões são suportados em vários serviços e bibliotecas de cliente, incluindo o Azure Active Directory, Open Web Interface para Katana .NET (OWIN) e bibliotecas do Azure AD.
*  Tipo de conceder: tipo de conceder de credenciais do cliente. Credenciais do cliente é um dos tipos de concessão de quatro Olá OAuth 2.0. Muitas vezes, é utilizado para acesso ao Microsoft Azure AD Graph API.
*  Modo de autenticação: principal de serviço. Olá outro modo de autenticação é utilizador ou a autenticação interativa.

Um total de quatro aplicações ou serviços envolvidas no fluxo de autenticação e autorização Olá do Azure AD para utilizando os Media Services. Serviços e aplicações de Olá e fluxo de Olá, descritas Olá a tabela seguinte:

|Tipo de aplicação |Aplicação |Fluxo|
|---|---|---|
|Cliente | Aplicação de cliente ou solução | Esta aplicação (na realidade, o proxy) está registada no inquilino do Azure AD Olá no qual Olá Media Services do Azure de subscrição e Olá residem conta de serviço. Olá principal de serviço da aplicação Olá registado é, em seguida, concedida a função de proprietário ou contribuinte na Olá controlo de acesso (IAM) da conta de serviço de suporte de dados de Olá. o principal de serviço Olá é representado por Olá app ID de cliente e o segredo do cliente. |
|Fornecedor de identidade (IDP) | Azure AD como IDP | principal de serviço de aplicação registada Olá (ID de cliente e segredo do cliente) é autenticado pelo Azure AD como Olá IDP. Esta autenticação é efetuada internamente e implicitamente. Como no fluxo de credenciais do cliente, o cliente de Olá está autenticado em vez de utilizador de Olá. |
|Proteger o serviço de Token (STS) / servidor OAuth | Azure AD como STS | Após a autenticação por Olá IDP (ou servidor de OAuth em termos de OAuth 2.0), um token de acesso ou um Token Web JSON (JWT) é emitido pelo Azure AD como servidor de STS/OAuth para o recurso de camada média do acesso toohello: no nosso caso, Olá ponto final de API de REST dos serviços de suporte de dados. |
|Recurso | API REST dos Serviços de Multimédia | Cada chamada de API de REST dos serviços de suporte de dados está autorizada por um token de acesso que é emitido pelo Azure AD como STS ou servidor de OAuth Olá. |

Se executar o código de exemplo de Olá e capturar um JWT ou um token de acesso, Olá JWT tem Olá seguintes atributos:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Seguem-se os mapeamentos de Olá entre atributos Olá Olá JWT e Olá quatro aplicações ou serviços na Olá anterior a tabela:

|Tipo de aplicação |Aplicação |Atributo JWT |
|---|---|---|
|Cliente |Aplicação de cliente ou solução |AppID: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". ID de cliente Olá de uma aplicação irá registar tooAzure AD na secção seguinte, Olá. |
|Fornecedor de identidade (IDP) | Azure AD como IDP |IDP: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Olá GUID é inquilino de ID do Microsoft hello (microsoft.onmicrosoft.com). Cada inquilino tem um ID próprio, exclusivo. |
|Proteger o serviço de Token (STS) / servidor OAuth |Azure AD como STS | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Olá GUID é inquilino de ID do Microsoft hello (microsoft.onmicrosoft.com). |
|Recurso | API REST dos Serviços de Multimédia |aud: "https://rest.media.azure.net". destinatário Olá ou o público-alvo de token de acesso de Olá. |

## <a name="steps-for-setup"></a>Passos de configuração

tooregister e configurar uma aplicação do Azure AD para autenticação do Azure AD e tooobtain um token de acesso para chamar o ponto final de API de REST dos serviços de suporte de dados do Azure Olá, Olá concluir os seguintes passos:

1.  No Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), registar um inquilino de toohello do Azure AD de aplicação (por exemplo, wzmediaservice) do Azure AD (por exemplo, microsoft.onmicrosoft.com). Não interessa se registado como aplicação web ou aplicação nativa. Além disso, pode escolher qualquer URL de início de sessão e o URL de resposta (por exemplo, http://wzmediaservice.com para ambos).
2. No Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), aceda a toohello **configurar** separador da sua aplicação. Olá nota **ID de cliente**. Em seguida, em **chaves**, gerar uma **chave cliente** (segredo do cliente). 

    > [!NOTE] 
    > Tome nota do segredo do cliente Olá. Este não será apresentado novamente.
    
3.  No Olá [portal do Azure](http://ms.portal.azure.com), aceda a conta de Media Services toohello. Selecione Olá **controlo de acesso** painel (IAM). Adicione um novo membro que tem Olá proprietário ou função de contribuinte Olá. Para o principal de Olá, procure o nome da aplicação Olá que registou no passo 1 (neste exemplo, wzmediaservice).

## <a name="info-toocollect"></a>Informações toocollect

tooprepare REST codificação, recolher Olá tooinclude de pontos de dados no código Olá os seguintes:

*   Azure AD como um ponto final STS: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. Deste ponto final, é pedido um token de acesso JWT. Além disso tooserving como um IDP, do Azure AD também serve como um STS. O Azure AD emite um JWT para acesso a recursos (um token de acesso). Um token JWT tem várias afirmações.
*   API de REST do suporte de dados dos serviços do Azure como recursos ou o público-alvo: https://rest.media.azure.net.
*   ID de cliente: Ver passo 2 [passos para a configuração](#steps-for-setup).
*   Segredo do cliente: ver passo 2 [passos para a configuração](#steps-for-setup).
*   Os serviços de suporte de dados de conta de ponto final de REST API no Olá seguinte formato:

    https://[media_service_account_name].restv2. [data_center].media.azure.net/API 

    Este é o ponto final de Olá com que todas as API de REST de serviços de suporte de dados são efetuadas chamadas na sua aplicação. Por exemplo, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

Em seguida, pode colocar estes cinco parâmetros no seu ficheiro Web. config ou o App. config, toouse no seu código.

## <a name="sample-code"></a>Código de exemplo

Pode encontrar o código de exemplo de Olá no [do Azure AD Authentication para acesso de serviços de suporte de dados do Azure: ambos através da REST API](https://github.com/willzhan/WAMSRESTSoln).

código de exemplo de Olá tem duas partes:

*   Um projeto de biblioteca DLL, que tem todo Olá REST API o código de autorização e autenticação do Azure AD. Também tem um método para efetuar a REST API chamadas toohello API de REST dos serviços de suporte de dados ponto final, com o token de acesso de Olá.
*   Um cliente de teste da consola, que inicia a autenticação do Azure AD e chama a API de REST de serviços de suporte de dados diferentes.

projeto de exemplo de Olá tem três funcionalidades:

*   Azure AD as autenticações através de credenciais do cliente Olá conceder ao utilizar apenas Olá REST API.
*   Acesso de Media Services do Azure utilizando apenas Olá REST API.
*   Acesso de armazenamento do Azure utilizando Olá apenas a REST API (como toocreate utilizada uma conta de Media Services, utilizando a REST API).


## <a name="where-is-hello-refresh-token"></a>Onde está o token de atualização de Olá?

Poderão pedir-lhe algumas leitores: onde está o token de atualização de Olá? Por que motivo não utilizar um token de atualização aqui?

objetivo Olá um token de atualização não é toorefresh um token de acesso. Em vez disso, é concebida toobypass intervenção do utilizador ou de autenticação de utilizador final e receber um token de acesso válido quando expira um token de anterior. Um nome melhor para um token de atualização poderá ser algo como "Ignorar re-sessão-no token de utilizador do".

Se utilizar Olá fluxo (nome de utilizador e palavra-passe, agir em nome de um utilizador) de concessão de autorização do OAuth 2.0, um token de atualização ajuda a obter um acesso renovado token sem pedir intervenção do utilizador. No entanto, para Olá OAuth 2.0 fluxo dita neste artigo de concessão de credenciais do cliente, o cliente de Olá funciona no seu próprio nome. Não precisa de intervenção do utilizador de todo, e servidor de autorização de Olá não necessita de demasiado (e não serão) dão-lhe um token de atualização. Se a depuração Olá **GetUrlEncodedJWT** método, tenha em atenção que a resposta de Olá do ponto final de tokens Olá tem um token de acesso, mas nenhum token de atualização.

## <a name="next-steps"></a>Passos seguintes

Introdução ao [carregar ficheiros tooyour conta](media-services-dotnet-upload-files.md).
