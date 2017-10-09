
### <a name="installation-failures"></a>Falhas na instalação
| **Exemplo da mensagem de erro** | **Ação recomendada** |
|--------------------------|------------------------|
|ERRO Falha tooload contas. Erro: System.IO.IOException: ligação de transporte de dados não é possível tooread Olá quando instalar e registar Olá servidor CS.| Certifique-se de que o TLS 1.0 está ativado no computador de Olá. |

### <a name="registration-failures"></a>Falhas de registo
Falhas de registo podem ser debugged revendo os registos de Olá no Olá **%ProgramData%\ASRLogs** pasta.

| **Exemplo da mensagem de erro** | **Ação recomendada** |
|--------------------------|------------------------|
|**09:20:06**:InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>Mensagem: ACS50008: O token SAML é inválido.<br>ID de rastreio: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>ID de correlação: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97 ><br>Carimbo de data/hora: **2016-12-12 14:50:08Z<br>** | Certifique-se de que o tempo de Olá no relógio do seu sistema não é mais de 15 minutos a hora local de Olá. Execute novamente o registo de Olá Olá instalador toocomplete.|
|**09:35:27** : DRRegistrationException enquanto tentava tooget todos os Cofre de recuperação de desastre para o certificado selecionado Olá:: Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException emitiu, Exception.Message: ACS50008: SAML token é inválido.<br>ID de rastreio: e5ad1af1-2d39-4970-8eef-096e325c9950<br>ID de correlação: abe9deb8-3e64-464d-8375-36db9816427a<br>Carimbo de data/hora: **2016-05-19 01:35:39Z**<br> | Certifique-se de que o tempo de Olá no relógio do seu sistema não é mais de 15 minutos a hora local de Olá. Execute novamente o registo de Olá Olá instalador toocomplete.|
|06:28:45: certificado toocreate falhada<br>06:28:45: Não é possível continuar a configuração. Um certificado necessário tooSite tooauthenticate que não é possível criar a recuperação. Execute Novamente a Configuração | Certifique-se de que está a executar o programa de configuração como administrador local. |
