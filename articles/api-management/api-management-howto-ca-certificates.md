---
title: Add a custom CA certificate - Azure API Management | Microsoft Docs
description: Learn how to add a custom CA certificate in Azure API Management.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/20/2018
ms.author: apimpm
ms.openlocfilehash: 9d3399ba6ee724d91117486744ad1431f53edbce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967610"
---
# <a name="how-to-add-a-custom-ca-certificate-in-azure-api-management"></a><span data-ttu-id="b17a4-103">How to add a custom CA certificate in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="b17a4-103">How to add a custom CA certificate in Azure API Management</span></span>

<span data-ttu-id="b17a4-104">Azure API Management allows installing CA certificates on the machine inside the trusted root and intermediate certificate stores.</span><span class="sxs-lookup"><span data-stu-id="b17a4-104">Azure API Management allows installing CA certificates on the machine inside the trusted root and intermediate certificate stores.</span></span> <span data-ttu-id="b17a4-105">This functionality should be used if your services require a custom CA certificate.</span><span class="sxs-lookup"><span data-stu-id="b17a4-105">This functionality should be used if your services require a custom CA certificate.</span></span>

<span data-ttu-id="b17a4-106">The article shows how to manage CA certificates of an Azure API Management service instance in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b17a4-106">The article shows how to manage CA certificates of an Azure API Management service instance in the Azure portal.</span></span>

## <span data-ttu-id="b17a4-107"><a name="step1"> </a>Upload a CA certificate</span><span class="sxs-lookup"><span data-stu-id="b17a4-107"><a name="step1"> </a>Upload a CA certificate</span></span>

![Add CA certificates](media/api-management-howto-ca-certificates/00.png)

<span data-ttu-id="b17a4-109">Follow the steps below to upload a new CA certificate.</span><span class="sxs-lookup"><span data-stu-id="b17a4-109">Follow the steps below to upload a new CA certificate.</span></span> <span data-ttu-id="b17a4-110">If you have not created an API Management service instance yet, see the tutorial [Create an API Management service instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="b17a4-110">If you have not created an API Management service instance yet, see the tutorial [Create an API Management service instance](get-started-create-service-instance.md).</span></span>

1. <span data-ttu-id="b17a4-111">Navigate to your Azure API Management service instance in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b17a4-111">Navigate to your Azure API Management service instance in the Azure portal.</span></span>

2. <span data-ttu-id="b17a4-112">Select **CA certificates** from the menu.</span><span class="sxs-lookup"><span data-stu-id="b17a4-112">Select **CA certificates** from the menu.</span></span>

3. <span data-ttu-id="b17a4-113">Click the **+ Add** button.</span><span class="sxs-lookup"><span data-stu-id="b17a4-113">Click the **+ Add** button.</span></span>  

    ![Add CA certificates](media/api-management-howto-ca-certificates/01.png)  

4. <span data-ttu-id="b17a4-115">Browse for the certificate and decide on the certificate store.</span><span class="sxs-lookup"><span data-stu-id="b17a4-115">Browse for the certificate and decide on the certificate store.</span></span> <span data-ttu-id="b17a4-116">Only the public key is needed, so the password is not required.</span><span class="sxs-lookup"><span data-stu-id="b17a4-116">Only the public key is needed, so the password is not required.</span></span>

    ![Add CA certificates](media/api-management-howto-ca-certificates/02.png)  

5. <span data-ttu-id="b17a4-118">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b17a4-118">Click **Save**.</span></span> <span data-ttu-id="b17a4-119">This operation may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="b17a4-119">This operation may take a few minutes.</span></span>

    ![Add CA certificates](media/api-management-howto-ca-certificates/03.png)  

> [!NOTE]
> <span data-ttu-id="b17a4-121">You can upload a CA certificate using the `New-AzureRmApiManagementSystemCertificate` Powershell command.</span><span class="sxs-lookup"><span data-stu-id="b17a4-121">You can upload a CA certificate using the `New-AzureRmApiManagementSystemCertificate` Powershell command.</span></span>

## <span data-ttu-id="b17a4-122"><a name="step1a"> </a>Delete a client certificate</span><span class="sxs-lookup"><span data-stu-id="b17a4-122"><a name="step1a"> </a>Delete a client certificate</span></span>

<span data-ttu-id="b17a4-123">To delete a certificate, click context menu **...** and select **Delete** beside the certificate.</span><span class="sxs-lookup"><span data-stu-id="b17a4-123">To delete a certificate, click context menu **...** and select **Delete** beside the certificate.</span></span>

![Delete CA certificates](media/api-management-howto-ca-certificates/04.png)  

[Upload a CA certificate]: #step1
[Delete a CA certificate]: #step1a