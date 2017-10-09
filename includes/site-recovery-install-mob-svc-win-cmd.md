1. <span data-ttu-id="20e2c-101">Copie a pasta local do Olá instalador tooa (por exemplo, C:\Temp) no servidor de Olá que pretende que o tooprotect.</span><span class="sxs-lookup"><span data-stu-id="20e2c-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="20e2c-102">Execute os seguintes comandos como administrador, numa linha de comandos de Olá:</span><span class="sxs-lookup"><span data-stu-id="20e2c-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="20e2c-103">tooinstall serviço de mobilidade, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="20e2c-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="20e2c-104">Agora o agente de Olá tem toobe registado hello do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="20e2c-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="20e2c-105">Argumentos da linha de comandos de instalador do serviço de mobilidade</span><span class="sxs-lookup"><span data-stu-id="20e2c-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="20e2c-106">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="20e2c-106">Parameter</span></span>|<span data-ttu-id="20e2c-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="20e2c-107">Type</span></span>|<span data-ttu-id="20e2c-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="20e2c-108">Description</span></span>|<span data-ttu-id="20e2c-109">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="20e2c-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="20e2c-110">/ Função</span><span class="sxs-lookup"><span data-stu-id="20e2c-110">/Role</span></span>|<span data-ttu-id="20e2c-111">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="20e2c-111">Mandatory</span></span>|<span data-ttu-id="20e2c-112">Especifica se deve ser instalado o serviço de mobilidade (MS) ou MasterTarget(MT) deve ser instalado</span><span class="sxs-lookup"><span data-stu-id="20e2c-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="20e2c-113">MS</span><span class="sxs-lookup"><span data-stu-id="20e2c-113">MS</span></span> </br> <span data-ttu-id="20e2c-114">MT</span><span class="sxs-lookup"><span data-stu-id="20e2c-114">MT</span></span>|
|<span data-ttu-id="20e2c-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="20e2c-115">/InstallLocation</span></span>|<span data-ttu-id="20e2c-116">Opcional</span><span class="sxs-lookup"><span data-stu-id="20e2c-116">Optional</span></span>|<span data-ttu-id="20e2c-117">Localização onde o serviço de mobilidade está instalado</span><span class="sxs-lookup"><span data-stu-id="20e2c-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="20e2c-118">Qualquer pasta no computador de Olá</span><span class="sxs-lookup"><span data-stu-id="20e2c-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="20e2c-119">/ Plataforma</span><span class="sxs-lookup"><span data-stu-id="20e2c-119">/Platform</span></span>|<span data-ttu-id="20e2c-120">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="20e2c-120">Mandatory</span></span>|<span data-ttu-id="20e2c-121">Especifica a plataforma de Olá no qual Olá serviço de mobilidade está a obter instalado</span><span class="sxs-lookup"><span data-stu-id="20e2c-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="20e2c-122">- **VMware** : Utilize este valor se estiver a instalar o serviço de mobilidade numa VM em execução no *VMware vSphere anfitriões ESXi*, *anfitriões Hyper-V* e *Phsyical servidores*</span><span class="sxs-lookup"><span data-stu-id="20e2c-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="20e2c-123">- **Azure** : Utilize este valor se estiver a instalar o agente de uma VM do IaaS do Azure</span><span class="sxs-lookup"><span data-stu-id="20e2c-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="20e2c-124">VMware</span><span class="sxs-lookup"><span data-stu-id="20e2c-124">VMware</span></span> </br> <span data-ttu-id="20e2c-125">Azure</span><span class="sxs-lookup"><span data-stu-id="20e2c-125">Azure</span></span>|
|<span data-ttu-id="20e2c-126">/ Automática</span><span class="sxs-lookup"><span data-stu-id="20e2c-126">/Silent</span></span>|<span data-ttu-id="20e2c-127">Opcional</span><span class="sxs-lookup"><span data-stu-id="20e2c-127">Optional</span></span>|<span data-ttu-id="20e2c-128">Especifica o instalador de Olá toorun em modo silencioso</span><span class="sxs-lookup"><span data-stu-id="20e2c-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="20e2c-129">ND</span><span class="sxs-lookup"><span data-stu-id="20e2c-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="20e2c-130">registos de configuração de Olá podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="20e2c-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="20e2c-131">Argumentos da linha de comandos de registo do serviço de mobilidade</span><span class="sxs-lookup"><span data-stu-id="20e2c-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="20e2c-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="20e2c-132">Parameter</span></span>|<span data-ttu-id="20e2c-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="20e2c-133">Type</span></span>|<span data-ttu-id="20e2c-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="20e2c-134">Description</span></span>|<span data-ttu-id="20e2c-135">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="20e2c-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="20e2c-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="20e2c-136">/CSEndPoint</span></span> |<span data-ttu-id="20e2c-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="20e2c-137">Mandatory</span></span>|<span data-ttu-id="20e2c-138">Endereço IP do servidor de configuração de Olá</span><span class="sxs-lookup"><span data-stu-id="20e2c-138">IP address of hello configuration server</span></span>| <span data-ttu-id="20e2c-139">Qualquer endereço IP válido</span><span class="sxs-lookup"><span data-stu-id="20e2c-139">Any valid IP address</span></span>|
  |<span data-ttu-id="20e2c-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="20e2c-140">/PassphraseFilePath</span></span>|<span data-ttu-id="20e2c-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="20e2c-141">Mandatory</span></span>|<span data-ttu-id="20e2c-142">Localização do Olá frase de acesso</span><span class="sxs-lookup"><span data-stu-id="20e2c-142">Location of hello passphrase</span></span> |<span data-ttu-id="20e2c-143">Qualquer UNC válido ou o caminho do ficheiro local</span><span class="sxs-lookup"><span data-stu-id="20e2c-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="20e2c-144">Olá AgentConfiguration registos podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="20e2c-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
