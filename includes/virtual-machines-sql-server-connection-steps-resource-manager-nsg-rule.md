### <a name="configure-a-network-security-group-inbound-rule-for-the-vm"></a><span data-ttu-id="32120-101">Configure a Network Security Group inbound rule for the VM</span><span class="sxs-lookup"><span data-stu-id="32120-101">Configure a Network Security Group inbound rule for the VM</span></span>
<span data-ttu-id="32120-102">If you want to be able to connect to SQL Server over the internet, you have to configure an inbound rule on the Network Security Group for the port that your SQL Server instance is listening.</span><span class="sxs-lookup"><span data-stu-id="32120-102">If you want to be able to connect to SQL Server over the internet, you have to configure an inbound rule on the Network Security Group for the port that your SQL Server instance is listening.</span></span> <span data-ttu-id="32120-103">By default, this is TCP port 1433.</span><span class="sxs-lookup"><span data-stu-id="32120-103">By default, this is TCP port 1433.</span></span>

1. <span data-ttu-id="32120-104">In the portal, select **Virtual machines**, and then select your SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="32120-104">In the portal, select **Virtual machines**, and then select your SQL Server VM.</span></span>
2. <span data-ttu-id="32120-105">Then select the **Nework interfaces**.</span><span class="sxs-lookup"><span data-stu-id="32120-105">Then select the **Nework interfaces**.</span></span>
   
    ![network interface](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/rm-network-interface.png)
3. <span data-ttu-id="32120-107">Then select the Network Interface for your VM.</span><span class="sxs-lookup"><span data-stu-id="32120-107">Then select the Network Interface for your VM.</span></span>
4. <span data-ttu-id="32120-108">Click the **Network security group** link.</span><span class="sxs-lookup"><span data-stu-id="32120-108">Click the **Network security group** link.</span></span>
   
    ![network interface](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/rm-network-security-group.png)
5. <span data-ttu-id="32120-110">In the properties of the Network Security Group, expand **Inbound security rules**.</span><span class="sxs-lookup"><span data-stu-id="32120-110">In the properties of the Network Security Group, expand **Inbound security rules**.</span></span>
6. <span data-ttu-id="32120-111">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="32120-111">Click the **Add** button.</span></span>
7. <span data-ttu-id="32120-112">Provide a **Name** of "SQLServerPublicTraffic".</span><span class="sxs-lookup"><span data-stu-id="32120-112">Provide a **Name** of "SQLServerPublicTraffic".</span></span>
8. <span data-ttu-id="32120-113">Change **Protocol** to **TCP**.</span><span class="sxs-lookup"><span data-stu-id="32120-113">Change **Protocol** to **TCP**.</span></span>
9. <span data-ttu-id="32120-114">Specify a **Destination port range** of 1433 (or the port that your SQL Server Instance is listening on).</span><span class="sxs-lookup"><span data-stu-id="32120-114">Specify a **Destination port range** of 1433 (or the port that your SQL Server Instance is listening on).</span></span>
10. <span data-ttu-id="32120-115">Verify that **Action** is set to **Allow**.</span><span class="sxs-lookup"><span data-stu-id="32120-115">Verify that **Action** is set to **Allow**.</span></span> <span data-ttu-id="32120-116">The security rule dialog should look similar to the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="32120-116">The security rule dialog should look similar to the following screenshot.</span></span>
    
     ![network security rule](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/rm-network-security-rule.png)
11. <span data-ttu-id="32120-118">Click **OK** to save the rule for your VM.</span><span class="sxs-lookup"><span data-stu-id="32120-118">Click **OK** to save the rule for your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="32120-119">It is possible to have a second Network Security Group associated with your subnet (this is separate from the network security group on the VM).</span><span class="sxs-lookup"><span data-stu-id="32120-119">It is possible to have a second Network Security Group associated with your subnet (this is separate from the network security group on the VM).</span></span> <span data-ttu-id="32120-120">This is not done for you by default; however, if you created a network security group on your subnet, you must open port 1433 on both the subnet's and the VM's Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="32120-120">This is not done for you by default; however, if you created a network security group on your subnet, you must open port 1433 on both the subnet's and the VM's Network Security Group.</span></span> 
> 
> 




