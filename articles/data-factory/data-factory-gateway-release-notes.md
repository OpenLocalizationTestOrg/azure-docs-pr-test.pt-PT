---
title: notas de aaaRelease do Data Management Gateway | Microsoft Docs
description: "Notas de versão do Data Management Gateway tory"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="778c6-103">Notas de lançamento do Gateway de Gestão de Dados</span><span class="sxs-lookup"><span data-stu-id="778c6-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="778c6-104">Um dos desafios de Olá para integração de dados modernas é toomove dados tooand de toocloud no local.</span><span class="sxs-lookup"><span data-stu-id="778c6-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="778c6-105">Fábrica de dados torna esta integração com o Data Management Gateway, que é um agente que pode instalar o movimento de dados no local tooenable híbrida.</span><span class="sxs-lookup"><span data-stu-id="778c6-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="778c6-106">Consulte Olá seguintes artigos para obter informações detalhadas sobre o Data Management Gateway e como toouse-lo:</span><span class="sxs-lookup"><span data-stu-id="778c6-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="778c6-107">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="778c6-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="778c6-108">Mover dados entre no local e na nuvem utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="778c6-109">VERSÃO ATUAL (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="778c6-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="778c6-110">Melhoramentos-</span><span class="sxs-lookup"><span data-stu-id="778c6-110">Enhancements-</span></span>
- <span data-ttu-id="778c6-111">Pode adicionar barramento de serviço de toowhitelist de entradas DNS, em vez de adicionar à lista branca todos os endereços IP do Azure da sua firewall (se necessário).</span><span class="sxs-lookup"><span data-stu-id="778c6-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="778c6-112">Pode encontrar a respetiva entrada DNS no portal do Azure (Data Factory -> 'Criar e implementar' -> 'Gateways' -> "serviceUrls" (no JSON)</span><span class="sxs-lookup"><span data-stu-id="778c6-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="778c6-113">Conector do HDFS suporta agora autoassinado certificado público, permitindo-lhe ignorar a validação de SSL.</span><span class="sxs-lookup"><span data-stu-id="778c6-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="778c6-114">Fixo: Problema com o gateway offline durante a atualização (devido tooclock desfasamento)</span><span class="sxs-lookup"><span data-stu-id="778c6-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="778c6-115">Versões anteriores</span><span class="sxs-lookup"><span data-stu-id="778c6-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="778c6-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="778c6-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="778c6-117">Melhoramentos-</span><span class="sxs-lookup"><span data-stu-id="778c6-117">Enhancements-</span></span>
-   <span data-ttu-id="778c6-118">Pode adicionar entradas DNS toowhitelist Service Bus, em vez de adicionar à lista branca todos os endereços IP do Azure da sua firewall (se necessário).</span><span class="sxs-lookup"><span data-stu-id="778c6-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="778c6-119">Obter mais detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="778c6-119">More details here.</span></span>
-   <span data-ttu-id="778c6-120">Agora pode copiar dados de/para um blob de bloco única cópia de segurança too4.75 TB, que é o tamanho de Olá máx. suportado de BLOBs de blocos.</span><span class="sxs-lookup"><span data-stu-id="778c6-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="778c6-121">(limite anterior era 195 GB).</span><span class="sxs-lookup"><span data-stu-id="778c6-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="778c6-122">Fixa: Fora de problema de memória ao unzipping vários ficheiros pequenos durante a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="778c6-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="778c6-123">Fixo: Índice fora do problema do intervalo ao copiar de Document DB tooan no local do SQL Server com a funcionalidade de idempotency.</span><span class="sxs-lookup"><span data-stu-id="778c6-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="778c6-124">Fixo: Script de limpeza do SQL Server não funciona com o servidor de SQL no local do Assistente para copiar.</span><span class="sxs-lookup"><span data-stu-id="778c6-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="778c6-125">Fixo: Nome de coluna com o espaço no final de Olá não funciona na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="778c6-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="778c6-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="778c6-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="778c6-127">Melhoramentos-</span><span class="sxs-lookup"><span data-stu-id="778c6-127">Enhancements-</span></span>
- <span data-ttu-id="778c6-128">Fixo: Problema com a falta de credenciais no reinício do computador de gateway.</span><span class="sxs-lookup"><span data-stu-id="778c6-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="778c6-129">Fixo: Problema com o registo durante gateway restaurar o utilizando um ficheiro de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="778c6-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="778c6-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="778c6-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="778c6-131">Melhoramentos-</span><span class="sxs-lookup"><span data-stu-id="778c6-131">Enhancements-</span></span>
- <span data-ttu-id="778c6-132">Fixa: Leitura incorreta de um valor nulo Decimal do Oracle como origem.</span><span class="sxs-lookup"><span data-stu-id="778c6-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="778c6-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="778c6-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="778c6-134">Novidades</span><span class="sxs-lookup"><span data-stu-id="778c6-134">What’s new</span></span>
- <span data-ttu-id="778c6-135">Os clientes podem fornecer comentários no gateway registar experiência.</span><span class="sxs-lookup"><span data-stu-id="778c6-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="778c6-136">Suportar um novo formato de compressão: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="778c6-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="778c6-137">Melhoramentos-</span><span class="sxs-lookup"><span data-stu-id="778c6-137">Enhancements-</span></span>
- <span data-ttu-id="778c6-138">Melhoramento de desempenho para Sink do Oracle, origem HDFS.</span><span class="sxs-lookup"><span data-stu-id="778c6-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="778c6-139">Correção de erros para automático de gateway atualizar, capacidade de processamento paralelo de gateway.</span><span class="sxs-lookup"><span data-stu-id="778c6-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="778c6-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="778c6-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="778c6-141">Melhoramentos</span><span class="sxs-lookup"><span data-stu-id="778c6-141">Enhancements</span></span>
- <span data-ttu-id="778c6-142">Melhor e mais robusta Gateway registo experiência-agora pode controlar o estado do progresso durante o processo de registo do Olá Gateway, que faz com que o registo de Olá experiência mais dinâmico.</span><span class="sxs-lookup"><span data-stu-id="778c6-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="778c6-143">Melhoria no Gateway restaurar processo - que pode continuar a recuperar gateway, mesmo se não tiver ficheiros de cópia de segurança de gateway de Olá com esta atualização.</span><span class="sxs-lookup"><span data-stu-id="778c6-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="778c6-144">Isto seria requerem credenciais de serviço ligado de tooreset no Portal.</span><span class="sxs-lookup"><span data-stu-id="778c6-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="778c6-145">Correção de erro.</span><span class="sxs-lookup"><span data-stu-id="778c6-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="778c6-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="778c6-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="778c6-147">Novidades</span><span class="sxs-lookup"><span data-stu-id="778c6-147">What’s new</span></span>

