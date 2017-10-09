Olá passos toounregister um servidor de processos difere consoante o estado de ligação com hello do servidor de configuração.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Anule o registo de um servidor de processos que está num estado ligado

1. Remoto no servidor de processos de Olá como administrador.
2. Iniciar Olá **painel de controlo** e abra **programas > desinstalar um programa**
3. Desinstalar um programa por nome de Olá **Microsoft Azure Site Recovery/processo de configuração Server**
4. Depois de concluído o passo 3, pode desinstalar **Configuração/Dependências do Servidor de Processos do Microsoft Azure Site Recovery**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Anule o registo de um servidor de processos que está num estado desligado

> [!WARNING]
> Olá de utilização abaixo passos deve ser utilizado se não houver nenhuma forma toorevive Olá máquina em que Olá foi instalado o servidor de processos.

1. Inicie sessão no servidor de configuração tooyour como administrador.
2. Abra uma linha de comandos administrativa e procurar no diretório toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. Agora, execute o comando de Olá.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Isto irá remover detalhes Olá hello do servidor de processos do sistema de Olá.
