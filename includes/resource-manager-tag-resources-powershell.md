<span data-ttu-id="c6514-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span><span class="sxs-lookup"><span data-stu-id="c6514-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="c6514-102">Before proceeding, check your version:</span><span class="sxs-lookup"><span data-stu-id="c6514-102">Before proceeding, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="c6514-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span><span class="sxs-lookup"><span data-stu-id="c6514-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span></span> <span data-ttu-id="c6514-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before proceeding with this topic.</span><span class="sxs-lookup"><span data-stu-id="c6514-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before proceeding with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="c6514-105">Every time you apply tags to a resource or resource group, you overwrite the existing tags on that resource or resource group.</span><span class="sxs-lookup"><span data-stu-id="c6514-105">Every time you apply tags to a resource or resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="c6514-106">Therefore, you must use a different approach based on whether the resource or resource group has existing tags that you want to preserve.</span><span class="sxs-lookup"><span data-stu-id="c6514-106">Therefore, you must use a different approach based on whether the resource or resource group has existing tags that you want to preserve.</span></span> <span data-ttu-id="c6514-107">To add tags to a:</span><span class="sxs-lookup"><span data-stu-id="c6514-107">To add tags to a:</span></span>

* <span data-ttu-id="c6514-108">resource group without existing tags.</span><span class="sxs-lookup"><span data-stu-id="c6514-108">resource group without existing tags.</span></span>

  ```powershell
  Set-AzureRmResourceGroup -Name TagTestGroup -Tag @{ Dept="IT"; Environment="Test" }
  ```

* <span data-ttu-id="c6514-109">resource group with existing tags.</span><span class="sxs-lookup"><span data-stu-id="c6514-109">resource group with existing tags.</span></span>

  ```powershell
  $tags = (Get-AzureRmResourceGroup -Name TagTestGroup).Tags
  $tags += @{Status="Approved"}
  Set-AzureRmResourceGroup -Tag $tags -Name TagTestGroup
  ```

* <span data-ttu-id="c6514-110">resource without existing tags.</span><span class="sxs-lookup"><span data-stu-id="c6514-110">resource without existing tags.</span></span>

  ```powershell
  Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName storageexample -ResourceGroupName TagTestGroup -ResourceType Microsoft.Storage/storageAccounts
  ```

* <span data-ttu-id="c6514-111">resource with existing tags.</span><span class="sxs-lookup"><span data-stu-id="c6514-111">resource with existing tags.</span></span>

  ```powershell
  $tags = (Get-AzureRmResource -ResourceName storageexample -ResourceGroupName TagTestGroup).Tags
  $tags += @{Status="Approved"}
  Set-AzureRmResource -Tag $tags -ResourceName storageexample -ResourceGroupName TagTestGroup -ResourceType Microsoft.Storage/storageAccounts
  ```

<span data-ttu-id="c6514-112">To apply all tags from a resource group to its resources, and **not retain existing tags on the resources**, use the following script:</span><span class="sxs-lookup"><span data-stu-id="c6514-112">To apply all tags from a resource group to its resources, and **not retain existing tags on the resources**, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="c6514-113">To apply all tags from a resource group to its resources, and **retain existing tags on resources that are not duplicates**, use the following script:</span><span class="sxs-lookup"><span data-stu-id="c6514-113">To apply all tags from a resource group to its resources, and **retain existing tags on resources that are not duplicates**, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="c6514-114">To remove all tags, pass an empty hash table.</span><span class="sxs-lookup"><span data-stu-id="c6514-114">To remove all tags, pass an empty hash table.</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name TagTestGgroup
```

<span data-ttu-id="c6514-115">To get resource groups with a specific tag, use `Find-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6514-115">To get resource groups with a specific tag, use `Find-AzureRmResourceGroup` cmdlet.</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="c6514-116">To get all the resources with a particular tag and value, use the `Find-AzureRmResource` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6514-116">To get all the resources with a particular tag and value, use the `Find-AzureRmResource` cmdlet.</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

