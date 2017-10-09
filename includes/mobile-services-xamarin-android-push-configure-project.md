
1. <span data-ttu-id="45640-101">Na vista solução de Olá (ou **Explorador de soluções** no Visual Studio), contexto Olá **componentes** pasta, clique em **obter mais componentes...** , procure Olá **cliente Google Cloud Messaging** componente e adicioná-la toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="45640-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="45640-102">Abra o ficheiro de projeto Olá ToDoActivity.cs e adicione o seguinte Olá utilizar instrução toohello classe:</span><span class="sxs-lookup"><span data-stu-id="45640-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="45640-103">No Olá **ToDoActivity** classe, adicione Olá novo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="45640-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="45640-104">Isto permite-lhe instância de cliente para dispositivos móveis Olá tooaccess do processo de serviço de processador de push Olá.</span><span class="sxs-lookup"><span data-stu-id="45640-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="45640-105">Adicionar Olá seguinte código toohello **OnCreate** método, após Olá **MobileServiceClient** é criado:</span><span class="sxs-lookup"><span data-stu-id="45640-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="45640-106">O **ToDoActivity** está agora preparado para adicionar notificações push.</span><span class="sxs-lookup"><span data-stu-id="45640-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

