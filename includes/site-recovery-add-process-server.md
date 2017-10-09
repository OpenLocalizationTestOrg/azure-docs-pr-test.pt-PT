1. Iniciar Olá do Azure Site Recovery UnifiedSetup.exe
2. No **antes de começar**, selecione **adicionar tooscale de servidores de processos adicionais saída implementação**.

  ![Adicionar servidor de processos](./media/site-recovery-add-process-server/ps-page-1.png)

3. No **detalhes do servidor de configuração**, especifique o endereço IP Olá hello do servidor de configuração e Olá o frase de acesso.

  ![Adicionar servidor de processos 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. No **definições da Internet**, especifique como o fornecedor em execução no hello do servidor de configuração se liga tooAzure recuperação de sites através de Olá Olá Internet.

  ![Adicionar servidor de processos 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Se pretender tooconnect com o proxy de Olá que está atualmente configurado no computador de Olá, selecione **ligar com definições de proxy existentes**.
   * Se pretender que Olá fornecedor tooconnect diretamente, selecione **ligar diretamente sem um proxy**.
   * Selecione se Olá proxy existente requer autenticação ou se quiser toouse um proxy personalizado para ligação de fornecedor Olá, **ligar com definições de proxy personalizado**.

     * Se utilizar um proxy personalizado, terá de endereço de Olá toospecify, porta e credenciais.
     * Se estiver a utilizar um proxy, poderá já deverá ter permitido os urls do serviço de toohello acesso.

5. No **verificação de pré-requisitos**, a configuração executa um toomake de verificação se a instalação pode ser executada. Se é apresentado um aviso sobre Olá **verificação de sincronização de hora Global**, certifique-se essa hora Olá no relógio do sistema Olá (**data e hora** definições) é Olá mesmo como Olá fuso horário.

     ![Adicionar servidor de processos 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. No **ambiente detalhes**, selecione se que vai tooreplicate VMs de VMware. Se pretender, a configuração verifica se o PowerCLI 6.0 está instalado.

     ![Adicionar servidor de processos 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. No **instalar localização**, selecione de onde pretende que os binários de Olá tooinstall e armazenar cache Olá. unidade de Olá que selecionar tem de ter, pelo menos, 5 GB de espaço em disco disponível, mas recomenda-se uma unidade de cache com, pelo menos, 600 GB de espaço livre.
     ![Adicionar servidor de processos 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. No **seleção de rede**, especifique o serviço de escuta de Olá (placa de rede e a porta SSL) no qual envia de servidor de configuração Olá e recebe dados de replicação. Porta 9443 é Olá predefinido porta é utilizada para enviar e receber tráfego de replicação, mas pode modificar este toosuit número de porta requisitos do seu ambiente. Porta de toohello adição 9443, também Iremos abrir porta 443, que é utilizada por um operações de replicação de tooorchestrate de servidor web. Não utilize a Porta 443 para enviar ou receber tráfego de replicação.

     ![Adicionar servidor de processos 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. No **resumo**, reveja as informações de Olá e clique em **instalar**. Quando a instalação estiver concluída, é gerada uma frase de acesso. Irá precisar dela, quando ativar a replicação, por isso, copie-a e mantenha-a numa localização segura.

     ![Adicionar servidor de processos 7](./media/site-recovery-add-process-server/ps-page-8.png)
