## <a name="sample-scenario"></a><span data-ttu-id="bd08a-101">Sample Scenario</span><span class="sxs-lookup"><span data-stu-id="bd08a-101">Sample Scenario</span></span>
<span data-ttu-id="bd08a-102">To better illustrate how to manage NSGs, this article uses the scenario below.</span><span class="sxs-lookup"><span data-stu-id="bd08a-102">To better illustrate how to manage NSGs, this article uses the scenario below.</span></span>

![VNet scenario](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-nsg-scenario-include/figure1.png)

<span data-ttu-id="bd08a-104">In this scenario you will create an NSG for each subnet in the **TestVNet** virtual network, as described below:</span><span class="sxs-lookup"><span data-stu-id="bd08a-104">In this scenario you will create an NSG for each subnet in the **TestVNet** virtual network, as described below:</span></span> 

* <span data-ttu-id="bd08a-105">**NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-105">**NSG-FrontEnd**.</span></span> <span data-ttu-id="bd08a-106">The front end NSG will be applied to the *FrontEnd* subnet, and contain two rules:</span><span class="sxs-lookup"><span data-stu-id="bd08a-106">The front end NSG will be applied to the *FrontEnd* subnet, and contain two rules:</span></span>    
  * <span data-ttu-id="bd08a-107">**rdp-rule**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-107">**rdp-rule**.</span></span> <span data-ttu-id="bd08a-108">This rule will allow RDP traffic to the *FrontEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="bd08a-108">This rule will allow RDP traffic to the *FrontEnd* subnet.</span></span>
  * <span data-ttu-id="bd08a-109">**web-rule**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-109">**web-rule**.</span></span> <span data-ttu-id="bd08a-110">This rule will allow HTTP traffic to the *FrontEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="bd08a-110">This rule will allow HTTP traffic to the *FrontEnd* subnet.</span></span>
* <span data-ttu-id="bd08a-111">**NSG-BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-111">**NSG-BackEnd**.</span></span> <span data-ttu-id="bd08a-112">The back end NSG will be applied to the *BackEnd* subnet, and contain two rules:</span><span class="sxs-lookup"><span data-stu-id="bd08a-112">The back end NSG will be applied to the *BackEnd* subnet, and contain two rules:</span></span>    
  * <span data-ttu-id="bd08a-113">**sql-rule**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-113">**sql-rule**.</span></span> <span data-ttu-id="bd08a-114">This rule allows SQL traffic only from the *FrontEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="bd08a-114">This rule allows SQL traffic only from the *FrontEnd* subnet.</span></span>
  * <span data-ttu-id="bd08a-115">**web-rule**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-115">**web-rule**.</span></span> <span data-ttu-id="bd08a-116">This rule denies all internet bound traffic from the *BackEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="bd08a-116">This rule denies all internet bound traffic from the *BackEnd* subnet.</span></span>

<span data-ttu-id="bd08a-117">The combination of these rules create a DMZ-like scenario, where the back end subnet can only receive incoming traffic for SQL traffic from the front end subnet, and has no access to the Internet, while the front end subnet can communicate with the Internet, and receive incoming HTTP requests only.</span><span class="sxs-lookup"><span data-stu-id="bd08a-117">The combination of these rules create a DMZ-like scenario, where the back end subnet can only receive incoming traffic for SQL traffic from the front end subnet, and has no access to the Internet, while the front end subnet can communicate with the Internet, and receive incoming HTTP requests only.</span></span>

<span data-ttu-id="bd08a-118">To deploy the scenario described above, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="bd08a-118">To deploy the scenario described above, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="bd08a-119">In the sample instructions below, the template was used to deploy a resource group names **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="bd08a-119">In the sample instructions below, the template was used to deploy a resource group names **RG-NSG**.</span></span> 

