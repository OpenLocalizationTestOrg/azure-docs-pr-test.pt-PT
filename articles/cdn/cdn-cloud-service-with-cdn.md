---
title: "aaaIntegrate um serviço em nuvem do Azure com o Azure CDN | Microsoft Docs"
description: "Saiba como toodeploy um serviço em nuvem que serve conteúdo a partir de um ponto de final de CDN do Azure integrado"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a>Integrar um serviço em nuvem a CDN do Azure
Um serviço em nuvem pode ser integrado com a CDN do Azure, que serve qualquer conteúdo da localização do serviço de nuvem a Olá. Este oferece abordagem Olá seguintes vantagens:

* Fácil de implementar e atualizar imagens, scripts e tramas nos diretórios de projeto do seu serviço em nuvem
* Atualizar facilmente os pacotes de NuGet Olá no seu serviço de nuvem, tais como jQuery ou versões de arranque de configuração
* Gerir a sua aplicação Web e o servido CDN conteúdo tudo a partir de Olá mesmo interface de Visual Studio
* Fluxo de trabalho de implementação unificada para a sua aplicação Web e o conteúdo servido de CDN
* Integrar o agrupamento do ASP.NET e minification com CDN do Azure

## <a name="what-you-will-learn"></a>O que aprenderá
Neste tutorial, ficará a saber como:

