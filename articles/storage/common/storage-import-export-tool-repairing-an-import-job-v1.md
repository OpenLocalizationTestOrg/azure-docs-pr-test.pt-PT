---
title: "aaaRepairing uma tarefa de importação do Azure para importar/exportar - v1 | Microsoft Docs"
description: "Saiba como toorepair uma tarefa de importação que foi criada e executada com hello do Azure para importar/exportar serviço."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b1cb7d7832276a05c0912cf57505e2a5d79e7846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Reparação de uma tarefa de importação
Olá serviço de importação/exportação do Microsoft Azure poderá falhar toocopy alguns dos seus ficheiros ou partes de um ficheiro de toohello serviço Blob do Windows Azure. Algumas razões para falhas incluem:  
  
-   Ficheiros danificados  
  
-   Unidades danificadas  
  
-   chave de conta do storage de Olá alterado enquanto o ficheiro de Olá estava a ser transferido.  
  
Pode executar Olá ferramenta de importação/exportação do Microsoft Azure com o da tarefa de importação Olá cópia registo ficheiros e Olá ferramenta carregamentos Olá ficheiros em falta (ou partes de um ficheiro) tooyour do Windows Azure armazenamento conta toocomplete Olá tarefa de importação.  
  
## <a name="repairimport-parameters"></a>Parâmetros de RepairImport

Olá parâmetros seguintes podem ser especificados com **RepairImport**: 
  
|||  
|-|-|  
|**/r:**< RepairFile\>|**Necessário.** Ficheiro de reparação de toohello do caminho, que controla o progresso de Olá de reparação de Olá e permite-lhe tooresume uma reparação de interrompida. Cada unidade tem de ter um e apenas um ficheiro de reparação. Ao iniciar uma reparação de uma determinada unidade, passe no ficheiro reparação do Olá caminho tooa, que ainda não existe. tooresume uma reparação de interrompida, deverá passar no nome de Olá de um ficheiro de reparação existente. Olá reparação ficheiro correspondente toohello unidade de destino têm sempre de ser especificada.|  
|**/LOGDIR:**< LogDirectory\>|**Opcional.** diretório de registo de Olá. Ficheiros de registo verboso são escritos toothis diretório. Não se for especificado nenhum diretório de registo, o diretório atual Olá é utilizado como diretório de registo Olá.|  
|**/d:**< TargetDirectories\>|**Necessário.** Um ou mais diretórios de valores separados por ponto e vírgula que contêm Olá originais ficheiros que foram importados. unidade de importação de Olá também pode ser utilizada, mas não é necessária se alternativo localizações dos ficheiros originais não estiverem disponíveis.|  
|**/BK:**< BitLockerKey\>|**Opcional.** Deve especificar a chave do BitLocker Olá se quiser Olá ferramenta toounlock uma unidade encriptada onde os ficheiros originais Olá estão disponíveis.|  
|**/SN:**< StorageAccountName\>|**Necessário.** nome de Olá Olá da conta de armazenamento para Olá importar tarefa.|  
|**/SK:**< StorageAccountKey\>|**Necessário** se e apenas se não for especificado um contentor SAS. chave da conta para conta de armazenamento Olá Olá Olá importar tarefa.|  
|**/csas:**< ContainerSas\>|**Necessário** se, e apenas se, chave de conta do storage Olá não está especificado. Olá contentor SAS para aceder a blobs Olá associados à tarefa de importação de Olá.|  
|**/ CopyLogFile:**< DriveCopyLogFile\>|**Necessário.** Caminho toohello unidade Copiar ficheiro de registo (o registo verboso ou de registo de erros). ficheiro de Olá é gerado pelo Olá serviço de importação/exportação do Windows Azure e pode ser transferido do armazenamento de BLOBs de Olá associado à tarefa Olá. ficheiro de registo de cópia de Olá contém informações sobre a blobs com falhas ou ficheiros, que são toobe reparada.|  
|**/ PathMapFile:**< DrivePathMapFile\>|**Opcional.** Ficheiro de texto do caminho tooa que pode ser utilizado tooresolve ambiguities se tiver vários ficheiros com o mesmo nome que foram a importação dentro de Olá Olá mesma tarefa. Olá primeiro tempo Olá ferramenta é executada, pode preencher deste ficheiro com a todos os nomes ambíguos Olá dos. As execuções subsequentes da ferramenta de Olá utilizam ambiguities de Olá de tooresolve este ficheiro.|  
  