- <span data-ttu-id="778c6-148">Agora pode armazenar credenciais da origem de dados localmente.</span><span class="sxs-lookup"><span data-stu-id="778c6-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="778c6-149">Olá credenciais estão encriptadas.</span><span class="sxs-lookup"><span data-stu-id="778c6-149">hello credentials are encrypted.</span></span> <span data-ttu-id="778c6-150">credenciais de origens de dados de Olá podem ser recuperadas e restaurados com autoridade utilizando o ficheiro de cópia de segurança de Olá que pode ser exportado da Olá existente Gateway, todos os no local.</span><span class="sxs-lookup"><span data-stu-id="778c6-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="778c6-151">Melhoramentos-</span><span class="sxs-lookup"><span data-stu-id="778c6-151">Enhancements-</span></span>

- <span data-ttu-id="778c6-152">Experiência de registo de Gateway melhor e mais robusta.</span><span class="sxs-lookup"><span data-stu-id="778c6-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="778c6-153">Suporta a deteção automática da configuração de QuoteChar para formato de texto no Assistente para copiar e melhorar Olá global Formatar precisão de deteção.</span><span class="sxs-lookup"><span data-stu-id="778c6-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="778c6-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="778c6-154">2.3.6100.2</span></span>

- <span data-ttu-id="778c6-155">Suporte firstRowAsHeader e a deteção automática SkipLineCount no Assistente de cópia de ficheiros de texto no sistema de ficheiros no local e HDFS.</span><span class="sxs-lookup"><span data-stu-id="778c6-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="778c6-156">Melhorar a estabilidade Olá de ligação de rede entre o gateway e o Service Bus</span><span class="sxs-lookup"><span data-stu-id="778c6-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="778c6-157">Algumas correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="778c6-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="778c6-158">2.2.6072.1</span></span>

