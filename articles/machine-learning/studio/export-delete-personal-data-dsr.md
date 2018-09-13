---
title: Export and delete your data from Machine Learning Studio - Azure | Microsoft Docs
description: In-product data stored by Azure Machine Learning Studio is available for export and deletion through the Azure portal and also through authenticated REST APIs. Telemetry data can be accessed through the Azure Privacy Portal. This article shows you how.
services: machine-learning
author: heatherbshapiro
ms.author: hshapiro
manager: cgronlun
ms.reviewer: jmartens, mldocs
ms.service: machine-learning
ms.component: studio
ms.topic: conceptual
ms.date: 05/25/2018
ms.openlocfilehash: 2ebd777a9723732de6ebbdf07020802190cb4b61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856604"
---
# <a name="export-and-delete-in-product-user-data-from-machine-learning-studio"></a><span data-ttu-id="b5c92-105">Export and delete in-product user data from Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b5c92-105">Export and delete in-product user data from Machine Learning Studio</span></span>

<span data-ttu-id="b5c92-106">You can delete or export in-product data stored by Azure Machine Learning Studio by using the Azure portal, the Studio interface, PowerShell, and authenticated REST APIs.</span><span class="sxs-lookup"><span data-stu-id="b5c92-106">You can delete or export in-product data stored by Azure Machine Learning Studio by using the Azure portal, the Studio interface, PowerShell, and authenticated REST APIs.</span></span> <span data-ttu-id="b5c92-107">This article tells you how.</span><span class="sxs-lookup"><span data-stu-id="b5c92-107">This article tells you how.</span></span> 

<span data-ttu-id="b5c92-108">Telemetry data can be accessed through the Azure Privacy portal.</span><span class="sxs-lookup"><span data-stu-id="b5c92-108">Telemetry data can be accessed through the Azure Privacy portal.</span></span> 

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-dsr-and-stp-note.md)]

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

## <a name="what-kinds-of-user-data-does-studio-collect"></a><span data-ttu-id="b5c92-109">What kinds of user data does Studio collect?</span><span class="sxs-lookup"><span data-stu-id="b5c92-109">What kinds of user data does Studio collect?</span></span>

<span data-ttu-id="b5c92-110">For this service, user data consists of information about users authorized to access workspaces and telemetry records of user interactions with the service.</span><span class="sxs-lookup"><span data-stu-id="b5c92-110">For this service, user data consists of information about users authorized to access workspaces and telemetry records of user interactions with the service.</span></span>

<span data-ttu-id="b5c92-111">There are two kinds of user data in Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="b5c92-111">There are two kinds of user data in Machine Learning Studio:</span></span>
- <span data-ttu-id="b5c92-112">**Personal account data:** Account IDs and email addresses associated with an account.</span><span class="sxs-lookup"><span data-stu-id="b5c92-112">**Personal account data:** Account IDs and email addresses associated with an account.</span></span>
- <span data-ttu-id="b5c92-113">**Customer data:** Data you uploaded to analyze.</span><span class="sxs-lookup"><span data-stu-id="b5c92-113">**Customer data:** Data you uploaded to analyze.</span></span>

## <a name="studio-account-types-and-how-data-is-stored"></a><span data-ttu-id="b5c92-114">Studio account types and how data is stored</span><span class="sxs-lookup"><span data-stu-id="b5c92-114">Studio account types and how data is stored</span></span>

<span data-ttu-id="b5c92-115">There are three kinds of accounts in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b5c92-115">There are three kinds of accounts in Machine Learning Studio.</span></span> <span data-ttu-id="b5c92-116">The kind of account you have determines how your data is stored and how you can delete or export it.</span><span class="sxs-lookup"><span data-stu-id="b5c92-116">The kind of account you have determines how your data is stored and how you can delete or export it.</span></span>

- <span data-ttu-id="b5c92-117">A **guest workspace** is a free, anonymous account.</span><span class="sxs-lookup"><span data-stu-id="b5c92-117">A **guest workspace** is a free, anonymous account.</span></span> <span data-ttu-id="b5c92-118">You sign up without providing credentials, such as an email address or password.</span><span class="sxs-lookup"><span data-stu-id="b5c92-118">You sign up without providing credentials, such as an email address or password.</span></span>
    -  <span data-ttu-id="b5c92-119">Data is purged after the guest workspace expires.</span><span class="sxs-lookup"><span data-stu-id="b5c92-119">Data is purged after the guest workspace expires.</span></span>
    - <span data-ttu-id="b5c92-120">Guest users can export customer data through the UI, REST APIs, or PowerShell package.</span><span class="sxs-lookup"><span data-stu-id="b5c92-120">Guest users can export customer data through the UI, REST APIs, or PowerShell package.</span></span>
- <span data-ttu-id="b5c92-121">A **free workspace** is a free account you sign in to with Microsoft account credentials - an email address and password.</span><span class="sxs-lookup"><span data-stu-id="b5c92-121">A **free workspace** is a free account you sign in to with Microsoft account credentials - an email address and password.</span></span>
    - <span data-ttu-id="b5c92-122">You can export and delete personal and customer data, which are subject to data subject rights (DSR) requests.</span><span class="sxs-lookup"><span data-stu-id="b5c92-122">You can export and delete personal and customer data, which are subject to data subject rights (DSR) requests.</span></span>
    - <span data-ttu-id="b5c92-123">You can export customer data through the UI, REST APIs, or PowerShell package.</span><span class="sxs-lookup"><span data-stu-id="b5c92-123">You can export customer data through the UI, REST APIs, or PowerShell package.</span></span>
    - <span data-ttu-id="b5c92-124">For free workspaces not using Azure AD accounts, telemetry can be exported using the Privacy Portal.</span><span class="sxs-lookup"><span data-stu-id="b5c92-124">For free workspaces not using Azure AD accounts, telemetry can be exported using the Privacy Portal.</span></span>
    - <span data-ttu-id="b5c92-125">When you delete the workspace, you delete all personal customer data.</span><span class="sxs-lookup"><span data-stu-id="b5c92-125">When you delete the workspace, you delete all personal customer data.</span></span>
- <span data-ttu-id="b5c92-126">A **standard workspace** is a paid account you access with sign-in credentials.</span><span class="sxs-lookup"><span data-stu-id="b5c92-126">A **standard workspace** is a paid account you access with sign-in credentials.</span></span>
    - <span data-ttu-id="b5c92-127">You can export and delete personal and customer data, which are subject to DSR requests.</span><span class="sxs-lookup"><span data-stu-id="b5c92-127">You can export and delete personal and customer data, which are subject to DSR requests.</span></span>
    - <span data-ttu-id="b5c92-128">You can access data through the Azure Privacy portal</span><span class="sxs-lookup"><span data-stu-id="b5c92-128">You can access data through the Azure Privacy portal</span></span>
    - <span data-ttu-id="b5c92-129">You can export personal and customer data through the UI, REST APIs, or PowerShell package</span><span class="sxs-lookup"><span data-stu-id="b5c92-129">You can export personal and customer data through the UI, REST APIs, or PowerShell package</span></span>
    - <span data-ttu-id="b5c92-130">You can delete your data in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5c92-130">You can delete your data in the Azure portal.</span></span>

## <a name="delete-workspace-data-in-studio"></a><span data-ttu-id="b5c92-131">Delete workspace data in Studio</span><span class="sxs-lookup"><span data-stu-id="b5c92-131">Delete workspace data in Studio</span></span> 

### <a name="delete-individual-assets"></a><span data-ttu-id="b5c92-132">Delete individual assets</span><span class="sxs-lookup"><span data-stu-id="b5c92-132">Delete individual assets</span></span>

<span data-ttu-id="b5c92-133">Users can delete assets in a workspace by selecting them, and then selecting the delete button.</span><span class="sxs-lookup"><span data-stu-id="b5c92-133">Users can delete assets in a workspace by selecting them, and then selecting the delete button.</span></span>

![Delete assets in Machine Learning Studio](./media/export-delete-personal-data-dsr/delete-studio-asset.png)

### <a name="delete-an-entire-workspace"></a><span data-ttu-id="b5c92-135">Delete an entire workspace</span><span class="sxs-lookup"><span data-stu-id="b5c92-135">Delete an entire workspace</span></span>

<span data-ttu-id="b5c92-136">Users can also delete their entire workspace:</span><span class="sxs-lookup"><span data-stu-id="b5c92-136">Users can also delete their entire workspace:</span></span>
- <span data-ttu-id="b5c92-137">Paid workspace: Delete through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5c92-137">Paid workspace: Delete through the Azure portal.</span></span>
- <span data-ttu-id="b5c92-138">Free workspace: Use the delete button in the **Settings** pane.</span><span class="sxs-lookup"><span data-stu-id="b5c92-138">Free workspace: Use the delete button in the **Settings** pane.</span></span>

![Delete a free workspace in Machine Learning Studio](./media/export-delete-personal-data-dsr/delete-studio-data-workspace.png)
 
## <a name="export-studio-data-with-powershell"></a><span data-ttu-id="b5c92-140">Export Studio data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5c92-140">Export Studio data with PowerShell</span></span>
<span data-ttu-id="b5c92-141">Use PowerShell to export all your information to a portable format from Azure Machine Learning Studio using commands.</span><span class="sxs-lookup"><span data-stu-id="b5c92-141">Use PowerShell to export all your information to a portable format from Azure Machine Learning Studio using commands.</span></span> <span data-ttu-id="b5c92-142">For information, see the [PowerShell module for Azure Machine Learning](powershell-module.md) article.</span><span class="sxs-lookup"><span data-stu-id="b5c92-142">For information, see the [PowerShell module for Azure Machine Learning](powershell-module.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5c92-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5c92-143">Next steps</span></span>

<span data-ttu-id="b5c92-144">For documentation covering web services and commitment plan billing, see [Azure Machine Learning REST API reference](https://docs.microsoft.com/rest/api/machinelearning/).</span><span class="sxs-lookup"><span data-stu-id="b5c92-144">For documentation covering web services and commitment plan billing, see [Azure Machine Learning REST API reference](https://docs.microsoft.com/rest/api/machinelearning/).</span></span> 
