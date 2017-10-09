---
title: aaaCreate artefactos personalizados para a VM do DevTest Labs | Microsoft Docs
description: Saiba como tooauthor seus artefactos para utilizam com o DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="15174-103">Criar artefactos personalizados para a VM do DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="15174-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="15174-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="15174-104">Overview</span></span>
<span data-ttu-id="15174-105">**Artefactos** são utilizado toodeploy e configurar a sua aplicação depois de uma VM está aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="15174-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="15174-106">Um artefacto é composta por um ficheiro de definição de artefacto e outros ficheiros de script são armazenados numa pasta num repositório de git.</span><span class="sxs-lookup"><span data-stu-id="15174-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="15174-107">Ficheiros de definição de artefacto consistem em JSON e expressões que pode utilizar toospecify que pretende tooinstall numa VM.</span><span class="sxs-lookup"><span data-stu-id="15174-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="15174-108">Por exemplo, pode definir o nome de Olá dos parâmetros que são disponibilizados quando Olá comando é executado, toorun de comando e um artefacto.</span><span class="sxs-lookup"><span data-stu-id="15174-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="15174-109">Pode consultar os ficheiros de script de tooother dentro do ficheiro de definição de artefacto Olá por nome.</span><span class="sxs-lookup"><span data-stu-id="15174-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="15174-110">Formato de ficheiro de definição de artefactos</span><span class="sxs-lookup"><span data-stu-id="15174-110">Artifact definition file format</span></span>
<span data-ttu-id="15174-111">Olá exemplo seguinte mostra as secções de Olá que compõem a estrutura básica do Olá de um ficheiro de definição:</span><span class="sxs-lookup"><span data-stu-id="15174-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="15174-112">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="15174-112">Element name</span></span> | <span data-ttu-id="15174-113">Necessário?</span><span class="sxs-lookup"><span data-stu-id="15174-113">Required?</span></span> | <span data-ttu-id="15174-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="15174-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15174-115">$schema</span><span class="sxs-lookup"><span data-stu-id="15174-115">$schema</span></span> |<span data-ttu-id="15174-116">Não</span><span class="sxs-lookup"><span data-stu-id="15174-116">No</span></span> |<span data-ttu-id="15174-117">Localização do ficheiro de esquema JSON Olá que ajuda a validade Olá Olá do ficheiro de definição de teste.</span><span class="sxs-lookup"><span data-stu-id="15174-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="15174-118">Título</span><span class="sxs-lookup"><span data-stu-id="15174-118">title</span></span> |<span data-ttu-id="15174-119">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-119">Yes</span></span> |<span data-ttu-id="15174-120">Nome do artefacto de Olá apresentado no laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="15174-121">descrição</span><span class="sxs-lookup"><span data-stu-id="15174-121">description</span></span> |<span data-ttu-id="15174-122">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-122">Yes</span></span> |<span data-ttu-id="15174-123">Descrição do artefacto de Olá apresentado no laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="15174-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="15174-124">iconUri</span></span> |<span data-ttu-id="15174-125">Não</span><span class="sxs-lookup"><span data-stu-id="15174-125">No</span></span> |<span data-ttu-id="15174-126">URI de ícone de Olá apresentado no laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="15174-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="15174-127">targetOsType</span></span> |<span data-ttu-id="15174-128">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-128">Yes</span></span> |<span data-ttu-id="15174-129">Sistema operativo de Olá VM onde os artefactos está instalado.</span><span class="sxs-lookup"><span data-stu-id="15174-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="15174-130">As opções suportadas são: Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="15174-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="15174-131">parâmetros</span><span class="sxs-lookup"><span data-stu-id="15174-131">parameters</span></span> |<span data-ttu-id="15174-132">Não</span><span class="sxs-lookup"><span data-stu-id="15174-132">No</span></span> |<span data-ttu-id="15174-133">Valores que são fornecidos quando o comando de instalação do artefacto é executado numa máquina.</span><span class="sxs-lookup"><span data-stu-id="15174-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="15174-134">Isto ajuda a personalizar o artefacto.</span><span class="sxs-lookup"><span data-stu-id="15174-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="15174-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="15174-135">runCommand</span></span> |<span data-ttu-id="15174-136">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-136">Yes</span></span> |<span data-ttu-id="15174-137">Comando que é executado numa VM de instalação de artefactos.</span><span class="sxs-lookup"><span data-stu-id="15174-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="15174-138">Parâmetros de artefactos</span><span class="sxs-lookup"><span data-stu-id="15174-138">Artifact parameters</span></span>
<span data-ttu-id="15174-139">Na secção de parâmetros de Olá Olá do ficheiro de definição, especifique os valores de um utilizador pode introduzir ao instalar um artefacto.</span><span class="sxs-lookup"><span data-stu-id="15174-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="15174-140">Pode consultar os valores de toothese no comando de instalação do artefacto Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="15174-141">Definir os parâmetros com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="15174-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="15174-142">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="15174-142">Element name</span></span> | <span data-ttu-id="15174-143">Necessário?</span><span class="sxs-lookup"><span data-stu-id="15174-143">Required?</span></span> | <span data-ttu-id="15174-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="15174-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15174-145">tipo</span><span class="sxs-lookup"><span data-stu-id="15174-145">type</span></span> |<span data-ttu-id="15174-146">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-146">Yes</span></span> |<span data-ttu-id="15174-147">Tipo de valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="15174-147">Type of parameter value.</span></span> <span data-ttu-id="15174-148">Consulte Olá lista para Olá permitido tipos os seguintes:</span><span class="sxs-lookup"><span data-stu-id="15174-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="15174-149">displayName</span><span class="sxs-lookup"><span data-stu-id="15174-149">displayName</span></span> |<span data-ttu-id="15174-150">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-150">Yes</span></span> |<span data-ttu-id="15174-151">Nome do parâmetro de Olá que é o utilizador tooa apresentadas no laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="15174-152">descrição</span><span class="sxs-lookup"><span data-stu-id="15174-152">description</span></span> |<span data-ttu-id="15174-153">Sim</span><span class="sxs-lookup"><span data-stu-id="15174-153">Yes</span></span> |<span data-ttu-id="15174-154">Descrição do parâmetro de Olá que é apresentado no laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="15174-155">Olá permitidos tipos são:</span><span class="sxs-lookup"><span data-stu-id="15174-155">hello allowed types are:</span></span>

