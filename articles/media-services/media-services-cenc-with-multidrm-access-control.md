---
title: "CENC com múltipla DRM e controlo de acesso: uma estrutura de referência e a implementação no Azure e Azure dos Media Services | Microsoft Docs"
description: "Saiba mais sobre como toolicensing Olá Microsoft® uniforme de transmissão em fluxo cliente transferências Kit."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>CENC com Controlo de Acesso e Multi-DRM: Uma Estrutura de Referência e Implementação no Azure e Serviços de Multimédia do Azure
 
## <a name="introduction"></a>Introdução
É bem conhecidos que é uma tarefa complexa toodesign e criar um subsistema DRM para um OTT ou online de solução de transmissão em fluxo. Sendo uma comuns práticas para operadores online fornecedores vídeo toooutsource fornecedores de serviços esta parte toospecialized DRM. objetivo de Olá deste documento é toopresent uma estrutura de referência e a implementação do subsistema DRM ponto-a-ponto OTT ou solução de transmissão em fluxo online.

leitores de Olá direcionado deste documento são engenheiros de trabalhar no subsistema DRM de OTT ou transmissão em fluxo/várias-screen soluções online ou qualquer leitores interessados no subsistema DRM. pressuposto Olá é que os leitores encontram familiarizados com pelo menos uma das tecnologias DRM Olá no mercado Olá, tais como PlayReady, Widevine, do FairPlay ou Adobe acesso.

