
1. Na vista solução de Olá (ou **Explorador de soluções** no Visual Studio), contexto Olá **componentes** pasta, clique em **obter mais componentes...** , procure Olá **cliente Google Cloud Messaging** componente e adicioná-la toohello projeto.
2. Abra o ficheiro de projeto Olá ToDoActivity.cs e adicione o seguinte Olá utilizar instrução toohello classe:
   
        using Gcm.Client;
3. No Olá **ToDoActivity** classe, adicione Olá novo código a seguir: 
   
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
   
    Isto permite-lhe instância de cliente para dispositivos móveis Olá tooaccess do processo de serviço de processador de push Olá.
4. Adicionar Olá seguinte código toohello **OnCreate** método, após Olá **MobileServiceClient** é criado:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

O **ToDoActivity** está agora preparado para adicionar notificações push.

