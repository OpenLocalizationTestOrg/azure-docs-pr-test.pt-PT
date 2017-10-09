


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="e2c18-101">Marcação de uma Máquina Virtual através de modelos</span><span class="sxs-lookup"><span data-stu-id="e2c18-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="e2c18-102">Em primeiro lugar, vamos ver etiquetagem através de modelos.</span><span class="sxs-lookup"><span data-stu-id="e2c18-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="e2c18-103">[Este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) etiquetas, coloca na Olá os seguintes recursos: computação (Máquina Virtual), de armazenamento (conta de armazenamento) e de rede (endereço IP público, rede Virtual e Interface de rede).</span><span class="sxs-lookup"><span data-stu-id="e2c18-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="e2c18-104">Este modelo é para uma VM do Windows, mas pode ser adaptado para VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="e2c18-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="e2c18-105">Clique em Olá **implementar tooAzure** botão de Olá [ligação de modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="e2c18-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="e2c18-106">Isto irá navegue toohello [portal do Azure](https://portal.azure.com/) onde pode implementar este modelo.</span><span class="sxs-lookup"><span data-stu-id="e2c18-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Implementação simples com etiquetas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="e2c18-108">Este modelo inclui Olá seguintes tags: *departamento*, *aplicação*, e *criado pelo*.</span><span class="sxs-lookup"><span data-stu-id="e2c18-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="e2c18-109">Pode adicionar/editar estas etiquetas diretamente no modelo de Olá se pretender que os nomes de etiqueta diferentes.</span><span class="sxs-lookup"><span data-stu-id="e2c18-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Etiquetas do Azure num modelo](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="e2c18-111">Como pode ver, etiquetas Olá são definidas como pares chave/valor, separados por ponto e vírgula (:).</span><span class="sxs-lookup"><span data-stu-id="e2c18-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="e2c18-112">etiquetas de Olá tem de ser definidas neste formato:</span><span class="sxs-lookup"><span data-stu-id="e2c18-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="e2c18-113">Guarde o ficheiro de modelo de Olá depois de concluir a edição-lo com etiquetas de Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="e2c18-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="e2c18-114">Em seguida, no Olá **Editar parâmetros** secção, pode preencher valores de Olá para as suas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="e2c18-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Editar etiquetas no portal do Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="e2c18-116">Clique em **criar** toodeploy este modelo com os valores de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="e2c18-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="e2c18-117">Marcação através de Olá Portal</span><span class="sxs-lookup"><span data-stu-id="e2c18-117">Tagging through hello Portal</span></span>
<span data-ttu-id="e2c18-118">Depois de criar os recursos com etiquetas, pode ver, adicionar e eliminar etiquetas no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2c18-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="e2c18-119">Selecione Olá etiquetas ícone tooview as suas etiquetas:</span><span class="sxs-lookup"><span data-stu-id="e2c18-119">Select hello tags icon tooview your tags:</span></span>

![Ícone de etiquetas no portal do Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="e2c18-121">Adicione uma nova etiqueta através do portal Olá ao definir o seu próprio par chave/valor e guardá-lo.</span><span class="sxs-lookup"><span data-stu-id="e2c18-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Adicionar nova etiqueta no portal do Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="e2c18-123">A nova etiqueta deverá agora aparecer na lista de Olá de etiquetas para o seu recurso.</span><span class="sxs-lookup"><span data-stu-id="e2c18-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Nova etiqueta guardada no portal do Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

