---
title: "aaaAzure AD v2 Windows Desktop introdução - configuração | Microsoft Docs"
description: "Como aplicações de .NET de ambiente de trabalho do Windows (XAML) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar o projeto

Esta secção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate um .NET de ambiente de trabalho do Windows (XAML) de aplicação com *início de sessão com a Microsoft* que possa consultar APIs da Web que necessita de um token.

aplicação Olá criada por este guia expõe um botão toograph e mostrar os resultados no ecrã e botão de início de sessão.

> Prefere toodownload projeto do Visual Studio este exemplo em vez disso? [Transferir um projeto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.


### <a name="create-your-application"></a>Criar a sua aplicação
1. No Visual Studio:`File` > `New` > `Project`<br/>
2. Em *modelos*, selecione`Visual C#`
3. Selecione `WPF App` (ou *aplicação WPF* dependendo da versão de Olá do seu Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Adicionar Olá biblioteca de autenticação da Microsoft (MSAL) tooyour projeto
1. No Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Copie/cole seguinte Olá no Olá janela consola do Gestor de pacote:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> pacote de Olá acima instala Olá biblioteca de autenticação da Microsoft (MSAL). MSAL processa a aquisição, colocação em cache e atualizar o utilizador toskens utilizado tooaccess APIs protegidas pelo Azure Active Directory v2.

## <a name="add-hello-code-tooinitialize-msal"></a>Adicionar Olá código tooinitialize MSAL
Este passo irá ajudá-lo a criar uma interação de toohandle classe com MSAL biblioteca, tais como o processamento de tokens.

1. Abra Olá `App.xaml.cs` de ficheiros e adicionar referência Olá para a classe de toohello MSAL biblioteca:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Atualize seguinte de toohello de classe de aplicação Olá:
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a>Criar a IU da aplicação
secção de Olá abaixo mostra como uma aplicação pode consultar um servidor de back-end protegidos, como o Microsoft Graph. Um ficheiro de MainWindow.xaml automaticamente deverá ser criado como parte do seu modelo de projeto. Abrir este ficheiro este ficheiro e, em seguida, siga as instruções de Olá abaixo:

Substitua a sua aplicação `<Grid>` com ser seguinte Olá:

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
