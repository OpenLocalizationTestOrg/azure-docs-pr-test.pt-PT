> [!IMPORTANT]
> <span data-ttu-id="49cf1-101">tooreceive notificações Push do Mobile Engagement, terá de tooenable `Silent Remote Notifications` na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="49cf1-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="49cf1-102">Terá de matriz do tooadd Olá valor da notificação remota toohello UIBackgroundModes no ficheiro info. plist.</span><span class="sxs-lookup"><span data-stu-id="49cf1-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="49cf1-103">Abra `info.plist` ficheiros no projeto Olá</span><span class="sxs-lookup"><span data-stu-id="49cf1-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="49cf1-104">Clique no item superior do Olá na lista de Olá (`Information Property List`) e adicione uma nova linha</span><span class="sxs-lookup"><span data-stu-id="49cf1-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="49cf1-105">Olá nova linha introduza`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="49cf1-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="49cf1-106">Clique na linha de Olá Olá seta para a esquerda tooexpand</span><span class="sxs-lookup"><span data-stu-id="49cf1-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="49cf1-107">Adicionar Olá seguinte item de toohello valor 0`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="49cf1-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="49cf1-108">Depois de efetuar Olá alterar, ficheiro info. plist Olá XML deve conter Olá seguinte chave e valor:</span><span class="sxs-lookup"><span data-stu-id="49cf1-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="49cf1-109">Se estiver a utilizar o **Xcode 7+** e o **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="49cf1-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="49cf1-110">Ative **Notificações Push** em Destinos > Nome do Destino > Capacidades.</span><span class="sxs-lookup"><span data-stu-id="49cf1-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

