---
title: Getting started with Storage Explorer (Preview) | Microsoft Docs
description: Manage Azure storage resources with Storage Explorer (Preview)
services: storage
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: caad415589f6fb947c76da8df50dddfbe6570109
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550999"
---
# <a name="getting-started-with-storage-explorer-preview"></a><span data-ttu-id="fb213-103">Getting started with Storage Explorer (Preview)</span><span class="sxs-lookup"><span data-stu-id="fb213-103">Getting started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="fb213-104">Overview</span><span class="sxs-lookup"><span data-stu-id="fb213-104">Overview</span></span>
<span data-ttu-id="fb213-105">Microsoft Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="fb213-105">Microsoft Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="fb213-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="fb213-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (Preview)][15]

## <a name="prerequisites"></a><span data-ttu-id="fb213-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb213-108">Prerequisites</span></span>
* [<span data-ttu-id="fb213-109">Download and install Storage Explorer (preview)</span><span class="sxs-lookup"><span data-stu-id="fb213-109">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="fb213-110">Connect to a storage account or service</span><span class="sxs-lookup"><span data-stu-id="fb213-110">Connect to a storage account or service</span></span>
<span data-ttu-id="fb213-111">Storage Explorer (Preview) provides a number of ways to connect to storage accounts.</span><span class="sxs-lookup"><span data-stu-id="fb213-111">Storage Explorer (Preview) provides a number of ways to connect to storage accounts.</span></span> <span data-ttu-id="fb213-112">This includes connecting to storage accounts associated with your Azure subscriptions, connecting to storage accounts and services shared from other Azure subscriptions, and even connecting to and managing local storage using the Azure Storage Emulator.</span><span class="sxs-lookup"><span data-stu-id="fb213-112">This includes connecting to storage accounts associated with your Azure subscriptions, connecting to storage accounts and services shared from other Azure subscriptions, and even connecting to and managing local storage using the Azure Storage Emulator.</span></span> <span data-ttu-id="fb213-113">In addition, you can work with storage accounts in global and national Azure:</span><span class="sxs-lookup"><span data-stu-id="fb213-113">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="fb213-114">[Connect to an Azure subscription](#connect-to-an-azure-subscription) - Manage storage resources belonging to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fb213-114">[Connect to an Azure subscription](#connect-to-an-azure-subscription) - Manage storage resources belonging to your Azure subscription.</span></span>
* <span data-ttu-id="fb213-115">[Work with local development storage](#work-with-local-development-storage) - Manage local storage using the Azure Storage Emulator.</span><span class="sxs-lookup"><span data-stu-id="fb213-115">[Work with local development storage](#work-with-local-development-storage) - Manage local storage using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="fb213-116">[Attach to external storage](#attach-or-detach-an-external-storage-account) - Manage storage resources belonging to another Azure subscription or under national Azure clouds using the storage account's name, key, and endpoints.</span><span class="sxs-lookup"><span data-stu-id="fb213-116">[Attach to external storage](#attach-or-detach-an-external-storage-account) - Manage storage resources belonging to another Azure subscription or under national Azure clouds using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="fb213-117">[Attach storage account using SAS](#attach-storage-account-using-sas) - Manage storage resources belonging to another Azure subscription using a SAS.</span><span class="sxs-lookup"><span data-stu-id="fb213-117">[Attach storage account using SAS](#attach-storage-account-using-sas) - Manage storage resources belonging to another Azure subscription using a SAS.</span></span>
* <span data-ttu-id="fb213-118">[Attach service using SAS](#attach-service-using-sas) - Manage a specific storage service (blob container, queue, or table) belonging to another Azure subscription using a SAS.</span><span class="sxs-lookup"><span data-stu-id="fb213-118">[Attach service using SAS](#attach-service-using-sas) - Manage a specific storage service (blob container, queue, or table) belonging to another Azure subscription using a SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="fb213-119">Connect to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="fb213-119">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="fb213-120">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fb213-120">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="fb213-121">In Storage Explorer (Preview), select **Azure Account settings**.</span><span class="sxs-lookup"><span data-stu-id="fb213-121">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure account settings][0]
2. <span data-ttu-id="fb213-123">The left pane displays all the Microsoft accounts you've logged in to.</span><span class="sxs-lookup"><span data-stu-id="fb213-123">The left pane displays all the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="fb213-124">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fb213-124">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
> [!NOTE]
><span data-ttu-id="fb213-125">Connecting to national Azure such as Black Forest Azure, Fairfax Azure, and Mooncake Azure via sign-in is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="fb213-125">Connecting to national Azure such as Black Forest Azure, Fairfax Azure, and Mooncake Azure via sign-in is currently not supported.</span></span> <span data-ttu-id="fb213-126">See **Attach or detach an external storage account** section for how to connect to national Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="fb213-126">See **Attach or detach an external storage account** section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="fb213-127">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span><span class="sxs-lookup"><span data-stu-id="fb213-127">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="fb213-128">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fb213-128">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="fb213-129">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span><span class="sxs-lookup"><span data-stu-id="fb213-129">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Select Azure subscriptions][3]
4. <span data-ttu-id="fb213-131">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="fb213-131">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Selected Azure subscriptions][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="fb213-133">Connect to an Azure Stack subscription</span><span class="sxs-lookup"><span data-stu-id="fb213-133">Connect to an Azure Stack subscription</span></span>

1. <span data-ttu-id="fb213-134">VPN connection is needed for Storage Explorer to access Azure Stack subscription remotely.</span><span class="sxs-lookup"><span data-stu-id="fb213-134">VPN connection is needed for Storage Explorer to access Azure Stack subscription remotely.</span></span> <span data-ttu-id="fb213-135">To learn about how to set up VPN connection to Azure Stack, refer to [Connect to Azure Stack with VPN](azure-stack/azure-stack-connect-azure-stack.md#connect-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="fb213-135">To learn about how to set up VPN connection to Azure Stack, refer to [Connect to Azure Stack with VPN](azure-stack/azure-stack-connect-azure-stack.md#connect-with-vpn)</span></span>

2. <span data-ttu-id="fb213-136">For Azure Stack POC, you need to export Azure Stack authority root certificate.</span><span class="sxs-lookup"><span data-stu-id="fb213-136">For Azure Stack POC, you need to export Azure Stack authority root certificate.</span></span> <span data-ttu-id="fb213-137">Open `mmc.exe` on MAS-CON01, Azure Stack host machine or local machine with VPN connection to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fb213-137">Open `mmc.exe` on MAS-CON01, Azure Stack host machine or local machine with VPN connection to Azure Stack.</span></span> <span data-ttu-id="fb213-138">In **File**, select **Add/Remove Snap-in**, add **Certificates** to manage **Computer account** of **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="fb213-138">In **File**, select **Add/Remove Snap-in**, add **Certificates** to manage **Computer account** of **Local Computer**.</span></span>

   ![Load the Azure stack root certificate through mmc.exe][25]   

   <span data-ttu-id="fb213-140">Find **AzureStackCertificationAuthority** under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="fb213-140">Find **AzureStackCertificationAuthority** under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates**.</span></span> <span data-ttu-id="fb213-141">Right click on item, select **All Tasks -> Export**.</span><span class="sxs-lookup"><span data-stu-id="fb213-141">Right click on item, select **All Tasks -> Export**.</span></span> <span data-ttu-id="fb213-142">Then follow the dialogs to export certificate with **Base-64 encoded X.509 (.CER)**.</span><span class="sxs-lookup"><span data-stu-id="fb213-142">Then follow the dialogs to export certificate with **Base-64 encoded X.509 (.CER)**.</span></span> <span data-ttu-id="fb213-143">The exported certificate will be used in the next step.</span><span class="sxs-lookup"><span data-stu-id="fb213-143">The exported certificate will be used in the next step.</span></span>   

   ![Export the root Azure stack authority root certificate][26]   

3. <span data-ttu-id="fb213-145">In Storage Explorer (Preview), select the **Edit** menu, then **SSL Certificates**, then **Import Certificates**.</span><span class="sxs-lookup"><span data-stu-id="fb213-145">In Storage Explorer (Preview), select the **Edit** menu, then **SSL Certificates**, then **Import Certificates**.</span></span> <span data-ttu-id="fb213-146">Use the file picker dialog to find and open the certificate you explored in the previous step.</span><span class="sxs-lookup"><span data-stu-id="fb213-146">Use the file picker dialog to find and open the certificate you explored in the previous step.</span></span> <span data-ttu-id="fb213-147">After importing you will be prompted to restart Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="fb213-147">After importing you will be prompted to restart Storage Explorer.</span></span>

   ![Import the certificate into Storage Explorer (Preview)][27]

4. <span data-ttu-id="fb213-149">Once Storage Explorer (Preview) relaunches, select the **Edit** menu, and ensure **Target Azure Stack** is checked.</span><span class="sxs-lookup"><span data-stu-id="fb213-149">Once Storage Explorer (Preview) relaunches, select the **Edit** menu, and ensure **Target Azure Stack** is checked.</span></span> <span data-ttu-id="fb213-150">If not, check it and restart Storage Explorer for the change to take effect.</span><span class="sxs-lookup"><span data-stu-id="fb213-150">If not, check it and restart Storage Explorer for the change to take effect.</span></span> <span data-ttu-id="fb213-151">This configuration is required for  compatible with your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="fb213-151">This configuration is required for  compatible with your Azure Stack environment.</span></span>

   ![Ensure Target Azure Stack is selected][28]

5. <span data-ttu-id="fb213-153">On left side bar, select **Manage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="fb213-153">On left side bar, select **Manage Accounts**.</span></span> <span data-ttu-id="fb213-154">The left pane displays all the Microsoft accounts you are logged into.</span><span class="sxs-lookup"><span data-stu-id="fb213-154">The left pane displays all the Microsoft accounts you are logged into.</span></span> <span data-ttu-id="fb213-155">To connect to Azure Stack account, select **Add an account**.</span><span class="sxs-lookup"><span data-stu-id="fb213-155">To connect to Azure Stack account, select **Add an account**.</span></span>

   ![Add an Azure stack account][29]

6. <span data-ttu-id="fb213-157">Choose **Create Custom Environment** in under **Azure environment** in the **Add new account** dialog, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb213-157">Choose **Create Custom Environment** in under **Azure environment** in the **Add new account** dialog, then click **Next**.</span></span>

7. <span data-ttu-id="fb213-158">Input all required information of Azure Stack custom environment, then click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="fb213-158">Input all required information of Azure Stack custom environment, then click **Sign in**.</span></span>  <span data-ttu-id="fb213-159">Fill in the **Sign in to a Custom Cloud environment** dialog to sign in with Azure Stack account that is associated with at least one active Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="fb213-159">Fill in the **Sign in to a Custom Cloud environment** dialog to sign in with Azure Stack account that is associated with at least one active Azure Stack subscription.</span></span> <span data-ttu-id="fb213-160">Details for each field on the dialog are as follows:</span><span class="sxs-lookup"><span data-stu-id="fb213-160">Details for each field on the dialog are as follows:</span></span>

    * <span data-ttu-id="fb213-161">**Environment name** – The field can be customized by user.</span><span class="sxs-lookup"><span data-stu-id="fb213-161">**Environment name** – The field can be customized by user.</span></span>
    * <span data-ttu-id="fb213-162">**Authority** – The value should be https://login.windows.net.</span><span class="sxs-lookup"><span data-stu-id="fb213-162">**Authority** – The value should be https://login.windows.net.</span></span> <span data-ttu-id="fb213-163">For Azure China (Mooncake), please use https://login.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="fb213-163">For Azure China (Mooncake), please use https://login.chinacloudapi.cn.</span></span>
    * <span data-ttu-id="fb213-164">**Sign in resource id** – Retrieve the value by executing the following PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb213-164">**Sign in resource id** – Retrieve the value by executing the following PowerShell:</span></span>

    <span data-ttu-id="fb213-165">If you are Cloud Administrator:</span><span class="sxs-lookup"><span data-stu-id="fb213-165">If you are Cloud Administrator:</span></span>

    ```powershell
    PowerShell (Invoke-RestMethod -Uri https://adminmanagement.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
    ```

    <span data-ttu-id="fb213-166">If you are Tenant:</span><span class="sxs-lookup"><span data-stu-id="fb213-166">If you are Tenant:</span></span>

    ```powershell
    PowerShell (Invoke-RestMethod -Uri https://management.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
    ```

    * <span data-ttu-id="fb213-167">**Graph endpoint** – The value should be https://graph.windows.net.</span><span class="sxs-lookup"><span data-stu-id="fb213-167">**Graph endpoint** – The value should be https://graph.windows.net.</span></span> <span data-ttu-id="fb213-168">For Azure China (Mooncake), please use https://graph.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="fb213-168">For Azure China (Mooncake), please use https://graph.chinacloudapi.cn.</span></span>
    * <span data-ttu-id="fb213-169">**ARM resource id** – Use the same value as Sign in resource id.</span><span class="sxs-lookup"><span data-stu-id="fb213-169">**ARM resource id** – Use the same value as Sign in resource id.</span></span>
    * <span data-ttu-id="fb213-170">**ARM resource endpoint** – The samples of ARM resource endpoint:</span><span class="sxs-lookup"><span data-stu-id="fb213-170">**ARM resource endpoint** – The samples of ARM resource endpoint:</span></span>

    <span data-ttu-id="fb213-171">For Cloud Administrator: https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="fb213-171">For Cloud Administrator: https://adminmanagement.local.azurestack.external</span></span>   
    <span data-ttu-id="fb213-172">For Tenant: https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="fb213-172">For Tenant: https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="fb213-173">**Tenant Ids** – Optional.</span><span class="sxs-lookup"><span data-stu-id="fb213-173">**Tenant Ids** – Optional.</span></span> <span data-ttu-id="fb213-174">The value is given only when the directory must be specified.</span><span class="sxs-lookup"><span data-stu-id="fb213-174">The value is given only when the directory must be specified.</span></span>

8. <span data-ttu-id="fb213-175">Once you successfully sign in with an Azure Stack account, the left pane populates with the Azure Stack subscriptions associated with that account.</span><span class="sxs-lookup"><span data-stu-id="fb213-175">Once you successfully sign in with an Azure Stack account, the left pane populates with the Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="fb213-176">Select the Azure Stack subscriptions with which you want to work, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fb213-176">Select the Azure Stack subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="fb213-177">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure Stack subscriptions.)</span><span class="sxs-lookup"><span data-stu-id="fb213-177">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure Stack subscriptions.)</span></span>

   ![Select the Azure stack subscriptions after filling out the Custom Cloud Environment dialog][30]

9. <span data-ttu-id="fb213-179">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span><span class="sxs-lookup"><span data-stu-id="fb213-179">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

   ![List of storage accounts including Azure stack subscription accounts][31]

## <a name="work-with-local-development-storage"></a><span data-ttu-id="fb213-181">Work with local development storage</span><span class="sxs-lookup"><span data-stu-id="fb213-181">Work with local development storage</span></span>
<span data-ttu-id="fb213-182">Storage Explorer (Preview) enables you to work against local storage using the Azure Storage Emulator.</span><span class="sxs-lookup"><span data-stu-id="fb213-182">Storage Explorer (Preview) enables you to work against local storage using the Azure Storage Emulator.</span></span> <span data-ttu-id="fb213-183">This allows you to write code against and test storage without necessarily having a storage account deployed on Azure (since the storage account is being emulated by the Azure Storage Emulator).</span><span class="sxs-lookup"><span data-stu-id="fb213-183">This allows you to write code against and test storage without necessarily having a storage account deployed on Azure (since the storage account is being emulated by the Azure Storage Emulator).</span></span>

> [!NOTE]
> <span data-ttu-id="fb213-184">The Azure Storage Emulator is currently supported only for Windows.</span><span class="sxs-lookup"><span data-stu-id="fb213-184">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="fb213-185">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached** > **Storage Accounts** > **(Development)** node.</span><span class="sxs-lookup"><span data-stu-id="fb213-185">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Local development node][21]
2. <span data-ttu-id="fb213-187">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span><span class="sxs-lookup"><span data-stu-id="fb213-187">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="fb213-188">If the infobar is displayed, select **Download the latest version**, and install the emulator.</span><span class="sxs-lookup"><span data-stu-id="fb213-188">If the infobar is displayed, select **Download the latest version**, and install the emulator.</span></span>

    ![Download Azure Storage Emulator prompt][22]
3. <span data-ttu-id="fb213-190">Once the emulator is installed, you have the ability to create and work with local blobs, queues, and tables.</span><span class="sxs-lookup"><span data-stu-id="fb213-190">Once the emulator is installed, you have the ability to create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="fb213-191">To learn how to work with each storage account type, select one of the following links:</span><span class="sxs-lookup"><span data-stu-id="fb213-191">To learn how to work with each storage account type, select one of the following links:</span></span>

   * [<span data-ttu-id="fb213-192">Manage Azure blob storage resources</span><span class="sxs-lookup"><span data-stu-id="fb213-192">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
   * <span data-ttu-id="fb213-193">Manage Azure file share storage resources - *Coming soon*</span><span class="sxs-lookup"><span data-stu-id="fb213-193">Manage Azure file share storage resources - *Coming soon*</span></span>
   * <span data-ttu-id="fb213-194">Manage Azure queue storage resources - *Coming soon*</span><span class="sxs-lookup"><span data-stu-id="fb213-194">Manage Azure queue storage resources - *Coming soon*</span></span>
   * <span data-ttu-id="fb213-195">Manage Azure table storage resources - *Coming soon*</span><span class="sxs-lookup"><span data-stu-id="fb213-195">Manage Azure table storage resources - *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="fb213-196">Attach or detach an external storage account</span><span class="sxs-lookup"><span data-stu-id="fb213-196">Attach or detach an external storage account</span></span>
<span data-ttu-id="fb213-197">Storage Explorer (Preview) provides the ability to attach to external storage accounts so that storage accounts can be easily shared.</span><span class="sxs-lookup"><span data-stu-id="fb213-197">Storage Explorer (Preview) provides the ability to attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="fb213-198">This section explains how to attach to (and detach from) external storage accounts.</span><span class="sxs-lookup"><span data-stu-id="fb213-198">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="fb213-199">Get the storage account credentials</span><span class="sxs-lookup"><span data-stu-id="fb213-199">Get the storage account credentials</span></span>
<span data-ttu-id="fb213-200">To share an external storage account, the owner of that account must first get the credentials - account name and key - for the account and then share that information with the person wanting to attach to that (external) account.</span><span class="sxs-lookup"><span data-stu-id="fb213-200">To share an external storage account, the owner of that account must first get the credentials - account name and key - for the account and then share that information with the person wanting to attach to that (external) account.</span></span> <span data-ttu-id="fb213-201">Obtaining the storage account credentials can be done via the Azure portal by following these steps:</span><span class="sxs-lookup"><span data-stu-id="fb213-201">Obtaining the storage account credentials can be done via the Azure portal by following these steps:</span></span>

1. <span data-ttu-id="fb213-202">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb213-202">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fb213-203">Select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="fb213-203">Select **Browse**.</span></span>
3. <span data-ttu-id="fb213-204">Select **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="fb213-204">Select **Storage Accounts**.</span></span>
4. <span data-ttu-id="fb213-205">In the **Storage Accounts** blade, select the desired storage account.</span><span class="sxs-lookup"><span data-stu-id="fb213-205">In the **Storage Accounts** blade, select the desired storage account.</span></span>
5. <span data-ttu-id="fb213-206">In the **Settings** blade for the selected storage account, select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="fb213-206">In the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

   ![Access Keys option][5]
6. <span data-ttu-id="fb213-208">In the **Access keys** blade, copy the **STORAGE ACCOUNT NAME** and **KEY 1** values for use when attaching to the storage account.</span><span class="sxs-lookup"><span data-stu-id="fb213-208">In the **Access keys** blade, copy the **STORAGE ACCOUNT NAME** and **KEY 1** values for use when attaching to the storage account.</span></span>

   ![Access keys][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="fb213-210">Attach to an external storage account</span><span class="sxs-lookup"><span data-stu-id="fb213-210">Attach to an external storage account</span></span>
<span data-ttu-id="fb213-211">To attach to an external storage account, you need the account's name and key.</span><span class="sxs-lookup"><span data-stu-id="fb213-211">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="fb213-212">The section *Get the storage account credentials* explains how to obtain these values from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fb213-212">The section *Get the storage account credentials* explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="fb213-213">However, note that in the portal, the account key is called "key 1" so where the Storage Explorer (Preview) asks for an account key, you'll enter (or paste) the "key 1" value.</span><span class="sxs-lookup"><span data-stu-id="fb213-213">However, note that in the portal, the account key is called "key 1" so where the Storage Explorer (Preview) asks for an account key, you'll enter (or paste) the "key 1" value.</span></span>

1. <span data-ttu-id="fb213-214">In Storage Explorer (Preview), select **Connect to Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="fb213-214">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

   ![Connect to Azure storage option][23]
2. <span data-ttu-id="fb213-216">On the **Connect to Azure Storage** dialog, specify the account key ("key 1" value from the Azure portal), and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb213-216">On the **Connect to Azure Storage** dialog, specify the account key ("key 1" value from the Azure portal), and then select **Next**.</span></span>
> [!NOTE]
> <span data-ttu-id="fb213-217">You can enter Storage Connection string from a storage account on national Azure.</span><span class="sxs-lookup"><span data-stu-id="fb213-217">You can enter Storage Connection string from a storage account on national Azure.</span></span> <span data-ttu-id="fb213-218">For example, enter connection strings similar to the following to connect to Azure Black Forest storage accounts: DefaultEndpointsProtocol=https;AccountName=cawatest03;AccountKey=<storage_account_key>;EndpointSuffix=core.cloudapi.de; You can get the connection string from Azure portal in the same way as described in the **Get the storage account credentials** section</span><span class="sxs-lookup"><span data-stu-id="fb213-218">For example, enter connection strings similar to the following to connect to Azure Black Forest storage accounts: DefaultEndpointsProtocol=https;AccountName=cawatest03;AccountKey=<storage_account_key>;EndpointSuffix=core.cloudapi.de; You can get the connection string from Azure portal in the same way as described in the **Get the storage account credentials** section</span></span>

   ![Connect to Azure storage dialog][24]

3. <span data-ttu-id="fb213-220">In the **Attach External Storage** dialog, enter the storage account name in the **Account name** box, specify any other desired settings, and select **Next** when done.</span><span class="sxs-lookup"><span data-stu-id="fb213-220">In the **Attach External Storage** dialog, enter the storage account name in the **Account name** box, specify any other desired settings, and select **Next** when done.</span></span>

   ![Attach external storage dialog][8]
4. <span data-ttu-id="fb213-222">In the **Connection Summary** dialog, verify the information.</span><span class="sxs-lookup"><span data-stu-id="fb213-222">In the **Connection Summary** dialog, verify the information.</span></span> <span data-ttu-id="fb213-223">If you want to change anything, select **Back** and reenter the desired settings.</span><span class="sxs-lookup"><span data-stu-id="fb213-223">If you want to change anything, select **Back** and reenter the desired settings.</span></span> <span data-ttu-id="fb213-224">Once finished, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fb213-224">Once finished, select **Connect**.</span></span>
5. <span data-ttu-id="fb213-225">Once connected, the external storage account is displayed with the text **(External)** appended to the storage account name.</span><span class="sxs-lookup"><span data-stu-id="fb213-225">Once connected, the external storage account is displayed with the text **(External)** appended to the storage account name.</span></span>

   ![Result of connecting to an external storage account][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="fb213-227">Detach from an external storage account</span><span class="sxs-lookup"><span data-stu-id="fb213-227">Detach from an external storage account</span></span>
1. <span data-ttu-id="fb213-228">Right-click the external storage account you want to detach, and - from the context menu - select **Detach**.</span><span class="sxs-lookup"><span data-stu-id="fb213-228">Right-click the external storage account you want to detach, and - from the context menu - select **Detach**.</span></span>

   ![Detach from storage option][10]
2. <span data-ttu-id="fb213-230">When the confirmation message box appears, select **Yes** to confirm the detachment from the external storage account.</span><span class="sxs-lookup"><span data-stu-id="fb213-230">When the confirmation message box appears, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-storage-account-using-sas"></a><span data-ttu-id="fb213-231">Attach storage account using SAS</span><span class="sxs-lookup"><span data-stu-id="fb213-231">Attach storage account using SAS</span></span>
<span data-ttu-id="fb213-232">A [SAS (Shared Access Signature)](storage/storage-dotnet-shared-access-signature-part-1.md) gives the admin of an Azure subscription the ability to grant access to a storage account on a temporary basis without having to provide their Azure subscription credentials.</span><span class="sxs-lookup"><span data-stu-id="fb213-232">A [SAS (Shared Access Signature)](storage/storage-dotnet-shared-access-signature-part-1.md) gives the admin of an Azure subscription the ability to grant access to a storage account on a temporary basis without having to provide their Azure subscription credentials.</span></span>

<span data-ttu-id="fb213-233">To illustrate this, let's say UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span><span class="sxs-lookup"><span data-stu-id="fb213-233">To illustrate this, let's say UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="fb213-234">UserA generates a SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span><span class="sxs-lookup"><span data-stu-id="fb213-234">UserA generates a SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>
2. <span data-ttu-id="fb213-235">UserA shares the SAS with the person wanting access to the storage account - UserB, in our example.</span><span class="sxs-lookup"><span data-stu-id="fb213-235">UserA shares the SAS with the person wanting access to the storage account - UserB, in our example.</span></span>  
3. <span data-ttu-id="fb213-236">UserB uses Storage Explorer (Preview) to attach to the account belonging to UserA using the supplied SAS.</span><span class="sxs-lookup"><span data-stu-id="fb213-236">UserB uses Storage Explorer (Preview) to attach to the account belonging to UserA using the supplied SAS.</span></span>

### <a name="get-a-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="fb213-237">Get a SAS for the account you want to share</span><span class="sxs-lookup"><span data-stu-id="fb213-237">Get a SAS for the account you want to share</span></span>
1. <span data-ttu-id="fb213-238">In Storage Explorer (Preview), right-click the storage account you want share, and - from the context menu - select **Get Shared Access Signature**.</span><span class="sxs-lookup"><span data-stu-id="fb213-238">In Storage Explorer (Preview), right-click the storage account you want share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

   ![Get SAS context menu option][13]
2. <span data-ttu-id="fb213-240">On the **Shared Access Signature** dialog, specify the time frame and permissions you want for the account, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="fb213-240">On the **Shared Access Signature** dialog, specify the time frame and permissions you want for the account, and select **Create**.</span></span>

    ![Get SAS dialog][14]
3. <span data-ttu-id="fb213-242">A second **Shared Access Signature** dialog displays the SAS.</span><span class="sxs-lookup"><span data-stu-id="fb213-242">A second **Shared Access Signature** dialog displays the SAS.</span></span> <span data-ttu-id="fb213-243">Select **Copy** next to the **Connection String** to copy it to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="fb213-243">Select **Copy** next to the **Connection String** to copy it to the clipboard.</span></span> <span data-ttu-id="fb213-244">Select **Close** to dismiss the dialog.</span><span class="sxs-lookup"><span data-stu-id="fb213-244">Select **Close** to dismiss the dialog.</span></span>

### <a name="attach-to-the-shared-account-using-the-sas"></a><span data-ttu-id="fb213-245">Attach to the shared account using the SAS</span><span class="sxs-lookup"><span data-stu-id="fb213-245">Attach to the shared account using the SAS</span></span>
1. <span data-ttu-id="fb213-246">In Storage Explorer (Preview), select **Connect to Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="fb213-246">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

   ![Connect to Azure storage option][23]
2. <span data-ttu-id="fb213-248">On the **Connect to Azure Storage** dialog, specify the connection string, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb213-248">On the **Connect to Azure Storage** dialog, specify the connection string, and then select **Next**.</span></span>

   ![Connect to Azure storage dialog][24]
3. <span data-ttu-id="fb213-250">In the **Connection Summary** dialog, verify the information.</span><span class="sxs-lookup"><span data-stu-id="fb213-250">In the **Connection Summary** dialog, verify the information.</span></span> <span data-ttu-id="fb213-251">If you want to change anything, select **Back** and reenter the desired settings.</span><span class="sxs-lookup"><span data-stu-id="fb213-251">If you want to change anything, select **Back** and reenter the desired settings.</span></span> <span data-ttu-id="fb213-252">Once finished, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fb213-252">Once finished, select **Connect**.</span></span>
4. <span data-ttu-id="fb213-253">Once attached, the storage account displays with the text (SAS) appended to the account name you supplied.</span><span class="sxs-lookup"><span data-stu-id="fb213-253">Once attached, the storage account displays with the text (SAS) appended to the account name you supplied.</span></span>

   ![Result of attached to an account using SAS][17]

## <a name="attach-service-using-sas"></a><span data-ttu-id="fb213-255">Attach service using SAS</span><span class="sxs-lookup"><span data-stu-id="fb213-255">Attach service using SAS</span></span>
<span data-ttu-id="fb213-256">The section [Attach storage account using SAS](#attach-storage-account-using-sas) illustrates how an Azure subscription admin can grant temporary access to a storage account by generating (and sharing) a SAS for the storage account.</span><span class="sxs-lookup"><span data-stu-id="fb213-256">The section [Attach storage account using SAS](#attach-storage-account-using-sas) illustrates how an Azure subscription admin can grant temporary access to a storage account by generating (and sharing) a SAS for the storage account.</span></span> <span data-ttu-id="fb213-257">Similarly, a SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span><span class="sxs-lookup"><span data-stu-id="fb213-257">Similarly, a SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-a-sas-for-the-service-you-want-to-share"></a><span data-ttu-id="fb213-258">Generate a SAS for the service you want to share</span><span class="sxs-lookup"><span data-stu-id="fb213-258">Generate a SAS for the service you want to share</span></span>
<span data-ttu-id="fb213-259">In this context, a service can be a blob container, queue, or table.</span><span class="sxs-lookup"><span data-stu-id="fb213-259">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="fb213-260">The following sections explain how to generate the SAS for the listed service:</span><span class="sxs-lookup"><span data-stu-id="fb213-260">The following sections explain how to generate the SAS for the listed service:</span></span>

* [<span data-ttu-id="fb213-261">Get the SAS for a blob container</span><span class="sxs-lookup"><span data-stu-id="fb213-261">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="fb213-262">Get the SAS for a file share - *Coming soon*</span><span class="sxs-lookup"><span data-stu-id="fb213-262">Get the SAS for a file share - *Coming soon*</span></span>
* <span data-ttu-id="fb213-263">Get the SAS for a queue - *Coming soon*</span><span class="sxs-lookup"><span data-stu-id="fb213-263">Get the SAS for a queue - *Coming soon*</span></span>
* <span data-ttu-id="fb213-264">Get the SAS for a table - *Coming soon*</span><span class="sxs-lookup"><span data-stu-id="fb213-264">Get the SAS for a table - *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-using-the-sas"></a><span data-ttu-id="fb213-265">Attach to the shared account service using the SAS</span><span class="sxs-lookup"><span data-stu-id="fb213-265">Attach to the shared account service using the SAS</span></span>
1. <span data-ttu-id="fb213-266">In Storage Explorer (Preview), select **Connect to Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="fb213-266">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

   ![Connect to Azure storage option][23]
2. <span data-ttu-id="fb213-268">On the **Connect to Azure Storage** dialog, specify the SAS URI, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb213-268">On the **Connect to Azure Storage** dialog, specify the SAS URI, and then select **Next**.</span></span>

   ![Connect to Azure storage dialog][24]
3. <span data-ttu-id="fb213-270">In the **Connection Summary** dialog, verify the information.</span><span class="sxs-lookup"><span data-stu-id="fb213-270">In the **Connection Summary** dialog, verify the information.</span></span> <span data-ttu-id="fb213-271">If you want to change anything, select **Back** and reenter the desired settings.</span><span class="sxs-lookup"><span data-stu-id="fb213-271">If you want to change anything, select **Back** and reenter the desired settings.</span></span> <span data-ttu-id="fb213-272">Once finished, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fb213-272">Once finished, select **Connect**.</span></span>
4. <span data-ttu-id="fb213-273">Once attached, the newly attached service displays under the **(Service SAS)** node.</span><span class="sxs-lookup"><span data-stu-id="fb213-273">Once attached, the newly attached service displays under the **(Service SAS)** node.</span></span>

   ![Result of attaching to a shared service using SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="fb213-275">Search for storage accounts</span><span class="sxs-lookup"><span data-stu-id="fb213-275">Search for storage accounts</span></span>
<span data-ttu-id="fb213-276">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span><span class="sxs-lookup"><span data-stu-id="fb213-276">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="fb213-277">As you are typing into the search box, the left pane displays only the storage accounts that match the search value you've entered up to that point.</span><span class="sxs-lookup"><span data-stu-id="fb213-277">As you are typing into the search box, the left pane displays only the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="fb213-278">The following screen shot illustrates an example where I've searched for all storage accounts where the storage account name contains the text "tarcher".</span><span class="sxs-lookup"><span data-stu-id="fb213-278">The following screen shot illustrates an example where I've searched for all storage accounts where the storage account name contains the text "tarcher".</span></span>

![Storage account search][11]

<span data-ttu-id="fb213-280">To clear the search, select the **x** button in the search box.</span><span class="sxs-lookup"><span data-stu-id="fb213-280">To clear the search, select the **x** button in the search box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb213-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb213-281">Next steps</span></span>
* [<span data-ttu-id="fb213-282">Manage Azure blob storage resources with Storage Explorer (Preview)</span><span class="sxs-lookup"><span data-stu-id="fb213-282">Manage Azure blob storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png



























