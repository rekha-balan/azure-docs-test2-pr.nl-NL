## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="e7e6c-101">Set up Azure PowerShell for Azure DNS</span><span class="sxs-lookup"><span data-stu-id="e7e6c-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="e7e6c-102">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e7e6c-102">Before you begin</span></span>

<span data-ttu-id="e7e6c-103">Verify that you have the following items before beginning your configuration.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="e7e6c-104">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-104">An Azure subscription.</span></span> <span data-ttu-id="e7e6c-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7e6c-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e7e6c-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e7e6c-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e7e6c-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="e7e6c-108">Sign in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="e7e6c-108">Sign in to your Azure account</span></span>

<span data-ttu-id="e7e6c-109">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-109">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="e7e6c-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e7e6c-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-the-subscription"></a><span data-ttu-id="e7e6c-111">Select the subscription</span><span class="sxs-lookup"><span data-stu-id="e7e6c-111">Select the subscription</span></span>
 
<span data-ttu-id="e7e6c-112">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="e7e6c-113">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-113">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="e7e6c-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="e7e6c-114">Create a resource group</span></span>

<span data-ttu-id="e7e6c-115">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e7e6c-116">This location is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-116">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="e7e6c-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="e7e6c-118">You can skip this step if you are using an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="e7e6c-119">Register resource provider</span><span class="sxs-lookup"><span data-stu-id="e7e6c-119">Register resource provider</span></span>

<span data-ttu-id="e7e6c-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="e7e6c-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="e7e6c-122">This is a one-time operation for each subscription.</span><span class="sxs-lookup"><span data-stu-id="e7e6c-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```