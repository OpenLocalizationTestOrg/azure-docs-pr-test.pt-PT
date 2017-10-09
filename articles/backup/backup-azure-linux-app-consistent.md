---
title: "Cópia de segurança do Azure: consistentes com aplicações as cópias de segurança de VMs do Linux | Microsoft Docs"
description: "Utilize scripts tooguarantee cópias de segurança consistentes com aplicações tooAzure, para as máquinas virtuais do Linux. scripts de Olá aplicam-se apenas tooLinux VMs numa implementação do Resource Manager; scripts de Olá não aplicam tooWindows VMs ou implementações do service manager. Este artigo orienta-Olá os passos para configurar scripts Olá, incluindo a resolução de problemas."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "cópia de segurança consistentes da aplicação; cópia de segurança de VM do Azure com consistência de aplicações; Cópia de segurança de VM com Linux; Cópia de segurança do Azure"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Cópia de segurança consistentes com aplicações das VMs do Linux do Azure (pré-visualização)

Este artigo aborda Olá pré-scripts de Linux e script pós-implementação framework, e como pode ser utilizado tootake consistentes com aplicações as cópias de segurança de VMs do Linux do Azure.

> [!Note]
> arquitetura de pré- script de e scripts pós-implementação Olá só é suportada para máquinas virtuais do Linux implementadas no Azure Resource Manager. Scripts de consistência de aplicações não são suportados para máquinas de virtuais implementadas no Service Manager ou máquinas virtuais do Windows.
>

## <a name="how-hello-framework-works"></a>Como funciona o framework Olá

framework Olá fornece uma opção toorun pré-scripts de personalizados e scripts pós-cópia enquanto estiver a ser instantâneos VM. Pré-scripts são executados imediatamente antes de tirar o instantâneo VM Olá e scripts pós-implementação são executadas imediatamente depois de tomar instantâneo VM Olá. Este oferece Olá flexibilidade toocontrol sua aplicação e o ambiente enquanto estiver a ser instantâneos VM.

Neste cenário, é importante tooensure consistentes com aplicações cópia de segurança. pré-scripts de Olá podem invocar a aplicação nativa APIs tooquiesce Olá IOs e descarregar o disco de toohello conteúdo dentro da memória. Isto garante que instantâneo Olá é consistente com aplicações (ou seja, essa aplicação Olá é apresentada quando Olá VM arranca pós-restauro). Script de pós-implementação pode ser utilizado toothaw Olá IOs. Fazê-lo ao utilizando APIs de aplicação nativa para que a aplicação Olá possa retomar o instantâneo de post VM operações normais.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Passos tooconfigure pré- script de e script pós-implementação

1. Inicie sessão no Olá raiz utilizador toohello VM com Linux que pretende que sejam tooback cópias de segurança.

2. Transferir **VMSnapshotScriptPluginConfig.json** de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)e, em seguida, copie-toohello **etc/azure** pasta em todas as VMs de Olá que vai tooback cópias de segurança. Criar Olá **etc/azure** diretório se não existir já.

3. Copie Olá pré- script de e script pós-implementação para a sua aplicação no Olá todas as VMs que planeia tooback cópias de segurança. Pode copiar Olá scripts tooany localização Olá VM. Ser tooupdate se caminho completo do Olá de Olá ficheiros de script no Olá **VMSnapshotScriptPluginConfig.json** ficheiro.

4. Certifique-se Olá as seguintes permissões para estes ficheiros:

   - **VMSnapshotScriptPluginConfig.json**: permissão "600." Por exemplo, apenas os utilizadores "raiz" devem ter o ficheiro de toothis de permissões "leitura" e "escrita" e nenhum utilizador deve ter permissões de "executar".

   - **Ficheiro de pré-script de**: permissão "700."  Por exemplo, o utilizador de "raiz" só deve ter "ler", "escrita" e "executar" ficheiro de toothis de permissões.
  
   - **Script de pós-implementação** permissão "700." Por exemplo, o utilizador de "raiz" só deve ter "ler", "escrita" e "executar" ficheiro de toothis de permissões.

   > [!Important]
   > arquitetura de Olá fornece aos utilizadores uma grande quantidade de energia. É importante que é seguro e esse utilizador de "raiz" apenas tem acesso toocritical ficheiros JSON e o script.
   > Se os requisitos de Olá anteriores não forem cumpridos, o script de Olá não executado. Isto resulta numa cópia de segurança consistentes do sistema/falhas de ficheiros.
   >

