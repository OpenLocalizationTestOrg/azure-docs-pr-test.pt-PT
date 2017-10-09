---
title: "aplicação plataforma Universal do Windows (UWP) do aaaAdd authentication tooyour | Microsoft Docs"
description: "Saiba como os utilizadores de tooauthenticate de Mobile Apps do Azure App Service toouse da sua aplicação plataforma Universal do Windows (UWP) utilizando uma variedade de fornecedores de identidade, incluindo: AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Adicionar autenticação tooyour Windows aplicação
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tópico mostra como tooadd tooyour de autenticação baseada em nuvem aplicação móvel. Neste tutorial, é possível adicionar projeto de início rápido da plataforma Universal do Windows (UWP) de toohello de autenticação para Mobile Apps utilizando um fornecedor de identidade que é suportado pelo App Service do Azure. Após com êxito a ser autenticado e autorizado pelo seu back-end de aplicação móvel, é apresentado o valor de ID de utilizador Olá.

Este tutorial é baseado no início rápido de aplicações móveis Olá. Tem de concluir primeiro tutorial Olá [introdução às Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Registar a aplicação para autenticação e configurar Olá do serviço de aplicações
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Adicionar os URLs de redirecionamento de externo permitido de toohello de aplicação

Autenticação segura requer que defina um novo esquema de URL para a sua aplicação. Isto permite Olá autenticação sistema tooredirect back tooyour aplicação após a conclusão do processo de autenticação de Olá. Neste tutorial, utilizamos o esquema de URL Olá _appname_ ao longo. No entanto, pode utilizar qualquer esquema de URL que escolher. Deve ser exclusivo tooyour aplicações móveis. redirecionamento de Olá tooenable no lado do servidor de Olá:

1. No [portal do Azure] Olá, selecione o serviço de aplicações.

2. Clique em Olá **autenticação / autorização** opção do menu.

3. No Olá **permitidos URLs de redirecionamento externos**, introduza `url_scheme_of_your_app://easyauth.callback`.  Olá **url_scheme_of_your_app** esta cadeia é Olá esquema de URL para a sua aplicação móvel.  Deve seguir a especificação de URL normal para um protocolo (utilize letras e números apenas e começar com uma letra).  Deve efetuar uma nota da cadeia de Olá que escolher pois terá tooadjust código da aplicação móvel com Olá esquema de URL em vários locais.

4. Clique em **OK**.

5. Clique em **Guardar**.

## <a name="permissions"></a>Restringir os utilizadores tooauthenticated de permissões
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Agora, pode verificar que back-end do acesso anónimo tooyour foi desativada. Com Olá projeto de aplicação UWP definir como projeto de arranque Olá, implementar e executar a aplicação de Olá; Certifique-se de que uma exceção não processada com um código de estado de 401 (não autorizado) é desencadeada depois de Olá aplicação for iniciada. Isto acontece porque a aplicação Olá tenta tooaccess o código de aplicação móvel como um utilizador não autorizado, mas Olá *TodoItem* tabela agora requer autenticação.

Em seguida, irá atualizar utilizadores de tooauthenticate Olá aplicações antes de solicitar recursos a partir do seu serviço de aplicações.

## <a name="add-authentication"></a>Adicionar autenticação toohello aplicação
1. No projeto de aplicação UWP Olá ficheiro MainPage.xaml.cs e adicionar Olá seguinte fragmento de código:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Este código autentica o utilizador de Olá com um início de sessão do Facebook. Se estiver a utilizar um fornecedor de identidade que não seja o Facebook, altere o valor de Olá de **MobileServiceAuthenticationProvider** acima toohello valor para o seu fornecedor.
2. Substitua Olá **OnNavigatedTo()** método no MainPage.xaml.cs. Em seguida, irá adicionar um **sessão** botão toohello aplicação que aciona a autenticação.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Adicione Olá seguinte fragmento de código toohello MainPage.xaml.cs:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Abra o ficheiro de projeto MainPage.xaml Olá, localizar o elemento de Olá que define Olá **guardar** botão e substitua-o por Olá seguinte código:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Adicione Olá seguinte fragmento de código toohello App.xaml.cs:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Abra o ficheiro Package. appxmanifest, navegue demasiado**declarações**, na **declarações disponíveis** na lista pendente, selecione **protocolo** e clique em **adicionar** botão. Configurar agora Olá **propriedades** de Olá **protocolo** declaração. No **nome a apresentar**, adicionar nome Olá desejar toodisplay toousers da sua aplicação. No **nome**, adicione o {url_scheme_of_your_app}.
7. Prima Olá F5 toorun chave Olá aplicação, clique em Olá **sessão** botão e inicie sessão na aplicação Olá com o seu fornecedor de identidade que escolheu. Após o início de sessão, aplicação Olá é executado sem erros e são tooquery capaz de back-end e tornar toodata de atualizações.

## <a name="tokens"></a>Armazenar o token de autenticação de Olá no cliente Olá
Exemplo Olá de anterior mostrou um padrão início de sessão, que necessita de Olá cliente toocontact ambos os fornecedor de identidade Olá e hello do serviço de aplicações, sempre que essa aplicação Olá é iniciado. Não só é ineficaz, pode executar este método para utilização-relacionado com problemas de muitos clientes tente toostart aplicação em Olá mesmo tempo. Uma abordagem de melhor é o token de autorização de Olá toocache devolvido pelo seu serviço de aplicações e tente toouse este primeiro antes de utilizar um fornecedor com base no início de sessão.

> [!NOTE]
> Pode colocar em cache o token de Olá emitido por serviços aplicacionais independentemente se estão a utilizar autenticação geridos pelo cliente ou serviço gerido. Este tutorial utiliza a autenticação de serviço gerido.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Passos seguintes
Agora que concluiu este tutorial de autenticação básica, considere continuar em tooone de Olá seguintes tutoriais:

* [Adicionar a aplicação de tooyour de notificações push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Saiba como notificações de push tooadd suportam tooyour aplicação e configurar a sua aplicação móvel back-end toouse Notification Hubs do Azure toosend as notificações push.
* [Permitir sincronização offline para a sua aplicação](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Saiba como tooadd offline suportam a sua aplicação utilizando um back-end de aplicação móvel. Sincronização offline permite que os utilizadores finais toointeract com uma aplicação móvel&mdash;visualizar, adicionar ou modificar dados&mdash;, mesmo quando não existe nenhuma ligação de rede.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
