---
title: Create and configure Azure Kubernetes Service clusters in Azure using Ansible
description: Learn how to use Ansible to create and manage an Azure Kubernetes Service cluster in Azure
ms.service: ansible
keywords: ansible, azure, devops, bash, cloudshell, playbook, aks, container, Kubernetes
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 08/23/2018
ms.openlocfilehash: f7dbc124781992ada9c3538cf415b836d8764064
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871290"
---
# <a name="create-and-configure-azure-kubernetes-service-clusters-in-azure-using-ansible"></a><span data-ttu-id="db093-104">Create and configure Azure Kubernetes Service clusters in Azure using Ansible</span><span class="sxs-lookup"><span data-stu-id="db093-104">Create and configure Azure Kubernetes Service clusters in Azure using Ansible</span></span>
<span data-ttu-id="db093-105">Ansible allows you to automate the deployment and configuration of resources in your environment.</span><span class="sxs-lookup"><span data-stu-id="db093-105">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="db093-106">You can use Ansible to manage your Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="db093-106">You can use Ansible to manage your Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="db093-107">This article shows you how to use Ansible to create and configure an Azure Kubernetes Service cluster.</span><span class="sxs-lookup"><span data-stu-id="db093-107">This article shows you how to use Ansible to create and configure an Azure Kubernetes Service cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db093-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db093-108">Prerequisites</span></span>
- <span data-ttu-id="db093-109">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="db093-109">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
- <span data-ttu-id="db093-110">**Azure service principal** - When [creating the service principal](/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest#create-the-service-principal), note the following values: **appId**, **displayName**, **password**, and **tenant**.</span><span class="sxs-lookup"><span data-stu-id="db093-110">**Azure service principal** - When [creating the service principal](/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest#create-the-service-principal), note the following values: **appId**, **displayName**, **password**, and **tenant**.</span></span>

- <span data-ttu-id="db093-111">[!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation1.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation1.md)] [!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation2.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation2.md)]</span><span class="sxs-lookup"><span data-stu-id="db093-111">[!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation1.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation1.md)] [!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation2.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation2.md)]</span></span>

> [!Note]
> <span data-ttu-id="db093-112">Ansible 2.6 is required to run the following the sample playbooks in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="db093-112">Ansible 2.6 is required to run the following the sample playbooks in this tutorial.</span></span> 

## <a name="create-a-managed-aks-cluster"></a><span data-ttu-id="db093-113">Create a managed AKS cluster</span><span class="sxs-lookup"><span data-stu-id="db093-113">Create a managed AKS cluster</span></span>
<span data-ttu-id="db093-114">The following sample Ansible playbook creates a resource group, and an AKS cluster that resides in the resource group:</span><span class="sxs-lookup"><span data-stu-id="db093-114">The following sample Ansible playbook creates a resource group, and an AKS cluster that resides in the resource group:</span></span>

  ```yaml
  - name: Create Azure Kubernetes Service
    hosts: localhost
    connection: local
    vars:
      resource_group: myResourceGroup
      location: eastus
      aks_name: myAKSCluster
      username: azureuser
      ssh_key: "your_ssh_key"
      client_id: "your_client_id"
      client_secret: "your_client_secret"
    tasks:
    - name: Create resource group
      azure_rm_resourcegroup:
        name: "{{ resource_group }}"
        location: "{{ location }}"
    - name: Create a managed Azure Container Services (AKS) cluster
      azure_rm_aks:
        name: "{{ aks_name }}"
        location: "{{ location }}"
        resource_group: "{{ resource_group }}"
        dns_prefix: "{{ aks_name }}"
        linux_profile:
          admin_username: "{{ username }}"
          ssh_key: "{{ ssh_key }}"
        service_principal:
          client_id: "{{ client_id }}"
          client_secret: "{{ client_secret }}"
        agent_pool_profiles:
          - name: default
            count: 2
            vm_size: Standard_D2_v2
        tags:
          Environment: Production
  ```

<span data-ttu-id="db093-115">The following bullets help to explain the preceding Ansible playbook code:</span><span class="sxs-lookup"><span data-stu-id="db093-115">The following bullets help to explain the preceding Ansible playbook code:</span></span>
- <span data-ttu-id="db093-116">The first section within **tasks** defines a resource group named **myResourceGroup** within the **eastus** location.</span><span class="sxs-lookup"><span data-stu-id="db093-116">The first section within **tasks** defines a resource group named **myResourceGroup** within the **eastus** location.</span></span> 
- <span data-ttu-id="db093-117">The second section within **tasks** defines an AKS cluster named **myAKSCluster** within the **myResourceGroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="db093-117">The second section within **tasks** defines an AKS cluster named **myAKSCluster** within the **myResourceGroup** resource group.</span></span> 

<span data-ttu-id="db093-118">To create the AKS cluster with Ansible, save the preceding sample playbook as `azure_create_aks.yml`, and run the playbook with the following command:</span><span class="sxs-lookup"><span data-stu-id="db093-118">To create the AKS cluster with Ansible, save the preceding sample playbook as `azure_create_aks.yml`, and run the playbook with the following command:</span></span>

  ```bash
  ansible-playbook azure_create_aks.yml
  ```

<span data-ttu-id="db093-119">The output from the \**ansible-playbook* command looks similar to the following showing that the AKS cluster has been successfully created:</span><span class="sxs-lookup"><span data-stu-id="db093-119">The output from the \**ansible-playbook* command looks similar to the following showing that the AKS cluster has been successfully created:</span></span>

  ```bash
  PLAY [Create AKS] ****************************************************************************************

  TASK [Gathering Facts] ********************************************************************************************
  ok: [localhost]

  TASK [Create resource group] **************************************************************************************
  changed: [localhost]

  TASK [Create a Azure Container Services (AKS) cluster] ***************************************************
  changed: [localhost]

  PLAY RECAP *********************************************************************************************************
  localhost                  : ok=3    changed=2    unreachable=0    failed=0
  ```

