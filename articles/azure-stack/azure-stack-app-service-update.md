---
title: Update Azure App Service on Azure Stack | Microsoft Docs
description: Detailed guidance for updating Azure App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: anwestg
ms.openlocfilehash: 0e2b5b9902dbd3e9716801941663667bfa2b9da8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869176"
---
# <a name="update-azure-app-service-on-azure-stack"></a><span data-ttu-id="b71c5-103">Update Azure App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b71c5-103">Update Azure App Service on Azure Stack</span></span>

<span data-ttu-id="b71c5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="b71c5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="b71c5-105">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span><span class="sxs-lookup"><span data-stu-id="b71c5-105">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span></span>
>
>

<span data-ttu-id="b71c5-106">By following the instructions in this article, you can upgrade the [App Service resource provider](azure-stack-app-service-overview.md) deployed in an Azure Stack environment that is connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="b71c5-106">By following the instructions in this article, you can upgrade the [App Service resource provider](azure-stack-app-service-overview.md) deployed in an Azure Stack environment that is connected to the Internet.</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="b71c5-107">Prior to running the upgrade, make sure that you have already completed the [deployment of the Azure App Service on Azure Stack Resource Provider](azure-stack-app-service-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="b71c5-107">Prior to running the upgrade, make sure that you have already completed the [deployment of the Azure App Service on Azure Stack Resource Provider](azure-stack-app-service-deploy.md)</span></span>


## <a name="run-the-app-service-resource-provider-installer"></a><span data-ttu-id="b71c5-108">Run the App Service resource provider installer</span><span class="sxs-lookup"><span data-stu-id="b71c5-108">Run the App Service resource provider installer</span></span>

<span data-ttu-id="b71c5-109">During this process, the upgrade will:</span><span class="sxs-lookup"><span data-stu-id="b71c5-109">During this process, the upgrade will:</span></span>

* <span data-ttu-id="b71c5-110">Detect prior deployment of App Service</span><span class="sxs-lookup"><span data-stu-id="b71c5-110">Detect prior deployment of App Service</span></span>
* <span data-ttu-id="b71c5-111">Prepare all update packages and new versions of all OSS Libraries to be deployed</span><span class="sxs-lookup"><span data-stu-id="b71c5-111">Prepare all update packages and new versions of all OSS Libraries to be deployed</span></span>
* <span data-ttu-id="b71c5-112">Upload to Storage</span><span class="sxs-lookup"><span data-stu-id="b71c5-112">Upload to Storage</span></span>
* <span data-ttu-id="b71c5-113">Upgrade all App Service roles (Controllers, Management, Front-End, Publisher, and Worker roles)</span><span class="sxs-lookup"><span data-stu-id="b71c5-113">Upgrade all App Service roles (Controllers, Management, Front-End, Publisher, and Worker roles)</span></span>
* <span data-ttu-id="b71c5-114">Update App Service scale set definitions</span><span class="sxs-lookup"><span data-stu-id="b71c5-114">Update App Service scale set definitions</span></span>
* <span data-ttu-id="b71c5-115">Update App Service Resource Provider Manifest</span><span class="sxs-lookup"><span data-stu-id="b71c5-115">Update App Service Resource Provider Manifest</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b71c5-116">The App Service installer must be run on a machine which can reach the Azure Stack Administrator Azure Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="b71c5-116">The App Service installer must be run on a machine which can reach the Azure Stack Administrator Azure Resource Manager endpoint.</span></span>
>
>

<span data-ttu-id="b71c5-117">To upgrade your deployment of App Service on Azure Stack, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b71c5-117">To upgrade your deployment of App Service on Azure Stack, follow these steps:</span></span>

1. <span data-ttu-id="b71c5-118">Download the [App Service Installer](https://aka.ms/appsvcupdate3installer)</span><span class="sxs-lookup"><span data-stu-id="b71c5-118">Download the [App Service Installer](https://aka.ms/appsvcupdate3installer)</span></span>

2. <span data-ttu-id="b71c5-119">Run appservice.exe as an administrator</span><span class="sxs-lookup"><span data-stu-id="b71c5-119">Run appservice.exe as an administrator</span></span>

    ![App Service Installer][1]

3. <span data-ttu-id="b71c5-121">Click **Deploy App Service or upgrade to the latest version.**</span><span class="sxs-lookup"><span data-stu-id="b71c5-121">Click **Deploy App Service or upgrade to the latest version.**</span></span>

4. <span data-ttu-id="b71c5-122">Review and accept the Microsoft Software License Terms and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-122">Review and accept the Microsoft Software License Terms and then click **Next**.</span></span>

5. <span data-ttu-id="b71c5-123">Review and accept the third-party license terms and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-123">Review and accept the third-party license terms and then click **Next**.</span></span>

6. <span data-ttu-id="b71c5-124">Make sure that the Azure Stack Azure Resource Manager endpoint and Active Directory Tenant information is correct.</span><span class="sxs-lookup"><span data-stu-id="b71c5-124">Make sure that the Azure Stack Azure Resource Manager endpoint and Active Directory Tenant information is correct.</span></span> <span data-ttu-id="b71c5-125">If you used the default settings during Azure Stack Development Kit deployment, you can accept the default values here.</span><span class="sxs-lookup"><span data-stu-id="b71c5-125">If you used the default settings during Azure Stack Development Kit deployment, you can accept the default values here.</span></span> <span data-ttu-id="b71c5-126">However, if you customized the options when you deployed Azure Stack, you must edit the values in this window to reflect that.</span><span class="sxs-lookup"><span data-stu-id="b71c5-126">However, if you customized the options when you deployed Azure Stack, you must edit the values in this window to reflect that.</span></span> <span data-ttu-id="b71c5-127">For example, if you use the domain suffix *mycloud.com*, your Azure Stack Azure Resource Manager endpoint must change to *management.region.mycloud.com*.</span><span class="sxs-lookup"><span data-stu-id="b71c5-127">For example, if you use the domain suffix *mycloud.com*, your Azure Stack Azure Resource Manager endpoint must change to *management.region.mycloud.com*.</span></span> <span data-ttu-id="b71c5-128">After you confirm your information, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-128">After you confirm your information, click **Next**.</span></span>

    ![Azure Stack Cloud Information][2]

7. <span data-ttu-id="b71c5-130">On the next page:</span><span class="sxs-lookup"><span data-stu-id="b71c5-130">On the next page:</span></span>

   1. <span data-ttu-id="b71c5-131">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span><span class="sxs-lookup"><span data-stu-id="b71c5-131">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span></span>
        * <span data-ttu-id="b71c5-132">If you're using Azure Active Directory (Azure AD), enter the Azure AD admin account and password that you provided when you deployed Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b71c5-132">If you're using Azure Active Directory (Azure AD), enter the Azure AD admin account and password that you provided when you deployed Azure Stack.</span></span> <span data-ttu-id="b71c5-133">Click  **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-133">Click  **Sign In**.</span></span>
        * <span data-ttu-id="b71c5-134">If you're using Active Directory Federation Services (AD FS), provide your admin account.</span><span class="sxs-lookup"><span data-stu-id="b71c5-134">If you're using Active Directory Federation Services (AD FS), provide your admin account.</span></span> <span data-ttu-id="b71c5-135">For example, *cloudadmin@azurestack.local*.</span><span class="sxs-lookup"><span data-stu-id="b71c5-135">For example, *cloudadmin@azurestack.local*.</span></span> <span data-ttu-id="b71c5-136">Enter your password, and click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-136">Enter your password, and click **Sign In**.</span></span>
   2. <span data-ttu-id="b71c5-137">In the **Azure Stack Subscriptions** box, select the **Default Provider Subscription**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-137">In the **Azure Stack Subscriptions** box, select the **Default Provider Subscription**.</span></span>
   3. <span data-ttu-id="b71c5-138">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying to.</span><span class="sxs-lookup"><span data-stu-id="b71c5-138">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying to.</span></span> <span data-ttu-id="b71c5-139">For example, select **local** if your deploying to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="b71c5-139">For example, select **local** if your deploying to the Azure Stack Development Kit.</span></span>
   4. <span data-ttu-id="b71c5-140">If an existing App Service deployment is discovered, then the resource group and storage account will be populated and greyed out.</span><span class="sxs-lookup"><span data-stu-id="b71c5-140">If an existing App Service deployment is discovered, then the resource group and storage account will be populated and greyed out.</span></span>
   5. <span data-ttu-id="b71c5-141">Click **Next** to review the upgrade summary.</span><span class="sxs-lookup"><span data-stu-id="b71c5-141">Click **Next** to review the upgrade summary.</span></span>

    ![App Service Installation Detected][3]

8. <span data-ttu-id="b71c5-143">On the summary page:</span><span class="sxs-lookup"><span data-stu-id="b71c5-143">On the summary page:</span></span>
   1. <span data-ttu-id="b71c5-144">Verify the selections you made.</span><span class="sxs-lookup"><span data-stu-id="b71c5-144">Verify the selections you made.</span></span> <span data-ttu-id="b71c5-145">To make changes, use the **Previous** buttons to visit previous pages.</span><span class="sxs-lookup"><span data-stu-id="b71c5-145">To make changes, use the **Previous** buttons to visit previous pages.</span></span>
   2. <span data-ttu-id="b71c5-146">If the configurations are correct, select the check box.</span><span class="sxs-lookup"><span data-stu-id="b71c5-146">If the configurations are correct, select the check box.</span></span>
   3. <span data-ttu-id="b71c5-147">To start the upgrade, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-147">To start the upgrade, click **Next**.</span></span>

       ![App Service Upgrade Summary][4]

9. <span data-ttu-id="b71c5-149">Upgrade progress page:</span><span class="sxs-lookup"><span data-stu-id="b71c5-149">Upgrade progress page:</span></span>
    1. <span data-ttu-id="b71c5-150">Track the upgrade progress.</span><span class="sxs-lookup"><span data-stu-id="b71c5-150">Track the upgrade progress.</span></span> <span data-ttu-id="b71c5-151">The duration of the upgrade of App Service on Azure Stack varies dependent on number of role instances deployed.</span><span class="sxs-lookup"><span data-stu-id="b71c5-151">The duration of the upgrade of App Service on Azure Stack varies dependent on number of role instances deployed.</span></span>
    2. <span data-ttu-id="b71c5-152">After the upgrade successfully completes, click **Exit**.</span><span class="sxs-lookup"><span data-stu-id="b71c5-152">After the upgrade successfully completes, click **Exit**.</span></span>

        ![App Service Upgrade Progress][5]

<!--Image references-->
[1]: ./media/azure-stack-app-service-update/app-service-exe.png
[2]: ./media/azure-stack-app-service-update/app-service-azure-resource-manager-endpoints.png
[3]: ./media/azure-stack-app-service-update/app-service-installation-detected.png
[4]: ./media/azure-stack-app-service-update/app-service-upgrade-summary.png
[5]: ./media/azure-stack-app-service-update/app-service-upgrade-complete.png

## <a name="next-steps"></a><span data-ttu-id="b71c5-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="b71c5-154">Next steps</span></span>

<span data-ttu-id="b71c5-155">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span><span class="sxs-lookup"><span data-stu-id="b71c5-155">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

* [<span data-ttu-id="b71c5-156">SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="b71c5-156">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
* [<span data-ttu-id="b71c5-157">MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="b71c5-157">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)
