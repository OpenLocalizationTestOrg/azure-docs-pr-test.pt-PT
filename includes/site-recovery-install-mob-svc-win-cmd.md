1. Copie a pasta local do Olá instalador tooa (por exemplo, C:\Temp) no servidor de Olá que pretende que o tooprotect. Execute os seguintes comandos como administrador, numa linha de comandos de Olá:

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall serviço de mobilidade, execute Olá os seguintes comandos:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Agora o agente de Olá tem toobe registado hello do servidor de configuração.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>Argumentos da linha de comandos de instalador do serviço de mobilidade

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| Parâmetro|Tipo|Descrição|Valores possíveis|
|-|-|-|-|
|/ Função|Obrigatório|Especifica se deve ser instalado o serviço de mobilidade (MS) ou MasterTarget(MT) deve ser instalado|MS </br> MT|
|/InstallLocation|Opcional|Localização onde o serviço de mobilidade está instalado|Qualquer pasta no computador de Olá|
|/ Plataforma|Obrigatório|Especifica a plataforma de Olá no qual Olá serviço de mobilidade está a obter instalado </br> </br>- **VMware** : Utilize este valor se estiver a instalar o serviço de mobilidade numa VM em execução no *VMware vSphere anfitriões ESXi*, *anfitriões Hyper-V* e *Phsyical servidores* </br> - **Azure** : Utilize este valor se estiver a instalar o agente de uma VM do IaaS do Azure| VMware </br> Azure|
|/ Automática|Opcional|Especifica o instalador de Olá toorun em modo silencioso| ND|

>[!TIP]
> registos de configuração de Olá podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Argumentos da linha de comandos de registo do serviço de mobilidade

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Parâmetro|Tipo|Descrição|Valores possíveis|
  |-|-|-|-|
  |/ CSEndPoint |Obrigatório|Endereço IP do servidor de configuração de Olá| Qualquer endereço IP válido|
  |/PassphraseFilePath|Obrigatório|Localização do Olá frase de acesso |Qualquer UNC válido ou o caminho do ficheiro local|


>[!TIP]
> Olá AgentConfiguration registos podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
