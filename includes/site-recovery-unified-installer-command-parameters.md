|Nome do Parâmetro| Tipo | Descrição| Valores Possíveis|
|-|-|-|-|
| /ServerMode|Obrigatório|Especifica se ambos os servidores de configuração e o processo de Olá devem ser instalados, ou apenas o servidor de processos Olá|CS<br>PS|
|/InstallLocation|Obrigatório|pasta de Olá que Olá componentes são instalados| Qualquer pasta no computador de Olá|
|/MySQLCredsFilePath|Obrigatório|caminho do ficheiro Olá na qual Olá MySQL são armazenadas as credenciais do servidor|ficheiro de Olá deve ter o formato de Olá especificado abaixo|
|/VaultCredsFilePath|Obrigatório|caminho de Olá do ficheiro de credenciais de cofre Olá|Caminho do ficheiro válido|
|/EnvType|Obrigatório|Tipo de envrionment que pretende que o tooprotect |VMware<br>NonVMware|
|/PSIP|Obrigatório|Endereço IP do Olá NIC toobe utilizado para a transferência de dados de replicação| Qualquer endereço IP válido|
|/CSIP|Obrigatório|endereço IP Olá de NIC Olá no qual Olá servidor de configuração está a escutar| Qualquer endereço IP válido|
|/PassphraseFilePath|Obrigatório|Olá toolocation de caminho completo do ficheiro do Olá frase de acesso|Caminho do ficheiro válido|
|/BypassProxy|Opcional|Especifica que o servidor configuração Olá liga tooAzure sem um proxy|toodo obter este valor de Venu|
|/ProxySettingsFilePath|Opcional|Definições de proxy (Olá predefinido proxy precise de autenticação ou um proxy personalizado)|ficheiro de Olá deve estar no formato de Olá especificado abaixo|
|DataTransferSecurePort|Opcional|Número da porta no Olá PSIP toobe utilizada para dados de replicação| Número de Porta Válido (o valor predefinido é 9433)|
|/SkipSpaceCheck|Opcional|Ignorar a verificação de espaços para a cache do disco| |
|/AcceptThirdpartyEULA|Obrigatório|O sinalizador indica a aceitação do EULA de terceiros| |
|/ShowThirdpartyEULA|Opcional|Apresenta o EULA de terceiros. Se for fornecido como entrada, todos os outros parâmetros são ignorados| |