*  <span data-ttu-id="778c6-159">Suporta a definição de proxy HTTP para utilizar o gateway Olá Olá Gestor de configuração do Gateway.</span><span class="sxs-lookup"><span data-stu-id="778c6-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="778c6-160">Se configurado, o Blob do Azure, tabelas do Azure, Azure Data Lake e Document DB são acedidos através do proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="778c6-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="778c6-161">Processamento de TextFormat ao copiar dados a partir de cabeçalho de suporta / tooAzure Blob, o Azure Data Lake Store, sistema de ficheiros no local e no local HDFS.</span><span class="sxs-lookup"><span data-stu-id="778c6-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="778c6-162">Suporta a copiar dados de BLOBs de acréscimo e BLOBs de páginas, juntamente com Olá já suportadas BLOBs de blocos.</span><span class="sxs-lookup"><span data-stu-id="778c6-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="778c6-163">Apresenta um novo estado do gateway **Online (limitado)**, que indica que essa funcionalidade principal de Olá do gateway de Olá funciona, exceto o suporte de operação interativa Olá para o Assistente para copiar.</span><span class="sxs-lookup"><span data-stu-id="778c6-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="778c6-164">Melhora robustez Olá do registo de gateway utilizando a chave de registo.</span><span class="sxs-lookup"><span data-stu-id="778c6-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="778c6-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="778c6-165">2.1.6040.</span></span>

*  <span data-ttu-id="778c6-166">Controlador DB2 está incluído no pacote de instalação do gateway Olá agora.</span><span class="sxs-lookup"><span data-stu-id="778c6-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="778c6-167">Não é necessário tooinstall-lo em separado.</span><span class="sxs-lookup"><span data-stu-id="778c6-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="778c6-168">Controlador DB2 suporta agora o z/SO e DB2 para posso (como / 400) juntamente com plataformas Olá já suportadas (Linux, Unix e Windows).</span><span class="sxs-lookup"><span data-stu-id="778c6-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="778c6-169">Suporta a utilização de base de dados do Azure Cosmos como uma origem ou de destino para os arquivos de dados no local</span><span class="sxs-lookup"><span data-stu-id="778c6-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="778c6-170">Suporta a copiar o armazenamento de BLOBs de/toocold/frequente de dados, juntamente com Olá já suportadas conta do storage para fins gerais.</span><span class="sxs-lookup"><span data-stu-id="778c6-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="778c6-171">Permite-lhe tooconnect tooon local do SQL Server através do gateway com privilégios de início de sessão remoto.</span><span class="sxs-lookup"><span data-stu-id="778c6-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="778c6-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="778c6-172">2.0.6013.1</span></span>

