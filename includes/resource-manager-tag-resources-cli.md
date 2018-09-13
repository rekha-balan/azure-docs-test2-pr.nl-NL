<span data-ttu-id="fa96c-101">To add a tag to a resource group, use **azure group set**.</span><span class="sxs-lookup"><span data-stu-id="fa96c-101">To add a tag to a resource group, use **azure group set**.</span></span> <span data-ttu-id="fa96c-102">If the resource group does not have any existing tags, pass in the tag.</span><span class="sxs-lookup"><span data-stu-id="fa96c-102">If the resource group does not have any existing tags, pass in the tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="fa96c-103">Tags are updated as a whole.</span><span class="sxs-lookup"><span data-stu-id="fa96c-103">Tags are updated as a whole.</span></span> <span data-ttu-id="fa96c-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span><span class="sxs-lookup"><span data-stu-id="fa96c-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="fa96c-105">Tags are not inherited by resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="fa96c-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="fa96c-106">To add a tag to a resource, use **azure resource set**.</span><span class="sxs-lookup"><span data-stu-id="fa96c-106">To add a tag to a resource, use **azure resource set**.</span></span> <span data-ttu-id="fa96c-107">Pass the API version number for the resource type that you are adding the tag to.</span><span class="sxs-lookup"><span data-stu-id="fa96c-107">Pass the API version number for the resource type that you are adding the tag to.</span></span> <span data-ttu-id="fa96c-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span><span class="sxs-lookup"><span data-stu-id="fa96c-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="fa96c-109">In the results, look for the resource type you want.</span><span class="sxs-lookup"><span data-stu-id="fa96c-109">In the results, look for the resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="fa96c-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span><span class="sxs-lookup"><span data-stu-id="fa96c-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="fa96c-111">Tags exist directly on resources and resource groups.</span><span class="sxs-lookup"><span data-stu-id="fa96c-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="fa96c-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span><span class="sxs-lookup"><span data-stu-id="fa96c-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="fa96c-113">Which returns metadata about the resource group, including any tags applied to it.</span><span class="sxs-lookup"><span data-stu-id="fa96c-113">Which returns metadata about the resource group, including any tags applied to it.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="fa96c-114">You view the tags for a particular resource by using **azure resource show**.</span><span class="sxs-lookup"><span data-stu-id="fa96c-114">You view the tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="fa96c-115">To retrieve all the resources with a tag value, use:</span><span class="sxs-lookup"><span data-stu-id="fa96c-115">To retrieve all the resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="fa96c-116">To retrieve all the resource groups with a tag value, use:</span><span class="sxs-lookup"><span data-stu-id="fa96c-116">To retrieve all the resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="fa96c-117">You can view the existing tags in your subscription with the following command:</span><span class="sxs-lookup"><span data-stu-id="fa96c-117">You can view the existing tags in your subscription with the following command:</span></span>

```azurecli
azure tag list
```
