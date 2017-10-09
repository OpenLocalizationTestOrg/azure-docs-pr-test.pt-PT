---
title: "O Azure Active Directory B2C: Adicionar as suas políticas de toocustom atributos e utilizar no perfil editar | Microsoft Docs"
description: "Instruções sobre como utilizar as propriedades de extensão, atributos personalizados e incluindo-los na interface de utilizador Olá"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="5ee5f-103">O Azure Active Directory B2C: Criar e utilizar atributos personalizados num perfil personalizado Editar política</span><span class="sxs-lookup"><span data-stu-id="5ee5f-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5ee5f-104">Neste artigo, pode criar um atributo personalizado no diretório do Azure AD B2C e utiliza este novo atributo como uma afirmação personalizada no journey de utilizador de edição de perfil Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ee5f-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5ee5f-105">Prerequisites</span></span>

<span data-ttu-id="5ee5f-106">Olá concluir os passos no artigo Olá [introdução com as políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5ee5f-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="5ee5f-107">Utilize os atributos personalizados toocollect informações sobre os seus clientes no Azure Active Directory B2C através de políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="5ee5f-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="5ee5f-108">Diretório do Azure Active Directory (Azure AD) B2C é fornecido com um conjunto de atributos incorporado: determinado nome, o apelido, cidade, Código Postal, userPrincipalName, etc.  Muitas vezes, precisa de toocreate os seus próprios atributos.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="5ee5f-109">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5ee5f-109">For example:</span></span>
* <span data-ttu-id="5ee5f-110">Necessita de uma aplicação de cliente orientado toopersist um atributo, tais como "LoyaltyNumber."</span><span class="sxs-lookup"><span data-stu-id="5ee5f-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="5ee5f-111">Um fornecedor de identidade tem um identificador exclusivo do utilizador que tem de ser guardado como "uniqueUserGUID"."</span><span class="sxs-lookup"><span data-stu-id="5ee5f-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="5ee5f-112">Um journey personalizadas do utilizador tem de estado de Olá toopersist do utilizador, tais como "migrationStatus."</span><span class="sxs-lookup"><span data-stu-id="5ee5f-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="5ee5f-113">Com o Azure AD B2C, pode expandir o conjunto de Olá de atributos armazenados em cada conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="5ee5f-114">Também pode ler e escrever estes atributos utilizando Olá [AD Graph API do Azure](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5ee5f-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="5ee5f-115">As propriedades de extensão expandem o esquema de Olá Olá de objetos de utilizador no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="5ee5f-116">propriedade de extensão de termos de Olá, o atributo personalizado e afirmações personalizadas Consulte toohello a mesma coisa no contexto de Olá deste nome artigo e Olá varia consoante o contexto de Olá (aplicação, objeto, política).</span><span class="sxs-lookup"><span data-stu-id="5ee5f-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="5ee5f-117">As propriedades de extensão só podem ser registadas um objeto de aplicação, apesar de estes poderão conter dados para um utilizador.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="5ee5f-118">propriedade de Olá é aplicação toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-118">hello property is attached toohello application.</span></span> <span data-ttu-id="5ee5f-119">objeto da aplicação Olá tem de ser concedido acesso de escrita tooregister uma propriedade de extensão.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="5ee5f-120">100 propriedades de extensão (em todos os tipos e todas as aplicações) podem ser escritas tooany único objeto.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="5ee5f-121">As propriedades de extensão são adicionados a tipo de diretório de destino toohello e torna-se imediatamente acessíveis no inquilino do diretório de Olá, Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="5ee5f-122">Se for eliminada aplicação Olá, essas propriedades de extensão, juntamente com quaisquer dados contidos nos mesmos para todos os utilizadores também são removidas.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="5ee5f-123">Se uma propriedade de extensão é eliminada por Olá aplicação, é removido no Olá objetos de diretório de destino e Olá valores eliminados.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="5ee5f-124">Propriedades da extensão existem apenas num contexto de Olá de uma aplicação registada no inquilino Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="5ee5f-125">id de objeto Olá dessa aplicação deve ser incluído no Olá TechnicalProfile utilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="5ee5f-126">diretório de Olá, Azure AD B2C, incluem normalmente uma aplicação Web com o nome `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="5ee5f-127">Esta aplicação é principalmente utilizada pelo políticas incorporadas do b2c Olá para afirmações personalizadas Olá criadas através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="5ee5f-128">É recomendado utilizar extensões de tooregister esta aplicação para as políticas personalizadas do b2c apenas para utilizadores avançados.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="5ee5f-129">Instruções para isto são incluídas no Olá secção passos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="5ee5f-130">Criar um novo toostore de aplicação as propriedades de extensão de Olá</span><span class="sxs-lookup"><span data-stu-id="5ee5f-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="5ee5f-131">Abra uma sessão de navegação e navegue toohello [Azure porta](https://portal.azure.com) e inicie sessão com credenciais administrativas de Olá desejar tooconfigure de diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="5ee5f-132">Clique em **do Azure Active Directory** no menu de navegação esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="5ee5f-133">Poderá ser necessário toofind-lo ao selecionar mais de serviços >.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="5ee5f-134">Selecione **registos de aplicação** e clique em **novo registo de aplicação**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="5ee5f-135">Fornece o seguinte Olá recomendado entradas:</span><span class="sxs-lookup"><span data-stu-id="5ee5f-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="5ee5f-136">Especifique um nome para a aplicação web de Olá: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="5ee5f-137">Tipo de aplicação: app/API Web</span><span class="sxs-lookup"><span data-stu-id="5ee5f-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="5ee5f-138">Início de sessão URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="5ee5f-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="5ee5f-139">Selecione * * criar.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-139">Select **Create.</span></span> <span data-ttu-id="5ee5f-140">É apresentada a conclusão com êxito no Olá **notificações**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="5ee5f-141">Selecione a aplicação web de Olá recém-criado: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="5ee5f-142">Selecionadas definições: **as permissões necessárias**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="5ee5f-143">Selecionar a API **do Active Directory do Windows**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="5ee5f-144">Coloque uma marca de verificação nas permissões de aplicação: **leitura e escrita de dados de diretório**, e **guardar**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="5ee5f-145">Escolha **conceder permissões** e confirme **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="5ee5f-146">Copie a área de transferência tooyour e guarde Olá seguintes identificadores de WebApp-GraphAPI-DirectoryExtensions > Definições > propriedades ></span><span class="sxs-lookup"><span data-stu-id="5ee5f-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="5ee5f-147">**ID da aplicação** .</span><span class="sxs-lookup"><span data-stu-id="5ee5f-147">**Application ID** .</span></span> <span data-ttu-id="5ee5f-148">Exemplo:`103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="5ee5f-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="5ee5f-149">**ID de objeto**.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-149">**Object ID**.</span></span> <span data-ttu-id="5ee5f-150">Exemplo:`80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="5ee5f-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="5ee5f-151">Modificar o Olá tooadd de política personalizada ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="5ee5f-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="5ee5f-152">Olá <TechnicalProfile Id="AAD-Common"> é referenciado tooas "comuns", porque os respetivos elementos são incluídos no e reutilizados em todos os Olá do Azure Active Directory TechnicalProfiles utilizando o elemento de Olá:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="5ee5f-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="5ee5f-153">Quando hello TechnicalProfile escritas para a propriedade de extensão para Olá primeiro tempo toohello recentemente criado, pode deparar-se um erro de uso individual.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="5ee5f-154">propriedade de extensão de Olá é criada Olá pela primeira vez que é utilizado.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="5ee5f-155">Utilizar a nova propriedade de extensão Olá / personalizado o atributo em journey um utilizador</span><span class="sxs-lookup"><span data-stu-id="5ee5f-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="5ee5f-156">Olá abrir ficheiro de entidade Confiadora Party(RP) que descreve a política de editar journey de utilizador.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="5ee5f-157">Se estiver a iniciar a, poderá ser aconselhável toodownload a versão já configurada do hello RP PolicyEdit ficheiros diretamente a partir de Olá secção política do Azure B2C personalizada Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="5ee5f-158">Em alternativa, abra o ficheiro XML a partir da sua pasta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="5ee5f-159">Adicionar uma afirmação personalizada `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="5ee5f-160">Incluindo Olá personalizada de afirmação no Olá `<RelyingParty>` elemento, que é transmitida como um parâmetro toohello UserJourney TechnicalProfiles e incluída no token de Olá para aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="5ee5f-161">Adicionar um ficheiro de política de extensão de toohello de definição de afirmação `TrustFrameworkExtensions.xml` dentro Olá `<ClaimsSchema>` elemento conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="5ee5f-162">Adicionar Olá afirmação mesmo ficheiro de definição de política de Base de toohello `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="5ee5f-163">Adicionar um `ClaimType` definição na base de Olá e ficheiro de extensões de Olá normalmente não é necessária, no entanto, uma vez que os passos seguintes Olá adicionará Olá extension_loyaltyId tooTechnicalProfiles no ficheiro de Base de Olá, validação de política de Olá irão rejeitar o carregamento de Olá do ficheiro de base de Olá sem ele.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="5ee5f-164">Poderá ser útil tootrace execução Olá Olá journey de utilizador com o nome "ProfileEdit" no ficheiro de TrustFrameworkBase.xml Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="5ee5f-165">Procure journey de utilizador de Olá de Olá mesmo nome no seu editor e observar se Orchestration passo 5 invoca Olá TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="5ee5f-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="5ee5f-166">Procurar e inspecionar este toofamiliarize TechnicalProfile por si com o fluxo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="5ee5f-167">Adicionar loyaltyId como afirmações de entrada e saída no Olá TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="5ee5f-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="5ee5f-168">Adicione afirmação TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist Olá valor Olá afirmação na propriedade de extensão de Olá, para o utilizador atual do Olá no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="5ee5f-169">Adicione afirmação no valor de Olá tooread TechnicalProfile "AAD UserReadUsingObjectId" do atributo de extensão de Olá sempre que um utilizador inicia sessão.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="5ee5f-170">Deste modo, até que ponto Olá TechnicalProfiles foram alterados no fluxo de Olá do apenas para contas locais.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="5ee5f-171">Se o atributo novo Olá for pretendido no fluxo de Olá de uma conta federada/social, um conjunto diferente de TechnicalProfiles tem toobe alterado.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="5ee5f-172">Consulte os passos seguintes.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="5ee5f-173">elemento de IncludeTechnicalProfile Olá adiciona todos os elementos de Olá do AAD comuns toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="5ee5f-174">Testar a política personalizada de Olá utilizando "Executar agora"</span><span class="sxs-lookup"><span data-stu-id="5ee5f-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="5ee5f-175">Abra Olá **do Azure AD B2c** e navegue demasiado**identidade experiência Framework > políticas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="5ee5f-176">Selecione a política personalizada de Olá que carregou e clique em Olá **executar agora** botão.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="5ee5f-177">Deve ser capaz de toosign através de um endereço de e-mail.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="5ee5f-178">token de id de Olá devolveu tooyour aplicação inclui a nova propriedade de extensão Olá como uma afirmação personalizada precedida por extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="5ee5f-179">Consulte o exemplo.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="5ee5f-180">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5ee5f-180">Next steps</span></span>

<span data-ttu-id="5ee5f-181">Adicione Olá nova afirmação toohello fluxos para inícios de sessão de conta de redes sociais alterando Olá TechnicalProfiles listados.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="5ee5f-182">Estas duas TechnicalProfiles são utilizados por toowrite de inícios de sessão de conta federada/social e ler os dados de utilizador de Olá utilizando Olá alternativeSecurityId como Olá localizador de objeto de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="5ee5f-183">Utilizar Olá mesmos atributos de extensão entre as políticas incorporadas e personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="5ee5f-184">Quando adiciona os atributos de extensão (também conhecido como atributos personalizados) através de experiência do portal Olá, esses atributos estão registados utilizando Olá * *-extensões-aplicação b2c que existe na cada inquilino do b2c.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="5ee5f-185">toouse estes atributos de extensão na sua política personalizada:</span><span class="sxs-lookup"><span data-stu-id="5ee5f-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="5ee5f-186">Dentro do seu inquilino do b2c em portal.azure.com, navegue até demasiado**do Azure Active Directory** e selecione **registos de aplicação**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="5ee5f-187">Localizar o **aplicação de extensões de b2c** e selecione-</span><span class="sxs-lookup"><span data-stu-id="5ee5f-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="5ee5f-188">Em Olá de registo 'Essentials' **ID da aplicação** e Olá **ID de objeto**</span><span class="sxs-lookup"><span data-stu-id="5ee5f-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="5ee5f-189">Inclui-los os seus metadados do perfil comum AAD técnica como da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5ee5f-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="5ee5f-190">tookeep consistência com a experiência de portal Olá, criar estes atributos através da IU do portal de Olá *antes* utilizá-los no seu políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="5ee5f-191">Quando cria um atributo "ActivationStatus" no portal de Olá, tem de referenciar tooit da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5ee5f-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="5ee5f-192">Referência</span><span class="sxs-lookup"><span data-stu-id="5ee5f-192">Reference</span></span>

* <span data-ttu-id="5ee5f-193">A **perfil técnica (TP)** é um tipo de elemento que pode considerar como um *função* que define o nome de um ponto final, os metadados, o protocolo e detalhes Olá exchange de afirmações que Olá identidade Experiência Framework deverá efetuar.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="5ee5f-194">Quando isto *função* denomina-se um passo de orquestração ou a partir de outro TechnicalProfile, Olá InputClaims e OutputClaims são fornecidos como parâmetros pelo autor da chamada de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="5ee5f-195">Para um total tratamento nas propriedades da extensão, consulte o artigo de Olá [EXTENSÕES de esquema de DIRETÓRIO | CONCEITOS DE API DO GRÁFICO](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="5ee5f-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="5ee5f-196">Os atributos de extensão no Graph API são denominados utilizando Convenção Olá `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="5ee5f-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="5ee5f-197">As políticas personalizadas Consulte tooextensions atributos como extension_attributename, deste modo, omitindo Olá ApplicationObjectId no Olá XML</span><span class="sxs-lookup"><span data-stu-id="5ee5f-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
