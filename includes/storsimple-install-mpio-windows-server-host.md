#### <a name="to-install-mpio-on-the-host"></a><span data-ttu-id="d6da8-101">To install MPIO on the host</span><span class="sxs-lookup"><span data-stu-id="d6da8-101">To install MPIO on the host</span></span>
1. <span data-ttu-id="d6da8-102">Open Server Manager on your Windows Server host.</span><span class="sxs-lookup"><span data-stu-id="d6da8-102">Open Server Manager on your Windows Server host.</span></span> <span data-ttu-id="d6da8-103">By default, Server Manager starts when a member of the Administrators group logs on to a computer that is running Windows Server 2012 R2 or Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="d6da8-103">By default, Server Manager starts when a member of the Administrators group logs on to a computer that is running Windows Server 2012 R2 or Windows Server 2012.</span></span> <span data-ttu-id="d6da8-104">If the Server Manager is not already open, click **Start > Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-104">If the Server Manager is not already open, click **Start > Server Manager**.</span></span>
   
    ![Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-mpio-windows-server/IC740997.png)
2. <span data-ttu-id="d6da8-106">Click **Server Manager > Dashboard > Add roles and features**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-106">Click **Server Manager > Dashboard > Add roles and features**.</span></span> <span data-ttu-id="d6da8-107">This starts the **Add Roles and Features** wizard.</span><span class="sxs-lookup"><span data-stu-id="d6da8-107">This starts the **Add Roles and Features** wizard.</span></span>
   
    ![Add Roles And Features Wizard 1](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-mpio-windows-server/IC740998.png)
3. <span data-ttu-id="d6da8-109">In the **Add Roles and Features** wizard, do the following:</span><span class="sxs-lookup"><span data-stu-id="d6da8-109">In the **Add Roles and Features** wizard, do the following:</span></span>
   
   * <span data-ttu-id="d6da8-110">On the **Before you begin** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-110">On the **Before you begin** page, click **Next**.</span></span>
   * <span data-ttu-id="d6da8-111">On the **Select installation type** page, accept the default setting of **Role-based or feature-based** installation.</span><span class="sxs-lookup"><span data-stu-id="d6da8-111">On the **Select installation type** page, accept the default setting of **Role-based or feature-based** installation.</span></span> <span data-ttu-id="d6da8-112">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-112">Click **Next**.</span></span>
     
       ![Add Roles And Features Wizard 2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-mpio-windows-server/IC740999.png)
   * <span data-ttu-id="d6da8-114">On the **Select destination server** page, choose **Select a server from the server pool**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-114">On the **Select destination server** page, choose **Select a server from the server pool**.</span></span> <span data-ttu-id="d6da8-115">Your host server should be discovered automatically.</span><span class="sxs-lookup"><span data-stu-id="d6da8-115">Your host server should be discovered automatically.</span></span> <span data-ttu-id="d6da8-116">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-116">Click **Next**.</span></span>
   * <span data-ttu-id="d6da8-117">On the **Select server roles** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-117">On the **Select server roles** page, click **Next**.</span></span>
   * <span data-ttu-id="d6da8-118">On the **Select features** page, select **Multipath I/O**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-118">On the **Select features** page, select **Multipath I/O**, and click **Next**.</span></span>
     
       ![Add Roles And Features Wizard 5](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-mpio-windows-server/IC741000.png)
   * <span data-ttu-id="d6da8-120">On the **Confirm installation selections** page, confirm the selection and then select **Restart the destination server automatically if required**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="d6da8-120">On the **Confirm installation selections** page, confirm the selection and then select **Restart the destination server automatically if required**, as shown below.</span></span> <span data-ttu-id="d6da8-121">Click **Install**.</span><span class="sxs-lookup"><span data-stu-id="d6da8-121">Click **Install**.</span></span>
     
       ![Add Roles And Features Wizard 8](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-mpio-windows-server/IC741001.png)
   * <span data-ttu-id="d6da8-123">You will be notified when the installation is complete.</span><span class="sxs-lookup"><span data-stu-id="d6da8-123">You will be notified when the installation is complete.</span></span> <span data-ttu-id="d6da8-124">Click **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="d6da8-124">Click **Close** to close the wizard.</span></span>
     
       ![Add Roles And Features Wizard 9](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-mpio-windows-server/IC741002.png)







