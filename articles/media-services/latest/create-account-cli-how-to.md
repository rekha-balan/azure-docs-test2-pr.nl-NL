---
title: Create an Azure Media Services account with the Azure CLI | Microsoft Docs
description: Follow the steps of this quickstart to create an Azure Media Services account.
services: media-services
documentationcenter: ''
author: Juliako
manager: cflower
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.custom: ''
ms.date: 03/27/2018
ms.author: juliako
ms.openlocfilehash: ca01f32709ce7c9fc49629415cd8697a9d9ba43a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864658"
---
# <a name="create-an-azure-media-services-account"></a><span data-ttu-id="09bc2-103">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="09bc2-103">Create an Azure Media Services account</span></span>

<span data-ttu-id="09bc2-104">To start encrypting, encoding, analyzing, managing, and streaming media content in Azure, you need to create a Media Services account.</span><span class="sxs-lookup"><span data-stu-id="09bc2-104">To start encrypting, encoding, analyzing, managing, and streaming media content in Azure, you need to create a Media Services account.</span></span> <span data-ttu-id="09bc2-105">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="09bc2-105">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span></span>

<span data-ttu-id="09bc2-106">This topic describes steps for creating a new Azure Media Services account using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="09bc2-106">This topic describes steps for creating a new Azure Media Services account using the Azure CLI.</span></span>  

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="09bc2-107">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="09bc2-107">Log in to Azure</span></span>

<span data-ttu-id="09bc2-108">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span><span class="sxs-lookup"><span data-stu-id="09bc2-108">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="09bc2-109">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="09bc2-109">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="09bc2-110">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="09bc2-110">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="09bc2-111">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="09bc2-111">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span></span> 

## <a name="set-the-azure-subscription"></a><span data-ttu-id="09bc2-112">Set the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="09bc2-112">Set the Azure subscription</span></span>

<span data-ttu-id="09bc2-113">In the following command, provide the Azure subscription ID that you want to use for the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="09bc2-113">In the following command, provide the Azure subscription ID that you want to use for the Media Services account.</span></span> <span data-ttu-id="09bc2-114">You can see a list of subscriptions that you have access to by navigating to [Subscriptions](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="09bc2-114">You can see a list of subscriptions that you have access to by navigating to [Subscriptions](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

```azurecli-interactive
az account set --subscription mySubscriptionId
```
 
[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]
 
## <a name="next-steps"></a><span data-ttu-id="09bc2-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="09bc2-115">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09bc2-116">Stream a file</span><span class="sxs-lookup"><span data-stu-id="09bc2-116">Stream a file</span></span>](stream-files-dotnet-quickstart.md)
