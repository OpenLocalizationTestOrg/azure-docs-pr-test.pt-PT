---
title: aaaHPC pacote do cluster com o Azure Active Directory | Microsoft Docs
description: Saiba como toointegrate um 2016 de pacote HPC cluster no Azure com o Azure Active Directory
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="c4bf2-103">Gerir um cluster HPC Pack no Azure utilizando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4bf2-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="c4bf2-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) suporta a integração com [do Azure Active Directory](../../active-directory/index.md) (Azure AD) para os administradores que implementar um cluster HPC Pack no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="c4bf2-105">Siga os passos de Olá neste artigo para Olá seguintes tarefas de nível elevadas:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="c4bf2-106">Integrar manualmente o seu cluster HPC Pack com o seu inquilino do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4bf2-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="c4bf2-107">Gerir e agendar tarefas no seu cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="c4bf2-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="c4bf2-108">Integrar uma solução de cluster HPC Pack com o Azure AD segue o padrão de passos toointegrate outras aplicações e serviços.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="c4bf2-109">Este artigo pressupõe que está familiarizado com a gestão de utilizador básico no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="c4bf2-110">Para obter mais informações e em segundo plano, consulte Olá [documentação do Azure Active Directory](../../active-directory/index.md) e Olá secção a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="c4bf2-111">Vantagens da integração</span><span class="sxs-lookup"><span data-stu-id="c4bf2-111">Benefits of integration</span></span>


<span data-ttu-id="c4bf2-112">Azure Active Directory (Azure AD) é um multi-inquilino baseado na nuvem diretório e identidade do serviço de gestão que fornece acesso de início de sessão único (SSO) toocloud soluções.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="c4bf2-113">Integração de um cluster HPC Pack com o Azure AD pode ajudar a alcançar Olá os seguintes objetivos:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="c4bf2-114">Remova o controlador de domínio do Active Directory tradicional Olá do cluster HPC Pack de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="c4bf2-115">Isto pode ajudar a reduzir os custos de Olá de manutenção cluster Olá se isto não é necessário para o seu negócio e o processo de implementação de Olá speed-up dos.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="c4bf2-116">Tirar partido das Olá seguintes vantagens que são colocadas pelo Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="c4bf2-117">Início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c4bf2-117">Single sign-on</span></span> 
    *   <span data-ttu-id="c4bf2-118">Utilizar uma identidade de AD local para o cluster HPC Pack de Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="c4bf2-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Ambiente do Active Directory do Azure](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="c4bf2-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4bf2-120">Prerequisites</span></span>
