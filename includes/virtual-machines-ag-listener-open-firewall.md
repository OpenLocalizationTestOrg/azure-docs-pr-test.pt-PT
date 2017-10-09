Neste passo, vai criar uma regra tooopen Olá sonda porta de firewall de Olá com balanceamento de carga do ponto final (59999, conforme especificado anteriormente) e outra regra de porta de serviço de escuta do grupo de disponibilidade do tooopen Olá. Uma vez que criou o ponto final com balanceamento de carga de Olá no Olá VMs que contêm as réplicas do grupo de disponibilidade, precisará de porta da sonda tooopen Olá e porta de serviço de escuta de Olá no Olá respetivas VMs.

1. Em VMs que alojam as réplicas, iniciar **Firewall do Windows com segurança avançada**.

2. Clique com botão direito **regras de entrada**e, em seguida, clique em **nova regra**.

3. No Olá **tipo de regra** página, selecione **porta**e, em seguida, clique em **seguinte**.

4. No Olá **protocolo e portas** página, selecione **TCP**, tipo **59999** no Olá **portas locais específicas** caixa e, em seguida, clique em **Seguinte**.

5. No Olá **ação** página, mantenha **permitir ligação Olá** selecionada e, em seguida, clique em **seguinte**.

6. No Olá **perfil** página, aceite as predefinições de Olá e, em seguida, clique em **seguinte**.

7. No Olá **nome** página, numa Olá **nome** texto caixa, especifique um nome de regra, tal como **sempre no serviço de escuta de sonda de porta**e, em seguida, clique em **concluir**.

8. Repita Olá precedente passos para a porta do serviço de escuta de grupo de disponibilidade do Olá (tal como especificado anteriormente no parâmetro de Olá $EndpointPort do script Olá) e, em seguida, especifique um nome de regra adequada, tais como **sempre no serviço de escuta de porta**.

