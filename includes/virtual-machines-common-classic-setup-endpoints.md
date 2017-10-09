
Cada ponto final tem um *Porta pública* e um *porta privada*:

* Porta pública Olá é utilizada pelo toolisten de Balanceador de carga do Azure Olá para receber tráfego toohello máquina virtual a partir Olá Internet.
* Porta privada Olá é utilizada pelo Olá toolisten de máquina virtual para receber tráfego, tooan normalmente destinados a aplicação ou serviço em execução na máquina virtual de Olá.

Os valores predefinidos para Olá protocolo de endereço IP e portas TCP ou UDP para protocolos de rede bem conhecidos são fornecidas quando criar pontos finais com Olá portal do Azure. Para os pontos finais personalizados, terá de toospecify Olá correto protocolo IP (TCP ou UDP) e as portas públicas e privadas do Olá. tráfego de entrada toodistribute aleatoriamente em várias máquinas virtuais, terá de toocreate um conjunto com balanceamento de carga constituídas por vários pontos finais.

Depois de criar um ponto final, pode utilizar um controlo lista (ACL) toodefine as regras de acesso que permitem ou negam o tráfego de entrada Olá toohello Porta pública do ponto final de Olá com base no respetivo endereço IP de origem. No entanto, se a máquina virtual de Olá numa rede virtual do Azure, deve de utilizar grupos de segurança de rede em vez disso. Para obter mais informações, consulte [sobre grupos de segurança de rede](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> Configuração da firewall para máquinas virtuais do Azure é efetuada automaticamente para as portas associadas a pontos finais de conectividade remota que Azure configura automaticamente. Para as portas especificadas para todos os outros pontos finais, nenhuma configuração é feita automaticamente toohello firewall da máquina virtual de Olá. Quando cria um ponto final da máquina virtual de Olá, terá de tooensure Olá firewall da máquina virtual de Olá também permite que o tráfego de Olá de protocolo de Olá e configuração de ponto final de toohello porta privada correspondente. tooconfigure Olá firewall, consulte a documentação de Olá ou a ajuda online para o sistema de operativo Olá em execução na máquina virtual de Olá.
>
>

## <a name="create-an-endpoint"></a>Criar um ponto final
1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **máquinas virtuais**e, em seguida, clique no nome de Olá da máquina virtual de Olá que pretende que o tooconfigure.
3. Clique em **pontos finais** no Olá **definições** grupo. Olá **pontos finais** todos os Olá atual pontos finais para a máquina virtual de Olá listas de páginas. (Este exemplo é uma VM do Windows. Um VM do Linux por predefinição apresentará um ponto final de SSH.)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Pontos Finais](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Na barra de comando de Olá acima entradas de ponto final de Olá, clique em **adicionar**.
5. No Olá **adicionar ponto final** , escreva um nome para o ponto final de Olá no **nome**.
6. No **protocolo**, escolha o **TCP** ou **UDP**.
7. No **Porta pública**, escreva o número de porta de Olá para tráfego de entrada de Olá de Olá Internet. No **porta privada**, escreva o número de porta de Olá no qual Olá máquina virtual está a escutar. Estes números de porta podem ser diferentes. Certifique-se de que Olá firewall na máquina virtual de Olá tiver sido configurado tooallow Olá tráfego correspondente toohello protocolo (no passo 6) e uma porta privada.
10. Clique em **OK**.

Olá novo ponto final de será listado no Olá **pontos finais** página.

![Criação do ponto final com êxito](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Gerir Olá ACL num ponto final
conjunto de Olá toodefine de computadores que podem enviar tráfego, Olá ACL num ponto final pode restringir o tráfego com base no endereço IP de origem. Siga estes passos tooadd, modificar ou remover uma ACL num ponto final.

> [!NOTE]
> Se o ponto final de Olá faz parte de um conjunto com balanceamento de carga, quaisquer alterações que efetuar toohello ACL num ponto final são pontos finais de tooall aplicada no conjunto de Olá.
>
>

Se a máquina virtual de Olá numa rede virtual do Azure, recomendamos que grupos de segurança de rede em vez de ACLs. Para obter mais informações, consulte [sobre grupos de segurança de rede](../articles/virtual-network/virtual-networks-nsg.md).

1. Se ainda não o fez, inicie sessão no toohello portal do Azure.
2. Clique em **máquinas virtuais**e, em seguida, clique no nome de Olá da máquina virtual de Olá que pretende que o tooconfigure.
3. Clique em **Pontos Finais**. Na lista de Olá, selecione o ponto final adequado de Olá. a lista de ACL Olá é Olá parte inferior da página Olá.

   ![Especifique os detalhes ACL](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Utilize as linhas em Olá lista tooadd, eliminar ou editar regras para uma ACL e alterar a sua ordem. Olá **sub-rede remota** valor é um intervalo de endereços IP para o tráfego de entrada de Olá Internet que Olá toopermit de utilizações de Balanceador de carga do Azure ou negar o tráfego de Olá com base no respetivo endereço IP de origem. Ser se toospecify Olá intervalo de endereços IP no formato CIDR, também conhecido como formato de prefixo de endereço. Um exemplo é `10.1.0.0/8`.

 ![Nova entrada ACL](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


Pode utilizar regras tooallow o tráfego apenas de computadores específicos correspondente tooyour computadores sobre o tráfego de Internet ou toodeny Olá de intervalos de endereços específica, conhecidos.

regras de Olá são avaliadas por ordem, começando com a primeira regra de Olá e terminando regra último Olá. Isto significa que as regras devem ser ordenadas do toomost menos restritivo restritivo. Para obter exemplos e obter mais informações, consulte [o que é uma lista de controlo de acesso de rede](../articles/virtual-network/virtual-networks-acl.md).
