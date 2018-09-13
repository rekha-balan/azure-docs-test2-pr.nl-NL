1. <span data-ttu-id="b84c4-101">Launch the Azure Site Recovery UnifiedSetup.exe</span><span class="sxs-lookup"><span data-stu-id="b84c4-101">Launch the Azure Site Recovery UnifiedSetup.exe</span></span>
2. <span data-ttu-id="b84c4-102">In **Before you begin**, select **Add additional process servers to scale out deployment**.</span><span class="sxs-lookup"><span data-stu-id="b84c4-102">In **Before you begin**, select **Add additional process servers to scale out deployment**.</span></span>

  ![Add process server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-1.png)

3. <span data-ttu-id="b84c4-104">In **Configuration Server Details**, specify the IP address of the Configuration Server, and the passphrase.</span><span class="sxs-lookup"><span data-stu-id="b84c4-104">In **Configuration Server Details**, specify the IP address of the Configuration Server, and the passphrase.</span></span>

  ![Add process server 2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-2.png)
4. <span data-ttu-id="b84c4-106">In **Internet Settings**, specify how the Provider running on the Configuration Server connects to Azure Site Recovery over the Internet.</span><span class="sxs-lookup"><span data-stu-id="b84c4-106">In **Internet Settings**, specify how the Provider running on the Configuration Server connects to Azure Site Recovery over the Internet.</span></span>

  ![Add process server 3](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-3.png)

   * <span data-ttu-id="b84c4-108">If you want to connect with the proxy that's currently set up on the machine, select **Connect with existing proxy settings**.</span><span class="sxs-lookup"><span data-stu-id="b84c4-108">If you want to connect with the proxy that's currently set up on the machine, select **Connect with existing proxy settings**.</span></span>
   * <span data-ttu-id="b84c4-109">If you want the Provider to connect directly, select **Connect directly without a proxy**.</span><span class="sxs-lookup"><span data-stu-id="b84c4-109">If you want the Provider to connect directly, select **Connect directly without a proxy**.</span></span>
   * <span data-ttu-id="b84c4-110">If the existing proxy requires authentication, or if you want to use a custom proxy for the Provider connection, select **Connect with custom proxy settings**.</span><span class="sxs-lookup"><span data-stu-id="b84c4-110">If the existing proxy requires authentication, or if you want to use a custom proxy for the Provider connection, select **Connect with custom proxy settings**.</span></span>

     * <span data-ttu-id="b84c4-111">If you use a custom proxy, you need to specify the address, port, and credentials.</span><span class="sxs-lookup"><span data-stu-id="b84c4-111">If you use a custom proxy, you need to specify the address, port, and credentials.</span></span>
     * <span data-ttu-id="b84c4-112">If you're using a proxy, you should have already allowed access to the service urls.</span><span class="sxs-lookup"><span data-stu-id="b84c4-112">If you're using a proxy, you should have already allowed access to the service urls.</span></span>

5. <span data-ttu-id="b84c4-113">In **Prerequisites Check**, Setup runs a check to make sure that installation can run.</span><span class="sxs-lookup"><span data-stu-id="b84c4-113">In **Prerequisites Check**, Setup runs a check to make sure that installation can run.</span></span> <span data-ttu-id="b84c4-114">If a warning appears about the **Global time sync check**, verify that the time on the system clock (**Date and Time** settings) is the same as the time zone.</span><span class="sxs-lookup"><span data-stu-id="b84c4-114">If a warning appears about the **Global time sync check**, verify that the time on the system clock (**Date and Time** settings) is the same as the time zone.</span></span>

     ![Add process server 4](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-4.png)

6. <span data-ttu-id="b84c4-116">In **Environment Details**, select whether you're going to replicate VMware VMs.</span><span class="sxs-lookup"><span data-stu-id="b84c4-116">In **Environment Details**, select whether you're going to replicate VMware VMs.</span></span> <span data-ttu-id="b84c4-117">If you are, then setup checks that PowerCLI 6.0 is installed.</span><span class="sxs-lookup"><span data-stu-id="b84c4-117">If you are, then setup checks that PowerCLI 6.0 is installed.</span></span>

     ![Add process server 5](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-5.png)

7. <span data-ttu-id="b84c4-119">In **Install Location**, select where you want to install the binaries and store the cache.</span><span class="sxs-lookup"><span data-stu-id="b84c4-119">In **Install Location**, select where you want to install the binaries and store the cache.</span></span> <span data-ttu-id="b84c4-120">The drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span><span class="sxs-lookup"><span data-stu-id="b84c4-120">The drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span></span>
     <span data-ttu-id="b84c4-121">![Add process server 5](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-6.png)</span><span class="sxs-lookup"><span data-stu-id="b84c4-121">![Add process server 5](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-6.png)</span></span>

8. <span data-ttu-id="b84c4-122">In **Network Selection**, specify the listener (network adapter and SSL port) on which the Configuration Server sends and receives replication data.</span><span class="sxs-lookup"><span data-stu-id="b84c4-122">In **Network Selection**, specify the listener (network adapter and SSL port) on which the Configuration Server sends and receives replication data.</span></span> <span data-ttu-id="b84c4-123">Port 9443 is the default port used for sending and receiving replication traffic, but you can modify this port number to suit your environment's requirements.</span><span class="sxs-lookup"><span data-stu-id="b84c4-123">Port 9443 is the default port used for sending and receiving replication traffic, but you can modify this port number to suit your environment's requirements.</span></span> <span data-ttu-id="b84c4-124">In addition to the port 9443, we also open port 443, which is used by a web server to orchestrate replication operations.</span><span class="sxs-lookup"><span data-stu-id="b84c4-124">In addition to the port 9443, we also open port 443, which is used by a web server to orchestrate replication operations.</span></span> <span data-ttu-id="b84c4-125">Do not use Port 443 for sending or receiving replication traffic.</span><span class="sxs-lookup"><span data-stu-id="b84c4-125">Do not use Port 443 for sending or receiving replication traffic.</span></span>

     ![Add process server 6](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-7.png)
9. <span data-ttu-id="b84c4-127">In **Summary**, review the information and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="b84c4-127">In **Summary**, review the information and click **Install**.</span></span> <span data-ttu-id="b84c4-128">When installation finishes, a passphrase is generated.</span><span class="sxs-lookup"><span data-stu-id="b84c4-128">When installation finishes, a passphrase is generated.</span></span> <span data-ttu-id="b84c4-129">You will need this when you enable replication, so copy it and keep it in a secure location.</span><span class="sxs-lookup"><span data-stu-id="b84c4-129">You will need this when you enable replication, so copy it and keep it in a secure location.</span></span>

     ![Add process server 7](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-add-process-server/ps-page-8.png)