Por DRM, iremos também incluem CENC (encriptação comum) com múltipla DRM. Uma tendência principais na transmissão em fluxo online e do setor OTT é toouse CENC com várias-native-DRM em várias plataformas de cliente, que é um bit da tendência de anterior Olá da utilização de um único DRM e o cliente SDK em várias plataformas de cliente. Quando utilizar CENC com várias native DRM tanto PlayReady como Widevine são encriptados de acordo com Olá [encriptação comum (ISO/IEC 23001 7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) especificação.

vantagens de Olá de CENC com múltipla DRM são os seguintes:

1. Reduz o custo de uma vez que o processamento de encriptação único é utilizado direcionada para plataformas diferentes com o respetivos DRMs nativos; de encriptação
2. Reduz o custo de Olá de gerir recursos encriptados, uma vez que é necessária apenas uma única cópia dos recursos encriptadas;
3. Elimina o custo de licenciamento, uma vez que o cliente DRM nativo Olá é normalmente livre na respetiva plataforma nativa de clientes DRM.

Microsoft foi um promoter Active Directory de DASH e CENC juntamente com alguns jogadores principais da indústria. Serviços de suporte de dados do Microsoft Azure tem sido fornecer suporte de DASH e CENC. Para anúncios recentes, consulte blogues do Mingfei: [serviços de entrega de licença de anunciar Widevine da Google nos Media Services do Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/), e [empacotamento Widevine da Google para entrega de adiciona de Media Services do Azure fluxo de múltipla DRM](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).  

### <a name="overview-of-this-article"></a>Descrição geral deste artigo
objetivo Olá deste artigo inclui os seguintes Olá:

1. Fornece uma conceção de referência do subsistema DRM utilizando CENC com múltipla DRM;
2. Fornece uma implementação de referência na plataforma de Media Services do Microsoft Azure/Azure;
3. Descreve alguns tópicos de design e implementação.

Artigo de Olá, "múltipla DRM" abrange seguinte Olá:

1. Microsoft PlayReady
2. Widevine da Google
3. Apple FairPlay 

Olá tabela seguinte resume as aplicações de plataforma nativo/nativo Olá e browsers suportados por cada DRM.

| **Plataforma de cliente** | **Suporte nativo DRM** | **Browser/aplicação** | **Formatos de transmissão em fluxo** |
| --- | --- | --- | --- |
| **TVs inteligentes, o operador STBs, OTT STBs** |PlayReady principalmente, e/ou Widevine e/ou outras |Linux, Opera, WebKit, outros |Vários formatos |
| **Dispositivos Windows 10 (Windows PC, Windows Tablets, Windows Phone, Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |TRAÇO (para HLS, PlayReady não é suportado)<br/><br/>DASH, transmissão em fluxo uniforme (para HLS, PlayReady não é suportado) |
| **Dispositivos Android (telemóvel, Tablet, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), os clientes dos X e Apple TV** |FairPlay |Safari 8 + /Safari/Chrome EME |HLS |


Tendo em consideração Olá atual estado de implementação para cada DRM um serviço, normalmente, será útil tooimplement 2 ou 3 DRMs toomake se resolver todos os tipos de Olá dos pontos finais no Olá melhor forma.

Existe um compromisso entre complexidade Olá de lógica de serviço Olá e complexidade Olá no Olá cliente lado tooreach um determinado nível de utilizador experiência Olá de vários clientes.

toomake a seleção, tenha em atenção estes factos:

* PlayReady nativamente está implementado em cada dispositivo de Windows, em alguns dispositivos Android e disponível através do software SDKs em praticamente qualquer plataforma
* Widevine nativamente é implementada em todos os dispositivos Android, no Chrome e outros dispositivos
* FairPlay está disponível apenas em iOS e os clientes Mac OS ou através do iTunes.

Por isso, seria um múltipla DRM típica:

* Opção 1: PlayReady e Widevine
* Opção 2: PlayReady, Widevine e FairPlay

## <a name="a-reference-design"></a>Um design de referência
Nesta secção, iremos irá apresentar um design de referência que é agnóstico relativamente tootechnologies utilizado tooimplement-lo.

Um subsistema DRM pode conter Olá os seguintes componentes:

1. Gestão de chaves
2. Empacotamento DRM
3. Entrega de licença de DRM
4. Verificação de elegibilidade
5. Autenticação/autorização
6. Leitor
7. Origem/CDN

Olá diagrama seguinte ilustra Olá elevado nível a interação entre componentes Olá um subsistema DRM.

![Subsistema com CENC DRM](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Existem três básicas "camadas" na estrutura de Olá:

1. Camada de back-office (em negra) que não são expostos externamente;
2. Camada de "DMZ" (azul) que contém todos os pontos finais de Olá destinado ao público;
3. Camada da Internet de pública (blue leve) que contém o CDN e jogadores com o tráfego através da Internet pública.

Deverá haver uma ferramenta de gestão de conteúdo para controlar a proteção de DRM, independentemente de já é encriptação estática ou dinâmica. devem incluir entradas de Olá para a encriptação de DRM:

1. Conteúdo de vídeo MBR;
2. Chave de conteúdo;
3. URL de aquisição de licença.

Durante o período de reprodução, o fluxo de nível elevado Olá é:

1. Utilizador é autenticado;
2. O token de autorização é criado para o utilizador Olá;
3. Conteúdo DRM protegido (manifesto) é transferido tooplayer;
4. Leitor submete aquisição pedido toolicense servidores de licenças de juntamente com o ID de chave e a autorização token.

Antes de mover toohello seguinte tópico, algumas palavras sobre Olá design da gestão de chaves.

| **ContentKey – ativo** | **Cenário** |
| --- | --- |
| 1 – 1 |caso mais simples de Olá. Fornece controlo finest Olá. Mas isto normalmente resulta em custo de entrega de licença Olá mais elevado. No mínimo licença de um pedido é necessário para cada recurso protegido. |
| 1-para-muitos |Pode utilizar Olá mesmo conteúdo da chave para vários recursos. Por exemplo, para todos os elementos de Olá num grupo lógico como um género ou um subconjunto do género (ou Gene de filmes), pode utilizar uma única chave de conteúdo. |
| Muitos-para-1 |Várias chaves de conteúdo são necessárias para cada recurso. <br/><br/>Por exemplo, se precisar de tooapply dinâmica proteção CENC com múltipla DRM para MPEG-DASH e encriptação AES-128 dinâmica para HLS, tem duas separadas conteúdas chaves, cada um com o seu próprio ContentKeyType. (Para a chave de conteúdo Olá utilizado para proteção de CENC dinâmica, ContentKeyType.CommonEncryption devem ser utilizados, enquanto para Olá conteúdo deve ser utilizada a chave utilizada para encriptação AES-128 dinâmica, ContentKeyType.EnvelopeEncryption.)<br/><br/>Noutro exemplo, na proteção CENC do TRAÇO conteúdo, em teoria, uma chave de conteúdo pode ser utilizado tooprotect de transmissão e outra sequência de áudio tooprotect de chave de conteúdo. |
| Muitos – demasiado-muitos |Combinação de Olá acima dois cenários: mesmo recurso "grupo de" Olá, um conjunto de conteúdos, as chaves são utilizadas para cada um dos vários recursos no Olá. |

Outro fator importante tooconsider é a utilização de Olá de licenças persistentes e não persistente.

Por que razão são estas considerações importantes?

Têm de entrega de toolicense impacto direto custo se utilizar a nuvem pública para a entrega de licença. Vejamos Olá seguir dois tooillustrate de cenários de design diferentes:

1. Uma subscrição mensal: utilizar licença persistente e mapeamento de recurso de chave de conteúdo de 1-para-muitos. Por exemplo, para todos os Olá menores filmes, utilizamos uma única chave de conteúdo para a encriptação. Neste caso:

    Total de licenças de # pedidas para todos os menores filmes/dispositivo = 1
2. Uma subscrição mensal: utilizar a licença não persistentes e mapeamento de 1 para 1 entre os recursos e a chave de conteúdo. Neste caso:

    Total de licenças de # pedidas para todos os menores filmes/dispositivo = [observadas de filmes #] x [sessões #]

Como pode facilmente, Olá dois diferentes estruturas resultam numa licença muito diferente pedido, por conseguinte, padrões de entrega de licença custo se o serviço de entrega de licença é fornecido por uma nuvem pública como os serviços de suporte de dados do Azure.

## <a name="mapping-design-tootechnology-for-implementation"></a>Tootechnology de estrutura de mapeamento para implementação
Em seguida, iremos mapear nosso tootechnologies design genérico na plataforma de Media Services do Microsoft Azure/Azure, especificando que toouse de tecnologia para cada bloco modular.

Olá tabela seguinte mostra o mapeamento de Olá:

| **Bloco modular** | **Tecnologia** |
| --- | --- |
| **Leitor** |[Media Player do Azure](https://azure.microsoft.com/services/media-services/media-player/) |
| **Fornecedor de identidade (IDP)** |Azure Active Directory |
| **Serviço de Token seguro (STS)** |Azure Active Directory |
| **Fluxo de trabalho de proteção de DRM** |Proteção dinâmica de serviços de multimédia do Azure |
| **Entrega de licença DRM** |1. Licença entrega (PlayReady, Widevine, do FairPlay), de serviços de multimédia do Azure ou <br/>2. Servidor de licenças de Axinom, <br/>3. Servidor de licenças PlayReady personalizado |
| **Origem** |Ponto final de transmissão em fluxo de serviços de multimédia do Azure |
| **Gestão de chaves** |Não é necessária para a implementação de referência |
| **Gestão de conteúdo** |Uma aplicação de consola c# |

Por outras palavras, o fornecedor de identidade (IDP) e proteger o Token serviço (STS) será do Azure AD. Para o leitor, utilizamos [API do Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). Os Media Services do Azure e o leitor de multimédia do Azure suportam DASH e CENC com múltipla DRM.

Olá seguinte diagrama mostra Olá estrutura geral e de fluxo com Olá acima mapeamento de tecnologia.

![CENC no AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

Na ordem tooset segurança encriptação CENC dinâmica, a ferramenta de gestão de conteúdo de Olá utilizará Olá seguintes entradas:

1. Abrir conteúdo;
2. Chave de conteúdo da chave geração/gestão;
3. URL de aquisição de licença;
4. Uma lista de informações do Azure AD.

Olá resultado da ferramenta de gestão de conteúdo de Olá será:

1. ContentKeyAuthorizationPolicy que contém a especificação de Olá na forma como a entrega de licença verifica um token JWT e especificações de licença da DRM;
2. AssetDeliveryPolicy que contém as especificações na transmissão em fluxo formato, proteção DRM e URLs de aquisição de licença.

Durante o tempo de execução, o fluxo de Olá é como abaixo:

1. Após a autenticação de utilizador, é gerado um token JWT;
2. Uma das afirmações de Olá incluídas no token JWT de Olá é afirmação "grupos" que contém o ID de objeto de grupo Olá de "EntitledUserGroup". Esta afirmação será utilizada para transmitir "verificar a elegibilidade".
3. Manifesto de cliente de transferências de leitor de um CENC conteúdo protegido e "verá" seguintes Olá:

   1. ID da chave
   2. o conteúdo de Olá é CENC protegido,
   3. URL de aquisição de licença.
4. Leitor faz um pedido de aquisição de licença com base no Olá browser/DRM suportado. No pedido de aquisição de licença de Olá, ID de chave e Olá JWT, também irá ser submetido token. Serviço de entrega de licença irá verificar token JWT de Olá e afirmações de Olá contidas antes de emitir Olá necessário licença.

## <a name="implementation"></a>Implementação
### <a name="implementation-procedures"></a>Procedimentos de implementação
implementação de Olá irá incluir Olá os seguintes passos:

1. Preparar o teste asset(s): codificar/pacote uma teste vídeo toomulti múltipla fragmentada MP4 nos Media Services do Azure. Este elemento não é DRM protegido. Proteção de DRM será efetuada pela proteção dinâmica mais tarde.
2. Criar chave ID e conteúdo chave (e opcionalmente de seed chave). Para o nosso objetivo, sistema de gestão de chaves não é necessária uma vez que vamos são lidar com apenas um único conjunto de ID e a chave de conteúdo para alguns dos recursos de teste; da chave
3. Utilize serviços de entrega de API do AMS tooconfigure múltipla DRM licença para o recurso de teste de Olá. Se estiver a utilizar servidores de licenças personalizados pela sua empresa ou fornecedores da sua empresa em vez dos serviços de licenciamento no Media Services do Azure, pode ignorar este passo e especificar os URLs de aquisição de licença no passo de Olá para configurar a entrega de licença. API de AMS é necessário toospecify detalhada de algumas configurações, tais como restrição de política de autorização, licença modelos de resposta para diferentes serviços de licença da DRM, etc. Neste momento, Olá portal do Azure não ainda fornecer Olá necessário da IU para esta configuração. Pode encontrar informações de nível de API e exemplo de código no documento de Leonor Kornich: [utilizando PlayReady e/ou Widevine a encriptação comum dinâmica](media-services-protect-with-drm.md).
4. Utilize a política de entrega de elemento do AMS API tooconfigure para o recurso de teste de Olá. Pode encontrar informações de nível de API e exemplo de código no documento de Leonor Kornich: [utilizando PlayReady e/ou Widevine a encriptação comum dinâmica](media-services-protect-with-drm.md).
5. Criar e configurar um inquilino do Azure Active Directory no Azure;
6. Crie algumas contas de utilizador e grupos no seu inquilino do Azure Active Directory: deve criar, pelo menos, "EntitledUser" de grupo e adicionar um grupo de toothis do utilizador. Os utilizadores deste grupo serão passaram a verificação de elegibilidade na aquisição de licença e não os utilizadores deste grupo não conseguirá efetuar verificação de autenticação toopass e não será capaz de tooacquire qualquer licença. Facto de ser membro deste grupo de "EntitledUser" é uma afirmação de necessário "nos grupos" no Olá JWT token emitido pelo Azure AD. Este requisito de afirmação deve ser especificado na configuração de passo de serviços de entrega de licença de múltipla DRM.
7. Crie uma aplicação ASP.NET MVC que irá alojar o leitor de vídeo. Esta aplicação ASP.NET vai ser protegida com autenticação de utilizador no inquilino do Azure Active Directory de Olá. Afirmações adequadas serão incluídas em tokens de acesso de Olá obtidos após a autenticação de utilizador. Para este passo, recomenda-se OpenID Connect API. É necessário Olá tooinstall pacotes NuGet os seguintes:
   * Pacote de instalação Microsoft.Azure.ActiveDirectory.GraphClient
   * Pacote de instalação Microsoft.Owin.Security.OpenIdConnect
   * Pacote de instalação Microsoft.Owin.Security.Cookies
   * Pacote de instalação Microsoft.Owin.Host.SystemWeb
   * Pacote de instalação Microsoft.IdentityModel.Clients.ActiveDirectory
8. Criar um leitor utilizando [API do Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). [ProtectionInfo API do Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/) permite-lhe toospecify que toouse de tecnologia DRM em várias plataformas DRM.
9. Matriz de teste:

| **DRM** | **Browser** | **Resultado para o utilizador realizada** | **Resultado para o utilizador anular realizada** |
| --- | --- | --- | --- |
| **PlayReady** |Limite de MS ou IE11 no Windows 10 |Concluída com êxito |Falhar |
| **Widevine** |Chrome no Windows 10 |Concluída com êxito |Falhar |
| **FairPlay** |TBD | | |

George Trifonov da equipa de serviços de suporte de dados do Azure tem de escrever um blogue fornecendo passos de detalhado na configuração do Azure Active Directory para uma aplicação de leitor de ASP.NET MVC: [integrar o Azure suporte de dados de serviços da OWIN MVC baseada em aplicações com o Azure Active Directory e restringir conteúdo de entrega de chave com base em afirmações JWT](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George também ter escrito um blogue no [autenticação de token JWT nos Media Services do Azure e a encriptação dinâmica](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). E Eis a [em integração do Azure AD com a entrega de chave de Media Services do Azure](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Para informações sobre o Azure Active Directory:

* Pode encontrar informações de Programador no [guia para programadores Directory Active do Azure](../active-directory/active-directory-developers-guide.md).
* Pode encontrar informações de administrador no [administrar o diretório do Azure AD](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Alguns gotchas numa implementação
Existem algumas "gotchas" na implementação de Olá. Hopefully Olá lista de "gotchas" a seguir pode ajudá-lo caso se depare com problemas de resolução de problemas.

1. **Emissor** URL deve terminar com **"/"**.  

    **Público-alvo** deve ser Olá ID de cliente da aplicação de leitor e deverá ainda adicionar **"/"** no fim de Olá do URL do emissor Olá.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    No [JWT descodificador](http://jwt.calebb.net/), deverá ver **aud** e **iss** como abaixo no token JWT de Olá:

    ![gotcha 1ª](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Adicione aplicação toohello de permissões no AAD (no separador de configuração da aplicação Olá). Isto é necessário para cada aplicação (versões de locais e implementadas).

    ![2nd gotcha](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Utilize o emissor de direito de Olá na como configurar a proteção de CENC dinâmica:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    seguinte Olá não irá funcionar:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Olá GUID é o ID de inquilino do AAD Olá Olá GUID pode ser encontrada no pop-up de pontos finais no portal do Azure.
4. Associação ao grupo de conceder privilégios de afirmações. Certifique-se no ficheiro de manifesto de aplicação do AAD, temos seguinte Olá

    "groupMembershipClaims": "All", (valor predefinido de Olá é nulo)
5. Definição adequada TokenType ao criar requisitos de restrição.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Uma vez que adicionar suportar JWT (AAD) Ademais tooSWT (ACS), o predefinido Olá TokenType é TokenType.JWT. Se utilizar SWT/ACS, tem de definir tooTokenType.SWT.

## <a name="additional-topics-for-implementation"></a>Tópicos adicionais para a implementação
Em seguida, irá detetar uss alguns tópicos adicionais no nosso design e implementação.

### <a name="http-or-https"></a>HTTP ou HTTPS?
Olá aplicação de leitor de ASP.NET MVC criámos têm de suportar seguinte Olá:

1. Autenticação de utilizador através do Azure AD que precisa de toobe em HTTPS;
2. Troca de tokens JWT entre cliente e o Azure AD que precisa de toobe em HTTPS;
3. Aquisição de licença da DRM pelo cliente de Olá que é necessário toobe em HTTPS se a entrega de licença é fornecida pelos serviços de suporte de dados do Azure. Obviamente, PlayReady suite de produto não mandatar HTTPS para entrega de licença. Se o servidor de licenças PlayReady está fora do Media Services do Azure, pode ser utilizado por HTTP ou HTTPS.

Por conseguinte, Olá aplicação do leitor ASP.NET utilizará HTTPS como melhor prática. Isto significa Olá que Azure Media Player será uma página em HTTPS. No entanto, para transmissão em fluxo preferir HTTP, por conseguinte, é necessário tooconsider misto problema conteúdo.

1. Browser não permitem o conteúdo misto. Mas permitem plug-ins, como o Silverlight e OSMF Plug-in para uniforme e travessão. Conteúdo misto é um problema de segurança: trata-se devido a ameaça de toohello de Olá capacidade tooinject JS maliciosos que pode provocar Olá toobe de dados de cliente em risco.  Browsers bloquear este por predefinição, não sendo até ao momento Olá toowork de forma apenas à volta no lado do servidor (origem) de Olá, tooallow todos os domínios (independentemente https ou http). Isto é provavelmente não é uma boa ideia.
2. Iremos deve evitar conteúdo misto: ambos utilizam HTTP ou ambos utilizam HTTPS. Quando a reprodução do conteúdo misto, silverlightSS técnico requer limpar um aviso de conteúdo misto. técnico de flashSS processa conteúdo misto sem aviso conteúdo misto.
3. Se o ponto final de transmissão em fluxo foi criado antes de Agosto de 2014, não suporta HTTPS. Neste caso,. Crie e utilize um novo ponto de final de transmissão em fluxo para HTTPS.

Numa implementação de referência de Olá, para conteúdo DRM protegido, aplicações e de transmissão em fluxo serão em HTTTPS. Para abrir conteúdos, leitor Olá não necessita de autenticação ou de licença, pelo que terá de Olá liberty toouse o HTTP ou HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Azure Active Directory que o rollover da chave de assinatura
Este é um tootake ponto importante em consideração da sua implementação. Se não considere o seguinte na sua implementação, sistema Olá concluída, eventualmente, deixará de trabalho completamente dentro de um máximo de 6 semanas.

Azure AD utiliza uma confiança de tooestablish padrão da indústria entre si próprio e aplicações através do Azure AD. Especificamente, o Azure AD utiliza uma chave de assinatura que é composta por um par de chaves público e privado. Quando o Azure AD cria um token de segurança que contenha informações sobre o utilizador Olá, este token é assinada pelo Azure AD utilizando a respetiva chave privada antes de ser enviada aplicação de back-toohello. tooverify Olá token é válido e, na verdade, teve origem do Azure AD, aplicação Olá necessário validar a assinatura do token de Olá utilizando a chave pública Olá exposto pelo Azure AD que está contido no documento de metadados de Federação do inquilino Olá. Esta chave pública – e Olá chave a partir da qual deriva de assinatura – são Olá um mesmo utilizado para todos os inquilinos no Azure AD.

Informações detalhadas sobre o rollover da chave do Azure AD podem ser encontrada no documento de Olá: [informações importantes sobre o Rollover de chave de assinatura no Azure AD](../active-directory/active-directory-signing-key-rollover.md).

Entre Olá [par de chaves públicas-privadas](https://login.microsoftonline.com/common/discovery/keys/),

* a chave privada Olá é utilizada pelo Azure Active Directory toogenerate um token JWT;
* chave pública Olá é utilizado por uma aplicação, tais como serviços de entrega de licença DRM no token JWT do AMS tooverify Olá;

Para fins de segurança, o Azure Active Directory roda periodicamente este certificado (todas as semanas 6). Em caso de falhas de segurança, o rollover da chave Olá pode ocorrer a qualquer altura. Por conseguinte, serviços de entrega de licença de Olá AMS necessária a chave de público de Olá de tooupdate utilizado como o Azure AD roda par de chaves Olá, caso contrário, a autenticação com token na AMS irá falhar e não será emitida nenhuma licença.

Isto é conseguido através da definição TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument quando configurar os serviços de entrega de licença DRM.

Olá fluxo do token JWT está abaixo:

1. Azure AD irá emitir o token JWT de Olá com chave privada atual para um utilizador autenticado; Olá
2. Quando um leitor vê um CENC com conteúdo de múltipla DRM protegido, irá localizar primeiro o token JWT de Olá emitido pelo Azure AD.
3. leitor de Olá envia o pedido de aquisição de licença com os serviços de entrega do Olá JWT token toolicense em AMS;
4. Serviços de entrega de licença de Olá AMS irão utilizar a chave pública atual válido Olá do token JWT do Azure AD tooverify Olá, antes de emitir licenças.

Serviços de entrega de licença DRM serão sempre ser a verificar Olá atual/uma chave pública válida do Azure AD. chave pública Olá apresentada pelo Azure AD será chave Olá utilizado para verificar um token JWT emitido pelo Azure AD.

E se o rollover da chave de Olá acontece depois do AAD gera um token JWT, mas antes de Olá JWT token é enviado pelo jogadores tooDRM licença entrega serviços no AMS para verificação?

Porque uma chave poderá ser revertida a qualquer momento, não há sempre mais do que uma chave pública válida disponíveis no documento de metadados de Federação Olá. Entrega de licença de Media Services do Azure pode utilizar qualquer um dos Olá chaves especificado no documento de Olá, uma vez que uma chave em breve, poderá ser revertida outro pode ser sua substituição e assim sucessivamente.

### <a name="where-is-hello-access-token"></a>Onde é Olá Token de acesso?
Se observar como uma aplicação web chama uma aplicação de API em [identidade da aplicação com a concessão de credenciais do OAuth 2.0 cliente](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), o fluxo de autenticação de Olá é como abaixo:

1. Um utilizador é iniciada no tooAzure AD na aplicação web de Olá (consulte Olá [Web Browser tooWeb aplicação](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. ponto final de autorização de Olá do Azure AD redireciona Olá aplicação de cliente da back toohello de agente de utilizador com um código de autorização. agente de utilizador Olá devolve URI de redirecionamento de autorização código toohello cliente da aplicação.
3. aplicação de web de Olá tem tooacquire um token de acesso para que possa autenticar toohello web API e obter o recurso de Olá assim o desejar. Torna o ponto final de token tooAzure um pedido do AD, fornecendo credenciais Olá, ID de cliente e URI de ID da aplicação de web da API. Apresenta tooprove de código de autorização de Olá esse Olá utilizador consentiu.
4. Azure AD autentica aplicação Olá e devolve um token de acesso JWT que é utilizado toocall Olá web API.
5. Através de HTTPS, a aplicação de web de Olá utiliza Olá devolvido Olá de token tooadd JWT acesso cadeia JWT com uma designação de "Portador" no cabeçalho de autorização de Olá de API do web toohello Olá pedido. API web do Olá, em seguida, valida o token JWT de Olá e se a validação for bem sucedida, devolve Olá pretendido recursos.

Neste fluxo "identidade da aplicação", a API web do Olá confianças que Olá web aplicação Olá autenticado o utilizador. Por este motivo, este padrão é chamado um subsistema fidedigno. Olá [diagrama nesta página](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) descreve como o funciona de fluxo de concessão de códigos de autorização.

Na aquisição de licença com o token restrição, iremos estiver a seguir Olá mesmo padrão do subsistema fidedigna. E o serviço de entrega de licença Olá nos Media Services do Azure é o recurso de web API de Olá, Olá "recursos de back-end" tooaccess necessita de uma aplicação web. Por isso, onde está o token de acesso de Olá?

Realmente, vamos obter token de acesso do Azure AD. Após a autenticação com êxito do utilizador, é devolvido o código de autorização. código de autorização de Olá, em seguida, é utilizado, juntamente com o ID e a aplicação de chave de cliente, tooexchange token de acesso. E o token de acesso de Olá para aceder a uma aplicação de "ponteiro" apontar ou que representa o serviço de entrega de licença de Media Services do Azure.

Vamos precisar tooregister e configurar Olá "ponteiro" aplicação no Azure AD, seguindo os passos de Olá abaixo:

1. No inquilino Olá do Azure AD

   * Adicione uma aplicação (recurso) com o URL de início de sessão:

   https://[resource_name].azurewebsites.NET/ e

   * URL de ID da aplicação:

   https://[aad_tenant_name].onmicrosoft.com/[resource_name];
2. Adicionar uma nova chave para a aplicação de recursos de Olá;
3. Atualizar o ficheiro de manifesto de aplicação Olá, para que a propriedade de groupMembershipClaims Olá tem Olá seguinte valor: "groupMembershipClaims": "All",  
4. Na aplicação do Azure AD Olá apontar toohello leitor de aplicação web, na secção de Olá "aplicações tooother de permissões", adicione Olá recursos da aplicação que foi adicionada no passo 1 acima. Em "permissões delegadas" verificar "Acesso [resource_name]" marca de verificação. Isto dá-permissão de aplicação web de Olá toocreate tokens de acesso para aceder à aplicação do recurso Olá. Deve efetuar este procedimento para a versão local e implementado da aplicação web de Olá se estiver a desenvolver com a aplicação de web do Visual Studio e o Azure.

Por conseguinte, token JWT de Olá emitido pelo Azure AD é, de facto, token de acesso de Olá para aceder a este recurso de "ponteiro".

### <a name="what-about-live-streaming"></a>E vai em direto transmissão em fluxo?
No Olá acima, nosso debate tem sido concentrar-se em ativos a pedido. E vai transmissão em direto?

Olá boas notícias é que pode utilizar exatamente Olá mesmo design e implementação para proteger a transmissão em fluxo em direto nos Media Services do Azure, por encará-los asset Olá associado um programa como um "recurso VOD".

Especificamente, é bem conhecido que toodo em direto de transmissão em fluxo em Media Services do Azure, terá de toocreate um canal, em seguida, um programa no canal de Olá. programa de Olá toocreate, terá de toocreate um recurso que irá conter o arquivo em direto de Olá programa Olá. Na ordem tooprovide CENC com proteção múltipla DRM de conteúdo em direto Olá, tudo o que precisa toodo, é tooapply Olá mesmo elemento de toohello de processamento de configuração/como se era um "recurso VOD" antes de iniciar o programa de Olá.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>O que sobre servidores de licenças fora de Media Services do Azure?
Muitas vezes, os clientes podem tenham investido em licença farm de servidores tem os seus próprios dados center ou alojado por fornecedores de serviços DRM. Felizmente, proteção de conteúdos do serviços de suporte de dados do Azure permite-lhe toooperate no modo de híbrida: conteúdo alojado e protegidas dinamicamente Media Services do Azure, enquanto licenças DRM são fornecidas pelos servidores fora Media Services do Azure. Neste caso, existem Olá seguintes considerações de alterações:

1. Olá serviço de Token seguro necessidades tooissue tokens que são aceitáveis e podem ser verificados pelo farm de servidores de licenciamento Olá. Por exemplo, servidores de licenças Widevine Olá fornecidas pelo Axinom requer um token JWT específico que contém "mensagem elegibilidade". Por conseguinte, terá de toohave tooissue um STS esse token JWT. os autores de Olá concluir essa uma implementação e para encontrar os detalhes de Olá Olá seguir o documento no [Centro de documentação do Azure](https://azure.microsoft.com/documentation/): [utilizando Axinom toodeliver Widevine licenças tooAzure Media Services](media-services-axinom-integration.md).
2. Já não necessita de tooconfigure entrega serviço de licença (ContentKeyAuthorizationPolicy) nos serviços de suporte de dados do Azure. O que precisa é de toodo tooprovide Olá licença aquisição URLs (para PlayReady, Widevine e do FairPlay) quando configurar AssetDeliveryPolicy configurar CENC com múltipla DRM.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>E se quiser toouse um STS personalizado?
Pode existir algumas razões que um cliente pode escolher toouse um STS personalizada (proteger o serviço de tokens) para fornecer os tokens JWT. Alguns deles são:

1. Olá fornecedor de identidade (IDP) utilizado pelo cliente de Olá não suporta STS. Neste caso, um STS personalizado podem ser uma opção.
2. cliente de Olá pode precisar de mais flexível ou mais rígido controlo integrar STS de subscritor do cliente, sistema de faturação. Por exemplo, um operador MVPD poderão oferecer vários pacotes de subscritor OTT como premium e básica, desporto, operador de Olá etc. poderá ser útil toomatch Olá afirmações num token com o pacote de um subscritor para que apenas o conteúdo no pacote direita Olá é disponibilizado. Neste caso, um STS personalizado fornece Olá necessário flexibilidade e controlo.

Duas alterações necessário toobe efetuada ao utilizar um STS personalizado:

1. Quando configurar o serviço de entrega de licença para um recurso, tem de chave de segurança de Olá toospecify utilizado para a verificação pelo STS personalizado Olá (mais detalhes abaixo) em vez de chave atual do Olá do Azure Active Directory.
2. Quando é gerado um token JTW, foi especificada uma chave de segurança em vez de chave privada do Olá Olá atual X509 do certificado de no Azure Active Directory.

Existem dois tipos de chaves de segurança:

1. A chave simétrica: Olá a mesma chave é utilizada para gerar e verificar um token JWT;
2. Chave assimétrica: um par de chaves públicas-privadas num certificado é utilizado com a chave privada para encriptar/gerar um JWT token e Olá chave pública para verificar o token de Olá de X509.

#### <a name="tech-note"></a>Nota de técnico
Se utilizar o .NET Framework / c# como a sua plataforma de desenvolvimento, Olá X509 certificado utilizado para a chave de segurança assimétrico tem de ter, pelo menos, 2048 de comprimento de chave. Este é um requisito da classe de Olá System.IdentityModel.Tokens.X509AsymmetricSecurityKey no .NET Framework. Caso contrário, será emitida Olá seguinte exceção:

IDX10630: Olá 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' para a assinatura não pode ser menor que '2048' bits.

## <a name="hello-completed-system-and-test"></a>sistema de Olá concluído e teste
Vamos ajudá-alguns cenários no sistema de ponto a ponto Olá concluída, para que os leitores podem ter um basic "geral" do comportamento de Olá antes de obter uma conta de início de sessão.

Olá aplicação web de leitor e o início de sessão podem ser encontrados [aqui](https://openidconnectweb.azurewebsites.net/).

Se o que precisa é "não integrada" cenário: ativos vídeos alojadas nos serviços de suporte de dados do Azure que tem um desprotegidos ou DRM protegido, mas sem autenticação com token (emitir toowhoever uma licença a solicitá-lo), pode testar sem início de sessão (por mudar tooHTTP esteja as vídeo de transmissão em fluxo através de HTTP).

Se o que precisa é o cenário de integrada de ponto a ponto: ativos vídeos está sob dinâmica DRM a proteção na Media Services do Azure, com autenticação de token e o token JWT gerados pelo Azure AD, tem de toologin.

### <a name="user-login"></a>Início de sessão do utilizador
Ordem tootest Olá ponto-a-ponto integrado DRM sistema, terá de toohave uma "conta de" criado ou adicionado.

Que conta?

Embora o Azure permitisse apenas o acesso os utilizadores da conta Microsoft,-lo agora permite o acesso por utilizadores de ambos os sistemas. Isto foi feito, fazendo com que todos os Olá Azure propriedades de fidedignidade do Azure AD para autenticação, ter a autenticação de utilizadores organizacionais do Azure AD e ao criar uma relação de Federação em que o Azure AD confia sistema de identidade do consumidor do Olá Microsoft conta utilizadores de consumidor tooauthenticate. Como resultado, o Azure AD é tooauthenticate capaz de contas da Microsoft "convidado", bem como contas "nativas" do Azure AD.

Uma vez que o Azure AD confia domínio da conta Microsoft (MSA), pode adicionar as contas de qualquer um dos Olá seguir toohello de domínios personalizado do Azure AD de inquilino e utilizam Olá conta toologin:

| **Nome de domínio** | **Domínio** |
| --- | --- |
| **Domínio de inquilino personalizada do Azure AD** |somename.onmicrosoft.com |
| **Domínio empresarial** |Microsoft.com |
| **Domínio da conta Microsoft (MSA)** |Outlook.com, live.com, hotmail.com |

Poderá contactar qualquer um dos Olá autores toohave uma conta criada ou adicionadas por si.

Seguem-se Olá capturas de ecrã das páginas de início de sessão diferente utilizadas pelas contas de domínio diferente.

**Conta de domínio de inquilino do Azure AD personalizado**: neste caso, verá a página de início de sessão personalizado Olá do domínio de inquilino Olá personalizado do Azure AD.

![Conta de domínio do inquilino personalizada do Azure AD](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Conta de domínio da Microsoft com smart card**: neste caso, verá a página de início de sessão de Olá personalizada ao Microsoft empresarial IT com a autenticação de dois fatores.

![Conta de domínio do inquilino personalizada do Azure AD](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Conta Microsoft (MSA)**: neste caso, consulte a página de início de sessão de Olá da Microsoft Account para consumidores.

![Conta de domínio do inquilino personalizada do Azure AD](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Utilizar extensões de suporte de dados encriptados para PlayReady
Num browser moderno com encriptados multimédia extensões (EME) para PlayReady suporte, tais como browser IE 11 no Windows 8.1 e cópia de segurança e o Microsoft Edge no Windows 10, PlayReady será hello DRM subjacente para EME.

![Utilizar EME para PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

área de leitor escuro Olá é devido facto toohello que PlayReady proteção impede um realizem captura de ecrã de vídeo protegida.

Olá seguinte ecrã mostra os plug-ins de leitor de Olá e suporte MSE/EME.

![Utilizar EME para PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

EME no Microsoft Edge e o IE 11 no Windows 10 permite invocar de [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) em dispositivos Windows 10 que a suportam. PlayReady SL3000 desbloqueia fluxo Olá de conteúdos melhorado premium (4K, HDR, etc.) e modelos de entrega de conteúdo novo (antecipado janela para o conteúdo avançado).

Concentre-se nos dispositivos com Windows hello: PlayReady é Olá apenas DRM no hardware de Olá disponível nos dispositivos do Windows (PlayReady SL3000). Um serviço de transmissão em fluxo pode utilizar PlayReady, através de EME ou através de uma aplicação de UWP e oferecem uma qualidade do vídeo superior com PlayReady SL3000 que outro DRM. Normalmente, 2 mil conteúdo irá fluir pelo Chrome ou Firefox e Olá de 4 K conteúdo através do Microsoft Edge/IE11 ou uma aplicação de UWP no mesmo dispositivo (consoante as definições de serviço e de implementação).

#### <a name="using-eme-for-widevine"></a>Utilizar EME para Widevine
Num browser moderno com suporte para EME/Widevine, por exemplo, o Chrome 41 + no Windows 10, Windows 8.1, Mac OSX Yosemite e o Chrome em Android 4.4.4, Widevine da Google é Olá DRM atrás EME.

![Utilizar EME para Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Tenha em atenção que Widevine não impede um realizem captura de ecrã de vídeo protegida.

![Utilizar EME para Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Utilizadores não realizados
Se um utilizador não é um membro do grupo "Utilizadores denominada", utilizador de Olá não será capaz de toopass "verificar a elegibilidade" e o serviço de licença de múltipla DRM Olá será refuse tooissue Olá pedida licença, conforme mostrado abaixo. Olá detalhada descrição é "adquirir licenças falha", que é que concebida.

![Utilizadores não realizados](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Executar personalizado serviço de Token seguro
Para o cenário de Olá da execução personalizado Secure Token serviço (STS), token JWT de Olá será emitido pelo STS personalizado Olá utilizando a chave simétrico ou assimétrico.

Olá maiúsculas e minúsculas de utilização de chave simétrica (utilizando o Chrome):

![Executar STS personalizados](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

Olá caso de utilização de chave assimétrica através de um X509 do certificado (utilizando o browser moderno Microsoft).

![Executar STS personalizados](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

Em ambos os Olá acima casos, o utilizador autenticação permanece Olá mesmo – através do Azure AD. Step-by-Olá única diferença é que os tokens JWT são emitidos pelo Olá STS personalizado em vez do Azure AD. Obviamente, quando configurar a proteção de CENC dinâmica, restrição Olá do serviço de entrega de licença especifica tipo Olá do JWT token, chave simétrico ou assimétrico.

## <a name="summary"></a>Resumo
Neste documento, discutimos CENC com várias native DRM e controlo de acesso através da autenticação token: respetiva estrutura e a respetiva implementação utilizando o Azure, os Media Services do Azure e Azure Media Player.

* Um design de referência é apresentado que contém todos os componentes necessários Olá no subsistema DRM/CENC;
* Uma implementação de referência no Azure, o Media Services do Azure e o leitor de multimédia do Azure.
* Alguns tópicos diretamente envolvido Olá design e implementação também são debatidos.

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
