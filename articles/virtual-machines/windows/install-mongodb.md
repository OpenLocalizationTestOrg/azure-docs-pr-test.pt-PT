---
title: aaaInstall MongoDB numa VM do Windows no Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB numa VM do Azure com o Windows Server 2012 R2 criados com o modelo de implementação do Resource Manager Olá."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="f5c5e-103">Instalar e configurar o MongoDB uma VM do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="f5c5e-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="f5c5e-104">[MongoDB](http://www.mongodb.org) é um popular open source e de elevado desempenho base de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="f5c5e-105">Este artigo irá orientá-lo a instalar e configurar o MongoDB numa máquina virtual (VM) do Windows Server 2012 R2 no Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="f5c5e-106">Também pode [instalar MongoDB numa VM com Linux no Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5c5e-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f5c5e-107">Prerequisites</span></span>
<span data-ttu-id="f5c5e-108">Antes de instalar e configurar o MongoDB, necessário toocreate uma VM e, idealmente, adicione um tooit de disco de dados.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="f5c5e-109">Consulte os seguintes artigos toocreate uma VM de Olá e adicione um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="f5c5e-110">Criar uma VM do Windows Server utilizando [Olá portal do Azure](quick-create-portal.md) ou [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="f5c5e-111">Anexar um dados disco tooa VM do Windows Server utilizando [Olá portal do Azure](attach-managed-disk-portal.md) ou [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="f5c5e-112">toobegin instalar e configurar o MongoDB, [iniciar sessão tooyour VM do Windows Server](connect-logon.md) utilizando o ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="f5c5e-113">Instalar MongoDB</span><span class="sxs-lookup"><span data-stu-id="f5c5e-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5c5e-114">Funcionalidades de segurança do MongoDB, como a autenticação e o enlace de endereço IP, não estão ativadas por predefinição.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="f5c5e-115">Funcionalidades de segurança devem ser ativadas antes de implementar o ambiente de produção do MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="f5c5e-116">Para obter mais informações, consulte [autenticação e de segurança do MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="f5c5e-117">Depois de se ligar tooyour VM utilizando o ambiente de trabalho remoto, abra o Internet Explorer de Olá **iniciar** menu Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="f5c5e-118">Selecione **utilizar definições de segurança, privacidade e compatibilidade recomendadas** quando o Internet Explorer primeiro abre e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="f5c5e-119">Configuração de segurança avançada do Internet Explorer está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="f5c5e-120">Adicione a lista de toohello do Olá MongoDB Web site de sites autorizados:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="f5c5e-121">Selecione Olá **ferramentas** ícone no canto superior direito de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="f5c5e-122">No **opções da Internet**, selecione Olá **segurança** separador e, em seguida, selecione Olá **Sites fidedignos** ícone.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="f5c5e-123">Clique em Olá **Sites** botão.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-123">Click hello **Sites** button.</span></span> <span data-ttu-id="f5c5e-124">Adicionar *https://\*. mongodb.org* toohello lista de sites fidedignos e a caixa de diálogo Olá, em seguida, feche.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Configurar definições de segurança do Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="f5c5e-126">Procurar toohello [MongoDB - transfere](http://www.mongodb.org/downloads) página (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="f5c5e-127">Se necessário, selecione Olá **Comunidade servidor** edition e, em seguida, selecione de Olá mais recente estável versão atual para o Windows Server 2008 R2 de 64 bits e posterior.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="f5c5e-128">toodownload Olá instalador, clique em **transferências (msi)**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Transferir o instalador do MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="f5c5e-130">Execute o instalador do Olá depois de concluída a transferência de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="f5c5e-131">Ler e aceitar o contrato de licença de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="f5c5e-132">Quando lhe for pedido, selecione **concluída** instalar.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="f5c5e-133">No ecrã final Olá, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="f5c5e-134">Configurar Olá VM e MongoDB</span><span class="sxs-lookup"><span data-stu-id="f5c5e-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="f5c5e-135">as variáveis de caminho Olá não são atualizadas pelo programa de instalação do Olá MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="f5c5e-136">Sem Olá MongoDB `bin` localização na sua variável de caminho, terá de caminho completo do toospecify Olá sempre que utilizar um executável do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="f5c5e-137">variável de caminho do tooadd Olá localização tooyour:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="f5c5e-138">Contexto Olá **iniciar** menu e selecione **sistema**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="f5c5e-139">Clique em **definições de sistema avançadas**e, em seguida, clique em **variáveis de ambiente**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="f5c5e-140">Em **variáveis do sistema**, selecione **caminho**e, em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurar variáveis de caminho](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="f5c5e-142">Adicionar Olá caminho tooyour MongoDB `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="f5c5e-143">MongoDB é normalmente instalado na *c:\Programas\Microsoft Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="f5c5e-144">Verifique o caminho de instalação de Olá no VM.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="f5c5e-145">Olá exemplo seguinte adiciona toohello de localização de instalação do Olá predefinido MongoDB `PATH` variável:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="f5c5e-146">Ser se tooadd Olá à esquerda ponto e vírgula (`;`) tooindicate que estiver a adicionar um tooyour localização `PATH` variável.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="f5c5e-147">Crie diretórios de dados e de registo do MongoDB no seu disco de dados.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="f5c5e-148">De Olá **iniciar** menu, selecione **linha de comandos**.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="f5c5e-149">os seguintes exemplos de Olá criar diretórios Olá no disco f:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="f5c5e-150">Iniciar uma instância do MongoDB com Olá comando a seguir, ajuste os dados de tooyour Olá caminho e inicie diretórios em conformidade:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="f5c5e-151">Pode demorar alguns minutos para MongoDB tooallocate ficheiros do diário Olá e começar a escutar ligações.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="f5c5e-152">Todas as mensagens de registo são direcionado toohello *F:\MongoLogs\mongolog.log* ficheiro como `mongod.exe` servidor é iniciado e atribui ficheiros do diário.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f5c5e-153">linha de comandos Olá permanece direcionada para esta tarefa enquanto a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="f5c5e-154">Deixe Olá linha de comandos janela abra toocontinue com MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="f5c5e-155">Em alternativa, instale o MongoDB como serviço, conforme detalhado no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="f5c5e-156">Para uma experiência mais robusta do MongoDB, instalar Olá `mongod.exe` como um serviço.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="f5c5e-157">Criação de um serviço significa que não precisa de tooleave numa linha de comandos executar sempre que quiser toouse MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="f5c5e-158">Crie serviço Olá forma, ajustar Olá caminho tooyour dados e registo de diretórios em conformidade:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="f5c5e-159">Olá comando anterior cria um serviço com o nome MongoDB, com uma descrição do "BD de Mongo".</span><span class="sxs-lookup"><span data-stu-id="f5c5e-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="f5c5e-160">também está especificado Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="f5c5e-161">Olá `--dbpath` opção especifica a localização de Olá do diretório de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="f5c5e-162">Olá `--logpath` opção tem de ser toospecify utilizado um ficheiro de registo, porque o serviço em execução Olá não tem uma saída de toodisplay de janela de comando.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="f5c5e-163">Olá `--logappend` opção especifica que um reinício do serviço de Olá provoca o ficheiro de registo saída tooappend toohello existente.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="f5c5e-164">toostart Olá MongoDB serviço, executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="f5c5e-165">Para obter mais informações sobre como criar o serviço de MongoDB Olá, consulte [configurar um serviço do Windows para o MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="f5c5e-166">Instância do MongoDB de Olá de teste</span><span class="sxs-lookup"><span data-stu-id="f5c5e-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="f5c5e-167">Com o MongoDB em execução como uma única instância ou instalado como um serviço, pode agora começar a criar e utilizar as bases de dados.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="f5c5e-168">Olá toostart shell administrativa do MongoDB, abrir outra janela de linha de comandos de Olá **iniciar** menu e introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="f5c5e-169">Pode listar as bases de dados de Olá com Olá `db` comando.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="f5c5e-170">Insira alguns dados da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="f5c5e-171">Procure dados da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="f5c5e-172">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="f5c5e-173">Olá saída `mongo` consola da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="f5c5e-174">Configurar regras de grupo de segurança de rede e de firewall</span><span class="sxs-lookup"><span data-stu-id="f5c5e-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="f5c5e-175">Agora que MongoDB está instalado e em execução, abra uma porta na Firewall do Windows, pelo que pode ligar remotamente tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="f5c5e-176">toocreate uma nova regra de entrada tooallow a porta TCP 27017, abra uma linha de comandos administrativa do PowerShell e introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f5c5e-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="f5c5e-177">Também pode criar regra de Olá utilizando Olá **Firewall do Windows com segurança avançada** ferramenta de gestão gráficas.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="f5c5e-178">Crie uma nova regra de entrada tooallow a porta TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="f5c5e-179">Se necessário, crie um grupo de segurança de rede regra tooallow acesso tooMongoDB de fora da sub-rede de rede virtual do Azure existente Olá.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="f5c5e-180">Olá pode criar regras do grupo de segurança de rede utilizando Olá [portal do Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="f5c5e-181">Tal como acontece com as regras de Firewall do Windows hello, permita a interface de rede virtual do TCP porta 27017 toohello da sua VM do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="f5c5e-182">A porta TCP 27017 é Olá predefinido porta é utilizada por MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="f5c5e-183">Pode alterar esta porta utilizando Olá `--port` parâmetro ao iniciar `mongod.exe` manualmente ou a partir de um serviço.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="f5c5e-184">Se alterar a porta de Olá, certifique-se tooupdate Olá Firewall do Windows e o grupo de segurança de rede regras no Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f5c5e-185">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f5c5e-185">Next steps</span></span>
<span data-ttu-id="f5c5e-186">Neste tutorial, aprendeu como tooinstall e configurar o MongoDB na sua VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="f5c5e-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="f5c5e-187">Pode agora aceder MongoDB na sua VM do Windows, por seguir Olá avançadas tópicos Olá [documentação do MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="f5c5e-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

