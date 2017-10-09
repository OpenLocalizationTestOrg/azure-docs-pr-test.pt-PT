<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Resolução de problemas de falhas na atualização
**E se vir uma notificação que Olá verificações de pré-atualização falhou?**

Se uma pré-verificação de falhar, certifique-se de que tem consultou barra de notificação detalhada Olá na Olá parte inferior da página Olá. Isto fornece orientações sobre como a pré-verificação de toowhich falhou. Olá ilustração seguinte mostra uma instância em que é apresentada essa uma notificação. Neste caso, verificação de estado de funcionamento do controlador de Olá e verificação de estado de funcionamento do componente de hardware falharam. Em Olá **estado do Hardware** secção, pode ver que ambos **controlador 0** e **controlador 1** componentes necessitem de atenção.

  ![Falha de pré-verificação](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Terá de toomake se de que tanto os controladores de bom estado de funcionamento e online. Também terá de certificar-se de que todos os componentes de hardware de Olá no dispositivo do StorSimple Olá são apresentados toobe bom estado de funcionamento na página de manutenção de Olá toomake. Em seguida, pode tentar tooinstall atualizações. Se não tiver problemas de componente de hardware do toofix capaz de Olá, em seguida, terá de toocontact Support da Microsoft para os passos seguintes.

**E se receber uma mensagem de erro "Não foi possível instalar atualizações" e Olá recomendação é toorefer toohello atualização guia toodetermine Olá causa da falha de Olá de resolução de problemas?**

Uma causa provável para este pode ser que não têm servidores do Microsoft Update de toohello de conectividade. Trata-se de uma verificação manual que necessita de toobe efetuada. Se perder o servidor de atualização de toohello de conectividade, provocaria a falha de tarefa de atualização. Pode verificar a conectividade de Olá executando o seguinte cmdlet a partir da interface do Windows PowerShell Olá do dispositivo StorSimple de Olá:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Execute o cmdlet Olá em ambos os controladores.

Se tiver verificado existe conectividade de Olá e continuar toosee este problema, contacte a Microsoft Support para passos seguintes.

**E se vir uma falha de atualização ao atualizar a sua tooUpdate dispositivo 4 e tanto os controladores de Olá estão em execução de atualização 4?**

Iniciar atualização 4, se os dois controladores de Olá estão em execução Olá a mesma versão do software e se existe uma falha de atualização, os controladores de Olá não entrar em modo de recuperação. Esta situação pode surgir se hello correção de software do dispositivo (atualização 1 de ordem) é aplicado tooboth Olá controladores com êxito, mas outras correções (ordem 2nd e Ordem 3rd) são ainda toobe aplicada. A iniciar a atualização 4, os controladores de Olá entrarão num modo de recuperação apenas se os dois controladores de Olá estejam a executar versões de software diferentes. 

Se o utilizador Olá vê uma falha de atualização quando ambos os controladores estão em execução de atualização 4, recomendamos que aguarde alguns minutos e, em seguida, repetir a actualização. Se tentativas Olá não for bem-sucedida, em seguida, deve contactar o Support da Microsoft.