## <a name="using-hello-repairimport-command"></a>Utilizando o comando de RepairImport Olá  
Importar dados de toorepair por transmissão em fluxo de dados de Olá rede Olá, tem de especificar diretórios Olá que contêm ficheiros originais Olá foram importar utilizando Olá `/d` parâmetro. Tem de especificar também o ficheiro de registo de cópia Olá que transferiu a partir da sua conta de armazenamento. Uma linha de comandos típico toorepair uma tarefa de importação com falhas parciais aspeto:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
No Olá estava danificado seguinte exemplo de um ficheiro de registo de cópia, um fragmento de 64K de um ficheiro na unidade de Olá que foi enviada para a tarefa de importação de Olá. Uma vez que esta falha apenas Olá indicada, o restante Olá Olá os blobs na tarefa de Olá foram importadas com êxito.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Quando este registo de cópia é passado toohello ferramenta de importação/exportação do Azure, a ferramenta Olá tenta importar de Olá toofinish para este ficheiro ao copiar o conteúdo em falta Olá através de rede de Olá. Exemplo de Olá acima, os seguintes ferramenta Olá procura do ficheiro original Olá `\animals\koala.jpg` dentro de diretórios de Olá dois `C:\Users\bob\Pictures` e `X:\BobBackup\photos`. O ficheiro se hello `C:\Users\bob\Pictures\animals\koala.jpg` existe Olá ferramenta de importação/exportação do Azure cópias Olá intervalo em falta do blob de dados correspondente do toohello `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>A resolução de conflitos quando utilizar RepairImport  
Em algumas situações, ferramenta Olá pode não ser capaz de toofind ou ficheiro necessárias do Olá aberta para uma das Olá seguintes motivos: não foi possível encontrar o ficheiro de Olá, Olá ficheiro não está acessível, o nome de ficheiro Olá é ambíguo ou Olá o conteúdo do ficheiro Olá já não está correto.  
  
Um erro ambíguo pode ocorrer se a ferramenta de Olá está a tentar toolocate `\animals\koala.jpg` e não existe um ficheiro com esse nome sob ambos `C:\Users\bob\pictures` e `X:\BobBackup\photos`. Ou seja, ambos `C:\Users\bob\pictures\animals\koala.jpg` e `X:\BobBackup\photos\animals\koala.jpg` existe em unidades de tarefa de importação de Olá.  
  
Olá `/PathMapFile` opção permite-lhe tooresolve estes erros. Pode especificar o nome de Olá do ficheiro de Olá, que contém a lista de Olá de ficheiros que Olá ferramenta não foi possível identificar toocorrectly. Olá seguinte exemplo de linha de comandos preenche `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
ferramenta de Olá irá, em seguida, escrever caminhos de ficheiro problemáticas Olá demasiado`9WM35C2V_pathmap.txt`, um em cada linha. Por exemplo, o ficheiro de Olá pode conter Olá seguir entradas depois de executar o comando de Olá:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Para cada ficheiro na lista de Olá, deve tentar toolocate e abrir Olá ficheiro tooensure é ferramenta toohello disponíveis. Se assim o desejar a ferramenta de Olá tootell explicitamente onde toofind um ficheiro, pode modificar Olá mapear o ficheiro e caminho adicionar Olá caminho tooeach ficheiro Olá mesma linha, separada por um caráter de separador:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Depois de efetuar ferramenta de toohello disponíveis de ficheiros necessários hello, ou atualizar ficheiro de mapa de caminho Olá, pode voltar a executar o processo de importação do Olá ferramenta toocomplete Olá.  
  
## <a name="next-steps"></a>Passos seguintes
 
* [Configurar a definição Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)   
* [Preparar as unidades de disco rígido para uma tarefa de importação](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisão do estado da tarefa com ficheiros de registo de cópia](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparação de uma tarefa de exportação](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Resolução de problemas Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-troubleshooting-v1.md)