*  <span data-ttu-id="778c6-173">Pode selecionar Olá cultura do idioma toobe utilizado por um gateway durante a instalação manual.</span><span class="sxs-lookup"><span data-stu-id="778c6-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="778c6-174">Quando o gateway não funciona conforme esperado, pode escolher os registos do gateway toosend dos últimos sete dias tooMicrosoft toofacilitate resolução de problemas do problema Olá.</span><span class="sxs-lookup"><span data-stu-id="778c6-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="778c6-175">Se o gateway não está ligado toohello o serviço em nuvem, pode escolher toosave e arquivar registos do gateway.</span><span class="sxs-lookup"><span data-stu-id="778c6-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="778c6-176">Melhoramentos de interface de utilizador para o Gestor de configuração do gateway:</span><span class="sxs-lookup"><span data-stu-id="778c6-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="778c6-177">Tornar o estado do gateway mais visíveis no separador de início de Olá.</span><span class="sxs-lookup"><span data-stu-id="778c6-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="778c6-178">Controlos reorganizados e simplificados.</span><span class="sxs-lookup"><span data-stu-id="778c6-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="778c6-179">Pode copiar dados de um armazenamento utilizando Olá [ferramenta de pré-visualização de cópia sem código](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="778c6-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="778c6-180">Consulte [testado cópia](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre esta funcionalidade em geral.</span><span class="sxs-lookup"><span data-stu-id="778c6-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="778c6-181">Pode utilizar dados de tooingress do Data Management Gateway diretamente a partir de uma base de dados do SQL Server no local para o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="778c6-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="778c6-182">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-182">Performance improvements</span></span>

    * <span data-ttu-id="778c6-183">Melhore o desempenho sobre a visualização de esquema/pré-visualização contra do SQL Server na ferramenta de pré-visualização de cópia sem código.</span><span class="sxs-lookup"><span data-stu-id="778c6-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="778c6-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="778c6-184">1.12.5953.1</span></span>

*  <span data-ttu-id="778c6-185">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="778c6-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="778c6-186">1.11.5918.1</span></span>

*  <span data-ttu-id="778c6-187">Tamanho máximo do registo de eventos do gateway Olá aumentou de 1 MB too40 MB.</span><span class="sxs-lookup"><span data-stu-id="778c6-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="778c6-188">Uma caixa de diálogo de aviso é apresentada no caso seja necessário um reinício durante a atualização automática do gateway.</span><span class="sxs-lookup"><span data-stu-id="778c6-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="778c6-189">Pode escolher toorestart direito, em seguida, ou posterior.</span><span class="sxs-lookup"><span data-stu-id="778c6-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="778c6-190">No caso de falha de atualização automática, o instalador do gateway repete a atualização automática três vezes no máximo.</span><span class="sxs-lookup"><span data-stu-id="778c6-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="778c6-191">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-191">Performance improvements</span></span>

    * <span data-ttu-id="778c6-192">Melhore o desempenho para carregar tabelas grandes a partir do servidor no local, num cenário de cópia sem código.</span><span class="sxs-lookup"><span data-stu-id="778c6-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="778c6-193">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="778c6-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="778c6-194">1.10.5892.1</span></span>

*  <span data-ttu-id="778c6-195">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-195">Performance improvements</span></span>

*  <span data-ttu-id="778c6-196">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="778c6-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="778c6-197">1.9.5865.2</span></span>

*  <span data-ttu-id="778c6-198">Capacidade de atualização de automática zero touch</span><span class="sxs-lookup"><span data-stu-id="778c6-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="778c6-199">Ícone de tabuleiro novo com indicadores de estado do gateway</span><span class="sxs-lookup"><span data-stu-id="778c6-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="778c6-200">Capacidade demasiado "atualizar agora" do cliente de Olá</span><span class="sxs-lookup"><span data-stu-id="778c6-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="778c6-201">Hora de agendamento de atualização de tooset de capacidade</span><span class="sxs-lookup"><span data-stu-id="778c6-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="778c6-202">Script do PowerShell para ativando ou desativando a atualização automática /</span><span class="sxs-lookup"><span data-stu-id="778c6-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="778c6-203">Suporte para o formato JSON</span><span class="sxs-lookup"><span data-stu-id="778c6-203">Support for JSON format</span></span>  
*  <span data-ttu-id="778c6-204">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-204">Performance improvements</span></span>
*  <span data-ttu-id="778c6-205">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="778c6-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="778c6-206">1.8.5822.1</span></span>

*  <span data-ttu-id="778c6-207">Melhorar a experiência de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="778c6-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="778c6-208">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-208">Performance improvements</span></span>
*  <span data-ttu-id="778c6-209">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="778c6-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="778c6-210">1.7.5795.1</span></span>

*  <span data-ttu-id="778c6-211">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-211">Performance improvements</span></span>
*  <span data-ttu-id="778c6-212">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="778c6-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="778c6-213">1.7.5764.1</span></span>

*  <span data-ttu-id="778c6-214">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-214">Performance improvements</span></span>
*  <span data-ttu-id="778c6-215">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="778c6-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="778c6-216">1.6.5735.1</span></span>

*  <span data-ttu-id="778c6-217">Suporte no local HDFS origem/Sink</span><span class="sxs-lookup"><span data-stu-id="778c6-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="778c6-218">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-218">Performance improvements</span></span>
*  <span data-ttu-id="778c6-219">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="778c6-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="778c6-220">1.6.5696.1</span></span>

*  <span data-ttu-id="778c6-221">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-221">Performance improvements</span></span>
*  <span data-ttu-id="778c6-222">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="778c6-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="778c6-223">1.6.5676.1</span></span>

*  <span data-ttu-id="778c6-224">Ferramentas de diagnóstico de suporte no Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="778c6-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="778c6-225">Colunas de tabela de suporte para origens de dados em tabela do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-226">Suporte de armazém de dados SQL do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-227">Suporte Reclusive BlobSource e FileSource do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-228">Suporta CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy BlobSink e FileSink com cópia binária do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-229">Suporta a atividade de cópia de relatório de progresso do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-230">Validação da conectividade de origem de dados de suporte do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-231">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="778c6-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="778c6-232">1.6.5672.1</span></span>

*  <span data-ttu-id="778c6-233">Nome da tabela de suporte para a origem de dados ODBC do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-234">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-234">Performance improvements</span></span>
*  <span data-ttu-id="778c6-235">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="778c6-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="778c6-236">1.6.5658.1</span></span>

*  <span data-ttu-id="778c6-237">Sink do ficheiro de suporte do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-238">Suporte preservar hierarquia na cópia de binária para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-239">Suporta Idempotency de atividade de cópia do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-240">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="778c6-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="778c6-241">1.6.5640.1</span></span>

*  <span data-ttu-id="778c6-242">Suporte 3 mais origens de dados para o Azure Data Factory (ODBC OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="778c6-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="778c6-243">Suporte caráter da plica no parser de csv para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-244">Suporte de compressão (BZip2)</span><span class="sxs-lookup"><span data-stu-id="778c6-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="778c6-245">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="778c6-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="778c6-246">1.5.5612.1</span></span>

*  <span data-ttu-id="778c6-247">Suporta cinco bases de dados relacionais (MySQL, PostgreSQL, DB2, Teradata e Sybase) do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="778c6-248">Suporte de compressão (Gzip e Deflate)</span><span class="sxs-lookup"><span data-stu-id="778c6-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="778c6-249">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-249">Performance improvements</span></span>
*  <span data-ttu-id="778c6-250">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="778c6-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="778c6-251">1.4.5549.1</span></span>

*  <span data-ttu-id="778c6-252">Adicionar suporte de origem de dados Oracle para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="778c6-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="778c6-253">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="778c6-253">Performance improvements</span></span>
*  <span data-ttu-id="778c6-254">Correções de erros</span><span class="sxs-lookup"><span data-stu-id="778c6-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="778c6-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="778c6-255">1.4.5492.1</span></span>

*  <span data-ttu-id="778c6-256">Binário unificado que suporte serviços do Microsoft Azure Data Factory e Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="778c6-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="778c6-257">Otimizar o processo de IU de configuração e registo Olá</span><span class="sxs-lookup"><span data-stu-id="778c6-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="778c6-258">O Azure Data Factory – suportam a entrada do Azure e de saída para a origem de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="778c6-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="778c6-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="778c6-259">1.2.5303.1</span></span>

*  <span data-ttu-id="778c6-260">Corrija toosupport de problema de tempo limite mais ligações de origens de dados morosa.</span><span class="sxs-lookup"><span data-stu-id="778c6-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="778c6-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="778c6-261">1.1.5526.8</span></span>

*  <span data-ttu-id="778c6-262">Requer o .NET Framework 4.5.1 como pré-requisito durante a configuração.</span><span class="sxs-lookup"><span data-stu-id="778c6-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="778c6-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="778c6-263">1.0.5144.2</span></span>

*  <span data-ttu-id="778c6-264">Não existem alterações que afetam os cenários do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="778c6-264">No changes that affect Azure Data Factory scenarios.</span></span>
