1. Execute o ficheiro de instalação do programa de configuração Unified Olá.
2. No **antes de começar**, selecione **instalar o servidor de processos e o servidor de configuração de Olá**.

    ![Antes de começar](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. No **licença de Software de terceiros**, clique em **aceito** toodownload e instalar MySQL.

    ![Software de terceiros](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. No **registo**, selecione a chave de registo de Olá transferiu a partir do Cofre de Olá.

    ![Registo](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. No **definições da Internet**, especifique como o fornecedor em execução no servidor de configuração de Olá liga tooAzure recuperação de sites através de Olá Olá Internet.

   a. Se pretender tooconnect com o proxy de Olá que está atualmente configurado no computador de Olá, selecione **ligar tooAzure recuperação do Site utilizando um servidor proxy**.

   b. Se pretender que Olá fornecedor tooconnect diretamente, selecione **se ligue diretamente tooAzure recuperação de sites sem um servidor proxy**.

   c. Selecione se Olá proxy existente requer autenticação ou se quiser toouse um proxy personalizado para ligação de fornecedor Olá, **ligar com definições de proxy personalizado**.

     * Se utilizar um proxy personalizado, terá de endereço de Olá toospecify, porta e credenciais.
     * Se estiver a utilizar um proxy, já deverá ter permitido os URLs de Olá descritos em [pré-requisitos](#prerequisites).

     ![Firewall](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. No **verificação de pré-requisitos**, a configuração executa um toomake de verificação se a instalação pode ser executada. Se é apresentado um aviso sobre Olá **verificação de sincronização de hora Global**, certifique-se essa hora Olá no relógio do sistema Olá (**data e hora** definições) é Olá mesmo como Olá fuso horário.

    ![Pré-requisitos](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. No **MySQL configuração**, crie as credenciais de início de sessão toohello MySQL instância do servidor que está instalada.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. No **ambiente detalhes**, selecione se que vai tooreplicate VMs de VMware. Se, em seguida, a configuração verifica se PowerCLI 6.0 está instalada.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. No **instalar localização**, selecione de onde pretende que os binários de Olá tooinstall e armazenar cache Olá. unidade de Olá que selecionar tem de ter, pelo menos, 5 GB de espaço em disco disponível, mas recomenda-se uma unidade de cache com, pelo menos, 600 GB de espaço livre.

    ![Localização de instalação](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. No **seleção de rede**, especifique o serviço de escuta de Olá (placa de rede e a porta SSL) no qual envia de servidor de configuração de Olá e recebe dados de replicação. Porta 9443 é Olá predefinido porta é utilizada para enviar e receber tráfego de replicação, mas pode modificar este toosuit número de porta requisitos do seu ambiente. Porta de toohello adição 9443, também Iremos abrir porta 443, que é utilizada por um operações de replicação de tooorchestrate de servidor web. Não utilize a porta 443 para enviar ou receber tráfego de replicação.

    ![Seleção de rede](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. No **resumo**, reveja as informações de Olá e clique em **instalar**. Quando a instalação estiver concluída, é gerada uma frase de acesso. Irá precisar dela, quando ativar a replicação, por isso, copie-a e mantenha-a numa localização segura.

    ![Resumo](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Após a conclusão de registo, o servidor de Olá é apresentado no Olá **definições** > **servidores** painel no Cofre de Olá.
