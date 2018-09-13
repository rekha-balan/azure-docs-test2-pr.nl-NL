---
title: Create and manage virtual machines in DevTest Labs with Azure CLI | Microsoft Docs
description: Learn how to use Azure DevTest Labs to create and manage virtual machines with Azure CLI 2.0
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 5e50bc3c6804a6f3d3dafd07b2918605c4cbc6ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867340"
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="e3523-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e3523-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="e3523-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span><span class="sxs-lookup"><span data-stu-id="e3523-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="e3523-105">Before you begin:</span><span class="sxs-lookup"><span data-stu-id="e3523-105">Before you begin:</span></span>

* <span data-ttu-id="e3523-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="e3523-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="e3523-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e3523-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="e3523-108">To start, run az login to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="e3523-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="e3523-109">Create and verify the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e3523-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="e3523-110">Create a VM from a marketplace image with ssh authentication.</span><span class="sxs-lookup"><span data-stu-id="e3523-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="e3523-111">Put the **lab's resource group** name in the --resource-group parameter.</span><span class="sxs-lookup"><span data-stu-id="e3523-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="e3523-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#az-lab-vm-create).</span><span class="sxs-lookup"><span data-stu-id="e3523-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#az-lab-vm-create).</span></span>


<span data-ttu-id="e3523-113">Verify that the VM is available.</span><span class="sxs-lookup"><span data-stu-id="e3523-113">Verify that the VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="e3523-114">Start and connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e3523-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="e3523-115">Start a VM.</span><span class="sxs-lookup"><span data-stu-id="e3523-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="e3523-116">Put the **lab's resource group** name in the --resource-group parameter.</span><span class="sxs-lookup"><span data-stu-id="e3523-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="e3523-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="e3523-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="e3523-118">Update the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e3523-118">Update the virtual machine</span></span>
<span data-ttu-id="e3523-119">Apply artifacts to a VM.</span><span class="sxs-lookup"><span data-stu-id="e3523-119">Apply artifacts to a VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="e3523-120">List artifacts available in the lab.</span><span class="sxs-lookup"><span data-stu-id="e3523-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="e3523-121">Stop and delete the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e3523-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="e3523-122">Stop a VM.</span><span class="sxs-lookup"><span data-stu-id="e3523-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="e3523-123">Delete a VM.</span><span class="sxs-lookup"><span data-stu-id="e3523-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]