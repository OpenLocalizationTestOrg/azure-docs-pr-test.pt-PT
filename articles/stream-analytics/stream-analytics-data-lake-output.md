---
title: "Análise de Data Lake Store saída de aaaStream | Microsoft Docs"
description: "Configuração de autenticação e autorização de um Azure Data Lake Store numa tarefa do Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="6b25b-103">Saída de Stream Analytics Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6b25b-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="6b25b-104">Tarefas do Stream Analytics suportam vários métodos de saída, a ser um um [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="6b25b-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="6b25b-105">O Azure Data Lake Store é um repositório de hiper escala a nível da empresa para cargas de trabalho de análise de macrodados.</span><span class="sxs-lookup"><span data-stu-id="6b25b-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="6b25b-106">Arquivo data Lake permite-lhe toostore dados de qualquer tamanho, tipo e velocidade de ingestão para análises exploratórias e operacionais.</span><span class="sxs-lookup"><span data-stu-id="6b25b-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="6b25b-107">Autorizar a conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6b25b-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="6b25b-108">Quando a Data Lake Store é selecionada como uma saída no Olá portal do Azure, terá de aceder a utilização de tooauthorize do Data Lake Store existente ou toorequest toohello Data Lake Store através do Portal clássico do Olá.</span><span class="sxs-lookup"><span data-stu-id="6b25b-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="6b25b-109">Se já tiver acesso tooData Lake Store, clique em "Autorizar agora" e por um breve período de tempo a página irá aparecer que indica "Redirecting tooauthorization".</span><span class="sxs-lookup"><span data-stu-id="6b25b-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="6b25b-110">página Olá automaticamente será fechada e será apresentada com a página Olá que permitiria tooconfigure Olá Data Lake Store saída.</span><span class="sxs-lookup"><span data-stu-id="6b25b-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="6b25b-111">Se não tiver assinado cópias de segurança para o Data Lake Store, pode seguir Olá "Inscrever-me agora" ligação tooinitiate Olá pedido ou, siga Olá [obter instruções de introdução](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b25b-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="6b25b-112">Configurar propriedades de saída do Data Lake Store Olá</span><span class="sxs-lookup"><span data-stu-id="6b25b-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="6b25b-113">Assim que tiver a conta de Data Lake Store Olá autenticada, pode configurar propriedades de Olá para a saída do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6b25b-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="6b25b-114">tabela de Olá abaixo é Olá obter lista de nomes de propriedade e os respetivos tooconfigure de descrição de saída do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6b25b-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="6b25b-115"><B>NOME DA PROPRIEDADE</B></span><span class="sxs-lookup"><span data-stu-id="6b25b-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="6b25b-116"><B>DESCRIÇÃO</B></span><span class="sxs-lookup"><span data-stu-id="6b25b-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-117">Alias de saída</span><span class="sxs-lookup"><span data-stu-id="6b25b-117">Output Alias</span></span></td>
<td><span data-ttu-id="6b25b-118">Este é um nome amigável utilizado em consultas toodirect Olá consulta saída toothis Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6b25b-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-119">Conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6b25b-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="6b25b-120">nome de Olá Olá da conta de armazenamento onde está a enviar o resultado.</span><span class="sxs-lookup"><span data-stu-id="6b25b-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="6b25b-121">Será apresentada uma lista de contas do Data Lake Store Olá a sessão de utilizador tem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="6b25b-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-122">Caminho do prefixo padrão [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="6b25b-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="6b25b-123">Olá ficheiro caminho utilizado toowrite os ficheiros dentro do Olá especificado conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6b25b-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="6b25b-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="6b25b-124">{date}, {time}</span></span><BR><span data-ttu-id="6b25b-125">Exemplo 1: pasta1/logs / {date} / {time}</span><span class="sxs-lookup"><span data-stu-id="6b25b-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="6b25b-126">Exemplo 2: pasta1/logs / {date}</span><span class="sxs-lookup"><span data-stu-id="6b25b-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-127">Formato de data [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="6b25b-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="6b25b-128">Se o token de data de Olá é utilizado no caminho de prefixo Olá, pode selecionar o formato de data Olá na qual os ficheiros estão organizados.</span><span class="sxs-lookup"><span data-stu-id="6b25b-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="6b25b-129">Exemplo: DD/MM/DD</span><span class="sxs-lookup"><span data-stu-id="6b25b-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-130">Formato de hora [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="6b25b-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="6b25b-131">Se o token de tempo de Olá é utilizado no caminho de prefixo Olá, especifique o formato de hora Olá na qual os ficheiros estão organizados.</span><span class="sxs-lookup"><span data-stu-id="6b25b-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="6b25b-132">Valor de Olá só suportada está atualmente HH.</span><span class="sxs-lookup"><span data-stu-id="6b25b-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-133">Formato de serialização de eventos</span><span class="sxs-lookup"><span data-stu-id="6b25b-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="6b25b-134">Formato de serialização para dados de saída.</span><span class="sxs-lookup"><span data-stu-id="6b25b-134">Serialization format for output data.</span></span> <span data-ttu-id="6b25b-135">JSON, CSV e Avro são suportados.</span><span class="sxs-lookup"><span data-stu-id="6b25b-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="6b25b-136">Encoding</span></span></td>
<td><span data-ttu-id="6b25b-137">Se o formato CSV ou JSON, uma codificação tem de ser especificada.</span><span class="sxs-lookup"><span data-stu-id="6b25b-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="6b25b-138">UTF-8 é Olá apenas formato de codificação suportado neste momento.</span><span class="sxs-lookup"><span data-stu-id="6b25b-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-139">Delimitador</span><span class="sxs-lookup"><span data-stu-id="6b25b-139">Delimiter</span></span></td>
<td><span data-ttu-id="6b25b-140">Só é aplicável a serialização de CSV.</span><span class="sxs-lookup"><span data-stu-id="6b25b-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="6b25b-141">Stream Analytics suporta um número de delimitadores comuns para serializar os dados CSV.</span><span class="sxs-lookup"><span data-stu-id="6b25b-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="6b25b-142">Os valores suportados são vírgula, ponto e vírgula, espaço, separador e barra vertical.</span><span class="sxs-lookup"><span data-stu-id="6b25b-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6b25b-143">formato</span><span class="sxs-lookup"><span data-stu-id="6b25b-143">Format</span></span></td>
<td><span data-ttu-id="6b25b-144">Só é aplicável a serialização do JSON.</span><span class="sxs-lookup"><span data-stu-id="6b25b-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="6b25b-145">Separadas por linhas Especifica que Olá saída será formatada, fazendo com que cada objeto JSON separado por uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="6b25b-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="6b25b-146">A matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="6b25b-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="6b25b-147">Renovar autorização do arquivo Data Lake</span><span class="sxs-lookup"><span data-stu-id="6b25b-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="6b25b-148">Atualmente, não há uma limitação em que o token de autenticação de Olá tem toobe atualizado manualmente todos os 90 dias para todas as tarefas com a saída do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6b25b-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="6b25b-149">Também terá de toore-autenticar a sua conta do Data Lake Store, se tiver alterado a palavra-passe, uma vez que a tarefa foi criada ou pela última vez autenticada.</span><span class="sxs-lookup"><span data-stu-id="6b25b-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="6b25b-150">Um sintoma de que este problema é um erro nos registos de operação de Olá com a indicação de necessidade de nova autorização e nenhum resultado da tarefa.</span><span class="sxs-lookup"><span data-stu-id="6b25b-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="6b25b-151">tooresolve este problema, parar a tarefa em execução e aceda a saída tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6b25b-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="6b25b-152">Clique em ligação de "Autorização de renovação" Olá e por um breve período de tempo a página irá aparecer que indica "Redirecting tooauthorization …".</span><span class="sxs-lookup"><span data-stu-id="6b25b-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="6b25b-153">página Olá irá fechar automaticamente e se tiver êxito, irá indicar "Autorização tem foi renovada com êxito".</span><span class="sxs-lookup"><span data-stu-id="6b25b-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="6b25b-154">Que, em seguida, precisa tooclick "Guardar" em Olá parte inferior da página Olá e pode avançar ao reiniciar a tarefa de Olá perda de dados de tooavoid de hora da última paragem.</span><span class="sxs-lookup"><span data-stu-id="6b25b-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

