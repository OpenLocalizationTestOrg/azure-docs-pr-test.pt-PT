---
title: "aaaHow toouse Olá multisservidor Azure Plug-in com a integração contínua Hudson | Microsoft Docs"
description: "Descreve como toouse Olá Azure multisservidor Plug-in com a integração contínua Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="ecac2-103">Como toouse Olá Azure multisservidor Plug-in com a integração contínua Hudson</span><span class="sxs-lookup"><span data-stu-id="ecac2-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="ecac2-104">Olá, Azure multisservidor Plug-in para Hudson permite-lhe nós de multisservidor tooprovision no Azure quando em execução distribuída baseia-se.</span><span class="sxs-lookup"><span data-stu-id="ecac2-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="ecac2-105">Instalar Olá Azure multisservidor Plug-in</span><span class="sxs-lookup"><span data-stu-id="ecac2-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="ecac2-106">No dashboard de Hudson Olá, clique em **gerir Hudson**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ecac2-107">No Olá **gerir Hudson** página, clique em **gerir plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="ecac2-108">Clique em Olá **disponível** separador.</span><span class="sxs-lookup"><span data-stu-id="ecac2-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="ecac2-109">Clique em **pesquisa** e tipo **Azure** toolimit Olá lista toorelevant plug-ins.</span><span class="sxs-lookup"><span data-stu-id="ecac2-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="ecac2-110">Se optar por tooscroll através da lista de Olá de plug-ins disponíveis, encontrará Olá multisservidor Azure Plug-in em Olá **distribuídas compilar e gestão de clusters** secção Olá **outros** separador.</span><span class="sxs-lookup"><span data-stu-id="ecac2-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="ecac2-111">Selecione a caixa de verificação Olá para **Plug-in do Azure multisservidor**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="ecac2-112">Clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-112">Click **Install**.</span></span>
7. <span data-ttu-id="ecac2-113">Reinicie Hudson.</span><span class="sxs-lookup"><span data-stu-id="ecac2-113">Restart Hudson.</span></span>

<span data-ttu-id="ecac2-114">Agora que Olá Plug-in estiver instalado, passos Olá seria tooconfigure Olá Plug-in com o perfil de subscrição do Azure e toocreate um modelo que será utilizado na criação de Olá VM para o nó de multisservidor Olá.</span><span class="sxs-lookup"><span data-stu-id="ecac2-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="ecac2-115">Configurar Olá Azure multisservidor Plug-in com o seu perfil de subscrição</span><span class="sxs-lookup"><span data-stu-id="ecac2-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="ecac2-116">Um perfil de subscrição, também referidos tooas definições de publicação, é um ficheiro XML que contém as credenciais seguras e algumas informações adicionais, terá de toowork com o Azure no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="ecac2-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="ecac2-117">Olá tooconfigure multisservidor Azure Plug-in, tem de:</span><span class="sxs-lookup"><span data-stu-id="ecac2-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="ecac2-118">O id de subscrição</span><span class="sxs-lookup"><span data-stu-id="ecac2-118">Your subscription id</span></span>
* <span data-ttu-id="ecac2-119">Um certificado de gestão para a sua subscrição</span><span class="sxs-lookup"><span data-stu-id="ecac2-119">A management certificate for your subscription</span></span>

<span data-ttu-id="ecac2-120">Pode encontrá-las no seu [perfil subscrição].</span><span class="sxs-lookup"><span data-stu-id="ecac2-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="ecac2-121">Segue-se um exemplo de um perfil de subscrição.</span><span class="sxs-lookup"><span data-stu-id="ecac2-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="ecac2-122">Assim que tiver o seu perfil de subscrição, siga estas Olá tooconfigure de passos do Azure multisservidor Plug-in.</span><span class="sxs-lookup"><span data-stu-id="ecac2-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="ecac2-123">No dashboard de Hudson Olá, clique em **gerir Hudson**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ecac2-124">Clique em **Configurar sistema**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="ecac2-125">Desloque para baixo Olá de toofind de página Olá **nuvem** secção.</span><span class="sxs-lookup"><span data-stu-id="ecac2-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="ecac2-126">Clique em **Adicionar nova nuvem > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![Adicionar nova na nuvem][add new cloud]
   
    <span data-ttu-id="ecac2-128">Isto irá mostrar campos olá onde terá tooenter detalhes da sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="ecac2-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![configurar o perfil][configure profile]
