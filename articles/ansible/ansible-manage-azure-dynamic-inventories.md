---
title: Use Ansible to manage your Azure dynamic inventories
description: Learn how to use Ansible to manage your Azure dynamic inventories
ms.service: ansible
keywords: ansible, azure, devops, bash, cloudshell, dynamic inventory
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.date: 08/09/2018
ms.topic: article
ms.openlocfilehash: 1b8c1ba80b4c69f36e8304cbe978452a359ac911
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866295"
---
# <a name="use-ansible-to-manage-your-azure-dynamic-inventories"></a><span data-ttu-id="0fc3c-104">Use Ansible to manage your Azure dynamic inventories</span><span class="sxs-lookup"><span data-stu-id="0fc3c-104">Use Ansible to manage your Azure dynamic inventories</span></span>
<span data-ttu-id="0fc3c-105">Ansible can be used to pull inventory information from various sources (including cloud sources such as Azure) into a *dynamic inventory*.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-105">Ansible can be used to pull inventory information from various sources (including cloud sources such as Azure) into a *dynamic inventory*.</span></span> <span data-ttu-id="0fc3c-106">In this article, you use the [Azure Cloud Shell](./ansible-run-playbook-in-cloudshell.md) to configure an Ansible Azure Dynamic Inventory in which you create two virtual machines, tag one of those virtual machines, and install Nginx on the tagged virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-106">In this article, you use the [Azure Cloud Shell](./ansible-run-playbook-in-cloudshell.md) to configure an Ansible Azure Dynamic Inventory in which you create two virtual machines, tag one of those virtual machines, and install Nginx on the tagged virtual machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fc3c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0fc3c-107">Prerequisites</span></span>

- <span data-ttu-id="0fc3c-108">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-108">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>

