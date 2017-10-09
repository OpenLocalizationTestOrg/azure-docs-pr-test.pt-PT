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
## <a name="set-up-your-project"></a>Configurar o projeto

> Prefere toodownload projeto do Android Studio este exemplo em vez disso? [Transferir um projeto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.


### <a name="create-a-new-project"></a>Criar um novo projeto 
1.  Abra o Android Studio, aceda a:`File` > `New` > `New Project`
2.  Nome da aplicação e clique em`Next`
3.  Certifique-se de que tooselect *API 21 ou mais recente (Android 5.0)* e clique em`Next`
4.  Deixe `Empty Activity`, clique em `Next`, em seguida,`Finish`


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Adicionar Olá biblioteca de autenticação da Microsoft (MSAL) tooyour projeto
1.  No Android Studio, aceda a:`Gradle Scripts` > `build.gradle (Module: app)`
2.  Copiar e colar seguinte de Olá código em `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Sobre este pacote

pacote de Olá acima instala Olá biblioteca de autenticação da Microsoft (MSAL). MSAL processa a aquisição, colocação em cache e atualizar o utilizador tokens utilizados tooaccess APIs protegidas pelo ponto final do Azure Active Directory v2.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Criar a IU da aplicação

1.  Abra: `activity_main.xml` em`res` > `layout`
2.  Esquema de atividade de Olá de alteração de `android.support.constraint.ConstraintLayout` ou outros demasiado`LinearLayout`
3.  Adicionar `android:orientation="vertical"` propriedade demasiado`LinearLayout` nós
4.  Copiar e colar seguinte de Olá code para Olá `LinearLayout` nó, substituindo o conteúdo atual Olá:

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

