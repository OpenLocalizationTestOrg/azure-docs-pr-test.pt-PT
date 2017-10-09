---
title: "aaaDeploying grandes implementações"
description: "Saiba como implementações de grande toodeploy utilizando Olá Toolkit do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="d5286-103">Implementar grandes implementações</span><span class="sxs-lookup"><span data-stu-id="d5286-103">Deploying Large Deployments</span></span>
<span data-ttu-id="d5286-104">Se a sua implementação é demasiado grande toobe contido na pasta de approot Olá predefinido, pode utilizar um recurso de armazenamento local como a pasta de raiz de implementação de Olá para o JDK e servidor de aplicação.</span><span class="sxs-lookup"><span data-stu-id="d5286-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="d5286-105">toouse um recurso de armazenamento local como pasta raiz de implementação de Olá para implementações grandes</span><span class="sxs-lookup"><span data-stu-id="d5286-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="d5286-106">Crie um novo recurso do armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="d5286-106">Create a new local storage resource.</span></span> <span data-ttu-id="d5286-107">nome de Olá do recurso de Olá não importa.</span><span class="sxs-lookup"><span data-stu-id="d5286-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="d5286-108">Recursos de armazenamento é definida ao nível da função de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5286-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="d5286-109">Olá mais rápida forma tooaccess Olá armazenamento local caixa de diálogo Configuração, do qual pode criar um novo recurso do armazenamento local, é utilizando Olá os seguintes passos: função de Olá do rato no Olá **Explorador de projeto** vista (expandir a Projeto do Azure nó se não vir a função de Olá), clique em **Azure**e, em seguida, clique em **armazenamento Local**.</span><span class="sxs-lookup"><span data-stu-id="d5286-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="d5286-110">Dentro do Olá **armazenamento Local** caixa de diálogo, clique em **adicionar** toocreate um novo recurso do armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="d5286-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="d5286-111">Olá conjunto pretendido tooat de tamanho, pelo menos, 2048 MB (tudo menos poderá provocar Olá mesmo problemas de tamanho de ficheiro como seria encontrar Olá approot).</span><span class="sxs-lookup"><span data-stu-id="d5286-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="d5286-112">Certifique-se de que **apagar conteúdo de Olá quando é reciclada, instância de função Olá** é verificado; Isto irá ajudar a impedir a execução em conflitos com ficheiros pré-existentes no recurso de Olá de lógica de arranque da implementação de Olá Olá quando a função a instância é reciclada.</span><span class="sxs-lookup"><span data-stu-id="d5286-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="d5286-113">Certifique-se de que Olá **armazenar variável de ambiente Olá caminho do diretório do recurso após a implementação** valor é definido toohello cadeia **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="d5286-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="d5286-114">A caixa de diálogo de recursos de armazenamento local terá um aspeto semelhante toohello seguinte.</span><span class="sxs-lookup"><span data-stu-id="d5286-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="d5286-115">Em alternativa, se utilizar **DEPLOYROOT** como Olá *nome* do seu recurso local e não altere o nome de variável de ambiente gerado automaticamente do Olá (que será definido demasiado **DEPLOYROOT_PATH** nesse caso), que funciona para a sua aplicação bem.</span><span class="sxs-lookup"><span data-stu-id="d5286-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="d5286-116">Informações adicionais sobre a criação de um recurso de armazenamento local podem ser encontradas em [propriedades de armazenamento Local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="d5286-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="d5286-117">Veja Também</span><span class="sxs-lookup"><span data-stu-id="d5286-117">See Also</span></span>
<span data-ttu-id="d5286-118">[Toolkit do Azure do Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d5286-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="d5286-119">[Criar uma aplicação do Olá mundo do Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d5286-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="d5286-120">[Instalar Olá Toolkit de Azure do Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d5286-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="d5286-121">Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="d5286-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
