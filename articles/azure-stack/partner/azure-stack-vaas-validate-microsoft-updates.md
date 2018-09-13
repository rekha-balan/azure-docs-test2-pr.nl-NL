---
title: Validate software updates from Microsoft in Azure Stack validation as a service | Microsoft Docs
description: Learn how to validate software updates from Microsoft with validation as a service.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: 6ef8c0486a694ac44c53375b24893812b10343e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969270"
---
# <a name="validate-software-updates-from-microsoft"></a><span data-ttu-id="3069d-103">Validate software updates from Microsoft</span><span class="sxs-lookup"><span data-stu-id="3069d-103">Validate software updates from Microsoft</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="3069d-104">Microsoft will periodically release updates to the Azure Stack software.</span><span class="sxs-lookup"><span data-stu-id="3069d-104">Microsoft will periodically release updates to the Azure Stack software.</span></span> <span data-ttu-id="3069d-105">These updates are provided to Azure Stack co-engineering partners in advance of being made publicly available so that they can validate the updates against their solutions and provide feedback to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3069d-105">These updates are provided to Azure Stack co-engineering partners in advance of being made publicly available so that they can validate the updates against their solutions and provide feedback to Microsoft.</span></span>

## <a name="test-an-existing-solution"></a><span data-ttu-id="3069d-106">Test an existing solution</span><span class="sxs-lookup"><span data-stu-id="3069d-106">Test an existing solution</span></span>

1. <span data-ttu-id="3069d-107">Sign in to the [validation portal](https://azurestackvalidation.com).</span><span class="sxs-lookup"><span data-stu-id="3069d-107">Sign in to the [validation portal](https://azurestackvalidation.com).</span></span>

2. <span data-ttu-id="3069d-108">Select an existing solution where the updated from Microsoft has been deployed and select **Start** on the **Package Validation** tile.</span><span class="sxs-lookup"><span data-stu-id="3069d-108">Select an existing solution where the updated from Microsoft has been deployed and select **Start** on the **Package Validation** tile.</span></span>

    ![Package Validation](media/image3.png)

3. <span data-ttu-id="3069d-110">Enter the validation name.</span><span class="sxs-lookup"><span data-stu-id="3069d-110">Enter the validation name.</span></span>

4. <span data-ttu-id="3069d-111">Enter the URL to the OEM package that was installed on the solution at deployment time.</span><span class="sxs-lookup"><span data-stu-id="3069d-111">Enter the URL to the OEM package that was installed on the solution at deployment time.</span></span> <span data-ttu-id="3069d-112">Use the URL for the package stored on the Azure blob service.</span><span class="sxs-lookup"><span data-stu-id="3069d-112">Use the URL for the package stored on the Azure blob service.</span></span> <span data-ttu-id="3069d-113">For more information, see [Create an Azure storage blob to store logs](azure-stack-vaas-set-up-account.md#create-an-azure-storage-blob-to-store-logs).</span><span class="sxs-lookup"><span data-stu-id="3069d-113">For more information, see [Create an Azure storage blob to store logs](azure-stack-vaas-set-up-account.md#create-an-azure-storage-blob-to-store-logs).</span></span>

5. <span data-ttu-id="3069d-114">Select **Upload** to add your deployment configuration file.</span><span class="sxs-lookup"><span data-stu-id="3069d-114">Select **Upload** to add your deployment configuration file.</span></span> <span data-ttu-id="3069d-115">Refer to the [Validating a New Azure Stack Solution](azure-stack-vaas-validate-solution-new.md) for information on uploading your deployment configuration file.</span><span class="sxs-lookup"><span data-stu-id="3069d-115">Refer to the [Validating a New Azure Stack Solution](azure-stack-vaas-validate-solution-new.md) for information on uploading your deployment configuration file.</span></span>

6. <span data-ttu-id="3069d-116">The deployment configuration file must then be customized with the correct environment parameters file, see [Environment parameters](azure-stack-vaas-parameters.md#environment-parameters) for additional details.</span><span class="sxs-lookup"><span data-stu-id="3069d-116">The deployment configuration file must then be customized with the correct environment parameters file, see [Environment parameters](azure-stack-vaas-parameters.md#environment-parameters) for additional details.</span></span>

    > [!Note]   
    > <span data-ttu-id="3069d-117">The deployment configuration file can be further customized by adding common test parameters.</span><span class="sxs-lookup"><span data-stu-id="3069d-117">The deployment configuration file can be further customized by adding common test parameters.</span></span> <span data-ttu-id="3069d-118">For more information, see [Workflow common parameters for Azure Stack validation as a service](azure-stack-vaas-parameters.md)</span><span class="sxs-lookup"><span data-stu-id="3069d-118">For more information, see [Workflow common parameters for Azure Stack validation as a service](azure-stack-vaas-parameters.md)</span></span>

7. <span data-ttu-id="3069d-119">The user name and password for the tenant user, service admin, and cloud admin must be entered manually.</span><span class="sxs-lookup"><span data-stu-id="3069d-119">The user name and password for the tenant user, service admin, and cloud admin must be entered manually.</span></span>

8. <span data-ttu-id="3069d-120">Provide the URL to the Azure Storage blob to store the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="3069d-120">Provide the URL to the Azure Storage blob to store the diagnostic logs.</span></span> <span data-ttu-id="3069d-121">For more information, see [Create an Azure storage blob to store logs](azure-stack-vaas-set-up-account.md#create-an-azure-storage-blob-to-store-logs).</span><span class="sxs-lookup"><span data-stu-id="3069d-121">For more information, see [Create an Azure storage blob to store logs](azure-stack-vaas-set-up-account.md#create-an-azure-storage-blob-to-store-logs).</span></span>

    > [!Note]  
    > <span data-ttu-id="3069d-122">Descriptive tags may be entered to label the workflow.</span><span class="sxs-lookup"><span data-stu-id="3069d-122">Descriptive tags may be entered to label the workflow.</span></span>

10. <span data-ttu-id="3069d-123">Select **Submit** to save the workflow.</span><span class="sxs-lookup"><span data-stu-id="3069d-123">Select **Submit** to save the workflow.</span></span>

<span data-ttu-id="3069d-124">The solution workflow runs for approximately 24 hours.</span><span class="sxs-lookup"><span data-stu-id="3069d-124">The solution workflow runs for approximately 24 hours.</span></span> <span data-ttu-id="3069d-125">Add a link to or instruction on scheduling the tests.</span><span class="sxs-lookup"><span data-stu-id="3069d-125">Add a link to or instruction on scheduling the tests.</span></span> <span data-ttu-id="3069d-126">Clear in the tool.</span><span class="sxs-lookup"><span data-stu-id="3069d-126">Clear in the tool.</span></span>

<span data-ttu-id="3069d-127">Find more information on monitoring the progress of a validation run, see [Monitor a test ](azure-stack-vaas-monitor-test.md).</span><span class="sxs-lookup"><span data-stu-id="3069d-127">Find more information on monitoring the progress of a validation run, see [Monitor a test ](azure-stack-vaas-monitor-test.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3069d-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="3069d-128">Next steps</span></span>

- <span data-ttu-id="3069d-129">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="3069d-129">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
