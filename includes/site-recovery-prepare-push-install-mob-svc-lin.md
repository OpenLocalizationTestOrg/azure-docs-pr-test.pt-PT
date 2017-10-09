### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Preparar uma instalação por push num servidor Linux

1. Certifique-se de que existe conectividade de rede entre o computador com Linux Olá e servidor de processos de Olá.
2. Crie uma conta que esse servidor de processos Olá pode utilizar o computador de Olá tooaccess. Olá conta deve ser um **raiz** utilizador no servidor de Linux Olá origem. (Utilize esta conta apenas para a instalação de push Olá e para as atualizações.)
3. Verifique se o ficheiro /etc/hosts Olá na origem de Olá Linux server tem entradas que mapeiam os endereços de tooIP Olá local hostname associados a todas as placas de rede.
4. Instale pacotes de openssh, servidor openssh e openssl mais recentes no Olá no computador de Olá que pretende que o tooreplicate.
5. Certifique-se de que o Secure Shell (SSH) está ativado e em execução na porta 22.
6. Ative a autenticação de subsistema e a palavra-passe SFTP no ficheiro de sshd_config Olá:
  1.  Inicie sessão como **raiz**.
  2.  No Olá ficheiro etc/ssh/ficheiro sshd_config, localizar Olá linha que começa com **PasswordAuthentication**.
  3.  Anule os comentários linha Olá e altere o valor de Olá demasiado**Sim**.
  4.  Linha de Olá localizar que comece com **subsistema** e anule os comentários linha Olá.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Reiniciar Olá **sshd** serviço.

7. Adicione a conta de Olá que criou no CSPSConfigtool.
    1.  Inicie sessão no servidor de configuração tooyour.
    2.  Abra **cspsconfigtool.exe**. (Está disponível como um atalho no ambiente de trabalho Olá e na pasta de %ProgramData%\home\svsystems\bin Olá.)
    3.  No Olá **gerir contas** separador, clique em **adicionar conta**.
    4.  Adicione conta Olá que criou. 
    5.  Introduza as credenciais de Olá que utilizar ao ativar a replicação para um computador.
