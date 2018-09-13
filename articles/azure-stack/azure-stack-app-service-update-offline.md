---
title: Update Azure App Service Offline | Microsoft Docs
description: Detailed guidance for updating Azure App Service on Azure Stack offline
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: anwestg
ms.openlocfilehash: f48872d1853dfd4c40022f42c8e237973ac70fe6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856534"
---
# <a name="offline-update-of-azure-app-service-on-azure-stack"></a><span data-ttu-id="84e65-103">Offline update of Azure App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="84e65-103">Offline update of Azure App Service on Azure Stack</span></span>

<span data-ttu-id="84e65-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="84e65-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84e65-105">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span><span class="sxs-lookup"><span data-stu-id="84e65-105">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span></span>
>
>

<span data-ttu-id="84e65-106">By following the instructions in this article, you can upgrade the [App Service resource provider](azure-stack-app-service-overview.md) deployed in an Azure Stack environment that is:</span><span class="sxs-lookup"><span data-stu-id="84e65-106">By following the instructions in this article, you can upgrade the [App Service resource provider](azure-stack-app-service-overview.md) deployed in an Azure Stack environment that is:</span></span>

* <span data-ttu-id="84e65-107">not connected to the Internet</span><span class="sxs-lookup"><span data-stu-id="84e65-107">not connected to the Internet</span></span>
* <span data-ttu-id="84e65-108">secured by Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="84e65-108">secured by Active Directory Federation Services (AD FS).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84e65-109">Prior to running the upgrade, make sure that you have already completed the [deployment of the Azure App Service on Azure Stack Resource Provider](azure-stack-app-service-deploy-offline.md)</span><span class="sxs-lookup"><span data-stu-id="84e65-109">Prior to running the upgrade, make sure that you have already completed the [deployment of the Azure App Service on Azure Stack Resource Provider](azure-stack-app-service-deploy-offline.md)</span></span>
>
>

## <a name="run-the-app-service-resource-provider-installer"></a><span data-ttu-id="84e65-110">Run the App Service resource provider installer</span><span class="sxs-lookup"><span data-stu-id="84e65-110">Run the App Service resource provider installer</span></span>

<span data-ttu-id="84e65-111">To upgrade the App Service resource provider in an Azure Stack environment, you must complete these tasks:</span><span class="sxs-lookup"><span data-stu-id="84e65-111">To upgrade the App Service resource provider in an Azure Stack environment, you must complete these tasks:</span></span>

