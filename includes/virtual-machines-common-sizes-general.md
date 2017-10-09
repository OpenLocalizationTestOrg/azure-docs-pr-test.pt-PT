
<!-- A-series, Av2-series, D-series, Dv2-series, DS-series*, DSv2-series* -->

- Olá série A e série Av2 VMs podem ser implementadas numa variedade de tipos de hardware e os processadores. tamanho de Olá está limitado, com base no hardware de Olá, o desempenho do processador consistente toooffer para Olá executar instância, independentemente do hardware Olá que está implementada no. toodetermine Olá hardware físico em que este tamanho for implementado, consulta Olá hardware virtual numa Olá Máquina Virtual.

- VMs de série D são aplicações toorun concebida exigem maior capacidade de computação e o desempenho de disco temporário. VMs de série D fornecem processadores mais rápidos, numa proporção de memória para vCPU superior e uma unidade de estado sólido (SSD) para o disco temporário Olá. Para obter mais informações, consulte anúncio Olá no Olá blogue do Azure, [novos tamanhos de Máquina Virtual de série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

- Série Dv2, um toohello another série D original, funcionalidades uma CPU mais poderosa. Olá Dv2 série CPU é sobre 35% mais rapidamente do que Olá CPU de série D. Se baseia no Olá geração mais recente 2.4 GHz Intel Xeon® E5-2673 v3 processador (Haswell) e com Olá Intel Turbo intensificação tecnologia 2.0, pode ir segurança too3.1 GHz. tem de Olá Dv2 série Olá mesmas configurações de memória e o disco como Olá série D.

- os tamanhos de camada básico Olá são principalmente para cargas de trabalho de desenvolvimento e outras aplicações que não requerem o balanceamento de carga, dimensionamento automático ou memória intensivas máquinas virtuais. Para obter informações sobre os tamanhos de VMs mais adequados para aplicações de produção, veja (Tamanhos das máquinas virtuais) [virtual-machines-size-specs.md] e, para obter informações sobre os preços das VMs, veja [Preços de Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="dsv3-series"></a>Série Dsv3

ACU: 160-190

Tamanhos de série Dsv3 baseiam-se no Olá 2.3 GHz Intel XEON® E5-2673 v4 (Broadwell) processador e pode conseguir 3.5GHz com Intel Turbo intensificação tecnologia 2.0 e utilizar o armazenamento premium. os tamanhos de série Dsv3 Olá oferecem uma combinação de vCPU, memória e armazenamento temporário para a maioria das cargas de trabalho de produção.


| Tamanho             | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito máximo do armazenamento temporário e em cache: IOPS/MBps (tamanho da cache em GiB) | Débito máximo do disco não colocado em cache: IOPS/MBps | NICs. Máx. / Desempenho de rede esperado (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_D2s_v3  | 2      | 8           | 16             | 4              | 4,000 / 32 (50)                                                       | 3,200 / 48                                | 2/moderado                                   |
| Standard_D4s_v3  | 4      | 16          | 32             | 8              | 8,000 / 64 (100)                                                      | 6,400 / 96                                | 2/moderado                                   |
| Standard_D8s_v3  | 8      | 32          | 64             | 16             | 16,000 / 128 (200)                                                    | 12,800 / 192                              | 4 / alto                                       |
| Standard_D16s_v3 | 16     | 64          | 128            | 32             | 32,000 / 256 (400)                                                    | 25,600 / 384                              | 8 / alto                                       |


## <a name="dv3-series"></a>Série Dv3

ACU: 160-190

Tamanhos de série Dv3 baseiam-se no Olá 2.3 GHz Intel XEON® E5-2673 v4 (Broadwell) processador e pode conseguir 3.5GHz com Intel Turbo intensificação tecnologia 2.0. os tamanhos de série Dv3 Olá oferecem uma combinação de vCPU, memória e armazenamento temporário para a maioria das cargas de trabalho de produção.

O armazenamento de discos de dados são cobrados em separado das máquinas virtuais. toouse discos de armazenamento premium, utilize os tamanhos de Dsv3 Olá. Olá preços e faturação medidores para tamanhos de Dsv3 são Olá igual Dv3 série. 


| Tamanho            | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito do armazenamento temporário máximo: IOPS/MBps de Leitura/MBps de Escrita | NICs/Largura de banda da rede máximos |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_D2_v3  | 2         | 8           | 50             | 4              | 3000/46/23                                               | 2/moderado                 |
| Standard_D4_v3  | 4         | 16          | 100            | 8              | 6000/93/46                                               | 2/moderado                 |
| Standard_D8_v3  | 8         | 32          | 200            | 16             | 12000/187/93                                             | 4 / alto                     |
| Standard_D16_v3 | 16        | 64          | 400            | 32             | 24000/375/187                                            | 8 / alto                     |


## <a name="dsv2-series"></a>Série DSv2

ACU: 210-250

| Tamanho | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito máximo do armazenamento temporário e em cache: IOPS/MBps (tamanho da cache em GiB) | Débito máximo do disco não colocado em cache: IOPS/MBps | NICs. Máx. / Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1_v2 |1 |3.5 |7 |2 |4,000 / 32 (43) |3,200 / 48 |2 / 750 |
| Standard_DS2_v2 |2 |7 |14 |4 |8,000 / 64 (86) |6,400 / 96 |2 / 1500 |
| Standard_DS3_v2 |4 |14 |28 |8 |16,000 / 128 (172) |12,800 / 192 |4 / 3000 |
| Standard_DS4_v2 |8 |28 |56 |16 |32,000 / 256 (344) |25,600 / 384 |8 / 6000 |
| Standard_DS5_v2 |16 |56 |112 |32 |64,000 / 512 (688) |51,200 / 768 |8 / 6000 - 12000 &#8224;|



## <a name="dv2-series"></a>Série Dv2

ACU: 210-250

| Tamanho              | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Débito do armazenamento temporário máximo: IOPS/MBps de Leitura/MBps de Escrita | Máximo do disco de dados/débito: IOPS | NICs. Máx. / Desempenho de rede esperado (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1_v2    | 1         | 3.5         | 50             | 3000 / 46 / 23                                           | 2 / 2x500                         | 2 / 750                 |
| Standard_D2_v2    | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1500                     |
| Standard_D3_v2    | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 3000                     |
| Standard_D4_v2    | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 6000                     |
| Standard_D5_v2    | 16        | 56          | 800            | 48000 / 750 / 375                                        | 32 / 32x500                       | 8 / 6000 - 12000 &#8224;          |


<br>

## <a name="ds-series"></a>Série DS

ACU: 160

| Tamanho | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito máximo do armazenamento temporário e em cache: IOPS/MBps (tamanho da cache em GiB) | Débito máximo do disco não colocado em cache: IOPS/MBps | NICs. Máx. / Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1 |1 |3.5 |7 |2 |4,000 / 32 (43) |3,200 / 32 |2 / 500 |
| Standard_DS2 |2 |7 |14 |4 |8,000 / 64 (86) |6,400 / 64 |2 / 1000 |
| Standard_DS3 |4 |14 |28 |8 |16,000 / 128 (172) |12,800 / 128 |4 / 2000 |
| Standard_DS4 |8 |28 |56 |16 |32,000 / 256 (344) |25,600 / 256 |8 / 4000 |

<br>

## <a name="d-series"></a>Série D 

ACU: 160

| Tamanho         | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Débito do armazenamento temporário máximo: IOPS/MBps de Leitura/MBps de Escrita | Máximo do disco de dados/débito: IOPS | NICs. Máx. / Desempenho de rede esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1  | 1         | 3.5         | 50             | 3000 / 46 / 23                                           | 2 / 2x500                         | 2 / 500                 |
| Standard_D2  | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1000                     |
| Standard_D3  | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 2000                     |
| Standard_D4  | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 4000                     |

<br>


## <a name="av2-series"></a>Série Av2

ACU: 100

| Tamanho            | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Débito do armazenamento temporário máximo: IOPS/MBps de Leitura/MBps de Escrita | Máximo do disco de dados/débito: IOPS | NICs. Máx. / Desempenho de rede esperado (Mbps) | 
|-----------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_A1_v2  | 1         | 2           | 10             | 1000 / 20 / 10                                           | 2 / 2x500               | 2 / 250                 |
| Standard_A2_v2  | 2         | 4           | 20             | 2000 / 40 / 20                                           | 4 / 4x500               | 2 / 500                 |
| Standard_A4_v2  | 4         | 8           | 40             | 4000 / 80 / 40                                           | 8 / 8x500               | 4 / 1000                     |
| Standard_A8_v2  | 8         | 16          | 80             | 8000 / 160 / 80                                          | 16 / 16x500             | 8 / 2000                     |
| Standard_A2m_v2 | 2         | 16          | 20             | 2000 / 40 / 20                                           | 4 / 4x500               | 2 / 500                 |
| Standard_A4m_v2 | 4         | 32          | 40             | 4000 / 80 / 40                                           | 8 / 8x500               | 4 / 1000                     |
| Standard_A8m_v2 | 8         | 64          | 80             | 8000 / 160 / 80                                          | 16 / 16x500             | 8 / 2000                     |

<br>

## <a name="a-series"></a>Série A

ACU: 50-100

| Tamanho | vCPU | Memória: GiB | Armazenamento (HDD) temporário: GiB | Discos de dados máximos | Débito máximo do disco de dados: IOPS | NICs. Máx. / Desempenho de rede esperado (Mbps)  |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A0* |1 |0.768 |20 |1 |1x500 |2 / 100 |
| Standard_A1 |1 |1.75 |70 |2 |2x500 |2 / 500  |
| Standard_A2 |2 |3.5 |135 |4 |4x500 |2 / 500 |
| Standard_A3 |4 |7 |285 |8 |8x500 |2 / 1000 |
| Standard_A4 |8 |14 |605 |16 |16x500 |4 / 2000 |
| Standard_A5 |2 |14 |135 |4 |4x500 |2 / 500 |
| Standard_A6 |4 |28 |285 |8 |8x500 |2 / 1000 |
| Standard_A7 |8 |56 |605 |16 |16x500 |4 / 2000 |
<br>

* Olá A0 tamanho é excessiva subscrito no hardware físico Olá. Para este tamanho específico apenas, outras implementações de cliente podem afetar o desempenho de Olá da sua carga de trabalho em execução. desempenho relativo Olá é descrito abaixo como Olá esperado da linha de base, assunto tooan aproximado variabilidade de percentagem de 15.

### <a name="standard-a0---a4-using-cli-and-powershell"></a>Standard A0 a A4 que utiliza a CLI e o PowerShell
No modelo de implementação clássica Olá, alguns nomes de tamanho VM são ligeiramente diferentes na CLI e o PowerShell:

* Standard_A0 é ExtraSmall 
* Standard_A1 é Small
* Standard_A2 é Medium
* Standard_A3 é Large
* Standard_A4 é ExtraLarge

## <a name="basic-a"></a>Básico A

|Tamanho – Tamanho\Nome | vCPU |Memória|NICs (Máx)|Tamanho máximo do disco temporário |Um máximo de discos de dados 1023 GB cada)|Um máximo de IOPS (300 por disco)|
|---|---|---|---|---|---|---|
|A0\Basic_A0|1|768 MB|2| 20 GB|1|1 x 300|
|A1\Basic_A1|1|1,75 GB|2| 40 GB |2|2 x 300|
|A2\Basic_A2|2|3,5 GB|2| 60 GB|4|4 x 300|
|A3\Basic_A3|4|7 GB|2| 120 GB |8|8 x 300|
|A4\Basic_A4|8|14 GB|2| 240 GB |16|16 x 300|
