---
title: Validate original equipment manufacturer (OEM) packages  in Azure Stack validation as a service | Microsoft Docs
description: Learn how to check original equipment manufacturer (OEM) packages with validation as a service.
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
ms.openlocfilehash: cefa32c35df4e87d4d2b983ee8c4a16dc065e774
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855909"
---
# <a name="validate-oem-packages"></a><span data-ttu-id="b89d2-103">Validate OEM packages</span><span class="sxs-lookup"><span data-stu-id="b89d2-103">Validate OEM packages</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="b89d2-104">You can test a new OEM package when there has been a change to the firmware or drivers for a completed solution validation.</span><span class="sxs-lookup"><span data-stu-id="b89d2-104">You can test a new OEM package when there has been a change to the firmware or drivers for a completed solution validation.</span></span> <span data-ttu-id="b89d2-105">When your package has passed the test, it is signed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b89d2-105">When your package has passed the test, it is signed by Microsoft.</span></span> <span data-ttu-id="b89d2-106">Your test must contain the updated OEM extension package with the drivers and firmware that have passed Windows Server logo and PCS tests.</span><span class="sxs-lookup"><span data-stu-id="b89d2-106">Your test must contain the updated OEM extension package with the drivers and firmware that have passed Windows Server logo and PCS tests.</span></span>