* <span data-ttu-id="c4bf2-121">**Cluster HPC Pack 2016 implementado em máquinas virtuais do Azure** – para obter os passos, consulte [implementar um cluster HPC Pack 2016 no Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="c4bf2-122">Precisará de nome DNS de Olá do nó principal Olá e Olá as credenciais de um administrador de cluster para concluir os passos de Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c4bf2-123">Integração do Active Directory do Azure não é suportada em versões do pacote HPC antes do HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="c4bf2-124">**Computador cliente** -precisa de um Windows ou Windows Server cliente computador demasiado executa HPC Pack cliente utilitários.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="c4bf2-125">Se pretender que apenas portal web do toouse Olá HPC Pack ou as tarefas de toosubmit de REST API, pode utilizar qualquer computador cliente à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="c4bf2-126">**Utilitários de cliente de HPC Pack** -instalar utilitários de cliente de HPC Pack Olá no computador de cliente Olá, utilizando o pacote de instalação livre Olá disponível a partir do Olá Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="c4bf2-127">Passo 1: Registar o servidor de cluster HPC Olá inquilino do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4bf2-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="c4bf2-128">Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c4bf2-129">Clique em **do Active Directory** no Olá menu à esquerda e, em seguida, clique em Olá diretório pretendido na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="c4bf2-130">Tem de ter recursos de tooaccess permissão no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="c4bf2-131">Clique em **utilizadores**e certifique-se de que existem utilizador contas já criados ou configurado.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="c4bf2-132">Clique em **aplicações** > **adicionar**e, em seguida, clique em **adicionar uma aplicação que a minha organização está a desenvolver**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="c4bf2-133">Introduza Olá informações no Assistente de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="c4bf2-134">**Nome** -HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="c4bf2-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="c4bf2-135">**Tipo** - selecione **aplicação e/ou Web API Web**</span><span class="sxs-lookup"><span data-stu-id="c4bf2-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="c4bf2-136">**Início de sessão URL**- hello base de URL para o exemplo Olá, que está por predefinição`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="c4bf2-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="c4bf2-137">**URI de ID de aplicação** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="c4bf2-138">Substitua `<Directory_name`> com o nome completo do seu inquilino do Azure AD, por exemplo, Olá `hpclocal.onmicrosoft.com`e substitua `<application_name>` com o nome de Olá que selecionou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="c4bf2-139">Depois de é adicionada a aplicação Olá, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="c4bf2-140">Configure Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="c4bf2-141">Selecione **Sim** para **aplicação é a multi-inquilino**</span><span class="sxs-lookup"><span data-stu-id="c4bf2-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="c4bf2-142">Selecione **Sim** para **utilizador atribuição tooaccess necessário aplicação**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="c4bf2-143">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-143">Click **Save**.</span></span> <span data-ttu-id="c4bf2-144">Quando terminar de guardar, clique em **gerir manifesto**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="c4bf2-145">Esta ação transfere ficheiros de notation (JSON) de objeto da aplicação manifesto JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="c4bf2-146">Edite o manifesto de Olá transferido através da localização Olá `appRoles` definição e adicionar Olá seguir a função de aplicação:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="c4bf2-147">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-147">Save hello file.</span></span> <span data-ttu-id="c4bf2-148">Em seguida, no portal de Olá, clique em **gerir manifesto** > **carregar manifesto**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="c4bf2-149">Em seguida, pode carregar o manifesto editado Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="c4bf2-150">Clique em **utilizadores**, selecione um utilizador e, em seguida, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="c4bf2-151">Atribua um Olá funções disponíveis (HpcUsers ou HpcAdminMirror) toohello utilizador.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="c4bf2-152">Repita este passo com outros utilizadores no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="c4bf2-153">Para obter informações gerais sobre os utilizadores de cluster, consulte [gerir utilizadores do Cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="c4bf2-154">utilizadores toomanage, é recomendável utilizar o painel de pré-visualização do Azure Active Directory Olá no Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="c4bf2-155">Passo 2: Registar o cliente de cluster HPC de Olá inquilino do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4bf2-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="c4bf2-156">Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c4bf2-157">Clique em **do Active Directory** no Olá menu à esquerda e, em seguida, clique em Olá diretório pretendido na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="c4bf2-158">Tem de ter recursos de tooaccess permissão no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="c4bf2-159">Clique em **aplicações** > **adicionar**e, em seguida, clique em **adicionar uma aplicação que a minha organização está a desenvolver**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="c4bf2-160">Introduza Olá informações no Assistente de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="c4bf2-161">**Nome** -HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="c4bf2-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="c4bf2-162">**Tipo** - selecione **aplicação cliente nativa**</span><span class="sxs-lookup"><span data-stu-id="c4bf2-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="c4bf2-163">**URI de redirecionamento** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="c4bf2-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="c4bf2-164">Depois de é adicionada a aplicação Olá, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="c4bf2-165">Olá cópia **ID de cliente** valor e guarde-o.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="c4bf2-166">Poderá precisa deste mais tarde quando configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="c4bf2-167">No **aplicações de tooother permissões**, clique em **Adicionar aplicação**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="c4bf2-168">Procurar e adicionar Olá HpcPackClusterServer aplicação (criada no passo 1).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="c4bf2-169">No Olá **permissões delegadas** lista pendente, selecione **acesso HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="c4bf2-170">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="c4bf2-171">Passo 3: Configurar o cluster HPC de Olá</span><span class="sxs-lookup"><span data-stu-id="c4bf2-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="c4bf2-172">Ligar toohello HPC Pack 2016 nó principal no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="c4bf2-173">Inicie o HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="c4bf2-174">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="c4bf2-175">onde</span><span class="sxs-lookup"><span data-stu-id="c4bf2-175">where</span></span>

    * <span data-ttu-id="c4bf2-176">`AADTenant`Especifica o nome de inquilino do Azure AD de Olá, tais como`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="c4bf2-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="c4bf2-177">`AADClientAppId`Especifica o ID de cliente de Olá da aplicação Olá criada no passo 2.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="c4bf2-178">Reinicie o serviço de HpcSchedulerStateful Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="c4bf2-179">Num cluster com vários nós principais, pode executar os seguintes comandos do PowerShell no Olá nó principal tooswitch Olá réplica primária para o serviço de HpcSchedulerStateful Olá de Olá:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="c4bf2-180">Passo 4: Gerir e submeter as tarefas de cliente de Olá</span><span class="sxs-lookup"><span data-stu-id="c4bf2-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="c4bf2-181">utilitários de cliente do tooinstall Olá HPC Pack no seu computador, transferir os ficheiros de configuração de HPC Pack 2016 (instalação completa) da Olá Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="c4bf2-182">Quando iniciar a instalação de Olá, escolha a opção de configuração de Olá para Olá **utilitários de cliente de HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="c4bf2-183">computador de cliente do tooprepare Olá, instale o certificado de Olá utilizado durante [a configuração de cluster HPC](hpcpack-2016-cluster.md) no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="c4bf2-184">Utilizar o Windows padrão de certificado gestão procedimentos tooinstall Olá certificado público toohello **certificados-utilizador atual** > **autoridades de certificação de raiz fidedigna** armazenar.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="c4bf2-185">Pode agora executar comandos de HPC Pack Olá ou utilizar toosubmit Olá GUI do Gestor de tarefa do pacote HPC e gerir tarefas de cluster utilizando a conta de Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="c4bf2-186">Para opções de submissão da tarefa, consulte [cluster HPC submeter tarefas tooan pacote HPC no Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="c4bf2-187">Quando tenta tooconnect toohello HPC Pack cluster do Azure para Olá pela primeira vez, é apresentada uma janela de pop-up.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="c4bf2-188">Introduza o seu toolog de credenciais do Azure AD no.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="c4bf2-189">token de Olá, em seguida, é colocado em cache.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-189">hello token is then cached.</span></span> <span data-ttu-id="c4bf2-190">Cluster de toohello ligações posterior na utilização do Azure Olá colocadas em cache token, a menos que as alterações de autenticação ou Olá em cache está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="c4bf2-191">Por exemplo, depois de concluir os passos anteriores Olá, pode consultar as tarefas a partir de um cliente no local da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="c4bf2-192">Cmdlets útil para submissão da tarefa com a integração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4bf2-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="c4bf2-193">Gerir a cache de token local Olá</span><span class="sxs-lookup"><span data-stu-id="c4bf2-193">Manage hello local token cache</span></span>

<span data-ttu-id="c4bf2-194">HPC Pack 2016 fornece dois novos cmdlets do HPC PowerShell cache de token toomanage Olá local.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="c4bf2-195">Estes cmdlets são úteis para submeter tarefas de forma não interativa.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="c4bf2-196">Consulte o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="c4bf2-197">Defina credenciais de Olá para submeter tarefas utilizando a conta de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4bf2-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="c4bf2-198">Por vezes, poderá ser útil tarefa de Olá toorun em utilizador de cluster HPC de Olá (para um cluster HPC associados a um domínio, executar como utilizador de domínio; para um cluster HPC não associados ao domínio, executado como um utilizador local no nó principal Olá).</span><span class="sxs-lookup"><span data-stu-id="c4bf2-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="c4bf2-199">Utilize Olá seguintes credenciais de Olá tooset de comandos:</span><span class="sxs-lookup"><span data-stu-id="c4bf2-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="c4bf2-200">Em seguida, submeta tarefa Olá da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-200">Then submit hello job as follows.</span></span> <span data-ttu-id="c4bf2-201">Olá tarefa é executada em $localUser em nós de computação Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="c4bf2-202">Se `–Credential` não for especificado com `Submit-HpcJob`, Olá trabalho ou tarefa é executado sob um utilizador local mapeado como Olá conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="c4bf2-203">(cluster HPC de Olá cria um utilizador local com o mesmo nome como Olá tarefas do Azure AD conta toorun Olá de Olá.)</span><span class="sxs-lookup"><span data-stu-id="c4bf2-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="c4bf2-204">Definir os dados expandidos para Olá conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="c4bf2-205">Isto é útil quando em execução uma tarefa MPI em nós de Linux utilizando a conta de Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4bf2-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="c4bf2-206">Definir os dados expandidos para Olá conta do Azure AD próprio</span><span class="sxs-lookup"><span data-stu-id="c4bf2-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="c4bf2-207">Definir os dados expandidos e executadas como utilizador de cluster HPC</span><span class="sxs-lookup"><span data-stu-id="c4bf2-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

