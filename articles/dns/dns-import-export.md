---
title: "aaaImport e exportar uma zona de domínio do ficheiro tooAzure DNS utilizando a CLI do Azure 1.0 | Microsoft Docs"
description: Saiba como tooimport e exportar um DNS zona ficheiro tooAzure DNS ao utilizar a CLI do Azure 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="7fee5-103">Importar e exportar um ficheiro de zona DNS utilizando Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7fee5-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="7fee5-104">Este artigo explica como como tooimport e exportar ficheiros de zona DNS para utilizar o DNS do Azure Olá CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="7fee5-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="7fee5-105">Migração de zona de tooDNS de introdução</span><span class="sxs-lookup"><span data-stu-id="7fee5-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="7fee5-106">Um ficheiro de zona DNS é um ficheiro de texto que contém os detalhes de cada registo de sistema de nomes de domínio (DNS) na zona de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="7fee5-107">Segue um formato de padrão, tornando adequado para transferir os registos DNS entre sistemas DNS.</span><span class="sxs-lookup"><span data-stu-id="7fee5-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="7fee5-108">Utilizando um ficheiro de zona é um rápido, fiável e uma forma conveniente tootransfer uma zona DNS ou a sair DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="7fee5-109">O DNS do Azure suporta a importar e exportar ficheiros de zona utilizando Olá interface de linha de comandos (CLI) do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="7fee5-110">Importar de ficheiro de zona é **não** atualmente suportados através do Azure PowerShell ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="7fee5-111">Olá CLI do Azure 1.0 é uma ferramenta de linha de comandos de várias plataformas utilizada para gestão de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="7fee5-112">Está disponível para a plataformas Windows, Mac e Linux Olá de Olá [página de transferências do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7fee5-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="7fee5-113">Suporte em várias plataformas é importante para importar e exportar ficheiros de zona, porque Olá software de servidor de nome mais comuns, [VINCULAR](https://www.isc.org/downloads/bind/), normalmente, é executado no Linux.</span><span class="sxs-lookup"><span data-stu-id="7fee5-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="7fee5-114">Não existem atualmente duas versões do Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="7fee5-115">CLI1.0 baseia-se no Node.js e tem de comandos a partir "azure".</span><span class="sxs-lookup"><span data-stu-id="7fee5-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="7fee5-116">CLI2.0 baseia-se no Python e tem de começar com "az" de comandos.</span><span class="sxs-lookup"><span data-stu-id="7fee5-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="7fee5-117">Ao importar de ficheiro de zona é suportado em ambas as versões, recomendamos que utilize comandos CLI1.0 Olá, conforme descrito nesta página.</span><span class="sxs-lookup"><span data-stu-id="7fee5-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="7fee5-118">Obter o ficheiro de zona DNS existente</span><span class="sxs-lookup"><span data-stu-id="7fee5-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="7fee5-119">Antes de importar um ficheiro de zona DNS no DNS do Azure, terá de tooobtain uma cópia do ficheiro de zona Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="7fee5-120">origem deste ficheiro Olá depende em que zona DNS Olá está alojada atualmente.</span><span class="sxs-lookup"><span data-stu-id="7fee5-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="7fee5-121">Se a zona DNS for alojada por um serviço de parceiro (por exemplo, um de domínios, o fornecedor de alojamento DNS dedicado ou o fornecedor de nuvem alternativo), que o serviço deve fornecer o ficheiro de zona DNS toodownload Olá Olá capacidade.</span><span class="sxs-lookup"><span data-stu-id="7fee5-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="7fee5-122">Se a sua zona DNS estiver alojada no DNS do Windows, a pasta de predefinida de Olá para ficheiros de zona Olá é **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="7fee5-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="7fee5-123">ficheiro de zona do Olá caminho completo tooeach também mostra no Olá **geral** separador da consola do DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="7fee5-124">Se a sua zona DNS estiver alojada utilizando o ENLACE, localização Olá do ficheiro de zona Olá para cada zona é especificada no ficheiro de configuração de ENLACE Olá **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="7fee5-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="7fee5-125">Ficheiros de zona transferidos da GoDaddy tem um formato ligeiramente não padrão.</span><span class="sxs-lookup"><span data-stu-id="7fee5-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="7fee5-126">É necessário toocorrect isto antes de importar estes ficheiros de zona no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="7fee5-127">Nomes DNS no Olá RDATA de cada registo DNS estão especificados como nomes totalmente qualificados, mas não têm um terminar "." Isto significa que são interpretados por outros sistemas DNS como nomes relativos.</span><span class="sxs-lookup"><span data-stu-id="7fee5-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="7fee5-128">Terá de tooedit Olá zona ficheiro tooappend Olá terminar "." tootheir nomes antes de importá-los no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="7fee5-129">Por exemplo, Olá Registro CNAME "www 3600 em CNAME contoso.com" deve ser alterada demasiado "www 3600 CNAME em contoso.com."</span><span class="sxs-lookup"><span data-stu-id="7fee5-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="7fee5-130">(com um terminar ".").</span><span class="sxs-lookup"><span data-stu-id="7fee5-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="7fee5-131">Importar um ficheiro de zona DNS para o DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="7fee5-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="7fee5-132">Importar um ficheiro de zona cria uma nova zona no DNS do Azure se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="7fee5-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="7fee5-133">Se já existir uma zona de Olá, hello conjuntos de registos no ficheiro de zona Olá têm de ser intercalados com conjuntos de registos existente Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="7fee5-134">Comportamento de intercalação</span><span class="sxs-lookup"><span data-stu-id="7fee5-134">Merge behavior</span></span>

