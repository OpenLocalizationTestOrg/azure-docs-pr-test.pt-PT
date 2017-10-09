---
title: aaaEncryption no Azure Data Lake Store | Microsoft Docs
description: "Compreender como funciona a encriptação e a rotação de chaves no Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Encriptação de dados no Azure Data Lake Store

A encriptação no Azure Data Lake Store ajuda-o a proteger os seus dados, implementar políticas de segurança da empresa e cumprir os requisitos de conformidade normativa. Este artigo fornece uma descrição geral do design Olá e descreve alguns dos aspetos técnicos do Olá de implementação.

O Data Lake Store suporta a encriptação de dados inativos e em trânsito. No caso dos dados inativos, o Data Lake Store suporta a encriptação transparente "ativada por predefinição". Eis o que cada um destes termos significa em maior detalhe:

* **Por predefinição**: ao criar uma nova conta de Data Lake Store, predefinição Olá ativa a encriptação. Depois disso, os dados armazenados no Data Lake Store são sempre encriptado toostoring anterior no suporte de dados persistente. Este é o comportamento de Olá para todos os dados e não pode ser alterada depois de ser criada uma conta.
* **Transparente**: Data Lake Store automaticamente toopersisting anteriores de dados de encripta e desencripta tooretrieval anteriores de dados. encriptação de Olá é configurada e gerida de Olá ao nível do Data Lake Store por um administrador. Não são efetuadas alterações toohello dados acesso a APIs. Assim, não é preciso fazer alterações nas aplicações e serviços que interagem com o Data Lake Store devido à encriptação.

Os dados em trânsito (também denominados dados em movimento) também são sempre encriptados no Data Lake Store. Além disso tooencrypting dados toostoring anterior toopersistent suporte de dados Olá dados sempre também estão protegidos em trânsito através de HTTPS. HTTPS é Olá único protocolo é suportado para Olá que interfaces de REST do Data Lake Store. Olá diagrama seguinte mostra como os dados torna-se encriptados no Data Lake Store:

