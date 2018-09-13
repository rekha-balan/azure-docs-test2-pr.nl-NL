### <a name="to-verify-your-connection-by-using-powershell"></a><span data-ttu-id="941ab-101">To verify your connection by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="941ab-101">To verify your connection by using PowerShell</span></span>
<span data-ttu-id="941ab-102">You can verify that your connection succeeded by using the `Get-AzureRmVirtualNetworkGatewayConnection` cmdlet, with or without `-Debug`.</span><span class="sxs-lookup"><span data-stu-id="941ab-102">You can verify that your connection succeeded by using the `Get-AzureRmVirtualNetworkGatewayConnection` cmdlet, with or without `-Debug`.</span></span> 

1. <span data-ttu-id="941ab-103">Use the following cmdlet example, configuring the values to match your own.</span><span class="sxs-lookup"><span data-stu-id="941ab-103">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="941ab-104">If prompted, select 'A' in order to run 'All'.</span><span class="sxs-lookup"><span data-stu-id="941ab-104">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="941ab-105">In the example, `-Name` refers to the name of the connection that you created and want to test.</span><span class="sxs-lookup"><span data-stu-id="941ab-105">In the example, `-Name` refers to the name of the connection that you created and want to test.</span></span>
   
        Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
2. <span data-ttu-id="941ab-106">After the cmdlet has finished, view the values.</span><span class="sxs-lookup"><span data-stu-id="941ab-106">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="941ab-107">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span><span class="sxs-lookup"><span data-stu-id="941ab-107">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
        Body:
        {
          "name": "MyGWConnection",
          "id":
        "/subscriptions/086cfaa0-0d1d-4b1c-94544-f8e3da2a0c7789/resourceGroups/MyRG/providers/Microsoft.Network/connections/MyGWConnection",
          "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "1c484f82-23ec-47e2-8cd8-231107450446b",
            "virtualNetworkGateway1": {
              "id":
        "/subscriptions/086cfaa0-0d1d-4b1c-94544-f8e3da2a0c7789/resourceGroups/MyRG/providers/Microsoft.Network/virtualNetworkGa
        teways/vnetgw1"
            },
            "localNetworkGateway2": {
              "id":
        "/subscriptions/086cfaa0-0d1d-4b1c-94544-f8e3da2a0c7789/resourceGroups/MyRG/providers/Microsoft.Network/localNetworkGate
        ways/LocalSite"
            },
            "connectionType": "IPsec",
            "routingWeight": 10,
            "sharedKey": "abc123",
            "connectionStatus": "Connected",
            "ingressBytesTransferred": 33509044,
            "egressBytesTransferred": 4142431
          }

### <a name="to-verify-your-connection-by-using-the-azure-portal"></a><span data-ttu-id="941ab-108">To verify your connection by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="941ab-108">To verify your connection by using the Azure portal</span></span>
<span data-ttu-id="941ab-109">In the Azure portal, you can view the connection status by navigating to the connection.</span><span class="sxs-lookup"><span data-stu-id="941ab-109">In the Azure portal, you can view the connection status by navigating to the connection.</span></span> <span data-ttu-id="941ab-110">There are multiple ways to do this.</span><span class="sxs-lookup"><span data-stu-id="941ab-110">There are multiple ways to do this.</span></span> <span data-ttu-id="941ab-111">The following steps show one way to navigate to your connection and verify.</span><span class="sxs-lookup"><span data-stu-id="941ab-111">The following steps show one way to navigate to your connection and verify.</span></span>

1. <span data-ttu-id="941ab-112">In the [Azure portal](http://portal.azure.com), click **All resources** and navigate to your virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="941ab-112">In the [Azure portal](http://portal.azure.com), click **All resources** and navigate to your virtual network gateway.</span></span>
2. <span data-ttu-id="941ab-113">On the blade for your virtual network gateway, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="941ab-113">On the blade for your virtual network gateway, click **Connections**.</span></span> <span data-ttu-id="941ab-114">You can see the status of each connection.</span><span class="sxs-lookup"><span data-stu-id="941ab-114">You can see the status of each connection.</span></span>
3. <span data-ttu-id="941ab-115">Click the name of the connection that you want to verify to open **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="941ab-115">Click the name of the connection that you want to verify to open **Essentials**.</span></span> <span data-ttu-id="941ab-116">In Essentials, you can view more information about your connection.</span><span class="sxs-lookup"><span data-stu-id="941ab-116">In Essentials, you can view more information about your connection.</span></span> <span data-ttu-id="941ab-117">The **Status** is 'Succeeded' and 'Connected' when you have made a successful connection.</span><span class="sxs-lookup"><span data-stu-id="941ab-117">The **Status** is 'Succeeded' and 'Connected' when you have made a successful connection.</span></span>
   
    ![Verify connection](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/vpn-gateway-verify-connection-rm-include/connectionsucceeded.png)


