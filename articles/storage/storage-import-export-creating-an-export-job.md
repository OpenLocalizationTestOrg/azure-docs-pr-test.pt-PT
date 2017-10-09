---
title: "uma tarefa para Azure importar/exportar a exportação de aaaCreate | Microsoft Docs"
description: "Saiba como toocreate uma exportação da tarefa para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="c613c-103">Criar uma tarefa de exportação para Olá serviço importar/exportar do Azure</span><span class="sxs-lookup"><span data-stu-id="c613c-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="c613c-104">Criar uma tarefa de exportação para o serviço de importação/exportação do Microsoft Azure Olá utilizando a REST API de Olá envolve Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c613c-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="c613c-105">Selecionar Olá blobs tooexport.</span><span class="sxs-lookup"><span data-stu-id="c613c-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="c613c-106">Obter uma localização de envio.</span><span class="sxs-lookup"><span data-stu-id="c613c-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="c613c-107">A criar tarefa de exportação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-107">Creating hello export job.</span></span>

-   <span data-ttu-id="c613c-108">Envio sua tooMicrosoft unidades vazio através de um serviço de carrier suportados.</span><span class="sxs-lookup"><span data-stu-id="c613c-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="c613c-109">A atualizar a tarefa de exportação de Olá com informações de pacote Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="c613c-110">Receber Olá unidades novamente a partir do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c613c-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="c613c-111">Consulte [utilizando Olá importação/exportação do Windows Azure serviço tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para uma descrição geral do serviço de importação/exportação Olá e um tutorial que demonstra como toouse Olá [portal do Azure](https://portal.azure.com/) toocreate e gerir importação e exportação de tarefas.</span><span class="sxs-lookup"><span data-stu-id="c613c-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="c613c-112">Selecionar tooexport de blobs</span><span class="sxs-lookup"><span data-stu-id="c613c-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="c613c-113">toocreate uma tarefa de exportação, terá de tooprovide uma lista de blobs que pretende que tooexport da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c613c-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="c613c-114">Existem algumas formas tooselect blobs toobe exportado:</span><span class="sxs-lookup"><span data-stu-id="c613c-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="c613c-115">Pode utilizar um tooselect de caminho relativo blob um blob único e todos os respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="c613c-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="c613c-116">Pode utilizar um tooselect de caminho relativo blob um blob único excluindo respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="c613c-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="c613c-117">Pode utilizar um caminho relativo de blob e um tooselect de tempo de instantâneos um único instantâneo.</span><span class="sxs-lookup"><span data-stu-id="c613c-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="c613c-118">Pode utilizar um tooselect de prefixo de blob todos os blobs e instantâneos com Olá fornecido prefixo.</span><span class="sxs-lookup"><span data-stu-id="c613c-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="c613c-119">Pode exportar todos os blobs e instantâneos na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="c613c-120">Para obter mais informações sobre como especificar blobs tooexport, consulte Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="c613c-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="c613c-121">Obter a localização de envio</span><span class="sxs-lookup"><span data-stu-id="c613c-121">Obtaining your shipping location</span></span>
<span data-ttu-id="c613c-122">Antes de criar uma tarefa de exportação, terá de tooobtain um nome de localização de envio e o endereço ao chamar Olá [obter localização](https://portal.azure.com) ou [lista localizações](/rest/api/storageimportexport/listlocations) operação.</span><span class="sxs-lookup"><span data-stu-id="c613c-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="c613c-123">`List Locations`irá devolver uma lista de localizações e os respetivos endereços de correio postal.</span><span class="sxs-lookup"><span data-stu-id="c613c-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="c613c-124">Pode selecionar uma localização Olá devolvida lista e são enviados o seu endereço de toothat unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="c613c-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="c613c-125">Também pode utilizar Olá `Get Location` Olá tooobtain de operação de envio endereço para uma localização específica diretamente.</span><span class="sxs-lookup"><span data-stu-id="c613c-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="c613c-126">Siga os passos de Olá abaixo localização de envio de Olá tooobtain:</span><span class="sxs-lookup"><span data-stu-id="c613c-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="c613c-127">Identifica o nome de Olá de localização de Olá da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c613c-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="c613c-128">Este valor pode ser encontrado na Olá **localização** campo na conta de armazenamento a Olá **Dashboard** no clássico Olá portal ou consultado para utilizando a operação de API de gestão do serviço de Olá [obter Propriedades da conta de armazenamento](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="c613c-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="c613c-129">Obter a localização de Olá que estão disponíveis tooprocess esta conta de armazenamento ao chamar Olá `Get Location` operação.</span><span class="sxs-lookup"><span data-stu-id="c613c-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="c613c-130">Se hello `AlternateLocations` propriedade de localização de Olá contém localização Olá próprio, em seguida, é toouse pode nesta localização.</span><span class="sxs-lookup"><span data-stu-id="c613c-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="c613c-131">Caso contrário, chamar Olá `Get Location` operação com uma das localizações alternativas Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="c613c-132">a localização original Olá pode estar fechada temporariamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="c613c-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="c613c-133">Criar tarefa de exportação de Olá</span><span class="sxs-lookup"><span data-stu-id="c613c-133">Creating hello export job</span></span>
 <span data-ttu-id="c613c-134">tarefa de exportação de Olá toocreate, chamada Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="c613c-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="c613c-135">Terá de Olá tooprovide seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c613c-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="c613c-136">Um nome para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-136">A name for hello job.</span></span>

-   <span data-ttu-id="c613c-137">nome da conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-137">hello storage account name.</span></span>

-   <span data-ttu-id="c613c-138">Olá envio de nome de localização, obtido no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="c613c-139">Um tipo de tarefa (exportação).</span><span class="sxs-lookup"><span data-stu-id="c613c-139">A job type (Export).</span></span>

-   <span data-ttu-id="c613c-140">endereço de retorno olá onde devem ser enviadas Olá unidades após conclusão da tarefa de exportação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="c613c-141">Olá toobe de lista de blobs (ou prefixos de blob) exportado.</span><span class="sxs-lookup"><span data-stu-id="c613c-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="c613c-142">As unidades de envio</span><span class="sxs-lookup"><span data-stu-id="c613c-142">Shipping your drives</span></span>
 <span data-ttu-id="c613c-143">Em seguida, utilizar Olá ferramenta de importação/exportação do Azure toodetermine Olá número de unidades que precisa de toosend, com base em blobs Olá que selecionou toobe exportado e Olá tamanho de unidade.</span><span class="sxs-lookup"><span data-stu-id="c613c-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="c613c-144">Consulte Olá [referência de ferramenta de importação/exportação do Azure](storage-import-export-tool-how-to-v1.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="c613c-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="c613c-145">Pacote de pacote Olá unidades numa única e envie-los toohello endereço obtido no Olá passo anterior.</span><span class="sxs-lookup"><span data-stu-id="c613c-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="c613c-146">Tenha em atenção Olá número do seu pacote para o passo seguinte Olá de controlo.</span><span class="sxs-lookup"><span data-stu-id="c613c-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="c613c-147">Tem de enviar a unidades através de um serviço operadora suportados, o que irá fornecer um número de controlo do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="c613c-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="c613c-148">Atualizar a tarefa de exportação de Olá com as suas informações de pacote</span><span class="sxs-lookup"><span data-stu-id="c613c-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="c613c-149">Depois de ter o seu número de controlo, chamar Olá [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) nome da operação tooupdated Olá operadora e o controlo número para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="c613c-150">Opcionalmente, pode especificar Olá número de unidades, endereço do remetente Olá e data de envio de Olá bem.</span><span class="sxs-lookup"><span data-stu-id="c613c-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="c613c-151">Pacotes hello a receber</span><span class="sxs-lookup"><span data-stu-id="c613c-151">Receiving hello package</span></span>
 <span data-ttu-id="c613c-152">Depois de ter sido processada a tarefa de exportação, será devolvida a unidades tooyou com os seus dados encriptados.</span><span class="sxs-lookup"><span data-stu-id="c613c-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="c613c-153">Pode obter a chave do BitLocker Olá para cada uma das unidades de Olá ao chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="c613c-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="c613c-154">Em seguida, pode desbloquear unidade Olá utilizando a chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="c613c-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="c613c-155">ficheiro de manifesto de unidade de Olá em cada unidade contém a lista de Olá dos ficheiros na unidade de Olá, bem como endereço de blob original Olá para cada ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c613c-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c613c-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c613c-156">Next steps</span></span>

* [<span data-ttu-id="c613c-157">Utilizar a REST API do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="c613c-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
