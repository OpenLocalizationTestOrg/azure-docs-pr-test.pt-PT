---
title: "aaaException Azure de gestão - ferramenta de modelação de ameaça do Microsoft - | Microsoft Docs"
description: "Mitigações ameaças expostas no Olá ferramenta modelação de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="302b6-103">Moldura de segurança: Gestão de exceções | Mitigações</span><span class="sxs-lookup"><span data-stu-id="302b6-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="302b6-104">Produtos/serviços</span><span class="sxs-lookup"><span data-stu-id="302b6-104">Product/Service</span></span> | <span data-ttu-id="302b6-105">Artigo</span><span class="sxs-lookup"><span data-stu-id="302b6-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="302b6-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="302b6-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="302b6-107">WCF - não inclua serviceDebug nó no ficheiro de configuração</span><span class="sxs-lookup"><span data-stu-id="302b6-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="302b6-108">WCF - não inclua serviceMetadata nó no ficheiro de configuração</span><span class="sxs-lookup"><span data-stu-id="302b6-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="302b6-109">**API Web**</span><span class="sxs-lookup"><span data-stu-id="302b6-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="302b6-110">Certifique-se de que o processamento de exceções adequada é efetuado na API Web do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="302b6-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="302b6-111">**Aplicação Web**</span><span class="sxs-lookup"><span data-stu-id="302b6-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="302b6-112">Expõe detalhes de segurança em mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="302b6-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="302b6-113">Implementar a página de processamento de erros de predefinido</span><span class="sxs-lookup"><span data-stu-id="302b6-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="302b6-114">Definir o método de implementação tooRetail no IIS</span><span class="sxs-lookup"><span data-stu-id="302b6-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="302b6-115">Exceções se falhar de forma segura</span><span class="sxs-lookup"><span data-stu-id="302b6-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="302b6-116"><a id="servicedebug"></a>WCF - não inclua serviceDebug nó no ficheiro de configuração</span><span class="sxs-lookup"><span data-stu-id="302b6-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="302b6-117">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-117">Title</span></span>                   | <span data-ttu-id="302b6-118">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-119">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-119">**Component**</span></span>               | <span data-ttu-id="302b6-120">WCF</span><span class="sxs-lookup"><span data-stu-id="302b6-120">WCF</span></span> | 
| <span data-ttu-id="302b6-121">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-121">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-122">Compilação</span><span class="sxs-lookup"><span data-stu-id="302b6-122">Build</span></span> |  
| <span data-ttu-id="302b6-123">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-123">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-124">Genérico, o NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="302b6-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="302b6-125">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-125">**Attributes**</span></span>              | <span data-ttu-id="302b6-126">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-126">N/A</span></span>  |
| <span data-ttu-id="302b6-127">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-127">**References**</span></span>              | <span data-ttu-id="302b6-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Unido](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="302b6-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="302b6-129">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-129">**Steps**</span></span> | <span data-ttu-id="302b6-130">Serviços de comunicação Framework WCF (Windows) podem ser configurado tooexpose informações de depuração.</span><span class="sxs-lookup"><span data-stu-id="302b6-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="302b6-131">Depurar informações não devem ser utilizadas em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="302b6-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="302b6-132">Olá `<serviceDebug>` tag define se a funcionalidade de informações de depuração Olá está ativada para um serviço WCF.</span><span class="sxs-lookup"><span data-stu-id="302b6-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="302b6-133">Se Olá includeExceptionDetailInFaults de atributo estiver definido tootrue, informações de exceção da aplicação Olá serão devolvidas tooclients.</span><span class="sxs-lookup"><span data-stu-id="302b6-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="302b6-134">Os atacantes podem tirar partido de informações adicionais de Olá ganham da saída toomount ataques direcionados em framework Olá, base de dados ou outros recursos utilizados por aplicação Olá de depuração.</span><span class="sxs-lookup"><span data-stu-id="302b6-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="302b6-135">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-135">Example</span></span>
<span data-ttu-id="302b6-136">Olá seguinte ficheiro de configuração inclui Olá `<serviceDebug>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="302b6-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="302b6-137">Desative as informações de depuração no serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="302b6-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="302b6-138">Isto pode ser conseguido através da remoção Olá `<serviceDebug>` etiquetas do ficheiro de configuração da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="302b6-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="302b6-139"><a id="servicemetadata"></a>WCF - não inclua serviceMetadata nó no ficheiro de configuração</span><span class="sxs-lookup"><span data-stu-id="302b6-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="302b6-140">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-140">Title</span></span>                   | <span data-ttu-id="302b6-141">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-142">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-142">**Component**</span></span>               | <span data-ttu-id="302b6-143">WCF</span><span class="sxs-lookup"><span data-stu-id="302b6-143">WCF</span></span> | 
| <span data-ttu-id="302b6-144">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-144">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-145">Compilação</span><span class="sxs-lookup"><span data-stu-id="302b6-145">Build</span></span> |  
| <span data-ttu-id="302b6-146">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-146">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-147">Genérico</span><span class="sxs-lookup"><span data-stu-id="302b6-147">Generic</span></span> |
| <span data-ttu-id="302b6-148">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-148">**Attributes**</span></span>              | <span data-ttu-id="302b6-149">Genérico, o NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="302b6-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="302b6-150">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-150">**References**</span></span>              | <span data-ttu-id="302b6-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Unido](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="302b6-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="302b6-152">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-152">**Steps**</span></span> | <span data-ttu-id="302b6-153">Informações sobre um serviço a expor publicamente pode fornecer aos atacantes aprofundadas importantes como podem explorar o serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="302b6-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="302b6-154">Olá `<serviceMetadata>` tag ativa a funcionalidade de publicação de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="302b6-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="302b6-155">Metadados do serviço podem conter informações confidenciais que não devem estar acessíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="302b6-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="302b6-156">No mínimo, permita apenas utilizadores fidedignos tooaccess Olá metadados e certifique-se de que não estão expostas informações desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="302b6-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="302b6-157">Melhor ainda, desative completamente Olá capacidade toopublish metadados.</span><span class="sxs-lookup"><span data-stu-id="302b6-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="302b6-158">Uma configuração de WCF segura não irá conter Olá `<serviceMetadata>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="302b6-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="302b6-159"><a id="exception"></a>Certifique-se de que o processamento de exceções adequada é efetuado na API Web do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="302b6-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="302b6-160">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-160">Title</span></span>                   | <span data-ttu-id="302b6-161">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-162">**Component**</span></span>               | <span data-ttu-id="302b6-163">API Web</span><span class="sxs-lookup"><span data-stu-id="302b6-163">Web API</span></span> | 
| <span data-ttu-id="302b6-164">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-164">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-165">Compilação</span><span class="sxs-lookup"><span data-stu-id="302b6-165">Build</span></span> |  
| <span data-ttu-id="302b6-166">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-166">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-167">MVC 5, 6 DE MVC</span><span class="sxs-lookup"><span data-stu-id="302b6-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="302b6-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-168">**Attributes**</span></span>              | <span data-ttu-id="302b6-169">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-169">N/A</span></span>  |
| <span data-ttu-id="302b6-170">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-170">**References**</span></span>              | <span data-ttu-id="302b6-171">[Excepção a processar a API Web do ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [modelo validação na API Web do ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="302b6-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="302b6-172">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-172">**Steps**</span></span> | <span data-ttu-id="302b6-173">Por predefinição, os mais exceções não identificadas na API Web do ASP.NET estão convertidas uma resposta HTTP com o código de estado`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="302b6-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="302b6-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-174">Example</span></span>
<span data-ttu-id="302b6-175">código de estado de Olá toocontrol devolvido pelo Olá API, `HttpResponseException` podem ser utilizados como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="302b6-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="302b6-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-176">Example</span></span>
<span data-ttu-id="302b6-177">Para obter mais controlo da resposta de exceção Olá, Olá `HttpResponseMessage` classe pode ser utilizada, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="302b6-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="302b6-178">toocatch não processada exceções que não sejam do tipo de Olá `HttpResponseException`, podem ser utilizados filtros de excepção.</span><span class="sxs-lookup"><span data-stu-id="302b6-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="302b6-179">Filtros de excepção implementam Olá `System.Web.Http.Filters.IExceptionFilter` interface.</span><span class="sxs-lookup"><span data-stu-id="302b6-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="302b6-180">Olá toowrite da forma mais simples um filtro de excepções é tooderive de Olá `System.Web.Http.Filters.ExceptionFilterAttribute` classe e substitua Olá OnException método.</span><span class="sxs-lookup"><span data-stu-id="302b6-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="302b6-181">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-181">Example</span></span>
<span data-ttu-id="302b6-182">Eis um filtro que converte `NotImplementedException` exceções para o código de estado HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="302b6-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="302b6-183">Existem várias formas tooregister um filtro de excepções de Web API:</span><span class="sxs-lookup"><span data-stu-id="302b6-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="302b6-184">Por ação</span><span class="sxs-lookup"><span data-stu-id="302b6-184">By action</span></span>
- <span data-ttu-id="302b6-185">Pelo controlador</span><span class="sxs-lookup"><span data-stu-id="302b6-185">By controller</span></span>
- <span data-ttu-id="302b6-186">Global</span><span class="sxs-lookup"><span data-stu-id="302b6-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="302b6-187">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-187">Example</span></span>
<span data-ttu-id="302b6-188">Olá tooapply filtrar tooa de ação específica, adicione o filtro de Olá como uma ação de toohello atributo:</span><span class="sxs-lookup"><span data-stu-id="302b6-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="302b6-189">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-189">Example</span></span>
<span data-ttu-id="302b6-190">tooapply Olá filtro tooall das ações de Olá num `controller`, adicionar um filtro de Olá como um atributo toohello `controller` classe:</span><span class="sxs-lookup"><span data-stu-id="302b6-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="302b6-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-191">Example</span></span>
<span data-ttu-id="302b6-192">Olá tooapply globalmente filtrar os controladores de Web API tooall, adicionar uma instância de Olá filtro toohello `GlobalConfiguration.Configuration.Filters` coleção.</span><span class="sxs-lookup"><span data-stu-id="302b6-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="302b6-193">Filtros de excepção nesta coleção aplicam a ação de controlador do tooany Web API.</span><span class="sxs-lookup"><span data-stu-id="302b6-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="302b6-194">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-194">Example</span></span>
<span data-ttu-id="302b6-195">Para a validação do modelo, estado do modelo de Olá pode ser transmitido tooCreateErrorResponse método conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="302b6-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="302b6-196">Certifique-se ligações Olá Olá referências secção para obter detalhes adicionais sobre o processamento excecional e a validação do modelo na API Web do ASP.Net</span><span class="sxs-lookup"><span data-stu-id="302b6-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="302b6-197"><a id="messages"></a>Expõe detalhes de segurança em mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="302b6-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="302b6-198">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-198">Title</span></span>                   | <span data-ttu-id="302b6-199">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-200">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-200">**Component**</span></span>               | <span data-ttu-id="302b6-201">Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="302b6-201">Web Application</span></span> | 
| <span data-ttu-id="302b6-202">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-202">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-203">Compilação</span><span class="sxs-lookup"><span data-stu-id="302b6-203">Build</span></span> |  
| <span data-ttu-id="302b6-204">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-204">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-205">Genérico</span><span class="sxs-lookup"><span data-stu-id="302b6-205">Generic</span></span> |
| <span data-ttu-id="302b6-206">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-206">**Attributes**</span></span>              | <span data-ttu-id="302b6-207">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-207">N/A</span></span>  |
| <span data-ttu-id="302b6-208">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-208">**References**</span></span>              | <span data-ttu-id="302b6-209">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-209">N/A</span></span>  |
| <span data-ttu-id="302b6-210">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-210">**Steps**</span></span> | <p><span data-ttu-id="302b6-211">Mensagens de erro genérica são fornecidas diretamente toohello utilizador sem incluir dados confidenciais de aplicações.</span><span class="sxs-lookup"><span data-stu-id="302b6-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="302b6-212">Exemplos de dados confidenciais incluem:</span><span class="sxs-lookup"><span data-stu-id="302b6-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="302b6-213">Nomes de servidor</span><span class="sxs-lookup"><span data-stu-id="302b6-213">Server names</span></span></li><li><span data-ttu-id="302b6-214">Cadeias de ligação</span><span class="sxs-lookup"><span data-stu-id="302b6-214">Connection strings</span></span></li><li><span data-ttu-id="302b6-215">Nomes de utilizador</span><span class="sxs-lookup"><span data-stu-id="302b6-215">Usernames</span></span></li><li><span data-ttu-id="302b6-216">Palavras-passe</span><span class="sxs-lookup"><span data-stu-id="302b6-216">Passwords</span></span></li><li><span data-ttu-id="302b6-217">Procedimentos de SQL</span><span class="sxs-lookup"><span data-stu-id="302b6-217">SQL procedures</span></span></li><li><span data-ttu-id="302b6-218">Detalhes de falhas SQL dinâmicos</span><span class="sxs-lookup"><span data-stu-id="302b6-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="302b6-219">O rastreio da pilha e linhas de código</span><span class="sxs-lookup"><span data-stu-id="302b6-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="302b6-220">Variáveis armazenadas na memória</span><span class="sxs-lookup"><span data-stu-id="302b6-220">Variables stored in memory</span></span></li><li><span data-ttu-id="302b6-221">Localizações de pasta ou unidade</span><span class="sxs-lookup"><span data-stu-id="302b6-221">Drive and folder locations</span></span></li><li><span data-ttu-id="302b6-222">Pontos de instalação da aplicação</span><span class="sxs-lookup"><span data-stu-id="302b6-222">Application install points</span></span></li><li><span data-ttu-id="302b6-223">Definições de configuração de anfitrião</span><span class="sxs-lookup"><span data-stu-id="302b6-223">Host configuration settings</span></span></li><li><span data-ttu-id="302b6-224">Outros detalhes de aplicação interna</span><span class="sxs-lookup"><span data-stu-id="302b6-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="302b6-225">Trapping todos os erros numa aplicação e fornecer as mensagens de erro genérica, bem como ativar erros personalizados no IIS irá ajudar a impedir a divulgação de informações.</span><span class="sxs-lookup"><span data-stu-id="302b6-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="302b6-226">Base de dados do SQL Server e exceções de .NET processar, entre outros arquiteturas de processamento de erros são especialmente verboso e extremamente úteis tooa utilizador mal intencionado a aplicação de criação de perfis.</span><span class="sxs-lookup"><span data-stu-id="302b6-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="302b6-227">Fazê-lo não diretamente Olá apresentar conteúdo de uma classe derivada da classe de exceção de .NET Olá e certifique-se de que tem o processamento de exceções adequado, para que uma exceção inesperada não é inadvertidamente diretamente gerado toohello utilizador.</span><span class="sxs-lookup"><span data-stu-id="302b6-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="302b6-228">Forneça um erro genérico diretamente mensagens utilizador toohello que abstracta away detalhes específicos encontrados diretamente na mensagem de exceção/erro Olá</span><span class="sxs-lookup"><span data-stu-id="302b6-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="302b6-229">Não apresentar Olá conteúdo de uma exceção de .NET de classe diretamente toohello utilizador</span><span class="sxs-lookup"><span data-stu-id="302b6-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="302b6-230">Trap todas as mensagens de erro e se adequado informar o utilizador Olá através de um cliente de aplicação de toohello enviado de mensagem de erro genérico</span><span class="sxs-lookup"><span data-stu-id="302b6-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="302b6-231">Expõe conteúdo Olá da classe de exceção Olá diretamente o utilizador toohello, especialmente Olá devolver o valor de `.ToString()`, ou Olá valores das propriedades de mensagem ou o rastreio da pilha de Olá.</span><span class="sxs-lookup"><span data-stu-id="302b6-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="302b6-232">Estas informações de registo e apresentar um utilizador de toohello mensagem mais innocuous em segurança</span><span class="sxs-lookup"><span data-stu-id="302b6-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="302b6-233"><a id="default"></a>Implementar a página de processamento de erros de predefinido</span><span class="sxs-lookup"><span data-stu-id="302b6-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="302b6-234">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-234">Title</span></span>                   | <span data-ttu-id="302b6-235">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-236">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-236">**Component**</span></span>               | <span data-ttu-id="302b6-237">Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="302b6-237">Web Application</span></span> | 
| <span data-ttu-id="302b6-238">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-238">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-239">Compilação</span><span class="sxs-lookup"><span data-stu-id="302b6-239">Build</span></span> |  
| <span data-ttu-id="302b6-240">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-240">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-241">Genérico</span><span class="sxs-lookup"><span data-stu-id="302b6-241">Generic</span></span> |
| <span data-ttu-id="302b6-242">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-242">**Attributes**</span></span>              | <span data-ttu-id="302b6-243">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-243">N/A</span></span>  |
| <span data-ttu-id="302b6-244">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-244">**References**</span></span>              | <span data-ttu-id="302b6-245">[Editar a caixa de diálogo de definições de páginas de erro.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="302b6-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="302b6-246">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-246">**Steps**</span></span> | <p><span data-ttu-id="302b6-247">Quando uma aplicação ASP.NET falha e faz com que um HTTP/1.x 500 Erro interno do servidor ou uma configuração de funcionalidades (tais como a filtragem de pedidos) impede que uma página que está a ser apresentada, será gerada uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="302b6-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="302b6-248">Os administradores podem optar se ou não a aplicação Olá deverá apresentar uma mensagem amigável toohello cliente, cliente de toohello de mensagem de erro detalhada ou toolocalhost de mensagem de erro detalhadas apenas.</span><span class="sxs-lookup"><span data-stu-id="302b6-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="302b6-249">Olá <customErrors> tag em Web. config de Olá tem três modos de:</span><span class="sxs-lookup"><span data-stu-id="302b6-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="302b6-250">**No:** Especifica que erros personalizados estão ativados.</span><span class="sxs-lookup"><span data-stu-id="302b6-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="302b6-251">Não se for especificado nenhum atributo defaultRedirect, os utilizadores veem um erro genérico.</span><span class="sxs-lookup"><span data-stu-id="302b6-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="302b6-252">erros personalizados Olá são mostrados a clientes remotos toohello e anfitrião local toohello</span><span class="sxs-lookup"><span data-stu-id="302b6-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="302b6-253">**Desativar:** Especifica que erros personalizados estão desativados.</span><span class="sxs-lookup"><span data-stu-id="302b6-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="302b6-254">Olá erros ASP.NET detalhados são apresentados toohello de clientes remotos e o anfitrião local toohello</span><span class="sxs-lookup"><span data-stu-id="302b6-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="302b6-255">**RemoteOnly:** Especifica que erros personalizados são apresentados apenas toohello clientes remotos e que o ASP.NET erros são apresentados toohello de anfitrião local.</span><span class="sxs-lookup"><span data-stu-id="302b6-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="302b6-256">Este é o valor predefinido de Olá</span><span class="sxs-lookup"><span data-stu-id="302b6-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="302b6-257">Abra Olá `web.config` de ficheiros para o site e aplicações Olá e certifique-se de que a tag de Olá tem um `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` definido.</span><span class="sxs-lookup"><span data-stu-id="302b6-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="302b6-258"><a id="deployment"></a>Definir o método de implementação tooRetail no IIS</span><span class="sxs-lookup"><span data-stu-id="302b6-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="302b6-259">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-259">Title</span></span>                   | <span data-ttu-id="302b6-260">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-261">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-261">**Component**</span></span>               | <span data-ttu-id="302b6-262">Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="302b6-262">Web Application</span></span> | 
| <span data-ttu-id="302b6-263">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-263">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-264">Implementação</span><span class="sxs-lookup"><span data-stu-id="302b6-264">Deployment</span></span> |  
| <span data-ttu-id="302b6-265">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-265">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-266">Genérico</span><span class="sxs-lookup"><span data-stu-id="302b6-266">Generic</span></span> |
| <span data-ttu-id="302b6-267">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-267">**Attributes**</span></span>              | <span data-ttu-id="302b6-268">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-268">N/A</span></span>  |
| <span data-ttu-id="302b6-269">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-269">**References**</span></span>              | <span data-ttu-id="302b6-270">[implementação de elemento (esquema de definições do ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="302b6-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="302b6-271">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-271">**Steps**</span></span> | <p><span data-ttu-id="302b6-272">Olá `<deployment retail>` comutador destina-se pelos servidores IIS de produção.</span><span class="sxs-lookup"><span data-stu-id="302b6-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="302b6-273">Este parâmetro é aplicações toohelp utilizados executadas com Olá um melhor desempenho possível e menor número possíveis informações de segurança leakages através da desativação de Olá saída do rastreio da aplicação capacidade toogenerate numa página, a desativação toodisplay de capacidade de Olá detalhes do erro mensagens tooend que os utilizadores e a desativação Olá depuração comutador.</span><span class="sxs-lookup"><span data-stu-id="302b6-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="302b6-274">Muitas vezes, comutadores e as opções centrados na programação, como falha solicitar o rastreio e depuração, são ativadas durante o desenvolvimento de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="302b6-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="302b6-275">Recomenda-se que o método de implementação de Olá em qualquer servidor de produção ser definido tooretail.</span><span class="sxs-lookup"><span data-stu-id="302b6-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="302b6-276">Abra o ficheiro de Machine. config Olá e certifique-se de que `<deployment retail="true" />` permanece definir tootrue.</span><span class="sxs-lookup"><span data-stu-id="302b6-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="302b6-277"><a id="fail"></a>Exceções se falhar de forma segura</span><span class="sxs-lookup"><span data-stu-id="302b6-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="302b6-278">Título</span><span class="sxs-lookup"><span data-stu-id="302b6-278">Title</span></span>                   | <span data-ttu-id="302b6-279">Detalhes</span><span class="sxs-lookup"><span data-stu-id="302b6-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="302b6-280">**Componente**</span><span class="sxs-lookup"><span data-stu-id="302b6-280">**Component**</span></span>               | <span data-ttu-id="302b6-281">Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="302b6-281">Web Application</span></span> | 
| <span data-ttu-id="302b6-282">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="302b6-282">**SDL Phase**</span></span>               | <span data-ttu-id="302b6-283">Compilação</span><span class="sxs-lookup"><span data-stu-id="302b6-283">Build</span></span> |  
| <span data-ttu-id="302b6-284">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="302b6-284">**Applicable Technologies**</span></span> | <span data-ttu-id="302b6-285">Genérico</span><span class="sxs-lookup"><span data-stu-id="302b6-285">Generic</span></span> |
| <span data-ttu-id="302b6-286">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="302b6-286">**Attributes**</span></span>              | <span data-ttu-id="302b6-287">N/D</span><span class="sxs-lookup"><span data-stu-id="302b6-287">N/A</span></span>  |
| <span data-ttu-id="302b6-288">**Referências**</span><span class="sxs-lookup"><span data-stu-id="302b6-288">**References**</span></span>              | [<span data-ttu-id="302b6-289">Falhar de forma segura</span><span class="sxs-lookup"><span data-stu-id="302b6-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="302b6-290">**Passos**</span><span class="sxs-lookup"><span data-stu-id="302b6-290">**Steps**</span></span> | <span data-ttu-id="302b6-291">Aplicação se falhar de forma segura.</span><span class="sxs-lookup"><span data-stu-id="302b6-291">Application should fail safely.</span></span> <span data-ttu-id="302b6-292">Um método que devolva um valor booleano, com base no que determinados decisão é efetuada, deve ter bloco exception cuidadosamente criado.</span><span class="sxs-lookup"><span data-stu-id="302b6-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="302b6-293">Existem muitos erros lógicos devido toowhich creep de problemas de segurança no, quando o bloco de excepção Olá é escrito carelessly.</span><span class="sxs-lookup"><span data-stu-id="302b6-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="302b6-294">Exemplo</span><span class="sxs-lookup"><span data-stu-id="302b6-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="302b6-295">Olá acima método sempre irá devolver True, se acontecer algum exceção.</span><span class="sxs-lookup"><span data-stu-id="302b6-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="302b6-296">Se o utilizador final de Olá fornece um URL incorreto, que Olá respeita do browser, mas Olá `Uri()` não construtor, isto irá gerar uma exceção e vítima Olá será executado toohello válido, mas com formato incorreto URL.</span><span class="sxs-lookup"><span data-stu-id="302b6-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
