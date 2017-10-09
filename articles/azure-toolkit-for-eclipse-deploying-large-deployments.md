---
title: "aaaDeploying grandes implementações"
description: "Saiba como implementações de grande toodeploy utilizando Olá Toolkit do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Implementar grandes implementações
Se a sua implementação é demasiado grande toobe contido na pasta de approot Olá predefinido, pode utilizar um recurso de armazenamento local como a pasta de raiz de implementação de Olá para o JDK e servidor de aplicação.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse um recurso de armazenamento local como pasta raiz de implementação de Olá para implementações grandes
1. Crie um novo recurso do armazenamento local. nome de Olá do recurso de Olá não importa. Recursos de armazenamento é definida ao nível da função de Olá. Olá mais rápida forma tooaccess Olá armazenamento local caixa de diálogo Configuração, do qual pode criar um novo recurso do armazenamento local, é utilizando Olá os seguintes passos: função de Olá do rato no Olá **Explorador de projeto** vista (expandir a Projeto do Azure nó se não vir a função de Olá), clique em **Azure**e, em seguida, clique em **armazenamento Local**. Dentro do Olá **armazenamento Local** caixa de diálogo, clique em **adicionar** toocreate um novo recurso do armazenamento local.

2. Olá conjunto pretendido tooat de tamanho, pelo menos, 2048 MB (tudo menos poderá provocar Olá mesmo problemas de tamanho de ficheiro como seria encontrar Olá approot).

3. Certifique-se de que **apagar conteúdo de Olá quando é reciclada, instância de função Olá** é verificado; Isto irá ajudar a impedir a execução em conflitos com ficheiros pré-existentes no recurso de Olá de lógica de arranque da implementação de Olá Olá quando a função a instância é reciclada.

4. Certifique-se de que Olá **armazenar variável de ambiente Olá caminho do diretório do recurso após a implementação** valor é definido toohello cadeia **DEPLOYROOT**. A caixa de diálogo de recursos de armazenamento local terá um aspeto semelhante toohello seguinte.

   ![][ic667943]

Em alternativa, se utilizar **DEPLOYROOT** como Olá *nome* do seu recurso local e não altere o nome de variável de ambiente gerado automaticamente do Olá (que será definido demasiado **DEPLOYROOT_PATH** nesse caso), que funciona para a sua aplicação bem.

Informações adicionais sobre a criação de um recurso de armazenamento local podem ser encontradas em [propriedades de armazenamento Local][Local storage properties].

## <a name="see-also"></a>Veja Também
[Toolkit do Azure do Eclipse][Azure Toolkit for Eclipse]

[Criar uma aplicação do Olá mundo do Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalar Olá Toolkit de Azure do Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
