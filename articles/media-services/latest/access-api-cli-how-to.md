---
title: Access the Azure Media Services API - Azure CLI | Microsoft Docs
description: Follow the steps of this how-to to access the Azure Media Services API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cflower
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.custom: mvc
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: e20cac5f1063589bdbfee0f384ac6af5a39811ed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857131"
---
# <a name="access-azure-media-services-api-with-the-azure-cli"></a><span data-ttu-id="68ae1-103">Access Azure Media Services API with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68ae1-103">Access Azure Media Services API with the Azure CLI</span></span>
 
<span data-ttu-id="68ae1-104">You should use the Azure AD service principal authentication to connect to the Azure Media Services API.</span><span class="sxs-lookup"><span data-stu-id="68ae1-104">You should use the Azure AD service principal authentication to connect to the Azure Media Services API.</span></span> <span data-ttu-id="68ae1-105">Your application needs to request an Azure AD token that has the following parameters:</span><span class="sxs-lookup"><span data-stu-id="68ae1-105">Your application needs to request an Azure AD token that has the following parameters:</span></span>

* <span data-ttu-id="68ae1-106">Azure AD tenant endpoint</span><span class="sxs-lookup"><span data-stu-id="68ae1-106">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="68ae1-107">Media Services resource URI</span><span class="sxs-lookup"><span data-stu-id="68ae1-107">Media Services resource URI</span></span>
* <span data-ttu-id="68ae1-108">Resource URI for REST Media Services</span><span class="sxs-lookup"><span data-stu-id="68ae1-108">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="68ae1-109">Azure AD application values: the client ID and client secret</span><span class="sxs-lookup"><span data-stu-id="68ae1-109">Azure AD application values: the client ID and client secret</span></span>

<span data-ttu-id="68ae1-110">This article shows you how to use the Azure CLI to create an Azure AD application and service principal and get the values that are needed to access Azure Media Services resources.</span><span class="sxs-lookup"><span data-stu-id="68ae1-110">This article shows you how to use the Azure CLI to create an Azure AD application and service principal and get the values that are needed to access Azure Media Services resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68ae1-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="68ae1-111">Prerequisites</span></span> 

<span data-ttu-id="68ae1-112">Create a new Azure Media Services account, as described in [this quickstart](create-account-cli-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="68ae1-112">Create a new Azure Media Services account, as described in [this quickstart](create-account-cli-quickstart.md).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="68ae1-113">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="68ae1-113">Log in to Azure</span></span>

<span data-ttu-id="68ae1-114">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span><span class="sxs-lookup"><span data-stu-id="68ae1-114">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="68ae1-115">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="68ae1-115">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="68ae1-116">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="68ae1-116">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="68ae1-117">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="68ae1-117">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="next-steps"></a><span data-ttu-id="68ae1-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="68ae1-118">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="68ae1-119">Stream a file</span><span class="sxs-lookup"><span data-stu-id="68ae1-119">Stream a file</span></span>](stream-files-dotnet-quickstart.md)

## <a name="see-also"></a><span data-ttu-id="68ae1-120">See also</span><span class="sxs-lookup"><span data-stu-id="68ae1-120">See also</span></span>

[<span data-ttu-id="68ae1-121">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68ae1-121">Azure CLI</span></span>](https://docs.microsoft.com/en-us/cli/azure/ams?view=azure-cli-latest)
