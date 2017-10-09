---
title: 'O Azure AD Connect: Como toorecover da LocalDB 10GB limitar problema | Microsoft Docs'
description: "Este tópico descreve como toorecover sincronização do Azure AD Connect do serviço quando encontra LocalDB 10GB limitar o problema."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>O Azure AD Connect: Como toorecover do limite de 10 GB LocalDB
O Azure AD Connect requer um dados de identidade do toostore de base de dados do SQL Server. Pode utilizar a predefinição de Olá que SQL Server 2012 Express LocalDB instalado com o Azure AD Connect ou utilizar o seu próprio SQL completo. O SQL Server Express impõe um limite de tamanho de 10 GB. Ao utilizar a LocalDB e este limite ser atingido, o Serviço de Sincronização do Azure AD Connect já não pode iniciar ou sincronizar corretamente. Este artigo fornece os passos de recuperação Olá.

## <a name="symptoms"></a>Sintomas
Existem dois sintomas comuns:

* Serviço de sincronização ligar do Azure AD **está em execução** , mas falhar toosynchronize com *"parou-base de dados-disco-completa"* erro.

* Serviço de sincronização ligar do Azure AD **é toostart não é possível**. Quando a tentativa de serviço de Olá toostart falhar com eventos 6323 e a mensagem de erro *"o servidor de Olá encontrou um erro porque o SQL Server está fora do espaço em disco."*

