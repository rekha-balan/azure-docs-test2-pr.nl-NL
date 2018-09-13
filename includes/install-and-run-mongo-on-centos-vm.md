<span data-ttu-id="e7ce5-101">Follow these steps to install and run MongoDB on a virtual machine running CentOS Linux.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-101">Follow these steps to install and run MongoDB on a virtual machine running CentOS Linux.</span></span>

> [!WARNING]
> <span data-ttu-id="e7ce5-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="e7ce5-103">Security features should be enabled before deploying MongoDB to a production environment.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="e7ce5-104">See [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) for more information.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-104">See [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) for more information.</span></span>
> 
> 

1. <span data-ttu-id="e7ce5-105">Configure the Package Management System (YUM) so that you can install MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-105">Configure the Package Management System (YUM) so that you can install MongoDB.</span></span> <span data-ttu-id="e7ce5-106">Create a */etc/yum.repos.d/10gen.repo* file to hold information about your repository and add the following:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-106">Create a */etc/yum.repos.d/10gen.repo* file to hold information about your repository and add the following:</span></span>
   
        [10gen]
        name=10gen Repository
        baseurl=http://downloads-distro.mongodb.org/repo/redhat/os/x86_64
        gpgcheck=0
        enabled=1
2. <span data-ttu-id="e7ce5-107">Save the repo file and then run the following command to update the local package database:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-107">Save the repo file and then run the following command to update the local package database:</span></span>
   
        $ sudo yum update
3. <span data-ttu-id="e7ce5-108">To install the package, run the following command to install the latest stable version of MongoDB and the associated tools:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-108">To install the package, run the following command to install the latest stable version of MongoDB and the associated tools:</span></span>
   
        $ sudo yum install mongo-10gen mongo-10gen-server
   
    <span data-ttu-id="e7ce5-109">Wait while MongoDB downloads and installs.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-109">Wait while MongoDB downloads and installs.</span></span>
4. <span data-ttu-id="e7ce5-110">Create a data directory.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-110">Create a data directory.</span></span> <span data-ttu-id="e7ce5-111">By default MongoDB stores data in the */data/db* directory, but you must create that directory.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-111">By default MongoDB stores data in the */data/db* directory, but you must create that directory.</span></span> <span data-ttu-id="e7ce5-112">To create it, run:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-112">To create it, run:</span></span>
   
        $ sudo mkdir -p /srv/datadrive/data
        $ sudo chown `id -u` /srv/datadrive/data
   
    <span data-ttu-id="e7ce5-113">For more information on installing MongoDB on Linux, see [Quickstart Unix][QuickstartUnix].</span><span class="sxs-lookup"><span data-stu-id="e7ce5-113">For more information on installing MongoDB on Linux, see [Quickstart Unix][QuickstartUnix].</span></span>
5. <span data-ttu-id="e7ce5-114">To start the database, run:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-114">To start the database, run:</span></span>
   
        $ mongod --dbpath /srv/datadrive/data --logpath /srv/datadrive/data/mongod.log
   
    <span data-ttu-id="e7ce5-115">All log messages will be directed to the */srv/datadrive/data/mongod.log* file as MongoDB server starts and preallocates journal files.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-115">All log messages will be directed to the */srv/datadrive/data/mongod.log* file as MongoDB server starts and preallocates journal files.</span></span> <span data-ttu-id="e7ce5-116">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-116">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span>
6. <span data-ttu-id="e7ce5-117">To start the MongoDB administrative shell, open a separate SSH or PuTTY window and run:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-117">To start the MongoDB administrative shell, open a separate SSH or PuTTY window and run:</span></span>
   
        $ mongo
        > db.foo.save ( { a:1 } )
        > db.foo.find()
        { _id : ..., a : 1 }
        > show dbs  
        ...
        > show collections  
        ...  
        > help  
   
    <span data-ttu-id="e7ce5-118">The database is created by the insert.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-118">The database is created by the insert.</span></span>
7. <span data-ttu-id="e7ce5-119">Once MongoDB is installed you must configure an endpoint so that MongoDB can be accessed remotely.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-119">Once MongoDB is installed you must configure an endpoint so that MongoDB can be accessed remotely.</span></span> <span data-ttu-id="e7ce5-120">In the Management Portal, click **Virtual Machines**, then click the name of your new virtual machine, then click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-120">In the Management Portal, click **Virtual Machines**, then click the name of your new virtual machine, then click **Endpoints**.</span></span>
   
    ![Endpoints][Image7]
8. <span data-ttu-id="e7ce5-122">Click **Add Endpoint** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-122">Click **Add Endpoint** at the bottom of the page.</span></span>
   
    ![Endpoints][Image8]
9. <span data-ttu-id="e7ce5-124">Add an endpoint with the following settings:</span><span class="sxs-lookup"><span data-stu-id="e7ce5-124">Add an endpoint with the following settings:</span></span>
   
   * <span data-ttu-id="e7ce5-125">**Name**: Mongo</span><span class="sxs-lookup"><span data-stu-id="e7ce5-125">**Name**: Mongo</span></span>
   * <span data-ttu-id="e7ce5-126">**Protocol**: TCP</span><span class="sxs-lookup"><span data-stu-id="e7ce5-126">**Protocol**: TCP</span></span>
   * <span data-ttu-id="e7ce5-127">**Public Port**: 27017</span><span class="sxs-lookup"><span data-stu-id="e7ce5-127">**Public Port**: 27017</span></span>
   * <span data-ttu-id="e7ce5-128">**Private Port**: 27017</span><span class="sxs-lookup"><span data-stu-id="e7ce5-128">**Private Port**: 27017</span></span>
   
   <span data-ttu-id="e7ce5-129">This will allow MongoDB to be accessed remotely.</span><span class="sxs-lookup"><span data-stu-id="e7ce5-129">This will allow MongoDB to be accessed remotely.</span></span>

[QuickStartUnix]: http://www.mongodb.org/display/DOCS/Quickstart+Unix


[Image7]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-centos-vm/LinuxVmAddEndpoint.png
[Image8]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mongo-on-centos-vm/LinuxVmAddEndpoint2.png


