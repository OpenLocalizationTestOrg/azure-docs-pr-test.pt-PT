---
title: "Introdução à biblioteca de CDN do Azure para .NET | Microsoft Docs"
description: "Saiba como escrever as aplicações de .NET para gerir a CDN do Azure com o Visual Studio."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Introdução à programação do CDN do Azure
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Pode utilizar o [biblioteca CDN do Azure para .NET](https://msdn.microsoft.com/library/mt657769.aspx) para automatizar a criação e gestão de perfis da CDN e os pontos finais.  Este tutorial explica a criação de uma aplicação de consola .NET simples que demonstra várias as operações disponíveis.  Este tutorial destina-se não descrever todos os aspetos da biblioteca da CDN do Azure para .NET em detalhe.

É necessário o Visual Studio 2015, para concluir este tutorial.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) livremente disponível para transferência.

> [!TIP]
> O [projeto conclusão deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) está disponível para transferência no MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Criar o projeto e adicionar pacotes Nuget
Agora que tiver criado um grupo de recursos para o nosso perfis da CDN e obtém nosso permissão de aplicação do Azure AD para gerir perfis da CDN e os pontos finais dentro desse grupo, podemos começar a criar a nossa aplicação.

No Visual Studio 2015, clique em **ficheiro**, **novo**, **projeto...**  para abrir a caixa de diálogo novo projeto.  Expanda **Visual c#**, em seguida, selecione **Windows** no painel à esquerda.  Clique em **aplicação de consola** no painel central.  Nomeie o projeto, em seguida, clique em **OK**.  

![Novo Projeto](./media/cdn-app-dev-net/cdn-new-project.png)

Nosso projeto vai utilizar algumas bibliotecas do Azure contidas nos pacotes de Nuget.  Vamos adicioná-las para o projeto.

1. Clique em de **ferramentas** menu, **Gestor de pacotes Nuget**, em seguida, **consola do Gestor de pacotes**.
   
    ![Gerir pacotes Nuget](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. Na consola do Gestor de pacotes, execute o seguinte comando para instalar o **Active Directory Authentication Library (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Execute o seguinte para instalar o **biblioteca de gestão do Azure CDN**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Diretivas, constantes, o método main e métodos de programa auxiliar
Vamos iniciar a estrutura básica do nosso programa escrito.

1. No separador de Program.cs, substitua o `using` diretivas na parte superior com o seguinte:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. É necessário definir algumas constantes que irão utilizar o nosso métodos.  No `Program` classe, mas antes o `Main` método, adicione o seguinte.  Não se esqueça de substituir os marcadores de posição, incluindo o  **&lt;angulares&gt;**, com os seus próprios valores conforme necessário.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Também o nível de classe, defina estas duas variáveis.  Utilizaremos estes mais tarde para determinar se a nossa perfil e ponto final de existir.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Substitua o `Main` método da seguinte forma:
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. Alguns dos nossos outros métodos que vão para solicitar ao utilizador com perguntas de "Sim/não".  Adicione o seguinte método para facilitar a que um pouco:
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Agora que a estrutura básica do nosso programa é escrita, criamos métodos chamados `Main` método.

## <a name="authentication"></a>Autenticação
Para que possa utilizar a biblioteca de gestão do Azure CDN, é necessário autenticar o nosso principal de serviço e obter um token de autenticação.  Este método utiliza a ADAL para obter o token.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

Se estiver a utilizar a autenticação de utilizador individuais, o `GetAccessToken` método terá um aspeto ligeiramente diferente.

> [!IMPORTANT]
> Utilize apenas código de exemplo, se escolher a autenticação de utilizador individuais em vez de um principal de serviço.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Não se esqueça de substituir `<redirect URI>` com o URI que introduziu quando se registou a aplicação no Azure AD de redirecionamento.

## <a name="list-cdn-profiles-and-endpoints"></a>Perfis da CDN lista e os pontos finais
Agora, está prontos para executar operações de CDN.  A primeira coisa que o nosso método é a lista de todos os perfis e os pontos finais no nosso grupo de recursos e se encontrar uma correspondência para os nomes de perfil e ponto final especificado no nosso constantes, faz com que uma nota do que para utilizar mais tarde, de modo que não tente criar duplicados.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Criar perfis da CDN e os pontos finais
Em seguida, vamos criar um perfil.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

Depois do perfil ser criado, vamos criar um ponto final.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> O exemplo acima, atribui o ponto final de uma origem com o nome *Contoso* com um nome de anfitrião `www.contoso.com`.  Deve alterar isto para apontar para o nome do anfitrião da sua própria origem.
> 
> 

## <a name="purge-an-endpoint"></a>Remover um ponto final
Pressupondo que foi criado o ponto final, uma tarefa comuns poderá querer efetuar no nosso programa é remover o conteúdo no nosso ponto final.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> No exemplo acima, a cadeia `/*` indica que pretender remover tudo na raiz do caminho do ponto final.  Isto é equivalente a verificação **remover todos os** na caixa de diálogo de "Remover" o portal do Azure. No `CreateCdnProfile` método, criar o nosso perfil como um **CDN do Azure da Verizon** utilizando o código de perfil `Sku = new Sku(SkuName.StandardVerizon)`, por isso, este será efetuada com êxito.  No entanto, **CDN do Azure da Akamai** perfis não suportam **remover todos os**, pelo que o se estava a utilizar um perfil de Akamai para este tutorial, seria necessário incluir caminhos específicos para remoção.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Eliminar perfis da CDN e os pontos finais
Os métodos de último eliminará nosso ponto final e o perfil.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-the-program"></a>Executar o programa
Iremos agora pode compilar e executar o programa clicando a **iniciar** botão no Visual Studio.

![Programa em execução](./media/cdn-app-dev-net/cdn-program-running-1.png)

Quando o programa atinge a linha de comandos acima, deve ser capaz de voltar para o grupo de recursos no portal do Azure e ver que o perfil foi criado.

![Êxito!](./media/cdn-app-dev-net/cdn-success.png)

Vamos, em seguida, pode confirmar os avisos para executar o resto do programa.

![Conclusão do programa](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Próximos Passos
Para ver o projeto de conclusão nestas instruções, [transferir o exemplo](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

Para obter documentação adicional sobre a biblioteca de gestão de CDN do Azure para .NET, ver o [na MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Gerir os recursos CDN com [PowerShell](cdn-manage-powershell.md).

