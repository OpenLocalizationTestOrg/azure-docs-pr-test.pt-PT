---
title: "Diagnóstico no Azure Stack"
description: "Como recolher ficheiros de registo para obter um diagnóstico na pilha do Azure"
services: azure-stack
author: jeffgilb
manager: femila
cloud: azure-stack
ms.service: azure-stack
ms.topic: article
ms.date: 12/15/2017
ms.author: jeffgilb
ms.reviewer: adshar
ms.openlocfilehash: e823aeb4291b3e765b35181c24b41fa58c170cca
ms.sourcegitcommit: 5108f637c457a276fffcf2b8b332a67774b05981
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/17/2018
---
# <a name="azure-stack-diagnostics-tools"></a>Ferramentas de diagnóstico de pilha do Azure

*Aplica-se a: Azure pilha integrado sistemas e Kit de desenvolvimento de pilha do Azure*
 
Pilha do Azure é uma coleção grande de componentes de trabalhar em conjunto e interagir entre si. Todos estes componentes geram os seus próprios registos exclusivos. Isto pode fazer diagnosticar problemas com uma tarefa difícil, especialmente para erros provenientes de vários interação de componentes de pilha do Azure. 

A nossa ferramentas de diagnóstico garantir que o mecanismo de coleção de registo é fácil e eficiente. O diagrama seguinte mostra como iniciar ferramentas de recolha em projetos de pilha do Azure:

![Ferramentas de diagnóstico de pilha do Azure](media/azure-stack-diagnostics/get-azslogs.png)
 
 
## <a name="trace-collector"></a>Recoletor de rastreio
 
O Recoletor do rastreio está ativado por predefinição e é executada continuamente em segundo plano para recolher todos os registos de rastreio de eventos para o Windows (ETW) de serviços de componentes de pilha do Azure. Os registos de ETW são armazenados numa partilha local comuns com um limite de antiguidade de cinco dias. Assim que este limite for atingido, os ficheiros mais antigos são eliminados como são criados novos. O predefinição o tamanho máximo permitido para cada ficheiro é 200 MB. Uma verificação de tamanho ocorre a cada 2 minutos, e se o ficheiro atual é > = 200 MB, é guardado e é gerado um novo ficheiro. Há também um limite de 8 GB no tamanho total do ficheiro gerado por sessão do evento. 

## <a name="log-collection-tool"></a>Ferramenta de registo de coleção
 
O cmdlet do PowerShell **Get-AzureStackLog** pode ser utilizado para recolher registos de todos os componentes de um ambiente de pilha do Azure. Guarda-las nos ficheiros zip numa localização definida pelo utilizador. Se a equipa de suporte técnico de pilha do Azure tem dos registos para ajudar a resolver um problema, estes poderão pedir-lhe para executar esta ferramenta.

> [!CAUTION]
> Estes ficheiros de registo podem conter informações de identificação pessoal (PII). Ter isto em consideração antes de a publica publicamente quaisquer ficheiros de registo.
 
Seguem-se alguns tipos de registo de exemplo que são recolhidos:
*   **Registos de implementação de pilha do Azure**
*   **Registos de eventos do Windows**
*   **Registos de Panther**
*   **Registos de cluster**
*   **Registos de diagnóstico de armazenamento**
*   **Registos ETW**

Estes ficheiros são recolhidos e guardados numa partilha pelo Recoletor do rastreio. O **Get-AzureStackLog** cmdlet do PowerShell, em seguida, pode ser utilizado para recolhê-las quando for necessário.
 
### <a name="to-run-get-azurestacklog-on-an-azure-stack-development-kit-asdk-system"></a>Para executar Get-AzureStackLog num sistema Kit de desenvolvimento de pilha do Azure (ASDK)
1. Inicie sessão como **AzureStack\CloudAdmin** no anfitrião.
2. Abra uma janela do PowerShell como administrador.
3. Execute o **Get-AzureStackLog** cmdlet do PowerShell.

