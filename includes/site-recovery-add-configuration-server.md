1. <span data-ttu-id="c2656-101">Run the Unified Setup installation file.</span><span class="sxs-lookup"><span data-stu-id="c2656-101">Run the Unified Setup installation file.</span></span>
2. <span data-ttu-id="c2656-102">In **Before you begin**, select **Install the configuration server and process server**.</span><span class="sxs-lookup"><span data-stu-id="c2656-102">In **Before you begin**, select **Install the configuration server and process server**.</span></span>
    <span data-ttu-id="c2656-103">![Before you start](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz1.png)</span><span class="sxs-lookup"><span data-stu-id="c2656-103">![Before you start](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz1.png)</span></span>
3. <span data-ttu-id="c2656-104">In **Third Party Software License**, click **I Accept** to download and install MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2656-104">In **Third Party Software License**, click **I Accept** to download and install MySQL.</span></span>

    ![Third-party software](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz2.png)
4. <span data-ttu-id="c2656-106">In **Registration**, select the registration key you downloaded from the vault.</span><span class="sxs-lookup"><span data-stu-id="c2656-106">In **Registration**, select the registration key you downloaded from the vault.</span></span>

    ![Registration](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz3.png)
5. <span data-ttu-id="c2656-108">In **Internet Settings**, specify how the Provider running on the configuration server connects to Azure Site Recovery over the Internet.</span><span class="sxs-lookup"><span data-stu-id="c2656-108">In **Internet Settings**, specify how the Provider running on the configuration server connects to Azure Site Recovery over the Internet.</span></span>

   * <span data-ttu-id="c2656-109">If you want to connect with the proxy that's currently set up on the machine, select **Connect with existing proxy settings**.</span><span class="sxs-lookup"><span data-stu-id="c2656-109">If you want to connect with the proxy that's currently set up on the machine, select **Connect with existing proxy settings**.</span></span>
   * <span data-ttu-id="c2656-110">If you want the Provider to connect directly, select **Connect directly without a proxy**.</span><span class="sxs-lookup"><span data-stu-id="c2656-110">If you want the Provider to connect directly, select **Connect directly without a proxy**.</span></span>
   * <span data-ttu-id="c2656-111">If the existing proxy requires authentication, or if you want to use a custom proxy for the Provider connection, select **Connect with custom proxy settings**.</span><span class="sxs-lookup"><span data-stu-id="c2656-111">If the existing proxy requires authentication, or if you want to use a custom proxy for the Provider connection, select **Connect with custom proxy settings**.</span></span>

     * <span data-ttu-id="c2656-112">If you use a custom proxy, you need to specify the address, port, and credentials.</span><span class="sxs-lookup"><span data-stu-id="c2656-112">If you use a custom proxy, you need to specify the address, port, and credentials.</span></span>
     * <span data-ttu-id="c2656-113">If you're using a proxy, you should have already allowed the URLs described in [prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="c2656-113">If you're using a proxy, you should have already allowed the URLs described in [prerequisites](#prerequisites).</span></span>

     ![Firewall](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz4.png)
6. <span data-ttu-id="c2656-115">In **Prerequisites Check**, Setup runs a check to make sure that installation can run.</span><span class="sxs-lookup"><span data-stu-id="c2656-115">In **Prerequisites Check**, Setup runs a check to make sure that installation can run.</span></span> <span data-ttu-id="c2656-116">If a warning appears about the **Global time sync check**, verify that the time on the system clock (**Date and Time** settings) is the same as the time zone.</span><span class="sxs-lookup"><span data-stu-id="c2656-116">If a warning appears about the **Global time sync check**, verify that the time on the system clock (**Date and Time** settings) is the same as the time zone.</span></span>

    ![Prerequisites](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz5.png)
7. <span data-ttu-id="c2656-118">In **MySQL Configuration**, create credentials for logging on to the MySQL server instance that is installed.</span><span class="sxs-lookup"><span data-stu-id="c2656-118">In **MySQL Configuration**, create credentials for logging on to the MySQL server instance that is installed.</span></span>

    ![MySQL](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz6.png)
8. <span data-ttu-id="c2656-120">In **Environment Details**, select whether you're going to replicate VMware VMs.</span><span class="sxs-lookup"><span data-stu-id="c2656-120">In **Environment Details**, select whether you're going to replicate VMware VMs.</span></span> <span data-ttu-id="c2656-121">If you are, then setup checks that PowerCLI 6.0 is installed.</span><span class="sxs-lookup"><span data-stu-id="c2656-121">If you are, then setup checks that PowerCLI 6.0 is installed.</span></span>

    ![MySQL](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz7.png)

9. <span data-ttu-id="c2656-123">In **Install Location**, select where you want to install the binaries and store the cache.</span><span class="sxs-lookup"><span data-stu-id="c2656-123">In **Install Location**, select where you want to install the binaries and store the cache.</span></span> <span data-ttu-id="c2656-124">The drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span><span class="sxs-lookup"><span data-stu-id="c2656-124">The drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span></span>

    ![Install location](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz8.png)
10. <span data-ttu-id="c2656-126">In **Network Selection**, specify the listener (network adapter and SSL port) on which the configuration server sends and receives replication data.</span><span class="sxs-lookup"><span data-stu-id="c2656-126">In **Network Selection**, specify the listener (network adapter and SSL port) on which the configuration server sends and receives replication data.</span></span> <span data-ttu-id="c2656-127">Port 9443 is the default port used for sending and receiving replication traffic, but you can modify this port number to suit your environment's requirements.</span><span class="sxs-lookup"><span data-stu-id="c2656-127">Port 9443 is the default port used for sending and receiving replication traffic, but you can modify this port number to suit your environment's requirements.</span></span> <span data-ttu-id="c2656-128">In addition to the port 9443, we also open port 443, which is used by a web server to orchestrate replication operations.</span><span class="sxs-lookup"><span data-stu-id="c2656-128">In addition to the port 9443, we also open port 443, which is used by a web server to orchestrate replication operations.</span></span> <span data-ttu-id="c2656-129">Do not use Port 443 for sending or receiving replication traffic.</span><span class="sxs-lookup"><span data-stu-id="c2656-129">Do not use Port 443 for sending or receiving replication traffic.</span></span>

    ![Network selection](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz9.png)


11. <span data-ttu-id="c2656-131">In **Summary**, review the information and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="c2656-131">In **Summary**, review the information and click **Install**.</span></span> <span data-ttu-id="c2656-132">When installation finishes, a passphrase is generated.</span><span class="sxs-lookup"><span data-stu-id="c2656-132">When installation finishes, a passphrase is generated.</span></span> <span data-ttu-id="c2656-133">You will need this when you enable replication, so copy it and keep it in a secure location.</span><span class="sxs-lookup"><span data-stu-id="c2656-133">You will need this when you enable replication, so copy it and keep it in a secure location.</span></span>

    ![Summary](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-configuration-server/combined-wiz10.png)

<span data-ttu-id="c2656-135">After registration finishes, the server is displayed on the **Settings** > **Servers** blade in the vault.</span><span class="sxs-lookup"><span data-stu-id="c2656-135">After registration finishes, the server is displayed on the **Settings** > **Servers** blade in the vault.</span></span>










