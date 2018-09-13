---
title: Use Azure CLI to create an Azure AD app and configure it to access Azure Media Services API | Microsoft Docs
description: This topic shows how to use the Azure CLI to create an Azure AD app and configure it to access Azure Media Services API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: fcd0ea10bd39f9e7252e114e8d6401a4fe0ecadb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865952"
---
# <a name="use-azure-cli-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a><span data-ttu-id="a3326-103">Use Azure CLI to create an AAD app and configure it to access Azure Media Services API</span><span class="sxs-lookup"><span data-stu-id="a3326-103">Use Azure CLI to create an AAD app and configure it to access Azure Media Services API</span></span>

<span data-ttu-id="a3326-104">This topic shows you how to use the Azure CLI to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span><span class="sxs-lookup"><span data-stu-id="a3326-104">This topic shows you how to use the Azure CLI to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a3326-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3326-105">Prerequisites</span></span>

- <span data-ttu-id="a3326-106">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="a3326-106">An Azure account.</span></span> <span data-ttu-id="a3326-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3326-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="a3326-108">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="a3326-108">A Media Services account.</span></span> <span data-ttu-id="a3326-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a3326-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="a3326-110">Use the Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a3326-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="a3326-111">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a3326-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a3326-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span><span class="sxs-lookup"><span data-stu-id="a3326-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="a3326-114">For more information, see [Overview of Azure Cloud Shell](../../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3326-114">For more information, see [Overview of Azure Cloud Shell](../../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-azure-cli"></a><span data-ttu-id="a3326-115">Create an Azure AD app and configure access to the media account with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a3326-115">Create an Azure AD app and configure access to the media account with Azure CLI</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create --assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="a3326-116">For example:</span><span class="sxs-lookup"><span data-stu-id="a3326-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="a3326-117">In this example, the **scope** is the full resource path for the media services account.</span><span class="sxs-lookup"><span data-stu-id="a3326-117">In this example, the **scope** is the full resource path for the media services account.</span></span> <span data-ttu-id="a3326-118">However, the **scope** can be at any level.</span><span class="sxs-lookup"><span data-stu-id="a3326-118">However, the **scope** can be at any level.</span></span>

<span data-ttu-id="a3326-119">For example, it could be one of the following levels:</span><span class="sxs-lookup"><span data-stu-id="a3326-119">For example, it could be one of the following levels:</span></span>
 
* <span data-ttu-id="a3326-120">The **subscription** level.</span><span class="sxs-lookup"><span data-stu-id="a3326-120">The **subscription** level.</span></span>
* <span data-ttu-id="a3326-121">The **resource group** level.</span><span class="sxs-lookup"><span data-stu-id="a3326-121">The **resource group** level.</span></span>
* <span data-ttu-id="a3326-122">The **resource** level (for example, a Media account).</span><span class="sxs-lookup"><span data-stu-id="a3326-122">The **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="a3326-123">For more information, see [Create an Azure service principal with the Azure CLI](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="a3326-123">For more information, see [Create an Azure service principal with the Azure CLI](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="a3326-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../../role-based-access-control/role-assignments-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a3326-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../../role-based-access-control/role-assignments-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3326-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3326-125">Next steps</span></span>

<span data-ttu-id="a3326-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="a3326-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
