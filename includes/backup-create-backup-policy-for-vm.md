## <a name="defining-a-backup-policy"></a>Definir uma política de cópia de segurança
Uma política de cópia de segurança define uma matriz de quando são tirados instantâneos de dados de Olá e quanto os instantâneos são retidos. Ao definir uma política para a cópia de segurança de uma VM, pode acionar uma tarefa de cópia de segurança *uma vez por dia*. Quando cria uma nova política, é aplicado toohello cofre. interface de política de cópia de segurança de Olá tem o seguinte aspeto:

![Política de cópia de segurança](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate uma política:

1. Introduza um nome para Olá **nome da política**.
2. Os instantâneos dos seus dados podem ser efetuados num intervalo Diário ou Semanal. Olá utilize **frequência de cópia de segurança** menu pendente toochoose se dados são tirados instantâneos diária ou semanal.
   
   * Se escolher um intervalo diário, utilize a Olá realçado controlo tooselect Olá hora do dia de Olá para instantâneo Olá. hora de Olá toochange, anule a seleção hora Olá e selecione Olá nova hora.
     
     ![Política de cópia de segurança diária](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Se escolher um intervalo semanal, utilize Olá controlos realçados tooselect Olá dia ou dias da semana de Olá e a hora de Olá de instantâneo de Olá tootake de dia. No menu dos dias Olá, selecione um ou vários dias. No menu de hora Olá, selecione uma hora. hora de Olá toochange, anule a seleção hora selecionada Olá e selecione Olá nova hora.
     
     ![Política de cópia de segurança semanal](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Por predefinição, todas as opções do **Intervalo de Retenção** estão selecionadas. Desmarque qualquer limite de intervalo de retenção não quiser toouse. Em seguida, especifique Olá toouse de intervalo (s).
   
    Mensal e anual períodos de retenção permitem-lhe instantâneos de Olá toospecify com base num incremento semanal ou diário.
   
   > [!NOTE]
   > Ao proteger uma VM, é executada uma tarefa de cópia de segurança uma vez por dia. tempo de Olá quando executa Olá de cópia de segurança é hello igual para cada intervalo de retenção.
   > 
   > 
4. Depois de definir todas as opções para a política de Olá, Olá parte superior do painel de Olá clique **guardar**.
   
    nova política de Olá é imediatamente aplicado toohello cofre.

