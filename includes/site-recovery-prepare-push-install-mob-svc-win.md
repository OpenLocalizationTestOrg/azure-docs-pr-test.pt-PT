### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Preparar para uma instalação de push num computador Windows

1. Certifique-se de que existe conectividade de rede entre o computador com o Windows hello e servidor de processos de Olá.
2. Crie uma conta que esse servidor de processos Olá pode utilizar o computador de Olá tooaccess. conta de Olá deve ter direitos de administrador (locais ou domínio). (Utilize esta conta apenas para a instalação de push Olá e para as atualizações de agente.)

   > [!NOTE]
   > Se não estiver a utilizar uma conta de domínio, desative o controlo de acesso de utilizador remoto no computador local Olá. toodisable controlo de acesso de utilizador remoto, na chave de registo de HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System Olá, adicione um novo DWORD: **LocalAccountTokenFilterPolicy**. Defina o valor de Olá demasiado**1**. toodo num comando de linha de comandos, execute Olá os seguintes comandos:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. Na Firewall do Windows no computador de Olá pretende tooprotect, selecione **permitir que uma aplicação ou funcionalidade através da Firewall**. Ativar **impressora partilha de ficheiros e** e **Windows Management Instrumentation (WMI)**. Para computadores que pertencem tooa domínio, pode configurar as definições da firewall Olá utilizando um objeto de política de grupo (GPO).

   ![Definições de firewall](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Adicione a conta de Olá que criou no CSPSConfigtool.
    1.  Inicie sessão no servidor de configuração tooyour.
    2.  Abra **cspsconfigtool.exe**. (Está disponível como um atalho no ambiente de trabalho Olá e na pasta de %ProgramData%\home\svsystems\bin Olá.)
    3.  No Olá **gerir contas** separador, selecione **adicionar conta**.
    4.  Adicione conta Olá que criou.
    5.  Introduza as credenciais de Olá que utilizar ao ativar a replicação para um computador.
