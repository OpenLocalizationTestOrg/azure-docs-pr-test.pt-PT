---
title: aaaHow toouse Blob Storage do Xamarin | Microsoft Docs
description: "Olá biblioteca de clientes do Storage do Azure para Xamarin permite aos programadores toocreate iOS, Android e Windows aplicações da loja com as suas interfaces de utilizador nativo. Este tutorial mostra como toouse Xamarin toocreate uma aplicação que utiliza o Blob storage do Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="cf2c9-104">Como toouse Blob Storage do Xamarin</span><span class="sxs-lookup"><span data-stu-id="cf2c9-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="cf2c9-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="cf2c9-105">Overview</span></span>
<span data-ttu-id="cf2c9-106">Xamarin permite aos programadores toouse um partilhado c# código base toocreate iOS, Android e Windows aplicações da loja com as suas interfaces de utilizador nativo.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="cf2c9-107">Este tutorial mostra como toouse Blob storage do Azure com uma aplicação Xamarin.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="cf2c9-108">Se quiser toolearn mais sobre o Storage do Azure, antes de explorar o código de Olá, consulte o artigo [introdução tooMicrosoft Storage do Azure](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cf2c9-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="cf2c9-109">Criar uma nova aplicação Xamarin</span><span class="sxs-lookup"><span data-stu-id="cf2c9-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="cf2c9-110">Para este tutorial, iremos irá criar uma aplicação que tenha como destino Android, iOS e Windows.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="cf2c9-111">Esta aplicação será simplesmente criar um contentor e carregar um blob para este contentor.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="cf2c9-112">Iremos utilizar Visual Studio no Windows, mas Olá learnings mesmos podem ser aplicadas ao criar uma aplicação utilizando o Xamarin Studio no macOS.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="cf2c9-113">Siga estes passos toocreate a aplicação:</span><span class="sxs-lookup"><span data-stu-id="cf2c9-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="cf2c9-114">Se ainda não o fez, transfira e instale [Xamarin para Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="cf2c9-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="cf2c9-115">Abra o Visual Studio e crie uma aplicação em branco (nativo portáteis): **ficheiro > novo > projeto > plataforma > App(Native Portable) em branco**.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="cf2c9-116">A solução no painel do Explorador de soluções de Olá com o botão direito e selecione **gerir pacotes NuGet para solução**.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="cf2c9-117">Procurar **Windowsazure** e instalar projetos do Olá mais recentes versão estável tooall na sua solução.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="cf2c9-118">Compilar e executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-118">Build and run your project.</span></span>

<span data-ttu-id="cf2c9-119">Agora, deve ter uma aplicação que lhe permite tooclick um botão que incrementa um contador.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="cf2c9-120">Criar o contentor e carregar blob</span><span class="sxs-lookup"><span data-stu-id="cf2c9-120">Create container and upload blob</span></span>
<span data-ttu-id="cf2c9-121">Em seguida, em seu `(Portable)` projeto, irá adicionar algum código demasiado`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="cf2c9-122">Este código cria um contentor e carrega um blob para este contentor.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="cf2c9-123">`MyClass.cs`deve ter o seguinte aspeto Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="cf2c9-123">`MyClass.cs` should look like hello following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="cf2c9-124">Certifique-se de que tooreplace "your_account_name_here" e "your_account_key_here" com o nome da conta real e a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="cf2c9-125">O iOS, Android e Windows Phone todos os projetos tem referências tooyour portátil projeto - que significa que pode escrever todos os do seu código partilhado num coloque e utilização-lo em todos os seus projetos.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="cf2c9-126">Agora pode adicionar Olá de linha de partido de colocar de toostart tooeach projeto de código a seguir:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="cf2c9-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="cf2c9-127">XamarinApp.Droid > mainactivity. CS</span><span class="sxs-lookup"><span data-stu-id="cf2c9-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="cf2c9-128">XamarinApp.iOS > viewcontroller. CS</span><span class="sxs-lookup"><span data-stu-id="cf2c9-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="cf2c9-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="cf2c9-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="cf2c9-130">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="cf2c9-130">Run hello application</span></span>
<span data-ttu-id="cf2c9-131">Pode agora executar esta aplicação no emulador do Android ou Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="cf2c9-132">Também pode executar esta aplicação no emulador do iOS, mas esta opção requer um MAC.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="cf2c9-133">Para obter instruções específicas sobre como toodo, leia a documentação de Olá para [ligar o Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="cf2c9-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="cf2c9-134">Depois de executar a aplicação, vai criar o contentor de Olá `mycontainer` na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="cf2c9-135">Deve conter blob Olá, `myblob`, que tem texto Olá, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="cf2c9-136">Pode verificar isto utilizando Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="cf2c9-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf2c9-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cf2c9-137">Next steps</span></span>
<span data-ttu-id="cf2c9-138">Neste tutorial, aprendeu como toocreate uma aplicação de plataformas cruzadas Xamarin que utiliza o armazenamento do Azure, especificamente concentrar-se num cenário no Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="cf2c9-139">No entanto, pode fazer muito mais com armazenamento de BLOBs não só, mas também com a tabela, ficheiros e armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="cf2c9-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="cf2c9-140">Consulte Olá artigos toolearn mais os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cf2c9-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="cf2c9-141">Introdução ao armazenamento de Blobs do Azure através do .NET</span><span class="sxs-lookup"><span data-stu-id="cf2c9-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="cf2c9-142">Introdução ao armazenamento de Tabelas do Azure através do .NET</span><span class="sxs-lookup"><span data-stu-id="cf2c9-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="cf2c9-143">Introdução ao Armazenamento de filas do Azure através do .NET</span><span class="sxs-lookup"><span data-stu-id="cf2c9-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="cf2c9-144">Introdução ao Armazenamento de Ficheiros do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="cf2c9-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

