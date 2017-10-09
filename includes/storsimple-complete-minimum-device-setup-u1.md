<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete Olá mínimo StorSimple a configuração do dispositivo
1. Selecione o dispositivo de Olá e clique em **início rápido**. Clique em **concluir a configuração de dispositivo** assistente toostart Olá configurar dispositivo.
2. No assistente Olá configurar dispositivo **definições básicas** diálogo caixa, Olá a seguir:
   
   1. Forneça um **nome amigável** para o dispositivo. nome Olá predefinido do dispositivo reflete informações como o modelo de dispositivo Olá e número de série. Pode atribuir um nome amigável de cópia de segurança too64 carateres toomanage seu dispositivo.
   2. Conjunto Olá **fuso horário** com base na localização geográfica Olá no qual Olá o dispositivo está a ser implementado. O dispositivo utiliza este fuso horário para todas as operações agendadas.
   3. Em **Definições de DNS**, forneça um endereço para o **Servidor DNS Secundário**. Se estiver a utilizar o IPv6, o campo de Olá será preenchido com base no prefixo de IPv6 Olá fornecido na interface do Windows PowerShell de Olá. 
      Se o servidor DNS secundário de Olá não estiver configurado, não será permitida toosave a configuração do dispositivo.
   4. Nas interfaces preparadas para iSCSI, ative, pelo menos, uma rede para iSCSI. Pelo menos uma interface de rede tem toobe ativado para a nuvem e uma interface preparada toobe preparada para iSCSI. DATA 0 é automaticamente ativado para a nuvem.
      
      ![Definições básicas para a configuração mínima do dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Clique em ícone de seta de Olá. ![Ícone de seta do StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. No Olá **Interfaces de rede** diálogo caixa, forneça Olá fixo endereços IP para o controlador 0 e o controlador 1. **controlador Olá endereços IP fixos necessário toobe livre IPs sub-rede de Olá acessível pelo endereço IP do dispositivo Olá.** Se hello dados 0 interface foi configurada para IPv4, hello fixo toobe de necessidade de endereços IP fornecido no Olá formato IPv4. Se tiver indicado um prefixo para a configuração IPv6, Olá endereços IP fixos será preenchido automaticamente nestes campos.

    ![Interfaces de rede para a configuração mínima do dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Olá endereços IP para o controlador de Olá fixos são utilizados para a manutenção do dispositivo de toohello Olá atualizações e, por conseguinte, tem de ser encaminháveis e consegue tooconnect toohello Internet Olá IPs fixo. Pode verificar que os IPs fixos do controlador fixo são encaminháveis com Olá [Test-HcsmConnection] [ Test] cmdlet. Olá seguinte exemplo mostra IPs fixos do controlador de fixo é encaminhada toohello Internet e pode aceder ao hello servidores do Microsoft Update. 

     ![Test-HcsmConnection a mostrar os IPs encaminháveis](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Clique em ícone de verificação Olá ![ícone de verificação StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Irá devolver toohello dispositivo **início rápido** página.
   
   > [!NOTE]
   > Pode modificar Olá todas as outras definições do dispositivo em qualquer altura acedendo Olá **configurar** página.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx