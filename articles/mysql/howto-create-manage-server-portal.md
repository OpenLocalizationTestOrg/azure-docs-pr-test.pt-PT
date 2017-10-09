---
title: aaaCreate e gerir a base de dados do Azure para o servidor de MySQL utilizando o portal do Azure | Microsoft Docs
description: "Este artigo descreve como pode rapidamente criar uma nova base de dados do Azure para o servidor de MySQL e gerir o servidor de Olá utilizando Olá Portal do Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Criar e gerir a base de dados do Azure para o servidor de MySQL utilizando o portal do Azure
Este artigo descreve como pode rapidamente criar uma nova base de dados do Azure para o servidor de MySQL e gerir o servidor de Olá utilizando Olá Portal do Azure. Gestão de servidor inclui visualizar detalhes do servidor e as bases de dados, repor palavra-passe e a eliminação Olá servidor.

## <a name="log-in-toohello-azure-portal"></a>Início de sessão toohello portal do Azure
Inicie sessão no toohello [portal do Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Criar uma Base de Dados do Azure para o servidor MySQL
Siga estes passos toocreate uma base de dados do Azure para o servidor de MySQL com o nome "mysqlserver4demo"

Clique 1 **novo** botão encontrado no canto esquerda superior Olá de Olá portal do Azure.

Selecione 2 **bases de dados** da página Olá e selecione **base de dados do Azure para MySQL** da página de bases de dados de Olá.

> É criada uma base de dados do Azure para o servidor de MySQL com um conjunto definido de [computação e armazenamento](./concepts-compute-unit-and-storage.md) recursos. base de dados de Olá é criado dentro de um grupo de recursos do Azure e numa base de dados do Azure para o servidor de MySQL.

![Criar novo-servidor](./media/howto-create-manage-server-portal/create-new-server.png)

3 - preencha Olá base de dados do Azure para o formulário de MySQL com Olá seguintes informações:

| **Campo do Formulário** | **Descrição do Campo** |
|----------------|-----------------------|
| *Nome do servidor* | Azure mysql (nome do servidor é exclusivo global) |
| *Subscrição* | MySQLaaS (selecione na lista pendente) |
| *Grupo de recursos* | MyResource (criar um novo grupo de recursos ou utilize uma já existente) |
| *Início de sessão de administrador do servidor* | myadmin (configure o nome da conta de administração) |
| *Palavra-passe* | palavra-passe de conta de administrador a configuração |
| *Confirmar palavra-passe* | confirme a palavra-passe da conta de administrador |
| *Localização* | Europa do Norte (selecione entre Europa do Norte e EUA oeste) |
| *Versão* | 5.6 (escolher a base de dados do Azure para a versão do servidor MySQL) |

Clique 4 **escalão de preço** toospecify Olá camada e o desempenho do nível de serviço para o novo servidor. Unidade pode ser configurada entre 50 e 100 na camada básica, 100 e 200 no escalão Standard, e o armazenamento pode ser adicionado, com base na quantidade incluída de computação. Para este guia HowTo, vamos escolha a unidade de computação de 50 e 50GB. Clique em **OK** toosave a seleção.
![Criar-server--escalão de preço](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

Clique 5 **criar** servidor de Olá tooprovision. O aprovisionamento demora alguns minutos.

> Verifique Olá **Pin toodashboard** controlo de fácil tooallow opção das implementações.
> [!NOTE]
> Apesar de segurança too1000GB na camada básica e 10000GB padrão camada será suportada para armazenamento, para a pré-visualização pública, o armazenamento máximo Olá está temporariamente too1000GB ainda limitado. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Atualizar uma base de dados do Azure para o servidor de MySQL
Depois do novo servidor é aprovisionado, o utilizador tem 2 opções tooedit um servidor existente: Repor palavra-passe de administrador ou escala cima/para baixo servidor Olá alterando computação-unidades de Olá.

### <a name="change-hello-administrator-user-password"></a>Palavra-passe de utilizador do administrador de Olá de alteração
1 - no servidor de Olá **descrição geral** painel, clique em **Repor palavra-passe** toopopulate uma janela de entrada e a confirmação da palavra-passe.

2 - Introduza a nova palavra-passe e Confirmar palavra-passe de Olá na janela de Olá como abaixo: ![reposição de palavra-passe](./media/howto-create-manage-server-portal/reset-password.png)

Clique 3 **OK** toosave Olá nova palavra-passe.

### <a name="scale-updown-by-changing-compute-units"></a>Escala para cima/para baixo alterando as unidades de computação

1 - no painel do servidor de Olá, sob **definições**, clique em **escalão de preço** tooopen Olá preços camada painel Olá base de dados do Azure para o servidor de MySQL.

Passo 2-siga 4 no **criar uma base de dados do Azure para o servidor de MySQL** toochange unidades de computação por Olá mesmo escalão de preço.

## <a name="delete-an-azure-database-for-mysql-server"></a>Eliminar uma base de dados do Azure para o servidor de MySQL

1 - no servidor de Olá **descrição geral** painel, clique em **eliminar** painel de confirmação de eliminação tooopen Olá comando botão.

Nome de servidor correto de tipo de 2 Olá na caixa de entrada do painel de Olá confirmação duplo.

Clique 3 **eliminar** botão novamente tooconfirm eliminar ação e aguarde pop-up "Eliminar êxito" na barra de notificação de Olá.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Lista Olá base de dados do Azure para bases de dados MySQL
No servidor de Olá **descrição geral** painel, desloque para baixo até ver a base de dados de Olá mosaico na parte inferior de Olá. Todas as bases de dados de Olá serão apresentados na tabela de Olá. Clique em **eliminar** painel de confirmação de eliminação tooopen Olá comando botão.

![Mostrar-bases de dados](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Mostrar detalhes de uma base de dados do Azure para o servidor de MySQL
Clique em **propriedades** em **definições** no servidor de Olá painel será aberto Olá **propriedades** painel. Em seguida, pode ver todas as informações detalhadas sobre o servidor de Olá.

## <a name="next-steps"></a>Passos seguintes

[Início rápido: Criar a base de dados do Azure para o servidor de MySQL utilizando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
