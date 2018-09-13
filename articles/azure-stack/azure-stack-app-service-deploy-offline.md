---
title: Deploy App Service in an offline environment in Azure Stack | Microsoft Docs
description: Detailed guidance on how to deploy App Service in a disconnected Azure Stack environment secured by AD FS.
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
ms.openlocfilehash: 9e36e470c3516c55089ce1e44540b6b1eacbb6b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825825"
---
# <a name="add-an-app-service-resource-provider-to-a-disconnected-azure-stack-environment-secured-by-ad-fs"></a><span data-ttu-id="5c19a-103">Add an App Service resource provider to a disconnected Azure Stack environment secured by AD FS</span><span class="sxs-lookup"><span data-stu-id="5c19a-103">Add an App Service resource provider to a disconnected Azure Stack environment secured by AD FS</span></span>

<span data-ttu-id="5c19a-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="5c19a-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c19a-105">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span><span class="sxs-lookup"><span data-stu-id="5c19a-105">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span></span>
>
>

<span data-ttu-id="5c19a-106">By following the instructions in this article, you can install the [App Service resource provider](azure-stack-app-service-overview.md) to an Azure Stack environment that is:</span><span class="sxs-lookup"><span data-stu-id="5c19a-106">By following the instructions in this article, you can install the [App Service resource provider](azure-stack-app-service-overview.md) to an Azure Stack environment that is:</span></span>

- <span data-ttu-id="5c19a-107">not connected to the Internet</span><span class="sxs-lookup"><span data-stu-id="5c19a-107">not connected to the Internet</span></span>
- <span data-ttu-id="5c19a-108">secured by Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="5c19a-108">secured by Active Directory Federation Services (AD FS).</span></span>

<span data-ttu-id="5c19a-109">To add the App Service resource provider to your offline Azure Stack deployment, you must complete these top-level tasks:</span><span class="sxs-lookup"><span data-stu-id="5c19a-109">To add the App Service resource provider to your offline Azure Stack deployment, you must complete these top-level tasks:</span></span>

1. <span data-ttu-id="5c19a-110">Complete the [prerequisite steps](azure-stack-app-service-before-you-get-started.md) (like purchasing certificates, which can take a few days to receive).</span><span class="sxs-lookup"><span data-stu-id="5c19a-110">Complete the [prerequisite steps](azure-stack-app-service-before-you-get-started.md) (like purchasing certificates, which can take a few days to receive).</span></span>
2. <span data-ttu-id="5c19a-111">[Download and extract the installation and helper files](azure-stack-app-service-before-you-get-started.md) to a machine connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="5c19a-111">[Download and extract the installation and helper files](azure-stack-app-service-before-you-get-started.md) to a machine connected to the Internet.</span></span>
3. <span data-ttu-id="5c19a-112">Create an offline installation package.</span><span class="sxs-lookup"><span data-stu-id="5c19a-112">Create an offline installation package.</span></span>
4. <span data-ttu-id="5c19a-113">Run the appservice.exe installer file.</span><span class="sxs-lookup"><span data-stu-id="5c19a-113">Run the appservice.exe installer file.</span></span>

## <a name="create-an-offline-installation-package"></a><span data-ttu-id="5c19a-114">Create an offline installation package</span><span class="sxs-lookup"><span data-stu-id="5c19a-114">Create an offline installation package</span></span>

<span data-ttu-id="5c19a-115">To deploy App Service in a disconnected environment, you must first create an offline installation package on a machine that's connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="5c19a-115">To deploy App Service in a disconnected environment, you must first create an offline installation package on a machine that's connected to the Internet.</span></span>

1. <span data-ttu-id="5c19a-116">Run the AppService.exe installer on a machine that's connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="5c19a-116">Run the AppService.exe installer on a machine that's connected to the Internet.</span></span>

2. <span data-ttu-id="5c19a-117">Click  **Advanced** > **Create offline installation package**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-117">Click  **Advanced** > **Create offline installation package**.</span></span>

    ![App Service Installer][1]

3. <span data-ttu-id="5c19a-119">The App Service installer creates an offline installation package and displays the path to it.</span><span class="sxs-lookup"><span data-stu-id="5c19a-119">The App Service installer creates an offline installation package and displays the path to it.</span></span> <span data-ttu-id="5c19a-120">You can click **Open folder** to open the folder in your file explorer.</span><span class="sxs-lookup"><span data-stu-id="5c19a-120">You can click **Open folder** to open the folder in your file explorer.</span></span>

    ![App Service Installer](media/azure-stack-app-service-deploy-offline/image02.png)

4. <span data-ttu-id="5c19a-122">Copy the installer (AppService.exe) and the offline installation package to your Azure Stack host machine.</span><span class="sxs-lookup"><span data-stu-id="5c19a-122">Copy the installer (AppService.exe) and the offline installation package to your Azure Stack host machine.</span></span>

## <a name="complete-the-offline-installation-of-app-service-on-azure-stack"></a><span data-ttu-id="5c19a-123">Complete the offline installation of App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5c19a-123">Complete the offline installation of App Service on Azure Stack</span></span>

1. <span data-ttu-id="5c19a-124">Run appservice.exe as an administrator from a computer that can reach the Azure Stack Admin Azure Resource Management endpoint.</span><span class="sxs-lookup"><span data-stu-id="5c19a-124">Run appservice.exe as an administrator from a computer that can reach the Azure Stack Admin Azure Resource Management endpoint.</span></span>

