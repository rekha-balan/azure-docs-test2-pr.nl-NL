---
title: Quickstart - Create an Azure Media Services account with Azure CLI| Microsoft Docs
description: Follow the steps of this quickstart to create an Azure Media Services account.
services: media-services
documentationcenter: ''
author: Juliako
manager: cflower
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: quickstart
ms.custom: mvc
ms.date: 03/27/2018
ms.author: juliako
ms.openlocfilehash: 9168a66c3afcd8dd0b05de15f5833c516ddb2250
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870430"
---
# <a name="quickstart-create-an-azure-media-services-account"></a><span data-ttu-id="00cf8-103">Quickstart: Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="00cf8-103">Quickstart: Create an Azure Media Services account</span></span>

> [!NOTE]
> <span data-ttu-id="00cf8-104">The latest version of Azure Media Services (2018-03-30) is in preview.</span><span class="sxs-lookup"><span data-stu-id="00cf8-104">The latest version of Azure Media Services (2018-03-30) is in preview.</span></span> <span data-ttu-id="00cf8-105">This version is also called v3.</span><span class="sxs-lookup"><span data-stu-id="00cf8-105">This version is also called v3.</span></span> 

<span data-ttu-id="00cf8-106">Whether you are a developer or a media content creator, to store, encrypt, encode, manage, and stream media content in Azure, you need to create a Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-106">Whether you are a developer or a media content creator, to store, encrypt, encode, manage, and stream media content in Azure, you need to create a Media Services account.</span></span> <span data-ttu-id="00cf8-107">When creating a Media Services account, you need to supply the ID of an Azure Storage account resource.</span><span class="sxs-lookup"><span data-stu-id="00cf8-107">When creating a Media Services account, you need to supply the ID of an Azure Storage account resource.</span></span> <span data-ttu-id="00cf8-108">The specified storage account is attached to your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-108">The specified storage account is attached to your Media Services account.</span></span> <span data-ttu-id="00cf8-109">This storage account resource has to be located in the same geographic region as the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-109">This storage account resource has to be located in the same geographic region as the Media Services account.</span></span>  

<span data-ttu-id="00cf8-110">This quickstart describes steps for creating a new Azure Media Services account using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="00cf8-110">This quickstart describes steps for creating a new Azure Media Services account using the Azure CLI.</span></span>  

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="00cf8-111">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="00cf8-111">Log in to Azure</span></span>

<span data-ttu-id="00cf8-112">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span><span class="sxs-lookup"><span data-stu-id="00cf8-112">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="00cf8-113">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="00cf8-113">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="00cf8-114">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="00cf8-114">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="00cf8-115">If you need to install or upgrade, see [Install the Azure CLI]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="00cf8-115">If you need to install or upgrade, see [Install the Azure CLI]( /cli/azure/install-azure-cli).</span></span> 

## <a name="set-the-azure-subscription"></a><span data-ttu-id="00cf8-116">Set the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="00cf8-116">Set the Azure subscription</span></span>

<span data-ttu-id="00cf8-117">In the following command, provide the Azure subscription ID that you want to use for the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-117">In the following command, provide the Azure subscription ID that you want to use for the Media Services account.</span></span> <span data-ttu-id="00cf8-118">You can see a list of subscriptions that you have access to by navigating to [Subscriptions](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="00cf8-118">You can see a list of subscriptions that you have access to by navigating to [Subscriptions](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

