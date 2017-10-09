



Dependendo do seu ambiente e opções, script Olá pode criar todos os Olá uma infraestrutura de cluster, incluindo Olá rede virtual do Azure, as contas do storage, cloud services, controlador de domínio, locais ou remotos bases de dados SQL, nó principal e cluster adicional nós. Em alternativa, script Olá pode utilizar a infraestrutura do Azure já existente e criar apenas Olá HPC nós de cluster.

Para obter informações gerais sobre o planeamento de um cluster HPC Pack, consulte Olá [avaliação do produto e planeamento](https://technet.microsoft.com/library/jj899596.aspx) e [introdução](https://technet.microsoft.com/library/jj899590.aspx) conteúdo Olá Biblioteca TechNet do HPC Pack 2012 R2.

## <a name="prerequisites"></a>Pré-requisitos
* **Subscrição do Azure**: pode utilizar uma subscrição em qualquer um dos Olá serviço Global do Azure ou do Azure China. Os limites de subscrição afetam o número de Olá e o tipo de nós de cluster, que pode implementar. Para informações, consulte [subscrição do Azure e limites de serviço, quotas e restrições](../articles/azure-subscription-service-limits.md).
* **Computador de cliente do Windows com o Azure PowerShell 0.8.10 ou posterior instalado e configurado**: consulte [começar com o Azure PowerShell](/powershell/azureps-cmdlets-docs) para instalação de instruções e passos de tooyour de tooconnect subscrição do Azure.
* **Script de implementação de HPC Pack IaaS**: transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Verificar a versão de Olá do script Olá executando `New-HPCIaaSCluster.ps1 –Version`. Este artigo baseia-se numa versão 4.5.2 do script Olá.
* **Ficheiro de script de configuração**: criar um ficheiro XML que script Olá utiliza o cluster do tooconfigure Olá HPC. Para informações e exemplos, consulte as secções mais adiante neste artigo e Olá ficheiro Manual.rtf que acompanha o script de implementação de Olá.

## <a name="syntax"></a>Sintaxe
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Execute o script de Olá como administrador.
> 
> 

### <a name="parameters"></a>Parâmetros
* **ConfigFile**: Especifica o caminho do ficheiro Olá Olá configuração toodescribe Olá HPC do cluster de ficheiros. Ver mais informações sobre o ficheiro de configuração de Olá neste tópico, ou no ficheiro de Olá Manual.rtf na pasta Olá que contém o script de Olá.
* **AdminUserName**: Especifica o nome de utilizador de Olá. Se a floresta de domínio Olá é criada pelo script de Olá, isto torna-se nome de utilizador de administrador local Olá para todas as VMs e nome de administrador de domínio de Olá. Se já existir uma floresta de domínio Olá, isto Especifica o utilizador de domínio Olá Olá tooinstall de nome de utilizador de administrador local HPC Pack.
* **AdminPassword**: Especifica a palavra-passe do administrador Olá. Se não for especificado na linha de comandos Olá, script Olá solicita a sua palavra-passe do tooinput Olá.
* **HPCImageName** (opcional): Especifica o nome de imagem de VM de pacote HPC Olá utilizado cluster do toodeploy Olá HPC. Tem de ser uma imagem fornecida Microsoft HPC Pack de Olá Azure Marketplace. Se não foi especificado Olá (recomendado normalmente), script escolhe Olá mais recente publicada [HPC Pack 2012 R2 imagem](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). imagem mais recente Olá é baseada no Windows Server 2012 R2 Datacenter com o HPC Pack 2012 R2 Update 3 instalado.
  
  > [!NOTE]
  > Falha na implementação se não especificar uma imagem de HPC Pack válida.
  > 
  > 
* **LogFile** (opcional): Especifica o caminho do ficheiro de registo de implementação de Olá. Se não for especificado, o script de Olá cria um ficheiro de registo no diretório temp do Olá do computador Olá executar script de Olá.
* **Force** (opcional): Suprime todos os pedidos de confirmação de Olá.
* **NoCleanOnFailure** (opcional): Especifica que as VMs do Azure que não são implementadas com êxito de Olá não são removidas. Remova estas VMs manualmente antes de executar novamente a implementação de Olá Olá scripts toocontinue ou Olá implementação poderá falhar.
* **PSSessionSkipCACheck** (opcional): para cada serviço em nuvem com as VMs implementadas por este script, é automaticamente gerado um certificado autoassinado pelo Azure e Olá todas as VMs num serviço em nuvem de Olá utilizar este certificado como Olá Windows predefinido Certificado de gestão (WinRM) remoto. funcionalidades HPC toodeploy nestas VMs do Azure, script Olá por predefinição instala temporariamente estes certificados no computador Local de Olá\\arquivo de autoridades de certificação de raiz fidedigna do Olá cliente computador toosuppress Olá "não fidedignos AC" segurança Ocorreu um erro durante a execução do script. certificados de Olá são removidos quando o script de Olá é concluída. Se este parâmetro for especificado, certificados de Olá não estão instalados no computador de cliente Olá e é suprimido aviso de segurança de Olá.
  
  > [!IMPORTANT]
  > Este parâmetro não é recomendado para implementações de produção.
  > 
  > 

### <a name="example"></a>Exemplo
Olá exemplo seguinte cria um cluster HPC Pack utilizando o ficheiro de configuração *MyConfigFile.xml*e especifica as credenciais de administrador para instalar Olá cluster.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Considerações adicionais
* script de Olá, opcionalmente, pode ativar a submissão da tarefa através do portal de web de HPC Pack Olá ou Olá API de REST do HPC Pack.
* script de Olá, opcionalmente, pode executar scripts de prévias e pós-configuração personalizados no nó principal Olá se pretender que o software adicional tooinstall ou configurar outras definições.

## <a name="configuration-file"></a>Ficheiro de configuração
ficheiro de configuração de Olá para o script de implementação de Olá é um ficheiro XML. ficheiro de esquema de Olá HPCIaaSClusterConfig.xsd é na pasta de script de implementação do Olá HPC Pack IaaS. **IaaSClusterConfig** Olá elemento de raiz do ficheiro de configuração de Olá, que contém elementos subordinados de Olá descritos em detalhe no ficheiro de Olá Manual.rtf na pasta de script de implementação de Olá.

