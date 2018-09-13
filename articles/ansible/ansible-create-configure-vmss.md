---
title: Create virtual machine scale sets in Azure using Ansible
description: Learn how to use Ansible to create and configure a virtual machine scale set in Azure
ms.service: ansible
keywords: ansible, azure, devops, bash, playbook, virtual machine, virtual machine scale set, vmss
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 08/24/2018
ms.openlocfilehash: f3b08c41d3bf083c7cca5897cee11a1a4b9c9092
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867558"
---
# <a name="create-virtual-machine-scale-sets-in-azure-using-ansible"></a><span data-ttu-id="2ecf7-104">Create virtual machine scale sets in Azure using Ansible</span><span class="sxs-lookup"><span data-stu-id="2ecf7-104">Create virtual machine scale sets in Azure using Ansible</span></span>
<span data-ttu-id="2ecf7-105">Ansible allows you to automate the deployment and configuration of resources in your environment.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-105">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="2ecf7-106">You can use Ansible to manage your virtual machine scale set (VMSS) in Azure, the same as you would manage any other Azure resource.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-106">You can use Ansible to manage your virtual machine scale set (VMSS) in Azure, the same as you would manage any other Azure resource.</span></span> <span data-ttu-id="2ecf7-107">This article shows you how to use Ansible to create and scale out a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-107">This article shows you how to use Ansible to create and scale out a virtual machine scale set.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2ecf7-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ecf7-108">Prerequisites</span></span>
- <span data-ttu-id="2ecf7-109">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-109">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
- <span data-ttu-id="2ecf7-110">[!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation1.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation1.md)] [!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation2.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation2.md)]</span><span class="sxs-lookup"><span data-stu-id="2ecf7-110">[!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation1.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation1.md)] [!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation2.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation2.md)]</span></span>

> [!Note]
> <span data-ttu-id="2ecf7-111">Ansible 2.6 is required to run the following the sample playbooks in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-111">Ansible 2.6 is required to run the following the sample playbooks in this tutorial.</span></span> 

## <a name="create-a-vmss"></a><span data-ttu-id="2ecf7-112">Create a VMSS</span><span class="sxs-lookup"><span data-stu-id="2ecf7-112">Create a VMSS</span></span>
<span data-ttu-id="2ecf7-113">This section presents a sample Ansible playbook that defines the following resources:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-113">This section presents a sample Ansible playbook that defines the following resources:</span></span>
- <span data-ttu-id="2ecf7-114">**Resource group** into which all of your resources will be deployed</span><span class="sxs-lookup"><span data-stu-id="2ecf7-114">**Resource group** into which all of your resources will be deployed</span></span>
- <span data-ttu-id="2ecf7-115">**Virtual network** in the 10.0.0.0/16 address space</span><span class="sxs-lookup"><span data-stu-id="2ecf7-115">**Virtual network** in the 10.0.0.0/16 address space</span></span>
- <span data-ttu-id="2ecf7-116">**Subnet** within the virtual network</span><span class="sxs-lookup"><span data-stu-id="2ecf7-116">**Subnet** within the virtual network</span></span>
- <span data-ttu-id="2ecf7-117">**Public IP address** that allows you to access resources across the Internet</span><span class="sxs-lookup"><span data-stu-id="2ecf7-117">**Public IP address** that allows you to access resources across the Internet</span></span>
- <span data-ttu-id="2ecf7-118">**Network security group** that controls the flow of network traffic in and out of your virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ecf7-118">**Network security group** that controls the flow of network traffic in and out of your virtual machine scale set</span></span>
- <span data-ttu-id="2ecf7-119">**Load balancer** that distributes traffic across a set of defined VMs using load balancer rules</span><span class="sxs-lookup"><span data-stu-id="2ecf7-119">**Load balancer** that distributes traffic across a set of defined VMs using load balancer rules</span></span>
- <span data-ttu-id="2ecf7-120">**Virtual machine scale set** that uses all the created resources</span><span class="sxs-lookup"><span data-stu-id="2ecf7-120">**Virtual machine scale set** that uses all the created resources</span></span>

