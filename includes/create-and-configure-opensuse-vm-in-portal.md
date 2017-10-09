1. Inicie sessão no toohello [portal clássico do Azure](http://manage.windowsazure.com).  
2. Na barra de comando de Olá em Olá parte inferior da janela de Olá, clique em **novo**.
3. Em **computação**, clique em **Máquina Virtual**e, em seguida, clique em **da galeria**.
   
    ![Criar uma nova máquina Virtual][Image1]
4. Em Olá **SUSE** grupo, selecione uma imagem de máquina virtual OpenSUSE e, em seguida, clique em Olá seta toocontinue.
5. No Olá primeiro **configuração da Máquina Virtual** página:
   
   * Escreva um **nome da Máquina Virtual**, tais como "testlinuxvm". Olá nome tem de conter entre 3 e 15 carateres, pode conter apenas letras, números e hífenes e deve começar com uma letra e terminar com uma letra ou número.
   * Certifique-se Olá **camada** e escolha um **tamanho**. camada de Olá determina os tamanhos de Olá que pode escolher. Olá afeta o tamanho custo de Olá de utilizá-la, bem como opções de configuração, tais como quantos discos de dados pode anexar. Para obter mais informações, consulte [tamanhos das virtual machines](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Escreva um **novo nome de utilizador**, ou aceite a predefinição de Olá, **azureuser**. Este nome é adicionado toohello Sudoers ficheiro da lista.
   * Decida qual o tipo de **autenticação** toouse. Para Diretrizes gerais da palavra-passe, consulte [palavras-passe seguras](http://msdn.microsoft.com/library/ms161962.aspx).
6. No Olá seguinte **configuração da Máquina Virtual** página:
   
   * Utilizar predefinição de Olá **criar um novo serviço de nuvem**.
   * No Olá **nome DNS** caixa, escreva um toouse de nome DNS exclusivo como parte do endereço de Olá, como "testlinuxvm".
   * No Olá **afinidade de região/grupo/Virtual Network** caixa, selecione uma região onde será alojada esta imagem de virtual.
   * Em **pontos finais**, mantenha o ponto final de SSH Olá. Pode adicionar outros agora, ou adicionar, alterar ou eliminá-los após a criação da máquina virtual de Olá.
     
     > [!NOTE]
     > Se pretender que uma máquina virtual de toouse uma rede virtual, **tem** especifique a rede virtual Olá quando criar máquina virtual de Olá. Não é possível adicionar a rede virtual da máquina virtual tooa depois de criar a máquina virtual de Olá. Para obter mais informações, consulte [descrição geral de rede Virtual](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. No Olá último **configuração da Máquina Virtual** página, manter as predefinições de Olá e, em seguida, clique em Olá toofinish de marca de verificação.

Olá portal apresenta uma lista de Olá nova máquina virtual em **máquinas virtuais**. Enquanto o estado de Olá é comunicado como **(aprovisionamento)**, máquina virtual de Olá está a ser configurada. Quando o estado de Olá é comunicado como **executar**, pode passar toohello próximo passo.

## <a name="connect-toohello-virtual-machine"></a>Ligar toohello Máquina Virtual
Irá utilizar o SSH PuTTY tooconnect toohello a máquina virtual ou, consoante o sistema de operativo Olá no computador de Olá que irá ligar a partir de:

* A partir de um computador com Linux, utilize SSH. Na linha de comandos Olá, escreva:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Escreva a palavra-passe do utilizador Olá.
* A partir de um computador com o Windows, utilize o PuTTY. Se não o tiver instalado, transfira-o de Olá [a página de transferências PuTTY][PuTTYDownload].
  
    Guardar **putty.exe** tooa diretório no seu computador. Abra uma linha de comandos, navegue até toothat pasta e executar **putty.exe**.
  
    Escreva o nome de anfitrião de Olá, como "testlinuxvm.cloudapp.net" e escreva "22" para Olá **porta**.
  
    ![Ecrã puTTY][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Atualizar Olá Máquina Virtual (opcional)
1. Depois de tiver a máquina virtual de toohello ligado, opcionalmente, pode instalar atualizações do sistema e correções de erros. toorun Olá atualização, o tipo:
   
    `$ sudo zypper update`
2. Selecione **Software**, em seguida, **actualização Online** atualizações disponíveis toolist. Selecione **aceitar** toostart Olá instalação e aplique a todos os patches de disponíveis novo (exceto Olá aqueles opcionais).
3. Após a instalação for efetuada, selecione **concluir**.  O sistema está agora a cópia de segurança toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
