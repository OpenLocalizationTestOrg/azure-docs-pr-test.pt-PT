---
title: "aaaCreate uma tarefa de importação para o Azure importar/exportar | Microsoft Docs"
description: "Saiba como toocreate uma importação de Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="42256-103">Criar uma tarefa de importação para Olá serviço importar/exportar do Azure</span><span class="sxs-lookup"><span data-stu-id="42256-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="42256-104">Criar uma tarefa de importação para o serviço de importação/exportação do Microsoft Azure Olá utilizando a REST API de Olá envolve Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="42256-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="42256-105">A preparar unidades com Olá ferramenta de importação/exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="42256-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="42256-106">Obter Olá localização toowhich tooship Olá unidade.</span><span class="sxs-lookup"><span data-stu-id="42256-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="42256-107">A criar tarefa de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-107">Creating hello import job.</span></span>

-   <span data-ttu-id="42256-108">Envio Olá unidades tooMicrosoft através de um serviço de carrier suportados.</span><span class="sxs-lookup"><span data-stu-id="42256-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="42256-109">Atualizar a tarefa de importação de Olá com Olá detalhes de envio.</span><span class="sxs-lookup"><span data-stu-id="42256-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="42256-110">Consulte [utilizando Olá importação/exportação do Microsoft Azure service tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para uma descrição geral do serviço de importação/exportação Olá e um tutorial que demonstra como toouse Olá [portal do Azure](https://portal.azure.com/) toocreate e gerir importação e exportação de tarefas.</span><span class="sxs-lookup"><span data-stu-id="42256-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="42256-111">Preparar as unidades com Olá ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="42256-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="42256-112">Olá passos tooprepare unidades para uma tarefa de importação são Olá, mesmo se criar Olá portal de Olá jobvia ou através de Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="42256-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="42256-113">Segue-se uma breve descrição geral da preparação da unidade.</span><span class="sxs-lookup"><span data-stu-id="42256-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="42256-114">Consulte toohello [Azure importação ExportTool referência](storage-import-export-tool-how-to-v1.md) para obter instruções completas.</span><span class="sxs-lookup"><span data-stu-id="42256-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="42256-115">Pode transferir a ferramenta de importação/exportação do Azure de Olá [aqui](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="42256-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="42256-116">Envolve a preparação da sua unidade:</span><span class="sxs-lookup"><span data-stu-id="42256-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="42256-117">Identificar Olá dados toobe importado.</span><span class="sxs-lookup"><span data-stu-id="42256-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="42256-118">Identificar os blobs de destino de Olá no armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42256-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="42256-119">Utilizar Olá ferramenta de importação/exportação do Azure toocopy tooone os dados ou mais unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="42256-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="42256-120">Olá ferramenta de importação/exportação do Azure também irá gerar um ficheiro de manifesto para cada uma das unidades de Olá conforme está preparado.</span><span class="sxs-lookup"><span data-stu-id="42256-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="42256-121">Contém um ficheiro de manifesto:</span><span class="sxs-lookup"><span data-stu-id="42256-121">A manifest file contains:</span></span>

-   <span data-ttu-id="42256-122">Enumeração de todos os ficheiros de Olá concebida para carregar e mapeamentos de Olá de tooblobs estes ficheiros.</span><span class="sxs-lookup"><span data-stu-id="42256-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="42256-123">Somas de verificação de segmentos de Olá de cada ficheiro.</span><span class="sxs-lookup"><span data-stu-id="42256-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="42256-124">Informações sobre tooassociate de metadados e as propriedades de Olá com cada blob.</span><span class="sxs-lookup"><span data-stu-id="42256-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="42256-125">Uma lista de Olá ação tootake se um blob que está a ser carregado tem Olá mesmo nome como um blob existente no contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="42256-126">Opções possíveis: a) Substituir BLOBs Olá com o ficheiro de Olá, b) manter blob existente Olá e ignorar a carregar ficheiro Olá, c) Acrescentar um nome de toohello sufixo, para que este não entra em conflito com outros ficheiros.</span><span class="sxs-lookup"><span data-stu-id="42256-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="42256-127">Obter a localização de envio</span><span class="sxs-lookup"><span data-stu-id="42256-127">Obtaining your shipping location</span></span>

<span data-ttu-id="42256-128">Antes de criar uma tarefa de importação, terá de tooobtain um nome de localização de envio e o endereço ao chamar Olá [lista localizações](/rest/api/storageimportexport/listlocations) operação.</span><span class="sxs-lookup"><span data-stu-id="42256-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="42256-129">`List Locations`irá devolver uma lista de localizações e os respetivos endereços de correio postal.</span><span class="sxs-lookup"><span data-stu-id="42256-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="42256-130">Pode selecionar uma localização Olá devolvida lista e são enviados o seu endereço de toothat unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="42256-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="42256-131">Também pode utilizar Olá `Get Location` Olá tooobtain de operação de envio endereço para uma localização específica diretamente.</span><span class="sxs-lookup"><span data-stu-id="42256-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="42256-132">Siga os passos de Olá abaixo localização de envio de Olá tooobtain:</span><span class="sxs-lookup"><span data-stu-id="42256-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="42256-133">Identifica o nome de Olá de localização de Olá da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="42256-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="42256-134">Este valor pode ser encontrado na Olá **localização** campo na conta de armazenamento a Olá **Dashboard** no Olá Azure portal ou consultado para utilizando a operação de API de gestão do serviço de Olá [obter armazenamento Propriedades da conta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="42256-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="42256-135">Obter a localização de Olá que está disponível tooprocess esta conta de armazenamento ao chamar Olá `Get Location` operação.</span><span class="sxs-lookup"><span data-stu-id="42256-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="42256-136">Se hello `AlternateLocations` propriedade de localização de Olá contém localização Olá próprio, em seguida, é toouse pode nesta localização.</span><span class="sxs-lookup"><span data-stu-id="42256-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="42256-137">Caso contrário, chamar Olá `Get Location` operação com uma das localizações alternativas Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="42256-138">a localização original Olá pode estar fechada temporariamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="42256-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="42256-139">Criar tarefa de importação de Olá</span><span class="sxs-lookup"><span data-stu-id="42256-139">Creating hello import job</span></span>
<span data-ttu-id="42256-140">tarefa de importação de Olá toocreate, chamada Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="42256-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="42256-141">Terá de Olá tooprovide seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="42256-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="42256-142">Um nome para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-142">A name for hello job.</span></span>

-   <span data-ttu-id="42256-143">nome da conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-143">hello storage account name.</span></span>

-   <span data-ttu-id="42256-144">Olá envio de nome de localização, obtido a partir do passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="42256-145">Um tipo de tarefa (importar).</span><span class="sxs-lookup"><span data-stu-id="42256-145">A job type (Import).</span></span>

-   <span data-ttu-id="42256-146">endereço de retorno olá onde devem ser enviadas Olá unidades após conclusão da tarefa de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="42256-147">lista de Olá de unidades de tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="42256-147">hello list of drives in hello job.</span></span> <span data-ttu-id="42256-148">Para cada unidade, tem de incluir Olá informações que foi obtidas durante o passo de preparação de unidade de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="42256-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="42256-149">Id de unidade de Olá</span><span class="sxs-lookup"><span data-stu-id="42256-149">hello drive Id</span></span>

    -   <span data-ttu-id="42256-150">chave do BitLocker Olá</span><span class="sxs-lookup"><span data-stu-id="42256-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="42256-151">caminho relativo do ficheiro de manifesto de Olá no disco rígido Olá</span><span class="sxs-lookup"><span data-stu-id="42256-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="42256-152">Olá Base16 codificado hash do ficheiro de manifesto MD5</span><span class="sxs-lookup"><span data-stu-id="42256-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="42256-153">As unidades de envio</span><span class="sxs-lookup"><span data-stu-id="42256-153">Shipping your drives</span></span>
<span data-ttu-id="42256-154">Tem a enviar o seu endereço de toohello de unidades que obteve no passo anterior Olá, e tem de fornecer Olá serviço de importação/exportação com Olá número de pacotes de Olá de controlo.</span><span class="sxs-lookup"><span data-stu-id="42256-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="42256-155">Tem de enviar a unidades através de um serviço operadora suportados, o que irá fornecer um número de controlo do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="42256-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="42256-156">Atualizar a tarefa de importação de Olá com as suas informações de envio</span><span class="sxs-lookup"><span data-stu-id="42256-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="42256-157">Depois de ter o seu número de controlo, chamar Olá [propriedades da tarefa de atualização](/api/storageimportexport/jobs#Jobs_Update) Olá tooupdate de operação de envio nome da operadora, o número de controlo de Olá para a tarefa de Olá e o número de conta de carrier Olá para envio de retorno.</span><span class="sxs-lookup"><span data-stu-id="42256-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="42256-158">Opcionalmente, pode especificar o número de Olá de unidades e Olá, bem como a data de envio.</span><span class="sxs-lookup"><span data-stu-id="42256-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42256-159">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="42256-159">Next steps</span></span>

* [<span data-ttu-id="42256-160">Utilizar a REST API do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="42256-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
