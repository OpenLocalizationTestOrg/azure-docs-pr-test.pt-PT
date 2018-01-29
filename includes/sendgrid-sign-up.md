Os clientes do Azure podem desbloquear 25 000 mensagens de e-mail gratuitas por mês. Estas 25 000 mensagens de e-mail mensais gratuitas dar-lhe-ão acesso a relatórios e análise avançados, bem como a [todas as APIs][all APIs] (Web, SMTP, Eventos, Análise, entre outras). Para obter informações sobre os serviços adicionais fornecidos pela SendGrid, visite a página [Soluções SendGrid][SendGrid Solutions].

### <a name="to-sign-up-for-a-sendgrid-account"></a>Para se inscrever numa conta SendGrid
1. Inicie sessão no [portal do Azure][Azure portal].
2. No menu à esquerda, clique em **Novo**.

    ![command-bar-new][command-bar-new]
3. Clique em **Suplementos** e, em seguida, em **SendGrid Email Delivery**.

    ![sendgrid-store][sendgrid-store]
4. Preencha o formulário de inscrição e selecione **Criar**.

    ![sendgrid-create][sendgrid-create]
5. Introduza um **Nome** para identificar o seu serviço SendGrid nas definições do Azure. Os nomes têm de ter entre 1 e 100 carateres e conter apenas carateres alfanuméricos, pontos, travessões e carateres de sublinhado. O nome tem de ser exclusivo na sua lista de Itens de Armazenamento do Azure subscritos.
6. Introduza e confirme a sua **Palavra-passe**.
7. Escolha a sua **Subscrição**.
8. Crie um novo **Grupo de recursos** ou utilize um existente.
9. Na secção **Escalão de preço**, selecione o plano SendGrid no qual pretende inscrever-se.

    ![sendgrid-pricing][sendgrid-pricing]
10. Introduza um **Código de Promoção** se tiver um.
11. Introduza as suas **Informações de Contacto**.
12. Leia e aceite os **Termos legais**.
13. Depois de confirmar a sua compra, verá uma janela de pop-up com a mensagem **Implementação efetuada com êxito** e verá a sua conta listada na secção **Todos os recursos**.

    ![all-resources][all-resources]

    Depois de concluir a compra e clicar no botão **Gerir** para iniciar o processo de verificação de e-mail, receberá uma mensagem de e-mail da SendGrid a pedir que verifique a sua conta. Se não receber esta mensagem ou se surgirem problemas a verificar a sua conta, veja estas FAQ.

    ![manage][manage]

    **Só pode enviar até 100 mensagens de e-mail por dia até ter verificado a sua conta.**

    Para modificar o seu plano de subscrição ou ver as definições de contacto do SendGrid, clique no nome do seu serviço SendGrid para abrir o dashboard do SendGrid Marketplace.

    ![settings][settings]

    Para enviar uma mensagem de e-mail com o SendGrid, tem de indicar a sua Chave de API.

### <a name="to-find-your-sendgrid-api-key"></a>Para localizar a Chave de API do SendGrid
1. Clique em **Gerir**.

    ![manage][manage]
2. No dashboard do SendGrid, selecione **Definições** e **Chaves de API** no menu à esquerda.

    ![api-keys][api-keys]

3. Clique na lista pendente **Criar Chave de API** e selecione **Chave de API Geral**.

    ![general-api-key][general-api-key]
4. No mínimo, forneça o **Nome desta chave** e disponibilize acesso total a **Envio de Correio** e selecione **Guardar**.

    ![access][access]
5. A API será apresentada uma vez nesta altura. Armazene-a de forma segura.

### <a name="to-find-your-sendgrid-credentials"></a>Para localizar as credenciais do SendGrid
1. Clique no ícone de chave para localizar o **Nome de utilizador**.

    ![key][key]
2. A palavra-passe é aquela que escolheu na configuração. Pode selecionar **Alterar palavra-passe** ou **Repor palavra-passe** para fazer alterações.

Para gerir as definições de capacidade de entrega de mensagens de e-mail, clique no **botão Gerir**. Isto irá redirecionar para o dashboard do SendGrid.

    ![manage][manage]

    For more information on sending email through SendGrid, visit the [Email API Overview][Email API Overview].

<!--images-->

[command-bar-new]: ./media/sendgrid-sign-up/new-addon.png
[sendgrid-store]: ./media/sendgrid-sign-up/sendgrid-store.png
[sendgrid-create]: ./media/sendgrid-sign-up/sendgrid-create.png
[sendgrid-pricing]: ./media/sendgrid-sign-up/sendgrid-pricing.png
[all-resources]: ./media/sendgrid-sign-up/all-resources.png
[manage]: ./media/sendgrid-sign-up/manage.png
[settings]: ./media/sendgrid-sign-up/settings.png
[api-keys]: ./media/sendgrid-sign-up/api-keys.png
[general-api-key]: ./media/sendgrid-sign-up/general-api-key.png
[access]: ./media/sendgrid-sign-up/access.png
[key]: ./media/sendgrid-sign-up/key.png

<!--Links-->

[SendGrid Solutions]: https://sendgrid.com/solutions
[Azure portal]: https://portal.azure.com
[SendGrid Getting Started]: http://sendgrid.com/docs
[SendGrid Provisioning Process]: https://support.sendgrid.com/hc/articles/200181628-Why-is-my-account-being-provisioned-
[all APIs]: https://sendgrid.com/docs/API_Reference/index.html
[Email API Overview]: https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html
