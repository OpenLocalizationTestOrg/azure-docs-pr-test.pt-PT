---
title: "aaaCreate e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando Olá portal do Azure | Microsoft Docs"
description: "Criar e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando Olá portal do Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Criar e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando Olá portal do Azure
Regras de firewall ao nível do servidor ativar administradores tooaccess uma base de dados do Azure para o servidor de MySQL a partir de um endereço IP especificado ou intervalo de endereços IP. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Criar uma regra de firewall ao nível do servidor no Olá portal do Azure

1. No painel server, MySQL Olá, em definições, clique em **ligação segurança** painel de segurança de ligação de Olá tooopen para Olá base de dados do Azure para MySQL.

   ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Clique em **Adicionar IP do meu** na barra de ferramentas de Olá toocreate uma regra com o endereço IP Olá do seu computador, como interpretadas pela Olá sistema do Azure.

   ![Portal do Azure – clique em Adicionar meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verifique o seu endereço IP antes de guardar a configuração de Olá. Em algumas situações, o endereço IP Olá observado pelo portal do Azure é diferente do endereço IP Olá utilizado quando aceder ao hello internet e os servidores do Azure. Por conseguinte, poderá ser necessário toochange Olá IP inicial e final IP toomake Olá regra função conforme esperado.

   Utilizar um motor de busca ou outra ferramenta online toocheck o seu próprio endereço IP (por exemplo, pesquisar "qual é o meu endereço IP").

   ![Bing para saber o que é o meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Adicione intervalos de endereços adicionais. Nas regras de Olá para Olá base de dados do Azure para firewall de MySQL, pode especificar um único endereço IP ou um intervalo de endereços. Se quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final IP. Ao abrir a firewall Olá permite que os administradores e utilizadores tooaccess qualquer base de dados no Olá MySQL servidor toowhich têm credenciais válidas.

   ![Portal do Azure – regras de firewall ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Clique em **guardar** no Olá toosave da barra de ferramentas, esta regra de firewall ao nível do servidor. Aguarde a confirmação de Olá Olá regras de firewall de toohello de atualização foi concluída com êxito.

   ![Portal do Azure – clique em Guardar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gerir regras de firewall ao nível do servidor existente através de Olá portal do Azure
Repita Olá passos toomanage Olá as regras de firewall.
* tooadd Olá do computador atual, clique em **+ adicionar My IP**.
* endereços IP adicionais tooadd, escreva Olá **nome da regra**, **IP inicial**, e **IP final**.
* toomodify uma regra existente, clique em qualquer um dos campos de Olá na regra Olá e modificar.
* regra de toodelete existente, clique o botão de reticências Olá […] e clique em **eliminar**.
* Clique em **guardar** alterações de Olá toosave.

## <a name="next-steps"></a>Passos seguintes
- Para obter ajuda na ligação tooan base de dados do Azure para o servidor de MySQL, consulte [bibliotecas de ligação para base de dados do Azure para MySQL](./concepts-connection-libraries.md)
