---
title: "aaaAuthenticating e autorização com Power BI Embedded"
description: "Autenticação e autorização com Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Autenticação e autorização com Power BI Embedded

Olá serviço Power BI Embedded utiliza **chaves** e **Tokens de aplicação** para autenticação e autorização, em vez de autenticação de utilizador final explícita. Neste modelo, a sua aplicação gere autenticação e autorização para os utilizadores finais. Quando for necessário, a sua aplicação cria e envia os Tokens de aplicação Olá que diz ao nosso serviço toorender Olá relatório pedido. Esta estrutura não requer o toouse de aplicação do Azure Active Directory para autenticação de utilizador e a autorização, embora ainda possa.

## <a name="two-ways-tooauthenticate"></a>Duas formas tooauthenticate

**Chave** -pode utilizar as chaves para todas as chamadas da API de REST do Power BI Embedded. podem encontrar chaves Olá Olá **portal do Azure** ao clicar no **todas as definições** e, em seguida, **chaves de acesso**. Trate sempre a sua chave como se fosse uma palavra-passe. Estas chaves tem toomake permissões chamar qualquer API de REST de uma coleção de área de trabalho específica.

toouse uma chave de uma chamada REST, adicione Olá cabeçalho de autorização os seguintes:            

    Authorization: AppKey {your key}

**Token de aplicação** -tokens de aplicação são utilizados para todos os pedidos embedding. Estiverem toobe concebida executar lado do cliente, pelo que estes restritos tooa único relatório e de melhores práticas tooset uma hora de expiração.

Os tokens de aplicação são um JWT (JSON Web Token) que esteja assinado por uma das suas chaves.

O token de aplicação pode conter Olá afirmações os seguintes:

| Afirmação | Descrição |
| --- | --- |
| **ver** |versão de Olá do token da aplicação Olá. 0.2.0 é a versão atual do Olá. |
| **aud** |Olá destina-se o destinatário do token de Olá. Para utilização do Power BI Embedded: "https://analysis.windows.net/powerbi/api". |
| **ISS** |Uma cadeia que indica que a aplicação Olá que emitiu o token de Olá. |
| **tipo** |tipo de Olá de token de aplicação que está a ser criada. Tipo de Olá só suportada atual é **incorporar**. |
| **WCN** |Token de Olá de nome de coleção de área de trabalho está a ser emitido para. |
| **WID** |Token de Olá de ID de área de trabalho está a ser emitidos para. |
| **RID** |Token de Olá de ID do relatório está a ser emitidos para. |
| **nome de utilizador** (opcional) |Utilizado com RLS, esta é uma cadeia que pode ajudar a identificar o utilizador Olá ao aplicar regras RLS. |
| **funções** (opcional) |Uma cadeia que contém Olá funções tooselect ao aplicar regras de segurança de nível de linha. Se a transmitir mais de uma função, deve ser transmitidas como uma matriz de sting. |
| **SCP** (opcional) |Uma cadeia contendo âmbitos de permissões de Olá. Se a transmitir mais de uma função, deve ser transmitidas como uma matriz de sting. |
| **EXP** (opcional) |Indica o tempo de Olá no qual Olá token irá expirar. Estas devem ser transmitidas como carimbos de Unix. |
| **NBF** (opcional) |Indica o tempo de Olá que Olá token começa a ser válido. Estas devem ser transmitidas como carimbos de Unix. |

Um token de aplicação de exemplo irá ter este aspeto:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Quando descodificar, irá procurar algo semelhante ao seguinte:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Existem métodos disponíveis dentro de Olá SDKs que o facilitar a criação de apptokens. Por exemplo, para o .NET pode examinar Olá [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe e Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) métodos.

Para o .NET SDK Olá, pode fazer referência demasiado[âmbitos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>âmbitos

Quando a utilização de tokens de incorporação, poderá pretender toorestrict utilização dos recursos de Olá que conceder acesso. Por este motivo, pode gerar um token com permissões com âmbito definido.

Olá seguem-se âmbitos disponíveis de Olá para Power BI Embedded.

|Âmbito|Descrição|
|---|---|
|Dataset.Read|Fornece a permissão tooread Olá especificado o conjunto de dados.|
|Dataset.Write|Fornece a permissão toowrite toohello especificado conjunto de dados.|
|Dataset.ReadWrite|Fornece a permissão tooread e escrita toohello especificado conjunto de dados.|
|Report.Read|Fornece a permissão tooview Olá especificado relatório.|
|Report.ReadWrite|Fornece a permissão tooview e editar Olá relatório especificado.|
|Workspace.Report.Create|Fornece um novo relatório no Olá especificado de permissão toocreate área de trabalho.|
|Workspace.Report.Copy|Fornece um relatório existente no Olá especificado de permissão tooclone área de trabalho.|

Pode fornecer vários âmbitos utilizando um espaço entre os âmbitos de Olá semelhante Olá seguinte.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Afirmações necessárias - âmbitos**

SCP: {scopesClaim} scopesClaim pode ser uma cadeia ou matriz de cadeias, salientar Olá permitido permissões tooworkspace recursos (relatório, conjunto de dados, etc.)

Um token descodificado, com âmbitos definido, seria ter um aspeto semelhante toohello seguinte.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Operações e âmbitos

|Operação|Recurso de destino|Permissões de token|
|---|---|---|
|Crie um novo relatório com base num conjunto de dados de (na memória).|Conjunto de dados|Dataset.Read|
|Criar um novo relatório com base num conjunto de dados de (na memória) e guarde o relatório de Olá.|Conjunto de dados|* Dataset.Read<br>* Workspace.Report.Create|
|Visualize e explore/Editar (na memória) um relatório existente. Report.Read implica Dataset.Read. Isto permitirá não permissões toosave edições.|Relatório|Report.Read|
|Editar e guardar um relatório existente.|Relatório|Report.ReadWrite|
|Guarde uma cópia de um relatório (Guardar como).|Relatório|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Eis como funciona o fluxo de Olá
1. Copie a aplicação de tooyour de chaves de API Olá. Pode obter chaves Olá em **Portal do Azure**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Token de asserções uma afirmação e tem um período de tempo de expiração.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Token obtém assinado com chaves de acesso da API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. O utilizador solicita tooview um relatório.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Token é validado com um chaves de acesso da API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded, envia um toouser de relatório.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Depois de **Power BI Embedded** envia um utilizador de toohello do relatório, utilizador de Olá pode ver o relatório de Olá na sua aplicação personalizada. Por exemplo, se importar Olá [exemplo analisar PBIX de dados de vendas](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), aplicação de web de exemplo de Olá deverá ter o seguinte aspeto:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Veja Também

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Introdução ao exemplo do Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Cenários comuns do Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introdução ao Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Repositório de Git do PowerBI CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
Mais perguntas? [Tente Olá da Comunidade do Power BI](http://community.powerbi.com/)