**Exemplos:**

  Recolha todos os registos para todas as funções:

  ```powershell
  Get-AzureStackLog -OutputPath C:\AzureStackLogs
  ```

  Recolha registos de funções VirtualMachines e BareMetal:

  ```powershell
  Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal
  ```

  Recolha registos de funções VirtualMachines e BareMetal, com data de filtragem de ficheiros de registo para as últimos 8 horas:
    
  ```powershell
  Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8)
  ```

  Recolha registos de funções VirtualMachines e BareMetal, com data de filtragem de ficheiros de registo para o período de tempo entre 8 horas e há a 2 horas:

  ```powershell
  Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date).AddHours(-2)
  ```

### <a name="to-run-get-azurestacklog-on-an-azure-stack-integrated-system"></a>Para executar Get-AzureStackLog uma pilha do Azure integrado no sistema

Para executar a ferramenta de coleção de registo num sistema integrado, tem de ter acesso ao ponto final com privilégios (PEP). Eis um script de exemplo, pode executar utilizando o PEP para recolher registos num sistema integrado:

```powershell
$ip = "<IP ADDRESS OF THE PEP VM>" # You can also use the machine name instead of IP here.
 
$pwd= ConvertTo-SecureString "<CLOUD ADMIN PASSWORD>" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("<DOMAIN NAME>\CloudAdmin", $pwd)
 
$shareCred = Get-Credential
 
$s = New-PSSession -ComputerName $ip -ConfigurationName PrivilegedEndpoint -Credential $cred

$fromDate = (Get-Date).AddHours(-8)
$toDate = (Get-Date).AddHours(-2)  #provide the time that includes the period for your issue
 
Invoke-Command -Session $s {    Get-AzureStackLog -OutputPath "\\<HLH MACHINE ADDRESS>\c$\logs" -OutputSharePath "<EXTERNAL SHARE ADDRESS>" -OutputShareCredential $using:shareCred  -FilterByRole Storage -FromDate $using:fromDate -ToDate $using:toDate}

if($s)
{
    Remove-PSSession $s
}
```

- Quando recolher os registos a partir de PEP, especifique o **OutputPath** parâmetro seja uma localização no computador anfitrião de ciclo de vida de Hardware (HLH). Certifique-se também de que a localização está encriptada.
- Os parâmetros **OutputSharePath** e **OutputShareCredential** são opcionais e são utilizadas quando carregar os registos para uma pasta partilhada externa. Utilize estes parâmetros *Ademais* para **OutputPath**. Se **OutputPath** não for especificado, a ferramenta de registo de coleção utiliza a unidade de sistema da PEP VM para armazenamento. Isto poderá originar o script falhou porque o espaço de disco é limitado.
- Conforme mostrado no exemplo anterior, o **FromDate** e **ToDate** parâmetros podem ser utilizados para recolher registos para um período de tempo específico. Isto pode ter de útil para cenários como recolher registos depois de aplicar um pacote de atualização num sistema integrado.

### <a name="parameter-considerations-for-both-asdk-and-integrated-systems"></a>Considerações de parâmetro para ASDK e sistemas integrados

- Se o **FromDate** e **ToDate** não foram especificados parâmetros, os registos serão recolhidos as últimos quatro horas por predefinição.
- Pode utilizar o **TimeOutInMinutes** parâmetro para definir o tempo limite para a recolha de registos. Está definido para 150 (horas 2,5) por predefinição.

- Atualmente, pode utilizar o **FilterByRole** parâmetro para recolha de registos de filtro para as seguintes funções:

   |   |   |   |
   | - | - | - |
   | ACSMigrationService     | ACSMonitoringService   | ACSSettingsService |
   | ACS                     | ACSFabric              | ACSFrontEnd        |
   | ACSTableMaster          | ACSTableServer         | ACSWac             |
   | ADFS                    | ASAppGateway           | BareMetal          |
   | BRP                     | AC                     | CPI                |
   | CRP                     | DeploymentMachine      | DHCP               |
   | Domínio                  | ECE                    | ECESeedRing        | 
   | FabricRing              | FabricRingServices     | FRP                |
   | Gateway                 | HealthMonitoring       | HRP                |   
   | IBC                     | InfraServiceController | KeyVaultAdminResourceProvider|
   | KeyVaultControlPlane    | KeyVaultDataPlane      | NC                 |   
   | NonPrivilegedAppGateway | NRP                    | SeedRing           |
   | SeedRingServices        | SLB                    | SQL                |   
   | SRP                     | Armazenamento                | StorageController  |
   | URP                     | UsageBridge            | virtualMachines    |  
   | FOI                     | WASPUBLIC              | WDS                |


