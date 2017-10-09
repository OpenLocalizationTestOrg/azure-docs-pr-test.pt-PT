<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate um volume
1. No dispositivo Olá **início rápido** página, clique em **adicionar um volume**. Esta ação inicia Olá Assistente adicionar um volume.
2. No Olá Assistente para adicionar um volume, em **definições básicas**, Olá a seguir:
   
   1. Forneça um **Nome** para o volume.
   2. Especifique Olá **capacidade aprovisionada** para o volume em GB ou TB. capacidade do volume Olá tem de ser entre 1 GB e 64 TB para um dispositivo físico.
   3. No Olá na lista pendente, selecione Olá **tipo de utilização** para o volume. 
   4. Se estiver a utilizar este volume para dados de arquivo, selecionar Olá **utilizar este volume para menos dados de arquivo acedidos com frequência** caixa de verificação. Para todos os outros casos de utilização selecione simplesmente **Volume em Camadas**. (Os volumes em camadas chamavam-se anteriormente volumes principais).
      
        ![Adicionar volume](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Clique Olá ícone de seta ![ícone de seta](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello a página seguinte.
3. No Olá **definições adicionais** caixa de diálogo Adicionar um novo registo de controlo de acesso (ACR):
   
   1. Forneça um **Nome** para o ACR.
   2. Em **nome do iniciador iSCSI**, fornecer Olá iSCSI nome qualificado (IQN) de anfitrião do Windows. Se não tiver Olá IQN, aceda demasiado[Get Olá IQN de um anfitrião Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Recomendamos que ative uma cópia de segurança predefinida selecionando Olá **ativar uma cópia de segurança predefinido para este volume** caixa de verificação. cópia de segurança do Olá predefinida criará uma política executada às 22:30 todos os dias (hora de dispositivo), que cria um instantâneo de nuvem do volume.
      
      > [!NOTE]
      > Depois da cópia de segurança de Olá é ativada aqui, não pode ser revertida. Terá de tooedit Olá volume toomodify esta definição.
      > 
      > 
      
        ![Adicionar volume](./media/storsimple-create-volume/AddVolume2-include.png)
4. Clique Olá ícone de verificação ![ícone de verificação](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Será criado um volume com Olá especificado definições.

![Vídeo disponível](./media/storsimple-create-volume/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toocreate um volume StorSimple, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).