<span data-ttu-id="2ecf7-121">Enter your own password for the *admin_password* value.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-121">Enter your own password for the *admin_password* value.</span></span>

  ```yaml
  - hosts: localhost
    vars:
      resource_group: myResourceGroup
      vmss_name: myVMSS
      vmss_lb_name: myVMSSlb
      location: eastus
      admin_username: azureuser
      admin_password: "your_password"
    tasks:
      - name: Create a resource group
        azure_rm_resourcegroup:
          name: "{{ resource_group }}"
          location: "{{ location }}"
      - name: Create virtual network
        azure_rm_virtualnetwork:
          resource_group: "{{ resource_group }}"
          name: "{{ vmss_name }}"
          address_prefixes: "10.0.0.0/16"
      - name: Add subnet
        azure_rm_subnet:
          resource_group: "{{ resource_group }}"
          name: "{{ vmss_name }}"
          address_prefix: "10.0.1.0/24"
          virtual_network: "{{ vmss_name }}"
      - name: Create public IP address
        azure_rm_publicipaddress:
          resource_group: "{{ resource_group }}"
          allocation_method: Static
          name: "{{ vmss_name }}"
      - name: Create Network Security Group that allows SSH
        azure_rm_securitygroup:
          resource_group: "{{ resource_group }}"
          name: "{{ vmss_name }}"
          rules:
            - name: SSH
              protocol: Tcp
              destination_port_range: 22
              access: Allow
              priority: 1001
              direction: Inbound

      - name: Create a load balancer
        azure_rm_loadbalancer:
          name: "{{ vmss_lb_name }}"
          location: "{{ location }}"
          resource_group: "{{ resource_group }}"
          public_ip: "{{ vmss_name }}"
          probe_protocol: Tcp
          probe_port: 8080
          probe_interval: 10
          probe_fail_count: 3
          protocol: Tcp
          load_distribution: Default
          frontend_port: 80
          backend_port: 8080
          idle_timeout: 4
          natpool_frontend_port_start: 50000
          natpool_frontend_port_end: 50040
          natpool_backend_port: 22
          natpool_protocol: Tcp

      - name: Create VMSS
        azure_rm_virtualmachine_scaleset:
          resource_group: "{{ resource_group }}"
          name: "{{ vmss_name }}"
          vm_size: Standard_DS1_v2
          admin_username: "{{ admin_username }}"
          admin_password: "{{ admin_password }}"
          ssh_password_enabled: true
          capacity: 2
          virtual_network_name: "{{ vmss_name }}"
          subnet_name: "{{ vmss_name }}"
          upgrade_policy: Manual
          tier: Standard
          managed_disk_type: Standard_LRS
          os_disk_caching: ReadWrite
          image:
            offer: UbuntuServer
            publisher: Canonical
            sku: 16.04-LTS
            version: latest
          load_balancer: "{{ vmss_lb_name }}"
          data_disks:
            - lun: 0
              disk_size_gb: 20
              managed_disk_type: Standard_LRS
              caching: ReadOnly
            - lun: 1
              disk_size_gb: 30
              managed_disk_type: Standard_LRS
              caching: ReadOnly
  ```

