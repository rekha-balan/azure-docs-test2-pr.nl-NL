<span data-ttu-id="bf444-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bf444-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf444-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="bf444-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="bf444-103">Security features should be enabled before deploying MongoDB to a production environment.</span><span class="sxs-lookup"><span data-stu-id="bf444-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="bf444-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="bf444-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="bf444-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bf444-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="bf444-106">Select the **Tools** button in the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="bf444-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="bf444-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span><span class="sxs-lookup"><span data-stu-id="bf444-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="bf444-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span><span class="sxs-lookup"><span data-stu-id="bf444-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="bf444-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="bf444-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="bf444-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span><span class="sxs-lookup"><span data-stu-id="bf444-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="bf444-111">Download, then run the MSI installer.</span><span class="sxs-lookup"><span data-stu-id="bf444-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="bf444-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bf444-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="bf444-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span><span class="sxs-lookup"><span data-stu-id="bf444-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="bf444-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span><span class="sxs-lookup"><span data-stu-id="bf444-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="bf444-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="bf444-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="bf444-116">From **Start**, select **Command Prompt** to open a command prompt window.</span><span class="sxs-lookup"><span data-stu-id="bf444-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="bf444-117">Type:</span><span class="sxs-lookup"><span data-stu-id="bf444-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="bf444-118">To run the database, run:</span><span class="sxs-lookup"><span data-stu-id="bf444-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="bf444-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span><span class="sxs-lookup"><span data-stu-id="bf444-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="bf444-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span><span class="sxs-lookup"><span data-stu-id="bf444-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="bf444-121">The command prompt stays focused on this task while your MongoDB instance is running.</span><span class="sxs-lookup"><span data-stu-id="bf444-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="bf444-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span><span class="sxs-lookup"><span data-stu-id="bf444-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="bf444-123">The database is created by the insert.</span><span class="sxs-lookup"><span data-stu-id="bf444-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="bf444-124">Alternatively, you can install mongod.exe as a service:</span><span class="sxs-lookup"><span data-stu-id="bf444-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="bf444-125">A service is installed named MongoDB with a description of "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="bf444-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="bf444-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span><span class="sxs-lookup"><span data-stu-id="bf444-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="bf444-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span><span class="sxs-lookup"><span data-stu-id="bf444-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="bf444-128">The `--dbpath` option specifies the location of the data directory.</span><span class="sxs-lookup"><span data-stu-id="bf444-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="bf444-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="bf444-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="bf444-130">To start the service, run this command:</span><span class="sxs-lookup"><span data-stu-id="bf444-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="bf444-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bf444-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="bf444-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span><span class="sxs-lookup"><span data-stu-id="bf444-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="bf444-133">a) In the left pane, select **Inbound Rules**.</span><span class="sxs-lookup"><span data-stu-id="bf444-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="bf444-134">In the **Actions** pane on the right, select **New Rule...**.</span><span class="sxs-lookup"><span data-stu-id="bf444-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Windows Firewall][Image1]

    <span data-ttu-id="bf444-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf444-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows Firewall][Image2]

    <span data-ttu-id="bf444-138">c) Select **TCP** and then **Specific local ports**.</span><span class="sxs-lookup"><span data-stu-id="bf444-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="bf444-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf444-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows Firewall][Image3]

    <span data-ttu-id="bf444-141">d) Select **Allow the connection** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf444-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Windows Firewall][Image4]

    <span data-ttu-id="bf444-143">e) Click **Next** again.</span><span class="sxs-lookup"><span data-stu-id="bf444-143">e) Click **Next** again.</span></span>

    ![Windows Firewall][Image5]

    <span data-ttu-id="bf444-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bf444-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows Firewall][Image6]

12. <span data-ttu-id="bf444-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span><span class="sxs-lookup"><span data-stu-id="bf444-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="bf444-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span><span class="sxs-lookup"><span data-stu-id="bf444-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="bf444-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="bf444-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Endpoints][Image7]

13. <span data-ttu-id="bf444-151">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="bf444-151">Click **Add**.</span></span>

14. <span data-ttu-id="bf444-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span><span class="sxs-lookup"><span data-stu-id="bf444-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="bf444-153">Opening this port allows MongoDB to be accessed remotely.</span><span class="sxs-lookup"><span data-stu-id="bf444-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![Endpoints][Image9]

> [!NOTE]
> <span data-ttu-id="bf444-155">The port 27017 is the default port used by MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bf444-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="bf444-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span><span class="sxs-lookup"><span data-stu-id="bf444-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="bf444-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span><span class="sxs-lookup"><span data-stu-id="bf444-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png









