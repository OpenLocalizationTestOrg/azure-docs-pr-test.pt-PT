---
title: "aaaHow toouse Olá SDK de aplicações móveis do Azure para Android | Microsoft Docs"
description: "Como toouse Olá SDK de aplicações móveis do Azure para Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="7a18b-103">Como toouse Olá SDK de aplicações móveis do Azure para Android</span><span class="sxs-lookup"><span data-stu-id="7a18b-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="7a18b-104">Este guia mostra como toouse Olá Android SDK de cliente para cenários comuns de tooimplement Mobile Apps, tais como:</span><span class="sxs-lookup"><span data-stu-id="7a18b-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="7a18b-105">Consultar dados (inserir, atualizar e eliminar).</span><span class="sxs-lookup"><span data-stu-id="7a18b-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="7a18b-106">Autenticação.</span><span class="sxs-lookup"><span data-stu-id="7a18b-106">Authentication.</span></span>
* <span data-ttu-id="7a18b-107">Processamento de erros.</span><span class="sxs-lookup"><span data-stu-id="7a18b-107">Handling errors.</span></span>
* <span data-ttu-id="7a18b-108">Personalizar cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-108">Customizing hello client.</span></span>

<span data-ttu-id="7a18b-109">Este guia está centrado nas Olá do lado do cliente Android SDK.</span><span class="sxs-lookup"><span data-stu-id="7a18b-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="7a18b-110">toolearn mais informações sobre como Olá SDKs do lado do servidor para Mobile Apps, consulte [trabalhar com o back-end de .NET SDK] [ 10] ou [como toouse Olá back-end Node.js SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="7a18b-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="7a18b-111">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="7a18b-111">Reference Documentation</span></span>

<span data-ttu-id="7a18b-112">Pode encontrar Olá [referência da API de Javadocs] [ 12] da biblioteca de cliente do Android Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a18b-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="7a18b-113">Plataformas suportadas</span><span class="sxs-lookup"><span data-stu-id="7a18b-113">Supported Platforms</span></span>

<span data-ttu-id="7a18b-114">Olá SDK de aplicações móveis do Azure para Android suporta níveis de API 19 através de 24 (KitKat através de Nougat) para o telefone e tablet fatores de formulários.</span><span class="sxs-lookup"><span data-stu-id="7a18b-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="7a18b-115">A autenticação, em particular, utiliza uma comuns web framework abordagem toogather as credenciais.</span><span class="sxs-lookup"><span data-stu-id="7a18b-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="7a18b-116">Autenticação de servidor fluxo não funciona com dispositivos de fator de formulário pequeno como observa.</span><span class="sxs-lookup"><span data-stu-id="7a18b-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="7a18b-117">A configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7a18b-117">Setup and Prerequisites</span></span>

