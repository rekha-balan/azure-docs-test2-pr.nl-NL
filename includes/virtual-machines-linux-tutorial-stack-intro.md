## <a name="create-a-resource-group"></a><span data-ttu-id="932d8-101">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="932d8-101">Create a resource group</span></span>

<span data-ttu-id="932d8-102">Create a resource group with the [az group create](/cli/azure/group#az_group_create) command.</span><span class="sxs-lookup"><span data-stu-id="932d8-102">Create a resource group with the [az group create](/cli/azure/group#az_group_create) command.</span></span> <span data-ttu-id="932d8-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="932d8-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="932d8-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="932d8-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="932d8-105">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="932d8-105">Create a virtual machine</span></span>

<span data-ttu-id="932d8-106">Create a VM with the [az vm create](/cli/azure/vm#az_vm_create) command.</span><span class="sxs-lookup"><span data-stu-id="932d8-106">Create a VM with the [az vm create](/cli/azure/vm#az_vm_create) command.</span></span> 

<span data-ttu-id="932d8-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span><span class="sxs-lookup"><span data-stu-id="932d8-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="932d8-108">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="932d8-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span> <span data-ttu-id="932d8-109">The command also sets *azureuser* as an administrator user name.</span><span class="sxs-lookup"><span data-stu-id="932d8-109">The command also sets *azureuser* as an administrator user name.</span></span> <span data-ttu-id="932d8-110">You use this name later to connect to the VM.</span><span class="sxs-lookup"><span data-stu-id="932d8-110">You use this name later to connect to the VM.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="932d8-111">When the VM has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="932d8-111">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="932d8-112">Take note of the `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="932d8-112">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="932d8-113">This address is used to access the VM in later steps.</span><span class="sxs-lookup"><span data-stu-id="932d8-113">This address is used to access the VM in later steps.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="932d8-114">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="932d8-114">Open port 80 for web traffic</span></span> 

<span data-ttu-id="932d8-115">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="932d8-115">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="932d8-116">Because this VM is going to be a web server, you need to open port 80 from the internet.</span><span class="sxs-lookup"><span data-stu-id="932d8-116">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="932d8-117">Use the [az vm open-port](/cli/azure/vm#az_vm_open_port) command to open the desired port.</span><span class="sxs-lookup"><span data-stu-id="932d8-117">Use the [az vm open-port](/cli/azure/vm#az_vm_open_port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="932d8-118">SSH into your VM</span><span class="sxs-lookup"><span data-stu-id="932d8-118">SSH into your VM</span></span>


<span data-ttu-id="932d8-119">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span><span class="sxs-lookup"><span data-stu-id="932d8-119">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="932d8-120">You need this IP address for several later steps.</span><span class="sxs-lookup"><span data-stu-id="932d8-120">You need this IP address for several later steps.</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="932d8-121">Use the following command to create an SSH session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="932d8-121">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="932d8-122">Substitute the correct public IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="932d8-122">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="932d8-123">In this example, the IP address is *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="932d8-123">In this example, the IP address is *40.68.254.142*.</span></span> <span data-ttu-id="932d8-124">*azureuser* is the administrator user name set when you created the VM.</span><span class="sxs-lookup"><span data-stu-id="932d8-124">*azureuser* is the administrator user name set when you created the VM.</span></span>

```bash
ssh azureuser@40.68.254.142
```