5. Configurar **VMSnapshotScriptPluginConfig.json** conforme descrito aqui:
    - **pluginName**: deixe este campo como está ou os scripts poderão não funcionar conforme esperado.

    - **preScriptLocation**: forneça o caminho completo do Olá do pré-script de Olá no Olá da toobe do uma cópia de segurança de VM.

    - **postScriptLocation**: forneça o caminho completo do Olá do script de pós-implementação Olá no Olá da toobe do uma cópia de segurança de VM.

    - **preScriptParams**: fornecer os parâmetros opcionais Olá que necessitam de toobe transmitido pré-scripts de toohello. Todos os parâmetros devem ser aspas e devem ser separados por vírgulas se existirem vários parâmetros.

    - **postScriptParams**: fornecer os parâmetros opcionais Olá que necessitam de toobe transmitido toohello script de pós-implementação. Todos os parâmetros devem ser aspas e devem ser separados por vírgulas se existirem vários parâmetros.

    - **preScriptNoOfRetries**: Definir Olá número de vezes que o pré-script de Olá deve ser repetida se não houver qualquer erro antes de terminar. Experimente de apenas um zero significa e sem repetição se ocorrer uma falha.

    - **postScriptNoOfRetries**: Definir Olá número de vezes que o script de pós-implementação Olá deve ser repetida se não houver qualquer erro antes de terminar. Experimente de apenas um zero significa e sem repetição se ocorrer uma falha.
    
    - **timeoutInSeconds**: especificar os tempos limite individuais para pré-scripts de Olá e scripts pós-implementação Olá.

    - **continueBackupOnFailure**: defina este valor demasiado**verdadeiro** se pretende a cópia de segurança do Azure toofall back tooa ficheiro sistema consistente/falhas cópia de segurança consistente se o pré- script de ou pós-falha do script. Definir este demasiado**falso** falha Olá cópia de segurança em caso de falha de script (exceto se tiver VM de disco único que fica novamente toocrash cópias de segurança consistentes independentemente desta definição).

    - **fsFreezeEnabled**: Especifique se Linux fsfreeze deve ser chamado enquanto estiver a ser consistência do sistema de ficheiros instantâneo tooensure Olá VM. É recomendável manter esta definição definida demasiado**verdadeiro** , a menos que a aplicação tem uma dependência na desativação fsfreeze.

6. arquitetura de script de Olá está agora configurada. Se já estiver configurada a cópia de segurança VM de Olá, a próxima cópia de segurança Olá invoca scripts Olá e aciona uma cópia de segurança consistentes com aplicações. Se não estiver configurada a cópia de segurança VM de Olá, configure-a utilizando [cópia de segurança cofres dos serviços de tooRecovery de máquinas virtuais do Azure.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Resolução de problemas

Certifique-se de adicionar o registo adequado ao escrever o pré- script de e scripts pós-implementação e rever o toofix de registos de script quaisquer problemas de script. Se ainda tiver problemas a execução de scripts, consulte toohello seguinte tabela para obter mais informações.

| Erro | Mensagem de erro | Ação recomendada |
| ------------------------ | -------------- | ------------------ |
| Pré-ScriptExecutionFailed |pré-scripts de Olá devolveram um erro, pelo que a cópia de segurança poderá não ser consistentes com aplicações. | Ver registos de falha de Olá do seu problema de Olá toofix script.|  
|   Post ScriptExecutionFailed |    script de pós-implementação Olá devolveu um erro que pode afetar o estado da aplicação. |  Ver registos de falha de Olá do seu problema do script toofix Olá e verifique o estado da aplicação Olá. |
| Pré-ScriptNotFound |  Olá pré-scripts de não foi encontrado na localização de Olá especificado no Olá **VMSnapshotScriptPluginConfig.json** ficheiro de configuração. | Certifique-se que ao script de disponibilizar está presente no caminho de Olá especificado no Olá config ficheiro tooensure consistentes com aplicações cópia de segurança.|
| Post ScriptNotFound | Olá pós-script não foi encontrado na localização de Olá especificado no Olá **VMSnapshotScriptPluginConfig.json** ficheiro de configuração. | Certifique-se que posterior ao script de disponibilizar está presente no caminho de Olá especificado no Olá config ficheiro tooensure consistentes com aplicações cópia de segurança.|
| IncorrectPluginhostFile | Olá **Pluginhost** ficheiro, que é fornecido com Olá VmSnapshotLinux extensão, está danificado, pelo que não é possível executar pré- scripts de e scripts pós-implementação e a cópia de segurança de Olá não é consistentes com aplicações.   | Desinstalar Olá **VmSnapshotLinux** extensão e serão automaticamente reinstalado ao problema de Olá de cópia de segurança toofix Olá seguinte. |
| IncorrectJSONConfigFile | Olá **VMSnapshotScriptPluginConfig.json** ficheiro incorreto, por isso, a pré-script e não é possível executar o script de pós-implementação e cópia de segurança de Olá não é consistentes com aplicações. | Transferir Olá cópia a partir de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) e configurá-la novamente. |
| Script de InsufficientPermissionforPre | Para executar scripts, utilizador de "raiz" deve ser o proprietário de Olá do ficheiro de Olá e ficheiro Olá deve ter permissões "700" (ou seja, deve ter apenas "proprietário" "ler", "escrita" e "executar" permissões). | Certifique-se de que o utilizador de "raiz" Olá "proprietário" de ficheiro de script de Olá e que apenas "proprietário" tem "ler", "escrita" e "executar" permissões. |
| Script de InsufficientPermissionforPost | Para executar scripts, utilizador raiz deve ser o proprietário de Olá do ficheiro de Olá e ficheiro Olá deve ter permissões "700" (ou seja, deve ter apenas "proprietário" "ler", "escrita" e "executar" permissões). | Certifique-se de que o utilizador de "raiz" Olá "proprietário" de ficheiro de script de Olá e que apenas "proprietário" tem "ler", "escrita" e "executar" permissões. |
| Pré-ScriptTimeout | Olá execução de pré-scripts de cópia de segurança consistentes com aplicações Olá excedido. | Verifique o script de Olá e aumentar o tempo limite de Olá em Olá **VMSnapshotScriptPluginConfig.json** ficheiro que está localizado em **etc/azure**. |
| Post ScriptTimeout | execução de Olá do pós-script de cópia de segurança consistentes com aplicações Olá excedeu o tempo limite. | Verifique o script de Olá e aumentar o tempo limite de Olá em Olá **VMSnapshotScriptPluginConfig.json** ficheiro que está localizado em **etc/azure**. |

## <a name="next-steps"></a>Passos seguintes
[Configurar o Cofre de serviços de recuperação de cópia de segurança tooa VM](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
