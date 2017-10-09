---
title: "aaaCreate uma aplicação do Azure de linha de negócio com a autenticação do Azure Active Directory | Microsoft Docs"
description: "Saiba como toocreate um ASP.NET MVC linha de negócio de aplicação no App Service do Azure que efetua a autenticação no Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Criar uma aplicação do Azure de linha de negócio com a autenticação do Azure Active Directory
Este artigo mostra como aplicação toocreate um .NET linha de negócio no [Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) utilizando Olá [autenticação / autorização](../app-service/app-service-authentication-overview.md) funcionalidade. Também mostra como toouse Olá [Active Directory Graph API do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery dados de diretório numa aplicação Olá.

inquilino do Azure Active Directory de Olá que utiliza pode ser um diretório só de Azure. Em alternativa, pode ser [sincronizadas com o Active Directory no local](../active-directory/active-directory-aadconnect.md) toocreate uma experiência único início de sessão para workers que estão no local e remoto. Este artigo utiliza o diretório predefinido de Olá para a sua conta do Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>O que irá criar
Irá criar uma simples aplicação de linha de negócio criar-leitura-atualizar-eliminar (CRUD) nas Web Apps do App Service que controla itens de trabalho com Olá seguintes funcionalidades:

* Autentica os utilizadores no Azure Active Directory
* Utilizadores de diretório de consulta e grupos utilizando [Active Directory Graph API do Azure](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Utilize Olá ASP.NET MVC *sem autenticação* modelo

Se precisar de controlo de acesso baseado em funções (RBAC) para a sua aplicação de linha de negócio no Azure, consulte [passo seguinte](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Do que precisa
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Tem de Olá seguintes toocomplete neste tutorial:

* Um inquilino do Azure Active Directory com utilizadores em vários grupos
* Aplicações de toocreate permissões no inquilino do Azure Active Directory de Olá
* Visual Studio 2013 atualização 4 ou posterior
* [Azure SDK 2.8.1 ou posterior](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Criar e implementar uma tooAzure de aplicação web
1. No Visual Studio, clique em **ficheiro** > **novo** > **projeto**.
2. Selecione **aplicação Web ASP.NET**, nomeie o projeto e, em **OK**.
3. Selecione Olá **MVC** modelo, em seguida, alterar autenticação Olá demasiado**sem autenticação**. Certifique-se **anfitrião na nuvem de Olá** está selecionada e clique em **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. No Olá **criar App Service** caixa de diálogo, clique em **adicionar uma conta** (e, em seguida, **adicionar uma conta** na lista pendente de Olá) toolog no tooyour conta do Azure.
5. Depois de a sessão configure a aplicação web. Criar um grupo de recursos e um novo plano de serviço de aplicações ao clicar em Olá respetivo **novo** botão. Clique em **explorar serviços Azure adicionais** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. No Olá **serviços** separador, clique em  **+**  tooadd uma base de dados do SQL Server para a sua aplicação. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. No **configurar a base de dados do SQL**, clique em **novo** toocreate uma instância do SQL Server.
8. No **configurar o SQL Server**, configurar a sua instância do SQL Server. Em seguida, clique em **OK**, **OK**, e **criar** tookick desativar a criação da aplicação Olá no Azure.
9. No **atividade do App Service do Azure**, pode ver quando a criação da aplicação Olá estiver concluída. Clique em  **publicar &lt;* appname*> toothis aplicação Web agora * *, em seguida, clique em **publicar**. 
   
    Depois de concluído o Visual Studio, é aberto Olá publicar a aplicação no browser Olá. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Configurar o acesso de autenticação e de diretório
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda Olá, clique em **serviços aplicacionais** > **&lt;*appname*> * * > **autenticação / autorização**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Ativar a autenticação do Azure Active Directory, clicando em **no** > **do Azure Active Directory** > **Express** > **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Clique em **guardar** na barra de comando Olá.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Depois de definições de autenticação de Olá são guardadas com êxito, tente navegar tooyour aplicação novamente no browser Olá. As predefinições de impôr a autenticação na aplicação Olá de todo. Se já não tiver sessão iniciada, é redirecionada tooa ecrã de início de sessão. Depois de a sessão, verá a aplicação protegida por HTTPS. Em seguida, precisa de aceder a tooenable toodirectory dados. 
5. Navegue toohello [portal clássico](https://manage.windowsazure.com).
6. No menu à esquerda Olá, clique em **do Active Directory** > **diretório predefinido** > **aplicações**  >   **&lt;* appname*> * *.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Esta é a aplicação do Azure Active Directory Olá que serviço de aplicações criado para tooenable Olá autorização / funcionalidade de autenticação.
7. Clique em **utilizadores** e **grupos** toomake se de que tem alguns utilizadores e grupos no diretório de Olá. Se não, crie alguns grupos e utilizadores de teste.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Clique em **configurar** tooconfigure esta aplicação.
9. Desloque para baixo toohello **chaves** secção e adicionar uma chave ao selecionar uma duração. Em seguida, clique em **permissões delegadas** e selecione **ler os dados de diretório**. 
   Clique em **Guardar**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Depois das definições são guardadas, desloque-se para uma cópia de segurança toohello **chaves** secção e clique em Olá **cópia** chave de cliente do botão toocopy Olá. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Se sair desta página agora, não será capaz de tooaccess este cliente chave nunca novamente.
    > 
    > 
11. Em seguida, terá de tooconfigure a aplicação web com esta chave. Inicie sessão no toohello [Explorador de recursos do Azure](https://resources.azure.com) com a sua conta do Azure.
12. Na Olá parte superior da página Olá, clique em **leitura/escrita** alterações toomake Olá Explorador de recursos do Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Localizar Olá definições de autenticação para a sua aplicação, localizado em subscrições >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **fornecedores** > **Microsoft**  >  **sites** > **&lt;*appname*> * * > **configuração**  >  **authsettings**.
14. Clique em **Editar**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. No painel de edição de Olá, defina Olá `clientSecret` e `additionalLoginParams` propriedades da seguinte forma.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Clique em **colocar** em Olá toosubmit superior as suas alterações.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Agora, tootest se tiver de autorização de Olá token tooaccess Olá Active Directory Graph API do Azure, basta navegar até ao  **https://&lt;*appname*>.azurewebsites.net/.auth/me** na sua browser. Se configurou tudo corretamente, deverá ver Olá `access_token` propriedade no Olá resposta JSON.
    
    Olá `~/.auth/me` caminho de URL é gerido pelo serviço de autenticação da aplicação / toogive de autorização todas as informações de Olá relacionadas com a sessão tooyour autenticado. Para obter mais informações, consulte [autenticação e autorização no serviço de aplicações do Azure](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Olá `access_token` tem um período de expiração. No entanto, autenticação do serviço de aplicação / autorização fornece funcionalidade de token de atualização com `~/.auth/refresh`. Para obter mais informações sobre como toouse-lo, consulte [App Store do Token de serviço](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Em seguida, irá fazer algo útil com dados de diretório.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Adicionar aplicação tooyour de funcionalidade de linha de negócio
Agora, pode criar um controlador de itens de trabalho CRUD simple.  

1. Na pasta de ~\Models Olá, crie um ficheiro de classe chamado WorkItem.cs e substitua `public class WorkItem {...}` com Olá seguinte código:
   
     utilizar System.ComponentModel.DataAnnotations;
   
     classe pública {de item de trabalho
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     enum pública WorkItemStatus {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Crie Olá projeto toomake a lógica de andaime do modelo toohello acessível novo no Visual Studio.
3. Adicionar um novo item estruturado `WorkItemsController` toohello ~\Controllers pasta (com o botão direito **controladores**, ponto demasiado**adicionar**e selecione **novo item estruturado**). 
4. Selecione **controlador MVC 5 com vistas, utilizando o Entity Framework** e clique em **adicionar**.
5. Modelo de Olá selecione que criou, em seguida, clique em  **+**  e, em seguida, **adicionar** tooadd num contexto de dados e, em seguida, clique em **adicionar**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. ~\Views\WorkItems\Create.cshtml (um item automaticamente estruturado), localize Olá `Html.BeginForm` método de programa auxiliar e torná-Olá alterações realçadas os seguintes:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Tenha em atenção que `token` e `tenant` são utilizadas pelo Olá `AadPicker` toomake objeto chama o Active Directory Graph API do Azure. Irá adicionar `AadPicker` mais tarde.     
   
   > [!NOTE]
   > Pode obter apenas bem `token` e `tenant` do lado do cliente Olá com `~/.auth/me`, mas que seria uma chamada de servidor adicionais. Por exemplo:
   > 
   > $.ajax ({dataType: "json," url: "/.auth/me", o êxito: função (dados) {var token = dados [0] .access_token; var inquilino = dados [0] .user_claims .find (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});
   > 
   > 
7. Efetuar Olá alterações mesmas com ~ \Views\WorkItems\Edit.cshtml.
8. Olá `AadPicker` objeto é definido num script terá tooadd tooyour projeto. Faça duplo clique Olá ~\Scripts pasta, aponte demasiado**adicionar**e clique em **ficheiro JavaScript**. Tipo `AadPickerLibrary` para Olá filename e clique em **OK**.
9. Copie o conteúdo Olá [aqui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) para ~ \Scripts\AadPickerLibrary.js.
   
   Script de Olá, Olá `AadPicker` objeto chamadas [Active Directory Graph API do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch para utilizadores e grupos que correspondem à entrada de Olá.  
10. ~\Scripts\AadPickerLibrary.js também utiliza Olá [widget de conclusão automática de IU jQuery](https://jqueryui.com/autocomplete/). Por isso, terá de projeto de tooyour tooadd jQuery IU. Clique com o botão direito no projeto e clique em **gerir pacotes NuGet**.
11. No Gestor de pacotes NuGet Olá, clique em Procurar, tipo **jquery-ui** na barra de pesquisa de Olá e clique em **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. No painel direito Olá, clique em **instalar**, em seguida, clique em **OK** tooproceed.
13. Abra ~\App_Start\BundleConfig.cs e Olá alterações realçadas os seguintes:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Existem mais toomanage de formas performant JavaScript e ficheiros CSS na sua aplicação. No entanto, para simplicidade que apenas vai toopiggyback em pacotes de Olá que são carregados com cada vista.
14. Por fim, no ~ \Global.asax, adicionar Olá seguinte linha de código no Olá `Application_Start()` método. `Ctrl`+`.`em cada erro de resolução de nomenclatura demasiado corrigir.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Terá desta linha de código porque utiliza o modelo MVC do Olá predefinido <code>[ValidateAntiForgeryToken]</code> decoration em algumas das ações de Olá. Devido a comportamento toohello descrito através de [Brock Allen](https://twitter.com/BrockLAllen) em [MVC 4, AntiForgeryToken e afirmações](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) o HTTP POST poderão falhar a validação de token antifalsificação porque:
    > 
    > * Azure Active Directory não envia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider Olá, que é necessário por predefinição pelo token antifalsificação de Olá.
    > * Se o Azure Active Directory é diretório sincronizado com o AD FS, confiança Olá do AD FS por predefinição não enviar Olá http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider afirmação está, embora seja possível configurar manualmente toosend do AD FS Esta afirmação.
    > 
    > `ClaimTypes.NameIdentifies`Especifica a afirmação Olá `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que forneça o Azure Active Directory.  
    > 
    > 
15. Agora, publica as suas alterações. Clique no seu projeto e clique em **publicar**.
16. Clique em **definições**, certifique-se de que existe está um tooyour de cadeia de ligação da base de dados do SQL Server, selecione **atualização de base de dados** toomake Olá alterações de esquema para o seu modelo e clique em **publicar** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. No browser Olá, navegue até toohttps: / /&lt;*appname*>.azurewebsites.net/workitems e clique em **criar novo**.
18. Clique na Olá **AssignedToName** caixa. Deverá ver agora os utilizadores e grupos do seu inquilino do Azure Active Directory numa lista pendente. Pode introduzir toofilter, ou utilizar Olá `Up` ou `Down` chave ou clique em tooselect Olá utilizador ou grupo. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Clique em **criar** alterações de Olá toosave. Em seguida, clique em **editar** no trabalho Olá criado item tooobserve Olá mesmo comportamento.

Congrats, está agora a executar uma aplicação de linha de negócio no Azure com acesso de diretório! Não há muito mais que pode fazer com o Olá Graph API. Consulte [referência da API do Azure AD Graph](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Passo seguinte
Se precisar de controlo de acesso baseado em funções (RBAC) para a sua aplicação de linha de negócio no azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para um exemplo da equipa do Azure Active Directory de Olá. Mostra-lhe como tooenable funções para a sua aplicação do Azure Active Directory e, em seguida, autorizar os utilizadores com Olá `[Authorize]` decoration.

Se a aplicação de linha de negócios tem de aceder a dados tooon local, consulte [acesso recursos no local utilizando as ligações híbridas no App Service do Azure](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Recursos adicionais
* [Autenticação e autorização no serviço de aplicações do Azure](../app-service/app-service-authentication-overview.md)
* [Autenticar com o Active Directory no local na sua aplicação do Azure](web-sites-authentication-authorization.md)
* [Criar uma aplicação de linha de negócio no Azure com a autenticação AD FS](web-sites-dotnet-lob-application-adfs.md)
* [Autenticação do serviço de aplicações e Olá AD Graph API do Azure](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Amostras do Microsoft Azure Active Directory e a documentação](https://github.com/AzureADSamples)
* [Azure Active Directory suportado Token e tipos de afirmação](http://msdn.microsoft.com/library/azure/dn195587.aspx)
