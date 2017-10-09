<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall uma atualização do Olá portal do Azure

1. Na página do serviço de Olá StorSimple, selecione o seu dispositivo. Navegue demasiado**dispositivos** > **manutenção**.
2. Na Olá parte inferior da página Olá, clique em **procurar atualizações**. É criada uma tarefa tooscan para as atualizações disponíveis. Será notificado quando a tarefa de Olá for concluída com êxito.
3. No Olá **atualizações de Software** secção no Olá mesmo página, as atualizações de software novo Olá estão disponíveis. Recomendamos que consulte as notas de versão Olá antes de aplicar uma atualização no seu dispositivo.
4. Na Olá parte inferior da página Olá, clique em **instalar atualizações**e, em seguida, **OK**.
5. No Olá **instalar atualizações** caixa de diálogo, certifique-se de que tiver seguido recomendações Olá, em seguida, selecione **posso compreender Olá acima requisito e estou pronto tooupgrade meu dispositivo** e clique em verificação Olá botão.
   
    ![Mensagem de confirmação](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Um conjunto de verificações de pré-requisitos é iniciado. Estas verificações incluem:
   
   * **As verificações de estado de funcionamento do controlador** tooverify ambos Olá de controladores de dispositivo são bom estado de funcionamento e online.
   * **Verificações de estado de funcionamento do componente de hardware** tooverify que Olá todos os componentes de hardware no dispositivo StorSimple estão em bom estado.
   * **DATA 0 verifica** tooverify que dados 0 estão ativados no seu dispositivo. Se esta interface não estiver ativada, terá de ativá-la e, em seguida, tentar novamente.
   * **DADOS 2 e dados 3 verificações** tooverify que dados 2 e dados 3 interfaces de rede não estão ativadas. Se estas interfaces estiverem ativadas, tem de desativar estas e, em seguida, tente tooupdate do seu dispositivo. Esta verificação é executada apenas se estiver a atualizar a partir de um dispositivo com software GA. Os dispositivos que executem as versões 0.1, 0.2 ou 0.3 não precisam desta verificação.
   * **Verificação de gateway** em qualquer dispositivo que executa um tooUpdate anterior da versão 1. Esta verificação é executada em todos os dispositivos de Olá anterior à atualização 1 software em execução, mas falha em dispositivos de Olá que tenham um gateway configurado para uma interface de rede que não sejam dados 0.
     
     atualização de Olá é aplicada se todas as verificações forem concluídas com êxito. Será notificado quando as verificações de Olá estão em curso.
     
     ![Notificação de pré-verificação](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Olá segue-se um exemplo em que as verificações de Olá falharam. Tem de verificar que os dois controladores de dispositivo Olá estão em bom estado e online. Também precisa de estado de funcionamento do toocheck Olá dos componentes de hardware Olá. Neste exemplo, os componentes Controlador 0 e Controlador 1 necessitam de atenção. Poderá ser necessário toocontact Support da Microsoft, caso não é possível resolver estes problemas por si.
     
       ![Falha das verificações](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Depois das verificações de Olá forem concluídas com êxito, é criada uma tarefa de atualização. Será notificado quando a tarefa de atualização de Olá é criada com êxito.
   
    ![Criação de tarefa de atualização](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    atualização de Olá, em seguida, é aplicada no seu dispositivo.
    
8. progresso de Olá toomonitor da tarefa de atualização de Olá, clique em **ver tarefa**. No Olá **tarefas** página, pode ver Olá em curso de atualização.
9. atualização de Olá demora algumas horas toocomplete. Selecione a tarefa de atualização de Olá e clique em **detalhes** tooview Olá detalhes sobre a tarefa de Olá em qualquer altura.
10. Após a conclusão da tarefa de Olá, navegue até toohello **manutenção** página e desloque para baixo demasiado**atualizações de Software**.