1. <span data-ttu-id="84e65-112">Download the [App Service Installer](https://aka.ms/appsvcupdate3installer)</span><span class="sxs-lookup"><span data-stu-id="84e65-112">Download the [App Service Installer](https://aka.ms/appsvcupdate3installer)</span></span>
2. <span data-ttu-id="84e65-113">Create an offline upgrade package.</span><span class="sxs-lookup"><span data-stu-id="84e65-113">Create an offline upgrade package.</span></span>
3. <span data-ttu-id="84e65-114">Run the App Service installer (appservice.exe) and complete the upgrade.</span><span class="sxs-lookup"><span data-stu-id="84e65-114">Run the App Service installer (appservice.exe) and complete the upgrade.</span></span>

<span data-ttu-id="84e65-115">During this process, the upgrade will:</span><span class="sxs-lookup"><span data-stu-id="84e65-115">During this process, the upgrade will:</span></span>

* <span data-ttu-id="84e65-116">Detect prior deployment of App Service</span><span class="sxs-lookup"><span data-stu-id="84e65-116">Detect prior deployment of App Service</span></span>
* <span data-ttu-id="84e65-117">Upload to Storage</span><span class="sxs-lookup"><span data-stu-id="84e65-117">Upload to Storage</span></span>
* <span data-ttu-id="84e65-118">Upgrade all App Service roles (Controllers, Management, Front-End, Publisher, and Worker roles)</span><span class="sxs-lookup"><span data-stu-id="84e65-118">Upgrade all App Service roles (Controllers, Management, Front-End, Publisher, and Worker roles)</span></span>
* <span data-ttu-id="84e65-119">Update App Service scale set definitions</span><span class="sxs-lookup"><span data-stu-id="84e65-119">Update App Service scale set definitions</span></span>
* <span data-ttu-id="84e65-120">Update App Service Resource Provider Manifest</span><span class="sxs-lookup"><span data-stu-id="84e65-120">Update App Service Resource Provider Manifest</span></span>

## <a name="create-an-offline-upgrade-package"></a><span data-ttu-id="84e65-121">Create an offline upgrade package</span><span class="sxs-lookup"><span data-stu-id="84e65-121">Create an offline upgrade package</span></span>

<span data-ttu-id="84e65-122">To upgrade App Service in a disconnected environment, you must first create an offline upgrade package on a machine that's connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="84e65-122">To upgrade App Service in a disconnected environment, you must first create an offline upgrade package on a machine that's connected to the Internet.</span></span>

1. <span data-ttu-id="84e65-123">Run appservice.exe as an administrator</span><span class="sxs-lookup"><span data-stu-id="84e65-123">Run appservice.exe as an administrator</span></span>

    ![App Service Installer][1]

2. <span data-ttu-id="84e65-125">Click **Advanced** > **Create offline package**</span><span class="sxs-lookup"><span data-stu-id="84e65-125">Click **Advanced** > **Create offline package**</span></span>

    ![App Service Installer Advanced][2]

3. <span data-ttu-id="84e65-127">The App Service installer creates an offline upgrade package and displays the path to it.</span><span class="sxs-lookup"><span data-stu-id="84e65-127">The App Service installer creates an offline upgrade package and displays the path to it.</span></span>  <span data-ttu-id="84e65-128">You can click **Open folder** to open the folder in your file explorer.</span><span class="sxs-lookup"><span data-stu-id="84e65-128">You can click **Open folder** to open the folder in your file explorer.</span></span>

4. <span data-ttu-id="84e65-129">Copy the installer (AppService.exe) and the offline upgrade package to your Azure Stack host machine.</span><span class="sxs-lookup"><span data-stu-id="84e65-129">Copy the installer (AppService.exe) and the offline upgrade package to your Azure Stack host machine.</span></span>

## <a name="complete-the-upgrade-of-app-service-on-azure-stack"></a><span data-ttu-id="84e65-130">Complete the upgrade of App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="84e65-130">Complete the upgrade of App Service on Azure Stack</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84e65-131">The App Service installer must be run on a machine which can reach the Azure Stack Administrator Azure Resource Manager Endpoint.</span><span class="sxs-lookup"><span data-stu-id="84e65-131">The App Service installer must be run on a machine which can reach the Azure Stack Administrator Azure Resource Manager Endpoint.</span></span>
>
>

1. <span data-ttu-id="84e65-132">Run appservice.exe as an administrator.</span><span class="sxs-lookup"><span data-stu-id="84e65-132">Run appservice.exe as an administrator.</span></span>

    ![App Service Installer][1]

2. <span data-ttu-id="84e65-134">Click **Advanced** > **Complete offline installation or upgrade**.</span><span class="sxs-lookup"><span data-stu-id="84e65-134">Click **Advanced** > **Complete offline installation or upgrade**.</span></span>

    ![App Service Installer Advanced][2]

3. <span data-ttu-id="84e65-136">Browse to the location of the offline upgrade package you previously created and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="84e65-136">Browse to the location of the offline upgrade package you previously created and then click **Next**.</span></span>

4. <span data-ttu-id="84e65-137">Review and accept the Microsoft Software License Terms and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="84e65-137">Review and accept the Microsoft Software License Terms and then click **Next**.</span></span>

5. <span data-ttu-id="84e65-138">Review and accept the third-party license terms and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="84e65-138">Review and accept the third-party license terms and then click **Next**.</span></span>

6. <span data-ttu-id="84e65-139">Make sure that the Azure Stack Azure Resource Manager endpoint and Active Directory Tenant information is correct.</span><span class="sxs-lookup"><span data-stu-id="84e65-139">Make sure that the Azure Stack Azure Resource Manager endpoint and Active Directory Tenant information is correct.</span></span> <span data-ttu-id="84e65-140">If you used the default settings during Azure Stack Development Kit deployment, you can accept the default values here.</span><span class="sxs-lookup"><span data-stu-id="84e65-140">If you used the default settings during Azure Stack Development Kit deployment, you can accept the default values here.</span></span> <span data-ttu-id="84e65-141">However, if you customized the options when you deployed Azure Stack, you must edit the values in this window to reflect that.</span><span class="sxs-lookup"><span data-stu-id="84e65-141">However, if you customized the options when you deployed Azure Stack, you must edit the values in this window to reflect that.</span></span> <span data-ttu-id="84e65-142">For example, if you use the domain suffix *mycloud.com*, your Azure Stack Azure Resource Manager endpoint must change to *management.region.mycloud.com*.</span><span class="sxs-lookup"><span data-stu-id="84e65-142">For example, if you use the domain suffix *mycloud.com*, your Azure Stack Azure Resource Manager endpoint must change to *management.region.mycloud.com*.</span></span> <span data-ttu-id="84e65-143">After you confirm your information, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="84e65-143">After you confirm your information, click **Next**.</span></span>

    ![Azure Stack Cloud Information][3]

7. <span data-ttu-id="84e65-145">On the next page:</span><span class="sxs-lookup"><span data-stu-id="84e65-145">On the next page:</span></span>

   1. <span data-ttu-id="84e65-146">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span><span class="sxs-lookup"><span data-stu-id="84e65-146">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span></span>
        * <span data-ttu-id="84e65-147">If you're using Azure Active Directory (Azure AD), enter the Azure AD admin account and password that you provided when you deployed Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="84e65-147">If you're using Azure Active Directory (Azure AD), enter the Azure AD admin account and password that you provided when you deployed Azure Stack.</span></span> <span data-ttu-id="84e65-148">Click  **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="84e65-148">Click  **Sign In**.</span></span>
        * <span data-ttu-id="84e65-149">If you're using Active Directory Federation Services (AD FS), provide your admin account.</span><span class="sxs-lookup"><span data-stu-id="84e65-149">If you're using Active Directory Federation Services (AD FS), provide your admin account.</span></span> <span data-ttu-id="84e65-150">For example, *cloudadmin@azurestack.local*.</span><span class="sxs-lookup"><span data-stu-id="84e65-150">For example, *cloudadmin@azurestack.local*.</span></span> <span data-ttu-id="84e65-151">Enter your password, and click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="84e65-151">Enter your password, and click **Sign In**.</span></span>
   2. <span data-ttu-id="84e65-152">In the **Azure Stack Subscriptions** box, select the **Default Provider Subscription**.</span><span class="sxs-lookup"><span data-stu-id="84e65-152">In the **Azure Stack Subscriptions** box, select the **Default Provider Subscription**.</span></span>
   3. <span data-ttu-id="84e65-153">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying to.</span><span class="sxs-lookup"><span data-stu-id="84e65-153">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying to.</span></span> <span data-ttu-id="84e65-154">For example, select **local** if your deploying to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="84e65-154">For example, select **local** if your deploying to the Azure Stack Development Kit.</span></span>
   4. <span data-ttu-id="84e65-155">If an existing App Service deployment is discovered, then the resource group and storage account will be populated and greyed out.</span><span class="sxs-lookup"><span data-stu-id="84e65-155">If an existing App Service deployment is discovered, then the resource group and storage account will be populated and greyed out.</span></span>
   5. <span data-ttu-id="84e65-156">Click **Next** to review the upgrade summary.</span><span class="sxs-lookup"><span data-stu-id="84e65-156">Click **Next** to review the upgrade summary.</span></span>

    ![App Service Installation Detected][4]

8. <span data-ttu-id="84e65-158">On the summary page:</span><span class="sxs-lookup"><span data-stu-id="84e65-158">On the summary page:</span></span>
   1. <span data-ttu-id="84e65-159">Verify the selections you made.</span><span class="sxs-lookup"><span data-stu-id="84e65-159">Verify the selections you made.</span></span> <span data-ttu-id="84e65-160">To make changes, use the **Previous** buttons to visit previous pages.</span><span class="sxs-lookup"><span data-stu-id="84e65-160">To make changes, use the **Previous** buttons to visit previous pages.</span></span>
   2. <span data-ttu-id="84e65-161">If the configurations are correct, select the check box.</span><span class="sxs-lookup"><span data-stu-id="84e65-161">If the configurations are correct, select the check box.</span></span>
   3. <span data-ttu-id="84e65-162">To start the upgrade, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="84e65-162">To start the upgrade, click **Next**.</span></span>

       ![App Service Upgrade Summary][5]

9. <span data-ttu-id="84e65-164">Upgrade progress page:</span><span class="sxs-lookup"><span data-stu-id="84e65-164">Upgrade progress page:</span></span>
    1. <span data-ttu-id="84e65-165">Track the upgrade progress.</span><span class="sxs-lookup"><span data-stu-id="84e65-165">Track the upgrade progress.</span></span> <span data-ttu-id="84e65-166">The duration of the upgrade of App Service on Azure Stack varies dependent on number of role instances deployed.</span><span class="sxs-lookup"><span data-stu-id="84e65-166">The duration of the upgrade of App Service on Azure Stack varies dependent on number of role instances deployed.</span></span>
    2. <span data-ttu-id="84e65-167">After the upgrade successfully completes, click **Exit**.</span><span class="sxs-lookup"><span data-stu-id="84e65-167">After the upgrade successfully completes, click **Exit**.</span></span>

        ![App Service Upgrade Progress][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-update-offline/app-service-exe.png
[2]: ./media/azure-stack-app-service-update-offline/app-service-exe-advanced.png
[3]: ./media/azure-stack-app-service-update-offline/app-service-azure-resource-manager-endpoints.png
[4]: ./media/azure-stack-app-service-update-offline/app-service-installation-detected.png
[5]: ./media/azure-stack-app-service-update-offline/app-service-upgrade-summary.png
[6]: ./media/azure-stack-app-service-update-offline/app-service-upgrade-complete.png

## <a name="next-steps"></a><span data-ttu-id="84e65-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="84e65-169">Next steps</span></span>

<span data-ttu-id="84e65-170">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span><span class="sxs-lookup"><span data-stu-id="84e65-170">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

* [<span data-ttu-id="84e65-171">SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="84e65-171">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
* [<span data-ttu-id="84e65-172">MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="84e65-172">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)