* <span data-ttu-id="15174-156">cadeia – qualquer cadeia JSON válida</span><span class="sxs-lookup"><span data-stu-id="15174-156">string – any valid JSON string</span></span>
* <span data-ttu-id="15174-157">Int – qualquer número inteiro JSON válido</span><span class="sxs-lookup"><span data-stu-id="15174-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="15174-158">bool – qualquer booleano de JSON válido</span><span class="sxs-lookup"><span data-stu-id="15174-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="15174-159">matriz – nenhuma matriz JSON válido</span><span class="sxs-lookup"><span data-stu-id="15174-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="15174-160">Funções e expressões de artefactos</span><span class="sxs-lookup"><span data-stu-id="15174-160">Artifact expressions and functions</span></span>
<span data-ttu-id="15174-161">Pode utilizar expressão e o comando de instalação do artefacto de Olá tooconstruct de funções.</span><span class="sxs-lookup"><span data-stu-id="15174-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="15174-162">As expressões são colocadas entre parênteses Retos ([e]) e são avaliadas quando artefactos Olá está instalado.</span><span class="sxs-lookup"><span data-stu-id="15174-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="15174-163">As expressões podem aparecer em qualquer local, um valor de cadeia JSON e sempre devolver um valor JSON diferente.</span><span class="sxs-lookup"><span data-stu-id="15174-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="15174-164">Se precisar de toouse uma cadeia literal, que começa com um parêntese [, tem de utilizar dois parênteses Retos [[.</span><span class="sxs-lookup"><span data-stu-id="15174-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="15174-165">Normalmente, utilizar expressões com funções tooconstruct um valor.</span><span class="sxs-lookup"><span data-stu-id="15174-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="15174-166">Tal como em JavaScript, chamadas de função estejam formatadas como functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="15174-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="15174-167">Olá lista seguinte mostra as funções comuns:</span><span class="sxs-lookup"><span data-stu-id="15174-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="15174-168">Parameters(parameterName) - devolve um valor de parâmetro que é fornecido quando Olá artefactos comando é executado.</span><span class="sxs-lookup"><span data-stu-id="15174-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="15174-169">concat (arg1 arg2, arg3,...) - combina vários valores de cadeia.</span><span class="sxs-lookup"><span data-stu-id="15174-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="15174-170">Esta função pode efetuar qualquer número de argumentos.</span><span class="sxs-lookup"><span data-stu-id="15174-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="15174-171">Olá seguinte exemplo mostra como toouse expressão e funções tooconstruct um valor:</span><span class="sxs-lookup"><span data-stu-id="15174-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="15174-172">Criar um artefacto personalizado</span><span class="sxs-lookup"><span data-stu-id="15174-172">Create a custom artifact</span></span>
<span data-ttu-id="15174-173">Crie os seus artefactos personalizados, seguindo estes passos:</span><span class="sxs-lookup"><span data-stu-id="15174-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="15174-174">Instalar um editor de JSON - é necessário um toowork do editor de JSON com ficheiros de definição de artefactos.</span><span class="sxs-lookup"><span data-stu-id="15174-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="15174-175">Recomendamos que utilize [Visual Studio Code](https://code.visualstudio.com/), que está disponível para Windows, Linux e OS X.</span><span class="sxs-lookup"><span data-stu-id="15174-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="15174-176">Obter um exemplo artifactfile.json - modificação artefactos Olá criado pela equipa do Azure DevTest Labs no nosso [repositório do GitHub](https://github.com/Azure/azure-devtestlab), em que foi criado uma biblioteca avançada de artefactos que o ajudam a criar os seus artefactos.</span><span class="sxs-lookup"><span data-stu-id="15174-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="15174-177">Transferir um ficheiro de definição de artefacto e efetuar alterações tooit toocreate seus artefactos.</span><span class="sxs-lookup"><span data-stu-id="15174-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="15174-178">Se utilizar o IntelliSense - tire partido IntelliSense toosee elementos válidos que podem ser utilizado tooconstruct um ficheiro de definição de artefactos.</span><span class="sxs-lookup"><span data-stu-id="15174-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="15174-179">Também pode ver Olá diferentes opções para os valores de um elemento.</span><span class="sxs-lookup"><span data-stu-id="15174-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="15174-180">Por exemplo, o IntelliSense mostrar de Olá duas opções do Windows ou Linux ao editar Olá **targetOsType** elemento.</span><span class="sxs-lookup"><span data-stu-id="15174-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="15174-181">Artefactos de Olá de arquivo num [repositório de git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="15174-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="15174-182">Crie um diretório separado para cada artefactos em que o nome de diretório Olá é Olá mesmo como nome de artefacto Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="15174-183">Armazenar o ficheiro de definição de artefacto Olá (artifactfile.json) no diretório de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="15174-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="15174-184">Comando de instalação de scripts de Olá de arquivo que são referenciados do artefacto de Olá.</span><span class="sxs-lookup"><span data-stu-id="15174-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="15174-185">Eis um exemplo de como pode ver uma pasta de artefacto:</span><span class="sxs-lookup"><span data-stu-id="15174-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Exemplo de repositório de git de artefactos](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="15174-187">Adicionar o laboratório de toohello de repositório de artefactos Olá - consulte o artigo toohello, [adicione um repositório de Git para artefactos e modelos](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="15174-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="15174-188">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="15174-188">Related articles</span></span>
* [<span data-ttu-id="15174-189">Como falhas de artefacto toodiagnose no DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="15174-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="15174-190">Associar um domínio do AD utilizando um modelo do resource manager no Azure DevTest Labs de tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="15174-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="15174-191">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="15174-191">Next steps</span></span>
* <span data-ttu-id="15174-192">Saiba como demasiado[adicionar um laboratório de tooa do repositório de artefactos Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="15174-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

