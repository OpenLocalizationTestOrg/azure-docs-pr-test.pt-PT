---
title: "aaaAzure AD v2 Android introdução - configuração | Microsoft Docs"
description: Como uma ap de Android pode obter um token de acesso e chamar Graph API do Microsoft ou de APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="6d9ef-103">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="6d9ef-103">Set up your project</span></span>

> <span data-ttu-id="6d9ef-104">Prefere toodownload projeto do Android Studio este exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="6d9ef-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="6d9ef-105">[Transferir um projeto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.</span><span class="sxs-lookup"><span data-stu-id="6d9ef-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="6d9ef-106">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="6d9ef-106">Create a new project</span></span> 
1.  <span data-ttu-id="6d9ef-107">Abra o Android Studio, aceda a:`File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="6d9ef-108">Nome da aplicação e clique em`Next`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="6d9ef-109">Certifique-se de que tooselect *API 21 ou mais recente (Android 5.0)* e clique em`Next`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="6d9ef-110">Deixe `Empty Activity`, clique em `Next`, em seguida,`Finish`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="6d9ef-111">Adicionar Olá biblioteca de autenticação da Microsoft (MSAL) tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="6d9ef-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="6d9ef-112">No Android Studio, aceda a:`Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="6d9ef-113">Copiar e colar seguinte de Olá código em `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="6d9ef-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="6d9ef-114">Sobre este pacote</span><span class="sxs-lookup"><span data-stu-id="6d9ef-114">About this package</span></span>

<span data-ttu-id="6d9ef-115">pacote de Olá acima instala Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="6d9ef-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="6d9ef-116">MSAL processa a aquisição, colocação em cache e atualizar o utilizador tokens utilizados tooaccess APIs protegidas pelo ponto final do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="6d9ef-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="6d9ef-117">Criar a IU da aplicação</span><span class="sxs-lookup"><span data-stu-id="6d9ef-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="6d9ef-118">Abra: `activity_main.xml` em`res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="6d9ef-119">Esquema de atividade de Olá de alteração de `android.support.constraint.ConstraintLayout` ou outros demasiado`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="6d9ef-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="6d9ef-120">Adicionar `android:orientation="vertical"` propriedade demasiado`LinearLayout` nós</span><span class="sxs-lookup"><span data-stu-id="6d9ef-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="6d9ef-121">Copiar e colar seguinte de Olá code para Olá `LinearLayout` nó, substituindo o conteúdo atual Olá:</span><span class="sxs-lookup"><span data-stu-id="6d9ef-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

