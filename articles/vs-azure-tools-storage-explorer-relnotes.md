---
title: "notas de versão aaaMicrosoft Explorador de armazenamento do Azure (pré-visualização) | Microsoft Docs"
description: "Notas de versão do Explorador de armazenamento do Microsoft Azure (pré-visualização)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="0d5ec-103">Notas de versão do Explorador de armazenamento do Microsoft Azure (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="0d5ec-104">Este artigo contém a versão de Olá notas do Explorador de armazenamento do Azure 0.8.16 (pré-visualização) da versão, bem como as notas de versão para versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="0d5ec-105">[Explorador de armazenamento do Microsoft Azure (pré-visualização)](./vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma que lhe permite tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="0d5ec-106">Versão 0.8.16 (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="0d5ec-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="0d5ec-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="0d5ec-108">Transferir o Explorador de armazenamento do Azure 0.8.16 (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="0d5ec-109">Explorador de armazenamento do Azure 0.8.16 (pré-visualização) para Windows</span><span class="sxs-lookup"><span data-stu-id="0d5ec-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="0d5ec-110">Explorador de armazenamento do Azure 0.8.16 (pré-visualização) para Mac</span><span class="sxs-lookup"><span data-stu-id="0d5ec-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="0d5ec-111">Explorador de armazenamento do Azure 0.8.16 (pré-visualização) para Linux</span><span class="sxs-lookup"><span data-stu-id="0d5ec-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="0d5ec-112">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-112">New</span></span>
* <span data-ttu-id="0d5ec-113">Quando abre um blob, Explorador de armazenamento solicitará tooupload Olá transferido ficheiros se for detetada alguma alteração</span><span class="sxs-lookup"><span data-stu-id="0d5ec-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="0d5ec-114">Pilha de Azure início de sessão experiência melhorada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="0d5ec-115">Desempenho melhorado Olá de carregamento/transferência pequena muitos ficheiros no Olá mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="0d5ec-116">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-116">Fixes</span></span>
* <span data-ttu-id="0d5ec-117">Para alguns tipos de BLOBs, escolher demasiado "substituir" durante um conflito de carregamento, por vezes, resultaria em carregamento Olá a ser reiniciado.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="0d5ec-118">Na versão 0.8.15, carregamentos, por vezes, seriam compartimento de 99%.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="0d5ec-119">Ao carregar a partilha de ficheiros de tooa de ficheiros, se tiver escolhido o diretório de tooa tooupload que ainda não existe, o carregamento irão falhar.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="0d5ec-120">Explorador de armazenamento foi incorretamente gerar carimbos de data / hora para assinaturas de acesso partilhado e consultas de tabela.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="0d5ec-121">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-121">Known Issues</span></span>
* <span data-ttu-id="0d5ec-122">Atualmente, o utilizando um nome e a cadeia de ligação de chave não funcionam.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="0d5ec-123">-Será corrigida na versão seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="0d5ec-124">Até que, em seguida, pode utilizar anexar com nome e chave.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="0d5ec-125">Se tentar tooopen um ficheiro com um nome de ficheiro do Windows inválido, transferências de Olá resultará num ficheiro não foi encontrado o erro.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="0d5ec-126">Depois de clicar em "Cancelar" uma tarefa, pode demorar um pouco para toocancel essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="0d5ec-127">Esta é uma limitação da biblioteca de nó de armazenamento do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="0d5ec-128">Depois de concluir o carregamento de um blob, separador de Olá que iniciado o carregamento de Olá seja atualizada.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="0d5ec-129">Esta é uma alteração do comportamento anterior e também fará com que toobe direcionado novamente toohello raiz do contentor de Olá que estiver no.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="0d5ec-130">Se optar por Olá certificado incorreto de PIN/smart card, em seguida, terá de toorestart na ordem toohave Explorador de armazenamento se esqueça de que decisão.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="0d5ec-131">Painel de definições de conta Olá pode mostrar que precisa de subscrições de toofilter tooreenter credenciais.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="0d5ec-132">Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="0d5ec-133">Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="0d5ec-134">Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="0d5ec-135">Para os utilizadores no Ubuntu 14.04, terá de tooensure GCC está a funcionar toodate - Isto pode ser feito através da execução Olá os seguintes comandos e, em seguida, reiniciar o computador:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="0d5ec-136">Para os utilizadores no Ubuntu 17.04, terá de tooinstall GConf - Isto pode ser feito Olá os seguintes comandos e, em seguida, reiniciar o computador a executar:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="0d5ec-137">Versão 0.8.14 (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="0d5ec-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="0d5ec-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="0d5ec-139">Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="0d5ec-140">Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização) para Windows</span><span class="sxs-lookup"><span data-stu-id="0d5ec-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="0d5ec-141">Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização) para Mac</span><span class="sxs-lookup"><span data-stu-id="0d5ec-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="0d5ec-142">Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização) para Linux</span><span class="sxs-lookup"><span data-stu-id="0d5ec-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="0d5ec-143">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-143">New</span></span>

* <span data-ttu-id="0d5ec-144">Atualizado too1.7.2 de versão Electron na vantagem de tootake de ordem de várias atualizações de segurança críticas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="0d5ec-145">-Pode agora aceder rapidamente ao guia de resolução de problemas online Olá menu Ajuda Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="0d5ec-146">Explorador de armazenamento de resolução de problemas [guia][2]</span><span class="sxs-lookup"><span data-stu-id="0d5ec-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="0d5ec-147">[Instruções] [ 3] sobre a ligação de subscrição do Azure pilha tooan</span><span class="sxs-lookup"><span data-stu-id="0d5ec-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="0d5ec-148">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-148">Known Issues</span></span>

