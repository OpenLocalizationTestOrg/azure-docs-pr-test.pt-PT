1. Copie Olá instalador tooa pasta local (por exemplo, /tmp dos) no servidor de Olá que pretende que o tooprotect. Num terminal, execute Olá os seguintes comandos:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall serviço de mobilidade, execute Olá os seguintes comandos:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Após a conclusão da instalação, Olá serviço de mobilidade tem de servidor de configuração do tooget toohello registado. Seguinte Olá execução de comando tooregister Olá serviço de mobilidade com o servidor de configuração.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Instalador do serviço de mobilidade da linha de comandos

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parâmetro|Tipo|Descrição|Valores possíveis|
|-|-|-|-|
|-r |Obrigatório|Especifica se deve ser instalado o serviço de mobilidade (MS) ou MasterTarget(MT) deve ser instalado|MS </br> MT|
|-d |Opcional|Localização onde será instalado o serviço de mobilidade|/usr/local/ASR|
|-v|Obrigatório|Especifica a plataforma de Olá no qual Olá serviço de mobilidade está a obter instalado </br> </br>- **VMware** : Utilize este valor se estiver a instalar o serviço de mobilidade numa VM em execução no *VMware vSphere anfitriões ESXi*, *anfitriões Hyper-V* e *Phsyical servidores* </br> - **Azure** : Utilize este valor se estiver a instalar o agente de uma VM do IaaS do Azure| VMware </br> Azure|
|-q|Opcional|Especifica o instalador toorun em modo silencioso| N/D|


#### <a name="mobility-service-configuration-command-line"></a>Configuração do serviço de mobilidade da linha de comandos

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parâmetro|Tipo|Descrição|Valores possíveis|
|-|-|-|-|
|-i |Obrigatório|IP de hello do servidor de configuração|Qualquer endereço IP válido|
|-P |Obrigatório|Ficheiro de Olá de caminho de ficheiro completo onde o frase de acesso de ligação de Olá é guardado|Qualquer pasta válido|
