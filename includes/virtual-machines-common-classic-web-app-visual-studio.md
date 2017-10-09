

Quando cria um projeto de aplicação web do Azure, pode aprovisionar uma máquina virtual no Azure. Em seguida, pode configurar Olá máquina com o software adicional ou utilizar a máquina virtual de Olá para fins de depuração ou diagnóstico.

toocreate uma máquina virtual, quando criar uma aplicação web, siga estes passos:

1. No Visual Studio, clique em **ficheiro** > **novo** > **projeto** > **Web**e, em seguida, escolha **Aplicação Web ASP.NET** (em Olá **Visual c#** ou **Visual Basic** nós).
2. No Olá **novo projeto ASP.NET** caixa de diálogo, tipo de Olá selecione da aplicação web que pretende e, na secção do Azure Olá da caixa de diálogo (no canto inferior direito de Olá) Olá, certifique-se de que Olá **anfitrião na nuvem de Olá**está selecionada a caixa de verificação (assinalada como esta caixa de verificação **criar recursos remotos** em algumas instalações).
   
    ![][0]
3. Para este exemplo, na lista pendente de Olá no Microsoft Azure, escolha **Máquina Virtual (v1)**e, em seguida, clique em Olá **OK** botão.
4. Inicie sessão no tooAzure se lhe for pedida. Olá **criar Máquina Virtual** é apresentada a caixa de diálogo.
   
    ![][2]
5. No Olá **nome DNS** caixa, introduza um nome para a máquina virtual de Olá. nome DNS Olá tem de ser exclusivo no Azure. Se o nome de Olá que introduziu não estiver disponível, aparece um ponto de exclamação vermelho.
6. No Olá **imagem** lista, selecione a imagem Olá toobase Olá virtual máquina que pretende em. Pode escolher qualquer uma das imagens da máquina de virtual do Azure standard de Olá ou a imagem que carregar tooAzure.
7. Deixe Olá **ativar o IIS e o Web Deploy** caixa de verificação selecionada, a menos que planeia tooinstall um servidor web diferente. Não será capaz de toopublish a partir do Visual Studio se desativar o Web Deploy. Pode adicionar o IIS e o Web Deploy tooany de imagens do Windows Server Olá empacotada, incluindo as suas próprias imagens personalizadas.
8. No Olá **tamanho** lista, escolha Olá tamanho de Olá máquina virtual.
9. Especifique Olá credenciais de início de sessão para esta máquina virtual. Tome nota dos mesmos, porque terá-los tooaccess Olá máquina através do ambiente de trabalho remoto.
10. No Olá **localização** lista, escolha Olá região toohost Olá máquina.
11. Clique em Olá **OK** toostart botão Criar máquina virtual de Olá. Pode seguir progresso Olá da operação de Olá numa Olá **saída** janela.
    
    ![][3]
12. Quando a máquina virtual de Olá é aprovisionada, scripts publicados são criados num **PublishScripts** nó na sua solução. Olá publicado script é executado e aprovisiona uma máquina virtual no Azure. Olá **saída** janela mostra o estado de Olá. script de Olá efetua Olá ações tooset máquina virtual de Olá os seguintes:
    
    * Cria a máquina virtual de Olá se ainda não existir.
    * Cria uma conta de armazenamento com o nome que comece com `devtest`, mas apenas se não existe já uma conta de armazenamento na região especificada Olá.
    * Cria um serviço em nuvem como um contentor para a máquina virtual de Olá e cria uma função da web da aplicação web de Olá.
    * Configura o Web Deploy na máquina virtual de Olá.
    * Configura o IIS e ASP.NET numa máquina virtual de Olá.
    
    ![][4]
13. (Opcional) Pode ligar a máquina virtual nova do toohello. No **Explorador de servidores**, expanda Olá **máquinas virtuais** nós, escolha o nó de Olá para a máquina virtual de Olá que criou e, no respetivo menu de atalho, escolha **ligar com o ambiente de trabalho remoto**. Em alternativa, na **Cloud Explorer** pode escolher **aberto no Portal** no menu de atalho de Olá e ligue-se toohello máquina de virtual não existe.
    
    ![][5]

## <a name="next-steps"></a>Passos seguintes
Se quiser toocustomize Olá scripts publicados que criou, leia mais informações aprofundadas em [utilizando Scripts do Windows PowerShell tooPublish tooDev e ambientes de teste](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
