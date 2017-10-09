<span data-ttu-id="ad6c6-101">Olá passos toounregister um servidor de processos difere consoante o estado de ligação com hello do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="ad6c6-102">Anule o registo de um servidor de processos que está num estado ligado</span><span class="sxs-lookup"><span data-stu-id="ad6c6-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="ad6c6-103">Remoto no servidor de processos de Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="ad6c6-104">Iniciar Olá **painel de controlo** e abra **programas > desinstalar um programa**</span><span class="sxs-lookup"><span data-stu-id="ad6c6-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="ad6c6-105">Desinstalar um programa por nome de Olá **Microsoft Azure Site Recovery/processo de configuração Server**</span><span class="sxs-lookup"><span data-stu-id="ad6c6-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="ad6c6-106">Depois de concluído o passo 3, pode desinstalar **Configuração/Dependências do Servidor de Processos do Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="ad6c6-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="ad6c6-107">Anule o registo de um servidor de processos que está num estado desligado</span><span class="sxs-lookup"><span data-stu-id="ad6c6-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="ad6c6-108">Olá de utilização abaixo passos deve ser utilizado se não houver nenhuma forma toorevive Olá máquina em que Olá foi instalado o servidor de processos.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="ad6c6-109">Inicie sessão no servidor de configuração tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="ad6c6-110">Abra uma linha de comandos administrativa e procurar no diretório toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="ad6c6-111">Agora, execute o comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="ad6c6-112">Isto irá remover detalhes Olá hello do servidor de processos do sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad6c6-112">This will purge hello details of hello process server from hello system.</span></span>
