Pode criar máquinas virtuais no Azure utilizando o Explorador de servidores no Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Criar uma máquina virtual do Azure no Explorador de servidores
Embora seja possível criar uma máquina virtual no Olá [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103), também pode criar uma máquina virtual no Azure através da utilização de comandos no Explorador de servidores. Máquinas virtuais podem ser utilizadas, por exemplo, tooprovide um frente terminar atrás de um comuns com balanceamento de carga ponto final público.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate uma nova máquina virtual
1. No Explorador de servidores, abra Olá **Azure** nó e clique em **máquinas virtuais**.
2. No menu de contexto de Olá, clique em **criar Máquina Virtual**.
   
    Olá **criar uma nova máquina Virtual** é apresentado o assistente.
   
    ![Olá comando Criar Máquina Virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. No Olá **escolha uma subscrição** página, selecione uma subscrição toouse ao criar a máquina virtual de Olá e, em seguida, clique em **seguinte**.
   
    Se não tem sessão iniciada no tooAzure, clique em **sessão** toosign no. Em seguida, selecione a subscrição do Azure na caixa de listagem pendente Olá se ainda não estiver selecionada.
4. No Olá **selecionar uma imagem de Máquina Virtual** página, selecione um tipo de imagem no Olá **tipo de imagem** pendente caixa de lista e, em seguida, selecione um imagens da máquina virtual na Olá **nome da imagem** caixa de listagem. Quando tiver terminado, clique em **seguinte**.
   
    ![Selecionar uma página de imagem de máquina virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Pode escolher Olá os seguintes tipos de imagem.
   
   * **Imagens públicas** apresenta uma lista de imagens da máquina virtual de sistemas operativos e o software de servidor, tais como o Windows Server e SQL Server.
   * **Imagens MSDN** apresenta uma lista de imagens da máquina virtual de subscritores de tooMSDN disponível do software, como o Visual Studio e o Microsoft Dynamics.
   * **Imagens de privada** listas especializada e generalizado imagens da máquina virtual que criou.
     
     toolearn sobre especializada e generalizado máquinas virtuais, consulte [imagem de VM](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Consulte [como tooCapture tooUse uma Máquina Virtual do Windows como um modelo](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) para obter informações sobre como tooturn uma máquina virtual a um modelo que pode utilizar tooquickly criar novos pré-configurados máquinas virtuais.
     
     Pode clicar uma máquina virtual imagem nome toosee informações sobre Olá imagem no lado direito de Olá da página Olá.
     
     > [!NOTE]
     > Não é possível adicionar toohello de imagens de máquina virtual **imagens pública** ou **imagens MSDN** lista porque são só de leitura. Todas as máquinas virtuais que criar são adicionadas toohello **privada imagens** lista.
     > 
     > 
     
     Se tiver um subscritor do MSDN com uma subscrição do Visual Studio-nível, pode criar uma máquina de virtual do Azure pré-criadas que contém o Visual Studio, bem como várias outras imagens. Para obter mais informações, consulte [criar uma Máquina Virtual no Visual Studio pela imagem a utilizar imagens Visual Studio 2013 Galeria para subscritores do MSDN](http://visualstudio2013msdngalleryimage.azurewebsites.net) e [subscrições MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs). |
5. No Olá **definições básicas de Máquina Virtual** página, introduza um nome de máquina e, em seguida, adicionar as especificações de Olá para a máquina virtual de Olá, incluindo o tamanho de Olá e um nome de utilizador e palavra-passe. Quando tiver terminado, clique em **seguinte**.
   
    Irá utilizar o novo nome de Olá e palavra-passe toolog numa máquina Olá utilizando o ambiente de trabalho remoto, pelo que é um toowrite boa ideia-los para baixo em maiúsculas e minúsculas se esqueça. Depois de criar uma máquina virtual do Azure no Visual Studio, pode alterar o tamanho e outras definições no Olá [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Se escolher maior tamanhos de máquina virtual de Olá, podem aplicar encargos adicionais. Consulte [detalhes de preços de máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/) para obter mais informações.
   > 
   > 
6. Máquinas virtuais criadas no Visual Studio requer um serviço em nuvem. No Olá **definições do serviço de nuvem** página, selecione um serviço em nuvem da máquina virtual de Olá ou clique em **< criar novo … >** na lista pendente de Olá se ainda não tiver uma nuvem de serviço ou quiser toouse um novo um. Também é necessária uma conta de armazenamento, por isso, escolha uma conta de armazenamento (ou crie uma nova conta de armazenamento) no Olá **conta de armazenamento** caixa de lista pendente. Consulte [introdução tooMicrosoft Storage do Azure](../articles/storage/common/storage-introduction.md) para obter mais informações.
7. Se quiser toospecify uma rede virtual (o que é opcional), selecione-o na Olá rede Virtual e sub-rede pendente caixas de listagem.
   
    Máquinas virtuais que são membros de um conjunto de disponibilidade estão domínios de falhas de toodifferent implementado. Consulte [Azure Virtual Network](https://azure.microsoft.com/services/virtual-network/) para obter mais informações.
8. Se pretender que a máquina virtual toobelong tooan conjunto de disponibilidade (também opcional), selecione Olá **Especifique um conjunto de disponibilidade** caixa de verificação e, em seguida, escolha um conjunto de disponibilidade no caixa de lista pendente de Olá. Quando tiver terminado, escolha Olá **seguinte** botão.
   
    Adicionar a máquina virtual tooan conjunto de disponibilidade ajuda-o a aplicação permanecem disponíveis durante falhas de rede, falhas de hardware de disco local e qualquer período de indisponibilidade planeado. Terá de toouse Olá [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103) define a redes virtuais toocreate, sub-redes e disponibilidade. Consulte [gerir Olá disponibilidade das Virtual Machines](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) para obter mais informações.
9. No Olá **pontos finais** página, especifique Olá pontos finais públicos que pretende que o toousers disponíveis da sua máquina virtual. Por exemplo, poderá escolher tooenable HTTP (porta 80) Ademais toohello ambiente de trabalho remoto e o PowerShell pontos finais, que estão ativados por predefinição. tooadd um ponto final, escolha um em Olá **nome de porta** pendente caixa de lista e, em seguida, escolha Olá **adicionar** botão. tooremove um ponto final, escolha Olá vermelho **X** seguinte toohello nome na lista de pontos finais de Olá.
   
    ![página de pontos finais de Olá no Assistente de máquinas virtuais de Olá.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    pontos finais de Olá que estão disponíveis dependem do serviço de nuvem Olá selecionado para a máquina virtual. Consulte [pontos finais de serviço do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) para obter mais informações.
   
   > [!NOTE]
   > Ativar pontos finais públicos faz com que serviços no seu toohello disponíveis de máquina virtual à internet. Ser tooinstall se e corretamente configurar pontos finais de Olá e os serviços na sua máquina virtual, tais como listas de controlo de acesso de definição (ACL) para pontos finais de Olá. Consulte [como tooSet pontos finais de cópia de segurança tooa Máquina Virtual](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) para obter mais informações.
   > 
   > 
10. Depois de terminado configurar definições da máquina virtual Olá, escolha Olá **criar** máquina virtual do botão toocreate Olá.
    
     Como o Azure cria a máquina virtual de Olá, Olá **registo de atividade do Azure** mostra Olá progresso da operação de criação de máquina virtual de Olá.
    
     ![Registo de atividade de máquina virtual - em curso.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     informações da máquina virtual apenas de tooview, escolha Olá **máquinas virtuais** separador Olá **registo de atividade do Azure**.
    
     ![Registo de atividades do virtual machine - foi concluído.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Se a operação de Olá for concluída com êxito, Olá nova máquina de virtual aparece por baixo Olá **máquinas virtuais** nó no Explorador de servidores. Pode iniciar sessão no-lo ao clicar em Olá **estabeleçam ligação através do ambiente de trabalho remoto** atalho.
    
     ![Máquina virtual no Explorador de servidores.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Gerir as máquinas virtuais
Na página de configuração de máquina virtual de Olá, além disso tooshutting abaixo, ligar, atualizar e adicionar pontos de verificação toohello selecionada máquina virtual, também pode ver ou alterar as definições da máquina virtual de Olá. Pode:

* Alterar tamanho da máquina virtual Olá.
* Conjunto de disponibilidade de Olá selecione toouse com a máquina virtual de Olá.
* Adicionar, remover ou alterar as definições de pontos finais públicos.
* Adicionar, remover ou configurar extensões de máquina virtual.
* Ver informações sobre os discos de Olá associados à máquina virtual de Olá.

### <a name="view-or-change-virtual-machine-settings"></a>Ver ou alterar as definições da máquina virtual
1. No Explorador de servidores, selecione a máquina virtual no Olá **Virtual Machines do Azure** nós.
2. No menu de atalho Olá, escolha **configurar** página de configuração de máquina virtual de Olá tooview.
   
    ![página de configuração de máquina virtual do Azure Olá](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Ver informações da máquina virtual Olá ou alterá-la.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Guardar ou restaurar o estado de Olá da sua máquina virtual
Como configurar a máquina virtual e instalar software, é tooregularly uma boa ideia guardar o seu progresso através da criação de pontos de verificação de máquina virtual. Um ponto de verificação é um instantâneo ou imagem, do estado atual do Olá da sua máquina virtual. Se houver algum problema com a máquina virtual de Olá ou, se quiser tooreconfigure Olá máquina, pode poupar tempo ao restauro de estado de ponto de verificação anterior tooa em vez de iniciar através do zero.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate um ponto de verificação de máquina virtual
1. No Explorador de servidores, selecione a máquina virtual no Olá **Virtual Machines do Azure** nós.
2. No menu de atalho Olá, escolha **configurar** página de configuração de máquina virtual de Olá tooview.
3. Na página de configuração de Olá, escolha Olá **Capturar imagem** botão.
   
    ![Botão de captura da página de configuração do Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Olá **capturar o Virtual Machine** é apresentada a caixa de diálogo.
   
    ![Caixa de diálogo de máquina virtual de captura do Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Forneça uma etiqueta da imagem e uma descrição. São fornecidos uma etiqueta predefinida e uma descrição, mas pode substitui-los com os seus próprios se assim o desejar.
5. Se já tiver executado o Sysprep na máquina virtual, selecione Olá **executei o Sysprep na máquina virtual de Olá** caixa.
   
    Sysprep é uma ferramenta que, entre outras coisas, remove dados específicos de sistemas a versão da máquina virtual Olá do Windows, tornando-o modelo que outros utilizadores podem utilizar. Consulte [como tooCapture tooUse uma Máquina Virtual do Windows como um modelo](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) para obter mais informações. Cópia de segurança Olá VM antes de executar o Sysprep.
6. Depois de terminado configurar definições de captura Olá, escolha Olá **capturar** o ponto de verificação do botão toocreate Olá.
   
    Como o Azure cria o ponto de verificação Olá, Olá **registo de atividade do Azure** mostra Olá progresso Olá operação.
   
    ![Captura de um ponto de verificação de máquina virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Quando concluir a operação de ponto de verificação Olá, irá vê-lo no Olá **registo de atividade do Azure**.
   
    ![Operação de ponto de verificação foi concluída](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>pontos de verificação de máquina virtual de toomanage
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>estado guardado anteriormente de toorestore tooa uma máquina virtual
* Siga os passos de Olá descritos em [passo a passo: efetuar nuvem restaura Microsoft Virtual Machines do Azure com o PowerShell - parte 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete um ponto de verificação
1. Aceda toohello [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Na página de configuração de máquina virtual de Olá, escolha Olá **imagens** separador na Olá parte superior da página Olá.
3. Escolha o ponto de verificação de Olá pretende toodelete e, em seguida, escolha Olá **eliminar** botão na Olá parte inferior da página Olá.

## <a name="shut-down-your-virtual-machine"></a>Encerre a máquina virtual
1. No Explorador de servidores, escolha a máquina virtual de Olá pretende tooshut para baixo no Olá **Virtual Machines do Azure** nós.
2. No menu de atalho Olá, escolha Olá **encerramento** comando ou escolha **configurar** tooview Olá página de configuração de máquina virtual e, em seguida, escolha Olá **encerramento**botão.

## <a name="next-steps"></a>Passos seguintes
toolearn mais sobre a criação de máquinas virtuais, consulte [criar com uma Máquina Virtual a executar Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [criar uma máquina virtual com o Windows no portal de pré-visualização do Azure Olá](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