<span data-ttu-id="b89d2-107">All tests finish within 24 hours with result of **succeeded**.</span><span class="sxs-lookup"><span data-stu-id="b89d2-107">All tests finish within 24 hours with result of **succeeded**.</span></span> <span data-ttu-id="b89d2-108">If any of the tests have a result of **failed**, file a bug in [Microsoft Collaborate](https://aka.ms/collaborate) and notify Microsoft by sending an email to [vaashelp@microsoft.com](mailto:vaashelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b89d2-108">If any of the tests have a result of **failed**, file a bug in [Microsoft Collaborate](https://aka.ms/collaborate) and notify Microsoft by sending an email to [vaashelp@microsoft.com](mailto:vaashelp@microsoft.com).</span></span>

## <a name="get-your-oem-package-signed"></a><span data-ttu-id="b89d2-109">Get your OEM package signed</span><span class="sxs-lookup"><span data-stu-id="b89d2-109">Get your OEM package signed</span></span>

1. <span data-ttu-id="b89d2-110">Ensure that the current monthly update has been applied.</span><span class="sxs-lookup"><span data-stu-id="b89d2-110">Ensure that the current monthly update has been applied.</span></span> <span data-ttu-id="b89d2-111">For the latest version, see the most recent version in [Azure Stack Operator Documentation > Overview > Release notes](https://docs.microsoft.com/azure/azure-stack/) .</span><span class="sxs-lookup"><span data-stu-id="b89d2-111">For the latest version, see the most recent version in [Azure Stack Operator Documentation > Overview > Release notes](https://docs.microsoft.com/azure/azure-stack/) .</span></span>

    <span data-ttu-id="b89d2-112">Microsoft software updates to Azure Stack are designated using a naming convention, for example, 1803 indicating the update is for March 2018.</span><span class="sxs-lookup"><span data-stu-id="b89d2-112">Microsoft software updates to Azure Stack are designated using a naming convention, for example, 1803 indicating the update is for March 2018.</span></span> <span data-ttu-id="b89d2-113">For information about the Azure Stack update policy, cadence and release notes are available, see [Azure Stack servicing policy](https://docs.microsoft.com/azure/azure-stack/azure-stack-servicing-policy).</span><span class="sxs-lookup"><span data-stu-id="b89d2-113">For information about the Azure Stack update policy, cadence and release notes are available, see [Azure Stack servicing policy](https://docs.microsoft.com/azure/azure-stack/azure-stack-servicing-policy).</span></span>

1. <span data-ttu-id="b89d2-114">Check system health status by running **Test-AzureStack** as described in [Run a validation test for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b89d2-114">Check system health status by running **Test-AzureStack** as described in [Run a validation test for Azure Stack.</span></span> <span data-ttu-id="b89d2-115">Fix any warnings and errors before launching any tests.</span><span class="sxs-lookup"><span data-stu-id="b89d2-115">Fix any warnings and errors before launching any tests.</span></span>

2. <span data-ttu-id="b89d2-116">In the [validation portal](https://azurestackvalidation.com), select an existing solution.</span><span class="sxs-lookup"><span data-stu-id="b89d2-116">In the [validation portal](https://azurestackvalidation.com), select an existing solution.</span></span> <span data-ttu-id="b89d2-117">If you have not added your solution, see [Add a new solution](azure-stack-vaas-validate-solution-new.md#add-a-new-solution).</span><span class="sxs-lookup"><span data-stu-id="b89d2-117">If you have not added your solution, see [Add a new solution](azure-stack-vaas-validate-solution-new.md#add-a-new-solution).</span></span>

3. <span data-ttu-id="b89d2-118">Select **Start** on the **Package Validations** tile to start a new workflow.</span><span class="sxs-lookup"><span data-stu-id="b89d2-118">Select **Start** on the **Package Validations** tile to start a new workflow.</span></span>

    ![Package Validations](media/image3.png)

4.  <span data-ttu-id="b89d2-120">Provide a diagnostics connection string.</span><span class="sxs-lookup"><span data-stu-id="b89d2-120">Provide a diagnostics connection string.</span></span> <span data-ttu-id="b89d2-121">For instructions, see [Set up a storage account](azure-stack-vaas-set-up-account.md).</span><span class="sxs-lookup"><span data-stu-id="b89d2-121">For instructions, see [Set up a storage account](azure-stack-vaas-set-up-account.md).</span></span>

    <span data-ttu-id="b89d2-122">An OEM Extension package must be specified for every Package Validation run.</span><span class="sxs-lookup"><span data-stu-id="b89d2-122">An OEM Extension package must be specified for every Package Validation run.</span></span> <span data-ttu-id="b89d2-123">Specify the OEM package that was installed on the solution at the time of Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="b89d2-123">Specify the OEM package that was installed on the solution at the time of Azure Stack deployment.</span></span> <span data-ttu-id="b89d2-124">For instructions, see [Create an Azure storage blob to store logs](azure-stack-vaas-set-up-account.md#create-an-azure-storage-blob-to-store-logs).</span><span class="sxs-lookup"><span data-stu-id="b89d2-124">For instructions, see [Create an Azure storage blob to store logs](azure-stack-vaas-set-up-account.md#create-an-azure-storage-blob-to-store-logs).</span></span>

    <span data-ttu-id="b89d2-125">A JSON file with the environment variables must be used to finish the input for required fields for the run to avoid mistakes in data entry.</span><span class="sxs-lookup"><span data-stu-id="b89d2-125">A JSON file with the environment variables must be used to finish the input for required fields for the run to avoid mistakes in data entry.</span></span> <span data-ttu-id="b89d2-126">For instructions, see [Get a configuration file in an Azure Stack deployment](azure-stack-vaas-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="b89d2-126">For instructions, see [Get a configuration file in an Azure Stack deployment](azure-stack-vaas-parameters.md).</span></span>

5. <span data-ttu-id="b89d2-127">Run the tests.</span><span class="sxs-lookup"><span data-stu-id="b89d2-127">Run the tests.</span></span>

6. <span data-ttu-id="b89d2-128">When all tests have successfully completed, send the name of your Solution and package validation to [vaashelp@microsoft.com](mailto:vaashelp@microsoft.com) to request package signing.</span><span class="sxs-lookup"><span data-stu-id="b89d2-128">When all tests have successfully completed, send the name of your Solution and package validation to [vaashelp@microsoft.com](mailto:vaashelp@microsoft.com) to request package signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b89d2-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="b89d2-129">Next steps</span></span>

- <span data-ttu-id="b89d2-130">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="b89d2-130">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
