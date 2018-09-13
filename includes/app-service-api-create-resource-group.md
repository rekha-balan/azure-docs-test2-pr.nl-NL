<span data-ttu-id="62862-101">Create a resource group with the [az group create](/cli/azure/group?view=azure-cli-latest#az_group_create) command.</span><span class="sxs-lookup"><span data-stu-id="62862-101">Create a resource group with the [az group create](/cli/azure/group?view=azure-cli-latest#az_group_create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="62862-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span><span class="sxs-lookup"><span data-stu-id="62862-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="62862-103">To see the available locations, run the `az appservice list-locations` command.</span><span class="sxs-lookup"><span data-stu-id="62862-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="62862-104">You generally create resources in a region near you.</span><span class="sxs-lookup"><span data-stu-id="62862-104">You generally create resources in a region near you.</span></span>
