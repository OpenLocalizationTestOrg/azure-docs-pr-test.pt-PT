---
title: "aaaAzure AD v2 iOS introdução - configuração | Microsoft Docs"
description: "Como as aplicações do iOS (Swift) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="75fbe-103">Configurar a sua aplicação iOS</span><span class="sxs-lookup"><span data-stu-id="75fbe-103">Setting up your iOS application</span></span>

<span data-ttu-id="75fbe-104">Esta secção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate uma aplicação iOS (Swift) com *início de sessão com a Microsoft* que possa consultar APIs da Web que necessitam de um token.</span><span class="sxs-lookup"><span data-stu-id="75fbe-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="75fbe-105">Prefere toodownload projeto do XCode este exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="75fbe-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="75fbe-106">[Transferir um projeto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.</span><span class="sxs-lookup"><span data-stu-id="75fbe-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="75fbe-107">Instalar Carthage toodownload e criar MSAL</span><span class="sxs-lookup"><span data-stu-id="75fbe-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="75fbe-108">Gestor de pacotes Carthage é utilizado durante o período de pré-visualização de Olá de MSAL – é integrado com o XCode, mantendo a capacidade de Olá da biblioteca do Microsoft toomake alterações toohello.</span><span class="sxs-lookup"><span data-stu-id="75fbe-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="75fbe-109">Transfira e instale a versão mais recente do Olá do Carthage [aqui](https://github.com/Carthage/Carthage/releases "Carthage URL de transferência")</span><span class="sxs-lookup"><span data-stu-id="75fbe-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="75fbe-110">Criar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="75fbe-110">Creating your application</span></span>

1.  <span data-ttu-id="75fbe-111">Abra o Xcode e selecione`Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="75fbe-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="75fbe-112">Selecione `iOS`  >  `Single view Application` e clique em *seguinte*</span><span class="sxs-lookup"><span data-stu-id="75fbe-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="75fbe-113">Dê um nome de produto e clique em *seguinte*</span><span class="sxs-lookup"><span data-stu-id="75fbe-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="75fbe-114">Selecione uma pasta toocreate a aplicação e clique em *criar*</span><span class="sxs-lookup"><span data-stu-id="75fbe-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="75fbe-115">Criar Olá MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="75fbe-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="75fbe-116">Siga as instruções de Olá abaixo toopull e, em seguida, criar a versão mais recente do Olá das bibliotecas MSAL Carthage a utilizar:</span><span class="sxs-lookup"><span data-stu-id="75fbe-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="75fbe-117">Abra o terminal de bash Olá e aceda a pasta raiz da aplicação toohello</span><span class="sxs-lookup"><span data-stu-id="75fbe-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="75fbe-118">Olá abaixo de copiar e colar Olá bash terminal toocreate um ficheiro de 'Cartfile':</span><span class="sxs-lookup"><span data-stu-id="75fbe-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="75fbe-119">Copie e cole Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="75fbe-119">Copy and paste hello below.</span></span> <span data-ttu-id="75fbe-120">Este comando obtém as dependências para uma pasta de Carthage/Checkouts, em seguida, baseia-se a biblioteca MSAL Olá:</span><span class="sxs-lookup"><span data-stu-id="75fbe-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="75fbe-121">processo de Olá acima é toodownload utilizado e compilação Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="75fbe-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="75fbe-122">MSAL processa a aquisição, colocação em cache e atualizar o utilizador tokens utilizados tooaccess APIs protegidas pelo Olá v2 do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="75fbe-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="75fbe-123">Adicionar Olá MSAL framework tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="75fbe-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="75fbe-124">No Xcode, abra Olá `General` separador</span><span class="sxs-lookup"><span data-stu-id="75fbe-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="75fbe-125">Aceda toohello `Linked Frameworks and Libraries` secção e clique em`+`</span><span class="sxs-lookup"><span data-stu-id="75fbe-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="75fbe-126">Selecione `Add other…`</span><span class="sxs-lookup"><span data-stu-id="75fbe-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="75fbe-127">Selecione: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` e clique em *abra*.</span><span class="sxs-lookup"><span data-stu-id="75fbe-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="75fbe-128">Deverá ver `MSAL.framework` adicionado toohello lista.</span><span class="sxs-lookup"><span data-stu-id="75fbe-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="75fbe-129">Aceda demasiado`Build Phases` separador e clique em `+` ícone, escolha`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="75fbe-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="75fbe-130">Adicionar Olá seguintes conteúdos toohello *script área*:</span><span class="sxs-lookup"><span data-stu-id="75fbe-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="75fbe-131">Adicionar Olá seguir demasiado<code>Input Files</code> clicando <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="75fbe-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="75fbe-132">Criar a IU da aplicação</span><span class="sxs-lookup"><span data-stu-id="75fbe-132">Creating your application’s UI</span></span>
<span data-ttu-id="75fbe-133">Um ficheiro de Main.storyboard automaticamente deverá ser criado como parte do seu modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="75fbe-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="75fbe-134">Siga as instruções de Olá abaixo toocreate Olá aplicação IU:</span><span class="sxs-lookup"><span data-stu-id="75fbe-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="75fbe-135">Controlar + clique `Main.storyboard` toobring configurar menu contextuais Olá e, em seguida, clique em:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="75fbe-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="75fbe-136">Substitua Olá `<scenes>` nó com o código de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="75fbe-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
