
1. <span data-ttu-id="39903-101">On the on-premises machine, log on to the [Azure Management Portal](http://manager.windowsazure.com) (this is the old portal).</span><span class="sxs-lookup"><span data-stu-id="39903-101">On the on-premises machine, log on to the [Azure Management Portal](http://manager.windowsazure.com) (this is the old portal).</span></span>
2. <span data-ttu-id="39903-102">At the bottom of the navigation pane, select **+NEW** > **App Services** > **BizTalk Service** > **Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="39903-102">At the bottom of the navigation pane, select **+NEW** > **App Services** > **BizTalk Service** > **Custom Create**.</span></span>
3. <span data-ttu-id="39903-103">Provide a **BizTalk Service Name** and select an **Edition**.</span><span class="sxs-lookup"><span data-stu-id="39903-103">Provide a **BizTalk Service Name** and select an **Edition**.</span></span> 
   
    <span data-ttu-id="39903-104">This tutorial uses **mobile1**.</span><span class="sxs-lookup"><span data-stu-id="39903-104">This tutorial uses **mobile1**.</span></span> <span data-ttu-id="39903-105">You will need to supply a unique name for your new BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="39903-105">You will need to supply a unique name for your new BizTalk Service.</span></span>
4. <span data-ttu-id="39903-106">Once the BizTalk Service has been created, select the **Hybrid Connections** tab, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="39903-106">Once the BizTalk Service has been created, select the **Hybrid Connections** tab, then click **Add**.</span></span>
   
    ![Add Hybrid Connection](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/hybrid-connections-create-new/3.png)
   
    <span data-ttu-id="39903-108">This creates a new hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="39903-108">This creates a new hybrid connection.</span></span>
5. <span data-ttu-id="39903-109">Provide a **Name** and **Host Name** for your hybrid connection and set **Port** to `1433`.</span><span class="sxs-lookup"><span data-stu-id="39903-109">Provide a **Name** and **Host Name** for your hybrid connection and set **Port** to `1433`.</span></span> 
   
    ![Configure Hybrid Connection](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/hybrid-connections-create-new/4.png)
   
    <span data-ttu-id="39903-111">The host name is the name of the on-premises server.</span><span class="sxs-lookup"><span data-stu-id="39903-111">The host name is the name of the on-premises server.</span></span> <span data-ttu-id="39903-112">This configures the hybrid connection to access SQL Server running on port 1433.</span><span class="sxs-lookup"><span data-stu-id="39903-112">This configures the hybrid connection to access SQL Server running on port 1433.</span></span> <span data-ttu-id="39903-113">If you are using a named SQL Server instance, instead use the static port you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="39903-113">If you are using a named SQL Server instance, instead use the static port you defined earlier.</span></span>
6. <span data-ttu-id="39903-114">After the new connection is created, the status of the of the new connection shows **On-premises setup incomplete**.</span><span class="sxs-lookup"><span data-stu-id="39903-114">After the new connection is created, the status of the of the new connection shows **On-premises setup incomplete**.</span></span>
7. <span data-ttu-id="39903-115">Navigate back to your mobile service, click **Configure**, scroll down to **Hybrid connections** and click **Add hybrid connection**, then select the hybrid connection that you just created and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="39903-115">Navigate back to your mobile service, click **Configure**, scroll down to **Hybrid connections** and click **Add hybrid connection**, then select the hybrid connection that you just created and click **OK**.</span></span>
   
    <span data-ttu-id="39903-116">This enables your mobile service to use your new hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="39903-116">This enables your mobile service to use your new hybrid connection.</span></span>

<span data-ttu-id="39903-117">Next, you'll need to install the Hybrid Connection Manager on the on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="39903-117">Next, you'll need to install the Hybrid Connection Manager on the on-premises computer.</span></span>



