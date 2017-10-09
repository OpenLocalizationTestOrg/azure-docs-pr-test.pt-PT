<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate um volume
1. No dispositivo Olá **início rápido** página, clique em **adicionar um volume** toostart Olá Assistente adicionar um volume.
2. No Olá Assistente para adicionar um volume, em **definições básicas**:
   
   1. Escreva um **Nome** para o volume.
   2. No Olá na lista pendente, selecione Olá **tipo de utilização** para o volume. Para cargas de trabalho que necessitem de garantias locais, latências baixas e desempenho superior, selecione um volume **Afixado localmente**. Para todos os outros dados, selecione um volume **Em camadas**. Se estiver a utilizar este volume para os dados de arquivo, marque **Utilizar este volume para dados de arquivo acedidos com menos frequência**. 
      
       Um volume localmente afixado é fortemente aprovisionado e assegura que os dados primários de Olá no volume de Olá permanecem dispositivo local toohello e não transbordam toohello nuvem.  Se criar um volume localmente afixado, dispositivo Olá verifica se existe espaço disponível nas camadas locais Olá volume de Olá tooprovision de Olá pedida tamanho. operação Olá de criação de um volume localmente afixado pode envolver transbordar dados existentes do Olá dispositivo toohello nuvem e tempo de Olá decorrido o volume de Olá toocreate poderá ser longo. tempo total Olá depende Olá tamanho do volume de Olá aprovisionado, largura de banda disponível e dados de Olá no seu dispositivo. 
      
       Um volume em camadas é fracamente aprovisionado e pode ser criado rapidamente. Selecionar **utilizar este volume para menos dados de arquivo acedidos com frequência** para direcionadas para o tamanho dos segmentos de dados de arquivo alterações Olá eliminação de duplicados para o volume de volume em camadas too512 KB. Se este campo não estiver marcado, o volume em camadas correspondente de Olá utiliza um tamanho de segmentos de 64 KB. Um tamanho de segmentos de eliminação de duplicados maior permite a transferência do Olá dispositivo tooexpedite Olá da nuvem de toohello do arquivo de dados de grandes dimensões.
   3. Especifique Olá **capacidade aprovisionada** para o volume. Tome nota da capacidade de Olá que estão disponível com base no tipo de volume Olá selecionado. Olá especificado não deve exceder o tamanho do volume de espaço disponível Olá.
      
       Pode aprovisionar volumes localmente afixados segurança too8.5 TB ou volumes em camadas segurança too200 TB no dispositivo 8100 Olá. No dispositivo 8600 maior Olá, pode aprovisionar volumes localmente afixados segurança too22.5 TB ou volumes em camadas segurança too500 TB. Tal como espaço local no dispositivo Olá está Olá toohost necessário trabalhar conjunto de volumes em camadas, criação de volumes localmente afixados tem impacto no espaço de Olá disponível para o aprovisionamento de volumes em camadas. Por conseguinte, se criar um volume afixado localmente, será reduzido o espaço disponível para criação de volumes em camadas. Da mesma forma, se for criado um volume em camadas, o espaço disponível do Olá para a criação de volumes localmente afixados é reduzido.
      
       Se aprovisionar um volume localmente afixado de 8.5 TB (tamanho máximo admissível) no dispositivo 8100, ter esgotado todo Olá local o espaço disponível no dispositivo Olá. Não será capaz de toocreate qualquer volume em camadas de que o ponto em diante como existe não está nenhum espaço local no conjunto de trabalho do Olá dispositivo toohost Olá de Olá camadas volume. Volumes em camadas existentes também afetam o espaço disponível em Olá. Por exemplo, se tiver um dispositivo 8100 que já tem volumes em camadas de, aproximadamente, 106 TB, está disponível apenas um espaço de 4 TB para volumes afixados localmente.
      
       Olá imagem seguinte mostra Olá **definições básicas** caixa de diálogo para um volume afixado localmente.
      
        ![Adicionar volume local](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Olá imagem seguinte mostra Olá **definições básicas** caixa de diálogo para um volume em camadas.
      
        ![Adicionar volume local](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Clique Olá ícone de seta ![ícone de seta](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello a página seguinte.
3. No Olá **definições adicionais** caixa de diálogo Adicionar um novo registo de controlo de acesso (ACR):
   
   1. Forneça um **Nome** para o ACR.
   2. Em **nome do iniciador iSCSI**, fornecer Olá iSCSI nome qualificado (IQN) de anfitrião do Windows. Se não tiver Olá IQN, aceda demasiado[Get Olá IQN de um anfitrião Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Em **cópia de segurança predefinida para este volume?**, selecione Olá **ativar** caixa de verificação. cópia de segurança do Olá predefinida cria uma política executada às 22:30 todos os dias (hora de dispositivo), que cria um instantâneo de nuvem do volume.
      
      > [!NOTE]
      > Depois da cópia de segurança de Olá é ativada aqui, não pode ser revertida. É necessário tooedit Olá volume toomodify esta definição.
      > 
      > 
      
      ![Adicionar volume](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Clique Olá ícone de verificação ![ícone de verificação](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). É criado um volume com Olá especificada as definições.