```azurecli-interactive
az account set --subscription <mySubscriptionId>
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="00cf8-119">Create an Azure Resource Group</span><span class="sxs-lookup"><span data-stu-id="00cf8-119">Create an Azure Resource Group</span></span>

<span data-ttu-id="00cf8-120">The following command creates a resource group in which you want to have the Storage and Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-120">The following command creates a resource group in which you want to have the Storage and Media Services account.</span></span> <span data-ttu-id="00cf8-121">Substitute the *myresourcegroup* placeholder with the name you want to use for your resource group.</span><span class="sxs-lookup"><span data-stu-id="00cf8-121">Substitute the *myresourcegroup* placeholder with the name you want to use for your resource group.</span></span>

```azurecli-interactive
az group create -n <myresourcegroup> -l westus2
```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="00cf8-122">Create an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="00cf8-122">Create an Azure Storage account</span></span>

<span data-ttu-id="00cf8-123">When creating a Media Services account, you need to supply the ID of an Azure Storage account resource.</span><span class="sxs-lookup"><span data-stu-id="00cf8-123">When creating a Media Services account, you need to supply the ID of an Azure Storage account resource.</span></span> <span data-ttu-id="00cf8-124">The specified storage account is attached to your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-124">The specified storage account is attached to your Media Services account.</span></span> 

<span data-ttu-id="00cf8-125">You must have one **Primary** storage account and you can have  any number of **Secondary** storage accounts associated with your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-125">You must have one **Primary** storage account and you can have  any number of **Secondary** storage accounts associated with your Media Services account.</span></span> <span data-ttu-id="00cf8-126">Media Services supports **General-purpose v2** (GPv2) or **General-purpose v1** (GPv1) accounts.</span><span class="sxs-lookup"><span data-stu-id="00cf8-126">Media Services supports **General-purpose v2** (GPv2) or **General-purpose v1** (GPv1) accounts.</span></span> <span data-ttu-id="00cf8-127">Blob only accounts are not allowed as **Primary**.</span><span class="sxs-lookup"><span data-stu-id="00cf8-127">Blob only accounts are not allowed as **Primary**.</span></span> <span data-ttu-id="00cf8-128">If you want to learn more about storage accounts, see [Azure Storage account options](../../storage/common/storage-account-options.md).</span><span class="sxs-lookup"><span data-stu-id="00cf8-128">If you want to learn more about storage accounts, see [Azure Storage account options](../../storage/common/storage-account-options.md).</span></span> 

<span data-ttu-id="00cf8-129">The following command creates the Storage account that is going to be associated with the Media Services Account (primary).</span><span class="sxs-lookup"><span data-stu-id="00cf8-129">The following command creates the Storage account that is going to be associated with the Media Services Account (primary).</span></span> <span data-ttu-id="00cf8-130">In the script below, substitute the *storageaccountforams* placeholder.</span><span class="sxs-lookup"><span data-stu-id="00cf8-130">In the script below, substitute the *storageaccountforams* placeholder.</span></span> <span data-ttu-id="00cf8-131">Ther 'account_name' must have length less than 24.</span><span class="sxs-lookup"><span data-stu-id="00cf8-131">Ther 'account_name' must have length less than 24.</span></span>

```azurecli-interactive
az storage account create -n <storageaccountforams> -g <myresourcegroup>
```

## <a name="create-an-azure-media-services-account"></a><span data-ttu-id="00cf8-132">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="00cf8-132">Create an Azure Media Services account</span></span>

<span data-ttu-id="00cf8-133">Below you can find the Azure CLI commands that creates a new Media Services account.</span><span class="sxs-lookup"><span data-stu-id="00cf8-133">Below you can find the Azure CLI commands that creates a new Media Services account.</span></span> <span data-ttu-id="00cf8-134">You just need to replace the following highlighted values:</span><span class="sxs-lookup"><span data-stu-id="00cf8-134">You just need to replace the following highlighted values:</span></span>

* <span data-ttu-id="00cf8-135">*myamsaccountname*</span><span class="sxs-lookup"><span data-stu-id="00cf8-135">*myamsaccountname*</span></span>
* <span data-ttu-id="00cf8-136">*myresourcegroup*</span><span class="sxs-lookup"><span data-stu-id="00cf8-136">*myresourcegroup*</span></span>
* <span data-ttu-id="00cf8-137">*storageaccountforams*</span><span class="sxs-lookup"><span data-stu-id="00cf8-137">*storageaccountforams*</span></span>

```azurecli-interactive
az ams create -n <myamsaccountname> -g <myresourcegroup> --storage-account <storageaccountforams>
```

## <a name="clean-up-resources"></a><span data-ttu-id="00cf8-138">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="00cf8-138">Clean up resources</span></span>

<span data-ttu-id="00cf8-139">If you no longer need any of the resources in your resource group, including the Media Services account you created in this Quickstart, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="00cf8-139">If you no longer need any of the resources in your resource group, including the Media Services account you created in this Quickstart, delete the resource group.</span></span>

<span data-ttu-id="00cf8-140">In the **CloudShell**, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="00cf8-140">In the **CloudShell**, execute the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="00cf8-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="00cf8-141">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00cf8-142">Stream a file</span><span class="sxs-lookup"><span data-stu-id="00cf8-142">Stream a file</span></span>](stream-files-dotnet-quickstart.md)
