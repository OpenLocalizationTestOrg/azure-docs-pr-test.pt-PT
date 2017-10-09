#### <a name="toostop-and-start-a-virtual-device"></a>toostop e iniciar um dispositivo virtual
toostop um dispositivo virtual, clique no respetivo nome e, em seguida, clique em **encerramento**. Enquanto o dispositivo virtual Olá está a encerrar, o respetivo estado é **parar**. Após a paragem do dispositivo virtual Olá, o respetivo estado é **parado**.

Utilize Olá os seguintes cmdlets toostop e iniciar um dispositivo virtual.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart um dispositivo virtual
Quando um dispositivo virtual está em execução e pretender toorestart, clique no respetivo nome e, em seguida, clique em **reiniciar**. Enquanto o dispositivo virtual Olá está a reiniciar, o respetivo estado é **reiniciar**. Quando o dispositivo virtual Olá estiver pronto para lhe toouse, o respetivo estado é **executar**.

Utilize Olá seguintes cmdlet toorestart um dispositivo virtual.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

