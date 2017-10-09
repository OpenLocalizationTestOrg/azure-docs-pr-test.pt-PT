<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete Olá mínimo StorSimple a configuração do dispositivo

   > [!NOTE]
   > Não é possível alterar o nome do dispositivo Olá depois de concluída a configuração mínima do dispositivo de Olá.
   
1. Na lista de tabela Olá dos dispositivos na Olá **dispositivos** painel, selecione e clique em seu dispositivo. Olá dispositivo estiver num **pronto tooset segurança** estado. Olá **configurar dispositivo** painel abre-se.

     ![Interfaces de rede para a configuração mínima do dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. No Olá **configurar dispositivo** painel:
   
   1. Forneça um **nome amigável** para o dispositivo. nome Olá predefinido do dispositivo reflete informações como o modelo de dispositivo Olá e número de série. Pode atribuir um nome amigável de cópia de segurança too64 carateres toomanage seu dispositivo.
   2. Conjunto Olá **fuso horário** com base na localização geográfica Olá no qual Olá o dispositivo está a ser implementado. O dispositivo utiliza este fuso horário para todas as operações agendadas.
   3. Em Olá **dados 0 definições**:

       1. Os dados 0 interface de rede mostra como ativada com Olá as definições de rede (IP, sub-rede, gateway) configuradas através do Assistente de configuração de Olá. Os DADOS 0 também são automaticamente ativados para a cloud, bem como a iSCSI.

       2. Fornece Olá fixo endereços IP para o controlador 0 e o controlador 1. **controlador Olá endereços IP fixos necessário toobe livre IPs sub-rede de Olá acessível pelo endereço IP do dispositivo Olá.** Se hello dados 0 interface foi configurada para IPv4, hello fixo toobe de necessidade de endereços IP fornecido no Olá formato IPv4. Se tiver indicado um prefixo para a configuração IPv6, Olá endereços IP fixos são preenchidos automaticamente nestes campos.

            ![Interfaces de rede para a configuração mínima do dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Olá endereços IP para o controlador de Olá fixos são utilizados para a manutenção do dispositivo de toohello Olá atualizações. Por conseguinte, Olá IPs fixo tem de ser encaminháveis e consegue tooconnect toohello Internet. Pode verificar que os IPs fixos do controlador fixo são encaminháveis com Olá [Test-HcsmConnection] [ Test] cmdlet. Olá seguinte exemplo mostra IPs fixos do controlador de fixo é encaminhada toohello Internet e pode aceder ao hello servidores do Microsoft Update.

            ![Test-HcsmConnection a mostrar os IPs encaminháveis](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Clique em **OK**. configuração do dispositivo Olá é iniciado. Quando a configuração do dispositivo Olá estiver concluída, será notificado. Olá alterações de estado do dispositivo demasiado**Online** no Olá **dispositivos** painel.

    ![Interfaces de rede para a configuração mínima do dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
