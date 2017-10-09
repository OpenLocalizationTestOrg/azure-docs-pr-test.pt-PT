Depois dos registos para o nome de domínio Olá terem sido propagados, deve ser capaz de toouse tooverify o browser que o nome de domínio personalizado pode ser utilizado tooaccess a sua aplicação web no App Service do Azure.

> [!NOTE]
> Pode demorar algum tempo para a sua toopropagate CNAME através de Olá sistema DNS. Pode utilizar um serviço como <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify Olá CNAME está disponível.
> 
> 

Se não já adicionou a aplicação web como um ponto final do Gestor de tráfego, deve fazê-antes de resolução de nomes funcione, como Olá domínio personalizado nome rotas tooTraffic Manager. Gestor de tráfego, em seguida, encaminha tooyour web app. Utilize as informações de Olá no [adicionar ou eliminar pontos finais](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd a aplicação web como um ponto final no perfil do Traffic Manager.

> [!NOTE]
> Se a sua aplicação web não estiver listada, ao adicionar um ponto final, certifique-se de que está configurado para **padrão** modo de plano de serviço de aplicações. Tem de utilizar **padrão** modo para a sua aplicação web no toowork de ordem com o Gestor de tráfego.
> 
> 

1. No seu browser, abra Olá [Portal do Azure](https://portal.azure.com).
2. No Olá **Web Apps** separador, clique no nome de Olá da sua aplicação web, selecione **definições**e, em seguida, selecione **domínios personalizados**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. No Olá **domínios personalizados** painel, clique em **adicionar hostname**.
4. Olá utilize **Hostname** texto caixas tooenter Olá Gestor de tráfego domínio nome tooassociate com esta aplicação web.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Clique em **validar** toosave a configuração de nome de domínio Olá.
6. Após clicar em **validar** Azure irá iniciar fluxo de trabalho de verificação de domínio. Isto irá verificar para a propriedade do domínio, bem como de êxito de disponibilidade e o relatório de nome de anfitrião ou de erro detalhadas com guidence prescritiva sobre como toofix Olá erro.    
7. Após a validação bem-sucedida **adicionar hostname** botão deixará de Active Directory e será capaz de toohello atribuir nome do anfitrião. Navegue agora o nome de domínio personalizado de tooyour num browser. Deverá ver a execução de aplicação utilizando o seu nome de domínio personalizado. 
   
   Depois de concluída a configuração, o nome de domínio personalizado de Olá será listado no Olá **nomes de domínio** secção da sua aplicação web.

Neste momento, deve ser o nome do nome de domínio do Traffic Manager do tooenter capaz de Olá no seu browser e veja que com êxito demora a aplicação web de tooyour.