### <a name="bkmk_gui"></a>Recolher registos utilizando uma interface gráfica do utilizador
Em vez de fornecer os parâmetros necessários para o cmdlet Get-AzureStackLog obter registos de pilha do Azure, também pode tirar partido das ferramentas de pilha do Azure disponíveis open source para localizado no principal do Azure pilha ferramentas ferramentas repositório do GitHub em http://aka.ms/AzureStackTools.

O **ERCS_AzureStackLogs.ps1** é armazenado no repositório GitHub ferramentas de script do PowerShell e é atualizado regularmente. Para se certificar de que tem a versão mais recente disponível, deve transferi-lo diretamente a partir do http://aka.ms/ERCS. O script iniciada a partir de uma sessão do PowerShell administrativa, liga ao ponto final com privilégios e executa o Get-AzureStackLog com parâmetros fornecidos. Se não existem parâmetros são fornecidos, o script será assumida a pedir para os parâmetros através de uma interface gráfica do utilizador.

Para saber mais sobre o script do ERCS_AzureStackLogs.ps1 PowerShell, pode ver [um breve vídeo](https://www.youtube.com/watch?v=Utt7pLsXEBc) ou ver o script [ficheiro Leia-me](https://github.com/Azure/AzureStack-Tools/blob/master/Support/ERCS_Logs/ReadMe.md) localizado no repositório do GitHub de ferramentas de pilha do Azure. 

### <a name="additional-considerations"></a>Considerações adicionais

* O comando demora algum tempo para executar com base nos que funções selecionadas os registos estão a recolher. Fatores coadjuvantes também incluem a duração de tempo especificada para a recolha de registos e o número de nós no ambiente de pilha do Azure.
* Após a conclusão da recolha de registos, consulte a nova pasta que criou no **OutputPath** parâmetro especificado no comando.
* Cada função tem os seus registos dentro ficheiros zip individuais. Dependendo do tamanho dos registos recolhidos, uma função tem os seus registos dividida em múltiplos ficheiros zip. Para uma função, se pretende que todos os ficheiros de registo deszipados para uma única pasta, utilize uma ferramenta que pode deszipe em massa (por exemplo, 7zip). Selecione todos os ficheiros zipped para a função e selecione **extrair aqui**. Isto unzips todos os ficheiros de registo para essa função numa única pasta intercalada.
* Um ficheiro chamado **Get-AzureStackLog_Output.log** também é criado na pasta que contém os ficheiros de registo zipped. Este ficheiro é um registo de resultado do comando, o que pode ser utilizado para resolver problemas durante a recolha de registos.
* Para investigar uma falha específica, podem ser necessária, registos de mais do que um componente.
    -   Registos de eventos para todas as VMs de infraestrutura e de sistema são recolhidos no *VirtualMachines* função.
    -   Sistema e os registos de eventos de todos os anfitriões são recolhidos no *BareMetal* função.
    -   Registos de eventos de Cluster de ativação pós-falha e Hyper-V são recolhidos no *armazenamento* função.
    -   ACS registos são recolhidos no *armazenamento* e *ACS* funções.

> [!NOTE]
> Os limites de tamanho e a idade são impostos os registos recolhidos conforme é essencial para garantir uma utilização eficiente do seu espaço de armazenamento para garantir não recebem flooded com os registos em. No entanto, quando diagnosticar um problema, por vezes, precisa de registos que poderão já não existir devido a estes limites. Assim, é **altamente recomendado** descarga dos registos para um espaço de armazenamento externo (uma conta de armazenamento no Azure, um dispositivo de armazenamento adicional no local etc.) a cada 8 a 12 horas e mantê-las existe de 1 a 3 meses, consoante o requisitos. Além disso, certifique-se que esta localização de armazenamento é encriptada.

## <a name="next-steps"></a>Passos Seguintes
[Resolução de problemas de pilha do Microsoft Azure](azure-stack-troubleshooting.md)

