---
title: include file
description: include file
services: media-services
author: Juliako
ms.service: media-services
ms.topic: include
ms.date: 04/13/2018
ms.author: juliako
ms.custom: include file
ms.openlocfilehash: 9ecb07a2cb278f6cde4ffdc3b252cb9e816d08da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45397005"
---
## <a name="create-a-media-services-account"></a><span data-ttu-id="507e4-103">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="507e4-103">Create a Media Services account</span></span>

<span data-ttu-id="507e4-104">You first need to create a Media Services account.</span><span class="sxs-lookup"><span data-stu-id="507e4-104">You first need to create a Media Services account.</span></span> <span data-ttu-id="507e4-105">This section shows what you need for the acount creation using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="507e4-105">This section shows what you need for the acount creation using the Azure CLI.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="507e4-106">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="507e4-106">Create a resource group</span></span>

<span data-ttu-id="507e4-107">Create a resource group using the following command.</span><span class="sxs-lookup"><span data-stu-id="507e4-107">Create a resource group using the following command.</span></span> <span data-ttu-id="507e4-108">An Azure resource group is a logical container into which resources like Azure Media Services accounts and the associated Storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="507e4-108">An Azure resource group is a logical container into which resources like Azure Media Services accounts and the associated Storage accounts are deployed and managed.</span></span>

```azurecli-interactive
az group create --name amsResourceGroup --location westus2
```

### <a name="create-a-storage-account"></a><span data-ttu-id="507e4-109">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="507e4-109">Create a storage account</span></span>

<span data-ttu-id="507e4-110">When creating a Media Services account, you need to supply the name of an Azure Storage account resource.</span><span class="sxs-lookup"><span data-stu-id="507e4-110">When creating a Media Services account, you need to supply the name of an Azure Storage account resource.</span></span> <span data-ttu-id="507e4-111">The specified storage account is attached to your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="507e4-111">The specified storage account is attached to your Media Services account.</span></span> 

<span data-ttu-id="507e4-112">You must have one **Primary** storage account and you can have  any number of **Secondary** storage accounts associated with your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="507e4-112">You must have one **Primary** storage account and you can have  any number of **Secondary** storage accounts associated with your Media Services account.</span></span> <span data-ttu-id="507e4-113">Media Services supports **General-purpose v2** (GPv2) or **General-purpose v1** (GPv1) accounts.</span><span class="sxs-lookup"><span data-stu-id="507e4-113">Media Services supports **General-purpose v2** (GPv2) or **General-purpose v1** (GPv1) accounts.</span></span> <span data-ttu-id="507e4-114">Blob only accounts are not allowed as **Primary**.</span><span class="sxs-lookup"><span data-stu-id="507e4-114">Blob only accounts are not allowed as **Primary**.</span></span> <span data-ttu-id="507e4-115">If you want to learn more about storage accounts, see [Azure Storage account options](../articles/storage/common/storage-account-options.md).</span><span class="sxs-lookup"><span data-stu-id="507e4-115">If you want to learn more about storage accounts, see [Azure Storage account options](../articles/storage/common/storage-account-options.md).</span></span> 

<span data-ttu-id="507e4-116">For more information about how storage accounts are used in Media Services, see [Storage accounts](../articles/media-services/latest/storage-account-concept.md).</span><span class="sxs-lookup"><span data-stu-id="507e4-116">For more information about how storage accounts are used in Media Services, see [Storage accounts](../articles/media-services/latest/storage-account-concept.md).</span></span>

<span data-ttu-id="507e4-117">The following command creates a Storage account that is going to be associated with the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="507e4-117">The following command creates a Storage account that is going to be associated with the Media Services account.</span></span> <span data-ttu-id="507e4-118">In the script below, you can substitute `storageaccountforams` with your value.</span><span class="sxs-lookup"><span data-stu-id="507e4-118">In the script below, you can substitute `storageaccountforams` with your value.</span></span> <span data-ttu-id="507e4-119">The account name must have length less than 24.</span><span class="sxs-lookup"><span data-stu-id="507e4-119">The account name must have length less than 24.</span></span>

```azurecli-interactive
az storage account create --name storageaccountforams \  
--kind StorageV2 \
--sku Standard_RAGRS \
--resource-group amsResourceGroup
```

### <a name="create-a-media-services-account"></a><span data-ttu-id="507e4-120">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="507e4-120">Create a Media Services account</span></span>

<span data-ttu-id="507e4-121">The following Azure CLI command creates a new Media Services account.</span><span class="sxs-lookup"><span data-stu-id="507e4-121">The following Azure CLI command creates a new Media Services account.</span></span> <span data-ttu-id="507e4-122">You can replace the following values: `amsaccount`  `storageaccountforams` (must match the value you gave for your storage account), and `amsResourceGroup` (must match the value you gave for the resource group).</span><span class="sxs-lookup"><span data-stu-id="507e4-122">You can replace the following values: `amsaccount`  `storageaccountforams` (must match the value you gave for your storage account), and `amsResourceGroup` (must match the value you gave for the resource group).</span></span>

```azurecli-interactive
az ams account create --name amsaccount --resource-group amsResourceGroup --storage-account storageaccountforams
```
