#### <a name="toocreate-a-virtual-device"></a>toocreate um dispositivo virtual
1. Olá portal do Azure, aceda toohello **StorSimple Manager** serviço.
2. Aceda toohello **dispositivos** página. Clique em **criar dispositivo virtual** na parte inferior de Olá de Olá **dispositivos** página.
3. No Olá **caixa de diálogo Criar dispositivo Virtual**, especifique os detalhes de Olá.
   
    ![Criar dispositivo virtual StorSimple](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Nome** – um nome exclusivo para o seu dispositivo virtual.
   2. **Modelo** -escolha Olá modelo do dispositivo virtual Olá. Este campo é apresentado apenas se estiver a executar a Atualização 2 ou posterior. Um dispositivo modelo 8010 oferece 30 TB de armazenamento Standard ao passo que o 8020 tem 64 TB de armazenamento Premium. Especifique 8010
   3. cenários de obtenção ao nível do item toodeploy de cópias de segurança. Selecione 8020 toodeploy elevado desempenho, baixa cargas de trabalho de latência ou utilizado como um dispositivo secundário para recuperação após desastre.
   4. **Versão** -escolha a versão de Olá do dispositivo virtual Olá. Se um dispositivo modelo 8020, em seguida, campo de versão Olá não será apresentado toohello utilizador. Esta opção está ausente se todos os Olá físico dispositivos registados com este serviço executam a atualização 1 (ou posterior). Este campo é apresentado apenas se tiver uma mistura de pré-atualização 1 e dispositivos físicos atualização 1 registados Olá mesmo serviço. Fornecido Olá versão do dispositivo virtual Olá irá determinar que dispositivo físico poderá utilizar a ativação pós-falha ou clonar a partir de, é importante que crie uma versão adequada do dispositivo virtual Olá. Selecione:
      
      * Atualização versão 0.3 se pretender efetuar a ativação pós-falha ou DR a partir de um dispositivo físico a executar a Atualização 0.3 ou anterior. 
      * Atualização versão 1 se pretender efetuar a ativação pós-falha ou clonar a partir de um dispositivo físico a executar a Atualização 1 (ou posterior). 
   5. **Rede virtual** – especifique uma rede virtual que pretende que toouse com este dispositivo virtual. Se utilizar o Premium Storage (atualização 2 ou posterior), tem de selecionar uma rede virtual que é suportada com Olá conta do Premium Storage. redes virtuais Olá não suportada estarão indisponíveis na lista pendente de Olá. Será avisado se selecionar uma rede virtual não suportada. 
   6. **Conta de armazenamento para a criação do dispositivo Virtual** – Selecione uma imagem da Olá de toohold de conta de armazenamento do dispositivo virtual Olá durante o aprovisionamento. Esta conta de armazenamento deve estar no Olá mesma região que o dispositivo virtual Olá e a rede virtual. Não deve ser utilizada para armazenamento de dados por Olá físico ou dispositivo virtual Olá. Por predefinição, será criada uma nova conta de armazenamento para esta finalidade. No entanto, se souber que já tem uma conta de armazenamento que é adequada para esta utilização, pode selecionar na lista de Olá. Se criar um dispositivo virtual premium, na lista pendente Olá apresentará apenas contas do Premium Storage. 
      
      > [!NOTE]
      > dispositivo virtual Olá só pode ser utilizado com contas de armazenamento do Azure Olá. Outros fornecedores de serviços em nuvem como Amazon, HP e OpenStack (que são suportados para o dispositivo físico Olá) não são suportados para o dispositivo virtual StorSimple Olá.
      > 
      > 
   7. Clique em Olá tooindicate de marca de verificação que compreender que dados de Olá armazenados no dispositivo virtual Olá serão alojados num Microsoft datacenter. Se utilizar apenas um dispositivo físico, a sua chave de encriptação é mantida com o dispositivo. Por conseguinte, a Microsoft não a poderá desencriptar. 
      
       Quando utilizar um dispositivo virtual tanto a chave de encriptação de Olá, como a chave de desencriptação de Olá são armazenadas no Microsoft Azure. Para obter mais informações, veja [Considerações de segurança para utilizar um dispositivo virtual](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Clique em Olá verificação ícone toocreate Olá dispositivo virtual. dispositivo Olá pode demorar cerca de 30 minutos toobe, aprovisionado.
      
      ![Fase de criação do dispositivo virtual StorSimple](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