* <span data-ttu-id="0d5ec-149">Botões de caixa de diálogo de confirmação do Olá Eliminar pasta não registar Olá cliques do rato no Linux.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="0d5ec-150">Solução é a chave do toouse Olá Enter</span><span class="sxs-lookup"><span data-stu-id="0d5ec-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="0d5ec-151">Se optar por Olá certificado incorreto de PIN/smart card, em seguida, terá de toorestart na ordem toohave Explorador de armazenamento se esquecer da decisão de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="0d5ec-152">Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros</span><span class="sxs-lookup"><span data-stu-id="0d5ec-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="0d5ec-153">Painel de definições de conta Olá pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem</span><span class="sxs-lookup"><span data-stu-id="0d5ec-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="0d5ec-154">Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="0d5ec-155">Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="0d5ec-156">Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="0d5ec-157">Ubuntu 14.04 tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="0d5ec-158">Versões anteriores</span><span class="sxs-lookup"><span data-stu-id="0d5ec-158">Previous releases</span></span>

* [<span data-ttu-id="0d5ec-159">Versão 0.8.13</span><span class="sxs-lookup"><span data-stu-id="0d5ec-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="0d5ec-160">Versão 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="0d5ec-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="0d5ec-161">Versão 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="0d5ec-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="0d5ec-162">Versão 0.8.7</span><span class="sxs-lookup"><span data-stu-id="0d5ec-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="0d5ec-163">Versão 0.8.6</span><span class="sxs-lookup"><span data-stu-id="0d5ec-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="0d5ec-164">Versão 0.8.5</span><span class="sxs-lookup"><span data-stu-id="0d5ec-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="0d5ec-165">Versão 0.8.4</span><span class="sxs-lookup"><span data-stu-id="0d5ec-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="0d5ec-166">Versão 0.8.3</span><span class="sxs-lookup"><span data-stu-id="0d5ec-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="0d5ec-167">Versão 0.8.2</span><span class="sxs-lookup"><span data-stu-id="0d5ec-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="0d5ec-168">Versão 0.8.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="0d5ec-169">Versão 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="0d5ec-170">Versão 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="0d5ec-171">Versão 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="0d5ec-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="0d5ec-172">Versão 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="0d5ec-173">Versão 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="0d5ec-174">Versão 0.8.13</span><span class="sxs-lookup"><span data-stu-id="0d5ec-174">Version 0.8.13</span></span>
<span data-ttu-id="0d5ec-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="0d5ec-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-176">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-176">New</span></span>

* <span data-ttu-id="0d5ec-177">Explorador de armazenamento de resolução de problemas [guia][2]</span><span class="sxs-lookup"><span data-stu-id="0d5ec-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="0d5ec-178">[Instruções] [ 3] sobre a ligação de subscrição do Azure pilha tooan</span><span class="sxs-lookup"><span data-stu-id="0d5ec-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-179">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-179">Fixes</span></span>

* <span data-ttu-id="0d5ec-180">Corrigido: O carregamento de ficheiros tinha uma elevada probabilidade de causar um fora de erro de memória</span><span class="sxs-lookup"><span data-stu-id="0d5ec-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="0d5ec-181">Fixo: Pode agora iniciar sessão com PIN/smart card</span><span class="sxs-lookup"><span data-stu-id="0d5ec-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="0d5ec-182">Corrigido: Abrir no Portal agora funciona com o Azure China, Datacenters do Azure, Azure US Government e pilha do Azure</span><span class="sxs-lookup"><span data-stu-id="0d5ec-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="0d5ec-183">Corrigido: Ao carregar um contentor do blob tooa pasta, um erro de "Operação ilegal", por vezes, ocorreriam</span><span class="sxs-lookup"><span data-stu-id="0d5ec-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="0d5ec-184">Corrigido: Selecionar tudo foi desativado durante a gestão de instantâneos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="0d5ec-185">Fixo: Olá metadados do blob base Olá podem obter substituídos depois de visualizar propriedades Olá dos respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-186">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-186">Known Issues</span></span>

* <span data-ttu-id="0d5ec-187">Se optar por Olá certificado incorreto de PIN/smart card, em seguida, terá de toorestart na ordem toohave Explorador de armazenamento se esquecer da decisão de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="0d5ec-188">Enquanto ampliado ou reduzir, o nível de zoom Olá momentaneamente pode repor nível predefinido de toohello</span><span class="sxs-lookup"><span data-stu-id="0d5ec-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="0d5ec-189">Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros</span><span class="sxs-lookup"><span data-stu-id="0d5ec-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="0d5ec-190">Painel de definições de conta Olá pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem</span><span class="sxs-lookup"><span data-stu-id="0d5ec-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="0d5ec-191">Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="0d5ec-192">Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="0d5ec-193">Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="0d5ec-194">Ubuntu 14.04 tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="0d5ec-195">Versão 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="0d5ec-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="0d5ec-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="0d5ec-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-197">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-197">New</span></span>

* <span data-ttu-id="0d5ec-198">Explorador de armazenamento agora será fechada automaticamente quando instala uma atualização de notificação de atualização de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="0d5ec-199">Acesso rápido no local fornece uma experiência melhorada para trabalhar com os recursos acedidos com frequência</span><span class="sxs-lookup"><span data-stu-id="0d5ec-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="0d5ec-200">No editor de contentor do Blob Olá, agora, pode ver que o virtual machine um blob em leasing pertence</span><span class="sxs-lookup"><span data-stu-id="0d5ec-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="0d5ec-201">Agora pode fechar o painel do lado esquerdo de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="0d5ec-202">Deteção agora é executado em Olá mesmo tempo como transferência</span><span class="sxs-lookup"><span data-stu-id="0d5ec-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="0d5ec-203">Estatísticas de utilização no contentor de BLOBs, a partilha de ficheiros e a tabela editores toosee Olá tamanho dos seus recursos ou a seleção de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="0d5ec-204">Pode agora o início de sessão tooAzure Active Directory (AAD) com base em contas de pilha do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="0d5ec-205">Pode agora mais 32 MB tooPremium as contas de armazenamento de ficheiros de arquivo de carregamento</span><span class="sxs-lookup"><span data-stu-id="0d5ec-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="0d5ec-206">Suporte de acessibilidade de melhorada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-206">Improved accessibility support</span></span>
* <span data-ttu-id="0d5ec-207">Agora pode adicionar fidedigna de Base-64 codificado certificados x. 509 SSL por vai tooEdit -&gt; certificados SSL -&gt; importar certificados</span><span class="sxs-lookup"><span data-stu-id="0d5ec-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-208">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-208">Fixes</span></span>

* <span data-ttu-id="0d5ec-209">Fixo: depois de atualizar as credenciais de uma conta, vista de árvore Olá seria, por vezes, não atualiza automaticamente</span><span class="sxs-lookup"><span data-stu-id="0d5ec-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="0d5ec-210">Corrigido: gerar uma SAS para tabelas e filas de emulador resultaria num URL inválido</span><span class="sxs-lookup"><span data-stu-id="0d5ec-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="0d5ec-211">Fixo: contas de armazenamento premium podem agora ser expandidas enquanto um proxy está ativado</span><span class="sxs-lookup"><span data-stu-id="0d5ec-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="0d5ec-212">Corrigido: Olá aplicar botão em contas de Olá página de gestão não funciona se tiver selecionadas de contas de 1 ou 0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="0d5ec-213">Fixo: carregar blobs que necessitam de resoluções de conflito poderão falhar - fixo em 0.8.11</span><span class="sxs-lookup"><span data-stu-id="0d5ec-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="0d5ec-214">Corrigido: enviar comentários foi quebrada em 0.8.11 - fixo em 0.8.12</span><span class="sxs-lookup"><span data-stu-id="0d5ec-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-215">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-215">Known Issues</span></span>

* <span data-ttu-id="0d5ec-216">Após a atualização too0.8.10, terá de toorefresh todas as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="0d5ec-217">Enquanto ampliado ou reduzir, o nível de zoom Olá pode repor momentaneamente nível predefinido de toohello.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="0d5ec-218">Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá causar erros.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="0d5ec-219">Painel de definições de conta Olá pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="0d5ec-220">Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="0d5ec-221">Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="0d5ec-222">Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="0d5ec-223">Ubuntu 14.04 tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="0d5ec-224">Versão 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="0d5ec-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="0d5ec-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="0d5ec-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="0d5ec-226">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-226">New</span></span>

* <span data-ttu-id="0d5ec-227">Explorador de armazenamento 0.8.9 irá transferir automaticamente a versão mais recente do Olá para atualizações.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="0d5ec-228">CORREÇÃO: utilizar um portal gerado tooattach URI de SAS que uma conta de armazenamento resulta num erro.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="0d5ec-229">Agora pode criar, gerir e promover instantâneos do blob.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="0d5ec-230">Pode agora iniciar sessão em contas de tooAzure China, Datacenters do Azure e Azure US Government.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="0d5ec-231">Agora, pode alterar o nível de zoom Olá.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-231">You can now change hello zoom level.</span></span> <span data-ttu-id="0d5ec-232">Utilize as opções de Olá Olá vista menu tooZoom no Zoom Out e repor Zoom.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="0d5ec-233">Carateres Unicode já são suportados nos metadados de utilizador para os blobs e de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="0d5ec-234">Melhoramentos de acessibilidade.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-234">Accessibility improvements.</span></span>
* <span data-ttu-id="0d5ec-235">notas de versão do Olá próxima versão podem ser visualizadas de notificação de atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="0d5ec-236">Também pode ver Olá atual notas de versão do menu de ajuda de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-237">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-237">Fixes</span></span>

* <span data-ttu-id="0d5ec-238">Fixo: número de versão Olá é agora apresentado corretamente no painel de controlo do Windows</span><span class="sxs-lookup"><span data-stu-id="0d5ec-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="0d5ec-239">Corrigido: pesquisa já não se encontra limitada too50, 000 nós</span><span class="sxs-lookup"><span data-stu-id="0d5ec-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="0d5ec-240">Fixo: partilha de ficheiros do carregamento tooa puserem para sempre se o diretório de destino Olá já não existe</span><span class="sxs-lookup"><span data-stu-id="0d5ec-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="0d5ec-241">Fixa: estabilidade melhorada para carregamentos de tempo e as transferências</span><span class="sxs-lookup"><span data-stu-id="0d5ec-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-242">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-242">Known Issues</span></span>

* <span data-ttu-id="0d5ec-243">Enquanto ampliado ou reduzir, o nível de zoom Olá pode repor momentaneamente nível predefinido de toohello.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="0d5ec-244">Acesso rápido só funciona com itens de subscrição com base.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="0d5ec-245">Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="0d5ec-246">-Pode demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos tem acesso rápido.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="0d5ec-247">Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá causar erros.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="0d5ec-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="0d5ec-249">Versão 0.8.7</span><span class="sxs-lookup"><span data-stu-id="0d5ec-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="0d5ec-250">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-250">New</span></span>

* <span data-ttu-id="0d5ec-251">Pode escolher como tooresolve conflitos no início de Olá de uma atualização, transferir ou copiar sessão numa janela de atividades de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="0d5ec-252">Coloque o cursor sobre um separador toosee Olá caminho completo do recurso de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="0d5ec-253">Ao clicar num separador, sincronizar com a localização no painel de navegação do lado esquerdo de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-254">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-254">Fixes</span></span>

* <span data-ttu-id="0d5ec-255">Fixo: Explorador de armazenamento é agora uma aplicação fidedigna no Mac</span><span class="sxs-lookup"><span data-stu-id="0d5ec-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="0d5ec-256">Fixo: Ubuntu 14.04 é novamente suportada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="0d5ec-257">Fixo:, Por vezes, Olá adicionar a conta está intermitente IU ao carregar as subscrições</span><span class="sxs-lookup"><span data-stu-id="0d5ec-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="0d5ec-258">Fixo:, Por vezes, nem todos os recursos de armazenamento foram listados no painel de navegação do lado esquerdo de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="0d5ec-259">Fixo: painel de ações de Olá por vezes apresentado ações vazias</span><span class="sxs-lookup"><span data-stu-id="0d5ec-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="0d5ec-260">Fixo: tamanho da janela Olá da sessão de Olá fechada pela última vez é agora retido</span><span class="sxs-lookup"><span data-stu-id="0d5ec-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="0d5ec-261">Corrigido: Pode abrir vários separadores para Olá mesmo recurso utilizando o menu de contexto de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-262">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-262">Known Issues</span></span>

* <span data-ttu-id="0d5ec-263">Acesso rápido só funciona com itens de subscrição com base.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="0d5ec-264">Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão</span><span class="sxs-lookup"><span data-stu-id="0d5ec-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="0d5ec-265">Poderá demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos possui um acesso rápido</span><span class="sxs-lookup"><span data-stu-id="0d5ec-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="0d5ec-266">Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros</span><span class="sxs-lookup"><span data-stu-id="0d5ec-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="0d5ec-267">Os identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado ou pode fazer com que a exceção não processada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="0d5ec-268">Para Olá pela primeira vez utilizando Olá Explorador de armazenamento no macOS, poderá ver vários pedidos solicitando a keychain de tooaccess de permissão do utilizador.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="0d5ec-269">Sugerimos que selecionou permitir sempre que, de modo linha Olá não apresentar novamente</span><span class="sxs-lookup"><span data-stu-id="0d5ec-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="0d5ec-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="0d5ec-271">Versão 0.8.6</span><span class="sxs-lookup"><span data-stu-id="0d5ec-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-272">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-272">New</span></span>

* <span data-ttu-id="0d5ec-273">Pode agora pin utilizado mais frequentemente serviços toohello acesso rápido para navegação fácil</span><span class="sxs-lookup"><span data-stu-id="0d5ec-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="0d5ec-274">Pode agora abrir editores vários separadores diferentes.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="0d5ec-275">Tooopen um separador temporário; de clique único Faça duplo clique tooopen um separador permanente. Pode também clicar em Olá separador temporário toomake-um separador permanente</span><span class="sxs-lookup"><span data-stu-id="0d5ec-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="0d5ec-276">Efetuamos desempenho percetível e melhoramentos estabilidade para carregamentos e transferências, especialmente para ficheiros grandes em máquinas rápidas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="0d5ec-277">Pastas "virtuais" vazias agora podem ser criadas em contentores de BLOBs</span><span class="sxs-lookup"><span data-stu-id="0d5ec-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="0d5ec-278">Ter novamente introduzimos pesquisa de âmbito com a nossa nova pesquisa avançada subcadeia, pelo que tem agora duas opções para procurar:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="0d5ec-279">Global pesquisar - basta introduzir um termo de pesquisa na caixa de texto de pesquisa de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="0d5ec-280">Pesquisa de âmbito - clique Olá Lupa ícone tooa nó seguinte, em seguida, adicionar um end de toohello termo de pesquisa do caminho de Olá, ou com o botão direito e selecione "Pesquisa de aqui"</span><span class="sxs-lookup"><span data-stu-id="0d5ec-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="0d5ec-281">Foi adicionado temas vários: claro (predefinição), escuros, elevado contraste negra e elevado contraste em branco.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="0d5ec-282">Aceda tooEdit -&gt; temas toochange sua preferência de temas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="0d5ec-283">Pode modificar as propriedades de Blob e ficheiro</span><span class="sxs-lookup"><span data-stu-id="0d5ec-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="0d5ec-284">Agora suportamos o codificado (base64) e não codificado de fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="0d5ec-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="0d5ec-285">No Linux, um SO de 64 bits é agora necessário.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="0d5ec-286">Para esta versão suportamos apenas 64 bits Ubuntu 16.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="0d5ec-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="0d5ec-287">Iremos foi atualizado com a nossa logótipo!</span><span class="sxs-lookup"><span data-stu-id="0d5ec-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-288">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-288">Fixes</span></span>

* <span data-ttu-id="0d5ec-289">Corrigido: Ecrã freezing problemas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="0d5ec-290">Fixo: Segurança avançada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="0d5ec-291">Corrigido: Contas anexadas, por vezes, duplicadas foi apresentada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="0d5ec-292">Fixo: Um blob com um tipo de conteúdo foi possível gerar uma exceção</span><span class="sxs-lookup"><span data-stu-id="0d5ec-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="0d5ec-293">Fixo: Olá de abrir o painel de consulta numa tabela vazia não foi possível</span><span class="sxs-lookup"><span data-stu-id="0d5ec-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="0d5ec-294">Fixo: Erros na pesquisa de varia</span><span class="sxs-lookup"><span data-stu-id="0d5ec-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="0d5ec-295">Fixo: Aumentar o número de Olá de recursos carregado a partir de 50 too100 quando clicar em "Mais carga"</span><span class="sxs-lookup"><span data-stu-id="0d5ec-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="0d5ec-296">Corrigido: Na primeira execução, se uma conta é iniciada, iremos agora selecionar todas as subscrições para essa conta por predefinição</span><span class="sxs-lookup"><span data-stu-id="0d5ec-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-297">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-297">Known Issues</span></span>

* <span data-ttu-id="0d5ec-298">Esta versão do Olá Explorador de armazenamento não é executado no Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="0d5ec-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="0d5ec-299">tooopen vários separadores para Olá mesmo recurso, efetue não continuamente, clique em Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="0d5ec-300">Clique no outro recurso e, em seguida, volte atrás e, em seguida, clique em Olá original recursos tooopen-lo novamente no outro separador</span><span class="sxs-lookup"><span data-stu-id="0d5ec-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="0d5ec-301">Acesso rápido só funciona com itens de subscrição com base.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="0d5ec-302">Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão</span><span class="sxs-lookup"><span data-stu-id="0d5ec-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="0d5ec-303">Poderá demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos possui um acesso rápido</span><span class="sxs-lookup"><span data-stu-id="0d5ec-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="0d5ec-304">Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros</span><span class="sxs-lookup"><span data-stu-id="0d5ec-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="0d5ec-305">Os identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado ou pode fazer com que a exceção não processada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="0d5ec-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="0d5ec-307">Versão 0.8.5</span><span class="sxs-lookup"><span data-stu-id="0d5ec-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-308">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-308">New</span></span>

* <span data-ttu-id="0d5ec-309">Pode agora utilizar SAS gerado pelo Portal chaves tooattach tooStorage contas e recursos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-310">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-310">Fixes</span></span>

* <span data-ttu-id="0d5ec-311">Corrigido: condição provável de antecipação durante a pesquisa, por vezes, causado toobecome de nós não é possível expandir</span><span class="sxs-lookup"><span data-stu-id="0d5ec-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="0d5ec-312">Fixo: "Utilizar HTTP" não funciona ao ligar a contas tooStorage com nome de conta e chave</span><span class="sxs-lookup"><span data-stu-id="0d5ec-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="0d5ec-313">Fixo: Chaves SAS (especialmente gerado pelo Portal aqueles) devolverem um erro de "à direita barra"</span><span class="sxs-lookup"><span data-stu-id="0d5ec-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="0d5ec-314">Fixo: tabela importar problemas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="0d5ec-315">Por vezes, a chave de partição e a chave de linha foram inversa</span><span class="sxs-lookup"><span data-stu-id="0d5ec-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="0d5ec-316">Não é possível tooread "nulo" chaves de partição</span><span class="sxs-lookup"><span data-stu-id="0d5ec-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-317">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-317">Known Issues</span></span>

* <span data-ttu-id="0d5ec-318">Identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado</span><span class="sxs-lookup"><span data-stu-id="0d5ec-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="0d5ec-319">Pilha do Azure não suporta atualmente a ficheiros, pelo que tentar ficheiros tooexpand irá mostrar um erro</span><span class="sxs-lookup"><span data-stu-id="0d5ec-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="0d5ec-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="0d5ec-321">Versão 0.8.4</span><span class="sxs-lookup"><span data-stu-id="0d5ec-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="0d5ec-322">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-322">New</span></span>

* <span data-ttu-id="0d5ec-323">Gerar contas de toostorage hiperligações diretas, contentores, filas, tabelas, ou partilhas de ficheiros para a partilha e fácil acedem a recursos de tooyour - Windows e Mac OS suporta</span><span class="sxs-lookup"><span data-stu-id="0d5ec-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="0d5ec-324">Procure os contentores de BLOBs, tabelas, filas, partilhas de ficheiros ou as contas do storage a partir da caixa de pesquisa de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="0d5ec-325">Agora pode agrupar cláusulas no construtor de consultas de tabela Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="0d5ec-326">Mudar o nome e copiar/colar contentores de BLOBs, partilhas de ficheiros, tabelas, blobs, blob pastas, ficheiros e diretórios de contas ligados por SAS e contentores</span><span class="sxs-lookup"><span data-stu-id="0d5ec-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="0d5ec-327">Mudar o nome e a cópia dos contentores de BLOBs e partilhas de ficheiros agora preservar as propriedades e os metadados</span><span class="sxs-lookup"><span data-stu-id="0d5ec-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-328">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-328">Fixes</span></span>

* <span data-ttu-id="0d5ec-329">Fixo: não é possível editar as entidades da tabela se contiverem propriedades booleanos ou binárias</span><span class="sxs-lookup"><span data-stu-id="0d5ec-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-330">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-330">Known Issues</span></span>

* <span data-ttu-id="0d5ec-331">Identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado</span><span class="sxs-lookup"><span data-stu-id="0d5ec-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="0d5ec-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="0d5ec-333">Versão 0.8.3</span><span class="sxs-lookup"><span data-stu-id="0d5ec-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="0d5ec-334">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-334">New</span></span>

* <span data-ttu-id="0d5ec-335">Mudar o nome de contentores, tabelas, partilhas de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0d5ec-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="0d5ec-336">Experiência melhorada de construtor de consultas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-336">Improved Query builder experience</span></span>
* <span data-ttu-id="0d5ec-337">Consultas de toosave e carga de capacidade</span><span class="sxs-lookup"><span data-stu-id="0d5ec-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="0d5ec-338">Direcionar ligações toostorage contas ou contentores, filas, tabelas ou partilhas para a partilha e facilmente aceder aos seus recursos de ficheiros (apenas Windows - macOS suportam disponível em breve!)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="0d5ec-339">Capacidade toomanage e configurar as regras CORS</span><span class="sxs-lookup"><span data-stu-id="0d5ec-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-340">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-340">Fixes</span></span>

* <span data-ttu-id="0d5ec-341">Fixo: Accounts Microsoft requerem reautenticação cada 8-12 horas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-342">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-342">Known Issues</span></span>

* <span data-ttu-id="0d5ec-343">Por vezes, hello IU pode aparecer congelada - maximizando a janela de Olá ajuda a resolver este problema</span><span class="sxs-lookup"><span data-stu-id="0d5ec-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="0d5ec-344">instalação de macOS pode necessitar de permissões elevadas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="0d5ec-345">Painel de definições de conta pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem</span><span class="sxs-lookup"><span data-stu-id="0d5ec-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="0d5ec-346">Partilhas de ficheiros de mudança de nome contentores de BLOBs, tabelas e não preservar metadados ou outras propriedades no contentor de Olá, tais como a quota de partilha de ficheiros, um nível de acesso público ou políticas de acesso</span><span class="sxs-lookup"><span data-stu-id="0d5ec-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="0d5ec-347">Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="0d5ec-348">Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome</span><span class="sxs-lookup"><span data-stu-id="0d5ec-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="0d5ec-349">Copiar ou mudar o nome de recursos não funciona no contas ligados por SAS</span><span class="sxs-lookup"><span data-stu-id="0d5ec-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="0d5ec-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="0d5ec-351">Versão 0.8.2</span><span class="sxs-lookup"><span data-stu-id="0d5ec-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="0d5ec-352">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-352">New</span></span>

* <span data-ttu-id="0d5ec-353">As contas de armazenamento estão agrupadas por subscrições; armazenamento de desenvolvimento e de recursos ligados através de SAS ou de chave são apresentados no nó (locais e anexadas)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="0d5ec-354">Terminar sessão das contas no painel de "Definições de conta do Azure"</span><span class="sxs-lookup"><span data-stu-id="0d5ec-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="0d5ec-355">Configurar tooenable de definições de proxy e gerir o início de sessão</span><span class="sxs-lookup"><span data-stu-id="0d5ec-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="0d5ec-356">Criar e quebra de concessões de blob</span><span class="sxs-lookup"><span data-stu-id="0d5ec-356">Create and break blob leases</span></span>
* <span data-ttu-id="0d5ec-357">Contentores de BLOBs aberta, filas, tabelas e os ficheiros de clique único</span><span class="sxs-lookup"><span data-stu-id="0d5ec-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-358">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-358">Fixes</span></span>

* <span data-ttu-id="0d5ec-359">Corrigido: inseridas com bibliotecas .NET ou Java de fila de mensagens não é corretamente descodificar a partir de base64</span><span class="sxs-lookup"><span data-stu-id="0d5ec-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="0d5ec-360">Fixo: $metrics tabelas não são apresentadas para contas do Blob Storage</span><span class="sxs-lookup"><span data-stu-id="0d5ec-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="0d5ec-361">Fixo: nó de tabelas não funciona para o armazenamento (desenvolvimento) local</span><span class="sxs-lookup"><span data-stu-id="0d5ec-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-362">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-362">Known Issues</span></span>

* <span data-ttu-id="0d5ec-363">instalação de macOS pode necessitar de permissões elevadas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="0d5ec-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="0d5ec-365">Versão 0.8.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="0d5ec-366">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-366">New</span></span>

* <span data-ttu-id="0d5ec-367">Suporte de partilha de ficheiros: ver, carregar, transferir, copiar ficheiros e diretórios, SAS URIs (criar e ligar)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="0d5ec-368">Experiência de utilizador para ligar tooStorage com SAS URIs ou chaves de conta melhorada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="0d5ec-369">Exportar os resultados da consulta de tabela</span><span class="sxs-lookup"><span data-stu-id="0d5ec-369">Export table query results</span></span>
* <span data-ttu-id="0d5ec-370">Reordenação de coluna de tabela e personalização</span><span class="sxs-lookup"><span data-stu-id="0d5ec-370">Table column reordering and customization</span></span>
* <span data-ttu-id="0d5ec-371">Ver os contentores de BLOBs de $logs e $metrics tabelas para contas de armazenamento com a métrica ativada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="0d5ec-372">Melhorado exportar e importar o comportamento, inclui agora o tipo de valor de propriedade</span><span class="sxs-lookup"><span data-stu-id="0d5ec-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-373">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-373">Fixes</span></span>

* <span data-ttu-id="0d5ec-374">Fixo: carregar ou transferir blobs grandes pode resultar em carregamentos/transferências incompletas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="0d5ec-375">Editar fixo:, adicionar ou importar uma entidade com um valor de cadeia numérica ("1") irá convertê-lo toodouble</span><span class="sxs-lookup"><span data-stu-id="0d5ec-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="0d5ec-376">Fixo: Não é possível tooexpand nó de tabela de Olá no ambiente de desenvolvimento local Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-377">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-377">Known Issues</span></span>

* <span data-ttu-id="0d5ec-378">$metrics tabelas não estão visíveis para contas do Blob Storage</span><span class="sxs-lookup"><span data-stu-id="0d5ec-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="0d5ec-379">Fila de mensagens através de programação adicionadas não pode ser apresentada corretamente se mensagens hello são codificadas com codificação Base64</span><span class="sxs-lookup"><span data-stu-id="0d5ec-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="0d5ec-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="0d5ec-381">Versão 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-382">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-382">New</span></span>

* <span data-ttu-id="0d5ec-383">Falhas de processamento para a aplicação de erros melhor</span><span class="sxs-lookup"><span data-stu-id="0d5ec-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-384">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-384">Fixes</span></span>

* <span data-ttu-id="0d5ec-385">Erros fixo onde as mensagens de barra de informações por vezes, não apareçam quando as credenciais de início de sessão eram necessárias</span><span class="sxs-lookup"><span data-stu-id="0d5ec-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-386">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-386">Known Issues</span></span>

* <span data-ttu-id="0d5ec-387">Tabelas: Adicionar, editar, ou importar uma entidade que tem uma propriedade com um valor numérico ambiguously, tais como "1" ou "1.0", e Olá utilizador tenta toosend-o como um `Edm.String`, valor de Olá regressará através do cliente de Olá API como um Edm.Double</span><span class="sxs-lookup"><span data-stu-id="0d5ec-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="0d5ec-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="0d5ec-389">Versão 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="0d5ec-390">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-390">New</span></span>

* <span data-ttu-id="0d5ec-391">Suporte de tabela: visualização, consultar, exportação, importar e as operações CRUD de entidades</span><span class="sxs-lookup"><span data-stu-id="0d5ec-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="0d5ec-392">Suporte da fila: visualizar, adicionar, dequeueing mensagens</span><span class="sxs-lookup"><span data-stu-id="0d5ec-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="0d5ec-393">Gerar o URI SAS para contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0d5ec-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="0d5ec-394">Ligar a contas de tooStorage URIs SAS</span><span class="sxs-lookup"><span data-stu-id="0d5ec-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="0d5ec-395">Notificações de atualização para atualizações futuras tooStorage Explorer</span><span class="sxs-lookup"><span data-stu-id="0d5ec-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="0d5ec-396">Atualizado para o aspeto e funcionalidade</span><span class="sxs-lookup"><span data-stu-id="0d5ec-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-397">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-397">Fixes</span></span>

* <span data-ttu-id="0d5ec-398">Melhorias de desempenho e fiabilidade</span><span class="sxs-lookup"><span data-stu-id="0d5ec-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="0d5ec-399">Problemas conhecidos &amp; mitigações</span><span class="sxs-lookup"><span data-stu-id="0d5ec-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="0d5ec-400">Transferência de ficheiros grandes blob não funciona corretamente - é recomendável utilizar o AzCopy enquanto foi resolver este problema</span><span class="sxs-lookup"><span data-stu-id="0d5ec-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="0d5ec-401">As credenciais da conta não serão possível obter nem em cache se a pasta raiz de Olá não é possível localizar ou não pode ser escrita</span><span class="sxs-lookup"><span data-stu-id="0d5ec-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="0d5ec-402">Se podemos são adicionar, editar ou importar uma entidade que tem uma propriedade com um valor numérico ambiguously, tais como "1" ou "1.0", e o utilizador Olá tenta toosend-o como um `Edm.String`, valor de Olá regressará através do cliente de Olá API como um Edm.Double</span><span class="sxs-lookup"><span data-stu-id="0d5ec-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="0d5ec-403">Quando importar os ficheiros CSV com os registos de múltiplas linhas, os dados de Olá poderão obter chopped ou scrambled</span><span class="sxs-lookup"><span data-stu-id="0d5ec-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="0d5ec-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="0d5ec-405">Versão 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="0d5ec-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-406">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-406">Fixes</span></span>

* <span data-ttu-id="0d5ec-407">Melhoria do desempenho global quando o carregamento, a transferência e copiar os blobs</span><span class="sxs-lookup"><span data-stu-id="0d5ec-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="0d5ec-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="0d5ec-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="0d5ec-409">Versão 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-410">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-410">New</span></span>

* <span data-ttu-id="0d5ec-411">Apoio técnico para Linux (paridade funcionalidades tooOSX)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="0d5ec-412">Adicionar contentores de Blobs com a chave de assinaturas de acesso partilhado (SAS)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="0d5ec-413">Adicionar contas de armazenamento para o Azure China</span><span class="sxs-lookup"><span data-stu-id="0d5ec-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="0d5ec-414">Adicionar contas de armazenamento com os pontos finais personalizados</span><span class="sxs-lookup"><span data-stu-id="0d5ec-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="0d5ec-415">Abra e visualize os blobs de texto e imagem de conteúdo de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="0d5ec-416">Ver e editar propriedades de BLOBs e metadados</span><span class="sxs-lookup"><span data-stu-id="0d5ec-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="0d5ec-417">Correções</span><span class="sxs-lookup"><span data-stu-id="0d5ec-417">Fixes</span></span>

* <span data-ttu-id="0d5ec-418">Corrigido: carregamento ou transferência um grande número de blobs (500 +) pode, por vezes, fazer com que Olá aplicação toohave um ecrã branco</span><span class="sxs-lookup"><span data-stu-id="0d5ec-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="0d5ec-419">Fixo: quando definir o nível de acesso de público do contentor de blob, valor novo Olá não é atualizada até que defina novamente Olá focarem-se no contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="0d5ec-420">Além disso, caixa de diálogo Olá sempre predefinições demasiado "não público aceder" e não Olá atual valor real.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="0d5ec-421">Geral melhor teclado acessibilidade e IU de suporte</span><span class="sxs-lookup"><span data-stu-id="0d5ec-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="0d5ec-422">Texto de histórico de navegação estrutural encapsula num wrapper quando é longo com espaço em branco</span><span class="sxs-lookup"><span data-stu-id="0d5ec-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="0d5ec-423">Caixa de diálogo SAS suporta a validação de entrada</span><span class="sxs-lookup"><span data-stu-id="0d5ec-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="0d5ec-424">Armazenamento local continua toobe disponível mesmo se as credenciais de utilizador expiraram</span><span class="sxs-lookup"><span data-stu-id="0d5ec-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="0d5ec-425">Quando é eliminado um contentor de blob aberta, o Explorador de blob Olá no lado direito de Olá está fechado</span><span class="sxs-lookup"><span data-stu-id="0d5ec-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-426">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-426">Known Issues</span></span>

* <span data-ttu-id="0d5ec-427">Linux tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:</span><span class="sxs-lookup"><span data-stu-id="0d5ec-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="0d5ec-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="0d5ec-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="0d5ec-429">Versão 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="0d5ec-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="0d5ec-430">novo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-430">New</span></span>

* <span data-ttu-id="0d5ec-431">macOS e as versões do Windows</span><span class="sxs-lookup"><span data-stu-id="0d5ec-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="0d5ec-432">A iniciar sessão tooview as contas do Storage – utilizar a sua conta da organização, Account Microsoft, 2FA, etc.</span><span class="sxs-lookup"><span data-stu-id="0d5ec-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="0d5ec-433">Armazenamento de desenvolvimento local (utilizar o emulador do storage apenas de Windows)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="0d5ec-434">Suporte de recursos do Azure Resource Manager e clássico</span><span class="sxs-lookup"><span data-stu-id="0d5ec-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="0d5ec-435">Criar e eliminar blobs, filas ou tabelas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="0d5ec-436">Procurar blobs específicos, filas ou tabelas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="0d5ec-437">Explore os conteúdos de Olá de contentores de BLOBs</span><span class="sxs-lookup"><span data-stu-id="0d5ec-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="0d5ec-438">Ver e navegar através de diretórios</span><span class="sxs-lookup"><span data-stu-id="0d5ec-438">View and navigate through directories</span></span>
* <span data-ttu-id="0d5ec-439">Carregar, transferir e eliminar os blobs e pastas</span><span class="sxs-lookup"><span data-stu-id="0d5ec-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="0d5ec-440">Ver e editar propriedades de BLOBs e metadados</span><span class="sxs-lookup"><span data-stu-id="0d5ec-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="0d5ec-441">Gerar chaves SAS</span><span class="sxs-lookup"><span data-stu-id="0d5ec-441">Generate SAS keys</span></span>
* <span data-ttu-id="0d5ec-442">Gerir e criar políticas de acesso armazenada (SAP)</span><span class="sxs-lookup"><span data-stu-id="0d5ec-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="0d5ec-443">Procurar blobs pelo prefixo</span><span class="sxs-lookup"><span data-stu-id="0d5ec-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="0d5ec-444">Arraste 'n drop tooupload de ficheiros ou transferir</span><span class="sxs-lookup"><span data-stu-id="0d5ec-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="0d5ec-445">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-445">Known Issues</span></span>

* <span data-ttu-id="0d5ec-446">Ao definir o nível de acesso de público do contentor de blob, valor novo Olá não for atualizado até que defina novamente Olá focarem-se no contentor de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="0d5ec-447">Quando abrir o nível de acesso público Olá diálogo tooset Olá, indica sempre "Sem acesso de público" como predefinição de Olá e não Olá atual valor real</span><span class="sxs-lookup"><span data-stu-id="0d5ec-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="0d5ec-448">Não é possível mudar o nome de blobs transferidos</span><span class="sxs-lookup"><span data-stu-id="0d5ec-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="0d5ec-449">Quando ocorre um erro e não é apresentado o erro de Olá de estado de entradas de registo de atividade será, por vezes, obter "presa" num em curso</span><span class="sxs-lookup"><span data-stu-id="0d5ec-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="0d5ec-450">Por vezes, falhas ou activa completamente branco quando tenta tooupload ou transferir um grande número de blobs</span><span class="sxs-lookup"><span data-stu-id="0d5ec-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="0d5ec-451">Por vezes, cancelar uma operação de cópia não funciona</span><span class="sxs-lookup"><span data-stu-id="0d5ec-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="0d5ec-452">Durante a criação de um contentor (tabela/fila/BLOBs), se introduzir um nome inválido e continuar toocreate outro sob um tipo de contentor diferente, não é possível definir o foco no novo tipo de Olá</span><span class="sxs-lookup"><span data-stu-id="0d5ec-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="0d5ec-453">Não é possível criar uma nova pasta ou mudar o nome de pasta</span><span class="sxs-lookup"><span data-stu-id="0d5ec-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md