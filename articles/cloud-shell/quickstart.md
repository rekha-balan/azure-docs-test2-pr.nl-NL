---
title: Bash in Azure Cloud Shell Quickstart | Microsoft Docs
description: Quickstart for Bash in Cloud Shell
services: ''
documentationcenter: ''
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/12/2018
ms.author: juluk
ms.openlocfilehash: 4b7e4302bba2efed12e19043da1f592bed12a2fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856301"
---
# <a name="quickstart-for-bash-in-azure-cloud-shell"></a><span data-ttu-id="091c7-103">Quickstart for Bash in Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="091c7-103">Quickstart for Bash in Azure Cloud Shell</span></span>

<span data-ttu-id="091c7-104">This document details how to use Bash in Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="091c7-104">This document details how to use Bash in Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="091c7-105">A [PowerShell in Azure Cloud Shell](quickstart-powershell.md) Quickstart is also available.</span><span class="sxs-lookup"><span data-stu-id="091c7-105">A [PowerShell in Azure Cloud Shell](quickstart-powershell.md) Quickstart is also available.</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="091c7-106">Start Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="091c7-106">Start Cloud Shell</span></span>
1. <span data-ttu-id="091c7-107">Launch **Cloud Shell** from the top navigation of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="091c7-107">Launch **Cloud Shell** from the top navigation of the Azure portal.</span></span> <br>
![](media/quickstart/shell-icon.png)

2. <span data-ttu-id="091c7-108">Select a subscription to create a storage account and Microsoft Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="091c7-108">Select a subscription to create a storage account and Microsoft Azure Files share.</span></span>
3. <span data-ttu-id="091c7-109">Select "Create storage"</span><span class="sxs-lookup"><span data-stu-id="091c7-109">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="091c7-110">You are automatically authenticated for Azure CLI 2.0 in every session.</span><span class="sxs-lookup"><span data-stu-id="091c7-110">You are automatically authenticated for Azure CLI 2.0 in every session.</span></span>

### <a name="select-the-bash-environment"></a><span data-ttu-id="091c7-111">Select the Bash environment</span><span class="sxs-lookup"><span data-stu-id="091c7-111">Select the Bash environment</span></span>
<span data-ttu-id="091c7-112">Check that the environment drop-down from the left-hand side of shell window says `Bash`.</span><span class="sxs-lookup"><span data-stu-id="091c7-112">Check that the environment drop-down from the left-hand side of shell window says `Bash`.</span></span> <br>
![](media/quickstart/env-selector.png)

### <a name="set-your-subscription"></a><span data-ttu-id="091c7-113">Set your subscription</span><span class="sxs-lookup"><span data-stu-id="091c7-113">Set your subscription</span></span>
1. <span data-ttu-id="091c7-114">List subscriptions you have access to.</span><span class="sxs-lookup"><span data-stu-id="091c7-114">List subscriptions you have access to.</span></span>
```azurecli-interactive
az account list
```

2. <span data-ttu-id="091c7-115">Set your preferred subscription:</span><span class="sxs-lookup"><span data-stu-id="091c7-115">Set your preferred subscription:</span></span> <br>
```azurecli-interactive
az account set --subscription my-subscription-name`
```

> [!TIP]
> <span data-ttu-id="091c7-116">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="091c7-116">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="091c7-117">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="091c7-117">Create a resource group</span></span>
<span data-ttu-id="091c7-118">Create a new resource group in WestUS named "MyRG".</span><span class="sxs-lookup"><span data-stu-id="091c7-118">Create a new resource group in WestUS named "MyRG".</span></span>
```azurecli-interactive
az group create --location westus --name MyRG
```

### <a name="create-a-linux-vm"></a><span data-ttu-id="091c7-119">Create a Linux VM</span><span class="sxs-lookup"><span data-stu-id="091c7-119">Create a Linux VM</span></span>
<span data-ttu-id="091c7-120">Create an Ubuntu VM in your new resource group.</span><span class="sxs-lookup"><span data-stu-id="091c7-120">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="091c7-121">The Azure CLI 2.0 will create SSH keys and set up the VM with them.</span><span class="sxs-lookup"><span data-stu-id="091c7-121">The Azure CLI 2.0 will create SSH keys and set up the VM with them.</span></span> <br>

```azurecli-interactive
az vm create -n myVM -g MyRG --image UbuntuLTS --generate-ssh-keys
```

> [!NOTE]
> <span data-ttu-id="091c7-122">Using `--generate-ssh-keys` instructs Azure CLI 2.0 to create and set up public and private keys in your VM and `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="091c7-122">Using `--generate-ssh-keys` instructs Azure CLI 2.0 to create and set up public and private keys in your VM and `$Home` directory.</span></span> <span data-ttu-id="091c7-123">By default keys are placed in Cloud Shell at `/home/<user>/.ssh/id_rsa` and `/home/<user>/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="091c7-123">By default keys are placed in Cloud Shell at `/home/<user>/.ssh/id_rsa` and `/home/<user>/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="091c7-124">Your `.ssh` folder is persisted in your attached file share's 5-GB image used to persist `$Home`.</span><span class="sxs-lookup"><span data-stu-id="091c7-124">Your `.ssh` folder is persisted in your attached file share's 5-GB image used to persist `$Home`.</span></span>

<span data-ttu-id="091c7-125">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="091c7-125">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="091c7-126">SSH into your Linux VM</span><span class="sxs-lookup"><span data-stu-id="091c7-126">SSH into your Linux VM</span></span>
1. <span data-ttu-id="091c7-127">Search for your VM name in the Azure portal search bar.</span><span class="sxs-lookup"><span data-stu-id="091c7-127">Search for your VM name in the Azure portal search bar.</span></span>
2. <span data-ttu-id="091c7-128">Click "Connect" to get your VM name and public IP address.</span><span class="sxs-lookup"><span data-stu-id="091c7-128">Click "Connect" to get your VM name and public IP address.</span></span> <br>
![](media/quickstart/sshcmd-copy.png)

3. <span data-ttu-id="091c7-129">SSH into your VM with the `ssh` cmd.</span><span class="sxs-lookup"><span data-stu-id="091c7-129">SSH into your VM with the `ssh` cmd.</span></span>
```
ssh username@ipaddress
```

<span data-ttu-id="091c7-130">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span><span class="sxs-lookup"><span data-stu-id="091c7-130">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span> <br>
![](media/quickstart/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="091c7-131">Cleaning up</span><span class="sxs-lookup"><span data-stu-id="091c7-131">Cleaning up</span></span> 
1. <span data-ttu-id="091c7-132">Exit your ssh session.</span><span class="sxs-lookup"><span data-stu-id="091c7-132">Exit your ssh session.</span></span>
```azurecli-interactive
exit
```

2. <span data-ttu-id="091c7-133">Delete your resource group and any resources within it.</span><span class="sxs-lookup"><span data-stu-id="091c7-133">Delete your resource group and any resources within it.</span></span>
```azurecli-interactive
az group delete -n MyRG
```

## <a name="next-steps"></a><span data-ttu-id="091c7-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="091c7-134">Next steps</span></span>
[<span data-ttu-id="091c7-135">Learn about persisting files for Bash in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="091c7-135">Learn about persisting files for Bash in Cloud Shell</span></span>](persisting-shell-storage.md) <br>
[<span data-ttu-id="091c7-136">Learn about Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="091c7-136">Learn about Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/) <br>
[<span data-ttu-id="091c7-137">Learn about Azure Files storage</span><span class="sxs-lookup"><span data-stu-id="091c7-137">Learn about Azure Files storage</span></span>](../storage/files/storage-files-introduction.md) <br>
