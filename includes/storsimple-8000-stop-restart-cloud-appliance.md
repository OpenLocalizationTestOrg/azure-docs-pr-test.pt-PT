#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop e iniciar uma aplicação de nuvem

1. toostop uma aplicação de nuvem, visite toohello VM para a sua aplicação de nuvem.
    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. A partir da barra de comando Olá, clique em **parar**.

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Quando lhe for pedida a confirmação, clique em **Sim**.

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Quando parar uma VM, esta é desalocada. Enquanto o dispositivo de Olá de nuvem está a parar, o respetivo estado é **Deallocating**. Após a paragem do dispositivo de Olá de nuvem, o respetivo estado é **parado (desalocado)**.

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Depois de uma VM estiver parada, clique em **iniciar** (botão torna-se disponível) toostart Olá VM. Depois do dispositivo de nuvem Olá começou a cópia de segurança, o respetivo estado é **iniciado**.

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Utilize Olá os seguintes cmdlets toostop e iniciar uma aplicação de nuvem.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart uma aplicação de nuvem

toorestart uma aplicação de nuvem, visite toohello VM para a sua aplicação de nuvem. A partir da barra de comando Olá, clique em **reiniciar**. Quando solicitado, confirme Olá reinício. Quando o dispositivo de nuvem Olá está pronto para lhe toouse, o respetivo estado é **executar**.

![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Utilize Olá seguintes cmdlet toorestart uma aplicação de nuvem.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

