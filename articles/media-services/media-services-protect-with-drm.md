---
title: "aaaUsing PlayReady e/ou Widevine a encriptação comum dinâmica | Microsoft Docs"
description: "Serviços de suporte de dados do Microsoft Azure permite-lhe toodeliver MPEG-DASH, transmissão em fluxo uniforme e Http-Live-Streaming (HLS) fluxos protegidos com o Microsoft PlayReady DRM. Também permite-lhe toodelivery DASH encriptado com Widevine DRM. Este tópico mostra como toodynamically encriptar com PlayReady e Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>Utilizar a encriptação comum dinâmica com PlayReady e/ou Widevine

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Serviços de suporte de dados do Microsoft Azure permite-lhe toodeliver MPEG-DASH, transmissão em fluxo uniforme e fluxos de HTTP-Live-Streaming (HLS) protegidos com [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Também permite-lhe toodeliver encriptado transmissões em fluxo DASH com licenças Widevine DRM. Tanto PlayReady como Widevine são encriptados por Olá especificação de encriptação comum (ISO/IEC 23001 7 CENC). Pode utilizar [SDK .NET do AMS](https://www.nuget.org/packages/windowsazure.mediaservices/) (começando com a versão de Olá 3.5.1) ou REST API tooconfigure toouse seu AssetDeliveryConfiguration Widevine.

Os Media Services fornecem um serviço para entrega de licenças PlayReady e Widevine DRM. Os Media Services também fornecem APIs que permitem-lhe configurar Olá direitos e restrições que pretende para Olá PlayReady ou Widevine DRM runtime tooenforce quando um utilizador reproduz conteúdo protegido. Quando um utilizador solicita um conteúdo DRM protegido, a aplicação de leitor de Olá solicitará uma licença do serviço de licença de Olá AMS. serviço de licença do AMS Olá irá emitir um leitor de toohello licença se está autorizado. Uma licença PlayReady ou Widevine contém a chave de desencriptação de Olá que pode ser utilizado por Olá cliente player toodecrypt e fluxo Olá conteúdo.

Também pode utilizar Olá seguir toohelp de parceiros de AMS fornecer licenças Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Para obter mais informações, consulte: integração com [Axinom](media-services-axinom-integration.md) e [castLabs](media-services-castlabs-integration.md).

Os Media Services suportam várias formas de autorização de utilizadores que efetuam pedidos de chave. Olá política de autorização da chave de conteúdo pode ter um ou mais restrições de autorização: aberto ou token restrito. política de Olá token restrito tem de ser acompanhada por um token emitido por uma Secure Token serviço (STS). Os Media Services suportam tokens no Olá [Web Tokens simples](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT). Para obter mais informações, consulte a política de autorização de configurar Olá da chave de conteúdo.

tootake partido da encriptação dinâmica, terá de toohave um elemento que contenha um conjunto de ficheiros MP4 de velocidade de transmissão múltipla ou ficheiros de origem de transmissão em fluxo uniforme de transmissão múltipla. Também precisa de políticas de entrega de Olá tooconfigure para ativo Olá (descrito mais à frente neste tópico). Em seguida, com base no formato de Olá especificado no URL de transmissão em fluxo de Olá, servidor de transmissão em fluxo a pedido Olá irá garantir que esse fluxo Olá é entregue no protocolo Olá que escolheu. Como resultado, só precisa de toostore e pagamento para ficheiros de Olá num único formato de armazenamento e dos Media Services irão compilar e disponibilizar Olá HTTP resposta adequada com base em cada pedido de um cliente.

Este tópico seria útil toodevelopers que funcionam em aplicações que entregam multimédia protegida com vários DRMs, tais como PlayReady e Widevine. tópico de Olá mostra como tooconfigure Olá ao serviço de entrega de licença PlayReady com políticas de autorização para que apenas os clientes autorizados foi receber licenças PlayReady ou Widevine. Também mostra como toouse encriptação dinâmica com PlayReady ou Widevine DRM sobre DASH.

>[!NOTE]
>Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado. toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado. 

## <a name="download-sample"></a>Transferir exemplo
Pode transferir o exemplo de Olá descrito neste artigo [aqui](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Configurar a Encriptação Comum Dinâmica e os Serviços de Entrega de Licença DRM

Olá seguem-se passos gerais que teria tooperform quando proteger os seus elementos com PlayReady, utilizando o serviço de entrega de licença de Media Services Olá e também da encriptação dinâmica.

1. Criar um elemento e carregar ficheiros para o elemento de Olá.
2. Codificar Olá asset contentora Olá ficheiro toohello velocidade de transmissão adaptável definido MP4.
3. Criar uma chave de conteúdo e associe-a com elemento Olá codificado. Nos Media Services, chave de conteúdo de Olá contém a chave de encriptação do elemento de Olá.
4. Configure a política de autorização de Olá da chave de conteúdo. política de autorização da chave de conteúdo de Olá tem de ser configurada por si e cumprida pelo cliente de Olá para Olá conteúdo toobe chave toohello entregue cliente.

    Ao criar a política de autorização da chave de conteúdo de Olá, seguintes elementos terão de toospecify Olá: entrega método (PlayReady ou Widevine), restrições (aberto ou token) e o tipo de entrega de chave de toohello específico informações que define a forma como a chave de Olá é entregue cliente toohello ([PlayReady](media-services-playready-license-template-overview.md) ou [Widevine](media-services-widevine-license-template-overview.md) o modelo de licença).

5. Configure a política de entrega de Olá para um recurso. configuração de políticas de entrega de Olá inclui: protocolo entrega (por exemplo, MPEG DASH, HLS, transmissão em fluxo uniforme ou todos), Olá tipo de encriptação dinâmica (por exemplo, encriptação comum), PlayReady ou Widevine URL de aquisição de licença.

    Foi possível aplicar o protocolo de tooeach outra política no Olá mesmo elemento. Por exemplo, pode aplicar encriptação de PlayReady tooSmooth/DASH e AES Envelope tooHLS. Quaisquer protocolos que não estão definidos numa política de entrega (por exemplo, adicionar uma única política que especifica apenas HLS como protocolo de Olá) serão bloqueados da transmissão em fluxo. Olá toothis de exceção é não se tiver nenhuma política de entrega de elemento definida de todo. Em seguida, todos os protocolos serão permitidos na Olá encriptado.

6. Crie um localizador OnDemand na ordem tooget um URL de transmissão em fluxo.

Irá encontrar um exemplo .NET concluído no final de Olá tópico Olá.

Olá seguinte imagem demonstra o fluxo de trabalho de Olá descrito acima. Aqui o token de Olá é utilizado para autenticação.

![Proteger com PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

resto Olá deste tópico fornece explicações detalhadas, exemplos de código e ligações tootopics que mostram como tooachieve Olá tarefas descritas acima.

## <a name="current-limitations"></a>Limitações atuais
Se adicionar ou atualizar uma política de entrega de elemento, tem de eliminar o localizador de Olá associada (se aplicável) e criar um novo localizador.

Limitação ao encriptar com Widevine com os Media Services do Azure: atualmente, não são suportados várias chaves de conteúdo.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Criar um elemento e carregar ficheiros para o elemento de Olá
Na ordem toomanage, codificar e transmitir os seus vídeos, primeiro tem de carregar o conteúdo para os Media Services do Microsoft Azure. Assim que seja carregado, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.

Para obter informações detalhadas, consulte [Carregar Ficheiros para uma conta de Media Services](media-services-dotnet-upload-files.md).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Codificar Olá asset contentora Olá ficheiro toohello velocidade de transmissão adaptável definido MP4
Com a encriptação dinâmica, tudo o que precisa é toocreate um elemento que contenha um conjunto de ficheiros MP4 de velocidade de transmissão múltipla ou ficheiros de origem de transmissão em fluxo uniforme de transmissão múltipla. Em seguida, com base no Olá formato especificado no manifesto de Olá e pedido de fragmento, Olá a pedido de transmissão em fluxo servidor irá garantir que recebem o fluxo de Olá no protocolo Olá que escolheu. Como resultado, só precisa de toostore e pagamento para ficheiros de Olá num único formato de armazenamento e o serviço de Media Services irão compilar e disponibilizar a resposta adequada Olá com base nos pedidos de um cliente. Para obter mais informações, consulte Olá [descrição geral de empacotamento dinâmico](media-services-dynamic-packaging-overview.md) tópico.

Para obter instruções sobre como tooencode, consulte [como tooencode um elemento com o codificador de multimédia Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Criar uma chave de conteúdo e associe-a com elemento codificado de Olá
Nos Media Services, chave de conteúdo de Olá contém a chave de Olá que pretende que o tooencrypt um recurso de com.

Para obter informações detalhadas, consulte [Criar chave de conteúdo](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurar a política de autorização de Olá da chave de conteúdo
Os Media Services suportam várias formas de autenticar utilizadores que efetuam pedidos de chave. política de autorização da chave de conteúdo de Olá tem de ser configurada por si e cumprida pelo cliente de Olá (leitor) para que toobe chave Olá entregar toohello cliente. Olá política de autorização da chave de conteúdo pode ter um ou mais restrições de autorização: aberto ou token restrito.

Para obter informações detalhadas, consulte [Configurar a Política de Autorização da Chave de Conteúdo](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).

## <a id="configure_asset_delivery_policy"></a>Configurar a política de entrega de elemento
Configure a política de entrega de Olá para o seu elemento. Alguns dos aspetos Olá configuração de política de entrega de elemento inclui:

* Olá URL de aquisição de licença DRM.
* Olá asset protocolo entrega (por exemplo, MPEG DASH, HLS, transmissão em fluxo uniforme ou todos).
* tipo de Olá de encriptação dinâmica (neste caso, a encriptação comum).

Para obter informações detalhadas, consulte [Configurar a política de entrega de elemento](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Criar um OnDemand na ordem tooget um URL de transmissão em fluxo o localizador de transmissão em fluxo
Terá de tooprovide ao utilizador com Olá transmissão em fluxo de URL para uniforme, DASH ou HLS.

> [!NOTE]
> Se adicionar ou atualizar a sua política de entrega de elementos, tem de eliminar um localizador existente (se aplicável) e criar um novo localizador.
>
>

Para obter instruções sobre como ver toopublish um recurso e compilação um URL de transmissão em fluxo, [compilar um URL de transmissão em fluxo](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Obter um token de teste
Obter um teste de token com base na restrição de token de Olá que foi utilizada para a política de autorização da chave de Olá.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


Pode utilizar Olá [leitor AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest sua transmissão em fluxo.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto de Visual Studio

1. Configurar o ambiente de desenvolvimento e preencher o ficheiro de App. config Olá com as informações de ligação, conforme descrito em [desenvolvimento de Media Services com .NET](media-services-dotnet-how-to-use.md). 
2. Adicionar Olá demasiado os seguintes elementos**appSettings** definida no ficheiro App. config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Exemplo

Olá exemplo seguinte demonstra a funcionalidade que foi introduzida no SDK de Media Services do Azure para .net-versão 3.5.2 (especificamente, Olá capacidade toodefine um Widevine modelo de licença e pedir uma licença Widevine a partir de Media Services do Azure).

Substitua o código de Olá no seu ficheiro Program.cs com o código de Olá apresentado nesta secção.

>[!NOTE]
>Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy). Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso. Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Certifique-se tooupdate variáveis toopoint toofolders onde estão localizados os ficheiros de entrada.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a>Passo seguinte
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consultar também
[CENC com Múltipla DRM e Controlo de Acesso](media-services-cenc-with-multidrm-access-control.md)

[Configurar empacotamento Widevine com AMS](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Anunciar os serviços de entrega de licença Widevine da Google nos Serviços de Multimédia do Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
