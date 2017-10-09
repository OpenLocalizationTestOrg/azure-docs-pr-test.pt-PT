---
title: aaaSigning Rollover de chave no Azure AD | Microsoft Docs
description: "Este artigo aborda Olá melhores práticas de rollover de chave de assinatura para o Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Iniciar o rollover da chave no Azure Active Directory
Este tópico descreve o que precisa de tooknow sobre as chaves públicas Olá que são utilizados em tokens de segurança do Azure Active Directory (Azure AD) toosign. É importante toonote que estes rollover de chaves periodicamente e, numa emergência, pode ser feito imediatamente. Todas as aplicações que utilizam o Azure AD devem ser capaz de tooprogrammatically identificador Olá rollover de chave processo ou estabelecer um processo manual de rollover periódica. Continuar a ler toounderstand como chaves Olá funcionem, como tooassess Olá impacto da aplicação do Olá rollover tooyour e como tooupdate a aplicação ou estabelecer um rollover manual periódica processo toohandle rollover da chave, se necessário.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Descrição geral das chaves de assinatura no Azure AD
Azure AD utiliza a criptografia de chave pública criada numa confiança de tooestablish normas da indústria entre si próprio e Olá aplicações que a utilizam. Em termos práticos, este procedimento funciona em Olá seguinte forma: AD do Azure utiliza uma chave de assinatura que é composta por um par de chaves público e privado. Quando um utilizador inicia sessão na aplicação tooan que utiliza o Azure AD para autenticação, o Azure AD cria um token de segurança que contenha informações sobre Olá utilizador. Este token é assinada pelo Azure AD utilizando a respetiva chave privada antes de ser enviada back toohello aplicação. tooverify Olá token é válido e, na verdade, teve origem do Azure AD, a aplicação Olá necessário validar a assinatura do token de Olá utilizando a chave pública Olá exposto pelo Azure AD que está contido no inquilino Olá [OpenID Connect documento de identificação](http://openid.net/specs/openid-connect-discovery-1_0.html) ou SAML/WS-Fed [documento de metadados de Federação](active-directory-federation-metadata.md).

Por motivos de segurança, do Azure AD assinatura faz chave periodicamente e, em caso de Olá de emergência, pode ser feito imediatamente. Qualquer aplicação que se integra com o Azure AD deve estar preparada toohandle um evento de rollover de chave não é relevante frequência podem ocorrer. Se não, e a aplicação tenta toouse uma assinatura de Olá expirada tooverify chave num token, Olá início de sessão pedido irá falhar.

Não há mais do que uma chave válida disponíveis no documento de identificação de OpenID Connect Olá e o documento de metadados de Federação Olá sempre. A aplicação deve estar preparada toouse qualquer uma das chaves de Olá especificado no documento de Olá, uma vez que uma chave em breve, poderá ser revertida outro pode ser sua substituição e assim sucessivamente.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Como tooassess se a sua aplicação será afetada e que toodo sobre o assunto
Como a aplicação processa o rollover da chave depende de variáveis, como o tipo de Olá de aplicação ou o protocolo de identidade e a biblioteca foi utilizada. secções Olá abaixo avaliar se tipos de aplicações mais comuns Olá são afetados por rollover da chave de Olá e fornecem orientações sobre como tooupdate Olá rollover automático da aplicação toosupport ou atualizar manualmente a chave de Olá.

* [Aplicações de cliente nativo aceder a recursos](#nativeclient)
* [As aplicações Web / APIs aceder a recursos](#webclient)
* [As aplicações Web / APIs proteger os recursos e compilada com serviços de aplicações do Azure](#appservices)
* [As aplicações Web / APIs proteger recursos com o .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication middleware](#owin)
* [As aplicações Web / APIs proteger recursos com o middleware .NET Core OpenID Connect ou JwtBearerAuthentication](#owincore)
* [As aplicações Web / APIs proteger recursos com o módulo de passport-azure-ad Node.js](#passport)
* [As aplicações Web / APIs proteger os recursos e criados com o Visual Studio 2015 ou Visual Studio 2017](#vs2015)
* [Aplicações Web de proteger os recursos e criados com o Visual Studio 2013](#vs2013)
* [APIs da Web proteger os recursos e criados com o Visual Studio 2013](#vs2013_webapi)
* [Aplicações Web de proteger os recursos e criados com o Visual Studio 2012](#vs2012)
* [Aplicações Web de proteger os recursos e criados com o Visual Studio 2010, o 2008 utilizando o Windows Identity Foundation](#vs2010)
* [As aplicações Web / APIs proteger os recursos a utilizar quaisquer outras bibliotecas de manualmente implementar qualquer um dos Olá suportados ou protocolos](#other)

Esta orientação é **não** aplicável para:

* As aplicações adicionadas a partir da Galeria de aplicações do Azure do AD (incluindo personalizada) ter orientações separada com que diz respeito toosigning chaves. [Obter mais informações.](../active-directory-sso-certs.md)
* No local as aplicações publicadas através do proxy da aplicação não tem tooworry sobre chaves de assinatura.

### <a name="nativeclient"></a>Aplicações de cliente nativo aceder a recursos
Aplicações que só estão a aceder a recursos (revertidos Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft), geralmente, apenas obter um token e transferem-o ao longo do proprietário do recurso toohello. Uma vez que estes não estiver a proteger os recursos, estes não inspecionar o token de Olá e, por conseguinte, é necessário tooensure que estejam corretamente assinados.

As aplicações cliente nativo, se o ambiente de trabalho ou de dispositivo móvel, inseridas nesta categoria e, por conseguinte, que não são afetadas por rollover Olá.

### <a name="webclient"></a>As aplicações Web / APIs aceder a recursos
Aplicações que só estão a aceder a recursos (revertidos Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft), geralmente, apenas obter um token e transferem-o ao longo do proprietário do recurso toohello. Uma vez que estes não estiver a proteger os recursos, estes não inspecionar o token de Olá e, por conseguinte, é necessário tooensure que estejam corretamente assinados.

As aplicações Web e APIs que estão a utilizar o fluxo de Olá só de aplicação web (credenciais de cliente / certificado de cliente), inseridas nesta categoria e, por conseguinte, que não são afetadas por rollover Olá.

### <a name="appservices"></a>As aplicações Web / APIs proteger os recursos e compilada com serviços de aplicações do Azure
A autenticação dos serviços aplicacionais Azure / funcionalidade de autorização (EasyAuth) já Olá lógica necessária às toohandle rollover da chave de automaticamente.

### <a name="owin"></a>As aplicações Web / APIs proteger recursos com o .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication middleware
Se a aplicação estiver a utilizar Olá .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication middleware, já tem Olá lógica necessária às toohandle rollover da chave de automaticamente.

Pode confirmar que a aplicação está a utilizar qualquer um destes procurando qualquer um dos seguintes fragmentos na sua aplicação Startup.cs ou Startup.Auth.cs de Olá

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>As aplicações Web / APIs proteger recursos com o middleware .NET Core OpenID Connect ou JwtBearerAuthentication
Se a sua aplicação utilizar Olá .NET Core OWIN OpenID Connect ou JwtBearerAuthentication middleware, já tem Olá lógica necessária às toohandle rollover da chave de automaticamente.

Pode confirmar que a aplicação está a utilizar qualquer um destes procurando qualquer um dos seguintes fragmentos na sua aplicação Startup.cs ou Startup.Auth.cs de Olá

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>As aplicações Web / APIs proteger recursos com o módulo de passport-azure-ad Node.js
Se a aplicação estiver a utilizar o módulo de passport ad Olá Node.js, já tem Olá lógica necessária às toohandle rollover da chave de automaticamente.

Pode confirmar que a aplicação passport-ad procurando Olá seguinte fragmento na app.js sua aplicação

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>As aplicações Web / APIs proteger os recursos e criados com o Visual Studio 2015 ou Visual Studio 2017
Se a aplicação foi criada utilizando um modelo de aplicação web no Visual Studio 2015 ou Visual Studio 2017 e selecionado **profissional e escolar contas** de Olá **alterar autenticação** menu, já tem o rollover da chave Olá lógica necessária às toohandle automaticamente. Esta lógica, incorporada middleware OWIN OpenID Connect Olá, obtém e coloca em cache Olá as chaves de documento de identificação de OpenID Connect Olá e atualiza periodicamente.

Se tiver adicionado manualmente a solução de tooyour de autenticação, a aplicação poderá não ter a lógica de rollover de chave necessário Olá. Terá de toowrite-lo por si ou Olá siga os passos em [aplicações Web / APIs utilizar quaisquer outras bibliotecas de ou implementar manualmente a qualquer um dos Olá suportado protocolos.](#other).

### <a name="vs2013"></a>Aplicações Web de proteger os recursos e criados com o Visual Studio 2013
Se a aplicação foi criada utilizando um modelo de aplicação web no Visual Studio 2013 e selecionado **contas institucionais** de Olá **alterar autenticação** menu, já tem Olá necessário lógica toohandle rollover de chave automaticamente. Esta lógica armazena o identificador exclusivo da sua organização e Olá nas duas tabelas de base de dados associado projeto Olá informações da chave de assinatura. Pode encontrar cadeia de ligação de Olá da base de dados de Olá no ficheiro Web. config do projeto Olá.

Se tiver adicionado manualmente a solução de tooyour de autenticação, a aplicação poderá não ter a lógica de rollover de chave necessário Olá. Terá de toowrite-lo por si ou Olá siga os passos em [aplicações Web / APIs utilizar quaisquer outras bibliotecas de ou implementar manualmente a qualquer um dos Olá suportado protocolos.](#other).

Olá, os passos seguintes irão ajudá-lo, certifique-se de que o lógica Olá está a funcionar corretamente na sua aplicação.

1. No Visual Studio 2013, abra a solução de Olá e, em seguida, clique em Olá **Explorador de servidores** separador na janela direita Olá.
2. Expanda **ligações de dados**, **DefaultConnection**e, em seguida, **tabelas**. Localizar Olá **IssuingAuthorityKeys** tabela, faça duplo clique nele e, em seguida, clique em **Mostrar dados de tabela**.
3. No Olá **IssuingAuthorityKeys** tabela, pode haver pelo menos uma linha que corresponde ao valor do thumbprint toohello para a chave de Olá. Elimine quaisquer linhas na tabela de Olá.
4. Contexto Olá **inquilinos** tabela e, em seguida, clique em **Mostrar dados de tabela**.
5. No Olá **inquilinos** tabela, pode haver pelo menos uma linha que corresponde ao identificador de inquilino do tooa diretório exclusivo. Elimine quaisquer linhas na tabela de Olá. Se não eliminar linhas de Olá em ambos os Olá **inquilinos** tabela e **IssuingAuthorityKeys** tabela, obterá um erro durante a execução.
6. Crie e execute a aplicação Olá. Depois de ter a sessão iniciada numa conta tooyour, pode parar a aplicação Olá.
7. Devolver toohello **Explorador de servidores** e observe Olá valores existentes na Olá **IssuingAuthorityKeys** e **inquilinos** tabela. Irá notar que tenham sido repovoados automaticamente, com informações adequadas do Olá do documento de metadados de Federação Olá.

### <a name="vs2013"></a>APIs da Web proteger os recursos e criados com o Visual Studio 2013
Se criar uma aplicação API da web no Visual Studio 2013 com o modelo de Web API Olá e, em seguida, selecionou **contas institucionais** de Olá **alterar autenticação** menu, já tenham Olá lógica necessária na sua aplicação.

Se tiver configurado manualmente authentication, siga as instruções de Olá abaixo toolearn como tooconfigure tooautomatically sua Web API atualizar as informações de chaves.

Olá fragmento de código seguinte demonstra como tooget Olá chaves mais recentes do documento de metadados de Federação Olá e, em seguida, utilize Olá [processador Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) token de Olá toovalidate. o fragmento de código Olá parte do princípio de que irá utilizar os seus próprios de colocação em cache mecanismo para persistentes toovalidate de chave de Olá futura tokens do Azure AD, se, ser na base de dados, o ficheiro de configuração ou noutro local.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Aplicações Web de proteger os recursos e criados com o Visual Studio 2012
Se a aplicação foi criada no Visual Studio 2012, provavelmente, utilizou Olá identidade e tooconfigure da ferramenta de acesso da aplicação. Também é provável que está a utilizar Olá [validar o registo de nome de emissor (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Olá VINR é responsável pela manutenção informações sobre fornecedores de identidade fidedigna (Azure AD) e as chaves de Olá utilizadas tokens toovalidate emitidos por-los. Olá VINR também torna tooautomatically fácil atualização Olá chave informações armazenadas num ficheiro Web. config, transferindo Olá mais recente Federação documento de metadados associado com o seu diretório, a verificar se a configuração de Olá está desatualizada com Olá mais recente documento e atualização Olá aplicação toouse Olá nova chave conforme necessário.

Se tiver criado a sua aplicação utilizar qualquer um dos exemplos de código Olá ou documentação instruções fornecida pela Microsoft, a lógica de rollover de chave Olá já está incluída no seu projeto. Vai notar que o código de Olá abaixo já existe no seu projeto. Se a aplicação ainda não tiver esta lógica, siga os passos de Olá abaixo tooadd de-lo e tooverify que está a funcionar corretamente.

1. No **Explorador de soluções**, adicione uma referência toohello **System** assemblagem de projecto adequadas Olá.
2. Abra Olá **Global.asax.cs** de ficheiros e adicione o seguinte Olá utilizando as diretivas de:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Adicionar Olá seguinte método toohello **Global.asax.cs** ficheiro:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Invocar Olá **RefreshValidationSettings()** método Olá **Application_Start()** método **Global.asax.cs** conforme mostrado:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Depois de ter seguido estes passos, será atualizado com informações mais recentes do Olá do documento de metadados de Federação Olá, incluindo chaves mais recentes Olá Web. config da sua aplicação. Esta atualização irá ocorrer sempre que o conjunto aplicacional recicla no IIS; Por predefinição, IIS está definido toorecycle aplicações cada 29 horas.

Siga os passos de Olá abaixo tooverify lógica de rollover de chave Olá está a funcionar.

1. Depois de ter verificado que a aplicação está a utilizar código Olá acima, abra Olá **Web. config** de ficheiros e navegue toohello  **<issuerNameRegistry>**  bloco, especificamente procura Olá seguir algumas linhas:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. No Olá  **<add thumbprint=””>**  definição, alterar o valor do thumbprint Olá ao substituir qualquer caráter com outro. Guardar Olá **Web. config** ficheiro.
3. Criar aplicação Olá e volte a executar. Se pode concluir o processo de início de sessão Olá, a aplicação com êxito é atualizar a chave de Olá transferindo informações Olá necessário do documento de metadados de Federação do diretório. Se estiver a ter problemas em iniciar sessão, certifique-se de alterações de Olá na sua aplicação estão corretas ao ler Olá [tooYour adicionar início de sessão na aplicação do Web utilizar o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tópico, ou transferir e inspecionar o seguinte código de exemplo de Olá: [ Aplicação multi-inquilino de nuvem do Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Aplicações Web de proteger os recursos e criados com o Visual Studio 2008 ou 2010 e a v 1.0 do Windows Identity Foundation (WIF) para o .NET 3.5
Se criou uma aplicação no v 1.0 do WIF, não há nenhuma atualização de tooautomatically mecanismo fornecido toouse de configuração da sua aplicação uma nova chave.

* *A forma mais fácil* utilizar ferramentas de FedUtil Olá incluída no Olá WIF SDK, que pode obter documento de metadados Olá mais recente e atualizar a configuração.
* Atualize o seu too.NET aplicação 4.5, que inclui a versão mais recente do Olá do WIF localizado no espaço de nomes de sistema de Olá. Em seguida, pode utilizar Olá [validar o registo de nome de emissor (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform as atualizações automáticas de configuração da aplicação Olá.
* Efetue um rollover manual de acordo com as instruções de Olá no fim de Olá deste documento de orientação.

Instruções toouse Olá FedUtil tooupdate a configuração:

1. Certifique-se de que tem Olá WIF v 1.0 SDK instalado no computador de desenvolvimento para o Visual Studio 2008 ou 2010. Pode [transferi-lo a partir daqui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se que ainda não instalou-lo.
2. No Visual Studio, abra a solução de Olá e, em seguida, clique no projeto aplicável Olá e selecione **atualizar os metadados de Federação**. Se esta opção não estiver disponível, FedUtil e/ou Olá WIF v 1.0 do SDK não foi instalado.
3. A partir da linha de comandos Olá, selecione **atualização** toobegin atualizar os metadados de Federação. Se tiver um ambiente de servidor acesso toohello onde está alojada aplicação Olá, opcionalmente, pode utilizar do FedUtil [Programador de atualização automática de metadados](https://msdn.microsoft.com/library/ee517272.aspx).
4. Clique em **concluir** processo de atualização de Olá toocomplete.

### <a name="other"></a>As aplicações Web / APIs proteger os recursos a utilizar quaisquer outras bibliotecas de manualmente implementar qualquer um dos Olá suportados ou protocolos
Se estiver a utilizar alguns outra biblioteca ou manualmente implementado qualquer um dos protocolos Olá suportado, terá de biblioteca de Olá tooreview ou o tooensure de implementação que Olá chave a ser obtida a partir do documento de identificação de OpenID Connect Olá ou Olá documento de metadados de Federação. Toocheck unidirecional para isto é toodo uma pesquisa no seu código ou código da biblioteca de Olá para quaisquer chamadas documento de identificação do tooeither Olá OpenID ou documento de metadados de Federação Olá.

Se a chave que estão a ser armazenados algures ou codificado na sua aplicação, pode manualmente obter chave Olá e atualize-lo em conformidade por efetuar um rollover manual de acordo com as instruções de Olá no fim de Olá deste documento de orientação. **É vivamente encouraged que melhoram o rollover automático de toosupport aplicação** utilizar qualquer um dos Olá contorno na interrupções futuras do artigo tooavoid e overhead se aproxima se o Azure AD aumenta a cadência da ou tem um rollover de fora de banda de emergência.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Como tootest sua toodetermine aplicação se serão afetada
Pode validar se a aplicação suporta o rollover de chave automático ao descarregar scripts Olá e seguir instruções Olá [este repositório do GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Como tooperform um rollover manual se a aplicação não suporta o rollover automático
Se a aplicação **não** suporta rollover automático, terá tooestablish um processo que periodicamente monitores do Azure AD da assinatura de chaves e efetua um rollover manual em conformidade. [Este repositório do GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contém scripts e instruções sobre como toodo isto.

