1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).

2. A partir do canto superior esquerdo de Olá, clique em **novo > computação > Centro de dados do Windows Server 2016**.

    ![Navegue toohello imagens de VM do Azure no portal de Olá](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. No Centro de dados do Windows Server 2016 Olá, selecione o modelo de implementação clássica Olá. Clique em Criar.

    ![Captura de ecrã que mostra as imagens de VM do Azure Olá disponíveis no portal de Olá](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Painel Básico

Painel de noções básicas de Olá pedidos administrativas informações de Olá máquina virtual.

1. Introduza um **nome** para a máquina virtual de Olá. Exemplo de Olá, _HeroVM_ é Olá nome da máquina virtual de Olá. nome de Olá tem de ser 1-15 carateres e não pode conter carateres especiais.

2. Introduza um **nome de utilizador** e uma forte **palavra-passe** que são utilizado toocreate uma conta local no Olá VM. Olá conta local é utilizada toosign no tooand gerir Olá VM. Exemplo de Olá, _azureuser_ é Olá nome de utilizador.

 Olá palavra-passe tem de ter entre 8-123 carateres e cumprir três fora de requisitos de complexidade de seguintes quatro de Olá: uma minúscula, uma maiúscula, um número e um caráter especial. Saiba mais sobre os [requisitos de nomes de utilizador e palavras-passe](../articles/virtual-machines/windows/faq.md).

3. Olá **subscrição** é opcional. Uma definição comum é "Pay As You Go".

4. Selecione um existente **grupo de recursos** ou nome de Olá de tipo para um novo. Exemplo de Olá, _HeroVMRG_ é o nome de Olá Olá do grupo de recursos.

5. Selecione um datacenter Azure **localização** onde pretende Olá toorun VM. Exemplo de Olá, **EUA Leste** Olá localização.

6. Quando tiver terminado, clique em **seguinte** toocontinue toohello seguinte painel.

    ![Captura de ecrã que mostra as Olá no painel de noções básicas de Olá para configurar uma VM do Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Painel Tamanho

Painel de tamanho de Olá identifica os detalhes de configuração de Olá de Olá VM e apresenta uma lista de várias opções que incluem o SO, número de processadores, tipo de disco de armazenamento e custos de utilização mensais estimado.  

Escolher um tamanho VM e, em seguida, clique em **selecione** toocontinue. Neste exemplo, _DS1_\__V2 padrão_ é o tamanho da VM Olá.

  ![Captura de ecrã do painel de tamanho de Olá que mostra Olá tamanhos de VM do Azure que pode selecionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Painel Definições

Painel de definições de Olá pedidos opções de armazenamento e rede. Pode aceitar as predefinições de Olá. O Azure cria entradas adequadas sempre que necessário.

Se tiver selecionado um tamanho da máquina virtual que o suporte, pode experimentar o Armazenamento Premium do Azure ao selecionar Premium (SSD) em Tipo de Disco.

Quando terminar de efetuar alterações, clique em **OK**.

## <a name="4-summary-blade"></a>4. Painel Resumo

Painel de resumo de Olá lista as definições de Olá especificadas no painel anterior Olá. Clique em **OK** quando estiver a imagem de Olá toomake pronto.

 ![Relatório de resumo painel fornecer as definições especificadas da máquina virtual de Olá](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Depois de criar a máquina virtual de Olá, portal Olá apresenta uma lista de Olá nova máquina virtual em **todos os recursos**e apresenta um mosaico de máquina virtual de Olá no dashboard de Olá. Olá nuvem serviço e o armazenamento conta correspondente também são criadas e listados. Máquina virtual de Olá e o serviço em nuvem são iniciados automaticamente e o estado está listado como **executar**.

 ![Configurar o agente da VM e Olá pontos finais da máquina virtual de Olá](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
