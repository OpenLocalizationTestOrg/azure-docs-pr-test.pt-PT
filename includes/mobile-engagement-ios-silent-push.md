> [!IMPORTANT]
> tooreceive notificações Push do Mobile Engagement, terá de tooenable `Silent Remote Notifications` na sua aplicação. Terá de matriz do tooadd Olá valor da notificação remota toohello UIBackgroundModes no ficheiro info. plist.
> 
> 

1. Abra `info.plist` ficheiros no projeto Olá
2. Clique no item superior do Olá na lista de Olá (`Information Property List`) e adicione uma nova linha
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Olá nova linha introduza`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Clique na linha de Olá Olá seta para a esquerda tooexpand
5. Adicionar Olá seguinte item de toohello valor 0`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Depois de efetuar Olá alterar, ficheiro info. plist Olá XML deve conter Olá seguinte chave e valor:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Se estiver a utilizar o **Xcode 7+** e o **iOS 9+**:
   
   * Ative **Notificações Push** em Destinos > Nome do Destino > Capacidades.

