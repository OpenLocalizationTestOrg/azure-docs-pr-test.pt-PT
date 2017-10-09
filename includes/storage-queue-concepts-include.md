## <a name="what-is-queue-storage"></a>O que é o Armazenamento de Filas?
Armazenamento de filas do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acedidas de qualquer local no mundo Olá através de chamadas autenticadas com HTTP ou HTTPS. Uma mensagem de fila única pode ser segurança too64 KB de tamanho e uma fila pode conter milhões de mensagens, cópia de segurança toohello limite da capacidade total de uma conta de armazenamento.

Utilizações comuns do Armazenamento de filas:

* Criar um registo de segurança de trabalho tooprocess de forma assíncrona
* Transmissão de mensagens de uma função de trabalho do Azure de tooan de função web do Azure

## <a name="queue-service-concepts"></a>Conceitos do Serviço Fila
Olá serviço fila contém Olá os seguintes componentes:

![Queue1](./media/storage-queue-concepts-include/queue1.png)

* **Formato de URL:** ficheiros são endereçáveis com Olá segue o formato de URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Olá seguinte URL endereça uma fila no diagrama de Olá:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Conta de armazenamento:** todas as acesso tooAzure armazenamento é feito através de uma conta de armazenamento. Veja [Metas de Desempenho e Escalabilidade do Storage do Azure](../articles/storage/common/storage-scalability-targets.md) para obter detalhes acerca da capacidade das contas de armazenamento.
* **Fila:** uma fila contém um conjunto de mensagens. Todas as mensagens têm de estar numa fila. Tenha em atenção de que nome da fila Olá tem de ser todo em minúsculas. Para obter informações sobre a nomenclatura de filas, veja [Nomenclatura de Filas e Metadados](https://msdn.microsoft.com/library/azure/dd179349.aspx).
* **Mensagem:** A mensagem, em qualquer formato de cópia de segurança too64 KB. Olá o tempo máximo que uma mensagem pode permanecer na fila de Olá é de 7 dias.