5. <span data-ttu-id="ecac2-130">Copie o certificado de gestão e o id de subscrição de Olá do seu perfil de subscrição e cole-os em campos apropriados Olá.</span><span class="sxs-lookup"><span data-stu-id="ecac2-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="ecac2-131">Quando copiar Olá id e a gestão de certificado de subscrição, **não** incluir as aspas Olá que coloque os valores de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecac2-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="ecac2-132">Clique em **verifique configuração**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="ecac2-133">Quando a configuração de Olá é verificada com êxito, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="ecac2-134">Configurar o plug-in modelo de máquina virtual para Olá multisservidor do Azure</span><span class="sxs-lookup"><span data-stu-id="ecac2-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="ecac2-135">Um modelo de máquina virtual define os parâmetros de Olá Olá Plug-in utilizará toocreate um nó subordinado no Azure.</span><span class="sxs-lookup"><span data-stu-id="ecac2-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="ecac2-136">No Olá os passos seguintes, irá ser criar modelo para uma VM com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ecac2-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="ecac2-137">No dashboard de Hudson Olá, clique em **gerir Hudson**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ecac2-138">Clique em **Configurar sistema**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="ecac2-139">Desloque para baixo Olá de toofind de página Olá **nuvem** secção.</span><span class="sxs-lookup"><span data-stu-id="ecac2-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="ecac2-140">Dentro do Olá **nuvem** secção, localizar **adicionar modelo de Máquina Virtual do Azure** e clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="ecac2-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![Adicionar modelo de vm][add vm template]
5. <span data-ttu-id="ecac2-142">Especifique um nome de serviço em nuvem no Olá **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="ecac2-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="ecac2-143">Se o nome de Olá especificado refere-se tooan existente serviço em nuvem, será aprovisionado Olá VM em que o serviço.</span><span class="sxs-lookup"><span data-stu-id="ecac2-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="ecac2-144">Caso contrário, o Azure irá criar um novo.</span><span class="sxs-lookup"><span data-stu-id="ecac2-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="ecac2-145">No Olá **Descrição** campo, introduza o texto que descreve o modelo de Olá estiver a criar.</span><span class="sxs-lookup"><span data-stu-id="ecac2-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="ecac2-146">Estas informações são apenas para fins de documentary e não são utilizadas no aprovisionamento de uma VM.</span><span class="sxs-lookup"><span data-stu-id="ecac2-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="ecac2-147">No Olá **etiquetas** campo, introduza **linux**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="ecac2-148">Esta etiqueta tooidentify utilizados Olá modelo que está a criar e é o modelo de Olá tooreference posteriormente utilizado ao criar uma tarefa de Hudson.</span><span class="sxs-lookup"><span data-stu-id="ecac2-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="ecac2-149">Selecione uma região onde será criada Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ecac2-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="ecac2-150">Selecione o tamanho da VM Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="ecac2-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="ecac2-151">Especifique uma conta de armazenamento onde Olá VM será criada.</span><span class="sxs-lookup"><span data-stu-id="ecac2-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="ecac2-152">Certifique-se de que está a ser Olá mesma região que o serviço de nuvem Olá que irá utilizar.</span><span class="sxs-lookup"><span data-stu-id="ecac2-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="ecac2-153">Se pretender que o novo armazenamento toobe, criado, pode deixar este campo em branco.</span><span class="sxs-lookup"><span data-stu-id="ecac2-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="ecac2-154">Período de retenção Especifica o número de Olá de minutos antes de Hudson elimina um subordinado de inatividade.</span><span class="sxs-lookup"><span data-stu-id="ecac2-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="ecac2-155">Deixe este valor predefinido Olá 60.</span><span class="sxs-lookup"><span data-stu-id="ecac2-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="ecac2-156">No **utilização**, selecione Olá condição apropriada quando este nó subordinado será utilizado.</span><span class="sxs-lookup"><span data-stu-id="ecac2-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="ecac2-157">Por agora, selecione **utilizar este nó quanto possível**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="ecac2-158">Neste momento, o formulário seria ter um aspeto toothis um pouco semelhante:</span><span class="sxs-lookup"><span data-stu-id="ecac2-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![configuração de modelo][template config]
13. <span data-ttu-id="ecac2-160">No **família de imagem ou Id** tiver toospecify que imagem do sistema será instalada na VM.</span><span class="sxs-lookup"><span data-stu-id="ecac2-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="ecac2-161">Pode selecionar numa lista de famílias de imagem ou especificar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="ecac2-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="ecac2-162">Se quiser tooselect de uma lista de famílias de imagem, introduza Olá primeiro caráter (maiúsculas e minúsculas) do nome de família Olá imagem.</span><span class="sxs-lookup"><span data-stu-id="ecac2-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="ecac2-163">Por exemplo, escrevendo **U** será apresentada uma lista de famílias de Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="ecac2-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="ecac2-164">Depois de selecionar a partir da lista de Olá, Jenkins irá utilizar Olá versão mais recente dessa imagem de sistema de que família quando aprovisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="ecac2-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![Lista de família do SO][OS family list]
    
     <span data-ttu-id="ecac2-166">Se tiver uma imagem personalizada que pretende que toouse em vez disso, introduza o nome de Olá dessa imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="ecac2-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="ecac2-167">Os nomes de imagens personalizadas não são apresentados numa lista, para que tenha tooensure Olá nome é introduzido corretamente.</span><span class="sxs-lookup"><span data-stu-id="ecac2-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="ecac2-168">Para este tutorial, escreva **U** toobring uma lista de imagens Ubuntu e selecione **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="ecac2-169">Para **iniciar método**, selecione **SSH**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="ecac2-170">Script de Olá abaixo de copiar e colar Olá **Init script** campo.</span><span class="sxs-lookup"><span data-stu-id="ecac2-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="ecac2-171">Olá **Init script** será executado após Olá é criada a VM.</span><span class="sxs-lookup"><span data-stu-id="ecac2-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="ecac2-172">Neste exemplo, o script de Olá instala Java, o git e ant.</span><span class="sxs-lookup"><span data-stu-id="ecac2-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="ecac2-173">No Olá **Username** e **palavra-passe** campos, introduza os valores preferidos para a conta de administrador de Olá que será criada na sua VM.</span><span class="sxs-lookup"><span data-stu-id="ecac2-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="ecac2-174">Clique em **verificar modelo** toocheck se Olá que foram especificados parâmetros são válidos.</span><span class="sxs-lookup"><span data-stu-id="ecac2-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="ecac2-175">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="ecac2-176">Criar uma tarefa de Hudson que é executada num nó subordinado no Azure</span><span class="sxs-lookup"><span data-stu-id="ecac2-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="ecac2-177">Nesta secção, irá criar uma tarefa de Hudson que será executada num nó subordinado no Azure.</span><span class="sxs-lookup"><span data-stu-id="ecac2-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="ecac2-178">No dashboard de Hudson Olá, clique em **nova tarefa**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="ecac2-179">Introduza um nome para a tarefa de Olá que estiver a criar.</span><span class="sxs-lookup"><span data-stu-id="ecac2-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="ecac2-180">Para o tipo de tarefa Olá, selecione **criar uma tarefa de estilo livre software**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="ecac2-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-181">Click **OK**.</span></span>
