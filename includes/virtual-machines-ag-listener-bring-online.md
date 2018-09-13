1. <span data-ttu-id="43182-101">Navigate back to Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="43182-101">Navigate back to Failover Cluster Manager.</span></span>  <span data-ttu-id="43182-102">Expand **Roles** and then highlight your Availability Group.</span><span class="sxs-lookup"><span data-stu-id="43182-102">Expand **Roles** and then highlight your Availability Group.</span></span>  <span data-ttu-id="43182-103">On the **Resources** tab, right-click the listener name and click Properties.</span><span class="sxs-lookup"><span data-stu-id="43182-103">On the **Resources** tab, right-click the listener name and click Properties.</span></span>
2. <span data-ttu-id="43182-104">Click the **Dependencies** tab. If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span><span class="sxs-lookup"><span data-stu-id="43182-104">Click the **Dependencies** tab. If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  <span data-ttu-id="43182-105">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="43182-105">Click **OK**.</span></span>
3. <span data-ttu-id="43182-106">Right-click the listener name and click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="43182-106">Right-click the listener name and click **Bring Online**.</span></span>
4. <span data-ttu-id="43182-107">Once the listener is online, from the **Resources** tab, right-click the availability group and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="43182-107">Once the listener is online, from the **Resources** tab, right-click the availability group and click **Properties**.</span></span>
   
    ![Configure the Availability Group Resource](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)
5. <span data-ttu-id="43182-109">Create a dependency on the listener name resource (not the IP address resources name).</span><span class="sxs-lookup"><span data-stu-id="43182-109">Create a dependency on the listener name resource (not the IP address resources name).</span></span> <span data-ttu-id="43182-110">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="43182-110">Click **OK**.</span></span>
   
    ![Add Dependency on the Listener Name](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)
6. <span data-ttu-id="43182-112">Launch **SQL Server Management Studio** and connect to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="43182-112">Launch **SQL Server Management Studio** and connect to the primary replica.</span></span>
7. <span data-ttu-id="43182-113">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **<AvailabilityGroupName>** | **Availability Group Listeners**.</span><span class="sxs-lookup"><span data-stu-id="43182-113">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **<AvailabilityGroupName>** | **Availability Group Listeners**.</span></span> 
8. <span data-ttu-id="43182-114">You should now see the listener name that you created in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="43182-114">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="43182-115">Right-click the listener name and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="43182-115">Right-click the listener name and click **Properties**.</span></span>
9. <span data-ttu-id="43182-116">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (in this tutorial, 1433 was the default), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="43182-116">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (in this tutorial, 1433 was the default), then click **OK**.</span></span>


