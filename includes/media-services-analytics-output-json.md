tarefa de Olá produz um ficheiro de saída JSON que contém metadados sobre faces detetados e controladas. metadados de Olá incluem coordenadas que indica a localização Olá faces, bem como um rosto ID número indicando que Olá controlo da que individuais. Números de ID de rostos em são suscetível tooreset em circunstâncias em enfrentam frontal Olá perdido, que se sobreponham a num intervalo de Olá, resultando em alguns indivíduos obter atribuídos a vários IDs.

Olá saída que JSON inclui Olá seguintes atributos:

| Elemento | Descrição |
| --- | --- |
| Versão |Isto refere-se versão toohello de Olá API de vídeo. |
| Índice | (Aplica-se apenas a tooAzure Redactor de suporte de dados) define o índice de moldura Olá de evento atual Olá. |
| escala temporal |"Ticks" por segundo de vídeo Olá. |
| deslocamento |Este é o desvio da hora Olá para carimbos de hora. Na versão 1.0 do vídeo APIs, este será sempre 0. No futuro cenários que suportamos, pode alterar este valor. |
| framerate |Fotogramas por segundo de Olá vídeo. |
| fragmentos |metadados de Olá é partes cópias de segurança em diferentes segmentos chamados fragmentos. Cada fragmento contém um início, a duração, o número do intervalo e o evento (s). |
| start |Olá hora de início da evento primeiro Olá 'ticks'. |
| Duração |comprimento de Olá de fragmento Olá, no "ticks". |
| intervalo |intervalo de Olá de cada entrada de evento no fragmento de Olá, no "ticks". |
| eventos |Cada evento contém faces Olá detetados e monitorizados dentro desse duração de tempo. É uma matriz de matriz de eventos. matriz externa Olá representa um intervalo de tempo. matriz interna Olá é constituído por 0 ou mais eventos que ocorreram neste ponto no tempo. Uma [Reto vazia] significa que nenhuma faces foram detetados. |
| ID |ID de Olá de rosto Olá que está a ser controlado. Este número poderá, inadvertidamente, alterar se um rosto torna-se determinados. Um indivíduo fornecido deve ter Olá mesmo ID ao longo de Olá vídeo em geral, mas este não poderá ser garantida devida toolimitations no algoritmo de deteção de Olá (occlusion, etc.) |
| x, y |canto superior esquerdo do Olá X e Y coordenadas de Olá enfrentam caixa delimitadora na escala normalizada de 0.0 too1.0. <br/>-X e Y coordenadas são uma toolandscape relativo sempre, pelo que o se tiver um vertical vídeo (ou upside pendente, no caso de Olá do iOS), terá de tootranspose Olá coordenadas em conformidade. |
| largura, altura |Olá sua largura e altura do Olá enfrentam caixa delimitadora na escala normalizada de 0.0 too1.0. |
| facesDetected |Este encontra-se no fim de Olá dos resultados JSON Olá e resume o número de Olá de faces esse algoritmo Olá detetado durante Olá vídeo. Porque Olá IDs pode ser reposto inadvertidamente, se um rosto torna-se determinados (por exemplo, enfrentam fica desligar o ecrã, procura ausente), este número poderá não sempre igual Olá verdadeiro diversas faces vídeo Olá. |

