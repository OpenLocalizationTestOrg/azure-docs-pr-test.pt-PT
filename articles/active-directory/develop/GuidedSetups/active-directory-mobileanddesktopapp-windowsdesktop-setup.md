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
## <a name="set-up-your-project"></a><span data-ttu-id="f371d-103">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="f371d-103">Set up your project</span></span>

<span data-ttu-id="f371d-104">Esta secção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate um .NET de ambiente de trabalho do Windows (XAML) de aplicação com *início de sessão com a Microsoft* que possa consultar APIs da Web que necessita de um token.</span><span class="sxs-lookup"><span data-stu-id="f371d-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="f371d-105">aplicação Olá criada por este guia expõe um botão toograph e mostrar os resultados no ecrã e botão de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="f371d-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="f371d-106">Prefere toodownload projeto do Visual Studio este exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="f371d-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="f371d-107">[Transferir um projeto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.</span><span class="sxs-lookup"><span data-stu-id="f371d-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="f371d-108">Criar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="f371d-108">Create your application</span></span>
1. <span data-ttu-id="f371d-109">No Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="f371d-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="f371d-110">Em *modelos*, selecione`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="f371d-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="f371d-111">Selecione `WPF App` (ou *aplicação WPF* dependendo da versão de Olá do seu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f371d-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="f371d-112">Adicionar Olá biblioteca de autenticação da Microsoft (MSAL) tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="f371d-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="f371d-113">No Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="f371d-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="f371d-114">Copie/cole seguinte Olá no Olá janela consola do Gestor de pacote:</span><span class="sxs-lookup"><span data-stu-id="f371d-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="f371d-115">pacote de Olá acima instala Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="f371d-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="f371d-116">MSAL processa a aquisição, colocação em cache e atualizar o utilizador toskens utilizado tooaccess APIs protegidas pelo Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="f371d-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="f371d-117">Adicionar Olá código tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="f371d-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="f371d-118">Este passo irá ajudá-lo a criar uma interação de toohandle classe com MSAL biblioteca, tais como o processamento de tokens.</span><span class="sxs-lookup"><span data-stu-id="f371d-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="f371d-119">Abra Olá `App.xaml.cs` de ficheiros e adicionar referência Olá para a classe de toohello MSAL biblioteca:</span><span class="sxs-lookup"><span data-stu-id="f371d-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="f371d-120">Atualize seguinte de toohello de classe de aplicação Olá:</span><span class="sxs-lookup"><span data-stu-id="f371d-120">Update hello App class toohello following:</span></span>
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

## <a name="create-your-applications-ui"></a><span data-ttu-id="f371d-121">Criar a IU da aplicação</span><span class="sxs-lookup"><span data-stu-id="f371d-121">Create your application’s UI</span></span>
<span data-ttu-id="f371d-122">secção de Olá abaixo mostra como uma aplicação pode consultar um servidor de back-end protegidos, como o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f371d-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="f371d-123">Um ficheiro de MainWindow.xaml automaticamente deverá ser criado como parte do seu modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f371d-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="f371d-124">Abrir este ficheiro este ficheiro e, em seguida, siga as instruções de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="f371d-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="f371d-125">Substitua a sua aplicação `<Grid>` com ser seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="f371d-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