## <a name="short-term-recovery-steps"></a>Passos de recuperação de curta duração
Esta secção fornece Olá passos tooreclaim DB o espaço necessário para a operação de tooresume do serviço de sincronização ligar do Azure AD. Olá passos incluem:
1. [Determinar o estado do serviço de sincronização Olá](#determine-the-synchronization-service-status)
2. [Base de dados de operação de encolhimento Olá](#shrink-the-database)
3. [Eliminar dados do histórico de execução](#delete-run-history-data)
4. [Reduza o período de retenção de dados do histórico de execução](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Determinar o estado do serviço de sincronização Olá
Em primeiro lugar, determine se Olá serviço de sincronização ainda está em execução ou não:

1. Inicie sessão no tooyour do Azure AD Connect servidor como administrador.

2. Aceda demasiado**Service Control Manager**.

3. Verificar o estado de Olá de **Microsoft Azure AD Sync**.


4. Se estiver em execução, não parar ou reiniciar o serviço de Olá. Ignorar [base de dados de operação de encolhimento Olá](#shrink-the-database) passo e vá demasiado[eliminar dados do histórico de execução](#delete-run-history-data) passo.

5. Se não está em execução, tente o serviço de Olá toostart. Se o serviço de Olá é iniciado com êxito, ignore [base de dados de operação de encolhimento Olá](#shrink-the-database) passo e vá demasiado[eliminar dados do histórico de execução](#delete-run-history-data) passo. Caso contrário, continue com [base de dados de operação de encolhimento Olá](#shrink-the-database) passo.

### <a name="shrink-hello-database"></a>Base de dados de operação de encolhimento Olá
Utilize toofree de operação de encolhimento Olá segurança Olá de toostart espaço suficiente DB serviço de sincronização. -Liberta espaço de base de dados removendo espaços em branco na base de dados de Olá. Este passo é melhor esforço, como não é garantido que pode recuperar sempre espaço. toolearn mais informações sobre a operação de encolhimento, leia este artigo [diminuir uma base de dados](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Ignore este passo se pode obter Olá toorun de serviço de sincronização. Não é recomendado tooshrink Olá BD do SQL que pode levar toopoor desempenho devido a fragmentação de tooincreased.

Olá nome da base de dados de Olá criada para o Azure AD Connect é **ADSync**. uma operação de encolhimento tooperform, tem de iniciar sessão como Olá sysadmin ou DBO da base de dados de Olá. Durante a instalação do Azure AD Connect, Olá seguintes contas é concedido direitos de administrador do sistema:
* Administradores locais
* conta de utilizador de Olá que foi utilizado toorun do Azure AD Connect instalação.
* Olá conta de serviço de sincronização que é utilizada como Olá operativo contexto do serviço de sincronização ligar do Azure AD.
* grupo local de Olá ADSyncAdmins que foi criada durante a instalação.

1. Cópia de segurança da base de dados de Olá copiando **ADSync.mdf** e **ADSync_log.ldf** ficheiros localizados em `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa de localização segura.

2. Inicie uma nova sessão do PowerShell.

3. Navegue toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Iniciar **sqlcmd** utilitário executando o comando de Olá `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, utilizando credenciais Olá um sysadmin ou Olá DBO da base de dados.

5. base de dados da Olá tooshrink, na linha de comandos do Olá sqlcmd (1 >), introduza `DBCC Shrinkdatabase(ADSync,1);`, seguido `GO` na linha seguinte Olá.

6. Se a operação de Olá for bem-sucedida, tente novamente toostart Olá serviço de sincronização. Se começar Olá serviço de sincronização, aceda demasiado[eliminar dados do histórico de execução](#delete-run-history-data) passo. Caso contrário, contacte o suporte.

### <a name="delete-run-history-data"></a>Eliminar dados do histórico de execução
Por predefinição, o Azure AD Connect mantém até compreendendo tooseven dias de dados do histórico de execução. Neste passo, vamos eliminar Olá espaço de tooreclaim DB de dados do histórico de execução para que o serviço de sincronização ligar do Azure AD pode começar a sincronizar novamente.

1.  Iniciar **Synchronization Service Manager** por vai → de tooSTART serviço de sincronização.

2.  Aceda toohello **operações** separador.

3.  Em **ações**, selecione **executa limpar**...

4.  Pode optar por **limpar todas as execuções** ou **encriptado é executado antes de... <date>**  opção. Recomenda-se que comece por limpar executar histórico de dados que são mais antigo do que dois dias. Se continuar toorun no problema de tamanho de base de dados, em seguida, escolha Olá **limpar todas as execuções** opção.

### <a name="shorten-retention-period-for-run-history-data"></a>Reduza o período de retenção de dados do histórico de execução
Este passo é a probabilidade de Olá tooreduce de execução para o problema de limite de 10 GB Olá após vários ciclos de sincronização.

1. Abra uma nova sessão do PowerShell.

2. Executar `Get-ADSyncScheduler` e tome nota dos Olá PurgeRunHistoryInterval propriedade, o que especifica o período de retenção atual Olá.

3. Executar `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` dias de tootwo período de retenção de Olá tooset. Ajuste o período de retenção de Olá conforme apropriado.

## <a name="long-term-solution--migrate-toofull-sql"></a>Solução de longa duração – migrar toofull SQL
Em geral, o problema de Olá é facto de que o tamanho de base de dados de 10 GB já não é suficiente para o Azure AD Connect toosynchronize sua tooAzure do Active Directory no local AD. Recomenda-se que mude toousing versão completa do Olá do SQL server. Não é possível diretamente substituir Olá LocalDB de uma implementação existente do Azure AD Connect com base de dados de Olá da versão completa do Olá do SQL Server. Em vez disso, tem de implementar um novo servidor do Azure AD Connect com a versão completa do Olá do SQL Server. Recomenda-se que efetue uma migração swing que em que o novo Azure AD Connect servidor Olá (com base de dados do SQL Server) é implementado como um servidor de teste, seguinte toohello existente servidor do Azure AD Connect (com LocalDB). 
* Para obter instruções sobre como tooconfigure SQL remoto com o Azure AD Connect, consulte tooarticle [instalação personalizada do Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Para obter instruções sobre a migração de swing para a atualização do Azure AD Connect, consulte tooarticle [do Azure AD Connect: atualização a partir de uma anterior toohello versão mais recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
