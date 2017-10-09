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
# <a name="security-frame-exception-management--mitigations"></a>Moldura de segurança: Gestão de exceções | Mitigações 
| Produtos/serviços | Artigo |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - não inclua serviceDebug nó no ficheiro de configuração](#servicedebug)</li><li>[WCF - não inclua serviceMetadata nó no ficheiro de configuração](#servicemetadata)</li></ul> |
| **API Web** | <ul><li>[Certifique-se de que o processamento de exceções adequada é efetuado na API Web do ASP.NET](#exception)</li></ul> |
| **Aplicação Web** | <ul><li>[Expõe detalhes de segurança em mensagens de erro](#messages)</li><li>[Implementar a página de processamento de erros de predefinido](#default)</li><li>[Definir o método de implementação tooRetail no IIS](#deployment)</li><li>[Exceções se falhar de forma segura](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - não inclua serviceDebug nó no ficheiro de configuração

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, o NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Unido](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passos** | Serviços de comunicação Framework WCF (Windows) podem ser configurado tooexpose informações de depuração. Depurar informações não devem ser utilizadas em ambientes de produção. Olá `<serviceDebug>` tag define se a funcionalidade de informações de depuração Olá está ativada para um serviço WCF. Se Olá includeExceptionDetailInFaults de atributo estiver definido tootrue, informações de exceção da aplicação Olá serão devolvidas tooclients. Os atacantes podem tirar partido de informações adicionais de Olá ganham da saída toomount ataques direcionados em framework Olá, base de dados ou outros recursos utilizados por aplicação Olá de depuração. |

### <a name="example"></a>Exemplo
Olá seguinte ficheiro de configuração inclui Olá `<serviceDebug>` etiquetas: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Desative as informações de depuração no serviço de Olá. Isto pode ser conseguido através da remoção Olá `<serviceDebug>` etiquetas do ficheiro de configuração da sua aplicação. 

## <a id="servicemetadata"></a>WCF - não inclua serviceMetadata nó no ficheiro de configuração

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Genérico, o NET Framework 3 |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Unido](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passos** | Informações sobre um serviço a expor publicamente pode fornecer aos atacantes aprofundadas importantes como podem explorar o serviço Olá. Olá `<serviceMetadata>` tag ativa a funcionalidade de publicação de metadados de Olá. Metadados do serviço podem conter informações confidenciais que não devem estar acessíveis publicamente. No mínimo, permita apenas utilizadores fidedignos tooaccess Olá metadados e certifique-se de que não estão expostas informações desnecessárias. Melhor ainda, desative completamente Olá capacidade toopublish metadados. Uma configuração de WCF segura não irá conter Olá `<serviceMetadata>` etiquetas. |

## <a id="exception"></a>Certifique-se de que o processamento de exceções adequada é efetuado na API Web do ASP.NET

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC 5, 6 DE MVC |
| **Atributos**              | N/D  |
| **Referências**              | [Excepção a processar a API Web do ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [modelo validação na API Web do ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Passos** | Por predefinição, os mais exceções não identificadas na API Web do ASP.NET estão convertidas uma resposta HTTP com o código de estado`500, Internal Server Error`|

### <a name="example"></a>Exemplo
código de estado de Olá toocontrol devolvido pelo Olá API, `HttpResponseException` podem ser utilizados como mostrado abaixo: 
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

### <a name="example"></a>Exemplo
Para obter mais controlo da resposta de exceção Olá, Olá `HttpResponseMessage` classe pode ser utilizada, conforme mostrado abaixo: 
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
toocatch não processada exceções que não sejam do tipo de Olá `HttpResponseException`, podem ser utilizados filtros de excepção. Filtros de excepção implementam Olá `System.Web.Http.Filters.IExceptionFilter` interface. Olá toowrite da forma mais simples um filtro de excepções é tooderive de Olá `System.Web.Http.Filters.ExceptionFilterAttribute` classe e substitua Olá OnException método. 

### <a name="example"></a>Exemplo
Eis um filtro que converte `NotImplementedException` exceções para o código de estado HTTP `501, Not Implemented`: 
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

Existem várias formas tooregister um filtro de excepções de Web API:
- Por ação
- Pelo controlador
- Global

### <a name="example"></a>Exemplo
Olá tooapply filtrar tooa de ação específica, adicione o filtro de Olá como uma ação de toohello atributo: 
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
### <a name="example"></a>Exemplo
tooapply Olá filtro tooall das ações de Olá num `controller`, adicionar um filtro de Olá como um atributo toohello `controller` classe: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Exemplo
Olá tooapply globalmente filtrar os controladores de Web API tooall, adicionar uma instância de Olá filtro toohello `GlobalConfiguration.Configuration.Filters` coleção. Filtros de excepção nesta coleção aplicam a ação de controlador do tooany Web API. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Exemplo
Para a validação do modelo, estado do modelo de Olá pode ser transmitido tooCreateErrorResponse método conforme mostrado abaixo: 
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

Certifique-se ligações Olá Olá referências secção para obter detalhes adicionais sobre o processamento excecional e a validação do modelo na API Web do ASP.Net 

## <a id="messages"></a>Expõe detalhes de segurança em mensagens de erro

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicação Web | 
| **Fase SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Passos** | <p>Mensagens de erro genérica são fornecidas diretamente toohello utilizador sem incluir dados confidenciais de aplicações. Exemplos de dados confidenciais incluem:</p><ul><li>Nomes de servidor</li><li>Cadeias de ligação</li><li>Nomes de utilizador</li><li>Palavras-passe</li><li>Procedimentos de SQL</li><li>Detalhes de falhas SQL dinâmicos</li><li>O rastreio da pilha e linhas de código</li><li>Variáveis armazenadas na memória</li><li>Localizações de pasta ou unidade</li><li>Pontos de instalação da aplicação</li><li>Definições de configuração de anfitrião</li><li>Outros detalhes de aplicação interna</li></ul><p>Trapping todos os erros numa aplicação e fornecer as mensagens de erro genérica, bem como ativar erros personalizados no IIS irá ajudar a impedir a divulgação de informações. Base de dados do SQL Server e exceções de .NET processar, entre outros arquiteturas de processamento de erros são especialmente verboso e extremamente úteis tooa utilizador mal intencionado a aplicação de criação de perfis. Fazê-lo não diretamente Olá apresentar conteúdo de uma classe derivada da classe de exceção de .NET Olá e certifique-se de que tem o processamento de exceções adequado, para que uma exceção inesperada não é inadvertidamente diretamente gerado toohello utilizador.</p><ul><li>Forneça um erro genérico diretamente mensagens utilizador toohello que abstracta away detalhes específicos encontrados diretamente na mensagem de exceção/erro Olá</li><li>Não apresentar Olá conteúdo de uma exceção de .NET de classe diretamente toohello utilizador</li><li>Trap todas as mensagens de erro e se adequado informar o utilizador Olá através de um cliente de aplicação de toohello enviado de mensagem de erro genérico</li><li>Expõe conteúdo Olá da classe de exceção Olá diretamente o utilizador toohello, especialmente Olá devolver o valor de `.ToString()`, ou Olá valores das propriedades de mensagem ou o rastreio da pilha de Olá. Estas informações de registo e apresentar um utilizador de toohello mensagem mais innocuous em segurança</li></ul>|

## <a id="default"></a>Implementar a página de processamento de erros de predefinido

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicação Web | 
| **Fase SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Editar a caixa de diálogo de definições de páginas de erro.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Passos** | <p>Quando uma aplicação ASP.NET falha e faz com que um HTTP/1.x 500 Erro interno do servidor ou uma configuração de funcionalidades (tais como a filtragem de pedidos) impede que uma página que está a ser apresentada, será gerada uma mensagem de erro. Os administradores podem optar se ou não a aplicação Olá deverá apresentar uma mensagem amigável toohello cliente, cliente de toohello de mensagem de erro detalhada ou toolocalhost de mensagem de erro detalhadas apenas. Olá <customErrors> tag em Web. config de Olá tem três modos de:</p><ul><li>**No:** Especifica que erros personalizados estão ativados. Não se for especificado nenhum atributo defaultRedirect, os utilizadores veem um erro genérico. erros personalizados Olá são mostrados a clientes remotos toohello e anfitrião local toohello</li><li>**Desativar:** Especifica que erros personalizados estão desativados. Olá erros ASP.NET detalhados são apresentados toohello de clientes remotos e o anfitrião local toohello</li><li>**RemoteOnly:** Especifica que erros personalizados são apresentados apenas toohello clientes remotos e que o ASP.NET erros são apresentados toohello de anfitrião local. Este é o valor predefinido de Olá</li></ul><p>Abra Olá `web.config` de ficheiros para o site e aplicações Olá e certifique-se de que a tag de Olá tem um `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` definido.</p>|

## <a id="deployment"></a>Definir o método de implementação tooRetail no IIS

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicação Web | 
| **Fase SDL**               | Implementação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [implementação de elemento (esquema de definições do ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Passos** | <p>Olá `<deployment retail>` comutador destina-se pelos servidores IIS de produção. Este parâmetro é aplicações toohelp utilizados executadas com Olá um melhor desempenho possível e menor número possíveis informações de segurança leakages através da desativação de Olá saída do rastreio da aplicação capacidade toogenerate numa página, a desativação toodisplay de capacidade de Olá detalhes do erro mensagens tooend que os utilizadores e a desativação Olá depuração comutador.</p><p>Muitas vezes, comutadores e as opções centrados na programação, como falha solicitar o rastreio e depuração, são ativadas durante o desenvolvimento de Active Directory. Recomenda-se que o método de implementação de Olá em qualquer servidor de produção ser definido tooretail. Abra o ficheiro de Machine. config Olá e certifique-se de que `<deployment retail="true" />` permanece definir tootrue.</p>|

## <a id="fail"></a>Exceções se falhar de forma segura

| Título                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicação Web | 
| **Fase SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Falhar de forma segura](https://www.owasp.org/index.php/Fail_securely) |
| **Passos** | Aplicação se falhar de forma segura. Um método que devolva um valor booleano, com base no que determinados decisão é efetuada, deve ter bloco exception cuidadosamente criado. Existem muitos erros lógicos devido toowhich creep de problemas de segurança no, quando o bloco de excepção Olá é escrito carelessly.|

### <a name="example"></a>Exemplo
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
Olá acima método sempre irá devolver True, se acontecer algum exceção. Se o utilizador final de Olá fornece um URL incorreto, que Olá respeita do browser, mas Olá `Uri()` não construtor, isto irá gerar uma exceção e vítima Olá será executado toohello válido, mas com formato incorreto URL. 
