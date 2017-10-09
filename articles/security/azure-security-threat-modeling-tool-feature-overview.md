---
title: "aaaMicrosoft ferramenta modelação de ameaça - Azure | Microsoft Docs"
description: "Saiba mais sobre todas as funcionalidades de Olá disponíveis no Olá ferramenta modelação de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="52cc3-103">Descrição geral da funcionalidade de ferramenta modelação de ameaça</span><span class="sxs-lookup"><span data-stu-id="52cc3-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="52cc3-104">Estamos satisfeitos por que escolheu toouse Olá ferramenta modelação de ameaça para a necessidades de modelação de ameaça!</span><span class="sxs-lookup"><span data-stu-id="52cc3-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="52cc3-105">Se ainda não o feito, visite  **[introdução Olá ferramenta modelação de ameaça](./azure-security-threat-modeling-tool-getting-started.md)**  Noções básicas de Olá toolearn.</span><span class="sxs-lookup"><span data-stu-id="52cc3-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="52cc3-106">A nossa ferramenta é atualizada frequentemente, por isso este guia, muitas vezes, toosee nosso funcionalidades e melhorias mais recentes.</span><span class="sxs-lookup"><span data-stu-id="52cc3-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="52cc3-107">Clicar no botão de "Criar um novo modelo" Olá abre uma página de início em branco, semelhante toohello imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="52cc3-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Página de início em branco](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="52cc3-109">Utilizar o modelo de ameaça Olá criados pela nossa equipa em Olá  **[introdução](./azure-security-threat-modeling-tool-getting-started.md)**  exemplo, vamos Consulte todas as funcionalidades de Olá disponíveis na ferramenta de Olá ainda hoje.</span><span class="sxs-lookup"><span data-stu-id="52cc3-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Modelo de ameaça básico](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="52cc3-111">Navegação</span><span class="sxs-lookup"><span data-stu-id="52cc3-111">Navigation</span></span>

<span data-ttu-id="52cc3-112">Antes de explorar as funcionalidades integradas Olá, vamos abordar componentes principais Olá encontrados na ferramenta de Olá</span><span class="sxs-lookup"><span data-stu-id="52cc3-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="52cc3-113">Itens de menu</span><span class="sxs-lookup"><span data-stu-id="52cc3-113">Menu items</span></span>

<span data-ttu-id="52cc3-114">experiência de Olá deve ser produtos da Microsoft tooother semelhantes.</span><span class="sxs-lookup"><span data-stu-id="52cc3-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="52cc3-115">Vamos começar por percorrer os itens de menu de nível superior de Olá:</span><span class="sxs-lookup"><span data-stu-id="52cc3-115">Let’s begin by going through hello top-level menu items:</span></span>

![Itens de menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="52cc3-117">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="52cc3-117">Label</span></span>                               | <span data-ttu-id="52cc3-118">Detalhes</span><span class="sxs-lookup"><span data-stu-id="52cc3-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="52cc3-119">**Ficheiro**</span><span class="sxs-lookup"><span data-stu-id="52cc3-119">**File**</span></span> | <ul><li><span data-ttu-id="52cc3-120">Abrir, guardar e fechar ficheiros</span><span class="sxs-lookup"><span data-stu-id="52cc3-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="52cc3-121">Contas de início de sessão In/Out do OneDrive</span><span class="sxs-lookup"><span data-stu-id="52cc3-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="52cc3-122">Ligações de partilha (vista + editar)</span><span class="sxs-lookup"><span data-stu-id="52cc3-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="52cc3-123">Ver informações de ficheiro</span><span class="sxs-lookup"><span data-stu-id="52cc3-123">View File Information</span></span></li><li><span data-ttu-id="52cc3-124">Aplique o novo modelo tooExisting modelos</span><span class="sxs-lookup"><span data-stu-id="52cc3-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="52cc3-125">**Editar**</span><span class="sxs-lookup"><span data-stu-id="52cc3-125">**Edit**</span></span> | <span data-ttu-id="52cc3-126">Anulação/Refazer ações, como também uma cópia, colar e delete</span><span class="sxs-lookup"><span data-stu-id="52cc3-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="52cc3-127">**Vista**</span><span class="sxs-lookup"><span data-stu-id="52cc3-127">**View**</span></span> | <ul><li><span data-ttu-id="52cc3-128">Alternar entre **Analysis** e **Design** vistas</span><span class="sxs-lookup"><span data-stu-id="52cc3-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="52cc3-129">Abra windows fechados (e.g.stencils, propriedades de elemento e mensagens)</span><span class="sxs-lookup"><span data-stu-id="52cc3-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="52cc3-130">Repor as definições de toodefault de esquema</span><span class="sxs-lookup"><span data-stu-id="52cc3-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="52cc3-131">**Diagrama**</span><span class="sxs-lookup"><span data-stu-id="52cc3-131">**Diagram**</span></span> | <span data-ttu-id="52cc3-132">Adicionar/eliminar diagramas e navegar pelas "Separadores" de diagramas</span><span class="sxs-lookup"><span data-stu-id="52cc3-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="52cc3-133">**Relatórios**</span><span class="sxs-lookup"><span data-stu-id="52cc3-133">**Reports**</span></span> | <span data-ttu-id="52cc3-134">Criar HTML relatórios tooshare com outras pessoas</span><span class="sxs-lookup"><span data-stu-id="52cc3-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="52cc3-135">**Ajuda**</span><span class="sxs-lookup"><span data-stu-id="52cc3-135">**Help**</span></span> | <span data-ttu-id="52cc3-136">Orienta toohelp é utilizar a ferramenta de Olá</span><span class="sxs-lookup"><span data-stu-id="52cc3-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="52cc3-137">ícones de Olá são os atalhos para os menus de nível superior de Olá:</span><span class="sxs-lookup"><span data-stu-id="52cc3-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="52cc3-138">Ícone</span><span class="sxs-lookup"><span data-stu-id="52cc3-138">Icon</span></span>                               | <span data-ttu-id="52cc3-139">Detalhes</span><span class="sxs-lookup"><span data-stu-id="52cc3-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="52cc3-140">**Abrir**</span><span class="sxs-lookup"><span data-stu-id="52cc3-140">**Open**</span></span> | <span data-ttu-id="52cc3-141">É aberto um novo ficheiro</span><span class="sxs-lookup"><span data-stu-id="52cc3-141">Opens a new file</span></span> |
| <span data-ttu-id="52cc3-142">**Guardar**</span><span class="sxs-lookup"><span data-stu-id="52cc3-142">**Save**</span></span> | <span data-ttu-id="52cc3-143">Guarda o ficheiro atual</span><span class="sxs-lookup"><span data-stu-id="52cc3-143">Saves current file</span></span> |
| <span data-ttu-id="52cc3-144">**Design**</span><span class="sxs-lookup"><span data-stu-id="52cc3-144">**Design**</span></span> | <span data-ttu-id="52cc3-145">Entrar em vista de estrutura, onde pode criar modelos</span><span class="sxs-lookup"><span data-stu-id="52cc3-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="52cc3-146">**Analisar**</span><span class="sxs-lookup"><span data-stu-id="52cc3-146">**Analyze**</span></span> | <span data-ttu-id="52cc3-147">Mostra gerado ameaças e as respetivas propriedades</span><span class="sxs-lookup"><span data-stu-id="52cc3-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="52cc3-148">**Adicionar diagrama**</span><span class="sxs-lookup"><span data-stu-id="52cc3-148">**Add Diagram**</span></span> | <span data-ttu-id="52cc3-149">Adiciona o novo diagrama (semelhante toonew separadores no Excel)</span><span class="sxs-lookup"><span data-stu-id="52cc3-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="52cc3-150">**Eliminar diagrama**</span><span class="sxs-lookup"><span data-stu-id="52cc3-150">**Delete Diagram**</span></span> | <span data-ttu-id="52cc3-151">Elimina o diagrama atual</span><span class="sxs-lookup"><span data-stu-id="52cc3-151">Deletes current diagram</span></span> |
| <span data-ttu-id="52cc3-152">**Cortar/copiar/colar**</span><span class="sxs-lookup"><span data-stu-id="52cc3-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="52cc3-153">Cópias/cuts/cola sobre elementos</span><span class="sxs-lookup"><span data-stu-id="52cc3-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="52cc3-154">**Anulação/Refazer**</span><span class="sxs-lookup"><span data-stu-id="52cc3-154">**Undo/Redo**</span></span> | <span data-ttu-id="52cc3-155">Ações anular/efectuar novamente</span><span class="sxs-lookup"><span data-stu-id="52cc3-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="52cc3-156">**Ampliar / reduzir**</span><span class="sxs-lookup"><span data-stu-id="52cc3-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="52cc3-157">Amplia inteira dentro ou fora do diagrama de Olá para uma melhor vista</span><span class="sxs-lookup"><span data-stu-id="52cc3-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="52cc3-158">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="52cc3-158">**Feedback**</span></span> | <span data-ttu-id="52cc3-159">Abre Olá fórum MSDN</span><span class="sxs-lookup"><span data-stu-id="52cc3-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="52cc3-160">Tela</span><span class="sxs-lookup"><span data-stu-id="52cc3-160">Canvas</span></span>

<span data-ttu-id="52cc3-161">espaço de olá onde pode arrastar e largar os elementos no.</span><span class="sxs-lookup"><span data-stu-id="52cc3-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="52cc3-162">Arrastar e largar é Olá mais rápida e modelos de toobuild de forma mais eficientes.</span><span class="sxs-lookup"><span data-stu-id="52cc3-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="52cc3-163">Também pode clique com o botão direito e selecione menu Olá, que adiciona genéricas versões dos elementos de Olá que estiver a utilizar, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="52cc3-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="52cc3-164">Remover stencil Olá numa tela Olá</span><span class="sxs-lookup"><span data-stu-id="52cc3-164">Dropping hello stencil on hello canvas</span></span>

![Largar tela](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="52cc3-166">Clicar no stencil Olá</span><span class="sxs-lookup"><span data-stu-id="52cc3-166">Clicking on hello stencil</span></span>

![Propriedades de elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="52cc3-168">Stencils</span><span class="sxs-lookup"><span data-stu-id="52cc3-168">Stencils</span></span>

<span data-ttu-id="52cc3-169">Onde pode encontrar todos os stencils toouse disponível com base no modelo de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="52cc3-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="52cc3-170">Se não conseguir localizar os elementos à direita Olá, tente utilizar outro modelo ou modificar um toofit às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="52cc3-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="52cc3-171">Geralmente, deve ser capaz de toofind uma combinação de categorias, como Olá aqueles abaixo:</span><span class="sxs-lookup"><span data-stu-id="52cc3-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="52cc3-172">Nome de stencil</span><span class="sxs-lookup"><span data-stu-id="52cc3-172">Stencil Name</span></span>                               | <span data-ttu-id="52cc3-173">Detalhes</span><span class="sxs-lookup"><span data-stu-id="52cc3-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="52cc3-174">**Processo**</span><span class="sxs-lookup"><span data-stu-id="52cc3-174">**Process**</span></span> | <span data-ttu-id="52cc3-175">Aplicações, plug-ins do Browser, Threads, máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="52cc3-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="52cc3-176">**Interactor externo**</span><span class="sxs-lookup"><span data-stu-id="52cc3-176">**External Interactor**</span></span> | <span data-ttu-id="52cc3-177">Fornecedores de autenticação, os Browsers, utilizadores, aplicações Web</span><span class="sxs-lookup"><span data-stu-id="52cc3-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="52cc3-178">**Arquivo de dados**</span><span class="sxs-lookup"><span data-stu-id="52cc3-178">**Data Store**</span></span> | <span data-ttu-id="52cc3-179">Registo de ficheiros, bases de dados de configuração de cache, armazenamento,</span><span class="sxs-lookup"><span data-stu-id="52cc3-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="52cc3-180">**Fluxo de dados**</span><span class="sxs-lookup"><span data-stu-id="52cc3-180">**Data Flow**</span></span> | <span data-ttu-id="52cc3-181">Binários, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, com o nome Pipe, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="52cc3-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="52cc3-182">**Limites de linha/limite de fidedignidade**</span><span class="sxs-lookup"><span data-stu-id="52cc3-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="52cc3-183">Redes empresariais, Internet, máquina, Sandbox, de modo Kernel/utilizador</span><span class="sxs-lookup"><span data-stu-id="52cc3-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="52cc3-184">Notas/mensagens</span><span class="sxs-lookup"><span data-stu-id="52cc3-184">Notes/Messages</span></span>

| <span data-ttu-id="52cc3-185">Componente</span><span class="sxs-lookup"><span data-stu-id="52cc3-185">Component</span></span>                               | <span data-ttu-id="52cc3-186">Detalhes</span><span class="sxs-lookup"><span data-stu-id="52cc3-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="52cc3-187">**Mensagens**</span><span class="sxs-lookup"><span data-stu-id="52cc3-187">**Messages**</span></span> | <span data-ttu-id="52cc3-188">Lógica de ferramenta interno que os utilizadores de alertas sempre que há um erro, como não existem fluxos de dados entre elementos</span><span class="sxs-lookup"><span data-stu-id="52cc3-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="52cc3-189">**Notas**</span><span class="sxs-lookup"><span data-stu-id="52cc3-189">**Notes**</span></span> | <span data-ttu-id="52cc3-190">Notas de ficheiro toohello adicionado por equipas de engenharia completamente Olá design e rever o processo manuais</span><span class="sxs-lookup"><span data-stu-id="52cc3-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="52cc3-191">Propriedades de elemento</span><span class="sxs-lookup"><span data-stu-id="52cc3-191">Element properties</span></span>

<span data-ttu-id="52cc3-192">Estes variam consoante a elementos Olá selecionados.</span><span class="sxs-lookup"><span data-stu-id="52cc3-192">These vary by hello elements selected.</span></span> <span data-ttu-id="52cc3-193">Para além dos limites de fidedignidade, todos os outros elementos contenham 3 seleções gerais:</span><span class="sxs-lookup"><span data-stu-id="52cc3-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="52cc3-194">Propriedade de elemento</span><span class="sxs-lookup"><span data-stu-id="52cc3-194">Element Property</span></span>                               | <span data-ttu-id="52cc3-195">Detalhes</span><span class="sxs-lookup"><span data-stu-id="52cc3-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="52cc3-196">**Nome**</span><span class="sxs-lookup"><span data-stu-id="52cc3-196">**Name**</span></span> | <span data-ttu-id="52cc3-197">Útil para atribuir nomes a sua toobe processos, arquivos, interactors e fluxos facilmente reconhecido</span><span class="sxs-lookup"><span data-stu-id="52cc3-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="52cc3-198">**Fora do âmbito**</span><span class="sxs-lookup"><span data-stu-id="52cc3-198">**Out of Scope**</span></span> | <span data-ttu-id="52cc3-199">Se selecionado, o elemento de Olá é retirado matriz de geração de ameaça Olá (não recomendado)</span><span class="sxs-lookup"><span data-stu-id="52cc3-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="52cc3-200">**Razão para fora do âmbito**</span><span class="sxs-lookup"><span data-stu-id="52cc3-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="52cc3-201">Os utilizadores de toolet do campo justificação saber porquê fora do âmbito selecionado</span><span class="sxs-lookup"><span data-stu-id="52cc3-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="52cc3-202">As propriedades são alteradas em cada categoria de elemento.</span><span class="sxs-lookup"><span data-stu-id="52cc3-202">Properties are changed under each element category.</span></span> <span data-ttu-id="52cc3-203">Clique em cada elemento tooinspect Olá as opções disponíveis, ou abra Olá modelo toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="52cc3-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="52cc3-204">Vamos colocar no funcionalidades Olá.</span><span class="sxs-lookup"><span data-stu-id="52cc3-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="52cc3-205">Ecrã de boas-vindas</span><span class="sxs-lookup"><span data-stu-id="52cc3-205">Welcome screen</span></span>

<span data-ttu-id="52cc3-206">ecrã de boas-vindas Olá é Olá primeira coisa que vê se abrir a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="52cc3-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="52cc3-207">Abra um modelo</span><span class="sxs-lookup"><span data-stu-id="52cc3-207">Open A model</span></span>

<span data-ttu-id="52cc3-208">Posicionado sobre o botão "Abrir um modelo" mostra 2 opções ocultas: "Aberta de neste computador" e "Aberta do OneDrive."</span><span class="sxs-lookup"><span data-stu-id="52cc3-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="52cc3-209">Olá abre pela primeira vez o ecrã de ficheiros abertos Olá, enquanto Olá segundo leva-o através do processo de início de sessão Olá para o OneDrive, permitindo-lhe toopick pastas e ficheiros após uma autenticação com êxito.</span><span class="sxs-lookup"><span data-stu-id="52cc3-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Modelo aberto](./media/azure-security-threat-modeling-tool/openmodel.png)

![Abra do computador ou do OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="52cc3-212">Comentários, problemas e sugestões</span><span class="sxs-lookup"><span data-stu-id="52cc3-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="52cc3-213">A seleção desta opção irá demorar toohello fóruns do MSDN para SDL ferramentas.</span><span class="sxs-lookup"><span data-stu-id="52cc3-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="52cc3-214">É toocheck uma excelente forma saída que outras pessoas são indicar sobre a ferramenta de Olá, incluindo soluções e ideias de novo.</span><span class="sxs-lookup"><span data-stu-id="52cc3-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Comentários](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="52cc3-216">Vista de estrutura</span><span class="sxs-lookup"><span data-stu-id="52cc3-216">Design view</span></span>

<span data-ttu-id="52cc3-217">Sempre que abrir ou criar um novo modelo, será direcionado toohello vista de estrutura.</span><span class="sxs-lookup"><span data-stu-id="52cc3-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="52cc3-218">A adição de elementos</span><span class="sxs-lookup"><span data-stu-id="52cc3-218">Adding elements</span></span>

<span data-ttu-id="52cc3-219">Existem 2 formas tooadd elementos na grelha de Olá:</span><span class="sxs-lookup"><span data-stu-id="52cc3-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="52cc3-220">**Arrastar e largar** – arraste grelha de toohello de elemento pretendido Olá, em seguida, utilize Olá elemento propriedades tooprovide obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="52cc3-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="52cc3-221">**Clique com o botão direito** – clique em qualquer lugar em grelha Olá e selecione a partir do menu de lista pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="52cc3-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="52cc3-222">Será apresentada uma representação genérica de que o elemento no ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="52cc3-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="52cc3-223">Elementos de ligação</span><span class="sxs-lookup"><span data-stu-id="52cc3-223">Connecting elements</span></span>

<span data-ttu-id="52cc3-224">Existem 2 formas tooconnect elementos na ferramenta de Olá:</span><span class="sxs-lookup"><span data-stu-id="52cc3-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="52cc3-225">**Arrastar e largar** – arraste grelha de toohello Olá pretendida do fluxo de dados e ligar-se ambos os elementos de adequado toohello termina.</span><span class="sxs-lookup"><span data-stu-id="52cc3-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="52cc3-226">**Clique em + deslocar** – clique no primeiro elemento de Olá (enviar dados), prima e mantenha premido Olá Shift chave e o segundo elemento de Olá selecione (receber dados).</span><span class="sxs-lookup"><span data-stu-id="52cc3-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="52cc3-227">Clique com o botão direito e selecione "Ligar".</span><span class="sxs-lookup"><span data-stu-id="52cc3-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="52cc3-228">Se estiver a utilizar um fluxo de dados bidirecional, ordem de Olá não é tão importante.</span><span class="sxs-lookup"><span data-stu-id="52cc3-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="52cc3-229">Propriedades</span><span class="sxs-lookup"><span data-stu-id="52cc3-229">Properties</span></span>

<span data-ttu-id="52cc3-230">Mostra todas as propriedades de Olá que podem ser modificadas no stencils Olá colocados no diagrama de Olá.</span><span class="sxs-lookup"><span data-stu-id="52cc3-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="52cc3-231">Propriedades de Olá toosee, basta clicar no stencil Olá e informações de Olá preenchidas em conformidade.</span><span class="sxs-lookup"><span data-stu-id="52cc3-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="52cc3-232">exemplo de Olá abaixo mostra antes e depois de um "base de dados" stencil é arrastar diagrama Olá:</span><span class="sxs-lookup"><span data-stu-id="52cc3-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="52cc3-233">Antes de</span><span class="sxs-lookup"><span data-stu-id="52cc3-233">Before</span></span>

![Antes de](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="52cc3-235">Após</span><span class="sxs-lookup"><span data-stu-id="52cc3-235">After</span></span>

![Após](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="52cc3-237">Mensagens</span><span class="sxs-lookup"><span data-stu-id="52cc3-237">Messages</span></span>

<span data-ttu-id="52cc3-238">Se criar um modelo de ameaça e se esqueça de fluem de dados de tooconnect tooelements, janela de mensagem de Olá notifica tooact.</span><span class="sxs-lookup"><span data-stu-id="52cc3-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="52cc3-239">Pode escolher tooignore-lo ou siga Olá problema de Olá toofix de instruções.</span><span class="sxs-lookup"><span data-stu-id="52cc3-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Mensagens](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="52cc3-241">Notas</span><span class="sxs-lookup"><span data-stu-id="52cc3-241">Notes</span></span>

<span data-ttu-id="52cc3-242">Mudar os separadores de mensagens tooNotes permite todos os seus pensamentos de modo tooadd notas tooyour diagrama toocapture</span><span class="sxs-lookup"><span data-stu-id="52cc3-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="52cc3-243">Vista de análise</span><span class="sxs-lookup"><span data-stu-id="52cc3-243">Analysis view</span></span>

<span data-ttu-id="52cc3-244">Depois de concluir a criação do diagrama, comutador através de vista tooanalysis ao vai toohello seleções de menu superior e escolha a paleta de paint de toohello seguinte do Olá Lupa.</span><span class="sxs-lookup"><span data-stu-id="52cc3-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Vista de análise](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="52cc3-246">Seleção de ameaça gerado</span><span class="sxs-lookup"><span data-stu-id="52cc3-246">Generated threat selection</span></span>

<span data-ttu-id="52cc3-247">Ao clicar numa ameaça, pode tirar partido das três funções únicas:</span><span class="sxs-lookup"><span data-stu-id="52cc3-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="52cc3-248">Funcionalidade</span><span class="sxs-lookup"><span data-stu-id="52cc3-248">Feature</span></span>                               | <span data-ttu-id="52cc3-249">Informações</span><span class="sxs-lookup"><span data-stu-id="52cc3-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="52cc3-250">**Indicador de leitura**</span><span class="sxs-lookup"><span data-stu-id="52cc3-250">**Read Indicator**</span></span> | <p><span data-ttu-id="52cc3-251">Ameaças agora está marcada como de leitura, que pode facilmente ajudar a manter um registo dos itens de Olá que já frequentou através de</span><span class="sxs-lookup"><span data-stu-id="52cc3-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Indicador Unread/leitura](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="52cc3-253">**Interação foco**</span><span class="sxs-lookup"><span data-stu-id="52cc3-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="52cc3-254">Interação no diagrama de Olá que pertencem a ameaça de toothat é realçada</span><span class="sxs-lookup"><span data-stu-id="52cc3-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Interação foco](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="52cc3-256">**Propriedades de ameaça**</span><span class="sxs-lookup"><span data-stu-id="52cc3-256">**Threat Properties**</span></span> | <p><span data-ttu-id="52cc3-257">Informações adicionais sobre ameaças Olá são preenchidas na janela de propriedades de ameaça Olá</span><span class="sxs-lookup"><span data-stu-id="52cc3-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Propriedades de ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="52cc3-259">Alteração da prioridade</span><span class="sxs-lookup"><span data-stu-id="52cc3-259">Priority change</span></span>

<span data-ttu-id="52cc3-260">Alterar o nível de prioridade de Olá de cada ameaça gerado também altera as respetivas toomake cores-ameaças de prioridade alta, média e baixa tooidentify fácil.</span><span class="sxs-lookup"><span data-stu-id="52cc3-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Alteração da prioridade](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="52cc3-262">Campos de editáveis de propriedades de ameaça</span><span class="sxs-lookup"><span data-stu-id="52cc3-262">Threat properties editable fields</span></span>

<span data-ttu-id="52cc3-263">Como mostrado na imagem de Olá acima, os utilizadores podem alterar as informações de Olá geradas pela ferramenta de Olá um também adicionar campos de toocertain de informações, tais como justificação.</span><span class="sxs-lookup"><span data-stu-id="52cc3-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="52cc3-264">Estes campos são gerados pelo modelo de Olá, pelo que se precisar de mais informações para cada ameaça, pode toomake encorajados modificações.</span><span class="sxs-lookup"><span data-stu-id="52cc3-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Propriedades de ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="52cc3-266">Relatórios</span><span class="sxs-lookup"><span data-stu-id="52cc3-266">Reports</span></span>

<span data-ttu-id="52cc3-267">Quando tiver terminado a alteração de prioridades e atualização Olá estado de cada gerado ameaça, pode guardar o ficheiro de Olá e/ou imprimir um relatório por ficar demasiado "relatório" e, em seguida, "Criar relatório completo."</span><span class="sxs-lookup"><span data-stu-id="52cc3-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="52cc3-268">Relatório de Olá tooname irá ser mais frequentes e quando o fizer, deverá ver algo semelhante imagem toohello abaixo:</span><span class="sxs-lookup"><span data-stu-id="52cc3-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Relatório](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="52cc3-270">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="52cc3-270">Next steps</span></span>

<span data-ttu-id="52cc3-271">toocontribute um modelo para a Comunidade Olá, visite tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  página.</span><span class="sxs-lookup"><span data-stu-id="52cc3-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="52cc3-272">**[Transferir](https://aka.ms/tmtpreview)**  Olá ferramenta tooget iniciada atualmente.</span><span class="sxs-lookup"><span data-stu-id="52cc3-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