- <span data-ttu-id="0fc3c-109">**Azure credentials** - [Create Azure credentials and configure Ansible](/azure/virtual-machines/linux/ansible-install-configure#create-azure-credentials)</span><span class="sxs-lookup"><span data-stu-id="0fc3c-109">**Azure credentials** - [Create Azure credentials and configure Ansible](/azure/virtual-machines/linux/ansible-install-configure#create-azure-credentials)</span></span>

## <a name="create-the-test-virtual-machines"></a><span data-ttu-id="0fc3c-110">Create the test virtual machines</span><span class="sxs-lookup"><span data-stu-id="0fc3c-110">Create the test virtual machines</span></span>

1. <span data-ttu-id="0fc3c-111">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="0fc3c-111">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="0fc3c-112">Open [Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="0fc3c-112">Open [Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

1. <span data-ttu-id="0fc3c-113">Create an Azure resource group to hold the virtual machines for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-113">Create an Azure resource group to hold the virtual machines for this tutorial.</span></span>

    > [!IMPORTANT]  
    > <span data-ttu-id="0fc3c-114">The Azure resource group you create in this step must have a name that is entirely lower-case.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-114">The Azure resource group you create in this step must have a name that is entirely lower-case.</span></span> <span data-ttu-id="0fc3c-115">Otherwise, the generation of the dynamic inventory will fail.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-115">Otherwise, the generation of the dynamic inventory will fail.</span></span>

    ```azurecli-interactive
    az group create --resource-group ansible-inventory-test-rg --location eastus
    ```

1. <span data-ttu-id="0fc3c-116">Create two Linux virtual machines on Azure using one of the following techniques:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-116">Create two Linux virtual machines on Azure using one of the following techniques:</span></span>

    - <span data-ttu-id="0fc3c-117">**Ansible playbook** - The article, [Create a basic virtual machine in Azure with Ansible](/azure/virtual-machines/linux/ansible-create-vm) illustrates how to create a virtual machine from an Ansible playbook.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-117">**Ansible playbook** - The article, [Create a basic virtual machine in Azure with Ansible](/azure/virtual-machines/linux/ansible-create-vm) illustrates how to create a virtual machine from an Ansible playbook.</span></span> <span data-ttu-id="0fc3c-118">If you use a playbook to define one or both of the virtual machines, ensure that the SSH connection is used instead of a password.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-118">If you use a playbook to define one or both of the virtual machines, ensure that the SSH connection is used instead of a password.</span></span>

    - <span data-ttu-id="0fc3c-119">**Azure CLI** - Issue each of the following commands in the Cloud Shell to create the two virtual machines:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-119">**Azure CLI** - Issue each of the following commands in the Cloud Shell to create the two virtual machines:</span></span>

        ```azurecli-interactive
        az vm create --resource-group ansible-inventory-test-rg \
                     --name ansible-inventory-test-vm1 \
                     --image UbuntuLTS --generate-ssh-keys
        ```

        ```azurecli-interactive
        az vm create --resource-group ansible-inventory-test-rg \
                     --name ansible-inventory-test-vm2 \
                     --image UbuntuLTS --generate-ssh-keys
        ```

## <a name="tag-a-virtual-machine"></a><span data-ttu-id="0fc3c-120">Tag a virtual machine</span><span class="sxs-lookup"><span data-stu-id="0fc3c-120">Tag a virtual machine</span></span>
<span data-ttu-id="0fc3c-121">You can [use tags to organize your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags#azure-cli) by user-defined categories.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-121">You can [use tags to organize your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags#azure-cli) by user-defined categories.</span></span> 

<span data-ttu-id="0fc3c-122">Enter the following [az resource tag](/cli/azure/resource?view=azure-cli-latest.md#az-resource-tag) command to tag the virtual machine `ansible-inventory-test-vm1` with the key `nginx`:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-122">Enter the following [az resource tag](/cli/azure/resource?view=azure-cli-latest.md#az-resource-tag) command to tag the virtual machine `ansible-inventory-test-vm1` with the key `nginx`:</span></span>

```azurecli-interactive
az resource tag --tags nginx --id /subscriptions/<YourAzureSubscriptionID>/resourceGroups/ansible-inventory-test-rg/providers/Microsoft.Compute/virtualMachines/ansible-inventory-test-vm1
```

## <a name="generate-a-dynamic-inventory"></a><span data-ttu-id="0fc3c-123">Generate a dynamic inventory</span><span class="sxs-lookup"><span data-stu-id="0fc3c-123">Generate a dynamic inventory</span></span>
<span data-ttu-id="0fc3c-124">Once you have your virtual machines defined (and tagged), it's time to generate the dynamic inventory.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-124">Once you have your virtual machines defined (and tagged), it's time to generate the dynamic inventory.</span></span> <span data-ttu-id="0fc3c-125">Ansible provides a Python script called [azure_rm.py](https://github.com/ansible/ansible/blob/devel/contrib/inventory/azure_rm.py) that generates a dynamic inventory of your Azure resources by making API requests to the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-125">Ansible provides a Python script called [azure_rm.py](https://github.com/ansible/ansible/blob/devel/contrib/inventory/azure_rm.py) that generates a dynamic inventory of your Azure resources by making API requests to the Azure Resource Manager.</span></span> <span data-ttu-id="0fc3c-126">The following steps walk you through using the `azure_rm.py` script to connect to your two test Azure virtual machines:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-126">The following steps walk you through using the `azure_rm.py` script to connect to your two test Azure virtual machines:</span></span>

1. <span data-ttu-id="0fc3c-127">Use the GNU `wget` command to retrieve the `azure_rm.py` script:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-127">Use the GNU `wget` command to retrieve the `azure_rm.py` script:</span></span>

    ```azurecli-interactive
    wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/azure_rm.py
    ```

1. <span data-ttu-id="0fc3c-128">Use the `chmod` command to change the access permissions to the `azure_rm.py` script.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-128">Use the `chmod` command to change the access permissions to the `azure_rm.py` script.</span></span> <span data-ttu-id="0fc3c-129">The following command uses the `+x` parameter to allow for execution (running) of the specified file (`azure_rm.py`):</span><span class="sxs-lookup"><span data-stu-id="0fc3c-129">The following command uses the `+x` parameter to allow for execution (running) of the specified file (`azure_rm.py`):</span></span>

    ```azurecli-interactive
    chmod +x azure_rm.py
    ```

1. <span data-ttu-id="0fc3c-130">Use the [ansible command](https://docs.ansible.com/ansible/2.4/ansible.html) to connect to your resource group:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-130">Use the [ansible command](https://docs.ansible.com/ansible/2.4/ansible.html) to connect to your resource group:</span></span> 

    ```azurecli-interactive
    ansible -i azure_rm.py ansible-inventory-test-rg -m ping 
    ```

1. <span data-ttu-id="0fc3c-131">Once connected, you see results similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-131">Once connected, you see results similar to the following output:</span></span>

    ```Output
    ansible-inventory-test-vm1 | SUCCESS => {
        "changed": false,
        "failed": false,
        "ping": "pong"
    }
    ansible-inventory-test-vm2 | SUCCESS => {
        "changed": false,
        "failed": false,
        "ping": "pong"
    }
    ```

## <a name="enable-the-virtual-machine-tag"></a><span data-ttu-id="0fc3c-132">Enable the virtual machine tag</span><span class="sxs-lookup"><span data-stu-id="0fc3c-132">Enable the virtual machine tag</span></span>
<span data-ttu-id="0fc3c-133">Once you've set the desired tag, you need to "enable" the tag.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-133">Once you've set the desired tag, you need to "enable" the tag.</span></span> <span data-ttu-id="0fc3c-134">One way to enable a tag is by exporting the tag to an environment variable called `AZURE_TAGS` via the **export** command:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-134">One way to enable a tag is by exporting the tag to an environment variable called `AZURE_TAGS` via the **export** command:</span></span>

```azurecli-interactive
export AZURE_TAGS=nginx
```

<span data-ttu-id="0fc3c-135">Once the tag has been exported, you can try the `ansible` command again:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-135">Once the tag has been exported, you can try the `ansible` command again:</span></span>

```azurecli-interactive
ansible -i azure_rm.py ansible-inventory-test-rg -m ping 
```

<span data-ttu-id="0fc3c-136">You now see only one virtual machine (the one whose tag matches the value exported into the **AZURE_TAGS** environment variable):</span><span class="sxs-lookup"><span data-stu-id="0fc3c-136">You now see only one virtual machine (the one whose tag matches the value exported into the **AZURE_TAGS** environment variable):</span></span>

```Output
ansible-inventory-test-vm1 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```

## <a name="set-up-nginx-on-the-tagged-vm"></a><span data-ttu-id="0fc3c-137">Set up Nginx on the tagged VM</span><span class="sxs-lookup"><span data-stu-id="0fc3c-137">Set up Nginx on the tagged VM</span></span>
<span data-ttu-id="0fc3c-138">The purpose of tags is to enable the ability to quickly and easily work with subgroups of your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-138">The purpose of tags is to enable the ability to quickly and easily work with subgroups of your virtual machines.</span></span> <span data-ttu-id="0fc3c-139">For example, let's say you want to install Nginx only on virtual machines to which you've assigned a tag of `nginx`.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-139">For example, let's say you want to install Nginx only on virtual machines to which you've assigned a tag of `nginx`.</span></span> <span data-ttu-id="0fc3c-140">The following steps illustrate how easy that is to accomplish:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-140">The following steps illustrate how easy that is to accomplish:</span></span>

1. <span data-ttu-id="0fc3c-141">Create a file (to contain your playbook) named `nginx.yml` as follows:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-141">Create a file (to contain your playbook) named `nginx.yml` as follows:</span></span>

  ```azurecli-interactive
  vi nginx.yml
  ```

1. <span data-ttu-id="0fc3c-142">Insert the following code into the newly created `nginx.yml` file:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-142">Insert the following code into the newly created `nginx.yml` file:</span></span>

    ```yml
    ---
    - name: Install and start Nginx on an Azure virtual machine
    hosts: azure
    become: yes
    tasks:
    - name: install nginx
      apt: pkg=nginx state=installed
      notify:
      - start nginx

    handlers:
    - name: start nginx
      service: name=nginx state=started
    ```

1. <span data-ttu-id="0fc3c-143">Run the `nginx.yml` playbook:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-143">Run the `nginx.yml` playbook:</span></span>

    ```azurecli-interactive
    ansible-playbook -i azure_rm.py nginx.yml
    ```

1. <span data-ttu-id="0fc3c-144">Once you run the playbook, you see results similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="0fc3c-144">Once you run the playbook, you see results similar to the following output:</span></span>

    ```Output
    PLAY [Install and start Nginx on an Azure virtual machine] **********

    TASK [Gathering Facts] **********
    ok: [ansible-inventory-test-vm1]

    TASK [install nginx] **********
    changed: [ansible-inventory-test-vm1]

    RUNNING HANDLER [start nginx] **********
    ok: [ansible-inventory-test-vm1]

    PLAY RECAP **********
    ansible-inventory-test-vm1 : ok=3    changed=1    unreachable=0    failed=0
    ```

## <a name="test-nginx-installation"></a><span data-ttu-id="0fc3c-145">Test Nginx installation</span><span class="sxs-lookup"><span data-stu-id="0fc3c-145">Test Nginx installation</span></span>
<span data-ttu-id="0fc3c-146">This section illustrates one technique to test that Nginx is installed on your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-146">This section illustrates one technique to test that Nginx is installed on your virtual machine.</span></span>

1. <span data-ttu-id="0fc3c-147">Use the [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-list-ip-addresses) command to retrieve the IP address of the `ansible-inventory-test-vm1` virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-147">Use the [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-list-ip-addresses) command to retrieve the IP address of the `ansible-inventory-test-vm1` virtual machine.</span></span> <span data-ttu-id="0fc3c-148">The returned value (the virtual machine's IP address) is then used as the parameter to the SSH command to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-148">The returned value (the virtual machine's IP address) is then used as the parameter to the SSH command to connect to the virtual machine.</span></span>

    ```azurecli-interactive
    ssh `az vm list-ip-addresses \
    -n ansible-inventory-test-vm1 \
    --query [0].virtualMachine.network.publicIpAddresses[0].ipAddress -o tsv`
    ```

1. <span data-ttu-id="0fc3c-149">While connected to the `ansible-inventory-test-vm1` virtual machine, run the [nginx -v](https://nginx.org/en/docs/switches.html) command to determine if Nginx is installed.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-149">While connected to the `ansible-inventory-test-vm1` virtual machine, run the [nginx -v](https://nginx.org/en/docs/switches.html) command to determine if Nginx is installed.</span></span>

    ```azurecli-interactive
    nginx -v
    ```

1. <span data-ttu-id="0fc3c-150">Once you run the `nginx -v` command, you see the Nginx version (second line) that indicates that Nginx is installed.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-150">Once you run the `nginx -v` command, you see the Nginx version (second line) that indicates that Nginx is installed.</span></span>

    ```Output
    tom@ansible-inventory-test-vm1:~$ nginx -v

    nginx version: nginx/1.10.3 (Ubuntu)
    
    tom@ansible-inventory-test-vm1:~$
    ```

1. <span data-ttu-id="0fc3c-151">Press the **&lt;Ctrl>D** keyboard combination to disconnect the SSH session.</span><span class="sxs-lookup"><span data-stu-id="0fc3c-151">Press the **&lt;Ctrl>D** keyboard combination to disconnect the SSH session.</span></span>

1. <span data-ttu-id="0fc3c-152">Performing the preceding steps for the `ansible-inventory-test-vm2` virtual machine yields an informational message indicating where you can get Nginx (which implies that you don't have it installed at this point):</span><span class="sxs-lookup"><span data-stu-id="0fc3c-152">Performing the preceding steps for the `ansible-inventory-test-vm2` virtual machine yields an informational message indicating where you can get Nginx (which implies that you don't have it installed at this point):</span></span>

    ```Output
    tom@ansible-inventory-test-vm2:~$ nginx -v
    The program 'nginx' can be found in the following packages:
    * nginx-core
    * nginx-extras
    * nginx-full
    * nginx-lightTry: sudo apt install <selected package>
    tom@ansible-inventory-test-vm2:~$
    ```

## <a name="next-steps"></a><span data-ttu-id="0fc3c-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fc3c-153">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="0fc3c-154">Create a basic virtual machine in Azure with Ansible</span><span class="sxs-lookup"><span data-stu-id="0fc3c-154">Create a basic virtual machine in Azure with Ansible</span></span>](/azure/virtual-machines/linux/ansible-create-vm)
