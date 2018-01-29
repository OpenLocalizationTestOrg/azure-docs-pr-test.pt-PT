<!--author=alkohli last changed: 08/29/17-->

## <a name="troubleshooting-update-failures"></a>Resolução de problemas de falhas na atualização
**E se vir uma notificação informando-me de que as verificações de pré-atualização falharam?**

Se uma pré-verificação falhar, certifique-se de que viu a barra de notificação detalhada na parte inferior da página. Isto fornece orientações relativamente a qual pré-verificação falhou. Por exemplo, receberá uma notificação que falharam a verificação de estado de funcionamento do controlador e verificação de estado de funcionamento do componente de hardware. Aceda a **monitorização > Estado de funcionamento do Hardware**. Tem de certificar-se de que tanto os controladores são bom estado de funcionamento e online. Terá também de certificar-se de que todos os componentes de hardware no dispositivo StorSimple são apresentados para estar em bom estado de funcionamento neste painel. Pode então tentar instalar atualizações. Se não conseguir corrigir os problemas dos componentes de hardware, terá de contactar o Suporte da Microsoft para obter os passos a seguir.

**E se receber uma mensagem de erro “Não foi possível instalar as atualizações” e a recomendação for consultar o guia de resolução de problemas para determinar a causa da falha?**

Uma das causas prováveis poderia ser não ter conectividade aos servidores do Microsoft Update. Esta é uma verificação manual que tem de ser efetuada. Se perder a conectividade ao servidor de atualização, a tarefa de atualização falha. Pode verificar a conectividade ao executar o seguinte cmdlet a partir da interface do Windows PowerShell do seu dispositivo StorSimple:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Execute o cmdlet nos dois controladores.

Se verificar que há conectividade e continuar a ver este problema, contacte o Suporte da Microsoft para obter os passos a seguir.

**E se vir uma falha de atualização ao atualizar o seu dispositivo para a Atualização 4 e os dois controladores estiverem a executar a Atualização 4?**

Ao iniciarem a Atualização 4, se os dois controladores estiverem a executar a mesma versão de software e se existir uma falha de atualização, os controladores não entram em modo de recuperação. Esta situação pode surgir se a correção de software do dispositivo (atualização de 1.ª ordem) for aplicada aos dois controladores com êxito, mas se outras correções (de 2.ª e 3.ª ordem) ainda não tiverem sido aplicadas. Ao iniciarem a Atualização 4, os controladores só entram em modo de recuperação se os dois controladores estiverem a executar versões de software diferentes. 

Se o utilizador vir uma falha de atualização quando os dois controladores estiverem a executar a Atualização 4, recomendamos que aguarde alguns minutos e tente novamente a atualização. Se a tentativa não for bem sucedida, deverá contactar o Suporte da Microsoft.
