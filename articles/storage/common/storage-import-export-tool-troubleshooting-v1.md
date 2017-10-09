---
title: "Olá aaaTroubleshooting ferramenta de importação/exportação do Azure | Microsoft Docs"
description: "Saiba mais sobre alguns dos problemas comuns de Olá vistos quando utilizar Olá ferramenta de importação/exportação do Azure e como a toohandle-los."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Resolução de problemas Olá ferramenta de importação/exportação do Azure
Olá ferramenta de importação/exportação do Microsoft Azure devolve mensagens de erro se ficar para problemas. Este tópico apresenta alguns problemas comuns que os utilizadores podem executar no.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Uma sessão de cópia falha, o que devo fazer?  
 Quando uma sessão de cópia falha, existem duas opções:  
  
 Se o erro de Olá for repetição, por exemplo, se a partilha de rede Olá estava offline para um curto período e agora está novamente online, pode retomar a sessão de cópia de Olá. Se o erro de Olá não for repetição, por exemplo, se especificou o diretório do ficheiro de origem errado Olá nos parâmetros de linha de comandos Olá, terá de sessão de cópia de Olá tooabort. Consulte [preparar os discos rígidos de uma tarefa de importação](../storage-import-export-tool-preparing-hard-drives-import-v1.md) para obter mais informações sobre a retomar e abortar sessões de cópia.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>Não consigo retomar ou abortar uma sessão de cópia.  
 Se sessão de cópia de Olá está Olá primeira sessão de cópia para uma unidade, em seguida, mensagem de erro de saudação deve Estado: "Olá primeira sessão de cópia não pode ser retomado ou abortada." Neste caso, pode eliminar o ficheiro de diário antigo Olá e volte a executar o comando de Olá.  
  
 Se uma sessão de cópia não é hello primeiro uma para uma unidade, pode ser retomado sempre ou abortada.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Perdeu a ficheiros do diário de alterações de Olá, pode ainda criar tarefa de Olá?  
 ficheiros do diário de alterações de Olá para uma unidade contém Olá informações de copiar a unidade de toothis de dados e é necessário tooadd mais unidade de toohello de ficheiros e será utilizado toocreate uma tarefa de importação. Se o ficheiro do diário de alterações de Olá se tenha perdido, terá de tooredo todas as sessões de cópia de Olá para unidade Olá.  
  
## <a name="next-steps"></a>Passos seguintes
 
* [Configurar a ferramenta de importação/exportação do azure Olá](../storage-import-export-tool-setup-v1.md)   
* [Preparar as unidades de disco rígido para uma tarefa de importação](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisão do estado da tarefa com ficheiros de registo de cópia](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparação de uma tarefa de importação](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Reparação de uma tarefa de exportação](../storage-import-export-tool-repairing-an-export-job-v1.md)
