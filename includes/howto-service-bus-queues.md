## <a name="what-are-service-bus-queues"></a>O que são filas do Service Bus?
As filas do Service Bus suportam um modelo de comunicação de **mensagens mediadas**. Ao utilizar filas, os componentes de uma aplicação distribuída não comunicam diretamente entre si; trocam antes mensagens através de uma fila, que funciona como um intermediário (mediador). Um produtor de mensagens (remetente) entrega uma fila de toohello de mensagens e, em seguida, prossegue com o processamento. No modo assíncrono, um consumidor de mensagens (recetor) obtém a mensagem de saudação da fila de Olá e processa-os. produtor Olá não possui toowait para uma resposta do consumidor Olá na ordem toocontinue tooprocess e enviar mais mensagens. As filas oferecem **First In, First Out (FIFO)** mensagem entrega tooone ou mais consumidores concorrentes. Ou seja, as mensagens são normalmente recebidas e processadas por recetores segundo Olá Olá ordem pela qual foram adicionadas toohello fila, e cada mensagem é recebida e processada por apenas um consumidor de mensagens.

![QueueConcepts](./media/howto-service-bus-queues/sb-queues-08.png)

As filas do Service Bus são uma tecnologia para fins gerais que pode ser utilizada para uma vasta gama de cenários:

* Comunicação entre funções da Web e de trabalho numa aplicação Azure multicamadas.
* Comunicação entre aplicações no local e aplicações alojadas no Azure numa solução híbrida.
* Comunicação entre componentes de uma aplicação distribuída em execução no local em diferentes organizações ou departamentos de uma organização.

Utilizar as filas permite tooscale as aplicações mais facilmente e ativar a arquitetura de tooyour mais resiliência.


