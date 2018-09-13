## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="9b40d-101">Set up Azure CLI for Azure DNS</span><span class="sxs-lookup"><span data-stu-id="9b40d-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="9b40d-102">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9b40d-102">Before you begin</span></span>

<span data-ttu-id="9b40d-103">Verify that you have the following items before beginning your configuration.</span><span class="sxs-lookup"><span data-stu-id="9b40d-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="9b40d-104">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9b40d-104">An Azure subscription.</span></span> <span data-ttu-id="9b40d-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b40d-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9b40d-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span><span class="sxs-lookup"><span data-stu-id="9b40d-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="9b40d-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9b40d-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="9b40d-108">Sign in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="9b40d-108">Sign in to your Azure account</span></span>

<span data-ttu-id="9b40d-109">Open a console window and authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="9b40d-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="9b40d-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="9b40d-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="9b40d-111">Switch CLI mode</span><span class="sxs-lookup"><span data-stu-id="9b40d-111">Switch CLI mode</span></span>

<span data-ttu-id="9b40d-112">Azure DNS uses Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b40d-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="9b40d-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span><span class="sxs-lookup"><span data-stu-id="9b40d-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="9b40d-114">Select the subscription</span><span class="sxs-lookup"><span data-stu-id="9b40d-114">Select the subscription</span></span>

<span data-ttu-id="9b40d-115">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="9b40d-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="9b40d-116">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="9b40d-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="9b40d-117">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="9b40d-117">Create a resource group</span></span>

<span data-ttu-id="9b40d-118">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="9b40d-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9b40d-119">This is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="9b40d-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="9b40d-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9b40d-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="9b40d-121">You can skip this step if you are using an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="9b40d-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="9b40d-122">Register resource provider</span><span class="sxs-lookup"><span data-stu-id="9b40d-122">Register resource provider</span></span>

<span data-ttu-id="9b40d-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span><span class="sxs-lookup"><span data-stu-id="9b40d-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="9b40d-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9b40d-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="9b40d-125">This is a one-time operation for each subscription.</span><span class="sxs-lookup"><span data-stu-id="9b40d-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

