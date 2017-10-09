---
title: aaaConnect tooSQL base de dados utilizando o SQL Server Management Studio no Azure RemoteApp | Microsoft Docs
description: "Utilize este tutorial toolearn como toouse SQL Server Management Studio no Azure RemoteApp para segurança e desempenho ao ligar tooSQL da base de dados"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="20904-103">Utilizar o SQL Server Management Studio no Azure RemoteApp tooconnect tooSQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="20904-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20904-104">O Azure RemoteApp está a ser descontinuado.</span><span class="sxs-lookup"><span data-stu-id="20904-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="20904-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="20904-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="20904-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="20904-106">Introduction</span></span>
<span data-ttu-id="20904-107">Este tutorial mostra como toouse SQL Server Management Studio (SSMS) no Azure RemoteApp tooconnect tooSQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="20904-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="20904-108">Orienta Olá processo de configuração de SQL Server Management Studio no Azure RemoteApp, explica as vantagens de Olá e mostra as funcionalidades de segurança que pode utilizar no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="20904-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="20904-109">**Estimado tempo toocomplete:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="20904-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="20904-110">SSMS no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="20904-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="20904-111">O Azure RemoteApp é um serviço RDS no Azure que fornece as aplicações.</span><span class="sxs-lookup"><span data-stu-id="20904-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="20904-112">Pode saber mais acerca do mesmo aqui: [que é o RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="20904-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="20904-113">SSMS em execução no Azure RemoteApp fornecem Olá a mesma experiência como executar localmente o SSMS.</span><span class="sxs-lookup"><span data-stu-id="20904-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Captura de ecrã com SSMS em execução no Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="20904-115">Benefícios</span><span class="sxs-lookup"><span data-stu-id="20904-115">Benefits</span></span>
<span data-ttu-id="20904-116">Existem muitas vantagens toousing SSMS no Azure RemoteApp, incluindo:</span><span class="sxs-lookup"><span data-stu-id="20904-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="20904-117">A porta 1433 no Azure SQL server não tem toobe exposto externamente (fora do Azure).</span><span class="sxs-lookup"><span data-stu-id="20904-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="20904-118">Tookeep sem necessidade de adicionar e remover endereços IP na firewall do servidor de SQL do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="20904-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="20904-119">Todas as ligações do Azure RemoteApp ocorrem através de HTTPS utilizando a porta 443 encriptados protocolo de ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="20904-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="20904-120">É multiutilizador e pode dimensionar.</span><span class="sxs-lookup"><span data-stu-id="20904-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="20904-121">Há um ganhos de desempenho de ter o SSMS no Olá mesma região que Olá base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="20904-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="20904-122">Pode auditar a utilização do Azure RemoteApp com a edição de Premium Olá do Azure Active Directory que tem os relatórios de atividade do utilizador.</span><span class="sxs-lookup"><span data-stu-id="20904-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="20904-123">Pode ativar a autenticação multifator (MFA).</span><span class="sxs-lookup"><span data-stu-id="20904-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="20904-124">O acesso SSMS em qualquer local quando utilizar qualquer um dos Olá suportado clientes do Azure RemoteApp que inclui o iOS, Android, Mac, Windows Phone e PCs Windows.</span><span class="sxs-lookup"><span data-stu-id="20904-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="20904-125">Criar coleção do Olá do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="20904-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="20904-126">Seguem-se Olá passos toocreate a coleção do RemoteApp do Azure com o SSMS:</span><span class="sxs-lookup"><span data-stu-id="20904-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="20904-127">1. Criar uma nova VM do Windows da imagem</span><span class="sxs-lookup"><span data-stu-id="20904-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="20904-128">Utilize Olá "Windows Server remoto ambiente de trabalho sessão anfitrião Windows Server 2012 R2" de imagem de Olá Galeria toomake a nova VM.</span><span class="sxs-lookup"><span data-stu-id="20904-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="20904-129">2. Instalar o SSMS do SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="20904-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="20904-130">Vá para Olá nova VM e navegue até a página de transferência toothis: [rápida do Microsoft® SQL Server® 2014](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="20904-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="20904-131">Há uma transferência de tooonly opção SSMS.</span><span class="sxs-lookup"><span data-stu-id="20904-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="20904-132">Após a transferência, vá para o diretório de instalação de Olá e execute a configuração tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="20904-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="20904-133">Também precisa de tooinstall SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="20904-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="20904-134">Poderá transferi-lo aqui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="20904-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="20904-135">SQL Server 2014 Service Pack 1 inclui uma funcionalidade essencial para trabalhar com a SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="20904-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="20904-136">3. Executar script de validar e Sysprep</span><span class="sxs-lookup"><span data-stu-id="20904-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="20904-137">No Olá ambiente de trabalho de Olá VM é um script de PowerShell chamado validar.</span><span class="sxs-lookup"><span data-stu-id="20904-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="20904-138">Execute este fazendo duplo clique em.</span><span class="sxs-lookup"><span data-stu-id="20904-138">Run this by double-clicking.</span></span> <span data-ttu-id="20904-139">Irá verificar que esse Olá VM está pronto toobe utilizada para alojar remoto de aplicações.</span><span class="sxs-lookup"><span data-stu-id="20904-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="20904-140">Quando a verificação estiver concluída, pedirá toorun sysprep - escolha toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="20904-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="20904-141">Quando o sysprep estiver concluída, será encerrado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="20904-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="20904-142">toolearn mais sobre a criação de uma imagem do Azure RemoteApp, consulte: [como toocreate um modelo do RemoteApp imagem no Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="20904-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="20904-143">4. Captura de imagem</span><span class="sxs-lookup"><span data-stu-id="20904-143">4. Capture image</span></span>
<span data-ttu-id="20904-144">Quando Olá VM parou de funcionar, encontrá-lo no portal atual Olá e capturá-la.</span><span class="sxs-lookup"><span data-stu-id="20904-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="20904-145">toolearn mais informações sobre a capturar uma imagem do utilizador, consulte [capturar uma imagem de uma máquina virtual de Azure Windows criada com o modelo de implementação clássica Olá](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="20904-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="20904-146">5. Adicionar imagens de modelo do RemoteApp tooAzure</span><span class="sxs-lookup"><span data-stu-id="20904-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="20904-147">No Azure RemoteApp secção portal atual Olá Olá, aceda a toohello separador de imagens de modelo e clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="20904-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="20904-148">Na caixa de pop-up Olá, selecione "Importar uma imagem a partir da sua biblioteca de máquinas virtuais" e, em seguida, escolha Olá imagem que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="20904-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="20904-149">6. Criar a coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="20904-149">6. Create cloud collection</span></span>
<span data-ttu-id="20904-150">No portal atual Olá, crie uma nova coleção de nuvem do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="20904-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="20904-151">Escolha Olá imagem de modelo que acabou de importar com o SSMS instalado no mesmo.</span><span class="sxs-lookup"><span data-stu-id="20904-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Criar nova coleção na nuvem][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="20904-153">7. Publicar SSMS</span><span class="sxs-lookup"><span data-stu-id="20904-153">7. Publish SSMS</span></span>
<span data-ttu-id="20904-154">No Olá publicação separador da sua nova coleção de nuvem, selecione de publicar uma aplicação Olá Menu Iniciar e, em seguida, escolha SSMS Olá lista.</span><span class="sxs-lookup"><span data-stu-id="20904-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Publicar aplicações][5]

### <a name="8-add-users"></a><span data-ttu-id="20904-156">8. Adicionar utilizadores</span><span class="sxs-lookup"><span data-stu-id="20904-156">8. Add users</span></span>
<span data-ttu-id="20904-157">No separador de acesso de utilizador de Olá pode selecionar os utilizadores de Olá que terão acesso toothis Azure RemoteApp coleção que inclui apenas o SSMS.</span><span class="sxs-lookup"><span data-stu-id="20904-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Adicionar Utilizador][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="20904-159">9. Instalar a aplicação de cliente do Azure RemoteApp Olá</span><span class="sxs-lookup"><span data-stu-id="20904-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="20904-160">Pode transferir e instalar um cliente do Azure RemoteApp aqui: [transferir | O Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="20904-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="20904-161">Configurar o servidor SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="20904-161">Configure Azure SQL server</span></span>
<span data-ttu-id="20904-162">Olá apenas configuração necessária é tooensure serviços do Azure está ativada para firewall de Olá.</span><span class="sxs-lookup"><span data-stu-id="20904-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="20904-163">Se utilizar esta solução, em seguida, não terá tooadd qualquer IP endereços tooopen Olá firewall.</span><span class="sxs-lookup"><span data-stu-id="20904-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="20904-164">tráfego de rede de Olá permitido toohello do SQL Server é a partir de outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="20904-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Permitir do Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="20904-166">Autenticação Multifator (MFA)</span><span class="sxs-lookup"><span data-stu-id="20904-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="20904-167">MFA pode ser ativado especificamente para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="20904-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="20904-168">Aceda toohello separador de aplicações do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="20904-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="20904-169">Irá encontrar uma entrada para o Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="20904-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="20904-170">Se clique essa aplicação e, em seguida, configurar, será apresentada a página de Olá abaixo onde pode ativar a MFA para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="20904-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Ativar a MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="20904-172">Auditoria de atividade do utilizador com o Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="20904-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="20904-173">Se não tiver do Azure AD Premium e, em seguida, tiver tooturn-lo na Olá secção de licenças do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="20904-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="20904-174">Com o Premium ativado, pode atribuir utilizadores ao nível do toohello Premium.</span><span class="sxs-lookup"><span data-stu-id="20904-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="20904-175">Quando acede tooa utilizador no Azure Active Directory, em seguida, pode aceder toohello atividade separador toosee início de sessão informações tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="20904-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20904-176">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="20904-176">Next steps</span></span>
<span data-ttu-id="20904-177">Depois de concluir todos os Olá os passos acima, que será capaz de toorun Olá Azure RemoteApp cliente e iniciar sessão com um utilizador atribuído.</span><span class="sxs-lookup"><span data-stu-id="20904-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="20904-178">Será apresentada com o SSMS como uma das suas aplicações e pode executá-lo, tal como faria se foi instalado no seu computador com o SQL server tooAzure acesso.</span><span class="sxs-lookup"><span data-stu-id="20904-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="20904-179">Para obter mais informações sobre como toomake Olá tooSQL de ligação da base de dados, consulte [ligar tooSQL da base de dados com o SQL Server Management Studio e executar uma consulta de T-SQL de exemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="20904-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="20904-180">Tudo o que é por agora.</span><span class="sxs-lookup"><span data-stu-id="20904-180">That's everything for now.</span></span> <span data-ttu-id="20904-181">Divirta-se!</span><span class="sxs-lookup"><span data-stu-id="20904-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png