2. <span data-ttu-id="5c19a-125">Click **Advanced** > **Complete offline installation**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-125">Click **Advanced** > **Complete offline installation**.</span></span>

    ![App Service Installer][2]

3. <span data-ttu-id="5c19a-127">Browse to the location of the offline installation package you previously created, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-127">Browse to the location of the offline installation package you previously created, and then click **Next**.</span></span>

    ![App Service Installer](media/azure-stack-app-service-deploy-offline/image04.png)

4. <span data-ttu-id="5c19a-129">Review and accept the Microsoft Software License Terms, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-129">Review and accept the Microsoft Software License Terms, and then click **Next**.</span></span>

5. <span data-ttu-id="5c19a-130">Review and accept the third-party license terms, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-130">Review and accept the third-party license terms, and then click **Next**.</span></span>

6. <span data-ttu-id="5c19a-131">Make sure that the App Service cloud configuration information is correct.</span><span class="sxs-lookup"><span data-stu-id="5c19a-131">Make sure that the App Service cloud configuration information is correct.</span></span> <span data-ttu-id="5c19a-132">If you used the default settings during Azure Stack Development Kit deployment, you can accept the default values here.</span><span class="sxs-lookup"><span data-stu-id="5c19a-132">If you used the default settings during Azure Stack Development Kit deployment, you can accept the default values here.</span></span> <span data-ttu-id="5c19a-133">However, if you customized the options when you deployed Azure Stack or are deploying on an integrated system, you must edit the values in this window to reflect that.</span><span class="sxs-lookup"><span data-stu-id="5c19a-133">However, if you customized the options when you deployed Azure Stack or are deploying on an integrated system, you must edit the values in this window to reflect that.</span></span> <span data-ttu-id="5c19a-134">For example, if you use the domain suffix mycloud.com, your Azure Stack Tenant Azure Resource Manager endpoint must change to management.<region>.mycloud.com.</span><span class="sxs-lookup"><span data-stu-id="5c19a-134">For example, if you use the domain suffix mycloud.com, your Azure Stack Tenant Azure Resource Manager endpoint must change to management.<region>.mycloud.com.</span></span> <span data-ttu-id="5c19a-135">After you confirm your information, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-135">After you confirm your information, click **Next**.</span></span>

    ![App Service Installer][3]

7. <span data-ttu-id="5c19a-137">On the next page:</span><span class="sxs-lookup"><span data-stu-id="5c19a-137">On the next page:</span></span>
    1. <span data-ttu-id="5c19a-138">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span><span class="sxs-lookup"><span data-stu-id="5c19a-138">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span></span>
        - <span data-ttu-id="5c19a-139">Provide your admin account.</span><span class="sxs-lookup"><span data-stu-id="5c19a-139">Provide your admin account.</span></span> <span data-ttu-id="5c19a-140">For example, cloudadmin@azurestack.local.</span><span class="sxs-lookup"><span data-stu-id="5c19a-140">For example, cloudadmin@azurestack.local.</span></span> <span data-ttu-id="5c19a-141">Enter your password, and click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-141">Enter your password, and click **Sign In**.</span></span>
    2. <span data-ttu-id="5c19a-142">In the **Azure Stack Subscriptions** box, select the **Default Provider Subscription**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-142">In the **Azure Stack Subscriptions** box, select the **Default Provider Subscription**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5c19a-143">App Service can only be deployed into the **Default Provider Subscription** at this time.</span><span class="sxs-lookup"><span data-stu-id="5c19a-143">App Service can only be deployed into the **Default Provider Subscription** at this time.</span></span>  <span data-ttu-id="5c19a-144">In a future update App Service will deploy into the new Metering Subscription introduced in Azure Stack 1804 and all existing deployments will be migrated to this new subscription also.</span><span class="sxs-lookup"><span data-stu-id="5c19a-144">In a future update App Service will deploy into the new Metering Subscription introduced in Azure Stack 1804 and all existing deployments will be migrated to this new subscription also.</span></span>
    >
    >
    
    3. <span data-ttu-id="5c19a-145">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying to.</span><span class="sxs-lookup"><span data-stu-id="5c19a-145">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying to.</span></span> <span data-ttu-id="5c19a-146">For example, select **local** if your deploying to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="5c19a-146">For example, select **local** if your deploying to the Azure Stack Development Kit.</span></span>
    4. <span data-ttu-id="5c19a-147">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-147">Click **Next**.</span></span>

    ![App Service Installer][4]

