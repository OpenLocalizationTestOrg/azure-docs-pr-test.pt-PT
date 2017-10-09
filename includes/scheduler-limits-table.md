Olá, a tabela seguinte descreve cada um dos quotas de principais de Olá, limites, predefinições e limitações no agendador do Azure.

| Recurso | Descrição de limite |
| --- | --- |
| **Tamanho de tarefa** |O tamanho de tarefas máxima é 16K. Se um PUT ou de um PATCH resulta numa tarefa maior do que estes limites, é devolvido um código de estado pedido incorreto 400. |
| **Tamanho do URL do pedido** |Tamanho máximo do URL de pedido de Olá é 2048 carateres. |
| **Tamanho do cabeçalho agregado** |Tamanho do cabeçalho de agregação máximo é 4096 carateres. |
| **Contagem de cabeçalho** |Contagem de cabeçalho máximo é 50 cabeçalhos. |
| **Tamanho do corpo** |Tamanho máximo de corpo é 8192 carateres. |
| **Intervalo de periodicidade** |O intervalo de periodicidade máximo é 18 meses. |
| **Tempo de toostart de tempo** |"Hora de toostart de tempo" de máximo é 18 meses. |
| **Histórico de tarefas** |Corpo da resposta máximo armazenado no histórico da tarefa é 2048 bytes. |
| **Frequência** |quota de frequência máxima predefinida de Olá é 1 hora de uma coleção de tarefas gratuitas e 1 minuto uma coleção de tarefas padrão. a frequência máxima Olá é configurável num toobe de coleção de tarefas inferior ao máximo Olá. Todas as tarefas na coleção de tarefas Olá são definidas na coleção de tarefas Olá de valor de Olá limitado. Se tentar toocreate uma tarefa com uma frequência superior à frequência de máximo de Olá na coleção de tarefas Olá pedido irá falhar com um código de estado de conflito 409. |
| **Tarefas** |quota de tarefas máxima predefinida de Olá é 5 tarefas numa coleção de tarefas gratuitas e 50 tarefas numa coleção de tarefas padrão. número máximo de Olá de tarefas é configurável na coleção de tarefas. Todas as tarefas na coleção de tarefas Olá são definidas na coleção de tarefas Olá de valor de Olá limitado. Se tentar toocreate mais tarefas do que a quota de tarefas máxima Olá, em seguida, o pedido de Olá falha com um código de estado de conflito 409. |
| **Coleções de tarefas** |Número máximo de coleção de tarefas por subscrição é inferior 200.000. |
| **Retenção do histórico de tarefas** |Histórico da tarefa é retido durante a cópia de segurança too2 meses ou cópia de segurança toohello última execuções de 1000. |
| **Retenção de tarefa concluídas e falhadas** |As tarefas concluídas e falhadas são retidas por 60 dias. |
| **Tempo limite** |Não há um tempo de limite de pedido (não configurável) estático de 60 segundos para ações de HTTP. Para mais operações em execução, siga protocolos assíncronos de HTTP; Por exemplo, devolver um 202 imediatamente mas continuar a trabalhar em segundo plano de Olá. |

