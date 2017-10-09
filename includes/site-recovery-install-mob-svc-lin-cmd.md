1. <span data-ttu-id="82f10-101">Copie Olá instalador tooa pasta local (por exemplo, /tmp dos) no servidor de Olá que pretende que o tooprotect.</span><span class="sxs-lookup"><span data-stu-id="82f10-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="82f10-102">Num terminal, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="82f10-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="82f10-103">tooinstall serviço de mobilidade, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="82f10-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="82f10-104">Após a conclusão da instalação, Olá serviço de mobilidade tem de servidor de configuração do tooget toohello registado.</span><span class="sxs-lookup"><span data-stu-id="82f10-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="82f10-105">Seguinte Olá execução de comando tooregister Olá serviço de mobilidade com o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="82f10-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="82f10-106">Instalador do serviço de mobilidade da linha de comandos</span><span class="sxs-lookup"><span data-stu-id="82f10-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="82f10-107">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="82f10-107">Parameter</span></span>|<span data-ttu-id="82f10-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="82f10-108">Type</span></span>|<span data-ttu-id="82f10-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="82f10-109">Description</span></span>|<span data-ttu-id="82f10-110">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="82f10-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="82f10-111">-r</span><span class="sxs-lookup"><span data-stu-id="82f10-111">-r</span></span> |<span data-ttu-id="82f10-112">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="82f10-112">Mandatory</span></span>|<span data-ttu-id="82f10-113">Especifica se deve ser instalado o serviço de mobilidade (MS) ou MasterTarget(MT) deve ser instalado</span><span class="sxs-lookup"><span data-stu-id="82f10-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="82f10-114">MS</span><span class="sxs-lookup"><span data-stu-id="82f10-114">MS</span></span> </br> <span data-ttu-id="82f10-115">MT</span><span class="sxs-lookup"><span data-stu-id="82f10-115">MT</span></span>|
|<span data-ttu-id="82f10-116">-d</span><span class="sxs-lookup"><span data-stu-id="82f10-116">-d</span></span> |<span data-ttu-id="82f10-117">Opcional</span><span class="sxs-lookup"><span data-stu-id="82f10-117">Optional</span></span>|<span data-ttu-id="82f10-118">Localização onde será instalado o serviço de mobilidade</span><span class="sxs-lookup"><span data-stu-id="82f10-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="82f10-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="82f10-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="82f10-120">-v</span><span class="sxs-lookup"><span data-stu-id="82f10-120">-v</span></span>|<span data-ttu-id="82f10-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="82f10-121">Mandatory</span></span>|<span data-ttu-id="82f10-122">Especifica a plataforma de Olá no qual Olá serviço de mobilidade está a obter instalado</span><span class="sxs-lookup"><span data-stu-id="82f10-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="82f10-123">- **VMware** : Utilize este valor se estiver a instalar o serviço de mobilidade numa VM em execução no *VMware vSphere anfitriões ESXi*, *anfitriões Hyper-V* e *Phsyical servidores*</span><span class="sxs-lookup"><span data-stu-id="82f10-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="82f10-124">- **Azure** : Utilize este valor se estiver a instalar o agente de uma VM do IaaS do Azure</span><span class="sxs-lookup"><span data-stu-id="82f10-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="82f10-125">VMware</span><span class="sxs-lookup"><span data-stu-id="82f10-125">VMware</span></span> </br> <span data-ttu-id="82f10-126">Azure</span><span class="sxs-lookup"><span data-stu-id="82f10-126">Azure</span></span>|
|<span data-ttu-id="82f10-127">-q</span><span class="sxs-lookup"><span data-stu-id="82f10-127">-q</span></span>|<span data-ttu-id="82f10-128">Opcional</span><span class="sxs-lookup"><span data-stu-id="82f10-128">Optional</span></span>|<span data-ttu-id="82f10-129">Especifica o instalador toorun em modo silencioso</span><span class="sxs-lookup"><span data-stu-id="82f10-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="82f10-130">N/D</span><span class="sxs-lookup"><span data-stu-id="82f10-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="82f10-131">Configuração do serviço de mobilidade da linha de comandos</span><span class="sxs-lookup"><span data-stu-id="82f10-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="82f10-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="82f10-132">Parameter</span></span>|<span data-ttu-id="82f10-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="82f10-133">Type</span></span>|<span data-ttu-id="82f10-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="82f10-134">Description</span></span>|<span data-ttu-id="82f10-135">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="82f10-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="82f10-136">-i</span><span class="sxs-lookup"><span data-stu-id="82f10-136">-i</span></span> |<span data-ttu-id="82f10-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="82f10-137">Mandatory</span></span>|<span data-ttu-id="82f10-138">IP de hello do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="82f10-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="82f10-139">Qualquer endereço IP válido</span><span class="sxs-lookup"><span data-stu-id="82f10-139">Any valid IP Address</span></span>|
|<span data-ttu-id="82f10-140">-P</span><span class="sxs-lookup"><span data-stu-id="82f10-140">-P</span></span> |<span data-ttu-id="82f10-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="82f10-141">Mandatory</span></span>|<span data-ttu-id="82f10-142">Ficheiro de Olá de caminho de ficheiro completo onde o frase de acesso de ligação de Olá é guardado</span><span class="sxs-lookup"><span data-stu-id="82f10-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="82f10-143">Qualquer pasta válido</span><span class="sxs-lookup"><span data-stu-id="82f10-143">Any valid folder</span></span>|
