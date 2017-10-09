---
title: aaaWhat aconteceu toomy WebJob projeto (Visual Studio do armazenamento do Azure ligado service)? | Microsoft Docs
description: "Descreve o que aconteceu num projeto trabalho Web do Azure depois de ligar tooa conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ed0ce75f5b23eca3c41dacb48564d6e5b846f395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webjob-project-visual-studio-azure-storage-connected-service"></a>O projeto de WebJob toomy acontecido (Visual Studio do armazenamento do Azure ligado service)?
## <a name="references-added"></a>Referências adicionadas
pacote NuGet de armazenamento do Azure de Olá foi adicionado tooor atualizado no seu projeto de Visual Studio.  
Este pacote adiciona Olá .NET referências a seguir:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Configurationmanager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft**
* **Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Cadeia de ligação para o armazenamento de Azure adicionado
No ficheiro App. config de Olá do seu projeto, Olá **AzureWebJobsStorage** e **AzureWebJobsDashboard** entradas foram atualizadas com a cadeia de ligação e a chave da conta de armazenamento Olá selecionado.

Para obter mais informações, consulte [recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).