* [Integrar um ponto final de CDN do Azure com o serviço de nuvem e a servir conteúdo estático nas suas páginas Web da CDN do Azure](#deploy)
* [Configurar definições da cache de conteúdo estático no seu serviço em nuvem](#caching)
* [Servir conteúdo das ações de controlador através da CDN do Azure](#controller)
* [Personalizada incluídas e minified conteúdo através da CDN do Azure, mantendo o script de Olá depuração experiência no Visual Studio](#bundling)
* [Configurar a contingência os scripts e CSS quando a CDN do Azure está offline](#fallback)

## <a name="what-you-will-build"></a>O que irá criar
Irá implementar uma função de Web do serviço de nuvem utilizar a predefinição de Olá modelo MVC do ASP.NET, adicionar conteúdo de tooserve código a partir de uma CDN do Azure integrada, como uma imagem, resultados de ação de controlador e Olá predefinido JavaScript e CSS ficheiros e também escrever Olá tooconfigure de código mecanismo de contingência para pacotes servidos no evento Olá esse Olá CDN está offline.

## <a name="what-you-will-need"></a>O que precisa
Este tutorial tem Olá os seguintes pré-requisitos:

* Um Active Directory [conta do Microsoft Azure](/account/)
* Visual Studio 2015 com [SDK do Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Precisa de uma conta do Azure toocomplete neste tutorial:
> 
> * Pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -receberá créditos pode utilizar tootry saída paga serviços do Azure e, mesmo depois, pode manter Olá conta e utilizar os serviços do Azure, tais como Web sites gratuitos.
> * Pode [ativar os benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -sua subscrição do MSDN dá-lhe créditos todos os meses que pode utilizar para serviços pagos do Azure.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Implementar um serviço em nuvem
Nesta secção, irá implementar predefinido Olá modelo de aplicação de ASP.NET MVC na função de Web do serviço de nuvem do Visual Studio 2015 tooa e, em seguida, integrá-lo com um novo ponto final da CDN. Siga as instruções de Olá abaixo:

1. No Visual Studio 2015, criar um novo serviço em nuvem do Azure a partir da barra de menu Olá acedendo demasiado**ficheiro > novo > projeto > nuvem > serviço de nuvem do Azure**. Atribua um nome e clique em **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Selecione **função da Web ASP.NET** e clique em Olá  **>**  botão. Clique em OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Selecione **MVC** e clique em **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Agora, publica este tooan de função da Web serviço em nuvem do Azure. Clique no projeto de serviço em nuvem Olá e selecione **publicar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Se ainda não tiver iniciado no Microsoft Azure, clique em Olá **adicionar uma conta...**  Olá pendente e clique em **adicionar uma conta** item de menu.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. No início de sessão página Olá, inicie sessão com Olá conta Microsoft que utilizou tooactivate sua conta do Azure.
7. Assim que tem sessão iniciada, clique em **seguinte**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Partindo do princípio que ainda não criou uma conta de armazenamento ou de serviço de nuvem, o Visual Studio irão ajudá-lo a criar ambos. No Olá **criar serviço de nuvem e de conta** caixa de diálogo, o nome do tipo Olá serviço pretendido e região pretendida Olá selecione. Em seguida, clique em **Criar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. No Olá publicar a página de definições, verifique a configuração de Olá e clique em **publicar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > processo de publicação Olá para serviços em nuvem demora muito tempo. Olá ativar Web Deploy para a opção de funções todos os pode tornar a depuração do seu serviço em nuvem muito mais rápido, fornecendo atualizações rápida (mas temporário) tooyour funções da Web. Para obter mais informações sobre esta opção, consulte [publicação de um serviço em nuvem com as ferramentas do Azure de Olá](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Quando Olá **registo de atividade do Microsoft Azure** mostra que a publicação de estado é **concluído**, irá criar um ponto final da CDN que está integrado com este serviço em nuvem.
   
   > [!WARNING]
   > Se, após a publicação, o serviço em nuvem Olá implementado apresenta um ecrã de erro, é provável porque está a utilizar o serviço em nuvem Olá implementou um [convidado SO que não inclua a .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Pode contornar este problema por [implementar .NET 4.5.2 como uma tarefa de arranque](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Criar um novo perfil da CDN
Um perfil da CDN é uma coleção de pontos finais da CDN.  Cada perfil contém um ou mais pontos finais da CDN.  Pode ser útil toouse vários perfis tooorganize os pontos finais da CDN por domínio de internet, aplicação web ou alguns outros critérios.

> [!TIP]
> Se já tiver um perfil da CDN que pretende que toouse para este tutorial, avance demasiado[criar um novo ponto final da CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Criar um novo ponto final da CDN
**toocreate um novo ponto final da CDN para a sua conta de armazenamento**

1. No Olá [Azure Management Portal](https://portal.azure.com), navegue até tooyour perfil da CDN.  Poderá ter afixou-toohello dashboard no passo anterior Olá.  Se não, pode encontrá-lo ao clicar em **procurar**, em seguida, **perfis da CDN**, e clicar no perfil de Olá planear tooadd seu ponto final.
   
    é apresentado o painel do perfil da CDN Olá.
   
    ![Perfil da CDN][cdn-profile-settings]
2. Clique em Olá **adicionar ponto final** botão.
   
    ![Botão Adicionar ponto final][cdn-new-endpoint-button]
   
    Olá **adicionar um ponto final** é apresentado o painel.
   
    ![Painel Adicionar ponto final][cdn-add-endpoint]
3. Introduza um **Nome** para este ponto final da CDN.  Este nome será utilizado tooaccess os recursos em cache no domínio Olá `<EndpointName>.azureedge.net`.
4. No Olá **tipo de origem** lista pendente, selecione *serviço em nuvem*.  
5. No Olá **nome de anfitrião de origem** lista pendente, selecione o seu serviço de nuvem.
6. Deixe as predefinições de Olá para **caminho de origem**, **cabeçalho de anfitrião de origem**, e **porta de protocolo/origem**.  Tem de especificar, pelo menos, um protocolo (HTTP ou HTTPS).
7. Clique em Olá **adicionar** botão toocreate Olá novo ponto final.
8. Assim que for criado o ponto final de Olá, aparece uma lista de pontos finais para Olá perfil. Vista de lista de Olá mostra Olá URL toouse tooaccess colocados em cache conteúdo, bem como o domínio de origem Olá.
   
    ![Ponto final da CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > Olá ponto final não imediatamente estará disponível para utilização.  Pode demorar até too90 minutos para Olá registo toopropagate através da rede CDN Olá. Os utilizadores que tente imediatamente o nome de domínio do toouse Olá CDN poderão receber o código de estado 404 até que o conteúdo de Olá está disponível através de Olá CDN.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Olá teste ponto final de CDN
Quando o estado da publicação de Olá é **concluído**, abra uma janela do browser e navegue até demasiado**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. Na minha configuração, este URL é:

    http://camservice.azureedge.net/Content/bootstrap.css

Que corresponde ao toohello URL de origem no ponto final de CDN Olá os seguintes:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Quando navegar demasiado**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, dependendo do seu browser, será pedido toodownload ou abra Olá bootstrap.css que veio da sua aplicação Web publicada.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

Da mesma forma pode aceder a qualquer URL acessível publicamente em  **http://*&lt;serviceName >*.cloudapp.net/**, diretamente a partir do ponto final de CDN. Por exemplo:

* Um ficheiro. js a partir do caminho de /Script Olá
* Qualquer ficheiro de conteúdo de Olá /Content caminho
* Qualquer controlador/ação
* Se a cadeia de consulta Olá está ativada no ponto final de CDN, qualquer URL com cadeias de consulta

Na verdade, com Olá acima configuração, pode alojar serviço integralmente na nuvem Olá  **http://*&lt;cdnName >*.azureedge.net/**. Se posso navegue demasiado**http://camservice.azureedge.net/ * *, receber resultado da ação de Olá de Home/Index.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Isto não significa que, no entanto, que é sempre tooserve uma boa ideia um serviço integralmente na nuvem através da CDN do Azure. 

Uma CDN com otimização de entrega estático não necessariamente acelerar a entrega de elementos dinâmicos que não se destinam toobe em cache ou atualizado muito frequentemente, uma vez que Olá CDN tem de solicitar uma nova versão do recurso de Olá do servidor de origem Olá muito frequentemente. Para este cenário, pode ativar [aceleração dinâmico do Site](cdn-dynamic-site-acceleration.md) otimização (DSA) no ponto final de CDN que utiliza várias técnicas toospeed segurança entrega de elementos dinâmicos não colocáveis. 

Se tiver um site com uma combinação de conteúdo estático e dinâmico, pode escolher tooserve o conteúdo estático de CDN com um tipo de otimização estático (por exemplo, entrega web geral) e o conteúdo dinâmico tooserve diretamente a partir do servidor de origem Olá ou através de uma CDN ponto final com otimização de DSA ativado numa base de maiúsculas e minúsculas, maiúsculas e minúsculas. fim de toothat, já constatou como conteúdo individuais tooaccess ficheiros do ponto final de CDN Olá. Posso irá mostrar como tooserve uma ação de um controlador específico através de um ponto final de CDN específico no servir conteúdo das ações de controlador através da CDN do Azure.

alternativa Olá é toodetermine que conteúdo tooserve da CDN do Azure numa base caso a caso, o serviço em nuvem. fim de toothat, já constatou como conteúdo individuais tooaccess ficheiros do ponto final de CDN Olá. Posso irá mostrar como tooserve através de uma ação de um controlador específico Olá ponto final de CDN no [servir conteúdo das ações de controlador através do Azure CDN](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Configurar opções de colocação em cache para ficheiros estáticos no seu serviço em nuvem
Com a integração da CDN do Azure no seu serviço em nuvem, pode especificar a forma como pretende estático toobe conteúdo em cache no ponto final de CDN Olá. toodo, abra *Web. config* da função da Web do projeto (por exemplo, WebRole1) e adicione um `<staticContent>` elemento demasiado`<system.webServer>`. Olá XML abaixo configura Olá cache tooexpire em 3 dias.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Depois de fazê-lo, todos os ficheiros estáticos no seu serviço de nuvem serão observar Olá mesmo regra na sua cache da CDN. Para um controlo mais granular das definições da cache, adicione um *Web. config* para uma pasta de ficheiros e adicionar as definições não existe. Por exemplo, adicionar um *Web. config* ficheiro toohello *\Content* pasta e substitua Olá conteúdo com Olá XML a seguir:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Esta definição faz com que todos os ficheiros estáticos de Olá *\Content* toobe pasta em cache para 15 dias.

Para obter mais informações sobre como tooconfigure Olá `<clientCache>` elemento, consulte [Cache do cliente &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

No [servir conteúdo das ações de controlador através do Azure CDN](#controller), posso também irão mostrar como pode configurar definições de cache para resultados de ação de controlador na Olá cache da CDN.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Servir conteúdo das ações de controlador através da CDN do Azure
Ao integrar uma função de Web do serviço de nuvem com o CDN do Azure, é relativamente fácil tooserve conteúdo das ações de controlador através de Olá CDN do Azure. Que não seja a servir a sua nuvem service diretamente através da CDN do Azure (demonstrados acima), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra-lhe como toodo-o com um diversão MemeGenerator controlador no [reduzindo a latência na web Olá com Olá CDN do Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). Posso irá simplesmente reproduzi-la aqui.

Suponhamos no seu serviço em nuvem que pretende memes toogenerate com base numa imagem Chuck Norris mais novo / (fotografia por [João leve](http://www.flickr.com/photos/alan-light/218493788/)) como esta:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Tiver uma simples `Index` ação que permite que os clientes de Olá superlatives de Olá toospecify na imagem de Olá, em seguida, gera Olá meme depois de serem publique toohello ação. Uma vez que for Chuck Norris, que seria de esperar toobecome esta página wildly populares global. Este é um bom exemplo servir conteúdo por dinâmico com CDN do Azure.

Siga os passos de Olá acima toosetup esta ação de controlador:

1. No Olá *\Controllers* pasta, crie um novo ficheiro de CS chamado *MemeGeneratorController.cs* e substituir Olá conteúdo com Olá seguinte código. Ser se tooreplace Olá realçado parte com o nome do CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Clique com o botão direito na predefinição Olá `Index()` ação e selecione **Adicionar vista**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Aceite as definições de Olá abaixo e clique em **adicionar**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Abra Olá novo *Views\MemeGenerator\Index.cshtml* e substitua o conteúdo de Olá Olá seguir simple HTML para submeter superlatives Olá:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Publicar o serviço de nuvem de Olá novamente e navegue demasiado**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** no seu browser.

Quando submete valores de formulário Olá demasiado`/MemeGenerator/Index`, Olá `Index_Post` método da ação devolve uma ligação toohello `Show` método da ação com o identificador de entrada respetivos Olá. Ao clicar em ligação Olá, chegar Olá seguinte código:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Se está ligado o depurador local, em seguida, irá obter experiência de depuração regular Olá com um local de redirecionamento. Se estiver em execução no serviço de nuvem Olá, em seguida, irá redirecionar para:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Que corresponde ao toohello URL de origem no ponto final de CDN os seguintes:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Em seguida, pode utilizar Olá `OutputCacheAttribute` atributo em Olá `Generate` toospecify método como resultado da ação de Olá deve ser colocados em cache, que irão honrar CDN do Azure. código de Olá abaixo especificar uma expiração de cache de 1 hora (3.600 segundos).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Da mesma forma, poderá pode servir segurança conteúdo a partir de qualquer ação do controlador no seu serviço em nuvem através da CDN do Azure, com a opção de colocação em cache Olá assim o desejar.

Na secção seguinte, Olá, posso irá mostrar como tooserve Olá incluídas e minified scripts e CSS através da CDN do Azure.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Integrar o agrupamento do ASP.NET e minification com CDN do Azure
Scripts e CSS tramas alterar com pouca frequência e prime candidatos para Olá cache da CDN do Azure. Servir Olá toda função da Web através da CDN do Azure é toointegrate de forma mais fácil Olá agrupamento e minification com CDN do Azure. No entanto, poderá não quiser toodo isto, posso irá mostrar como toodo-preservando Olá pretendido develper experiência de agrupamento do ASP.NET e minification, tal como:

* Experiência de modo de depuração excelente
* Implementação simplificada
* Tooclients imediata de atualizações para as atualizações de versão do script/CSS
* Mecanismo de contingência quando ocorre uma falha de ponto final de CDN
* Minimizar a modificação do código

No Olá **WebRole1** projeto que criou no [integrar um ponto final de CDN do Azure com o seu Web site do Azure e a servir conteúdo estático nas suas páginas Web do Azure CDN](#deploy), abra *App_Start\ BundleConfig.cs* e observe Olá `bundles.Add()` chamadas de método.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Olá primeiro `bundles.Add()` instrução adiciona um pacote de scripts no diretório virtual Olá `~/bundles/jquery`. Em seguida, abra *Views\Shared\_layout. cshtml* toosee como tag de pacote Olá script é composto. Deve ser Olá toofind capaz de linha de código Razor os seguintes:

    @Scripts.Render("~/bundles/jquery")

Quando este código Razor é executado na função da Web do Azure de Olá, irá compor um `<script>` etiqueta Olá script seguinte toohello semelhante do pacote:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

No entanto, quando for executada no Visual Studio, escrevendo `F5`, irá compor cada ficheiro de script no pacote de Olá individualmente (no caso de Olá acima, apenas um ficheiro de script está no pacote de Olá):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Isto permite-lhe toodebug Olá no código JavaScript no seu ambiente de desenvolvimento ao reduzir as ligações de cliente simultâneas (agrupamento) e melhorando o ficheiro transferir desempenho (minification) na produção. É um toopreserve funcionalidade excelente com a integração da CDN do Azure. Além disso, uma vez que o pacote de Olá composto já contém uma cadeia de versão gerado automaticamente, pretende tooreplicate funcionalidade Olá, por isso, sempre que atualizar a versão de jQuery através do NuGet, pode ser atualizada no lado do cliente de Olá, assim como possíveis.

Siga os passos de Olá abaixo toointegration ASP.NET agrupamento e minification com o ponto final de CDN.

1. Novamente no *App_Start\BundleConfig.cs*, modificar Olá `bundles.Add()` métodos toouse outro [construtor do pacote](http://msdn.microsoft.com/library/jj646464.aspx), que especifica um endereço CDN. toodo Olá, substituir `RegisterBundles` definição de método com Olá seguinte código:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Ser tooreplace se `<yourCDNName>` com nome Olá a CDN do Azure.
   
    No palavras simples, que define `bundles.UseCdn = true` e adicionar um pacote de tooeach cuidadosamente crafted do URL da CDN. Por exemplo, Olá primeiro construtor no código Olá:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    é Olá igual ao:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Este construtor indica ao ASP.NET agrupamento e minification toorender ficheiros de script individuais quando debugged localmente, mas utilize Olá especificado CDN endereço tooaccess Olá script em questão. No entanto, tenha em atenção dois características importantes com este URL CDN cuidadosamente crafted:
   
   * Olá origem para este URL CDN é `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que é realmente Olá diretório virtual do pacote de script de Olá no seu serviço em nuvem.
   * Uma vez que estiver a utilizar o construtor CDN, Olá tag de script da CDN para pacote Olá já não contém cadeia de versão Olá gerado automaticamente no Olá composto URL. Tem de gerar manualmente uma cadeia de versão exclusivo sempre que o pacote de script de Olá é modificado tooforce uma cache de perder a sua CDN do Azure. AT Olá mesmo tempo, esta cadeia de versão exclusivo têm de permanecer constante através de vida de Olá de Olá implementação toomaximize acertos na cache na sua CDN do Azure após a implementação do pacote de Olá.
   * Olá, cadeia de consulta v = < W.X.Y.Z > obtém do *Properties\AssemblyInfo.cs* no seu projeto de função da Web. Pode ter um fluxo de trabalho de implementação que inclua incrementando versão da assemblagem Olá sempre publicar tooAzure. Em alternativa, pode modificar apenas *Properties\AssemblyInfo.cs* a cadeia de versão do projeto tooautomatically incremento Olá sempre que criar, utilizar o caráter universal de Olá ' *'. Por exemplo:
     
        [assemblagem: AssemblyVersion("1.0.0.*")]
     
     Outro toostreamline estratégia gerar uma cadeia exclusiva de vida de Olá de uma implementação irá funcionar aqui.
2. Voltar a publicar Olá cloud e acesso de serviço Olá página inicial.
3. Olá Vista código HTML da página Olá. Deve ser capaz de toosee Olá URL CDN composto, com uma cadeia de versão exclusivo sempre voltar a publicar o serviço de nuvem tooyour de alterações. Por exemplo:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. No Visual Studio, depurar o serviço em nuvem Olá no Visual Studio, escrevendo `F5`.,
5. Olá Vista código HTML da página Olá. Verão ainda cada ficheiro de script composto individualmente, para que pode ter uma depuração consistente experiência no Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Mecanismo de contingência para o URL de CDN
Quando o ponto final de CDN do Azure falha por algum motivo, quer toobe sua página Web smart suficiente tooaccess o servidor de Web de origem como opção de contingência Olá para carregar o JavaScript ou o arranque de configuração. É suficientemente grave toolose imagens no seu Web site devido a indisponibilidade de tooCDN, mas muito mais grave toolose página fundamental a funcionalidade fornecida pelo seu scripts e tramas.

Olá [pacote](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contém uma propriedade denominada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que lhe permitem mecanismo de contingência Olá tooconfigure falha da CDN. toouse esta propriedade, siga Olá passos abaixo:

1. No seu projeto de função da Web, abra *App_Start\BundleConfig.cs*, onde adicionou um URL de CDN em cada [construtor do pacote](http://msdn.microsoft.com/library/jj646464.aspx)e efetue o seguinte Olá realçado alterações tooadd mecanismo contingência toohello pacotes de predefinição:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Quando `CdnFallbackExpression` é não nula, script é injetado Olá HTML tootest se o pacote de Olá carregada com êxito e, se não, aceder ao mesmo pacote Olá diretamente a partir do servidor de Web de origem Olá. Esta propriedade tem de toobe conjunto tooa JavaScript expressão que testa se o pacote CDN respetivo Olá é carregado corretamente. expressão de Olá necessário tootest cada pacote difere de acordo com o toohello conteúdo. Para pacotes de predefinição Olá acima:
   
   * `window.jquery`está definido no jquery-{version}. js
   * `$.validator`está definido no jquery.validate.js
   * `window.Modernizr`está definido no modernizer-{version}. js
   * `$.fn.modal`está definido no bootstrap.js
     
     Poderá ter reparado que posso não definido CdnFallbackExpression para Olá `~/Cointent/css` pacote. Isto acontece porque atualmente não há um [erros nas System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) que injects um `<script>` etiqueta Olá CSS contingência em vez de Olá esperado `<link>` etiquetas.
     
     No entanto, há um bom [estilo pacote contingência](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferecidas pelo [Ember consultadoria grupo](https://github.com/EmberConsultingGroup).
2. solução de Olá toouse para CSS, crie um novo ficheiro de CS no seu projeto de função de Web *App_Start* pasta denominada *StyleBundleExtensions.cs*e substitua o respetivo conteúdo Olá [código a partir de GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. No *App_Start\StyleFundleExtensions.cs*, mudar o nome Olá espaço de nomes tooyour Web nome de função (por exemplo, **WebRole1**).
4. Voltar atrás demasiado`App_Start\BundleConfig.cs` e modificar Olá pela última vez `bundles.Add` instrução com Olá seguir o código realçado:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Este novo método de extensão utiliza Olá ideia mesma tooinject script no Olá HTML toocheck Olá DOM para Olá um nome de classe correspondente, o nome da regra e o valor de regra definido no pacote CSS Olá e o servidor de Web de origem do recai toohello back-se falhar de correspondência de Olá toofind.
5. Publica novamente o serviço de nuvem Olá e Olá home page do acesso.
6. Olá Vista código HTML da página Olá. Encontrará scripts injetado semelhante toohello seguinte:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Tenha em atenção que o script injetado para Olá CSS pacote contém ainda remnant errant de Olá de Olá `CdnFallbackExpression` propriedade na linha de Olá:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Mas desde Olá primeira parte Olá | | expressão será sempre devolver verdadeira (na linha de Olá diretamente acima que), a função de document.write() Olá nunca irá executar.

## <a name="more-information"></a>Mais Informações
* [Descrição geral do Olá Azure rede de entrega de conteúdos (CDN)](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Utilizar a CDN do Azure](cdn-create-new-endpoint.md)
* [Agrupamento do ASP.NET e Minification](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