* <span data-ttu-id="7fee5-135">Por predefinição, os conjuntos de registos existentes e novos são intercalados.</span><span class="sxs-lookup"><span data-stu-id="7fee5-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="7fee5-136">Os registos idênticos dentro de um conjunto de registo intercalado são anular duplicados.</span><span class="sxs-lookup"><span data-stu-id="7fee5-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="7fee5-137">Em alternativa, especificando Olá `--force` opção, Olá substitui do processo de importação conjuntos de registos existente com novos conjuntos de registos.</span><span class="sxs-lookup"><span data-stu-id="7fee5-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="7fee5-138">Conjuntos de registos existentes que não têm um registo correspondente definido no ficheiro de zona importado de Olá não são removidos.</span><span class="sxs-lookup"><span data-stu-id="7fee5-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="7fee5-139">Quando os conjuntos de registos são intercalados, hello tempo toolive (TTL) pré-existentes de conjuntos de registos é utilizado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="7fee5-140">Quando `--force` é utilizado, Olá TTL do novo conjunto de registos Olá é utilizado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="7fee5-141">Início de parâmetros de autoridade (SOA) (exceto `host`) sempre são obtidas a partir do ficheiro de zona importado Olá, independentemente `--force` é utilizado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="7fee5-142">Da mesma forma, para Olá nome servidor conjunto de registos no vértice da zona de Olá, hello TTL é sempre retirado do ficheiro de zona importado Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="7fee5-143">Um registo CNAME importado não substituir um CNAME existente com Olá, a menos que o mesmo nome de registo Olá `--force` parâmetro for especificado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="7fee5-144">Quando for um conflito entre um registo CNAME e outro registo do mesmo nome mas diferentes de Olá escreva (independentemente de qual é existente ou nova), o registo existente Olá é mantido.</span><span class="sxs-lookup"><span data-stu-id="7fee5-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="7fee5-145">Isto é independente da utilização de Olá de `--force`.</span><span class="sxs-lookup"><span data-stu-id="7fee5-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="7fee5-146">Informações adicionais sobre como importar</span><span class="sxs-lookup"><span data-stu-id="7fee5-146">Additional information about importing</span></span>

