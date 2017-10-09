## <a name="customize-and-extend-hello-device-management-actions"></a>Personalizar e expandir as ações de gestão de dispositivos de Olá

As soluções de IoT podem aumente Olá definido pelo conjunto de padrões de gestão de dispositivos ou ativar padrões personalizadas utilizando o dispositivo duplo de Olá e primitivos do método de nuvem para o dispositivo. Outros exemplos de ações de gestão de dispositivos incluem a reposição de fábrica, atualização de firmware, a atualização de software, gestão de energia, gestão de rede e a conectividade e encriptação de dados.

## <a name="device-maintenance-windows"></a>Janelas de manutenção do dispositivo

Normalmente, configurar as ações de tooperform dispositivos cada vez que minimiza a interrupções planeadas e período de indisponibilidade. Janelas de manutenção do dispositivo são frequentemente utilizadas padrão toodefine Olá vez quando um dispositivo deve ser atualizado a respetiva configuração. As soluções de back-end podem utilizar propriedades de Olá pretendido de Olá dispositivo duplo toodefine e ativar uma política no seu dispositivo que permite uma janela de manutenção. Quando um dispositivo receber a política de janela de manutenção de Olá, pode utilizar Olá comunicadas propriedade Olá duplo tooreport Olá do estado dos dispositivos da política de Olá. aplicação de back-end Olá, em seguida, pode utilizar o dispositivo duplo consultas tooattest toocompliance de dispositivos e cada política.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, utilizou tootrigger um método direto reiniciar o computador remoto num dispositivo. Olá utilizada comunicada propriedades tooreport Olá reinicie última hora dispositivo Olá e Olá do Olá consultado dispositivo duplo toodiscover reiniciar última hora do dispositivo Olá da nuvem Olá.

toocontinue introdução ao IoT Hub e padrões de gestão de dispositivos como remoto através de atualização de firmware de ar Olá, consulte:

[Tutorial: Como toodo um firmware atualizar][lnk-fwupdate]

toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.

toocontinue introdução ao IoT Hub, consulte [introdução ao IoT Edge][lnk-iot-edge].

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md