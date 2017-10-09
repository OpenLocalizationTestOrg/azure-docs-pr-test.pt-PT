---
title: aaaFrequently mais frequentes sobre o sobre o File storage do Azure | Microsoft Docs
description: Encontre respostas toofrequently mais frequentes sobre o sobre o File storage do Azure.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Perguntas mais frequentes sobre o File storage do Azure

## <a name="general"></a>Geral
* **Q. O que é o File storage do Azure?**  
   
    File storage do Azure é um sistema de ficheiros distribuído no Azure. Fornece uma interface de protocolo SMB que permite que o armazenamento de Olá toomount utilizadores como uma partilha nativa na máquina de Virtual do Azure suportada ou máquina no local.

* **Q. Por que motivo é útil File storage do Azure?**  
   
    File storage do Azure fornece acesso de dados partilhada em várias plataformas e VMs. Consulte demasiado[por que motivo File storage do Azure é útil](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Quando deve utilizar os ficheiros do Azure vs Blob do Azure vs do disco do Azure?**  
   
    Microsoft Azure fornece várias formas de dados toostore e acessos na nuvem de Olá.  
   
    File storage do Azure - fornece uma interface SMB, bibliotecas de cliente e uma interface REST que permite acesso fácil a partir de qualquer lugar toostored ficheiros.  
   
    Azure Blobs - fornece uma interface REST que permite que os dados não estruturados toobe armazenados e acedidos numa grande escala em blobs de blocos e de bibliotecas de cliente.  
   
    Dados do Azure discos - fornece uma interface REST que permite que os dados toobe forma permanente armazenados e acedido a partir de um disco rígido virtual ligado e bibliotecas de cliente.  
   
    Saber mais sobre [Deciding quando toouse Azure Blobs, ficheiros do Azure ou os discos de dados do Azure](storage-decide-blobs-files-disks.md)

* **Q. Como começar a utilizar com o File storage do Azure?**  
   
    Pode começar por criar uma partilha de ficheiros do Azure. Pode criar partilhas de ficheiros do Azure utilizando o Portal do Azure, os cmdlets do PowerShell de armazenamento do Azure de Olá, bibliotecas de cliente do Storage do Azure Olá ou Olá API de REST do Storage do Azure. Neste tutorial, irá aprender:

    * [Saiba como toocreate ficheiros do Azure partilhar utilizando Olá Portal](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Saiba como toocreate ficheiros do Azure partilhar com o Powershell](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Saiba como toocreate ficheiros do Azure partilhar com a CLI](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Que replicações são suportadas pelo File storage do Azure?**  
   
    File storage do Azure suporta apenas LRS ou GRS neste momento. Planeamos toosupport RA-GRS mas não existe nenhuma linha cronológica tooshare ainda.

## <a name="security-authentication-and-access-control"></a>Segurança, a autenticação e controlo de acesso

* **Q. Quais são os ficheiros de tooaccess de formas diferentes no File storage do Azure?**
    
    É possível montar a partilha de ficheiros de Olá no seu computador local utilizando o protocolo SMB 3.0 ou utilizar ferramentas como [Explorador de armazenamento](http://storageexplorer.com/) tooaccess ficheiros numa partilha de ficheiros. Da sua aplicação, pode utilizar bibliotecas de cliente de armazenamento, REST APIs ou tooaccess Powershell que partilham os seus ficheiros no ficheiro do Azure.

* **Q. Como pode fornecer os ficheiros de específica de acesso tooa utilizando um browser?**
    
    Através da SAS, pode gerar tokens com permissões específicas que são válidos por um intervalo de tempo especificado. Por exemplo, pode gerar um token com o ficheiro em particular tooa acesso só de leitura para um período de tempo específico. Quem tiver este url pode aceder a ficheiros Olá diretamente a partir de qualquer browser, enquanto é válido. As chaves SAS podem ser facilmente geradas a partir da IU, como o Explorador de Armazenamento.

* **Q. É possível toospecify as permissões de só de leitura ou só de escrita em pastas na partilha de Olá?**
    
    Não tem este nível de controlo sobre as permissões se montar a partilha de ficheiros de Olá através de SMB. No entanto, pode conseguir isto ao criar uma assinatura de acesso partilhado (SAS) através de Olá REST API ou de bibliotecas de cliente.  

* **Q. Como ativar a encriptação do lado do servidor para o File storage do Azure?**

    [Encriptação do lado do servidor](storage-service-encryption.md) para ficheiros do Azure storage está normalmente disponível em todas as regiões e nuvens públicas e national. Pode ativar SSE para armazenamento de ficheiros do Azure utilizando [portal do Azure](https://portal.azure.com/),[API de fornecedor de recursos de armazenamento do Microsoft Azure](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) ou [CLI do Azure](storage-azure-cli.md).
    
    Depois de ativar SSE no File storage do Azure, quaisquer novos dados escritos toohello o file storage nessa conta de armazenamento serão automaticamente encriptados. Esta funcionalidade está disponível para todos os novos dados escritos tooexisting ou novas partilhas numa conta de armazenamento nova ou existente. Não existe nenhum encargo adicional para ativar esta funcionalidade. Saber mais sobre [como tooenable SSE no File storage do Azure](storage-service-encryption.md).

* **Q. Autenticação baseada no Active Directory é suportada pelo File storage do Azure?**
   
    Atualmente, não suportamos a autenticação baseada no AD ou em ACLs, mas é uma funcionalidade que está presente na nossa lista de pedidos de funcionalidades. Por agora, as chaves de conta do Storage do Azure Olá são partilha de ficheiros utilizados tooprovide autenticação toohello. Oferecemos uma solução através de assinaturas de acesso partilhado (SAS) através de bibliotecas de cliente de REST API ou Olá Olá. Através da SAS, pode gerar tokens com permissões específicas que são válidos por um intervalo de tempo especificado. Por exemplo, pode gerar um token com tooa acesso só de leitura atribuído ficheiro com a expiração de 10 minutos. Quem tiver este token enquanto for válido tem acesso só de leitura de ficheiros de toothat para esses 10 minutos.
   
    SAS só é suportado através de bibliotecas de cliente de REST API ou de Olá. Ao montar a partilha de ficheiros de Olá através de Olá protocolo SMB, não é possível utilizar o conteúdo do tooits toodelegate acesso uma SAS. 
    
* **Q. Quais são as políticas de conformidade do Olá dados suportadas para o File storage do Azure?**

   File Storage do Azure é executado de Olá a mesma arquitetura de armazenamento como de outro armazenamento serviços no Storage do Azure e aplica-se Olá mesmo políticas de conformidade de dados. Obter mais informações sobre a compatibilidade de dados do Storage do Azure, pode transferir e consulte demasiado[documento de proteção de dados do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Acesso no local

* **Q.Do tenho toouse Azure ExpressRoute tooconnect tooAzure File storage de uma VM no local?**
   
    Não. Se não tiver o ExpressRoute, pode continuar a aceder Olá partilha de ficheiros no local, desde que tenha a porta 445 (saída de TCP) aberta para acesso à Internet. No entanto, pode utilizar ExpressRoute com File storage do Azure se assim o desejar.

* **Q. Como montar uma partilha de ficheiros do Azure no meu computador local?** 
    
    É possível montar Olá partilha de ficheiros através do protocolo SMB de Olá desde que a porta 445 (saída de TCP) esteja aberta e o cliente suportar o protocolo de Olá SMB 3.0 (por exemplo, estiver a utilizar Windows 10 ou Windows Server 2012). Volte a trabalhar com a porta de Olá toounblock de fornecedor do local ISP. Na Olá intermédio, pode ver os ficheiros utilizando [Explorador de armazenamento](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Faturação e preços
* **Q. Olá o tráfego de rede entre uma VM do Azure e uma contagem de partilha de ficheiros como largura de banda externa que é cobrada toohello subscrição?**
   
    Se a partilha de ficheiros de Olá e VM estiverem em Olá mesma região do Azure, hello tráfego entre as mesmas é gratuito. Se estiverem em regiões diferentes, tráfego Olá entre os mesmos será cobrado como largura de banda externa.

## <a name="backup"></a>Cópia de segurança

* **Q. Como posso criar cópias de segurança meu partilha de ficheiros do Azure?**
    
    Pode utilizar o AzCopy, RoboCopy, ou um 3rd ferramenta de cópia de segurança que pode uma partilha de ficheiros montados de cópia de segurança de terceiros. Esperamos instantâneos do toohave Olá capacidade tootake de partilhas de ficheiros no Olá quase futuro; será capaz de toouse toobackup esta funcionalidade de partilha de ficheiros do Azure.

## <a name="performance"></a>Desempenho

* **Q. Quais são os limites de escala Olá do File storage do Azure?**
    Para obter informações sobre metas de desempenho e escalabilidade do File storage do Azure, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. O meu desempenho foi lento ao tentar toounzip ficheiros no File storage do Azure. O que devo fazer?**
    
    tootransfer grande número de ficheiros para o File storage do Azure, recomendamos que utilize AzCopy (Windows, pré-visualização do Linux/Unix) ou do Azure Powershell, estas ferramentas foram otimizadas para transferência de rede.

* **Q. O que foi patches lançadas toofix problema de desempenho lento com o File storage do Azure?**
    
    equipa do Windows Hello lançou recentemente uma correção de toofix um problema de desempenho lento quando o cliente de Olá acede ao File storage do Azure do Windows 8.1 ou Windows Server 2012 R2. Para obter mais informações,. modificação Olá associados artigo KB [desempenho lento ao aceder o File storage do Azure a partir do Windows 8.1 ou Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Funcionalidades e interoperabilidade com outros serviços
* **Q. É um "testemunho de partilha de ficheiros" para um cluster de ativação pós-falha, uma das Olá casos de utilização do File storage do Azure?**
   
    Isto não é atualmente suportado.

* **Q. Existe uma operação de mudança de nome na Olá REST API?**
   
    Neste momento, não.

* **Q. Pode possível ter partilhas aninhadas, por outras palavras, uma partilha numa partilha?**
    
    Não. partilha de ficheiros de Olá é o controlador virtual Olá que é possível montar, pelo que não são suportadas partilhas aninhadas.

* **Q. Utilizar o File storage do Azure com o IBM MQ**
    
    A IBM lançou um clientes do documento tooguide IBM MQ quando configurar o File storage do Azure com o respetivo serviço. Para obter mais informações, consulte [como toosetup IBM MQ várias instância Gestor de filas com o serviço de ficheiro do Microsoft Azure](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Resolução de problemas
* **Q. Como posso resolver erros de armazenamento de ficheiros do Azure?**
    
    Pode consultar demasiado[File storage do Azure artigo de resolução de problemas](storage-troubleshoot-file-connection-problems.md) para obter orientações de resolução de problemas de ponto a ponto. 


## <a name="see-also"></a>Consultar também
Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos concetuais
* [Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Armazenamento de Ficheiros do Azure: um prático sistema de ficheiros SMB na cloud para Windows e Linux)
* [Como toouse File storage do Azure com o Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Suporte de ferramentas para o Armazenamento de ficheiros
* [Using Azure PowerShell with Azure Storage (Utilizar o Azure PowerShell com o Armazenamento do Azure)](storage-powershell-guide-full.md)
* [Como toouse AzCopy com armazenamento do Microsoft Azure](storage-use-azcopy.md)
* [Utilizar Olá CLI do Azure com o Storage do Azure](storage-azure-cli.md)
* [Resolver problemas do armazenamento de ficheiros do Azure](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Publicações no blogue
* [Azure File storage is now generally available (O Armazenamento de Ficheiros do Azure está agora disponível normalmente)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Por dentro do armazenamento de Ficheiros do Azure)
* [Introducing Microsoft Azure File Service (Introdução ao Serviço de Ficheiros do Microsoft Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrar dados tooAzure armazenamento de ficheiros](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referência
* [Storage Client Library for .NET reference (Referência da Biblioteca de Clientes do Armazenamento para .NET)](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [File Service REST API reference (Referência da API REST do Serviço do Ficheiros)](http://msdn.microsoft.com/library/azure/dn167006.aspx)
