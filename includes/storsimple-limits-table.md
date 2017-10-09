<!--author=alkohli last changed: 12/15/15-->

| Identificador de limite | Limite | Comentários |
| --- | --- | --- |
| Número máximo de credenciais da conta de armazenamento |64 | |
| Número máximo de contentores de volume |64 | |
| Número máximo de volumes |255 | |
| Número máximo de agendas por modelo de largura de banda |168 |Uma agenda para cada hora, todos os dias da semana de Olá (24 * 7). |
| Tamanho máximo de um volume em camadas em dispositivos físicos |64 TB para 8100 e 8600 |8100 e 8600 são dispositivos físicos. |
| Tamanho máximo de um volume em camadas em dispositivos virtuais no Azure |30 TB para 8010 <br></br> 64 TB para o 8020 |dispositivos 8010 e 8020 são dispositivos virtuais no Azure que utilizam o armazenamento Standard e Premium, respetivamente. |
| Tamanho máximo de um volume localmente afixado nos dispositivos físicos |9 TB para 8100 <br></br> 24 TB para 8600 |8100 e 8600 são dispositivos físicos. |
| Número máximo de ligações de iSCSI |512 | |
| Número máximo de ligações de iSCSI de iniciadores |512 | |
| Número máximo de registos de controlo de acesso por dispositivo |64 | |
| Número máximo de volumes de acordo com a política de cópia de segurança |24 | |
| Número máximo de cópias de segurança retidos por política de cópia de segurança |64 | |
| Número máximo de agendas de acordo com a política de cópia de segurança |10 | |
| Número máximo de instantâneos de qualquer tipo que podem ser mantidas por volume |256 |Isto inclui instantâneos locais e instantâneos de nuvem. |
| Número máximo de instantâneos que podem constar de qualquer dispositivo |10,000 | |
| Número máximo de volumes que podem ser processados em paralelo para cópia de segurança, restauro ou clonar |16 |<ul><li>Se existirem mais de 16 volumes, serão processados sequencialmente como processamento ranhuras fiquem disponíveis.</li><li>Novas cópias de segurança de um clonado ou restaurado volume em camadas não pode ocorrer até que a operação de Olá esteja concluída. No entanto, para um volume local, as cópias de segurança são permitidas depois de volume Olá está online.</li></ul> |
| Restaurar e clonar o tempo de recuperar volumes em camadas |< 2 minutos |<ul><li>volume de Olá é disponibilizada em dois minutos da operação de restauro ou um clone, independentemente do tamanho do volume Olá.</li><li>desempenho de volume de Olá inicialmente pode ser mais lento do que o normal como a maioria dos metadados e dados de Olá ainda reside na nuvem de Olá. Pode aumentar o desempenho como fluxos de dados do dispositivo StorSimple do Olá nuvem toohello.</li><li>metadados de toodownload Olá tempo total dependem Olá atribuído o tamanho do volume. Metadados é automaticamente colocados em dispositivo Olá em segundo plano de Olá a taxa de Olá de 5 minutos por TB de dados do volume alocado. Esta taxa pode ser afetada pela nuvem de toohello de largura de banda de Internet.</li><li>Olá restauro ou operação de clonagem está concluída quando todos os metadados de Olá estão nos dispositivos de Olá.</li><li>Não não possível efetuar operações de cópia de segurança até que o restauro de Olá ou operação de clonagem é totalmente concluída. |
| Restaurar o tempo de recuperação de volumes localmente afixados |< 2 minutos |<ul><li>volume de Olá é disponibilizada em dois minutos da operação de restauro Olá, independentemente do tamanho do volume Olá.</li><li>desempenho de volume de Olá inicialmente pode ser mais lento do que o normal como a maioria dos metadados e dados de Olá ainda reside na nuvem de Olá. Pode aumentar o desempenho como fluxos de dados do dispositivo StorSimple do Olá nuvem toohello.</li><li>metadados de toodownload Olá tempo total dependem Olá atribuído o tamanho do volume. Metadados é automaticamente colocados em dispositivo Olá em segundo plano de Olá a taxa de Olá de 5 minutos por TB de dados do volume alocado. Esta taxa pode ser afetada pela nuvem de toohello de largura de banda de Internet.</li><li>Ao contrário de volumes em camadas, no caso de Olá de volumes localmente afixados, dados do volume de Olá também são transferidos localmente no dispositivo Olá. operação de restauro Olá está concluída quando todos os dados do volume de Olá esteja toohello dispositivo.</li><li>operações de restauro Olá podem ser longas e restauro de Olá Olá tempo total toocomplete dependerão o tamanho do volume local Olá aprovisionado, da largura de banda de Internet e Olá existente dados no dispositivo Olá Olá. Operações de cópia de segurança no volume localmente afixado de Olá são permitidas enquanto a operação de restauro de Olá está em curso. |
| Disponibilidade de restauro dinâmico |Última ativação pós-falha | |
| Débito de leitura/escrita do máximo de clientes (quando servido a partir da camada SSD Olá) * |920/720 MB/s com um único 10GbE interface de rede |Cópia de segurança too2x com duas interfaces de rede e o MPIO. |
| Débito de leitura/escrita do máximo de clientes (quando servido a partir da camada HDD de Olá) * |120/250 MB/s | |
| Débito de leitura/escrita do máximo de clientes (quando servido a partir da camada de nuvem Olá) * |11/41 MB/s |Débito de leitura depende clientes gerar e manter a profundidade de fila de e/s suficiente. |

&#42; Débito máximo por tipo de e/s foi medido com cenários de 100 por cento escrita e leitura de 100 por cento. Débito real pode ser mais baixo e depende de e/s misturar e condições de rede.

