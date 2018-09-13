## <a name="sign-in-to-azure"></a><span data-ttu-id="09ca3-101">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="09ca3-101">Sign in to Azure</span></span>

<span data-ttu-id="09ca3-102">Sign in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="09ca3-102">Sign in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="09ca3-103">If you don't know which location you want to use, you can list the available locations.</span><span class="sxs-lookup"><span data-stu-id="09ca3-103">If you don't know which location you want to use, you can list the available locations.</span></span> <span data-ttu-id="09ca3-104">After the list is displayed, find the one you want to use.</span><span class="sxs-lookup"><span data-stu-id="09ca3-104">After the list is displayed, find the one you want to use.</span></span> <span data-ttu-id="09ca3-105">This example uses **eastus**.</span><span class="sxs-lookup"><span data-stu-id="09ca3-105">This example uses **eastus**.</span></span> <span data-ttu-id="09ca3-106">Store this in a variable and use the variable so you can change it in one place.</span><span class="sxs-lookup"><span data-stu-id="09ca3-106">Store this in a variable and use the variable so you can change it in one place.</span></span>

```powershell
Get-AzureRmLocation | select Location 
$location = "eastus"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="09ca3-107">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="09ca3-107">Create a resource group</span></span>

<span data-ttu-id="09ca3-108">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="09ca3-108">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="09ca3-109">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="09ca3-109">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
$resourceGroup = "myResourceGroup"
New-AzureRmResourceGroup -Name $resourceGroup -Location $location 
```

## <a name="create-a-storage-account"></a><span data-ttu-id="09ca3-110">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="09ca3-110">Create a storage account</span></span>

<span data-ttu-id="09ca3-111">Create a standard general-purpose storage account with LRS replication using [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/New-AzureRmStorageAccount), then retrieve the storage account context that defines the storage account to be used.</span><span class="sxs-lookup"><span data-stu-id="09ca3-111">Create a standard general-purpose storage account with LRS replication using [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/New-AzureRmStorageAccount), then retrieve the storage account context that defines the storage account to be used.</span></span> <span data-ttu-id="09ca3-112">When acting on a storage account, you reference the context instead of repeatedly providing the credentials.</span><span class="sxs-lookup"><span data-stu-id="09ca3-112">When acting on a storage account, you reference the context instead of repeatedly providing the credentials.</span></span> <span data-ttu-id="09ca3-113">This example creates a storage account called *mystorageaccount* with locally redundant storage(LRS) and blob encryption (enabled by default).</span><span class="sxs-lookup"><span data-stu-id="09ca3-113">This example creates a storage account called *mystorageaccount* with locally redundant storage(LRS) and blob encryption (enabled by default).</span></span>

```powershell
$storageAccount = New-AzureRmStorageAccount -ResourceGroupName $resourceGroup `
  -Name "mystorageaccount" `
  -Location $location `
  -SkuName Standard_LRS `
  -Kind Storage

$ctx = $storageAccount.Context
```
