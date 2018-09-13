
1. <span data-ttu-id="a1c1c-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span><span class="sxs-lookup"><span data-stu-id="a1c1c-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="a1c1c-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span><span class="sxs-lookup"><span data-stu-id="a1c1c-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="a1c1c-103">In the **ToDoActivity** class, add the following new code:</span><span class="sxs-lookup"><span data-stu-id="a1c1c-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="a1c1c-104">This enables you to access the mobile client instance from the push handler service process.</span><span class="sxs-lookup"><span data-stu-id="a1c1c-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="a1c1c-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span><span class="sxs-lookup"><span data-stu-id="a1c1c-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
     <span data-ttu-id="a1c1c-106">// Set the current instance of TodoActivity.</span><span class="sxs-lookup"><span data-stu-id="a1c1c-106">// Set the current instance of TodoActivity.</span></span>
     <span data-ttu-id="a1c1c-107">instance = this;</span><span class="sxs-lookup"><span data-stu-id="a1c1c-107">instance = this;</span></span>
   
     <span data-ttu-id="a1c1c-108">// Make sure the GCM client is set up correctly.</span><span class="sxs-lookup"><span data-stu-id="a1c1c-108">// Make sure the GCM client is set up correctly.</span></span>
     <span data-ttu-id="a1c1c-109">GcmClient.CheckDevice(this); GcmClient.CheckManifest(this);</span><span class="sxs-lookup"><span data-stu-id="a1c1c-109">GcmClient.CheckDevice(this); GcmClient.CheckManifest(this);</span></span>
   
     <span data-ttu-id="a1c1c-110">// Register the app for push notifications.</span><span class="sxs-lookup"><span data-stu-id="a1c1c-110">// Register the app for push notifications.</span></span>
     <span data-ttu-id="a1c1c-111">GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);</span><span class="sxs-lookup"><span data-stu-id="a1c1c-111">GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);</span></span>

<span data-ttu-id="a1c1c-112">Your **ToDoActivity** is now prepared for adding push notifications.</span><span class="sxs-lookup"><span data-stu-id="a1c1c-112">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

