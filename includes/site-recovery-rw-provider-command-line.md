UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ InstallDrive <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe de endereços IP utilizado para a transferência de dados] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parâmetros:

* /ServerMode: obrigatório. Especifica se ambos os servidores de configuração e o processo de Olá devem ser instalados, ou apenas o servidor de processos Olá. Valores de entrada: CS, PS.
* InstallLocation: obrigatório. pasta de Olá que Olá componentes são instalados.
* /MySQLCredsFilePath. Obrigatório. caminho do ficheiro Olá na qual Olá MySQL são armazenadas as credenciais do servidor. ficheiro de Olá deve estar no formato:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Obrigatório. localização de Olá do ficheiro de credenciais de cofre Olá
* /EnvType. Obrigatório. tipo de Olá de instalação. Valores: VMware, NonVMware
* /PSIP e /CSIP. Obrigatório. endereço IP de Hello do servidor de processos de Olá e servidor de configuração.
* /PassphraseFilePath. Obrigatório. localização de Olá do ficheiro do Olá frase de acesso.
* /BypassProxy. Opcional. Especifica que o servidor configuração Olá liga tooAzure sem um proxy.
* /ProxySettingsFilePath. Opcional. Definições de proxy (Olá predefinido proxy precise de autenticação ou um proxy personalizado). ficheiro de Olá deve estar no formato:
* [ProxySettings]
* ProxyAuthentication = "Sim/não"
* Proxy IP = "Endereço IP>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. Opcional. número de porta de Olá para dados de replicação.
* SkipSpaceCheck. Opcional. Ignorar a verificação de espaços para a cache.
* AcceptThirdpartyEULA. Obrigatório. Aceita Olá EULA de terceiros.
* ShowThirdpartyEULA. Obrigatório. Apresenta o EULA de terceiros. Se for fornecido como entrada, todos os outros parâmetros são ignorados.