<span data-ttu-id="7fee5-147">Olá notas seguintes fornecem detalhes técnicos adicionais sobre a zona de Olá importar processo.</span><span class="sxs-lookup"><span data-stu-id="7fee5-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="7fee5-148">Olá `$TTL` diretiva é opcional e é suportada.</span><span class="sxs-lookup"><span data-stu-id="7fee5-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="7fee5-149">Quando não existe nenhum `$TTL` diretiva é atribuída, os registos sem um valor de TTL explícito são importados predefinir tooa TTL de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="7fee5-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="7fee5-150">Quando dois regista no hello mesmo conjunto de registos especifique TTLs diferentes, é utilizado o valor mais baixo Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="7fee5-151">Olá `$ORIGIN` diretiva é opcional e é suportada.</span><span class="sxs-lookup"><span data-stu-id="7fee5-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="7fee5-152">Quando não existe nenhum `$ORIGIN` estiver definido, predefinição Olá utilizado o valor é o nome da zona Olá conforme especificado na linha de comandos Olá (juntamente com a terminar Olá ".").</span><span class="sxs-lookup"><span data-stu-id="7fee5-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="7fee5-153">Olá `$INCLUDE` e `$GENERATE` diretivas não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="7fee5-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="7fee5-154">Estes tipos de registos são suportados: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="7fee5-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="7fee5-155">Olá registo SOA é automaticamente criada pelo DNS do Azure quando é criada uma zona.</span><span class="sxs-lookup"><span data-stu-id="7fee5-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="7fee5-156">Quando importar um ficheiro de zona, todos os parâmetros SOA são obtidos a partir do ficheiro de zona Olá *exceto* Olá `host` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7fee5-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="7fee5-157">Este parâmetro utiliza o valor de Olá fornecido pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="7fee5-158">Isto acontece porque este parâmetro deve referir-se o servidor de nome principal de toohello fornecido pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="7fee5-159">também, o registo de servidor de nome de Olá definido no vértice da zona de Olá é criado automaticamente pelo DNS do Azure quando Olá zona é criada.</span><span class="sxs-lookup"><span data-stu-id="7fee5-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="7fee5-160">Apenas hello TTL deste conjunto de registos é importado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="7fee5-161">Estes registos contenham nomes dos servidores de nome Olá fornecidos pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="7fee5-162">dados do registo Olá não são substituídos pelos valores Olá contidos no ficheiro de zona importado Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="7fee5-163">Durante a pré-visualização pública, o DNS do Azure suporta apenas registos TXT de cadeia única.</span><span class="sxs-lookup"><span data-stu-id="7fee5-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="7fee5-164">Os registos TXT multistring são ser too255 concatenada e truncada carateres.</span><span class="sxs-lookup"><span data-stu-id="7fee5-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="7fee5-165">Formato CLI e valores</span><span class="sxs-lookup"><span data-stu-id="7fee5-165">CLI format and values</span></span>

<span data-ttu-id="7fee5-166">formato de Olá do Olá CLI do Azure comando tooimport uma zona DNS é:</span><span class="sxs-lookup"><span data-stu-id="7fee5-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="7fee5-167">Valores:</span><span class="sxs-lookup"><span data-stu-id="7fee5-167">Values:</span></span>

* <span data-ttu-id="7fee5-168">`<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de Olá no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="7fee5-169">`<zone name>`é o nome de Olá da zona de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="7fee5-170">`<zone file name>`é Olá/nome de caminho de Olá zona ficheiro toobe importado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="7fee5-171">Se não existir uma zona com este nome no grupo de recursos de Olá, é criado para si.</span><span class="sxs-lookup"><span data-stu-id="7fee5-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="7fee5-172">Se hello zona já existir, hello conjuntos de registos importados são intercalados com os conjuntos de registos existentes.</span><span class="sxs-lookup"><span data-stu-id="7fee5-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="7fee5-173">toooverwrite Olá existente conjuntos de registos, utilize Olá `--force` opção.</span><span class="sxs-lookup"><span data-stu-id="7fee5-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="7fee5-174">formato de Olá tooverify de um ficheiro de zona sem realmente importá-lo, utilize Olá `--parse-only` opção.</span><span class="sxs-lookup"><span data-stu-id="7fee5-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="7fee5-175">Passo 1.</span><span class="sxs-lookup"><span data-stu-id="7fee5-175">Step 1.</span></span> <span data-ttu-id="7fee5-176">Importar um ficheiro de zona</span><span class="sxs-lookup"><span data-stu-id="7fee5-176">Import a zone file</span></span>

<span data-ttu-id="7fee5-177">tooimport um ficheiro de zona para a zona de Olá **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="7fee5-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="7fee5-178">Inicie sessão no tooyour subscrição do Azure utilizando Olá CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="7fee5-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="7fee5-179">Selecione a subscrição de olá onde pretende toocreate a nova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7fee5-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="7fee5-180">O DNS do Azure é um serviço de só de Gestor de recursos do Azure, para que Olá CLI do Azure tem de ser desativados tooResource Manager modo.</span><span class="sxs-lookup"><span data-stu-id="7fee5-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="7fee5-181">Antes de utilizar o serviço de DNS do Azure Olá, tem de registar o fornecedor de recursos do subscrição toouse Olá Network.</span><span class="sxs-lookup"><span data-stu-id="7fee5-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="7fee5-182">(Esta é uma operação única para cada subscrição.)</span><span class="sxs-lookup"><span data-stu-id="7fee5-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="7fee5-183">Se ainda não tiver uma, terá também de toocreate um grupo de recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fee5-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="7fee5-184">zona de Olá tooimport **contoso.com** do ficheiro de Olá **contoso.com.txt** para uma nova zona DNS no grupo de recursos de Olá **myresourcegroup**, execute o comando de Olá `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="7fee5-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="7fee5-185">Este comando carrega o ficheiro de zona Olá e analisá-lo.</span><span class="sxs-lookup"><span data-stu-id="7fee5-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="7fee5-186">comando Olá executa uma série de comandos na zona de Olá de toocreate de serviço DNS do Azure Olá e conjuntos de todos os registos de Olá na zona de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="7fee5-187">comando Olá comunica o progresso na janela de consola Olá, juntamente com quaisquer erros ou avisos.</span><span class="sxs-lookup"><span data-stu-id="7fee5-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="7fee5-188">Porque os conjuntos de registos são criados em série, poderá demorar alguns minutos tooimport um ficheiro de zona grandes.</span><span class="sxs-lookup"><span data-stu-id="7fee5-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="7fee5-189">Passo 2.</span><span class="sxs-lookup"><span data-stu-id="7fee5-189">Step 2.</span></span> <span data-ttu-id="7fee5-190">Certifique-se a zona de Olá</span><span class="sxs-lookup"><span data-stu-id="7fee5-190">Verify hello zone</span></span>

