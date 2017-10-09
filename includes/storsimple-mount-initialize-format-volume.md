<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicializar e formatar um volume
1. Inicie o Iniciador do iSCSI Olá Microsoft.
2. No Olá **propriedades do iniciador iSCSI** janela, no Olá **deteção** separador, clique em **detetar Portal**.
3. No Olá **detetar Portal de destino** caixa de diálogo, forneça o endereço IP Olá da sua interface de rede com o iSCSI e, em seguida, clique em **OK**. 
4. No Olá **propriedades do iniciador iSCSI** janela, no Olá **destinos** separador, localize Olá **destinos detetados**. Estado do dispositivo Olá deve ser apresentadas como **inativo**.
5. Selecione o dispositivo de destino Olá e, em seguida, clique em **Connect**. Depois do dispositivo de Olá está ligado, o estado de Olá deve ser alterado demasiado**ligado**. (Para obter mais informações sobre como utilizar o Iniciador do iSCSI Olá Microsoft, consulte [iniciador iSCSI instalar e configurar o Microsoft][1]).
6. No anfitrião do Windows, prima a tecla de logótipo do Windows de Olá + X e, em seguida, clique em **executar**. 
7. No Olá **executar** caixa de diálogo, escreva **Diskmgmt.msc**. Clique em **OK**e Olá **gestão de discos** será apresentada a caixa de diálogo. painel direito Olá mostrará volumes Olá no seu anfitrião.
8. No Olá **gestão de discos** janela, hello volumes montados serão apresentados como mostrado na seguinte ilustração de Olá. Clique no volume de Olá detetado (clique no nome do disco de Olá) e, em seguida, clique em **Online**.
   
     ![Inicializar a formatação do volume](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. Clique no volume de Olá (clique no nome do disco de Olá) e, em seguida, clique em **inicializar**.
10. tooformat um volume simple, execute Olá os seguintes passos:
    
    1. Selecione o volume de Olá, faça duplo clique nele (clique área à direita Olá) e clique em **Novo Volume simples**.
    2. No Assistente de novo Volume simples Olá, especifique a letra de unidade e de tamanho do volume de Olá e configurar o volume de Olá como um sistema de ficheiros NTFS.
    3. Especifique um tamanho de unidade de alocação de 64 KB. Este tamanho de unidade de alocação funciona bem com algoritmos de eliminação de duplicados de Olá utilizados no Olá solução StorSimple.
    4. Efetue uma formatação rápida.

![Vídeo disponível](./media/storsimple-mount-initialize-format-volume/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toomount, inicializar e formatar um volume StorSimple, clique em [aqui](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/).

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
