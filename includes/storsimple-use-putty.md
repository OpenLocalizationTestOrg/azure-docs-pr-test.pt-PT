<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect através da consola de série de Olá
1. Ligar o seu dispositivo de toohello cabo série (diretamente ou através de um adaptador USB de série).
2. Abra Olá **painel de controlo**e, em seguida, abra Olá **Gestor de dispositivos**.
3. Identifique portas Olá COM conforme mostrado na seguinte ilustração de Olá.
   
     ![Ligar através da consola de série](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Inicie o PuTTY. 
5. No painel direito Olá, alterar Olá **tipo de ligação** demasiado**série**.
6. No painel direito Olá, escreva a porta COM correta do Olá. Certifique-se de que os parâmetros de configuração de série de Olá estão definidos da seguinte forma:
   
   * Velocidade: 115.200
   * Bits de dados: 8
   * Bits de paragem: 1
   * Paridade: Nenhuma
   * Fluxo de controlo: Nenhum
     
     Estas definições são apresentadas na Olá seguinte ilustração.
     
     ![Definições do PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Se Olá controlo de fluxo predefinido não funcionar, experimente defini Olá fluxo controlo tooXON/XOFF de entrada.
     > 
     > 
7. Clique em **abra** toostart uma sessão de série.

