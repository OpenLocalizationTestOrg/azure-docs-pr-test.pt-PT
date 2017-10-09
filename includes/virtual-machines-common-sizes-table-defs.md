
## <a name="size-table-definitions"></a>Definições da tabela de dimensionamento

- A capacidade de armazenamento é apresentada em unidades de GiB ou 1024^3 bytes. Quando a comparação com discos medido em GB (1000 ^ 3 bytes) toodisks medido em GiB (1024 ^ 3) não se esqueça de que os números de capacidade fornecidos no GiB podem aparecer mais pequenos. Por exemplo, 1023 GiB = 1098,4 GB
- O débito do disco é medido em operações de entrada/saída por segundo (IOPS) e MBps, em que MBps = 10^6 bytes/seg.
- Os discos de dados podem operar nos modos em cache ou não colocado em cache. Para a operação de disco de dados em cache, o modo de cache do anfitrião Olá estiver definido demasiado**ReadOnly** ou **ReadWrite**.  Para a operação de disco de dados uncached, o modo de cache do anfitrião Olá estiver definido demasiado**nenhum**.
- **Era esperado o desempenho da rede** é Olá agregados largura de banda máxima alocada por tipo VM em todos os NICs para todos os destinos. Os limites superiores não são garantidos, mas são tooprovide pretendido orientações para selecionar o tipo de direito VM Olá para aplicação Olá pretendido. O desempenho de rede real irá depender de vários fatores, incluindo congestionamento, cargas e definições da rede. Para obter mais informações sobre a otimização do débito de rede, veja [Otimizar o débito de rede para Windows e Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Olá tooachieve esperado o desempenho da rede no Linux ou Windows, poderá ser necessário tooselect uma versão específica ou otimizar a VM. Para obter mais informações, consulte [como tooreliably teste para a máquina virtual débito](../articles/virtual-network/virtual-network-bandwidth-testing.md).

- &#8224; 16 vCPU desempenho consistentemente será atingir o limite superior de Olá uma versão futura.


