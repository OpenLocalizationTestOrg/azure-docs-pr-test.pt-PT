#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate pontos finais públicos no dispositivo de Olá de nuvem

1. Inicie sessão no toohello portal do Azure.
2. Aceda demasiado**máquinas virtuais**e, em seguida, selecione e clique em máquina virtual Olá que está a ser utilizada como a aplicação de nuvem.
    
3. É necessário toocreate rede segurança grupo (NSG) regra toocontrol Olá fluxo de tráfego de e para a máquina virtual. Efetue Olá os seguintes passos toocreate uma regra NSG.
    1. Selecione **Grupo de segurança de rede**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Clique em Olá rede grupo de segurança predefinido que é apresentado.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Selecione **Regras de segurança de entrada**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Clique em **+ adicionar** toocreate uma regra de segurança de entrada.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        No painel de regra de segurança de entrada de adicionar Olá:

        1. Para Olá **nome**, seguinte do tipo Olá nome para o ponto final de Olá: WinRMHttps.
        
        2. Para Olá **prioridade**, selecione um número menor de 1000 (que é a prioridade de Olá para a regra predefinida de Olá). Valor mais alto de Olá, prioridade Olá inferior.

        3. Conjunto Olá **origem** demasiado**qualquer**.

        4. Para Olá **serviço**, selecione **WinRM**. Olá **protocolo** é automaticamente definido demasiado**TCP** e Olá **intervalo de porta** estiver definido demasiado**5986**.

        5. Clique em **OK** regra de Olá toocreate.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. O passo final é tooassociate grupo de segurança de rede com uma sub-rede ou de uma interface de rede específicas. Efetue Olá tooassociate passos a seguir o grupo de segurança de rede com uma sub-rede.
    1. Aceda demasiado**sub-redes**.
    2. Clique em **+ Associar**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Selecione a rede virtual e, em seguida, selecione a sub-rede adequada Olá.
    4. Clique em **OK** regra de Olá toocreate.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Depois de criar a regra de Olá, pode ver o respetivo endereço de IP Virtual público (VIP) do detalhes toodetermine Olá. Registe esse endereço.


