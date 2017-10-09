# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="78f69-101">Perguntas mais frequentes sobre os discos de VM do IaaS do Azure e os discos premium geridas e não geridas</span><span class="sxs-lookup"><span data-stu-id="78f69-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="78f69-102">Este artigo responde a algumas perguntas mais frequentes sobre discos gerida do Azure e o Premium Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="78f69-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="78f69-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="78f69-103">Managed Disks</span></span>

<span data-ttu-id="78f69-104">**O que é discos gerida do Azure?**</span><span class="sxs-lookup"><span data-stu-id="78f69-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="78f69-105">Discos geridos é uma funcionalidade que simplifica a gestão de discos para VMs IaaS do Azure, processando gestão de contas de armazenamento para si.</span><span class="sxs-lookup"><span data-stu-id="78f69-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="78f69-106">Para obter mais informações, consulte Olá [descrição geral de discos geridos](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78f69-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="78f69-107">**Se criar um disco gerido standard de um VHD existente que é 80 GB, quanto será que custo-me?**</span><span class="sxs-lookup"><span data-stu-id="78f69-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="78f69-108">Um disco gerido standard criado a partir de um VHD de 80 GB é tratado como o tamanho de disco padrão disponível seguinte Olá, que é um disco de S10.</span><span class="sxs-lookup"><span data-stu-id="78f69-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="78f69-109">Está a cobrada de acordo com toohello S10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="78f69-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="78f69-110">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="78f69-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="78f69-111">**Existem quaisquer custos de transação para discos geridos padrão?**</span><span class="sxs-lookup"><span data-stu-id="78f69-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="78f69-112">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-112">Yes.</span></span> <span data-ttu-id="78f69-113">Está a cobrado para cada transação.</span><span class="sxs-lookup"><span data-stu-id="78f69-113">You're charged for each transaction.</span></span> <span data-ttu-id="78f69-114">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="78f69-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="78f69-115">**Para um disco gerido standard, será posso cobrado para o tamanho real do Olá dos dados de Olá no disco Olá ou para a capacidade de Olá aprovisionado de disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="78f69-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="78f69-116">Está a cobrados com base na capacidade de Olá aprovisionado de disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="78f69-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="78f69-117">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="78f69-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="78f69-118">**Como é preços dos discos premium gerido diferente dos discos não geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="78f69-119">Olá preços dos discos premium gerido é Olá, mesmo que os discos premium não gerido.</span><span class="sxs-lookup"><span data-stu-id="78f69-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="78f69-120">**Pode alterar Olá armazenamento tipo de conta (Standard ou Premium) do meu discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="78f69-121">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-121">Yes.</span></span> <span data-ttu-id="78f69-122">Pode alterar o tipo de conta de armazenamento Olá dos seus discos geridos utilizando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="78f69-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="78f69-123">**Existe alguma forma posso pode copiar ou exportar uma conta de armazenamento privada do disco gerido tooa?**</span><span class="sxs-lookup"><span data-stu-id="78f69-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="78f69-124">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-124">Yes.</span></span> <span data-ttu-id="78f69-125">Pode exportar os discos geridos utilizando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="78f69-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="78f69-126">**Pode utilizar um ficheiro VHD num toocreate de conta de armazenamento do Azure um disco gerido com uma subscrição diferente?**</span><span class="sxs-lookup"><span data-stu-id="78f69-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="78f69-127">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-127">No.</span></span>

<span data-ttu-id="78f69-128">**Pode utilizar um ficheiro VHD num toocreate de conta de armazenamento do Azure um disco gerido numa região diferente?**</span><span class="sxs-lookup"><span data-stu-id="78f69-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="78f69-129">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-129">No.</span></span>

<span data-ttu-id="78f69-130">**Existem algumas limitações de dimensionamento para os clientes que utilizam discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="78f69-131">Discos geridos elimina os limites de Olá associados a contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="78f69-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="78f69-132">No entanto, o número de Olá de gerido discos por subscrição é limitado too2, 000 por predefinição.</span><span class="sxs-lookup"><span data-stu-id="78f69-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="78f69-133">Pode chamar suporte tooincrease este número.</span><span class="sxs-lookup"><span data-stu-id="78f69-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="78f69-134">**Pode tirar um instantâneo incremental de um disco gerido?**</span><span class="sxs-lookup"><span data-stu-id="78f69-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="78f69-135">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-135">No.</span></span> <span data-ttu-id="78f69-136">capacidade de instantâneos atual Olá faz uma cópia completa de um disco gerido.</span><span class="sxs-lookup"><span data-stu-id="78f69-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="78f69-137">No entanto, iremos estiver a planear toosupport instantâneos incrementais no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="78f69-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="78f69-138">**VMs num conjunto de disponibilidade podem consistir de uma combinação de discos geridos e?**</span><span class="sxs-lookup"><span data-stu-id="78f69-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="78f69-139">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-139">No.</span></span> <span data-ttu-id="78f69-140">Olá VMs num conjunto de disponibilidade tem de utilizar discos de todos os geridos ou todos os discos não geridos.</span><span class="sxs-lookup"><span data-stu-id="78f69-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="78f69-141">Quando criar um conjunto de disponibilidade, pode escolher o tipo de discos que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="78f69-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="78f69-142">**É a opção de predefinida de Olá de gerido discos no Olá portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="78f69-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="78f69-143">Atualmente não, mas irá tornar-se predefinição de Olá no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="78f69-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="78f69-144">**Pode criar um disco vazio gerido?**</span><span class="sxs-lookup"><span data-stu-id="78f69-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="78f69-145">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-145">Yes.</span></span> <span data-ttu-id="78f69-146">Pode criar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="78f69-146">You can create an empty disk.</span></span> <span data-ttu-id="78f69-147">Um disco gerido pode ser criado independentemente de uma VM, por exemplo, sem tooa VM a ligá-la.</span><span class="sxs-lookup"><span data-stu-id="78f69-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="78f69-148">**O que é o número de domínios de falhas de Olá suportada para um conjunto de disponibilidade que utiliza discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="78f69-149">Consoante a região de olá onde está localizado o conjunto de disponibilidade de Olá que utiliza discos geridos, o número de domínios de falhas de Olá suportado é 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="78f69-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="78f69-150">**Como é a conta de armazenamento standard Olá para configurar o diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="78f69-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="78f69-151">Configurar uma conta de armazenamento privada para diagnósticos da VM.</span><span class="sxs-lookup"><span data-stu-id="78f69-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="78f69-152">Olá futura, vamos planear tooswitch diagnóstico tooManaged discos bem.</span><span class="sxs-lookup"><span data-stu-id="78f69-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="78f69-153">**Que tipo de suporte de controlo de acesso baseado em funções está disponível para discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="78f69-154">Gerido funções do discos suporta três predefinido de chaves:</span><span class="sxs-lookup"><span data-stu-id="78f69-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="78f69-155">O proprietário: Podem gerir tudo, incluindo o acesso</span><span class="sxs-lookup"><span data-stu-id="78f69-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="78f69-156">Contribuidor: Podem gerir tudo, exceto acesso</span><span class="sxs-lookup"><span data-stu-id="78f69-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="78f69-157">Leitor: Podem ver tudo, mas não é possível efetuar alterações</span><span class="sxs-lookup"><span data-stu-id="78f69-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="78f69-158">**Existe alguma forma posso pode copiar ou exportar uma conta de armazenamento privada do disco gerido tooa?**</span><span class="sxs-lookup"><span data-stu-id="78f69-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="78f69-159">Pode obter uma assinatura de acesso partilhado só de leitura URI para Olá gerido em disco e utilizá-la toocopy Olá conteúdo tooa armazenamento privada conta local ou na armazenamento.</span><span class="sxs-lookup"><span data-stu-id="78f69-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="78f69-160">**Pode criar uma cópia do meu disco gerido?**</span><span class="sxs-lookup"><span data-stu-id="78f69-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="78f69-161">Os clientes podem tirar um instantâneo os respetivos discos geridos e, em seguida, utilizar Olá instantâneo toocreate outro disco gerido.</span><span class="sxs-lookup"><span data-stu-id="78f69-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="78f69-162">**Os discos não geridos ainda são suportados?**</span><span class="sxs-lookup"><span data-stu-id="78f69-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="78f69-163">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-163">Yes.</span></span> <span data-ttu-id="78f69-164">Suportamos discos não geridos e geridos.</span><span class="sxs-lookup"><span data-stu-id="78f69-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="78f69-165">Recomendamos que utilize discos geridos para novas cargas de trabalho e migre os discos de toomanaged cargas de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="78f69-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="78f69-166">**Se criar um disco de 128 GB e, em seguida, aumentar Olá tamanho too130 GB, será posso cobrado Olá seguinte tamanho do disco (GB de 512)?**</span><span class="sxs-lookup"><span data-stu-id="78f69-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="78f69-167">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-167">Yes.</span></span>

<span data-ttu-id="78f69-168">**Posso criar armazenamento localmente redundante, armazenamento georredundante, e discos geridos pelo armazenamento com redundância de zona?**</span><span class="sxs-lookup"><span data-stu-id="78f69-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="78f69-169">Discos gerida do Azure suporta atualmente os discos de armazenamento apenas localmente redundante gerido.</span><span class="sxs-lookup"><span data-stu-id="78f69-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="78f69-170">**Pode reduzir ou downsize meu discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="78f69-171">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-171">No.</span></span> <span data-ttu-id="78f69-172">Esta funcionalidade não é suportada atualmente.</span><span class="sxs-lookup"><span data-stu-id="78f69-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="78f69-173">**Posso alterar as propriedades de nome de computador Olá quando um especializadas (não criada utilizando a ferramenta de preparação do sistema de Olá ou generalizado) disco do sistema de operativo tooprovision utilizado uma VM?**</span><span class="sxs-lookup"><span data-stu-id="78f69-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="78f69-174">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-174">No.</span></span> <span data-ttu-id="78f69-175">Não é possível atualizar a propriedade de nome de computador Olá.</span><span class="sxs-lookup"><span data-stu-id="78f69-175">You can't update hello computer name property.</span></span> <span data-ttu-id="78f69-176">Olá nova VM herda-Olá VM principal, que era o disco do sistema operativo utilizada toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="78f69-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="78f69-177">**Onde posso encontrar exemplo do Azure Resource Manager modelos toocreate VMs com discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="78f69-178">Lista de modelos utilizando discos geridos</span><span class="sxs-lookup"><span data-stu-id="78f69-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="78f69-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="78f69-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="78f69-180">Geridos discos e a encriptação do serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="78f69-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="78f69-181">**É encriptação do serviço de armazenamento do Azure ativada por predefinição quando criar um disco gerido?**</span><span class="sxs-lookup"><span data-stu-id="78f69-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="78f69-182">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-182">Yes.</span></span>

<span data-ttu-id="78f69-183">**Quem gere as chaves de encriptação de Olá?**</span><span class="sxs-lookup"><span data-stu-id="78f69-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="78f69-184">Microsoft gere as chaves de encriptação de Olá.</span><span class="sxs-lookup"><span data-stu-id="78f69-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="78f69-185">**Pode desativar encriptação do serviço de armazenamento para os meus discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="78f69-186">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-186">No.</span></span>

<span data-ttu-id="78f69-187">**Encriptação do serviço de armazenamento só está disponível em regiões específicas?**</span><span class="sxs-lookup"><span data-stu-id="78f69-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="78f69-188">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-188">No.</span></span> <span data-ttu-id="78f69-189">Está disponível em todas as regiões de olá onde discos geridos está disponível.</span><span class="sxs-lookup"><span data-stu-id="78f69-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="78f69-190">Discos geridos está disponível em todas as regiões públicas e na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="78f69-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="78f69-191">**Como posso saber se se o meu disco gerido é encriptado?**</span><span class="sxs-lookup"><span data-stu-id="78f69-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="78f69-192">Pode encontrar tempo Olá quando um disco gerido foi criado a partir Olá portal do Azure, Olá CLI do Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78f69-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="78f69-193">Se houver tempo Olá após 9 de Junho de 2017, o disco está encriptado.</span><span class="sxs-lookup"><span data-stu-id="78f69-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="78f69-194">**Como encriptar o meu discos existentes que foram criados antes de 10 de Junho de 2017?**</span><span class="sxs-lookup"><span data-stu-id="78f69-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="78f69-195">A partir de 10 de Junho de 2017, os novos dados escritos discos tooexisting gerido é encriptados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="78f69-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="78f69-196">Podemos também estiver a planear tooencrypt de dados existente e encriptação Olá acontecerá assíncrona no fundo Olá.</span><span class="sxs-lookup"><span data-stu-id="78f69-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="78f69-197">Se tem de encriptar dados existentes agora, crie uma cópia do seu disco.</span><span class="sxs-lookup"><span data-stu-id="78f69-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="78f69-198">Novos discos serão encriptados.</span><span class="sxs-lookup"><span data-stu-id="78f69-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="78f69-199">Copiar discos geridos utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="78f69-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="78f69-200">Copiar discos geridos utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="78f69-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="78f69-201">**São gerido instantâneos e imagens encriptadas?**</span><span class="sxs-lookup"><span data-stu-id="78f69-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="78f69-202">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-202">Yes.</span></span> <span data-ttu-id="78f69-203">Gerido todos os instantâneos e as imagens criadas após 9 de Junho de 2017, são encriptadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="78f69-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="78f69-204">**Pode converter VMs com discos não geridos que estão localizados em contas de armazenamento que estão ou que foram anteriormente encriptados toomanaged discos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="78f69-205">Sim</span><span class="sxs-lookup"><span data-stu-id="78f69-205">Yes</span></span>

<span data-ttu-id="78f69-206">**Será um VHD exportado a partir de um disco gerido ou um instantâneo também será encriptado?**</span><span class="sxs-lookup"><span data-stu-id="78f69-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="78f69-207">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-207">No.</span></span> <span data-ttu-id="78f69-208">Mas se exportar uma tooan VHD encriptados conta de armazenamento de um disco gerido encriptado ou instantâneos, em seguida, são encriptado.</span><span class="sxs-lookup"><span data-stu-id="78f69-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="78f69-209">Os discos Premium: geridos e não geridas</span><span class="sxs-lookup"><span data-stu-id="78f69-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="78f69-210">**Se uma VM utiliza uma série de tamanho que suporte o Premium Storage, tais como uma série DSv2, posso anexar os discos de dados standard e premium?**</span><span class="sxs-lookup"><span data-stu-id="78f69-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="78f69-211">Sim.</span><span class="sxs-lookup"><span data-stu-id="78f69-211">Yes.</span></span>

<span data-ttu-id="78f69-212">**Posso anexar premium e série tamanho de tooa de discos de dados padrão que não suporta o Premium Storage, tais como a série de D, Dv2, G ou F?**</span><span class="sxs-lookup"><span data-stu-id="78f69-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="78f69-213">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-213">No.</span></span> <span data-ttu-id="78f69-214">Pode anexar apenas padrão a dados discos tooVMs que não utilizem uma série de tamanho que suporte o Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="78f69-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="78f69-215">**Se criar um disco de dados premium a partir de um VHD existente que estava 80 GB, quanto será que custo?**</span><span class="sxs-lookup"><span data-stu-id="78f69-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="78f69-216">Um disco de dados premium criado a partir de um VHD de 80 GB é tratado como Olá disponível a seguinte tamanho do disco premium, que é um disco de P10.</span><span class="sxs-lookup"><span data-stu-id="78f69-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="78f69-217">Está a cobrada de acordo com toohello P10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="78f69-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="78f69-218">**Existem custos de transação toouse Premium Storage?**</span><span class="sxs-lookup"><span data-stu-id="78f69-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="78f69-219">Não há um custo fixo para cada tamanho de disco, o que é aprovisionado com limites específicos no IOPS e débito.</span><span class="sxs-lookup"><span data-stu-id="78f69-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="78f69-220">Olá outros custos são largura de banda de saída e a capacidade de instantâneos, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="78f69-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="78f69-221">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="78f69-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="78f69-222">**Quais são Olá os limites de IOPS e débito que pode receber de cache em disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="78f69-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="78f69-223">Olá combinados limites para a cache e SSD local para uma série DS são 4000 IOPS por núcleos e 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="78f69-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="78f69-224">Olá série GS oferece 5000 IOPS por núcleos e 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="78f69-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="78f69-225">**É Olá que local SSD suportado para uma VM de discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="78f69-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="78f69-226">Olá local SSD é armazenamento temporário que está incluído com uma VM de discos geridos.</span><span class="sxs-lookup"><span data-stu-id="78f69-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="78f69-227">Existe um custo extra para este armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="78f69-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="78f69-228">Recomendamos que não utilize este toostore SSD local os dados da aplicação porque este não é continuada no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="78f69-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="78f69-229">**São não existe qualquer repercussions para Olá a utilização de operações de COMPACTAÇÃO em discos premium?**</span><span class="sxs-lookup"><span data-stu-id="78f69-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="78f69-230">Não há nenhuma utilização toohello downside cortar nos discos do Azure premium o ou os discos padrão.</span><span class="sxs-lookup"><span data-stu-id="78f69-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="78f69-231">Novos tamanhos de disco: geridos e não geridas</span><span class="sxs-lookup"><span data-stu-id="78f69-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="78f69-232">**O que é Olá maior tamanho do disco suportado para o sistema operativo e os discos de dados?**</span><span class="sxs-lookup"><span data-stu-id="78f69-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="78f69-233">tipo de partição de Olá que suporta o Azure para um disco de sistema operativo é registo Olá de arranque principal (MBR).</span><span class="sxs-lookup"><span data-stu-id="78f69-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="78f69-234">formato MBR Olá suporta um tamanho de disco segurança too2 TB.</span><span class="sxs-lookup"><span data-stu-id="78f69-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="78f69-235">Olá a maior dimensão possível que suporta o Azure para um disco de sistema operativo é 2 TB.</span><span class="sxs-lookup"><span data-stu-id="78f69-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="78f69-236">Azure suporta até too4 TB para discos de dados.</span><span class="sxs-lookup"><span data-stu-id="78f69-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="78f69-237">**O que é Olá maior blob tamanho de página que é suportado?**</span><span class="sxs-lookup"><span data-stu-id="78f69-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="78f69-238">Olá maior página tamanho do blob que suporte do Azure é de 8 TB (8,191 GB).</span><span class="sxs-lookup"><span data-stu-id="78f69-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="78f69-239">Não é suportada com mais de 4 TB (4,095 GB) ligado tooa VM como discos de sistema operativo ou de dados de blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="78f69-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="78f69-240">**É necessário toouse uma nova versão das ferramentas do Azure toocreate, anexar, redimensionar e carregar discos superiores a 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="78f69-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="78f69-241">Não precisa de tooupgrade sua toocreate de ferramentas do Azure existente, anexar ou redimensionar discos superiores a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="78f69-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="78f69-242">tooupload o VHD de ficheiros no local diretamente tooAzure como um blob de página ou disco não gerido, tem de conjuntos de ferramenta mais recentes do toouse Olá:</span><span class="sxs-lookup"><span data-stu-id="78f69-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="78f69-243">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="78f69-243">Azure tools</span></span>      | <span data-ttu-id="78f69-244">Versões suportadas</span><span class="sxs-lookup"><span data-stu-id="78f69-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="78f69-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78f69-245">Azure PowerShell</span></span> | <span data-ttu-id="78f69-246">Número de versão 4.1.0: versão de Junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="78f69-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="78f69-247">CLI do Azure v1</span><span class="sxs-lookup"><span data-stu-id="78f69-247">Azure CLI v1</span></span>     | <span data-ttu-id="78f69-248">Número de versão 0.10.13: versão de Maio de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="78f69-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="78f69-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="78f69-249">AzCopy</span></span>           | <span data-ttu-id="78f69-250">Número de versão 6.1.0: versão de Junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="78f69-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="78f69-251">suporte de Olá para v2 CLI do Azure e o Explorador de armazenamento do Azure está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="78f69-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="78f69-252">**P4 e P6 tamanhos de disco são suportados para os discos não geridos ou blobs de página?**</span><span class="sxs-lookup"><span data-stu-id="78f69-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="78f69-253">Não.</span><span class="sxs-lookup"><span data-stu-id="78f69-253">No.</span></span> <span data-ttu-id="78f69-254">P4 (32 GB) e P6 tamanhos de disco (64 GB) são suportados apenas para discos geridos.</span><span class="sxs-lookup"><span data-stu-id="78f69-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="78f69-255">Suporte para discos não geridos e blobs de páginas está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="78f69-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="78f69-256">**Se a minha premium existente gerido disco inferior a 64 GB foi criado antes de disco pequeno Olá foi ativado (em torno do dia 15 de Junho de 2017), como é é faturada?**</span><span class="sxs-lookup"><span data-stu-id="78f69-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="78f69-257">Discos premium pequeno existentes inferior a 64 GB continuar toobe cobrado de acordo com toohello P10 escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="78f69-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="78f69-258">**Como posso mudar a camada de disco de Olá dos discos premium pequeno inferior a 64 GB de P10 tooP4 ou P6?**</span><span class="sxs-lookup"><span data-stu-id="78f69-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="78f69-259">Pode tirar um instantâneo os discos pequenos e, em seguida, criar um Olá de comutador do disco tooautomatically tooP4 do escalão de preço ou P6 com base no tamanho de Olá aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="78f69-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="78f69-260">E se a minha pergunta não é atendida aqui?</span><span class="sxs-lookup"><span data-stu-id="78f69-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="78f69-261">Se a sua pergunta não está listada aqui, informe-nos e vamos ajudá-lo a encontrar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="78f69-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="78f69-262">Pode colocar uma pergunta no final deste artigo Olá nos comentários de Olá.</span><span class="sxs-lookup"><span data-stu-id="78f69-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="78f69-263">tooengage com a equipa de armazenamento do Azure Olá e outros membros da Comunidade sobre neste artigo, utilize Olá MSDN [fórum de armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="78f69-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="78f69-264">funcionalidades de toorequest, submeter o pedidos e ideias toohello [fórum de comentários do Storage do Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="78f69-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