5. <span data-ttu-id="ecac2-182">Na página de configuração da tarefa de Olá, selecione **restringir onde é possível executar este projeto**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="ecac2-183">Selecione **menu nó e a etiqueta** e selecione **linux** (especificamos esta etiqueta ao criar o modelo de máquina virtual de Olá na secção anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="ecac2-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="ecac2-184">No Olá **criar** secção, clique em **Adicionar passo de compilação** e selecione **executar shell**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="ecac2-185">Editar Olá script a seguir, substituindo **{github nome da sua conta}**, **{no nome do projeto}**, e **{diretório do seu projeto}** com adequado valores e cole Olá Editar o script na área de texto de Olá que aparece.</span><span class="sxs-lookup"><span data-stu-id="ecac2-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="ecac2-186">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecac2-186">Click on **Save**.</span></span>
10. <span data-ttu-id="ecac2-187">No Hudson dashboard de Olá, localize a tarefa de Olá que acabou de criar e clique em Olá **agendar uma compilação** ícone.</span><span class="sxs-lookup"><span data-stu-id="ecac2-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="ecac2-188">Hudson, em seguida, irá criar um nó subordinado com o modelo de Olá que criou na secção anterior Olá e executar o script de Olá que especificou no passo de compilação de Olá para esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="ecac2-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecac2-189">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="ecac2-189">Next Steps</span></span>
<span data-ttu-id="ecac2-190">Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="ecac2-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/
[perfil subscrição]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

