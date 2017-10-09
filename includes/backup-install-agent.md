## <a name="download-install-and-register-hello-azure-backup-agent"></a>Transferir, instalar e registar o agente de cópia de segurança do Azure Olá
Depois de criar o Cofre de cópia de segurança do Azure Olá, deve ser instalado um agente em cada uma das suas máquinas do Windows (Windows Server, cliente Windows, o servidor do System Center Data Protection Manager ou máquina do servidor de cópia de segurança do Azure) que permite fazer cópias de segurança de dados e aplicações tooAzure.

1. Inicie sessão no toohello [Portal de gestão](https://manage.windowsazure.com/)
2. Clique em **dos serviços de recuperação**, em seguida, selecione o Cofre de cópia de segurança Olá que pretende que o tooregister com um servidor. é apresentada a página de início rápido Olá para esse cofre de cópias de segurança.
   
    ![Início rápido](./media/backup-install-agent/quickstart.png)
3. Na página de início rápido de Olá, clique em Olá **cliente para o Windows Server ou o System Center Data Protection Manager ou o Windows** opção em **Transferir agente**. Clique em **guardar** toocopy-toohello de computador local.
   
    ![Guardar o agente](./media/backup-install-agent/agent.png)
4. Depois de instalar o agente de Olá, faça duplo clique MARSAgentInstaller.exe toolaunch Olá instalação Olá cópia de segurança do Azure agente. Escolha a pasta de instalação de Olá e pasta scratch necessário para o agente de Olá. localização da cache Olá especificada tem de ter espaço livre que é, pelo menos, 5% dos dados de cópia de segurança de Olá.
5. Se utilizar um toohello do proxy servidor tooconnect internet, no Olá **configuração de Proxy** ecrã, introduza os detalhes do servidor de proxy Olá. Se utilizar um proxy autenticado, introduza detalhes de nome e palavra-passe de utilizador do Olá neste ecrã.
6. agente de cópia de segurança do Azure Olá instala .NET Framework 4.5 e o Windows PowerShell (se ainda não estiver disponível) toocomplete Olá instalação.
7. Depois de Olá agente estiver instalado, clique em Olá **continuar tooRegistration** toocontinue botão com o fluxo de trabalho Olá.
   
   ![Registar](./media/backup-install-agent/register.png)
8. No ecrã de credenciais de cofre Olá, procure tooand Olá selecione cofre o ficheiro de credenciais que foi anteriormente transferido.
   
    ![Credenciais do Cofre](./media/backup-install-agent/vc.png)
   
    o ficheiro de credenciais do cofre Olá só é válido para 48 horas (após é transferida a partir do portal de Olá). Se encontrar qualquer erro este ecrã (por exemplo "as credenciais do cofre ficheiro fornecido expirou"), início de sessão toohello portal do Azure e as credenciais do Cofre de Olá transferências de ficheiros novamente.
   
    Certifique-se de que esse ficheiro de credenciais de cofre Olá está disponível numa localização que pode ser acedida pela aplicação de configuração de Olá. Se encontrar erros relacionados com de acesso, as credenciais do Cofre de Olá copiar ficheiro tooa localização temporária nesta máquina e repita a operação de Olá.
   
    Se ocorrer um erro de credenciais de cofre inválida (por exemplo "credenciais do cofre inválidas fornecidas") Olá ficheiro está danificado ou não tem credenciais mais recentes Olá associadas ao serviço de recuperação Olá. Repita a operação de Olá depois de transferir um novo ficheiro de credenciais do cofre a partir do portal de Olá. Este erro normalmente é utilizado se o utilizador Olá clica na Olá **credenciais do Cofre de transferência** opção na Olá portal do Azure, sucessivamente rápida. Neste caso, apenas Olá segundo cofre credencial ficheiro é válido.
9. No Olá **definição de encriptação** ecrã, pode gerar uma frase de acesso ou fornecer uma frase de acesso (mínimo de 16 carateres). Lembre-se a frase de acesso do toosave Olá numa localização segura.
   
    ![Encriptação](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Se hello frase de acesso de perda ou esquecimento; Não pode ajudar a Microsoft recuperar dados de cópia de segurança de Olá. utilizador final de Olá possui o frase de acesso de encriptação de Olá e Microsoft não têm visibilidade para o frase de acesso de Olá utilizada pelo utilizador final de Olá. Guarde o ficheiro de Olá numa localização segura conforme necessário durante uma operação de recuperação.
   > 
   > 
10. Assim que clicar em Olá **concluir** botão, hello máquina está registada com êxito toohello cofre e está agora pronto toostart cópia de segurança tooMicrosoft do Azure.
11. Ao utilizar o Microsoft Azure Backup autónomo pode modificar as definições de Olá especificadas durante o fluxo de trabalho do Olá registo clicando no Olá **alterar propriedades** opção na Olá cópia de segurança do Azure mmc snap.
    
    ![Alterar propriedades](./media/backup-install-agent/change.png)
    
    Em alternativa, ao utilizar o Data Protection Manager, pode modificar as definições de Olá especificadas durante o fluxo de trabalho do Olá registo clicando Olá **configurar** opção selecionando **Online** em Olá **Gestão** separador.
    
    ![Configurar o Azure Backup](./media/backup-install-agent/configure.png)