<span data-ttu-id="2ecf7-122">To create the virtual machine scale set environment with Ansible, save the preceding playbook as `vmss-create.yml`, or [download the sample Ansible playbook](https://github.com/Azure-Samples/ansible-playbooks/blob/master/vmss/vmss-create.yml).</span><span class="sxs-lookup"><span data-stu-id="2ecf7-122">To create the virtual machine scale set environment with Ansible, save the preceding playbook as `vmss-create.yml`, or [download the sample Ansible playbook](https://github.com/Azure-Samples/ansible-playbooks/blob/master/vmss/vmss-create.yml).</span></span>

<span data-ttu-id="2ecf7-123">To run the Ansible playbook, use the **ansible-playbook** command as follows:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-123">To run the Ansible playbook, use the **ansible-playbook** command as follows:</span></span>

  ```bash
  ansible-playbook vmss-create.yml
  ```

<span data-ttu-id="2ecf7-124">After running the playbook, output similar to the following example shows that the virtual machine scale set has been successfully created:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-124">After running the playbook, output similar to the following example shows that the virtual machine scale set has been successfully created:</span></span>

  ```bash
  PLAY [localhost] ***********************************************************

  TASK [Gathering Facts] *****************************************************
  ok: [localhost]

  TASK [Create a resource group] ****************************************************************************
  changed: [localhost]

  TASK [Create virtual network] ****************************************************************************
  changed: [localhost]

  TASK [Add subnet] **********************************************************
  changed: [localhost]

  TASK [Create public IP address] ****************************************************************************
  changed: [localhost]

  TASK [Create Network Security Group that allows SSH] ****************************************************************************
  changed: [localhost]

  TASK [Create a load balancer] ****************************************************************************
  changed: [localhost]

  TASK [Create VMSS] *********************************************************
  changed: [localhost]

  PLAY RECAP *****************************************************************
  localhost                  : ok=8    changed=7    unreachable=0    failed=0

  ```

## <a name="scale-out-a-vmss"></a><span data-ttu-id="2ecf7-125">Scale out a VMSS</span><span class="sxs-lookup"><span data-stu-id="2ecf7-125">Scale out a VMSS</span></span>
<span data-ttu-id="2ecf7-126">The created virtual machine scale set has two instances.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-126">The created virtual machine scale set has two instances.</span></span> <span data-ttu-id="2ecf7-127">If you navigate to the virtual machine scale set in the Azure portal, you see **Standard_DS1_v2 (2 instances)**.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-127">If you navigate to the virtual machine scale set in the Azure portal, you see **Standard_DS1_v2 (2 instances)**.</span></span> <span data-ttu-id="2ecf7-128">You can also use the [Azure Cloud Shell](https://shell.azure.com/) by running the following command within the Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-128">You can also use the [Azure Cloud Shell](https://shell.azure.com/) by running the following command within the Cloud Shell:</span></span>

  ```azurecli-interactive
  az vmss show -n myVMSS -g myResourceGroup --query '{"capacity":sku.capacity}' 
  ```

<span data-ttu-id="2ecf7-129">You see results similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-129">You see results similar to the following output:</span></span>

  ```bash
  {
    "capacity": 2,
  }
  ```

<span data-ttu-id="2ecf7-130">Now, let's scale from two instances to three instances.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-130">Now, let's scale from two instances to three instances.</span></span> <span data-ttu-id="2ecf7-131">The following Ansible playbook code retrieves information about the virtual machine scale, and changes its capacity from two to three.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-131">The following Ansible playbook code retrieves information about the virtual machine scale, and changes its capacity from two to three.</span></span> 

  ```yaml
  - hosts: localhost
    vars:
      resource_group: myResourceGroup
      vmss_name: myVMSS
    tasks: 
      - name: Get scaleset info
        azure_rm_virtualmachine_scaleset_facts:
          resource_group: "{{ resource_group }}"
          name: "{{ vmss_name }}"
          format: curated
        register: output_scaleset

      - name: Dump scaleset info
        debug:
          var: output_scaleset

      - name: Modify scaleset (change the capacity to 3)
        set_fact:
          body: "{{ output_scaleset.ansible_facts.azure_vmss[0] | combine({'capacity': 3}, recursive=True) }}"

      - name: Update something in that VMSS
        azure_rm_virtualmachine_scaleset: "{{ body }}"
  ```

<span data-ttu-id="2ecf7-132">To scale out the virtual machine scale set you created, save the preceding playbook as `vmss-scale-out.yml` or [download the sample Ansible playbook](https://github.com/Azure-Samples/ansible-playbooks/blob/master/vmss/vmss-scale-out.yml)).</span><span class="sxs-lookup"><span data-stu-id="2ecf7-132">To scale out the virtual machine scale set you created, save the preceding playbook as `vmss-scale-out.yml` or [download the sample Ansible playbook](https://github.com/Azure-Samples/ansible-playbooks/blob/master/vmss/vmss-scale-out.yml)).</span></span> 

<span data-ttu-id="2ecf7-133">The following command will run the playbook:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-133">The following command will run the playbook:</span></span>

  ```bash
  ansible-playbook vmss-scale-out.yml
  ```

<span data-ttu-id="2ecf7-134">The output from running the Ansible playbook shows that the virtual machine scale set has been successfully scaled out:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-134">The output from running the Ansible playbook shows that the virtual machine scale set has been successfully scaled out:</span></span>

  ```bash
  PLAY [localhost] **********************************************************

  TASK [Gathering Facts] ****************************************************
  ok: [localhost]

  TASK [Get scaleset info] ***************************************************************************
  ok: [localhost]

  TASK [Dump scaleset info] ***************************************************************************
  ok: [localhost] => {
      "output_scaleset": {
          "ansible_facts": {
              "azure_vmss": [
                  {
                      ......
                  }
              ]
          },
          "changed": false,
          "failed": false
      }
  }

  TASK [Modify scaleset (set upgradePolicy to Automatic and capacity to 3)] ***************************************************************************
  ok: [localhost]

  TASK [Update something in that VMSS] ***************************************************************************
  changed: [localhost]

  PLAY RECAP ****************************************************************
  localhost                  : ok=5    changed=1    unreachable=0    failed=0
  ```

<span data-ttu-id="2ecf7-135">If navigate to the virtual machine scale set you configured in the Azure portal, you see **Standard_DS1_v2 (3 instances)**.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-135">If navigate to the virtual machine scale set you configured in the Azure portal, you see **Standard_DS1_v2 (3 instances)**.</span></span> <span data-ttu-id="2ecf7-136">You can also verify the change with the [Azure Cloud Shell](https://shell.azure.com/) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2ecf7-136">You can also verify the change with the [Azure Cloud Shell](https://shell.azure.com/) by running the following command:</span></span>

  ```azurecli-interactive
  az vmss show -n myVMSS -g myResourceGroup --query '{"capacity":sku.capacity}' 
  ```

<span data-ttu-id="2ecf7-137">The result of running the command in Cloud Shell shows that three instances now exist.</span><span class="sxs-lookup"><span data-stu-id="2ecf7-137">The result of running the command in Cloud Shell shows that three instances now exist.</span></span> 

  ```bash
  {
    "capacity": 3,
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="2ecf7-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ecf7-138">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="2ecf7-139">Ansible sample playbook for VMSS</span><span class="sxs-lookup"><span data-stu-id="2ecf7-139">Ansible sample playbook for VMSS</span></span>](https://github.com/Azure-Samples/ansible-playbooks/tree/master/vmss)