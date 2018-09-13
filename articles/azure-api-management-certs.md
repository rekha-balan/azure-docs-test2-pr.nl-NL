---
title: Upload an Azure Management API Certificate | Microsoft Docs
description: Learn how to upload athe Management API certficate for the Azure Classic Portal.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: ''
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2016
ms.author: adegeo
ms.openlocfilehash: 7fcd383b25c54a7ddb9a45dabb45128523002010
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551647"
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="8de36-103">Upload an Azure Management API Management Certificate</span><span class="sxs-lookup"><span data-stu-id="8de36-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="8de36-104">Management certificates allow you to authenticate with the Service Management API provided by Azure.</span><span class="sxs-lookup"><span data-stu-id="8de36-104">Management certificates allow you to authenticate with the Service Management API provided by Azure.</span></span> <span data-ttu-id="8de36-105">Many programs and tools (such as Visual Studio or the Azure SDK) will use these certficates to automate configuration and deployment of various Azure services.</span><span class="sxs-lookup"><span data-stu-id="8de36-105">Many programs and tools (such as Visual Studio or the Azure SDK) will use these certficates to automate configuration and deployment of various Azure services.</span></span> <span data-ttu-id="8de36-106">**This only applies to the Azure classic portal**.</span><span class="sxs-lookup"><span data-stu-id="8de36-106">**This only applies to the Azure classic portal**.</span></span>

> [!WARNING]
> <span data-ttu-id="8de36-107">Be careful!</span><span class="sxs-lookup"><span data-stu-id="8de36-107">Be careful!</span></span> <span data-ttu-id="8de36-108">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span><span class="sxs-lookup"><span data-stu-id="8de36-108">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="8de36-109">More information about Azure certificates (including creating a self-signed certificate) is [available](cloud-services/cloud-services-certs-create.md#what-are-management-certificates) to you if you need it.</span><span class="sxs-lookup"><span data-stu-id="8de36-109">More information about Azure certificates (including creating a self-signed certificate) is [available](cloud-services/cloud-services-certs-create.md#what-are-management-certificates) to you if you need it.</span></span>

<span data-ttu-id="8de36-110">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span><span class="sxs-lookup"><span data-stu-id="8de36-110">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="8de36-111">Upload a management certificate</span><span class="sxs-lookup"><span data-stu-id="8de36-111">Upload a management certificate</span></span>
<span data-ttu-id="8de36-112">Once you have a management certficate created, (.cer file with only the public key) you can upload it into the portal.</span><span class="sxs-lookup"><span data-stu-id="8de36-112">Once you have a management certficate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="8de36-113">When the certificate is available in the portal, anyone with a matching certficiate (private key) can connect through the Management API and access the resources for the associated subscription.</span><span class="sxs-lookup"><span data-stu-id="8de36-113">When the certificate is available in the portal, anyone with a matching certficiate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="8de36-114">Log into the [Azure classic portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8de36-114">Log into the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8de36-115">Make sure to select the correct subscription that you want to associate a certificate with.</span><span class="sxs-lookup"><span data-stu-id="8de36-115">Make sure to select the correct subscription that you want to associate a certificate with.</span></span> <span data-ttu-id="8de36-116">Press the **Subscriptions** text at the top-right of the portal.</span><span class="sxs-lookup"><span data-stu-id="8de36-116">Press the **Subscriptions** text at the top-right of the portal.</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/subscription.png)
3. <span data-ttu-id="8de36-118">After you have the correct subscription selected, press **Settings** on the left side of the portal (you may need to scroll down).</span><span class="sxs-lookup"><span data-stu-id="8de36-118">After you have the correct subscription selected, press **Settings** on the left side of the portal (you may need to scroll down).</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/settings.png)
4. <span data-ttu-id="8de36-120">Press the **Management Certificates** tab.</span><span class="sxs-lookup"><span data-stu-id="8de36-120">Press the **Management Certificates** tab.</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/certificates-tab.png)
5. <span data-ttu-id="8de36-122">Press the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="8de36-122">Press the **Upload** button.</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/upload.png)
6. <span data-ttu-id="8de36-124">Fill out the dialog information and press the done **Checkmark**.</span><span class="sxs-lookup"><span data-stu-id="8de36-124">Fill out the dialog information and press the done **Checkmark**.</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/upload-dialog.png)

## <a name="next-steps"></a><span data-ttu-id="8de36-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="8de36-126">Next steps</span></span>
<span data-ttu-id="8de36-127">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [Service Management REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span><span class="sxs-lookup"><span data-stu-id="8de36-127">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [Service Management REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>