![Diagrama de encriptação de dados no Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Configurar a encriptação com o Data Lake Store

A encriptação no Data Lake Store é configurada durante a criação da conta e está sempre ativada por predefinição. Pode gerir chaves de Olá manualmente ou permitir que o Data Lake Store toomanage-las por si (esta é a predefinição de Olá).

Para obter mais informações, veja o artigo [Introdução](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

## <a name="how-encryption-works-in-data-lake-store"></a>Como funciona a encriptação no Data Lake Store

Olá seguintes informações abrange como chaves de encriptação mestra toomanage explica Olá três diferentes tipos de chaves, pode utilizar a encriptação de dados do Data Lake Store.

### <a name="master-encryption-keys"></a>Chaves de encriptação mestras

O Data Lake Store disponibiliza dois modos para gerir as chaves de encriptação mestras (Master Encryption Keys, MEKs). Por agora, assuma a que essa chave de encriptação mestra Olá é a chave de nível superior de Olá. Chave de encriptação mestra do acesso toohello é necessário toodecrypt quaisquer dados armazenados no Data Lake Store.

modos de Olá duas para gerir a chave de encriptação mestra Olá são os seguintes:

*   Chaves geridas por serviços
*   Chaves geridas pelo cliente

Em ambos os modos, chave de encriptação mestra Olá está protegida por armazenar no Cofre de chaves do Azure. O Cofre de chaves é um serviço completamente gerido, altamente seguro no Azure que pode ser utilizados toosafeguard de chaves criptográficas. Para obter mais informações, veja [Key Vault](https://azure.microsoft.com/services/key-vault).

Eis uma breve comparação das funcionalidades fornecidas pelo dois modos de Olá de gerir Olá MEKs.

|  | Chaves geridas por serviços | Chaves geridas pelo cliente |
| --- | --- | --- |
|Como são armazenados os dados?|Sempre encriptado toobeing anterior armazenado.|Sempre encriptado toobeing anterior armazenado.|
|Onde está armazenado a chave de encriptação mestra do Olá?|Cofre de Chaves|Cofre de Chaves|
|São qualquer encriptação chaves armazenadas no Olá limpar fora do Cofre de chaves? |Não|Não|
|Olá MEK pode ser obtida pelo Cofre de chaves?|Não. Após Olá que MEK é armazenado no Cofre de chaves, pode apenas ser utilizado para encriptação e desencriptação.|Não. Após Olá que MEK é armazenado no Cofre de chaves, pode apenas ser utilizado para encriptação e desencriptação.|
|Proprietário de instância do Cofre de chaves de Olá e Olá MEK?|Olá serviço do Data Lake Store|É proprietário de instância de Cofre de chaves de Olá, que pertence na sua própria subscrição do Azure. Olá MEK no Cofre de chaves pode ser gerido pelo software ou hardware.|
|Pode revogar acesso toohello MEK para Olá serviço do Data Lake Store?|Não|Sim. Pode gerir listas de controlo de acesso no Cofre de chaves e remover a identidade serviço toohello de entradas de controlo de acesso para Olá serviço do Data Lake Store.|
|Pode eliminar permanentemente Olá MEK?|Não|Sim. Se eliminar Olá MEK do Cofre de chaves, não não possível desencriptar os dados de Olá no Olá conta do Data Lake Store a qualquer pessoa, incluindo o serviço de arquivo Data Lake Olá. <br><br> Se tem explicitamente efetuada a cópia de segurança Olá MEK anterior toodeleting do Cofre de chaves, Olá MEK pode ser restaurado e, em seguida, podem ser recuperados dados Olá. No entanto, se não efetuou cópia de segurança Olá MEK anterior toodeleting-lo do Cofre de chaves, Olá no Olá conta do Data Lake Store podem nunca possível desencriptar os dados após essa data.|


Para além desta diferença de quem gere Olá MEK e Olá Cofre de chaves instância em que reside, rest Olá da estrutura de Olá é Olá mesmo para ambos os modos.

É importante tooremember seguinte de Olá Quando seleciona o modo de Olá Olá chaves de encriptação principal:

*   Pode escolher se o cliente toouse gerido chaves ou chaves de serviço gerida quando aprovisionar uma conta de Data Lake Store.
*   Depois de uma conta de Data Lake Store está aprovisionada, não é possível alterar o modo de Olá.

### <a name="encryption-and-decryption-of-data"></a>Encriptação e desencriptação de dados

Existem três tipos de chaves que são utilizadas na estrutura de Olá de encriptação de dados. Olá, a tabela seguinte fornece um resumo:

| Chave                   | Abreviatura | Associada a | Localização do armazenamento                             | Tipo       | Notas                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Chave de Encriptação Mestra | MEK          | Uma conta do Data Lake Store | Cofre de Chaves                              | Assimétrica | Pode ser gerida pelo Data Lake Store ou por si.                                                              |
| Chave de Encriptação de Dados   | DEK          | Uma conta do Data Lake Store | Armazenamento persistente, gerido pelo serviço Data Lake Store | Simétrica  | Olá DEK é encriptado pelo Olá MEK. Olá que DEK encriptado é o que é armazenado no suporte de dados persistente. |
| Chave de Encriptação de Blocos  | BEK          | Um bloco de dados | Nenhuma                                         | Simétrica  | Olá BEK é derivado de Olá DEK e blocos de dados de Olá.                                                      |

Olá seguinte diagrama ilustra estes conceitos:

![Chaves na encriptação de dados](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Algoritmo de pseudo quando um ficheiro é toobe desencriptado:
1.  Verifique se Olá DEK para a conta de Data Lake Store Olá em cache e pronto a ser utilizado.
    - Caso contrário, leia Olá encriptados DEK do armazenamento persistente e enviá-lo tooKey cofre toobe desencriptado. Olá cache desencriptar o DEK na memória. Está agora pronto toouse.
2.  Para cada bloco de dados no ficheiro de Olá:
    - Olá leitura encriptados bloco de dados do armazenamento persistente.
    - Gere Olá BEK de Olá DEK e bloco de encriptados Olá de dados.
    - Utilize Olá BEK toodecrypt dados.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Algoritmo de pseudo quando um bloco de dados é toobe encriptado:
1.  Verifique se Olá DEK para a conta de Data Lake Store Olá em cache e pronto a ser utilizado.
    - Caso contrário, leia Olá encriptados DEK do armazenamento persistente e enviá-lo tooKey cofre toobe desencriptado. Olá cache desencriptar o DEK na memória. Está agora pronto toouse.
2.  Gere um BEK exclusivo para o bloco de Olá de dados de Olá DEK.
3.  Encriptar o bloco de dados de Olá com Olá BEK, utilizando a encriptação AES 256.
4.  Bloco de dados encriptados de Olá de arquivo de dados no armazenamento persistente.

> [!NOTE] 
> Por motivos de desempenho, Olá DEK em Olá limpar é colocado em cache na memória para um curto período de tempo e é imediatamente eliminado posteriormente. No suporte de dados persistente, este é armazenado sempre encriptados pela Olá MEK.

## <a name="key-rotation"></a>Rotação de chaves

Quando estiver a utilizar chaves gerida pelo cliente, pode rodar Olá MEK. toolearn como tooset uma conta de Data Lake Store com chaves gerida pelo cliente, consulte [introdução](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Pré-requisitos

Quando configurar Olá conta do Data Lake Store, que escolheu toouse as suas próprias chaves. Esta opção não pode ser alterada depois Olá conta foi criada. Olá passos partem do princípio de que está a utilizar chaves gerida pelo cliente (ou seja, tiver escolhido as suas próprias chaves do Cofre de chaves).

Tenha em atenção que se utilizar opções predefinidas de Olá para encriptação, os dados são sempre encriptados através da utilização de chaves geridas pelo Data Lake Store. Nesta opção, não tem as chaves de Olá capacidade toorotate, como são geridos pelo Data Lake Store.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Como toorotate Olá MEK no Data Lake Store

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Procure a instância do Cofre de chaves de toohello que armazena as chaves associadas à sua conta do Data Lake Store. Selecione **Chaves**.

    ![Captura de ecrã do Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Selecione a chave de Olá associada com a sua conta do Data Lake Store e crie uma nova versão desta chave. Tenha em atenção que Data Lake Store atualmente apenas suporta a rotação da chave tooa nova versão de uma chave. Não suporta a rotação dos tooa outra chave.

   ![Captura de ecrã da janela Chaves, com a opção Nova Versão realçada](./media/data-lake-store-encryption/keynewversion.png)

4.  Procurar conta de armazenamento do Data Lake Store toohello e selecione **encriptação**.

    ![Captura de ecrã da janela da conta de armazenamento do Data Lake Store, com a opção Encriptação realçada](./media/data-lake-store-encryption/select-encryption.png)

5.  Uma mensagem notifica-o de que está disponível uma nova versão de chave da chave de Olá. Clique em **rodar chave** nova versão do tooupdate Olá toohello chave.

    ![Captura de ecrã da janela do Data Lake Store com a mensagem e a opção Rodar Chave realçadas](./media/data-lake-store-encryption/rotatekey.png)

Esta operação deve demorar menos de dois minutos e não existe nenhum período de indisponibilidade esperado devido tookey rotação. Depois de concluída a operação de Olá, a nova versão de Olá da chave de Olá está em utilização.
