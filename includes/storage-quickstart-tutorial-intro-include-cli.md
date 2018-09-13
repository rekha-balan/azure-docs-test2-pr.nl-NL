## <a name="create-a-resource-group"></a><span data-ttu-id="aec5a-101">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="aec5a-101">Create a resource group</span></span>

<span data-ttu-id="aec5a-102">Create an Azure resource group with the [az group create](/cli/azure/group#az_group_create) command.</span><span class="sxs-lookup"><span data-stu-id="aec5a-102">Create an Azure resource group with the [az group create](/cli/azure/group#az_group_create) command.</span></span> <span data-ttu-id="aec5a-103">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="aec5a-103">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli-interactive
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="aec5a-104">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="aec5a-104">Create a storage account</span></span>

<span data-ttu-id="aec5a-105">Create a general-purpose storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span><span class="sxs-lookup"><span data-stu-id="aec5a-105">Create a general-purpose storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="aec5a-106">The general-purpose storage account can be used for all four services: blobs, files, tables, and queues.</span><span class="sxs-lookup"><span data-stu-id="aec5a-106">The general-purpose storage account can be used for all four services: blobs, files, tables, and queues.</span></span> 

```azurecli-interactive
az storage account create \
    --name mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --sku Standard_LRS \
    --encryption blob
```

## <a name="specify-storage-account-credentials"></a><span data-ttu-id="aec5a-107">Specify storage account credentials</span><span class="sxs-lookup"><span data-stu-id="aec5a-107">Specify storage account credentials</span></span>

<span data-ttu-id="aec5a-108">The Azure CLI needs your storage account credentials for most of the commands in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="aec5a-108">The Azure CLI needs your storage account credentials for most of the commands in this tutorial.</span></span> <span data-ttu-id="aec5a-109">While there are several options for doing so, one of the easiest ways to provide them is to set `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span><span class="sxs-lookup"><span data-stu-id="aec5a-109">While there are several options for doing so, one of the easiest ways to provide them is to set `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>

<span data-ttu-id="aec5a-110">First, display your storage account keys by using the [az storage account keys list](/cli/azure/storage/account/keys#list) command:</span><span class="sxs-lookup"><span data-stu-id="aec5a-110">First, display your storage account keys by using the [az storage account keys list](/cli/azure/storage/account/keys#list) command:</span></span>

```azurecli-interactive
az storage account keys list \
    --account-name mystorageaccount \
    --resource-group myResourceGroup \
    --output table
```

<span data-ttu-id="aec5a-111">Now, set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span><span class="sxs-lookup"><span data-stu-id="aec5a-111">Now, set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span> <span data-ttu-id="aec5a-112">You can do this in the Bash shell by using the `export` command:</span><span class="sxs-lookup"><span data-stu-id="aec5a-112">You can do this in the Bash shell by using the `export` command:</span></span>

```bash
export AZURE_STORAGE_ACCOUNT="mystorageaccountname"
export AZURE_STORAGE_ACCESS_KEY="myStorageAccountKey"
```