<span data-ttu-id="7a18b-118">Olá concluída [início rápido de aplicações móveis](app-service-mobile-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a18b-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="7a18b-119">Esta tarefa garante que todos os pré-requisitos para o desenvolvimento de aplicações móveis do Azure foram cumpridos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="7a18b-120">Olá início rápido também o ajuda a configurar a sua conta e criar a sua primeira back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="7a18b-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="7a18b-121">Se decidir não toocomplete tutorial de início rápido de Olá, conclua Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7a18b-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="7a18b-122">[criar um back-end de aplicação móvel] [ 13] toouse com a sua aplicação Android.</span><span class="sxs-lookup"><span data-stu-id="7a18b-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="7a18b-123">No Android Studio, [atualização Olá Gradle compilar ficheiros](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="7a18b-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="7a18b-124">[Ativar a permissão de internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="7a18b-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="7a18b-125"><a name="gradle-build"></a>Olá Gradle criar ficheiro de atualização</span><span class="sxs-lookup"><span data-stu-id="7a18b-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="7a18b-126">Alterar ambas **gradle** ficheiros:</span><span class="sxs-lookup"><span data-stu-id="7a18b-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="7a18b-127">Adicione este código toohello *projeto* nível **gradle** ficheiro dentro Olá *buildscript* etiqueta:</span><span class="sxs-lookup"><span data-stu-id="7a18b-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="7a18b-128">Adicione este código toohello *módulo aplicação* nível **gradle** ficheiro dentro Olá *dependências* etiqueta:</span><span class="sxs-lookup"><span data-stu-id="7a18b-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="7a18b-129">Versão mais recente Olá está atualmente 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="7a18b-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="7a18b-130">versões de Olá suportado estão listadas [na gaveta][14].</span><span class="sxs-lookup"><span data-stu-id="7a18b-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="7a18b-131"><a name="enable-internet"></a>Ativar a permissão de internet</span><span class="sxs-lookup"><span data-stu-id="7a18b-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="7a18b-132">tooaccess do Azure, a aplicação tem de ter permissão de INTERNET Olá ativada.</span><span class="sxs-lookup"><span data-stu-id="7a18b-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="7a18b-133">Se ainda não estiver ativada, adicionar Olá seguinte linha de código tooyour **AndroidManifest.xml** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="7a18b-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="7a18b-134">Criar uma ligação de cliente</span><span class="sxs-lookup"><span data-stu-id="7a18b-134">Create a Client Connection</span></span>

<span data-ttu-id="7a18b-135">Mobile Apps do Azure fornece quatro funções tooyour de aplicações móveis:</span><span class="sxs-lookup"><span data-stu-id="7a18b-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="7a18b-136">Acesso a dados e a Sincronização Offline com um serviço de aplicações móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a18b-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="7a18b-137">Chame APIs personalizadas escritas com Olá SDK do servidor de aplicações do Azure Mobile.</span><span class="sxs-lookup"><span data-stu-id="7a18b-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="7a18b-138">Autenticação com o App Service do Azure autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="7a18b-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="7a18b-139">Registo da notificação com os Hubs de notificação push.</span><span class="sxs-lookup"><span data-stu-id="7a18b-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="7a18b-140">Cada uma destas funções primeiro exige que crie um `MobileServiceClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="7a18b-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="7a18b-141">Apenas um `MobileServiceClient` objecto deve ser criado dentro do seu cliente móvel (ou seja, deve ser um padrão de Singleton).</span><span class="sxs-lookup"><span data-stu-id="7a18b-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="7a18b-142">toocreate um `MobileServiceClient` objeto:</span><span class="sxs-lookup"><span data-stu-id="7a18b-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="7a18b-143">Olá `<MobileAppUrl>` é uma cadeia ou um objeto de URL que aponta tooyour back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="7a18b-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="7a18b-144">Se estiver a utilizar o back-end móvel toohost do App Service do Azure, em seguida, certifique-se de utilizar Olá segura `https://` versão do URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="7a18b-145">Olá cliente também requer acesso toohello atividade ou contexto - hello `this` parâmetro no exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="7a18b-146">Olá MobileServiceClient construção deverá ocorrer dentro de Olá `onCreate()` método de Olá atividade referenciada na Olá `AndroidManifest.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7a18b-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="7a18b-147">Como melhor prática, deve de separar as comunicações de servidor na sua própria classe (padrão de singleton).</span><span class="sxs-lookup"><span data-stu-id="7a18b-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="7a18b-148">Neste caso, deverá passar Olá atividade dentro de Olá construtor tooappropriately configurar serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="7a18b-149">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a18b-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="7a18b-150">Agora pode chamar `AzureServiceAdapter.Initialize(this);` no Olá `onCreate()` método da sua atividade principal.</span><span class="sxs-lookup"><span data-stu-id="7a18b-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="7a18b-151">Utilizam outros métodos de que necessitam do cliente do acesso toohello `AzureServiceAdapter.getInstance();` tooobtain um adaptador de serviço de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="7a18b-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="7a18b-152">Operações de dados</span><span class="sxs-lookup"><span data-stu-id="7a18b-152">Data Operations</span></span>

<span data-ttu-id="7a18b-153">núcleo de Olá de Olá SDK de aplicações móveis do Azure é tooprovide acesso toodata armazenado no SQL Azure no back-end de aplicação móvel de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="7a18b-154">Pode aceder a estes dados a utilizar classes com tipo seguro (preferidas) ou sem tipos consultas (não recomendadas).</span><span class="sxs-lookup"><span data-stu-id="7a18b-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="7a18b-155">em massa de Olá desta secção lida com a utilizar classes com tipo seguro.</span><span class="sxs-lookup"><span data-stu-id="7a18b-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="7a18b-156">Definir as classes de dados de cliente</span><span class="sxs-lookup"><span data-stu-id="7a18b-156">Define client data classes</span></span>

<span data-ttu-id="7a18b-157">dados de tooaccess das tabelas de SQL Azure, definir classes de dados de cliente que correspondem a tabelas toohello Olá back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="7a18b-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="7a18b-158">Os exemplos neste tópico partem do princípio de uma tabela com o nome **MyDataTable**, que tem Olá seguintes colunas:</span><span class="sxs-lookup"><span data-stu-id="7a18b-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="7a18b-159">ID</span><span class="sxs-lookup"><span data-stu-id="7a18b-159">id</span></span>
* <span data-ttu-id="7a18b-160">Texto</span><span class="sxs-lookup"><span data-stu-id="7a18b-160">text</span></span>
* <span data-ttu-id="7a18b-161">Concluir</span><span class="sxs-lookup"><span data-stu-id="7a18b-161">complete</span></span>

<span data-ttu-id="7a18b-162">Olá correspondente objeto escrito do lado do cliente reside num ficheiro denominado **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="7a18b-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="7a18b-163">Adicione métodos getter e setter para cada campo que adicionar.</span><span class="sxs-lookup"><span data-stu-id="7a18b-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="7a18b-164">Se a tabela de SQL Azure contiver mais colunas, seria adicionar classe de toothis de campos Olá correspondente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="7a18b-165">Por exemplo, se hello DTO (objeto de transferência de dados) tinha uma coluna de prioridade de número inteiro, em seguida, poderá adicionar este campo, juntamente com os seus métodos getter e setter:</span><span class="sxs-lookup"><span data-stu-id="7a18b-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="7a18b-166">toolearn como toocreate tabelas adicionais no seu back-end do Mobile Apps, consulte [como: definir um controlador de tabela] [ 15] (back-end do .NET) ou [definir tabelas utilizando um esquema dinâmica] [ 16] (Back-end do Node.js).</span><span class="sxs-lookup"><span data-stu-id="7a18b-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="7a18b-167">Uma tabela de back-end do Mobile Apps do Azure define cinco campos especiais, quatro que são tooclients disponíveis:</span><span class="sxs-lookup"><span data-stu-id="7a18b-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="7a18b-168">`String id`: Olá ID globalmente exclusivo para o registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="7a18b-169">Como melhor prática, certifique-Olá id Olá representação de um [UUID] [ 17] objeto.</span><span class="sxs-lookup"><span data-stu-id="7a18b-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="7a18b-170">`DateTimeOffset updatedAt`: Olá data/hora da última atualização da Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="7a18b-171">campo de updatedAt Olá é definido pelo servidor Olá e nunca deve ser definido pelo seu código de cliente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="7a18b-172">`DateTimeOffset createdAt`: Olá data/hora esse objeto Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="7a18b-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="7a18b-173">campo de createdAt Olá é definido pelo servidor Olá e nunca deve ser definido pelo seu código de cliente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="7a18b-174">`byte[] version`: Normalmente representado como uma cadeia, a versão de Olá seja também definido pelo servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="7a18b-175">`boolean deleted`: Indica que o registo de Olá foram eliminado mas não removido ainda.</span><span class="sxs-lookup"><span data-stu-id="7a18b-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="7a18b-176">Não utilize `deleted` como uma propriedade de classe.</span><span class="sxs-lookup"><span data-stu-id="7a18b-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="7a18b-177">Olá `id` campo é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7a18b-177">hello `id` field is required.</span></span>  <span data-ttu-id="7a18b-178">Olá `updatedAt` campo e `version` campo são utilizados para sincronização offline (para a resolução de sincronização e conflito incremental respetivamente).</span><span class="sxs-lookup"><span data-stu-id="7a18b-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="7a18b-179">Olá `createdAt` é um campo de referência de campo e não é utilizado pelo cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="7a18b-180">os nomes de Olá são "entre a transmissão" nomes de propriedades de Olá e não são ajustável.</span><span class="sxs-lookup"><span data-stu-id="7a18b-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="7a18b-181">No entanto, pode criar um mapeamento entre o objeto e Olá nomes de "entre a transmissão" utilizando Olá [gson] [ 3] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7a18b-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="7a18b-182">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a18b-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="7a18b-183">Criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="7a18b-183">Create a Table Reference</span></span>

<span data-ttu-id="7a18b-184">tooaccess uma tabela, primeiro crie um [MobileServiceTable] [ 8] objeto ao chamar Olá **getTable** método no Olá [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="7a18b-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="7a18b-185">Este método tem dois sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="7a18b-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="7a18b-186">No Olá seguinte código, **mClient** é um objeto de MobileServiceClient tooyour referência.</span><span class="sxs-lookup"><span data-stu-id="7a18b-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="7a18b-187">sobrecarga primeiro Olá é utilizada em que nome de classe de Olá e nome da tabela Olá são Olá mesmo e é hello um utilizado no Olá início rápido:</span><span class="sxs-lookup"><span data-stu-id="7a18b-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="7a18b-188">Olá sobrecarga segundo é utilizada quando o nome da tabela Olá é diferente do nome de classe de Olá: primeiro parâmetro de Olá é o nome de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="7a18b-189"><a name="query"></a>Consulta uma tabela de back-end</span><span class="sxs-lookup"><span data-stu-id="7a18b-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="7a18b-190">Em primeiro lugar, obtenha uma referência de tabela.</span><span class="sxs-lookup"><span data-stu-id="7a18b-190">First, obtain a table reference.</span></span>  <span data-ttu-id="7a18b-191">Em seguida, execute uma consulta numa referência de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="7a18b-192">Uma consulta é qualquer combinação de:</span><span class="sxs-lookup"><span data-stu-id="7a18b-192">A query is any combination of:</span></span>

* <span data-ttu-id="7a18b-193">A `.where()` [cláusula de filtro](#filtering).</span><span class="sxs-lookup"><span data-stu-id="7a18b-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="7a18b-194">Um `.orderBy()` [ordenação cláusula](#sorting).</span><span class="sxs-lookup"><span data-stu-id="7a18b-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="7a18b-195">A `.select()` [cláusula de seleção de campo](#selection).</span><span class="sxs-lookup"><span data-stu-id="7a18b-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="7a18b-196">A `.skip()` e `.top()` para [resultados do bloco paginado](#paging).</span><span class="sxs-lookup"><span data-stu-id="7a18b-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="7a18b-197">cláusulas Olá tem de ser apresentadas no Olá anterior a ordem.</span><span class="sxs-lookup"><span data-stu-id="7a18b-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="7a18b-198"><a name="filter"></a>Filtrar resultados</span><span class="sxs-lookup"><span data-stu-id="7a18b-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="7a18b-199">formulário de geral Olá de uma consulta é:</span><span class="sxs-lookup"><span data-stu-id="7a18b-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="7a18b-200">Olá anterior exemplo devolve todos os resultados (se o tamanho máximo de página toohello definido pelo servidor Olá).</span><span class="sxs-lookup"><span data-stu-id="7a18b-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="7a18b-201">Olá `.execute()` método executa a consulta de Olá no back-end de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="7a18b-202">Olá consulta é convertida tooan [OData v3] [ 19] consulta antes da transmissão toohello Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="7a18b-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="7a18b-203">Na receção, back-end das Mobile Apps do Olá converte consulta Olá uma instrução de SQL Server antes de executar a instância de SQL Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="7a18b-204">Uma vez que a atividade de rede demora algum tempo, Olá `.execute()` método devolve um [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="7a18b-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="7a18b-205"><a name="filtering"></a>Filtrar os dados devolvidos</span><span class="sxs-lookup"><span data-stu-id="7a18b-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="7a18b-206">Olá após a execução da consulta devolve todos os itens de Olá **ToDoItem** tabela onde **concluída** é igual a **falso**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="7a18b-207">**mToDoTable** Olá referência toohello serviço móvel tabela que criámos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="7a18b-208">Define um filtro com Olá **onde** chamada do método na referência de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="7a18b-209">Olá **onde** método é seguido um **campo** método seguido de um método que especifica o predicado de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="7a18b-210">Métodos de predicado possíveis incluem **eq** (igual a), **ne** (não igual a), **gt** (superior), **ge** (maior ou igual a), **lt** (inferior), **le** (menor ou igual a).</span><span class="sxs-lookup"><span data-stu-id="7a18b-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="7a18b-211">Estes métodos permitem-lhe comparar o número e toospecific valores de campos de cadeia.</span><span class="sxs-lookup"><span data-stu-id="7a18b-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="7a18b-212">Pode filtrar as datas.</span><span class="sxs-lookup"><span data-stu-id="7a18b-212">You can filter on dates.</span></span> <span data-ttu-id="7a18b-213">Olá métodos seguintes permitem-lhe comparar o campo de data completo de Olá ou partes da data de Olá: **ano**, **mês**, **dia**, **hora**, **minuto**, e **segundo**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="7a18b-214">Olá exemplo seguinte adiciona um filtro para itens cujo *data devida* é igual a 2013.</span><span class="sxs-lookup"><span data-stu-id="7a18b-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="7a18b-215">Olá seguintes métodos de suportam filtros complexos em campos de cadeia: **startsWith**, **endsWith**, **concat**, **subcadeia**, **indexOf**, **substituir**, **toLower**, **toUpper**, **compactar**, e  **comprimento**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="7a18b-216">Olá filtros de exemplo a seguir para a tabela de linhas em que hello *texto* coluna começa com "PRI0."</span><span class="sxs-lookup"><span data-stu-id="7a18b-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="7a18b-217">os seguintes métodos de operador de Olá é suportada em campos de números: **adicionar**, **sub**, **mul**, **div**, **mod**, **piso**, **limite**, e **arredondar**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="7a18b-218">Olá filtros de exemplo a seguir para a tabela de linhas em que hello **duração** é um número par.</span><span class="sxs-lookup"><span data-stu-id="7a18b-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="7a18b-219">Pode combinar os predicados com estes métodos lógicos: **e**, **ou** e **não**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="7a18b-220">Olá seguinte o exemplo combina duas Olá precedente exemplos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="7a18b-221">Agrupar e aninhar operadores lógicos:</span><span class="sxs-lookup"><span data-stu-id="7a18b-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="7a18b-222">Para obter mais debate e exemplos de filtragem, consulte [explorar richness Olá do modelo de consulta do cliente do Android Olá][20].</span><span class="sxs-lookup"><span data-stu-id="7a18b-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="7a18b-223"><a name="sorting"></a>Ordenação devolvida dados</span><span class="sxs-lookup"><span data-stu-id="7a18b-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="7a18b-224">Olá seguinte código devolve todos os itens de uma tabela com **ToDoItems** ordenados ascendente por Olá *texto* campo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="7a18b-225">*mToDoTable* Olá referência toohello back-end tabela que criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7a18b-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="7a18b-226">Olá primeiro parâmetro de Olá **orderBy** método é um nome de toohello igual de cadeia do campo de Olá no qual toosort.</span><span class="sxs-lookup"><span data-stu-id="7a18b-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="7a18b-227">segundo parâmetro de Olá utiliza Olá **QueryOrder** toospecify de enumeração se toosort ascendente ou descendente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="7a18b-228">Se está a filtrar utilizando Olá ***onde*** método, Olá ***onde*** método tem de ser invocado antes Olá ***orderBy*** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="7a18b-229"><a name="selection"></a>Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="7a18b-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="7a18b-230">Olá seguinte código ilustra como tooreturn todos os itens de uma tabela com **ToDoItems**, mas apenas apresenta Olá **concluída** e **texto** campos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="7a18b-231">**mToDoTable** Olá referência toohello back-end tabela que criámos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="7a18b-232">a função Olá parâmetros toohello selecione são os nomes de cadeia de Olá das colunas da tabela de Olá que pretende que o tooreturn.</span><span class="sxs-lookup"><span data-stu-id="7a18b-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="7a18b-233">Olá **selecione** método tem métodos toofollow como **onde** e **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="7a18b-234">Pode ser seguido de métodos de paginação, como **ignorar** e **superior**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="7a18b-235"><a name="paging"></a>Devolver dados nas páginas</span><span class="sxs-lookup"><span data-stu-id="7a18b-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="7a18b-236">Os dados são **sempre** devolvido nas páginas.</span><span class="sxs-lookup"><span data-stu-id="7a18b-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="7a18b-237">número máximo de Olá de registos devolvidos é definido pelo servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="7a18b-238">Se os pedidos de cliente de Olá mais registos, o servidor de Olá devolve número máximo de Olá de registos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="7a18b-239">Por predefinição, o tamanho máximo de página de Olá no servidor de Olá é 50 registos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="7a18b-240">primeiro exemplo de Olá mostra como tooselect Olá cinco itens superiores de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="7a18b-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="7a18b-241">consulta de Olá devolve itens Olá de uma tabela com **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="7a18b-242">**mToDoTable** Olá referência toohello back-end tabela que criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7a18b-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="7a18b-243">Segue-se uma consulta que ignora Olá primeiro cinco itens e, em seguida, devolve Olá cinco seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a18b-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="7a18b-244">Se quiser tooget todos os registos numa tabela, implemente código tooiterate através de todas as páginas:</span><span class="sxs-lookup"><span data-stu-id="7a18b-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="7a18b-245">Um pedido para todos os registos ao utilizar este método cria um mínimo de dois pedidos toohello Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="7a18b-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="7a18b-246">Escolher entre Olá para o tamanho de página direita é um equilíbrio entre a utilização da memória enquanto o pedido de Olá está a acontecer, a utilização de largura de banda e a atraso na receção de dados de Olá completamente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="7a18b-247">a predefinição de Olá (50 registos) é adequada para todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="7a18b-248">Se utilizar exclusivamente nos dispositivos de memória superiores, aumente a segurança too500.</span><span class="sxs-lookup"><span data-stu-id="7a18b-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="7a18b-249">Ter encontrámos esse tamanho de página Olá crescente para além de 500 regista resultados em atrasos inaceitável e problemas de memória grande.</span><span class="sxs-lookup"><span data-stu-id="7a18b-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="7a18b-250"><a name="chaining"></a>Como: concatenar métodos de consulta</span><span class="sxs-lookup"><span data-stu-id="7a18b-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="7a18b-251">os métodos de Olá no consultar tabelas de back-end podem concatenar.</span><span class="sxs-lookup"><span data-stu-id="7a18b-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="7a18b-252">Encadeamento métodos permite-lhe tooselect colunas específicas de filtrado linhas são ordenadas e bloco paginadas de consulta.</span><span class="sxs-lookup"><span data-stu-id="7a18b-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="7a18b-253">Pode criar filtros lógicos complexos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-253">You can create complex logical filters.</span></span>  <span data-ttu-id="7a18b-254">Cada método de consulta devolve um objeto da consulta.</span><span class="sxs-lookup"><span data-stu-id="7a18b-254">Each query method returns a Query object.</span></span> <span data-ttu-id="7a18b-255">série de Olá tooend de métodos e consulta de Olá, na verdade, de execução, chamada Olá **executar** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="7a18b-256">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a18b-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="7a18b-257">Olá encadeados consulta métodos tem de ser ordenados como segue:</span><span class="sxs-lookup"><span data-stu-id="7a18b-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="7a18b-258">Filtragem (**onde**) métodos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="7a18b-259">A ordenação (**orderBy**) métodos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="7a18b-260">Seleção (**selecione**) métodos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="7a18b-261">paginação (**ignorar** e **superior**) métodos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="7a18b-262"><a name="binding"></a>Vincular a interface de utilizador de toohello de dados</span><span class="sxs-lookup"><span data-stu-id="7a18b-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="7a18b-263">O enlace de dados envolve três componentes:</span><span class="sxs-lookup"><span data-stu-id="7a18b-263">Data binding involves three components:</span></span>

* <span data-ttu-id="7a18b-264">origem de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="7a18b-264">hello data source</span></span>
* <span data-ttu-id="7a18b-265">esquema do ecrã Olá</span><span class="sxs-lookup"><span data-stu-id="7a18b-265">hello screen layout</span></span>
* <span data-ttu-id="7a18b-266">adaptador de Olá que ties Olá, dois em conjunto.</span><span class="sxs-lookup"><span data-stu-id="7a18b-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="7a18b-267">No nosso código de exemplo, iremos devolver dados de Olá da tabela de Mobile Apps SQL Azure Olá **ToDoItem** para uma matriz.</span><span class="sxs-lookup"><span data-stu-id="7a18b-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="7a18b-268">Esta atividade é um padrão comum para aplicações de dados.</span><span class="sxs-lookup"><span data-stu-id="7a18b-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="7a18b-269">Consultas de base de dados, muitas vezes, devolvem uma coleção de linhas que Olá cliente obtém uma lista ou a matriz.</span><span class="sxs-lookup"><span data-stu-id="7a18b-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="7a18b-270">Neste exemplo, a matriz de Olá é origem de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="7a18b-271">código de Olá Especifica um esquema de ecrã que define a vista de Olá Olá de dados de que é apresentado no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="7a18b-272">Olá dois estão vinculados juntamente com um adaptador, o qual este código é uma extensão de Olá **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="7a18b-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="7a18b-273"><a name="layout"></a>Definir Olá esquema</span><span class="sxs-lookup"><span data-stu-id="7a18b-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="7a18b-274">esquema de Olá é definida por alguns fragmentos de código XML.</span><span class="sxs-lookup"><span data-stu-id="7a18b-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="7a18b-275">Tendo em conta um esquema existente, Olá seguinte código representa Olá **ListView** queremos toopopulate com os nossos dados do servidor.</span><span class="sxs-lookup"><span data-stu-id="7a18b-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="7a18b-276">No Olá precedente código, Olá *listitem* atributo especifica o id de Olá do esquema de Olá para uma linha individuais na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="7a18b-277">Este código especifica uma caixa de verificação e do respetivo texto associado e obtém instanciado uma vez para cada item na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="7a18b-278">Este esquema não apresenta Olá **id** campo e um esquema mais complexo de especificar os campos adicionais na apresentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="7a18b-279">Este código está a ser Olá **row_list_to_do.xml** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7a18b-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="7a18b-280"><a name="adapter"></a>Definir o adaptador de Olá</span><span class="sxs-lookup"><span data-stu-id="7a18b-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="7a18b-281">Uma vez que a origem de dados de Olá da nossa vista é uma matriz de **ToDoItem**, iremos subclasse nosso adaptador de um **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="7a18b-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="7a18b-282">Este subclasse produz uma vista para cada **ToDoItem** utilizando Olá **row_list_to_do** esquema.</span><span class="sxs-lookup"><span data-stu-id="7a18b-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="7a18b-283">No nosso código, iremos definir Olá seguir uma classe que seja uma extensão de Olá **ArrayAdapter&lt;i&gt;**  classe:</span><span class="sxs-lookup"><span data-stu-id="7a18b-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="7a18b-284">Substituir adaptadores Olá **getView** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="7a18b-285">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a18b-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="7a18b-286">Estamos a criar uma instância desta classe no nosso atividade da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7a18b-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="7a18b-287">Olá segundo parâmetro toohello ToDoItemAdapter construtor é um esquema de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="7a18b-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="7a18b-288">Iremos agora pode instanciar Olá **ListView** e atribuir Olá adaptador toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="7a18b-289"><a name="use-adapter"></a>Utilizar Olá adaptador tooBind toohello da IU</span><span class="sxs-lookup"><span data-stu-id="7a18b-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="7a18b-290">Agora, está pronto toouse o enlace de dados.</span><span class="sxs-lookup"><span data-stu-id="7a18b-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="7a18b-291">Olá código seguinte mostra como tooget itens na tabela de Olá e preenche Olá adaptador local com Olá devolvido itens.</span><span class="sxs-lookup"><span data-stu-id="7a18b-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="7a18b-292">Chamar adaptador Olá sempre modificar Olá **ToDoItem** tabela.</span><span class="sxs-lookup"><span data-stu-id="7a18b-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="7a18b-293">Uma vez que as modificações são efetuadas numa base de registo por registo, para processar uma única linha, em vez de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="7a18b-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="7a18b-294">Inserir um item, chamar Olá **adicionar** método no Olá adaptador; a eliminar, chamar Olá **remover** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="7a18b-295">Pode encontrar um exemplo completo em Olá [Android projeto de início rápido][21].</span><span class="sxs-lookup"><span data-stu-id="7a18b-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="7a18b-296"><a name="inserting"></a>Inserir dados de back-end de Olá</span><span class="sxs-lookup"><span data-stu-id="7a18b-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="7a18b-297">Instanciar uma instância de Olá *ToDoItem* classe e definir as respetivas propriedades.</span><span class="sxs-lookup"><span data-stu-id="7a18b-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="7a18b-298">Em seguida, utilize **INSERT ()** tooinsert um objeto:</span><span class="sxs-lookup"><span data-stu-id="7a18b-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="7a18b-299">Olá dados devolvidos pela entidade correspondências Olá inseridos na tabela de back-end Olá, ID de Olá incluídos e quaisquer outros valores (como Olá `createdAt`, `updatedAt`, e `version` campos) definida no back-end de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="7a18b-300">As tabelas de Mobile Apps requerem uma coluna de chave primária com o nome **id**. Esta coluna tem de ser uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="7a18b-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="7a18b-301">valor predefinido de Olá da coluna de ID de Olá é um GUID.</span><span class="sxs-lookup"><span data-stu-id="7a18b-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="7a18b-302">Pode fornecer outros valores exclusivos, como endereços de e-mail ou nomes de utilizador.</span><span class="sxs-lookup"><span data-stu-id="7a18b-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="7a18b-303">Quando um valor de ID de cadeia não é fornecido para um registo inserido, o back-end de Olá gera um novo GUID.</span><span class="sxs-lookup"><span data-stu-id="7a18b-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="7a18b-304">Valores de ID de cadeia fornecem Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="7a18b-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="7a18b-305">Os iDs podem ser gerados sem o tornar uma base de dados de toohello de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="7a18b-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="7a18b-306">Os registos são toomerge mais fácil de tabelas diferentes ou bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7a18b-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="7a18b-307">Valores de ID melhor integram com a lógica de uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="7a18b-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="7a18b-308">Os valores de ID de cadeia são **REQUIRED** para suporte de sincronização offline.</span><span class="sxs-lookup"><span data-stu-id="7a18b-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="7a18b-309">Não é possível alterar um Id assim que esta está armazenada na base de dados de back-end de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="7a18b-310"><a name="updating"></a>Atualize dados numa aplicação móvel</span><span class="sxs-lookup"><span data-stu-id="7a18b-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="7a18b-311">dados de tooupdate numa tabela, transmitir Olá novo objeto toohello **Update ()** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="7a18b-312">Neste exemplo, *item* é uma linha de referência tooa no Olá *ToDoItem* tabela, o que tenha tido tooit algumas alterações.</span><span class="sxs-lookup"><span data-stu-id="7a18b-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="7a18b-313">Olá linha com Olá mesmo **id** é atualizado.</span><span class="sxs-lookup"><span data-stu-id="7a18b-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="7a18b-314"><a name="deleting"></a>Eliminar dados de uma aplicação móvel</span><span class="sxs-lookup"><span data-stu-id="7a18b-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="7a18b-315">Olá código a seguir mostra como toodelete dados de uma tabela, especificando Olá objeto de dados.</span><span class="sxs-lookup"><span data-stu-id="7a18b-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="7a18b-316">Também pode eliminar um item, especificando Olá **id** campo Olá toodelete de linha.</span><span class="sxs-lookup"><span data-stu-id="7a18b-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="7a18b-317"><a name="lookup"></a>Procurar um item específico por Id</span><span class="sxs-lookup"><span data-stu-id="7a18b-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="7a18b-318">Procurar um item com específico **id** campo com Olá **lookUp()** método:</span><span class="sxs-lookup"><span data-stu-id="7a18b-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="7a18b-319"><a name="untyped"></a>Como: trabalhar com dados sem tipo</span><span class="sxs-lookup"><span data-stu-id="7a18b-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="7a18b-320">o modelo de programação sem tipo Olá dá-lhe controlo exato através de serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="7a18b-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="7a18b-321">Existem alguns cenários comuns em que pode ser útil toouse um modelo de programação sem tipo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="7a18b-322">Por exemplo, se a tabela de back-end contém demasiadas colunas e só precisa de tooreference um subconjunto de colunas de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="7a18b-323">modelo escrito Olá requer toodefine todas as colunas de Olá definidas no back-end das Mobile Apps de Olá na sua classe de dados.</span><span class="sxs-lookup"><span data-stu-id="7a18b-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="7a18b-324">Na maioria das chamadas à API para aceder aos dados de Olá é semelhante toohello escreveu chamadas de programação.</span><span class="sxs-lookup"><span data-stu-id="7a18b-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="7a18b-325">Olá principal diferença é que no modelo sem tipo Olá invocar métodos em Olá **MobileServiceJsonTable** objeto, em vez de Olá **MobileServiceTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="7a18b-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="7a18b-326"><a name="json_instance"></a>Criar uma instância de uma tabela sem tipo</span><span class="sxs-lookup"><span data-stu-id="7a18b-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="7a18b-327">Toohello semelhante escreveu modelo, pode começa por colocar uma referência de tabela, mas neste caso é um **MobileServicesJsonTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="7a18b-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="7a18b-328">Obter referência Olá ao chamar Olá **getTable** método numa instância do cliente de Olá:</span><span class="sxs-lookup"><span data-stu-id="7a18b-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="7a18b-329">Assim que tiver criado uma instância de Olá **MobileServiceJsonTable**, tem Olá virtualmente API mesmo disponível como com o modelo de programação escrito Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="7a18b-330">Em alguns casos, os métodos de Olá assumem um parâmetro sem tipo em vez de um parâmetro com tipo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="7a18b-331"><a name="json_insert"></a>Inserir uma tabela sem tipo</span><span class="sxs-lookup"><span data-stu-id="7a18b-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="7a18b-332">Olá a seguir mostra código como toodo insert.</span><span class="sxs-lookup"><span data-stu-id="7a18b-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="7a18b-333">Olá primeiro passo é toocreate um [JsonObject][1], que faz parte de Olá [gson] [ 3] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7a18b-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="7a18b-334">Em seguida, utilize **INSERT ()** tooinsert objeto sem tipo de Olá na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="7a18b-335">Se precisar de tooget Olá ID de objeto de Olá inserir, utilize Olá **getAsJsonPrimitive()** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="7a18b-336"><a name="json_delete"></a>Eliminar uma tabela sem tipo</span><span class="sxs-lookup"><span data-stu-id="7a18b-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="7a18b-337">Olá código seguinte mostra como toodelete uma instância, Olá neste caso, a mesma instância de um **JsonObject** que foi criado no antes de Olá *inserir* exemplo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="7a18b-338">código de Olá é Olá mesmo tal como acontece com Olá escreveu maiúsculas e minúsculas, mas o método de Olá tem uma assinatura diferente, porque referencia uma **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="7a18b-339">Também pode eliminar uma instância diretamente, utilizando o respetivo ID:</span><span class="sxs-lookup"><span data-stu-id="7a18b-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="7a18b-340"><a name="json_get"></a>Devolver todas as linhas a partir de uma tabela sem tipo</span><span class="sxs-lookup"><span data-stu-id="7a18b-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="7a18b-341">Olá a seguir mostra código como tooretrieve uma tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="7a18b-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="7a18b-342">Uma vez que estiver a utilizar uma tabela em JSON, pode obter apenas algumas das colunas da tabela de Olá seletivamente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="7a18b-343">Olá mesmo conjunto de filtragem, filtragem e paginação métodos disponíveis para o modelo com tipo Olá estão disponíveis para o modelo sem tipo Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="7a18b-344"><a name="offline-sync"></a>Implementar a Sincronização Offline</span><span class="sxs-lookup"><span data-stu-id="7a18b-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="7a18b-345">Olá cliente SDK do Azure Mobile Apps também implementa sincronização offline dos dados utilizando um toostore de base de dados do SQLite uma cópia dos dados do servidor de Olá localmente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="7a18b-346">Operações executadas numa tabela offline não necessitam de conectividade móveis toowork.</span><span class="sxs-lookup"><span data-stu-id="7a18b-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="7a18b-347">Ajudas de sincronização offline no resiliência e desempenho em despesa Olá de lógica mais complexa para resolução de conflitos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="7a18b-348">Olá cliente SDK do Azure Mobile Apps implementa Olá seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="7a18b-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="7a18b-349">Sincronização incremental: Registos nova e atualizados apenas são transferidos, guardar o consumo de memória e largura de banda.</span><span class="sxs-lookup"><span data-stu-id="7a18b-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="7a18b-350">Simultaneidade otimista: Operações são consideradas toosucceed.</span><span class="sxs-lookup"><span data-stu-id="7a18b-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="7a18b-351">Resolução de conflitos é deferida até que as atualizações são executadas no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="7a18b-352">Resolução de conflitos: Olá que SDK Deteta quando uma alteração em conflito foram efetuada no servidor de Olá e fornece hooks utilizador de Olá tooalert.</span><span class="sxs-lookup"><span data-stu-id="7a18b-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="7a18b-353">Eliminação de forma recuperável: Registos eliminados são marcados eliminados, permitindo que os outro dispositivos tooupdate respetiva cache offline.</span><span class="sxs-lookup"><span data-stu-id="7a18b-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="7a18b-354">Iniciar Sincronização Offline</span><span class="sxs-lookup"><span data-stu-id="7a18b-354">Initialize Offline Sync</span></span>

<span data-ttu-id="7a18b-355">Cada tabela offline tem de ser definida na cache de offline Olá antes de utilização.</span><span class="sxs-lookup"><span data-stu-id="7a18b-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="7a18b-356">Normalmente, a definição da tabela é feita imediatamente após a criação de hello do cliente de Olá:</span><span class="sxs-lookup"><span data-stu-id="7a18b-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="7a18b-357">Obter uma referência toohello Offline tabela de Cache</span><span class="sxs-lookup"><span data-stu-id="7a18b-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="7a18b-358">Para uma tabela online, utilize `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="7a18b-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="7a18b-359">Para uma tabela offline, utilize `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="7a18b-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="7a18b-360">Olá todos os métodos que estão disponíveis em tabelas online (incluindo filtragem, ordenação, paginação, inserir dados, atualizar dados e a eliminação de dados) funcionam igualmente bem em tabelas online e offline.</span><span class="sxs-lookup"><span data-stu-id="7a18b-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="7a18b-361">Sincronizar Olá Local Offline Cache</span><span class="sxs-lookup"><span data-stu-id="7a18b-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="7a18b-362">A sincronização é controlo Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="7a18b-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="7a18b-363">Segue-se um método de sincronização de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a18b-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="7a18b-364">Se for fornecido um nome de consulta toohello `.pull(query, queryname)` método, em seguida, sincronização incremental é registos apenas tooreturn utilizado e que foram criados ou alterados desde a solicitação de Olá pela última vez foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="7a18b-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="7a18b-365">Identificador de conflitos durante a Sincronização Offline</span><span class="sxs-lookup"><span data-stu-id="7a18b-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="7a18b-366">Se acontecer um conflito durante um `.push()` operação, uma `MobileServiceConflictException` é emitida.</span><span class="sxs-lookup"><span data-stu-id="7a18b-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="7a18b-367">item de servidor emitido Olá está incorporado na exceção de Olá e podem ser obtida pelos `.getItem()` na exceção de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="7a18b-368">Ajuste push Olá ao chamar Olá seguintes itens no objeto de MobileServiceSyncContext Olá:</span><span class="sxs-lookup"><span data-stu-id="7a18b-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="7a18b-369">Depois de todos os conflitos são marcados como quiser, chamar `.push()` novamente tooresolve Olá todos os conflitos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="7a18b-370"><a name="custom-api"></a>Chamar uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="7a18b-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="7a18b-371">Uma API personalizada permite-lhe toodefine pontos finais personalizados que expõem funcionalidades do servidor que não mapear tooan inserir, atualizar, eliminar ou operação de leitura.</span><span class="sxs-lookup"><span data-stu-id="7a18b-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="7a18b-372">Ao utilizar uma API personalizada, pode ter mais controlo sobre mensagens, incluindo o ler, definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem que não sejam JSON.</span><span class="sxs-lookup"><span data-stu-id="7a18b-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="7a18b-373">A partir de um cliente do Android, tem de chamar Olá **invokeApi** método toocall Olá personalizado ponto final de API.</span><span class="sxs-lookup"><span data-stu-id="7a18b-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="7a18b-374">Olá exemplo seguinte mostra como toocall um ponto final de API com o nome **completeAll**, que devolve uma classe de coleção com o nome **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="7a18b-375">Olá **invokeApi** método é denominado no cliente Olá, o que envia uma mensagem de pedido toohello nova API personalizada.</span><span class="sxs-lookup"><span data-stu-id="7a18b-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="7a18b-376">resultado de Olá devolvido por API personalizada Olá apresentado numa caixa de diálogo mensagem, tal como quaisquer erros.</span><span class="sxs-lookup"><span data-stu-id="7a18b-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="7a18b-377">Outras versões **invokeApi** permitem-lhe enviar um objeto no corpo do pedido de Olá opcionalmente, especifique o método de Olá HTTP e enviar parâmetros de consulta com o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="7a18b-378">Sem tipos versões do **invokeApi** são fornecidos bem.</span><span class="sxs-lookup"><span data-stu-id="7a18b-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="7a18b-379"><a name="authentication"></a>Adicionar autenticação tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="7a18b-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="7a18b-380">Tutoriais já descrevem em detalhe como tooadd estas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="7a18b-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="7a18b-381">Serviço de aplicações suporta [autenticar utilizadores de aplicação](app-service-mobile-android-get-started-users.md) através de vários fornecedores de identidade externas: Facebook, Google, Account Microsoft, Twitter e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a18b-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="7a18b-382">Pode definir permissões de acesso de toorestrict tabelas para operações específicas tooonly autenticada utilizadores.</span><span class="sxs-lookup"><span data-stu-id="7a18b-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="7a18b-383">Também pode utilizar a identidade de Olá utilizadores autenticados tooimplement das regras de autorização no seu back-end.</span><span class="sxs-lookup"><span data-stu-id="7a18b-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="7a18b-384">São suportados dois fluxos de autenticação: um **servidor** fluxo e um **cliente** fluxo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="7a18b-385">fluxo de servidor Olá fornece a experiência de autenticação mais simples de Olá, como baseia-se na interface de web de fornecedores de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="7a18b-386">Não existem SDKs adicionais são tooimplement necessária autenticação de fluxo do servidor.</span><span class="sxs-lookup"><span data-stu-id="7a18b-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="7a18b-387">Autenticação de fluxo de servidor não fornece uma integração profunda em dispositivos móveis Olá e só é recomendada para uma prova de cenários de conceito.</span><span class="sxs-lookup"><span data-stu-id="7a18b-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="7a18b-388">fluxo de cliente Olá permite a integração mais profunda com as capacidades específicas do dispositivo, como o início de sessão único como depende SDKs fornecidas pelo fornecedor de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="7a18b-389">Por exemplo, pode integrar Olá Facebook SDK na sua aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="7a18b-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="7a18b-390">cliente para dispositivos móveis Olá trocas na aplicação do Facebook Olá e confirma o início de sessão antes de troca de aplicação móvel de back-tooyour.</span><span class="sxs-lookup"><span data-stu-id="7a18b-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="7a18b-391">Quatro passos são necessários tooenable autenticação na sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="7a18b-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="7a18b-392">Registe a aplicação para autenticação com um fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="7a18b-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="7a18b-393">Configure o back-end do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7a18b-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="7a18b-394">Restringir os utilizadores de tooauthenticated de permissões tabela apenas em Olá back-end do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7a18b-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="7a18b-395">Adicione a aplicação de tooyour de código de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7a18b-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="7a18b-396">Pode definir permissões de acesso de toorestrict tabelas para operações específicas tooonly autenticada utilizadores.</span><span class="sxs-lookup"><span data-stu-id="7a18b-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="7a18b-397">Também pode utilizar Olá SID de um utilizador autenticado toomodify pedidos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="7a18b-398">Para obter mais informações, consulte [introdução à autenticação] e Olá documentação HOWTO de SDK do servidor.</span><span class="sxs-lookup"><span data-stu-id="7a18b-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="7a18b-399"><a name="caching"></a>Autenticação: Fluxo de servidor</span><span class="sxs-lookup"><span data-stu-id="7a18b-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="7a18b-400">Olá código seguinte inicia um processo de início de sessão de fluxo de servidor utilizando o fornecedor de Google Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="7a18b-401">É necessária configuração adicional devido aos requisitos de segurança de Olá para o fornecedor de Google Olá:</span><span class="sxs-lookup"><span data-stu-id="7a18b-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="7a18b-402">Além disso, adicione Olá classe de atividade principal do método toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7a18b-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="7a18b-403">Olá `GOOGLE_LOGIN_REQUEST_CODE` definido no seu main atividade é utilizada para Olá `login()` método e dentro de Olá `onActivityResult()` método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="7a18b-404">Pode escolher qualquer número exclusivo, desde que hello mesmo número é utilizado no Olá `login()` método e Olá `onActivityResult()` método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="7a18b-405">Se separar o código de cliente Olá para um adaptador de serviço (conforme mostrado anteriormente), deve chamar os métodos de adequada de Olá no adaptador de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="7a18b-406">Também precisa de projeto de Olá tooconfigure para customtabs.</span><span class="sxs-lookup"><span data-stu-id="7a18b-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="7a18b-407">Primeiro, especifique um URL de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="7a18b-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="7a18b-408">Adicionar Olá seguinte fragmento demasiado`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="7a18b-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="7a18b-409">Adicionar Olá **redirectUriScheme** toohello `build.gradle` ficheiro para a sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="7a18b-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="7a18b-410">Por fim, adicione `com.android.support:customtabs:23.0.1` toohello a lista de dependências em Olá `build.gradle` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="7a18b-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="7a18b-411">Obter ID de Olá de Olá utilizador com sessão iniciada de um **MobileServiceUser** utilizando Olá **getUserId** método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="7a18b-412">Para obter um exemplo de como toouse Futures toocall Olá assíncrono início de sessão APIs, consulte [introdução à autenticação].</span><span class="sxs-lookup"><span data-stu-id="7a18b-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="7a18b-413">Olá esquema de URL mencionado diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="7a18b-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="7a18b-414">Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` corresponder a maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="7a18b-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="7a18b-415"><a name="caching"></a>Tokens de autenticação de cache</span><span class="sxs-lookup"><span data-stu-id="7a18b-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="7a18b-416">Colocação em cache os tokens de autenticação requer toostore Olá ID de utilizador e o token de autenticação localmente no dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="7a18b-417">Olá próxima vez que inicia a aplicação Olá, seleciona cache Olá, e se estes valores não estiverem presentes, pode ignorar registo de Olá no procedimento rehydrate cliente Olá com estes dados.</span><span class="sxs-lookup"><span data-stu-id="7a18b-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="7a18b-418">No entanto estes dados são sensíveis e devem ser armazenado encriptados para segurança no caso de telefone Olá obtém roubado.</span><span class="sxs-lookup"><span data-stu-id="7a18b-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="7a18b-419">Pode ver um exemplo completo de como autenticação toocache tokens no [secção de tokens de autenticação da Cache][7].</span><span class="sxs-lookup"><span data-stu-id="7a18b-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="7a18b-420">Quando tenta toouse um token expirado, receberá um *401 não autorizado* resposta.</span><span class="sxs-lookup"><span data-stu-id="7a18b-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="7a18b-421">Pode processar erros de autenticação utilizando filtros.</span><span class="sxs-lookup"><span data-stu-id="7a18b-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="7a18b-422">Filtros interceptar pedidos toohello back-end do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7a18b-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="7a18b-423">o código de filtro de Olá testa a resposta de Olá para um 401, aciona o processo de início de sessão Olá e, em seguida, retoma pedido Olá que gerou Olá 401.</span><span class="sxs-lookup"><span data-stu-id="7a18b-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="7a18b-424"><a name="refresh"></a>Utilize Tokens de atualização</span><span class="sxs-lookup"><span data-stu-id="7a18b-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="7a18b-425">token de Olá devolvido por autorização e autenticação do serviço de aplicações do Azure tem um tempo de vida definido de uma hora.</span><span class="sxs-lookup"><span data-stu-id="7a18b-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="7a18b-426">Após este período, tem de voltar utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="7a18b-427">Se for um token de longa duração que receberam através da autenticação de fluxo de cliente, em seguida, pode voltar a utilizar com autenticação do serviço de aplicações do Azure e a utilização de autorização Olá mesmo token.</span><span class="sxs-lookup"><span data-stu-id="7a18b-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="7a18b-428">Outro token do App Service do Azure é gerado com uma duração de novo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="7a18b-429">Também pode registar Olá fornecedor toouse Tokens de atualização.</span><span class="sxs-lookup"><span data-stu-id="7a18b-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="7a18b-430">Um Token de atualização não está sempre disponível.</span><span class="sxs-lookup"><span data-stu-id="7a18b-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="7a18b-431">É necessária configuração adicional:</span><span class="sxs-lookup"><span data-stu-id="7a18b-431">Additional configuration is required:</span></span>

* <span data-ttu-id="7a18b-432">Para **do Azure Active Directory**, configurar um segredo de cliente para Olá aplicação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a18b-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="7a18b-433">Especifique o segredo do cliente Olá no Olá App Service do Azure quando configurar a autenticação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a18b-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="7a18b-434">Quando chamar `.login()`, transmitir `response_type=code id_token` como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="7a18b-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="7a18b-435">Para **Google**, transmitir Olá `access_type=offline` como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="7a18b-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="7a18b-436">Para **Account Microsoft**, selecione Olá `wl.offline_access` âmbito.</span><span class="sxs-lookup"><span data-stu-id="7a18b-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="7a18b-437">chamar toorefresh um token, `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="7a18b-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="7a18b-438">Como melhor prática, crie um filtro que Deteta uma resposta 401 do servidor de Olá e tenta token de utilizador de Olá toorefresh.</span><span class="sxs-lookup"><span data-stu-id="7a18b-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="7a18b-439">Iniciar sessão com a autenticação de cliente-fluxo</span><span class="sxs-lookup"><span data-stu-id="7a18b-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="7a18b-440">processo geral de Olá para iniciar sessão com a autenticação de fluxo de cliente é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a18b-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="7a18b-441">Configure a autorização e autenticação do serviço de aplicações do Azure tal como faria com autenticação de servidor fluxo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="7a18b-442">Integre o SDK de fornecedor de autenticação Olá para autenticação tooproduce um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="7a18b-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="7a18b-443">Chamar Olá `.login()` método da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7a18b-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="7a18b-444">Substitua Olá `onSuccess()` método com independentemente código que queira toouse num início de sessão com êxito.</span><span class="sxs-lookup"><span data-stu-id="7a18b-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="7a18b-445">Olá `{provider}` cadeia é um fornecedor de válido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, ou **twitter**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="7a18b-446">Se tiver implementado a autenticação personalizada, em seguida, também pode utilizar etiquetas de fornecedor de autenticação personalizado de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="7a18b-447"><a name="adal"></a>Autenticar os utilizadores com Olá Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="7a18b-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="7a18b-448">Pode utilizar os utilizadores de toosign do Active Directory Authentication Library (ADAL) Olá na sua aplicação com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a18b-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="7a18b-449">A utilização de um início de sessão do fluxo de cliente, muitas vezes, é preferível toousing Olá `loginAsync()` métodos que fornece uma funcionalidade do UX mais nativa e permite a personalização adicional.</span><span class="sxs-lookup"><span data-stu-id="7a18b-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="7a18b-450">Configurar o back-end da aplicação móvel para o início de sessão do AAD ao seguinte Olá [como tooconfigure App Service para início de sessão do Active Directory] [ 22] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a18b-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="7a18b-451">Certifique-se de que toocomplete Olá passo opcional de registar uma aplicação cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="7a18b-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="7a18b-452">Instale ADAL modificando o Olá tooinclude do gradle ficheiros seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="7a18b-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="7a18b-453">Adicione Olá aplicação tooyour de código a seguir, tornando Olá substituições os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7a18b-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="7a18b-454">Substitua **aqui de autoridade de inserção** com o nome de Olá do inquilino Olá no qual que aprovisionou a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="7a18b-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="7a18b-455">formato de Olá deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7a18b-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="7a18b-456">Substitua **INSERT-RESOURCE-ID-aqui** com o ID de cliente Olá do back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="7a18b-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="7a18b-457">Pode obter ID de cliente Olá de Olá **avançadas** separador em **definições do Azure Active Directory** no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="7a18b-458">Substitua **INSERT-cliente ID aqui** com o ID de cliente Olá copiados da aplicação de cliente nativo Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="7a18b-459">Substitua **INSERT-REDIRECIONAMENTO-URI-aqui** com o seu site */.auth/login/done* ponto final, utilizando o esquema HTTPS de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a18b-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="7a18b-460">Este valor deve ser semelhante demasiado*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="7a18b-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="7a18b-461"><a name="filters"></a>Ajustar Olá comunicação cliente-servidor</span><span class="sxs-lookup"><span data-stu-id="7a18b-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="7a18b-462">Olá ligação de cliente é normalmente uma ligação de HTTP básica Olá subjacente biblioteca HTTP fornecida com Olá Android SDK a utilizar.</span><span class="sxs-lookup"><span data-stu-id="7a18b-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="7a18b-463">Existem várias razões, razão pela qual pretenda toochange que:</span><span class="sxs-lookup"><span data-stu-id="7a18b-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="7a18b-464">Pretende toouse um tempos de limite de tooadjust de biblioteca HTTP alternativo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="7a18b-465">Pretende tooprovide uma barra de progresso.</span><span class="sxs-lookup"><span data-stu-id="7a18b-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="7a18b-466">Pretende tooadd uma funcionalidade de gestão de toosupport API de cabeçalho personalizado.</span><span class="sxs-lookup"><span data-stu-id="7a18b-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="7a18b-467">Pretende toointercept uma resposta de falha para que pode implementar a reautenticação rápida.</span><span class="sxs-lookup"><span data-stu-id="7a18b-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="7a18b-468">Pretende que o serviço de análise do tooan de pedidos do toolog back-end.</span><span class="sxs-lookup"><span data-stu-id="7a18b-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="7a18b-469">Utilizar uma biblioteca de HTTP alternativo</span><span class="sxs-lookup"><span data-stu-id="7a18b-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="7a18b-470">Chamar Olá `.setAndroidHttpClientFactory()` método imediatamente depois de criar uma referência de cliente.</span><span class="sxs-lookup"><span data-stu-id="7a18b-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="7a18b-471">Por exemplo, tooset Olá ligação too60 segundos de tempo limite (em vez da predefinição de Olá 10 segundos):</span><span class="sxs-lookup"><span data-stu-id="7a18b-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="7a18b-472">Implementar um filtro de progresso</span><span class="sxs-lookup"><span data-stu-id="7a18b-472">Implement a Progress Filter</span></span>

<span data-ttu-id="7a18b-473">Pode implementar um intercept de cada pedido, implementando um `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="7a18b-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="7a18b-474">Por exemplo, o seguinte Olá atualiza uma barra de progresso previamente criada:</span><span class="sxs-lookup"><span data-stu-id="7a18b-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="7a18b-475">Pode ligar a este cliente de toohello de filtro da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7a18b-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="7a18b-476">Personalizar a cabeçalhos de pedido</span><span class="sxs-lookup"><span data-stu-id="7a18b-476">Customize Request Headers</span></span>

<span data-ttu-id="7a18b-477">Utilize o seguinte Olá `ServiceFilter` e anexe o filtro de Olá em Olá mesma forma que Olá `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="7a18b-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="7a18b-478"><a name="conversions"></a>Configurar serialização automática</span><span class="sxs-lookup"><span data-stu-id="7a18b-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="7a18b-479">Pode especificar uma estratégia de conversão aplica-se a coluna de tooevery utilizando Olá [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="7a18b-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="7a18b-480">biblioteca de cliente do Android Olá utiliza [gson] [ 3] em segundo plano de Olá tooserialize Java objetos tooJSON dados antes do envio de dados de Olá tooAzure do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7a18b-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="7a18b-481">Olá código seguinte utiliza Olá **setFieldNamingStrategy()** estratégia de Olá tooset de método.</span><span class="sxs-lookup"><span data-stu-id="7a18b-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="7a18b-482">Neste exemplo eliminará Olá inicial caráter (um "m") e caráter seguinte, em seguida, minúsculos Olá, para cada nome de campo.</span><span class="sxs-lookup"><span data-stu-id="7a18b-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="7a18b-483">Por exemplo, este seria ativar "mId" em "id".</span><span class="sxs-lookup"><span data-stu-id="7a18b-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="7a18b-484">Implementar um Olá de tooreduce de estratégia de conversão necessita para `SerializedName()` anotações na maioria dos campos.</span><span class="sxs-lookup"><span data-stu-id="7a18b-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="7a18b-485">Este código tem de ser executado antes de criar uma referência de cliente para dispositivos móveis utilizando Olá **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="7a18b-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[introdução à autenticação]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
