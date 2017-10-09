#### <a name="toocreate-a-cloud-appliance"></a>toocreate uma aplicação de nuvem

1. Olá portal do Azure, aceda toohello **Gestor de dispositivos do StorSimple** serviço.
2. Aceda toohello **dispositivos** painel. A partir da barra de comando de Olá no painel de resumo de serviço de Olá, clique em **Criar aplicação de nuvem**.
    ![StorSimple cria aplicação da cloud](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. No Olá **Criar aplicação de nuvem** painel, especifique os detalhes de Olá.
   
    ![StorSimple cria aplicação da cloud](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Nome** – um nome exclusivo para a sua aplicação da cloud.
   2. **Modelo** -escolha Olá modelo do dispositivo de Olá de nuvem. Um dispositivo 8010 oferece 30 TB de armazenamento Standard ao passo que o 8020 tem 64 TB de armazenamento Premium. Especifique o 8010 toodeploy de cenários de obtenção a nível de item de cópias de segurança. Selecione 8020 toodeploy elevado desempenho, cargas de trabalho de latência baixa, ou utilizar como um dispositivo secundário para recuperação após desastre.
   3. **Versão** -escolha Olá versão da aplicação de nuvem Olá. versão de Olá corresponde toohello versão da imagem de disco virtual Olá que é o dispositivo de nuvem de Olá toocreate utilizados. Fornecido Olá versão da nuvem Olá aplicação determina qual físico dispositivo efetuar a ativação pós-falha ou clonar a partir do, é importante que crie uma versão adequada do dispositivo de Olá de nuvem.
   4. **Rede virtual** – especifique uma rede virtual que pretende que toouse com este dispositivo de nuvem. Se utilizar o Premium Storage, tem de selecionar uma rede virtual que é suportada com Olá conta do Premium Storage. redes virtuais Olá não suportado estão desativadas na lista pendente Olá. É avisado se selecionar uma rede virtual não suportada.
   5. **Sub-rede** -com base na rede virtual Olá selecionado, na lista pendente Olá apresenta sub-redes Olá associado. Atribua uma aplicação de nuvem de tooyour de sub-rede.
   6. **Conta de armazenamento** – Selecione uma imagem da Olá de toohold de conta de armazenamento do dispositivo de nuvem Olá durante o aprovisionamento. Esta conta de armazenamento deve estar no Olá mesma região que o dispositivo de Olá de nuvem e de rede virtual. Não deve ser utilizada para armazenamento de dados por Olá físico ou dispositivo de Olá de nuvem. Por predefinição, é criada uma nova conta de armazenamento para esta finalidade. No entanto, se souber que já tem uma conta de armazenamento que é adequada para esta utilização, pode selecionar na lista de Olá. Se criar uma aplicação de nuvem premium, na lista pendente Olá apresenta apenas as contas do Premium Storage.
      
      > [!NOTE]
      > aplicação de nuvem Olá só pode ser utilizado com contas de armazenamento do Azure Olá.
    
   7. Selecione Olá tooindicate de caixa de verificação que compreender que dados de Olá armazenados no dispositivo de Olá de nuvem estão alojados num Microsoft datacenter.
       * Se utilizar apenas um dispositivo físico, a sua chave de encriptação é mantida com o dispositivo. Por conseguinte, a Microsoft não a poderá desencriptar.

       * Quando utiliza uma aplicação de nuvem tanto a chave de encriptação de Olá, como a chave de desencriptação de Olá são armazenadas no Microsoft Azure. Para obter mais informações, veja [security considerations for using a cloud appliance](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security) (considerações de segurança para utilizar uma aplicação da cloud).
   8. Clique em **criar** tooprovision dispositivo de Olá de nuvem. dispositivo Olá pode demorar cerca de 30 minutos toobe, aprovisionado. Será notificado quando o dispositivo de nuvem Olá é criado com êxito. Aceda tooDevices painel e lista Olá de dispositivos atualiza a aplicação de nuvem de Olá toodisplay. Olá estado da aplicação Olá é **pronto tooset segurança**.
      
      ![Aplicação de nuvem do StorSimple tooset pronto cópias de segurança](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

