---
title: "aaaCreate e gerir a base de dados do Azure PostgreSQL das regras de firewall utilizando Olá portal do Azure | Microsoft Docs"
description: "Criar e gerir a base de dados do Azure PostgreSQL das regras de firewall utilizando Olá portal do Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Criar e gerir a base de dados do Azure PostgreSQL das regras de firewall utilizando Olá portal do Azure
Regras de firewall ao nível do servidor ativar administradores tooaccess uma base de dados do Azure para o servidor de PostgreSQL a partir de um endereço IP especificado ou intervalo de endereços IP. 

## <a name="prerequisites"></a>Pré-requisitos
toostep através deste tooguide como, tem de:
- Um servidor [criar uma base de dados do Azure para PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Criar uma regra de firewall ao nível do servidor no Olá portal do Azure
1. No painel de servidor PostgreSQL Olá, em definições, clique em **ligação segurança** painel de segurança de ligação de Olá tooopen para Olá base de dados do Azure para PostgreSQL.

  ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Clique em **Adicionar IP do meu** na barra de ferramentas Olá. Isto irá criar automaticamente uma regra com o endereço IP Olá do seu computador, como percetível por Olá sistema do Azure.

  ![Portal do Azure – clique em Adicionar meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verifique o seu endereço IP antes de guardar a configuração de Olá. Em algumas situações, o endereço IP Olá observado pelo portal do Azure é diferente do endereço IP Olá utilizado quando aceder ao hello internet e os servidores do Azure. Por conseguinte, poderá ser necessário toochange Olá IP inicial e final IP toomake Olá regra função conforme esperado.
Utilize um motor de busca ou outra ferramenta online toocheck os seus próprios endereços IP (por exemplo, pesquisa de Bing "qual é o meu IP").

  ![Pesquisa do Bing para saber o que é o meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Adicione intervalos de endereços adicionais. Nas regras de Olá para Olá base de dados do Azure para PostgreSQL firewall, pode especificar um único endereço IP ou um intervalo de endereços. Se quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final IP. Ao abrir a firewall Olá permite que os administradores e utilizadores toologin tooany da base de dados no Olá PostgreSQL servidor toowhich têm credenciais válidas.

  ![Portal do Azure – regras de firewall ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Clique em **guardar** no Olá toosave da barra de ferramentas, esta regra de firewall ao nível do servidor. Aguarde a confirmação de Olá Olá regras de firewall de toohello de atualização foi concluída com êxito.

  ![Portal do Azure – clique em Guardar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gerir regras de firewall ao nível do servidor existente através de Olá portal do Azure
Repita Olá passos toomanage Olá as regras de firewall.
* tooadd Olá do computador atual, clique no botão de Olá demasiado + **Adicionar IP do meu**. Clique em **guardar** alterações de Olá toosave.
* endereços IP adicionais tooadd, escreva na Olá nome da regra, o endereço IP inicial e o endereço IP final. Clique em **guardar** alterações de Olá toosave.
* toomodify uma regra existente, clique em qualquer um dos campos de Olá na regra Olá e modificar. Clique em **guardar** alterações de Olá toosave.
* toodelete uma regra existente, clique em reticências Olá [...] e clicar eliminar remove Olá regra. Clique em **guardar** alterações de Olá toosave.

## <a name="next-steps"></a>Passos seguintes
- Da mesma forma, pode aplicar o script demasiado[criar e gerir a base de dados do Azure PostgreSQL das regras de firewall ao utilizar a CLI do Azure](howto-manage-firewall-using-cli.md)
- Para obter ajuda na ligação tooan base de dados do Azure para o servidor de PostgreSQL, consulte [bibliotecas de ligação para base de dados do Azure para PostgreSQL](concepts-connection-libraries.md)
