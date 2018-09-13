---
title: Run Ansible with Bash in Azure Cloud Shell
description: Learn how to perform various Ansible tasks with Bash in Azure Cloud Shell
ms.service: ansible
keywords: ansible, azure, devops, bash, cloudshell, playbook, bash
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.date: 08/07/2018
ms.topic: article
ms.openlocfilehash: 9928f646905dd0da4b15166ec55e5d8a183cb210
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867918"
---
# <a name="run-ansible-with-bash-in-azure-cloud-shell"></a><span data-ttu-id="0fc19-104">Run Ansible with Bash in Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0fc19-104">Run Ansible with Bash in Azure Cloud Shell</span></span>

<span data-ttu-id="0fc19-105">In this tutorial, you learn how to use Bash within Cloud Shell to configure an Azure subscription as your Ansible workspace.</span><span class="sxs-lookup"><span data-stu-id="0fc19-105">In this tutorial, you learn how to use Bash within Cloud Shell to configure an Azure subscription as your Ansible workspace.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0fc19-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0fc19-106">Prerequisites</span></span>

- <span data-ttu-id="0fc19-107">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span><span class="sxs-lookup"><span data-stu-id="0fc19-107">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span></span>

- <span data-ttu-id="0fc19-108">**Configure Azure Cloud Shell** - If you are new to Azure Cloud Shell, the article, [Quickstart for Bash in Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart), illustrates how to start and configure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0fc19-108">**Configure Azure Cloud Shell** - If you are new to Azure Cloud Shell, the article, [Quickstart for Bash in Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart), illustrates how to start and configure Cloud Shell.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="automatic-credential-configuration"></a><span data-ttu-id="0fc19-109">Automatic credential configuration</span><span class="sxs-lookup"><span data-stu-id="0fc19-109">Automatic credential configuration</span></span>

<span data-ttu-id="0fc19-110">When signed into the Cloud Shell, Ansible authenticates with Azure to manage infrastructure without any additional configuration.</span><span class="sxs-lookup"><span data-stu-id="0fc19-110">When signed into the Cloud Shell, Ansible authenticates with Azure to manage infrastructure without any additional configuration.</span></span> <span data-ttu-id="0fc19-111">If you have more than one subscription, you can choose which subscription Ansible should work with by exporting the `AZURE_SUBSCRIPTION_ID` environment variable.</span><span class="sxs-lookup"><span data-stu-id="0fc19-111">If you have more than one subscription, you can choose which subscription Ansible should work with by exporting the `AZURE_SUBSCRIPTION_ID` environment variable.</span></span> <span data-ttu-id="0fc19-112">To list all of your Azure subscriptions, run the following command:</span><span class="sxs-lookup"><span data-stu-id="0fc19-112">To list all of your Azure subscriptions, run the following command:</span></span>

```azurecli-interactive
az account list
```

<span data-ttu-id="0fc19-113">Using the **id** of the subscription with which you want to work, set the **AZURE_SUBSCRIPTION_ID** as follows:</span><span class="sxs-lookup"><span data-stu-id="0fc19-113">Using the **id** of the subscription with which you want to work, set the **AZURE_SUBSCRIPTION_ID** as follows:</span></span>

```azurecli-interactive
export AZURE_SUBSCRIPTION_ID=<your-subscription-id>
```

## <a name="verify-the-configuration"></a><span data-ttu-id="0fc19-114">Verify the configuration</span><span class="sxs-lookup"><span data-stu-id="0fc19-114">Verify the configuration</span></span>
<span data-ttu-id="0fc19-115">To verify the successful configuration, use Ansible to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="0fc19-115">To verify the successful configuration, use Ansible to create a resource group.</span></span>

[!INCLUDE [create-resource-group-with-ansible.md](../../includes/ansible-create-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="0fc19-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fc19-116">Next steps</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0fc19-117">Create a basic virtual machine in Azure with Ansible</span><span class="sxs-lookup"><span data-stu-id="0fc19-117">Create a basic virtual machine in Azure with Ansible</span></span>](/azure/virtual-machines/linux/ansible-create-vm)