## <a name="scale-aks-nodes"></a><span data-ttu-id="db093-120">Scale AKS nodes</span><span class="sxs-lookup"><span data-stu-id="db093-120">Scale AKS nodes</span></span>

<span data-ttu-id="db093-121">The sample playbook in the previous section defines two nodes.</span><span class="sxs-lookup"><span data-stu-id="db093-121">The sample playbook in the previous section defines two nodes.</span></span> <span data-ttu-id="db093-122">If you need fewer or more container workloads on your cluster, you can easily adjust the number of nodes.</span><span class="sxs-lookup"><span data-stu-id="db093-122">If you need fewer or more container workloads on your cluster, you can easily adjust the number of nodes.</span></span> <span data-ttu-id="db093-123">The sample playbook in this section increases the number of nodes from two nodes to three.</span><span class="sxs-lookup"><span data-stu-id="db093-123">The sample playbook in this section increases the number of nodes from two nodes to three.</span></span> <span data-ttu-id="db093-124">Modifying the node count is done by changing the **count** value in the **agent_pool_profiles** block.</span><span class="sxs-lookup"><span data-stu-id="db093-124">Modifying the node count is done by changing the **count** value in the **agent_pool_profiles** block.</span></span> 

<span data-ttu-id="db093-125">Enter your own `ssh_key`, `client_id`, and `client_secret` in the **service_principal** block:</span><span class="sxs-lookup"><span data-stu-id="db093-125">Enter your own `ssh_key`, `client_id`, and `client_secret` in the **service_principal** block:</span></span>

```yaml
- name: Scale AKS cluster
  hosts: localhost
  connection: local
  vars:
    resource_group: myResourceGroup
    location: eastus
    aks_name: myAKSCluster
    username: azureuser
    ssh_key: "your_ssh_key"
    client_id: "your_client_id"
    client_secret: "your_client_secret"
  tasks:
  - name: Scaling an existed AKS cluster
    azure_rm_aks:
        name: "{{ aks_name }}"    
        location: "{{ location }}"
        resource_group: "{{ resource_group }}" 
        dns_prefix: "{{ aks_name }}" 
        linux_profile:
          admin_username: "{{ username }}"
          ssh_key: "{{ ssh_key }}"
        service_principal:
          client_id: "{{ client_id }}"
          client_secret: "{{ client_secret }}"
        agent_pool_profiles:
          - name: default
            count: 3
            vm_size: Standard_D2_v2
```

<span data-ttu-id="db093-126">To scale the Azure Kubernetes Service cluster with Ansible, save the preceding playbook as *azure_configure_aks.yml*, and run the playbook as follows:</span><span class="sxs-lookup"><span data-stu-id="db093-126">To scale the Azure Kubernetes Service cluster with Ansible, save the preceding playbook as *azure_configure_aks.yml*, and run the playbook as follows:</span></span>

  ```bash
  ansible-playbook azure_configure_aks.yml
  ```

<span data-ttu-id="db093-127">The following output shows that the AKS cluster has been successfully created:</span><span class="sxs-lookup"><span data-stu-id="db093-127">The following output shows that the AKS cluster has been successfully created:</span></span>

  ```bash
  PLAY [Scale AKS cluster] ***************************************************************

  TASK [Gathering Facts] ******************************************************************
  ok: [localhost]

  TASK [Scaling an existed AKS cluster] **************************************************
  changed: [localhost]

  PLAY RECAP ******************************************************************************
  localhost                  : ok=2    changed=1    unreachable=0    failed=0
  ```
## <a name="delete-a-managed-aks-cluster"></a><span data-ttu-id="db093-128">Delete a managed AKS cluster</span><span class="sxs-lookup"><span data-stu-id="db093-128">Delete a managed AKS cluster</span></span>

<span data-ttu-id="db093-129">The following sample Ansible playbook section illustrates how to delete an AKS cluster:</span><span class="sxs-lookup"><span data-stu-id="db093-129">The following sample Ansible playbook section illustrates how to delete an AKS cluster:</span></span>

  ```yaml
  - name: Delete a managed Azure Container Services (AKS) cluster
    hosts: localhost
    connection: local
    vars:
      resource_group: myResourceGroup
      aks_name: myAKSCluster
    tasks:
    - name: 
      azure_rm_aks:
        name: "{{ aks_name }}"
        resource_group: "{{ resource_group }}"
        state: absent
   ```

<span data-ttu-id="db093-130">To delete the Azure Kubernetes Service cluster with Ansible, save the preceding playbook as *azure_delete_aks.yml*, and run the playbook as follows:</span><span class="sxs-lookup"><span data-stu-id="db093-130">To delete the Azure Kubernetes Service cluster with Ansible, save the preceding playbook as *azure_delete_aks.yml*, and run the playbook as follows:</span></span>

  ```bash
  ansible-playbook azure_delete_aks.yml
  ```

<span data-ttu-id="db093-131">The following output shows that the AKS cluster has been successfully deleted:</span><span class="sxs-lookup"><span data-stu-id="db093-131">The following output shows that the AKS cluster has been successfully deleted:</span></span>
  ```bash
PLAY [Delete a managed Azure Container Services (AKS) cluster] ****************************

TASK [Gathering Facts] ********************************************************************
ok: [localhost]

TASK [azure_rm_aks] *********************************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
  ```
  
## <a name="next-steps"></a><span data-ttu-id="db093-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="db093-132">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="db093-133">Tutorial: Scale application in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="db093-133">Tutorial: Scale application in Azure Kubernetes Service (AKS)</span></span>](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale)
