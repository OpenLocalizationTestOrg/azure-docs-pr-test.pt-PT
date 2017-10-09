---
title: sistemas de Azure Logic Apps de ficheiros do local com o aaaConnect tooon | Microsoft Docs
description: "Ligar sistemas de ficheiros tooon local a partir do seu fluxo de trabalho de aplicação lógica através do gateway de dados do Olá no local e conector sistema de ficheiros"
keywords: sistemas de ficheiros
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="b9ed0-104">Ligar sistemas de ficheiros tooon local a partir das logic apps com o conector sistema de ficheiros de Olá</span><span class="sxs-lookup"><span data-stu-id="b9ed0-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="b9ed0-105">Conectividade de cloud híbrida é aplicações central toologic, os dados de toomanage Sim e em segurança acesso recursos no local, as logic apps podem utilizar o gateway de dados do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="b9ed0-106">Neste artigo, mostramos como tooconnect tooan no local o sistema de ficheiros com um cenário básico: copiar um ficheiro tooa de tooDropbox carregado da partilha de ficheiros, em seguida, envie um e-mail.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ed0-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9ed0-107">Prerequisites</span></span>

- <span data-ttu-id="b9ed0-108">Instalar e configurar mais recente Olá [gateway de dados no local](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="b9ed0-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="b9ed0-109">Instalar o gateway de dados de no local mais recente do Olá, versão 1.15.6150.1 ou superior.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="b9ed0-110">[Ligar o gateway de dados no local toohello](http://aka.ms/logicapps-gateway) listas Olá passos.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="b9ed0-111">gateway de Olá tem de ser instalado numa máquina no local antes de poder continuar com o resto Olá passos Olá.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="b9ed0-112">Adicionar acionadores e ações para estabelecer a ligação de sistema de ficheiros tooyour</span><span class="sxs-lookup"><span data-stu-id="b9ed0-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="b9ed0-113">Criar uma aplicação lógica e adicione este acionador Dropbox: **quando é criado um ficheiro**</span><span class="sxs-lookup"><span data-stu-id="b9ed0-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="b9ed0-114">Em acionador Olá, escolha **passo seguinte** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="b9ed0-115">Na caixa de pesquisa de Olá, introduza `file system` para que possa vê ações todos suportadas para o conector sistema de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Pesquisa para o conector do ficheiro](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="b9ed0-117">Escolha Olá **criar ficheiro** ação e criar um sistema de ficheiros de tooyour de ligação.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="b9ed0-118">Se não tiver uma ligação existente, é pedido toocreate um.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="b9ed0-119">Escolha **ligar através do gateway de dados no local**.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="b9ed0-120">Propriedades são apresentados.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-120">More properties appear.</span></span>
   2. <span data-ttu-id="b9ed0-121">Selecione a pasta de raiz para o seu sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="b9ed0-122">pasta de raiz de Olá é a pasta de principal de principais de Olá, que é utilizada para caminhos relativos para todas as ações relacionadas com o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="b9ed0-123">Pode especificar uma pasta local na máquina de olá onde está instalado o gateway de dados no local Olá ou pasta Olá pode ser uma partilha de rede que Olá máquina pode aceder.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="b9ed0-124">Introduza Olá nome de utilizador e palavra-passe para o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="b9ed0-125">Selecione o gateway de Olá que instalou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-125">Select hello gateway that you previously installed.</span></span>

       ![Configurar a ligação](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="b9ed0-127">Depois de fornecer todos os detalhes de Olá, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="b9ed0-128">As Logic Apps configura e testa a ligação, certificando-se de que a ligação de Olá funciona corretamente.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="b9ed0-129">Se a ligação de Olá está configurado corretamente, consulte as opções para a ação de Olá que selecionou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="b9ed0-130">conector de sistema de ficheiros de Olá está agora pronto para ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="b9ed0-131">Especifique que pretende que toocopy ficheiros da pasta de raiz de toohello Dropbox para a partilha de ficheiros no local.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Criar a ação de ficheiros](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="b9ed0-133">Após a sua lógica cópias Olá de aplicativo, adicione uma ação do Outlook que envia uma mensagem de e-mail para que utilizadores relevantes saber sobre o novo ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="b9ed0-134">Introduza destinatários Olá, o título e o corpo da mensagem de e-mail Olá.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="b9ed0-135">No Seletor de conteúdo dinâmico de Olá, pode escolher saídas de dados do conector de ficheiro Olá, para poder adicionar o e-mail de toohello mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Enviar correio eletrónico ação](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="b9ed0-137">Guarde a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-137">Save your logic app.</span></span> <span data-ttu-id="b9ed0-138">Teste a aplicação através do carregamento tooDropbox um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="b9ed0-139">ficheiro de Olá deve obter a partilha de ficheiros copiados toohello no local e deverá receber uma mensagem de e-mail sobre a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="b9ed0-140">Saiba como demasiado[monitorizar as logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b9ed0-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="b9ed0-141">Parabéns, tem agora uma aplicação de lógica de trabalho que pode ligar-se o sistema de ficheiros tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="b9ed0-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="b9ed0-142">Tente explorar outras funcionalidades que Olá ofertas de conector, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9ed0-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="b9ed0-143">Criar o ficheiro</span><span class="sxs-lookup"><span data-stu-id="b9ed0-143">Create file</span></span>
- <span data-ttu-id="b9ed0-144">Lista de ficheiros na pasta</span><span class="sxs-lookup"><span data-stu-id="b9ed0-144">List files in folder</span></span>
- <span data-ttu-id="b9ed0-145">Anexar ficheiro</span><span class="sxs-lookup"><span data-stu-id="b9ed0-145">Append file</span></span>
- <span data-ttu-id="b9ed0-146">Eliminar ficheiro</span><span class="sxs-lookup"><span data-stu-id="b9ed0-146">Delete file</span></span>
- <span data-ttu-id="b9ed0-147">Obter o conteúdo do ficheiro</span><span class="sxs-lookup"><span data-stu-id="b9ed0-147">Get file content</span></span>
- <span data-ttu-id="b9ed0-148">Obter o conteúdo do ficheiro com o caminho</span><span class="sxs-lookup"><span data-stu-id="b9ed0-148">Get file content using path</span></span>
- <span data-ttu-id="b9ed0-149">Obter metadados do ficheiro</span><span class="sxs-lookup"><span data-stu-id="b9ed0-149">Get file metadata</span></span>
- <span data-ttu-id="b9ed0-150">Obter os metadados de ficheiro com o caminho</span><span class="sxs-lookup"><span data-stu-id="b9ed0-150">Get file metadata using path</span></span>
- <span data-ttu-id="b9ed0-151">Lista de ficheiros na pasta raiz</span><span class="sxs-lookup"><span data-stu-id="b9ed0-151">List files in root folder</span></span>
- <span data-ttu-id="b9ed0-152">Ficheiro de atualização</span><span class="sxs-lookup"><span data-stu-id="b9ed0-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="b9ed0-153">Swagger Olá de vista</span><span class="sxs-lookup"><span data-stu-id="b9ed0-153">View hello swagger</span></span>
<span data-ttu-id="b9ed0-154">Consulte Olá [swagger detalhes](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="b9ed0-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="b9ed0-155">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="b9ed0-155">Get help</span></span>

<span data-ttu-id="b9ed0-156">perguntas tooask, responda às perguntas e saiba que outras Azure Logic Apps os utilizadores estão a fazer, visite Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="b9ed0-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="b9ed0-157">toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador do Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="b9ed0-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9ed0-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b9ed0-158">Next steps</span></span>

- <span data-ttu-id="b9ed0-159">[Ligar a dados local tooon](../logic-apps/logic-apps-gateway-connection.md) partir das logic apps</span><span class="sxs-lookup"><span data-stu-id="b9ed0-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="b9ed0-160">Saiba mais sobre [integração empresarial com o](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b9ed0-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