8. <span data-ttu-id="5c19a-149">You now have the option to deploy into an existing Virtual Network as configured through the steps [here](azure-stack-app-service-before-you-get-started.md#virtual-network), or allow the App Service installer to create a Virtual Network and associated Subnets.</span><span class="sxs-lookup"><span data-stu-id="5c19a-149">You now have the option to deploy into an existing Virtual Network as configured through the steps [here](azure-stack-app-service-before-you-get-started.md#virtual-network), or allow the App Service installer to create a Virtual Network and associated Subnets.</span></span>
    1. <span data-ttu-id="5c19a-150">Select **Create VNet with default settings**, accept the defaults, and then click **Next**, or;</span><span class="sxs-lookup"><span data-stu-id="5c19a-150">Select **Create VNet with default settings**, accept the defaults, and then click **Next**, or;</span></span>
    2. <span data-ttu-id="5c19a-151">Select **Use existing VNet and Subnets**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-151">Select **Use existing VNet and Subnets**.</span></span>
        1. <span data-ttu-id="5c19a-152">Select the **Resource Group** that contains your Virtual Network;</span><span class="sxs-lookup"><span data-stu-id="5c19a-152">Select the **Resource Group** that contains your Virtual Network;</span></span>
        2. <span data-ttu-id="5c19a-153">Choose the correct **Virtual Network** name you wish to deploy into;</span><span class="sxs-lookup"><span data-stu-id="5c19a-153">Choose the correct **Virtual Network** name you wish to deploy into;</span></span>
        3. <span data-ttu-id="5c19a-154">Select the correct **Subnet** values for each of the required role subnets;</span><span class="sxs-lookup"><span data-stu-id="5c19a-154">Select the correct **Subnet** values for each of the required role subnets;</span></span>
        4. <span data-ttu-id="5c19a-155">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="5c19a-155">Click **Next**</span></span>

    ![App Service Installer][5]

9. <span data-ttu-id="5c19a-157">Enter the information for your file share and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-157">Enter the information for your file share and then click **Next**.</span></span> <span data-ttu-id="5c19a-158">The address of the file share must use the Fully Qualified Domain Name, or IP Address of your File Server.</span><span class="sxs-lookup"><span data-stu-id="5c19a-158">The address of the file share must use the Fully Qualified Domain Name, or IP Address of your File Server.</span></span> <span data-ttu-id="5c19a-159">For example, \\\appservicefileserver.local.cloudapp.azurestack.external\websites, or \\\10.0.0.1\websites</span><span class="sxs-lookup"><span data-stu-id="5c19a-159">For example, \\\appservicefileserver.local.cloudapp.azurestack.external\websites, or \\\10.0.0.1\websites</span></span>

    > [!NOTE]
    > <span data-ttu-id="5c19a-160">The installer attempts to test connectivity to the fileshare before proceeding.</span><span class="sxs-lookup"><span data-stu-id="5c19a-160">The installer attempts to test connectivity to the fileshare before proceeding.</span></span>  <span data-ttu-id="5c19a-161">However, if you chose to deploy in an existing   Virtual Network, the installer might not be able to connect to the fileshare and displays a warning, asking whether you want to continue.</span><span class="sxs-lookup"><span data-stu-id="5c19a-161">However, if you chose to deploy in an existing   Virtual Network, the installer might not be able to connect to the fileshare and displays a warning, asking whether you want to continue.</span></span>  <span data-ttu-id="5c19a-162">Verify the fileshare information and continue if they are correct.</span><span class="sxs-lookup"><span data-stu-id="5c19a-162">Verify the fileshare information and continue if they are correct.</span></span>
    >
    >

   ![App Service Installer][8]

10. <span data-ttu-id="5c19a-164">On the next page:</span><span class="sxs-lookup"><span data-stu-id="5c19a-164">On the next page:</span></span>
    1. <span data-ttu-id="5c19a-165">In the **Identity Application ID** box, enter the GUID for the application you’re using for identity (from Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c19a-165">In the **Identity Application ID** box, enter the GUID for the application you’re using for identity (from Azure AD).</span></span>
    2. <span data-ttu-id="5c19a-166">In the **Identity Application certificate file** box, enter (or browse to) the location of the certificate file.</span><span class="sxs-lookup"><span data-stu-id="5c19a-166">In the **Identity Application certificate file** box, enter (or browse to) the location of the certificate file.</span></span>
    3. <span data-ttu-id="5c19a-167">In the **Identity Application certificate password** box, enter the password for the certificate.</span><span class="sxs-lookup"><span data-stu-id="5c19a-167">In the **Identity Application certificate password** box, enter the password for the certificate.</span></span> <span data-ttu-id="5c19a-168">This password is the one that you made note of when you used the script to create the certificates.</span><span class="sxs-lookup"><span data-stu-id="5c19a-168">This password is the one that you made note of when you used the script to create the certificates.</span></span>
    4. <span data-ttu-id="5c19a-169">In the **Azure Resource Manager root certificate file** box, enter (or browse to) the location of the certificate file.</span><span class="sxs-lookup"><span data-stu-id="5c19a-169">In the **Azure Resource Manager root certificate file** box, enter (or browse to) the location of the certificate file.</span></span>
    5. <span data-ttu-id="5c19a-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-170">Click **Next**.</span></span>

    ![App Service Installer][10]

11. <span data-ttu-id="5c19a-172">For each of the three certificate file boxes, click **Browse** and then navigate to the appropriate certificate file.</span><span class="sxs-lookup"><span data-stu-id="5c19a-172">For each of the three certificate file boxes, click **Browse** and then navigate to the appropriate certificate file.</span></span> <span data-ttu-id="5c19a-173">You must provide the password for each certificate.</span><span class="sxs-lookup"><span data-stu-id="5c19a-173">You must provide the password for each certificate.</span></span> <span data-ttu-id="5c19a-174">These certificates are the ones that you created in the [Create required certificates step](azure-stack-app-service-before-you-get-started.md#get-certificates).</span><span class="sxs-lookup"><span data-stu-id="5c19a-174">These certificates are the ones that you created in the [Create required certificates step](azure-stack-app-service-before-you-get-started.md#get-certificates).</span></span> <span data-ttu-id="5c19a-175">Click **Next** after entering all the information.</span><span class="sxs-lookup"><span data-stu-id="5c19a-175">Click **Next** after entering all the information.</span></span>

    | <span data-ttu-id="5c19a-176">Box</span><span class="sxs-lookup"><span data-stu-id="5c19a-176">Box</span></span> | <span data-ttu-id="5c19a-177">Certificate file name example</span><span class="sxs-lookup"><span data-stu-id="5c19a-177">Certificate file name example</span></span> |
    | --- | --- |
    | <span data-ttu-id="5c19a-178">**App Service default SSL certificate file**</span><span class="sxs-lookup"><span data-stu-id="5c19a-178">**App Service default SSL certificate file**</span></span> | <span data-ttu-id="5c19a-179">\_.appservice.local.AzureStack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="5c19a-179">\_.appservice.local.AzureStack.external.pfx</span></span> |
    | <span data-ttu-id="5c19a-180">**App Service API SSL certificate file**</span><span class="sxs-lookup"><span data-stu-id="5c19a-180">**App Service API SSL certificate file**</span></span> | <span data-ttu-id="5c19a-181">api.appservice.local.AzureStack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="5c19a-181">api.appservice.local.AzureStack.external.pfx</span></span> |
    | <span data-ttu-id="5c19a-182">**App Service Publisher SSL certificate file**</span><span class="sxs-lookup"><span data-stu-id="5c19a-182">**App Service Publisher SSL certificate file**</span></span> | <span data-ttu-id="5c19a-183">ftp.appservice.local.AzureStack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="5c19a-183">ftp.appservice.local.AzureStack.external.pfx</span></span> |

    <span data-ttu-id="5c19a-184">If you used a different domain suffix when you created the certificates, your certificate file names don’t use *local.AzureStack.external*.</span><span class="sxs-lookup"><span data-stu-id="5c19a-184">If you used a different domain suffix when you created the certificates, your certificate file names don’t use *local.AzureStack.external*.</span></span> <span data-ttu-id="5c19a-185">Instead, use your custom domain information.</span><span class="sxs-lookup"><span data-stu-id="5c19a-185">Instead, use your custom domain information.</span></span>

    ![App Service Installer][11]

12. <span data-ttu-id="5c19a-187">Enter the SQL Server details for the server instance used to host the App Service resource provider databases, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-187">Enter the SQL Server details for the server instance used to host the App Service resource provider databases, and then click **Next**.</span></span> <span data-ttu-id="5c19a-188">The installer validates the SQL connection properties.</span><span class="sxs-lookup"><span data-stu-id="5c19a-188">The installer validates the SQL connection properties.</span></span> <span data-ttu-id="5c19a-189">You **must** enter either the internal ip or fully qualified domain name for the SQL Server name.</span><span class="sxs-lookup"><span data-stu-id="5c19a-189">You **must** enter either the internal ip or fully qualified domain name for the SQL Server name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5c19a-190">The installer attempts to test connectivity to the SQl Server before proceeding.</span><span class="sxs-lookup"><span data-stu-id="5c19a-190">The installer attempts to test connectivity to the SQl Server before proceeding.</span></span>  <span data-ttu-id="5c19a-191">However, if you chose to deploy in an existing Virtual Network, the installer might not be able to connect to the SQL Server and displays a warning asking whether you want to continue.</span><span class="sxs-lookup"><span data-stu-id="5c19a-191">However, if you chose to deploy in an existing Virtual Network, the installer might not be able to connect to the SQL Server and displays a warning asking whether you want to continue.</span></span>  <span data-ttu-id="5c19a-192">Verify the SQL Server information and continue if they are correct.</span><span class="sxs-lookup"><span data-stu-id="5c19a-192">Verify the SQL Server information and continue if they are correct.</span></span>
    >
    > <span data-ttu-id="5c19a-193">From Azure App Service on Azure Stack 1.3 onwards, the installer will check that the SQL Server has database containment enabled at the SQL Server level.</span><span class="sxs-lookup"><span data-stu-id="5c19a-193">From Azure App Service on Azure Stack 1.3 onwards, the installer will check that the SQL Server has database containment enabled at the SQL Server level.</span></span>  <span data-ttu-id="5c19a-194">If it is not, you will be prompted with the following exception:</span><span class="sxs-lookup"><span data-stu-id="5c19a-194">If it is not, you will be prompted with the following exception:</span></span>
    > ```sql
    >    Enable contained database authentication for SQL server by running below command on SQL server (Ctrl+C to copy)
    >    ***********************************************************
    >    sp_configure 'contained database authentication', 1;  
    >    GO  
    >    RECONFIGURE;  
    >    GO
    >    ***********************************************************
    > ```
    > <span data-ttu-id="5c19a-195">Refer to the [release notes for Azure App Service on Azure Stack 1.3](azure-stack-app-service-release-notes-update-three.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="5c19a-195">Refer to the [release notes for Azure App Service on Azure Stack 1.3](azure-stack-app-service-release-notes-update-three.md) for more details.</span></span>
   
   ![App Service Installer][12]

13. <span data-ttu-id="5c19a-197">Review the role instance and SKU options.</span><span class="sxs-lookup"><span data-stu-id="5c19a-197">Review the role instance and SKU options.</span></span> <span data-ttu-id="5c19a-198">The defaults are populated with the minimum number of instances and the minimum SKU for each role in an ASDK Deployment.</span><span class="sxs-lookup"><span data-stu-id="5c19a-198">The defaults are populated with the minimum number of instances and the minimum SKU for each role in an ASDK Deployment.</span></span> <span data-ttu-id="5c19a-199">A summary of vCPU and memory requirements is provided to help plan your deployment.</span><span class="sxs-lookup"><span data-stu-id="5c19a-199">A summary of vCPU and memory requirements is provided to help plan your deployment.</span></span> <span data-ttu-id="5c19a-200">After you make your selections, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-200">After you make your selections, click **Next**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5c19a-201">For production deployments, follow the guidance in [Capacity planning for Azure App Service server roles in Azure Stack](azure-stack-app-service-capacity-planning.md).</span><span class="sxs-lookup"><span data-stu-id="5c19a-201">For production deployments, follow the guidance in [Capacity planning for Azure App Service server roles in Azure Stack](azure-stack-app-service-capacity-planning.md).</span></span>
     >
     >

    | <span data-ttu-id="5c19a-202">Role</span><span class="sxs-lookup"><span data-stu-id="5c19a-202">Role</span></span> | <span data-ttu-id="5c19a-203">Minimum instances</span><span class="sxs-lookup"><span data-stu-id="5c19a-203">Minimum instances</span></span> | <span data-ttu-id="5c19a-204">Minimum SKU</span><span class="sxs-lookup"><span data-stu-id="5c19a-204">Minimum SKU</span></span> | <span data-ttu-id="5c19a-205">Notes</span><span class="sxs-lookup"><span data-stu-id="5c19a-205">Notes</span></span> |
    | --- | --- | --- | --- |
    | <span data-ttu-id="5c19a-206">Controller</span><span class="sxs-lookup"><span data-stu-id="5c19a-206">Controller</span></span> | <span data-ttu-id="5c19a-207">1</span><span class="sxs-lookup"><span data-stu-id="5c19a-207">1</span></span> | <span data-ttu-id="5c19a-208">Standard_A2 - (2 vCPU, 3584 MB)</span><span class="sxs-lookup"><span data-stu-id="5c19a-208">Standard_A2 - (2 vCPU, 3584 MB)</span></span> | <span data-ttu-id="5c19a-209">Manages and maintains the health of the App Service cloud.</span><span class="sxs-lookup"><span data-stu-id="5c19a-209">Manages and maintains the health of the App Service cloud.</span></span> |
    | <span data-ttu-id="5c19a-210">Management</span><span class="sxs-lookup"><span data-stu-id="5c19a-210">Management</span></span> | <span data-ttu-id="5c19a-211">1</span><span class="sxs-lookup"><span data-stu-id="5c19a-211">1</span></span> | <span data-ttu-id="5c19a-212">Standard_A2 - (2 vCPUs, 3584 MB)</span><span class="sxs-lookup"><span data-stu-id="5c19a-212">Standard_A2 - (2 vCPUs, 3584 MB)</span></span> | <span data-ttu-id="5c19a-213">Manages the App Service Azure Resource Manager and API endpoints, portal extensions (admin, tenant, Functions portal), and the data service.</span><span class="sxs-lookup"><span data-stu-id="5c19a-213">Manages the App Service Azure Resource Manager and API endpoints, portal extensions (admin, tenant, Functions portal), and the data service.</span></span> <span data-ttu-id="5c19a-214">To support failover, increased the recommended instances to 2.</span><span class="sxs-lookup"><span data-stu-id="5c19a-214">To support failover, increased the recommended instances to 2.</span></span> |
    | <span data-ttu-id="5c19a-215">Publisher</span><span class="sxs-lookup"><span data-stu-id="5c19a-215">Publisher</span></span> | <span data-ttu-id="5c19a-216">1</span><span class="sxs-lookup"><span data-stu-id="5c19a-216">1</span></span> | <span data-ttu-id="5c19a-217">Standard_A1 - (1 vCPU, 1792 MB)</span><span class="sxs-lookup"><span data-stu-id="5c19a-217">Standard_A1 - (1 vCPU, 1792 MB)</span></span> | <span data-ttu-id="5c19a-218">Publishes content via FTP and web deployment.</span><span class="sxs-lookup"><span data-stu-id="5c19a-218">Publishes content via FTP and web deployment.</span></span> |
    | <span data-ttu-id="5c19a-219">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5c19a-219">FrontEnd</span></span> | <span data-ttu-id="5c19a-220">1</span><span class="sxs-lookup"><span data-stu-id="5c19a-220">1</span></span> | <span data-ttu-id="5c19a-221">Standard_A1 - (1 vCPU, 1792 MB)</span><span class="sxs-lookup"><span data-stu-id="5c19a-221">Standard_A1 - (1 vCPU, 1792 MB)</span></span> | <span data-ttu-id="5c19a-222">Routes requests to App Service applications.</span><span class="sxs-lookup"><span data-stu-id="5c19a-222">Routes requests to App Service applications.</span></span> |
    | <span data-ttu-id="5c19a-223">Shared Worker</span><span class="sxs-lookup"><span data-stu-id="5c19a-223">Shared Worker</span></span> | <span data-ttu-id="5c19a-224">1</span><span class="sxs-lookup"><span data-stu-id="5c19a-224">1</span></span> | <span data-ttu-id="5c19a-225">Standard_A1 - (1 vCPU, 1792 MB)</span><span class="sxs-lookup"><span data-stu-id="5c19a-225">Standard_A1 - (1 vCPU, 1792 MB)</span></span> | <span data-ttu-id="5c19a-226">Hosts web or API applications and Azure Functions apps.</span><span class="sxs-lookup"><span data-stu-id="5c19a-226">Hosts web or API applications and Azure Functions apps.</span></span> <span data-ttu-id="5c19a-227">You might want to add more instances.</span><span class="sxs-lookup"><span data-stu-id="5c19a-227">You might want to add more instances.</span></span> <span data-ttu-id="5c19a-228">As an operator, you can define your offering and choose any SKU tier.</span><span class="sxs-lookup"><span data-stu-id="5c19a-228">As an operator, you can define your offering and choose any SKU tier.</span></span> <span data-ttu-id="5c19a-229">The tiers must have a minimum of one vCPU.</span><span class="sxs-lookup"><span data-stu-id="5c19a-229">The tiers must have a minimum of one vCPU.</span></span> |

    ![App Service Installer][14]

    > [!NOTE]
    > <span data-ttu-id="5c19a-231">**Windows Server 2016 Core is not a supported platform image for use with Azure App Service on Azure Stack.  Do not use evaluation images for production deployments.  Azure App Service on Azure Stack requires that Microsoft.Net 3.5.1 SP1 is activated on the image used for deployment.   Marketplace syndicated Windows Server 2016 images do not have this feature enabled.**</span><span class="sxs-lookup"><span data-stu-id="5c19a-231">**Windows Server 2016 Core is not a supported platform image for use with Azure App Service on Azure Stack.  Do not use evaluation images for production deployments.  Azure App Service on Azure Stack requires that Microsoft.Net 3.5.1 SP1 is activated on the image used for deployment.   Marketplace syndicated Windows Server 2016 images do not have this feature enabled.**</span></span>

14. <span data-ttu-id="5c19a-232">In the **Select Platform Image** box, choose your deployment Windows Server 2016 virtual machine image from those available in the compute resource provider for the App Service cloud.</span><span class="sxs-lookup"><span data-stu-id="5c19a-232">In the **Select Platform Image** box, choose your deployment Windows Server 2016 virtual machine image from those available in the compute resource provider for the App Service cloud.</span></span> <span data-ttu-id="5c19a-233">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-233">Click **Next**.</span></span>

15. <span data-ttu-id="5c19a-234">On the next page:</span><span class="sxs-lookup"><span data-stu-id="5c19a-234">On the next page:</span></span>
     1. <span data-ttu-id="5c19a-235">Enter the Worker Role virtual machine administrator user name and password.</span><span class="sxs-lookup"><span data-stu-id="5c19a-235">Enter the Worker Role virtual machine administrator user name and password.</span></span>
     2. <span data-ttu-id="5c19a-236">Enter the Other Roles virtual machine administrator user name and password.</span><span class="sxs-lookup"><span data-stu-id="5c19a-236">Enter the Other Roles virtual machine administrator user name and password.</span></span>
     3. <span data-ttu-id="5c19a-237">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-237">Click **Next**.</span></span>

    ![App Service Installer][16]

16. <span data-ttu-id="5c19a-239">On the summary page:</span><span class="sxs-lookup"><span data-stu-id="5c19a-239">On the summary page:</span></span>
    1. <span data-ttu-id="5c19a-240">Verify the selections you made.</span><span class="sxs-lookup"><span data-stu-id="5c19a-240">Verify the selections you made.</span></span> <span data-ttu-id="5c19a-241">To make changes, use the **Previous** buttons to visit previous pages.</span><span class="sxs-lookup"><span data-stu-id="5c19a-241">To make changes, use the **Previous** buttons to visit previous pages.</span></span>
    2. <span data-ttu-id="5c19a-242">If the configurations are correct, select the check box.</span><span class="sxs-lookup"><span data-stu-id="5c19a-242">If the configurations are correct, select the check box.</span></span>
    3. <span data-ttu-id="5c19a-243">To start the deployment, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-243">To start the deployment, click **Next**.</span></span>

    ![App Service Installer][17]

17. <span data-ttu-id="5c19a-245">On the next page:</span><span class="sxs-lookup"><span data-stu-id="5c19a-245">On the next page:</span></span>
    1. <span data-ttu-id="5c19a-246">Track the installation progress.</span><span class="sxs-lookup"><span data-stu-id="5c19a-246">Track the installation progress.</span></span> <span data-ttu-id="5c19a-247">App Service on Azure Stack takes about 60 minutes to deploy based on the default selections.</span><span class="sxs-lookup"><span data-stu-id="5c19a-247">App Service on Azure Stack takes about 60 minutes to deploy based on the default selections.</span></span>
    2. <span data-ttu-id="5c19a-248">After the installer successfully finishes, click **Exit**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-248">After the installer successfully finishes, click **Exit**.</span></span>

    ![App Service Installer][18]

## <a name="validate-the-app-service-on-azure-stack-installation"></a><span data-ttu-id="5c19a-250">Validate the App Service on Azure Stack installation</span><span class="sxs-lookup"><span data-stu-id="5c19a-250">Validate the App Service on Azure Stack installation</span></span>

1. <span data-ttu-id="5c19a-251">In the Azure Stack admin portal, go to **Administration - App Service**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-251">In the Azure Stack admin portal, go to **Administration - App Service**.</span></span>

2. <span data-ttu-id="5c19a-252">In the overview under status, check to see that the **Status** shows **All roles are ready**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-252">In the overview under status, check to see that the **Status** shows **All roles are ready**.</span></span>

    ![App Service Management](media/azure-stack-app-service-deploy/image12.png)
    
> [!NOTE]
> <span data-ttu-id="5c19a-254">If you chose to deploy into an existing virtual network and a internal IP address to connect to your fileserver, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the fileserver.</span><span class="sxs-lookup"><span data-stu-id="5c19a-254">If you chose to deploy into an existing virtual network and a internal IP address to connect to your fileserver, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the fileserver.</span></span>  <span data-ttu-id="5c19a-255">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span><span class="sxs-lookup"><span data-stu-id="5c19a-255">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span></span>
> * <span data-ttu-id="5c19a-256">Source: Any</span><span class="sxs-lookup"><span data-stu-id="5c19a-256">Source: Any</span></span>
> * <span data-ttu-id="5c19a-257">Source port range: \*</span><span class="sxs-lookup"><span data-stu-id="5c19a-257">Source port range: \*</span></span>
> * <span data-ttu-id="5c19a-258">Destination: IP Addresses</span><span class="sxs-lookup"><span data-stu-id="5c19a-258">Destination: IP Addresses</span></span>
> * <span data-ttu-id="5c19a-259">Destination IP address range: Range of IPs for your fileserver</span><span class="sxs-lookup"><span data-stu-id="5c19a-259">Destination IP address range: Range of IPs for your fileserver</span></span>
> * <span data-ttu-id="5c19a-260">Destination port range: 445</span><span class="sxs-lookup"><span data-stu-id="5c19a-260">Destination port range: 445</span></span>
> * <span data-ttu-id="5c19a-261">Protocol: TCP</span><span class="sxs-lookup"><span data-stu-id="5c19a-261">Protocol: TCP</span></span>
> * <span data-ttu-id="5c19a-262">Action: Allow</span><span class="sxs-lookup"><span data-stu-id="5c19a-262">Action: Allow</span></span>
> * <span data-ttu-id="5c19a-263">Priority: 700</span><span class="sxs-lookup"><span data-stu-id="5c19a-263">Priority: 700</span></span>
> * <span data-ttu-id="5c19a-264">Name: Outbound_Allow_SMB445</span><span class="sxs-lookup"><span data-stu-id="5c19a-264">Name: Outbound_Allow_SMB445</span></span>
>

## <a name="test-drive-app-service-on-azure-stack"></a><span data-ttu-id="5c19a-265">Test drive App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5c19a-265">Test drive App Service on Azure Stack</span></span>

<span data-ttu-id="5c19a-266">After you deploy and register the App Service resource provider, test it to make sure that users can deploy web and API apps.</span><span class="sxs-lookup"><span data-stu-id="5c19a-266">After you deploy and register the App Service resource provider, test it to make sure that users can deploy web and API apps.</span></span>

> [!NOTE]
> <span data-ttu-id="5c19a-267">You need to create an offer that has the Microsoft.Web namespace within the plan.</span><span class="sxs-lookup"><span data-stu-id="5c19a-267">You need to create an offer that has the Microsoft.Web namespace within the plan.</span></span> <span data-ttu-id="5c19a-268">Then you need to have a tenant subscription that subscribes to this offer.</span><span class="sxs-lookup"><span data-stu-id="5c19a-268">Then you need to have a tenant subscription that subscribes to this offer.</span></span> <span data-ttu-id="5c19a-269">For more information, see [Create offer](azure-stack-create-offer.md) and [Create plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="5c19a-269">For more information, see [Create offer](azure-stack-create-offer.md) and [Create plan](azure-stack-create-plan.md).</span></span>
>
<span data-ttu-id="5c19a-270">You *must* have a tenant subscription to create applications that use App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5c19a-270">You *must* have a tenant subscription to create applications that use App Service on Azure Stack.</span></span> <span data-ttu-id="5c19a-271">The only capabilities that a service admin can complete within the admin portal are related to the resource provider administration of App Service.</span><span class="sxs-lookup"><span data-stu-id="5c19a-271">The only capabilities that a service admin can complete within the admin portal are related to the resource provider administration of App Service.</span></span> <span data-ttu-id="5c19a-272">These capabilities include adding capacity, configuring deployment sources, and adding Worker tiers and SKUs.</span><span class="sxs-lookup"><span data-stu-id="5c19a-272">These capabilities include adding capacity, configuring deployment sources, and adding Worker tiers and SKUs.</span></span>
>
<span data-ttu-id="5c19a-273">As of the third technical preview, to create web, API, and Azure Functions apps, you must use the tenant portal and have a tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="5c19a-273">As of the third technical preview, to create web, API, and Azure Functions apps, you must use the tenant portal and have a tenant subscription.</span></span>

1. <span data-ttu-id="5c19a-274">In the Azure Stack tenant portal, click **New** > **Web + Mobile** > **Web App**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-274">In the Azure Stack tenant portal, click **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="5c19a-275">On the **Web App** blade, type a name in the **Web app** box.</span><span class="sxs-lookup"><span data-stu-id="5c19a-275">On the **Web App** blade, type a name in the **Web app** box.</span></span>

3. <span data-ttu-id="5c19a-276">Under **Resource Group**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-276">Under **Resource Group**, click **New**.</span></span> <span data-ttu-id="5c19a-277">Type a name in the **Resource Group** box.</span><span class="sxs-lookup"><span data-stu-id="5c19a-277">Type a name in the **Resource Group** box.</span></span>

4. <span data-ttu-id="5c19a-278">Click **App Service plan/Location** > **Create New**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-278">Click **App Service plan/Location** > **Create New**.</span></span>

5. <span data-ttu-id="5c19a-279">On the **App Service plan** blade, type a name in the **App Service plan** box.</span><span class="sxs-lookup"><span data-stu-id="5c19a-279">On the **App Service plan** blade, type a name in the **App Service plan** box.</span></span>

6. <span data-ttu-id="5c19a-280">Click **Pricing tier** > **Free-Shared** or **Shared-Shared** > **Select** > **OK** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c19a-280">Click **Pricing tier** > **Free-Shared** or **Shared-Shared** > **Select** > **OK** > **Create**.</span></span>

7. <span data-ttu-id="5c19a-281">In under a minute, a tile for the new web app appears on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="5c19a-281">In under a minute, a tile for the new web app appears on the dashboard.</span></span> <span data-ttu-id="5c19a-282">Click the tile.</span><span class="sxs-lookup"><span data-stu-id="5c19a-282">Click the tile.</span></span>

8. <span data-ttu-id="5c19a-283">On the **Web App** blade, click **Browse** to view the default website for this app.</span><span class="sxs-lookup"><span data-stu-id="5c19a-283">On the **Web App** blade, click **Browse** to view the default website for this app.</span></span>

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a><span data-ttu-id="5c19a-284">Deploy a WordPress, DNN, or Django website (optional)</span><span class="sxs-lookup"><span data-stu-id="5c19a-284">Deploy a WordPress, DNN, or Django website (optional)</span></span>

1. <span data-ttu-id="5c19a-285">In the Azure Stack tenant portal, click **+**, go to the Azure Marketplace, deploy a Django website, and wait for successful completion.</span><span class="sxs-lookup"><span data-stu-id="5c19a-285">In the Azure Stack tenant portal, click **+**, go to the Azure Marketplace, deploy a Django website, and wait for successful completion.</span></span> <span data-ttu-id="5c19a-286">The Django web platform uses a file system-based database.</span><span class="sxs-lookup"><span data-stu-id="5c19a-286">The Django web platform uses a file system-based database.</span></span> <span data-ttu-id="5c19a-287">It doesn’t require any additional resource providers, such as SQL or MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c19a-287">It doesn’t require any additional resource providers, such as SQL or MySQL.</span></span>

2. <span data-ttu-id="5c19a-288">If you also deployed a MySQL resource provider, you can deploy a WordPress website from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5c19a-288">If you also deployed a MySQL resource provider, you can deploy a WordPress website from the Marketplace.</span></span> <span data-ttu-id="5c19a-289">When you're prompted for database parameters, enter the user name as *User1@Server1*, with the user name and server name of your choice.</span><span class="sxs-lookup"><span data-stu-id="5c19a-289">When you're prompted for database parameters, enter the user name as *User1@Server1*, with the user name and server name of your choice.</span></span>

3. <span data-ttu-id="5c19a-290">If you also deployed a SQL Server resource provider, you can deploy a DNN website from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5c19a-290">If you also deployed a SQL Server resource provider, you can deploy a DNN website from the Marketplace.</span></span> <span data-ttu-id="5c19a-291">When you're prompted for database parameters, choose a database in the computer running SQL Server that's connected to your resource provider.</span><span class="sxs-lookup"><span data-stu-id="5c19a-291">When you're prompted for database parameters, choose a database in the computer running SQL Server that's connected to your resource provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c19a-292">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c19a-292">Next steps</span></span>

<span data-ttu-id="5c19a-293">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span><span class="sxs-lookup"><span data-stu-id="5c19a-293">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

- [<span data-ttu-id="5c19a-294">SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="5c19a-294">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
- [<span data-ttu-id="5c19a-295">MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="5c19a-295">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)

<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-advanced-create-package.png
[2]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-advanced-complete-offline.png
[3]: ./media/azure-stack-app-service-deploy-offline/app-service-azure-stack-arm-endpoints.png
[4]: ./media/azure-stack-app-service-deploy-offline/app-service-azure-stack-subscription-information.png
[5]: ./media/azure-stack-app-service-deploy-offline/app-service-default-VNET-config.png
[6]: ./media/azure-stack-app-service-deploy-offline/app-service-custom-VNET-config.png
[7]: ./media/azure-stack-app-service-deploy-offline/app-service-custom-VNET-config-with-values.png
[8]: ./media/azure-stack-app-service-deploy-offline/app-service-fileshare-configuration.png
[9]: ./media/azure-stack-app-service-deploy-offline/app-service-fileshare-configuration-error.png
[10]: ./media/azure-stack-app-service-deploy-offline/app-service-identity-app.png
[11]: ./media/azure-stack-app-service-deploy-offline/app-service-certificates.png
[12]: ./media/azure-stack-app-service-deploy-offline/app-service-sql-configuration.png
[13]: ./media/azure-stack-app-service-deploy-offline/app-service-sql-configuration-error.png
[14]: ./media/azure-stack-app-service-deploy-offline/app-service-cloud-quantities.png
[15]: ./media/azure-stack-app-service-deploy-offline/app-service-windows-image-selection.png
[16]: ./media/azure-stack-app-service-deploy-offline/app-service-role-credentials.png
[17]: ./media/azure-stack-app-service-deploy-offline/app-service-azure-stack-deployment-summary.png
[18]: ./media/azure-stack-app-service-deploy-offline/app-service-deployment-progress.png
