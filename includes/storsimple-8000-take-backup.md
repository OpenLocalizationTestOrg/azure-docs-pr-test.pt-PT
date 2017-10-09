<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a>tootake uma cópia de segurança

1. Aceda tooyour do serviço StorSimple Manager de dispositivo. Olá tabela lista de dispositivos selecione e clique em seu dispositivo e, em seguida, clique em **todas as definições**. No Olá **definições** painel, vá demasiado**definições > Gerir > política de cópia de segurança**.

    ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu1.png)

2. No Olá **política de cópia de segurança** painel, clique em **+ Adicionar política**.

    ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu2.png)

3. No Olá **criar política de cópia de segurança** painel, forneça um nome que contenha entre 3 e 150 carateres para a sua política de cópia de segurança.

4. Selecione Olá volumes toobe uma cópia de segurança. Se selecionar mais do que um volume, estes volumes se encontram agrupado toocreate em conjunto uma cópia de segurança consistentes com falhas.

    ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu4.png)

5. No painel **Adicionar primeira agenda**:

    1. Selecione o tipo de Olá da cópia de segurança. Para restauros mais rápidos, selecione instantâneo **Local**. Para resiliência de dados, selecione instantâneo da **Cloud**.
    2. Especifique a frequência de cópia de segurança de Olá em minutos, horas, dias ou semanas.
    3. Selecione um tempo de retenção. Opções de retenção de Olá dependem da frequência de cópia de segurança de Olá. Por exemplo, para uma política diária, retenção de Olá pode ser especificada em semanas, enquanto que o período de retenção para uma política mensal é em meses.
    4. Selecione Olá Iniciar hora e data de política de cópia de segurança de Olá.
    5. Clique em **OK** política de cópia de segurança de Olá toocreate.

        ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. Clique em **criar** toostart a criação da política de cópia de segurança Olá. Será notificado quando a política de cópia de segurança de Olá é criada com êxito. lista de Olá das políticas de cópia de segurança também é atualizada.
      
      ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      Tem agora uma política de cópias de segurança que cria as cópias de segurança agendadas dos dados do seu volume.