<span data-ttu-id="7fee5-191">tooverify Olá zona DNS depois de importar o ficheiro de Olá, pode utilizar qualquer um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="7fee5-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="7fee5-192">Pode listar os registos de Olá utilizando Olá os seguintes comandos da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="7fee5-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="7fee5-193">Pode listar os registos de Olá utilizando o cmdlet do PowerShell Olá `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="7fee5-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="7fee5-194">Pode utilizar `nslookup` tooverify resolução de nomes para os registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="7fee5-195">Porque zona Olá não delegada ainda, terá de servidores de nomes de DNS do Azure corretos do toospecify Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="7fee5-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="7fee5-196">Olá exemplo seguinte mostra como tooretrieve Olá nomes de servidor atribuído toohello zona.</span><span class="sxs-lookup"><span data-stu-id="7fee5-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="7fee5-197">IT também mostra como tooquery Olá "www" registar utilizando `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="7fee5-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="7fee5-198">Passo 3.</span><span class="sxs-lookup"><span data-stu-id="7fee5-198">Step 3.</span></span> <span data-ttu-id="7fee5-199">Atualizar delegação de DNS</span><span class="sxs-lookup"><span data-stu-id="7fee5-199">Update DNS delegation</span></span>

<span data-ttu-id="7fee5-200">Depois de ter verificado que zona Olá foi importada corretamente, tem de tooupdate Olá DNS delegação toopoint toohello nomes DNS do Azure que servidores.</span><span class="sxs-lookup"><span data-stu-id="7fee5-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="7fee5-201">Para obter mais informações, consulte o artigo de Olá [atualizar delegação de DNS Olá](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="7fee5-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="7fee5-202">Exportar um ficheiro de zona DNS do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="7fee5-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="7fee5-203">formato de Olá do Olá CLI do Azure comando tooimport uma zona DNS é:</span><span class="sxs-lookup"><span data-stu-id="7fee5-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="7fee5-204">Valores:</span><span class="sxs-lookup"><span data-stu-id="7fee5-204">Values:</span></span>

* <span data-ttu-id="7fee5-205">`<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de Olá no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="7fee5-206">`<zone name>`é o nome de Olá da zona de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fee5-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="7fee5-207">`<zone file name>`é Olá/nome de caminho de Olá zona ficheiro toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="7fee5-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="7fee5-208">Como a importação de zona Olá, terá primeiro toosign no, escolha a sua subscrição e configurar o modo de Gestor de recursos de toouse Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="7fee5-209">tooexport um ficheiro de zona</span><span class="sxs-lookup"><span data-stu-id="7fee5-209">tooexport a zone file</span></span>

1. <span data-ttu-id="7fee5-210">Inicie sessão no tooyour subscrição do Azure utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="7fee5-211">Selecione a subscrição de olá onde pretende toocreate sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7fee5-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="7fee5-212">O DNS do Azure é um serviço de só de Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fee5-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="7fee5-213">Olá CLI do Azure tem de ser desativados tooResource Manager modo.</span><span class="sxs-lookup"><span data-stu-id="7fee5-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="7fee5-214">tooexport Olá zona DNS do Azure existente **contoso.com** no grupo de recursos **myresourcegroup** toohello ficheiro **contoso.com.txt** (na pasta atual Olá), execute `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="7fee5-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="7fee5-215">Este comando chamadas Olá tooenumerate de serviço DNS do Azure conjuntos de registos na zona de Olá e exporte o ficheiro de zona do Olá resultados tooa compatível com o ENLACE.</span><span class="sxs-lookup"><span data-stu-id="7fee5-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
