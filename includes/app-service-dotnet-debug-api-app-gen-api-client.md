## <a name="generate-an-api-app-client"></a><span data-ttu-id="cc36b-101">Generate an API app client</span><span class="sxs-lookup"><span data-stu-id="cc36b-101">Generate an API app client</span></span>
<span data-ttu-id="cc36b-102">The API App tools in Visual Studio make it easy to generate C# code that calls to your Azure API Apps from desktop, store, and mobile apps.</span><span class="sxs-lookup"><span data-stu-id="cc36b-102">The API App tools in Visual Studio make it easy to generate C# code that calls to your Azure API Apps from desktop, store, and mobile apps.</span></span> 

1. <span data-ttu-id="cc36b-103">In Visual Studio, open the solution that contains the API app from the [Create API app](../articles/app-service-api/app-service-dotnet-create-api-app.md) topic.</span><span class="sxs-lookup"><span data-stu-id="cc36b-103">In Visual Studio, open the solution that contains the API app from the [Create API app](../articles/app-service-api/app-service-dotnet-create-api-app.md) topic.</span></span> 
2. <span data-ttu-id="cc36b-104">From **Solution Explorer**, right-click the solution and select the **Add** > **New Project**.</span><span class="sxs-lookup"><span data-stu-id="cc36b-104">From **Solution Explorer**, right-click the solution and select the **Add** > **New Project**.</span></span>
   
    ![Add a new project](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/01-add-new-project-v3.png)
3. <span data-ttu-id="cc36b-106">In the **Add New Project** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc36b-106">In the **Add New Project** dialog, perform the following steps:</span></span>
   
   1. <span data-ttu-id="cc36b-107">Select the **Windows Desktop** category.</span><span class="sxs-lookup"><span data-stu-id="cc36b-107">Select the **Windows Desktop** category.</span></span>
   2. <span data-ttu-id="cc36b-108">Select the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="cc36b-108">Select the **Console Application** project template.</span></span>
   3. <span data-ttu-id="cc36b-109">Name the project.</span><span class="sxs-lookup"><span data-stu-id="cc36b-109">Name the project.</span></span>
   4. <span data-ttu-id="cc36b-110">Click **OK** to generate the new project in your existing solution.</span><span class="sxs-lookup"><span data-stu-id="cc36b-110">Click **OK** to generate the new project in your existing solution.</span></span>
      
      ![Add a new project](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/02-contact-list-console-project-v3.png)
4. <span data-ttu-id="cc36b-112">Right-click the newly created console application project and select **Add** > **Azure API App Client**.</span><span class="sxs-lookup"><span data-stu-id="cc36b-112">Right-click the newly created console application project and select **Add** > **Azure API App Client**.</span></span> 
   
    ![Add a new Client](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/03-add-azure-api-client-v3.png)
5. <span data-ttu-id="cc36b-114">In the **Add Microsoft Azure API App Client** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc36b-114">In the **Add Microsoft Azure API App Client** dialog, perform the following steps:</span></span> 
   
   1. <span data-ttu-id="cc36b-115">Select the **Download** option.</span><span class="sxs-lookup"><span data-stu-id="cc36b-115">Select the **Download** option.</span></span> 
   2. <span data-ttu-id="cc36b-116">From the drop-down list, select the API app that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cc36b-116">From the drop-down list, select the API app that you created earlier.</span></span> 
   3. <span data-ttu-id="cc36b-117">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc36b-117">Click **OK**.</span></span> 
      
      ![Generation Screen](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/04-select-the-api-v3.png)
      
      <span data-ttu-id="cc36b-119">The wizard will download the API metadata file and generate a typed interface for invoking the API App.</span><span class="sxs-lookup"><span data-stu-id="cc36b-119">The wizard will download the API metadata file and generate a typed interface for invoking the API App.</span></span>
      
      ![Generation Happening](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/05-metadata-downloading-v3.png)
      
      <span data-ttu-id="cc36b-121">Once code generation is complete, you'll see a new folder in Solution Explorer, with the name of the API app.</span><span class="sxs-lookup"><span data-stu-id="cc36b-121">Once code generation is complete, you'll see a new folder in Solution Explorer, with the name of the API app.</span></span> <span data-ttu-id="cc36b-122">This folder contains the code that implements the client and data models.</span><span class="sxs-lookup"><span data-stu-id="cc36b-122">This folder contains the code that implements the client and data models.</span></span> 
      
      ![Generation Complete](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/06-code-gen-output-v3.png)
6. <span data-ttu-id="cc36b-124">Open the **Program.cs** file from the project root and replace the **Main** method with the following code:</span><span class="sxs-lookup"><span data-stu-id="cc36b-124">Open the **Program.cs** file from the project root and replace the **Main** method with the following code:</span></span> 
   
        static void Main(string[] args)
        {
            var client = new ContactsList();
   
            // Send GET request.
            var contacts = client.Contacts.Get();
            foreach (var c in contacts)
            {
                Console.WriteLine("{0}: {1} {2}",
                    c.Id, c.Name, c.EmailAddress);
            }
   
            // Send POST request.
            client.Contacts.Post(new Models.Contact
            {
                EmailAddress = "lkahn@contoso.com",
                Name = "Loretta Kahn",
                Id = 4
            });
   
            Console.WriteLine("Finished");
            Console.ReadLine();
        }

## <a name="test-the-api-app-client"></a><span data-ttu-id="cc36b-125">Test the API app client</span><span class="sxs-lookup"><span data-stu-id="cc36b-125">Test the API app client</span></span>
<span data-ttu-id="cc36b-126">Once the API app has been coded, it's time to test the code.</span><span class="sxs-lookup"><span data-stu-id="cc36b-126">Once the API app has been coded, it's time to test the code.</span></span>

1. <span data-ttu-id="cc36b-127">Open **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cc36b-127">Open **Solution Explorer**.</span></span>
2. <span data-ttu-id="cc36b-128">Right-click the console application you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="cc36b-128">Right-click the console application you created in the previous section.</span></span>
3. <span data-ttu-id="cc36b-129">From the console application's context menu, select **Debug > Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="cc36b-129">From the console application's context menu, select **Debug > Start new instance**.</span></span> 
4. <span data-ttu-id="cc36b-130">A console windows should open and display all of the contacts.</span><span class="sxs-lookup"><span data-stu-id="cc36b-130">A console windows should open and display all of the contacts.</span></span> 
   
    ![Running console app](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-dotnet-debug-api-app-gen-api-client/running-console-app.png)
5. <span data-ttu-id="cc36b-132">Press **Enter** to dismiss the console window.</span><span class="sxs-lookup"><span data-stu-id="cc36b-132">Press **Enter** to dismiss the console window.</span></span>          








