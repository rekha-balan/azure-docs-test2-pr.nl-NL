---
title: Connect storage explorer to an Azure Stack subscription  or a storage account | Microsoft Docs
description: Learn how to connect storage explorer to an  Azure Stack subscription
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2018
ms.author: mabrigg
ms.reviewer: xiaofmao
ms.openlocfilehash: 2f974b7773e7a4cbc0eda32a267bb5ab939644d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866075"
---
# <a name="connect-storage-explorer-to-an-azure-stack-subscription-or-a-storage-account"></a><span data-ttu-id="9bc2b-103">Connect storage explorer to an Azure Stack subscription or a storage account</span><span class="sxs-lookup"><span data-stu-id="9bc2b-103">Connect storage explorer to an Azure Stack subscription or a storage account</span></span>

<span data-ttu-id="9bc2b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="9bc2b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="9bc2b-105">In this article, you'll learn how to connect to your Azure Stack subscriptions and storage accounts using storage explorer.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-105">In this article, you'll learn how to connect to your Azure Stack subscriptions and storage accounts using storage explorer.</span></span> <span data-ttu-id="9bc2b-106">Azure storage explorer is a standalone app that enables you to easily work with Azure Stack storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-106">Azure storage explorer is a standalone app that enables you to easily work with Azure Stack storage data on Windows, macOS, and Linux.</span></span>

> [!NOTE]  
> <span data-ttu-id="9bc2b-107">There are several tools available to move data to and from Azure Stack storage.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-107">There are several tools available to move data to and from Azure Stack storage.</span></span> <span data-ttu-id="9bc2b-108">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="9bc2b-108">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="9bc2b-109">If you haven't installed storage explorer yet, [download storage explorer](http://www.storageexplorer.com/) and install it.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-109">If you haven't installed storage explorer yet, [download storage explorer](http://www.storageexplorer.com/) and install it.</span></span>

<span data-ttu-id="9bc2b-110">After you connect to an Azure Stack subscription or a storage account, you can use the [Azure storage explorer articles](../../vs-azure-tools-storage-manage-with-storage-explorer.md) to work with your Azure Stack data.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-110">After you connect to an Azure Stack subscription or a storage account, you can use the [Azure storage explorer articles](../../vs-azure-tools-storage-manage-with-storage-explorer.md) to work with your Azure Stack data.</span></span> 

## <a name="prepare-for-connecting-to-azure-stack"></a><span data-ttu-id="9bc2b-111">Prepare for connecting to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9bc2b-111">Prepare for connecting to Azure Stack</span></span>

<span data-ttu-id="9bc2b-112">You need direct access to the Azure Stack or a VPN connection for storage explorer to access the Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-112">You need direct access to the Azure Stack or a VPN connection for storage explorer to access the Azure Stack subscription.</span></span> <span data-ttu-id="9bc2b-113">To learn how to set up a VPN connection to Azure Stack, see [Connect to Azure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="9bc2b-113">To learn how to set up a VPN connection to Azure Stack, see [Connect to Azure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="9bc2b-114">For the Azure Stack Development Kit, you need to export the Azure Stack authority root certificate.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-114">For the Azure Stack Development Kit, you need to export the Azure Stack authority root certificate.</span></span>

### <a name="export-and-then-import-the-azure-stack-certificate"></a><span data-ttu-id="9bc2b-115">Export and then import the Azure Stack certificate</span><span class="sxs-lookup"><span data-stu-id="9bc2b-115">Export and then import the Azure Stack certificate</span></span>

1. <span data-ttu-id="9bc2b-116">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-116">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection to Azure Stack.</span></span> 

2. <span data-ttu-id="9bc2b-117">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** to manage **My user account**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-117">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** to manage **My user account**.</span></span>

3. <span data-ttu-id="9bc2b-118">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-118">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Load the Azure Stack root certificate through mmc.exe](./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png)

4. <span data-ttu-id="9bc2b-120">Right-click the certificate, select **All Tasks** > **Export**, and then follow the instructions to export the certificate with **Base-64 encoded X.509 (.CER)**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-120">Right-click the certificate, select **All Tasks** > **Export**, and then follow the instructions to export the certificate with **Base-64 encoded X.509 (.CER)**.</span></span>

    <span data-ttu-id="9bc2b-121">The exported certificate will be used in the next step.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-121">The exported certificate will be used in the next step.</span></span>

5. <span data-ttu-id="9bc2b-122">Start storage explorer, and if you see the **Connect to Azure Storage** dialog box, cancel it.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-122">Start storage explorer, and if you see the **Connect to Azure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="9bc2b-123">On the **Edit** menu, point to **SSL Certificates**, and then select **Import Certificates**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-123">On the **Edit** menu, point to **SSL Certificates**, and then select **Import Certificates**.</span></span> <span data-ttu-id="9bc2b-124">Use the file picker dialog box to find and open the certificate that you exported in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-124">Use the file picker dialog box to find and open the certificate that you exported in the previous step.</span></span>

    <span data-ttu-id="9bc2b-125">After importing the certificate, you're prompted to restart storage explorer.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-125">After importing the certificate, you're prompted to restart storage explorer.</span></span>

    ![Import the certificate into storage explorer](./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png)

7. <span data-ttu-id="9bc2b-127">After storage explorer restarts, select the **Edit** menu, and check to see if **Target Azure Stack** is selected.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-127">After storage explorer restarts, select the **Edit** menu, and check to see if **Target Azure Stack** is selected.</span></span> <span data-ttu-id="9bc2b-128">If it isn't, select **Target Azure Stack**, and then restart storage explorer for the change to take effect.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-128">If it isn't, select **Target Azure Stack**, and then restart storage explorer for the change to take effect.</span></span> <span data-ttu-id="9bc2b-129">This configuration is required for compatibility with your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-129">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![Ensure Target Azure Stack is selected](./media/azure-stack-storage-connect-se/target-azure-stack.png)

## <a name="connect-to-an-azure-stack-subscription-with-azure-ad"></a><span data-ttu-id="9bc2b-131">Connect to an Azure Stack subscription with Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc2b-131">Connect to an Azure Stack subscription with Azure AD</span></span>

<span data-ttu-id="9bc2b-132">Use the following steps to connect storage explorer to an Azure Stack subscription, which belongs to an Azure Active Directory (Azure AD) account.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-132">Use the following steps to connect storage explorer to an Azure Stack subscription, which belongs to an Azure Active Directory (Azure AD) account.</span></span>

1. <span data-ttu-id="9bc2b-133">In the left pane of storage explorer, select **Manage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-133">In the left pane of storage explorer, select **Manage Accounts**.</span></span> 
    <span data-ttu-id="9bc2b-134">All the Microsoft subscription that you signed in are displayed.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-134">All the Microsoft subscription that you signed in are displayed.</span></span>

2. <span data-ttu-id="9bc2b-135">To connect to the Azure Stack subscription, select **Add an account**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-135">To connect to the Azure Stack subscription, select **Add an account**.</span></span>

    ![Add an Azure Stack account](./media/azure-stack-storage-connect-se/add-azure-stack-account.png)

3. <span data-ttu-id="9bc2b-137">In the Connect to Azure Storage dialog box, under **Azure environment**, select **Azure** or **Azure China**, which depends on the Azure Stack account that is being used, select **Sign in** to sign in with the Azure Stack account associated with at least one active Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-137">In the Connect to Azure Storage dialog box, under **Azure environment**, select **Azure** or **Azure China**, which depends on the Azure Stack account that is being used, select **Sign in** to sign in with the Azure Stack account associated with at least one active Azure Stack subscription.</span></span>

    ![Connect to Azure storage](./media/azure-stack-storage-connect-se/azure-stack-connect-to-storage.png)

4. <span data-ttu-id="9bc2b-139">After you successfully sign in with an Azure Stack account, the left pane is populated with the Azure Stack subscriptions associated with that account.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-139">After you successfully sign in with an Azure Stack account, the left pane is populated with the Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="9bc2b-140">Select the Azure Stack subscriptions that you want to work with, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-140">Select the Azure Stack subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="9bc2b-141">(Selecting or clearing the **All subscriptions** check box toggles selecting all or none of the listed Azure Stack subscriptions.)</span><span class="sxs-lookup"><span data-stu-id="9bc2b-141">(Selecting or clearing the **All subscriptions** check box toggles selecting all or none of the listed Azure Stack subscriptions.)</span></span>

    ![Select the Azure Stack subscriptions after filling out the Custom Cloud Environment dialog box](./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png)

    <span data-ttu-id="9bc2b-143">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-143">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

    ![List of storage accounts including Azure Stack subscription accounts](./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png)

## <a name="connect-to-an-azure-stack-subscription-with-ad-fs-account"></a><span data-ttu-id="9bc2b-145">Connect to an Azure Stack subscription with AD FS account</span><span class="sxs-lookup"><span data-stu-id="9bc2b-145">Connect to an Azure Stack subscription with AD FS account</span></span>

> [!Note]  
> <span data-ttu-id="9bc2b-146">The Azure Federated Service (AD FS) sign-in experience supports Storage Explorer 1.2.0 or newer versions with Azure Stack 1804 or newer update.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-146">The Azure Federated Service (AD FS) sign-in experience supports Storage Explorer 1.2.0 or newer versions with Azure Stack 1804 or newer update.</span></span>
<span data-ttu-id="9bc2b-147">Use the following steps to connect storage explorer to an Azure Stack subscription which belongs to an AD FS account.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-147">Use the following steps to connect storage explorer to an Azure Stack subscription which belongs to an AD FS account.</span></span>

1. <span data-ttu-id="9bc2b-148">Select **Manage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-148">Select **Manage Accounts**.</span></span> <span data-ttu-id="9bc2b-149">The explorer lists the Microsoft subscriptions that you signed in to.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-149">The explorer lists the Microsoft subscriptions that you signed in to.</span></span>
2. <span data-ttu-id="9bc2b-150">Select **Add an account** to connect to the Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-150">Select **Add an account** to connect to the Azure Stack subscription.</span></span>

    ![Add an account](media/azure-stack-storage-connect-se/add-an-account.png)

3. <span data-ttu-id="9bc2b-152">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-152">Select **Next**.</span></span> <span data-ttu-id="9bc2b-153">In the Connect to Azure Storage dialog box, under **Azure environment**, select **Use Custom Environment**, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-153">In the Connect to Azure Storage dialog box, under **Azure environment**, select **Use Custom Environment**, then click **Next**.</span></span>

    ![Connect to Azure Storage](media/azure-stack-storage-connect-se/connect-to-azure-storage.png)

4. <span data-ttu-id="9bc2b-155">Enter the required information of Azure Stack custom environment.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-155">Enter the required information of Azure Stack custom environment.</span></span> 

    | <span data-ttu-id="9bc2b-156">Field</span><span class="sxs-lookup"><span data-stu-id="9bc2b-156">Field</span></span> | <span data-ttu-id="9bc2b-157">Notes</span><span class="sxs-lookup"><span data-stu-id="9bc2b-157">Notes</span></span> |
    | ---   | ---   |
    | <span data-ttu-id="9bc2b-158">Environment name</span><span class="sxs-lookup"><span data-stu-id="9bc2b-158">Environment name</span></span> | <span data-ttu-id="9bc2b-159">The field can be customized by user.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-159">The field can be customized by user.</span></span> |
    | <span data-ttu-id="9bc2b-160">Azure Resource Manager endpoint</span><span class="sxs-lookup"><span data-stu-id="9bc2b-160">Azure Resource Manager endpoint</span></span> | <span data-ttu-id="9bc2b-161">The samples of Azure Resource Manager resource endpoints of Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-161">The samples of Azure Resource Manager resource endpoints of Azure Stack Development Kit.</span></span><br><span data-ttu-id="9bc2b-162">For operators: https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="9bc2b-162">For operators: https://adminmanagement.local.azurestack.external</span></span> <br> <span data-ttu-id="9bc2b-163">For users: https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="9bc2b-163">For users: https://management.local.azurestack.external</span></span> |

    <span data-ttu-id="9bc2b-164">If you are working on Azure Stack integrated system and don't know your management endpoint, contact your operator.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-164">If you are working on Azure Stack integrated system and don't know your management endpoint, contact your operator.</span></span>

    ![Add an account](./media/azure-stack-storage-connect-se/custom-environments.png)

5. <span data-ttu-id="9bc2b-166">Select **Sign in**, to connect to the Azure Stack account that associated with at least one active Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-166">Select **Sign in**, to connect to the Azure Stack account that associated with at least one active Azure Stack subscription.</span></span>



6. <span data-ttu-id="9bc2b-167">Select the Azure Stack subscriptions that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-167">Select the Azure Stack subscriptions that you want to work with.</span></span> <span data-ttu-id="9bc2b-168">Select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-168">Select **Apply**.</span></span>

    ![Account management](./media/azure-stack-storage-connect-se/account-management.png)

    <span data-ttu-id="9bc2b-170">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-170">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

    ![List of associated subscriptions](./media/azure-stack-storage-connect-se/list-of-associated-subscriptions.png)

## <a name="connect-to-an-azure-stack-storage-account"></a><span data-ttu-id="9bc2b-172">Connect to an Azure Stack storage account</span><span class="sxs-lookup"><span data-stu-id="9bc2b-172">Connect to an Azure Stack storage account</span></span>

<span data-ttu-id="9bc2b-173">You can also connect to an Azure Stack storage account using storage account name and key pair.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-173">You can also connect to an Azure Stack storage account using storage account name and key pair.</span></span>

1. <span data-ttu-id="9bc2b-174">In the left pane of storage explorer, select Manage Accounts.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-174">In the left pane of storage explorer, select Manage Accounts.</span></span> <span data-ttu-id="9bc2b-175">All the Microsoft accounts that you signed in are displayed.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-175">All the Microsoft accounts that you signed in are displayed.</span></span>

    ![Add an account](./media/azure-stack-storage-connect-se/azure-stack-sub-add-an-account.png)

2. <span data-ttu-id="9bc2b-177">To connect to the Azure Stack subscription, select **Add an account**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-177">To connect to the Azure Stack subscription, select **Add an account**.</span></span>

    ![Add an account](./media/azure-stack-storage-connect-se/azure-stack-use-a-storage-and-key.png)

3. <span data-ttu-id="9bc2b-179">In the Connect to Azure Storage dialog box, select **Use a storage account name and key**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-179">In the Connect to Azure Storage dialog box, select **Use a storage account name and key**.</span></span>

4. <span data-ttu-id="9bc2b-180">Input your account name in the **Account name**, paste account key into the **Account key** text box, select **Other (enter below)** in **Storage endpoints domain** and input the Azure Stack endpoint.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-180">Input your account name in the **Account name**, paste account key into the **Account key** text box, select **Other (enter below)** in **Storage endpoints domain** and input the Azure Stack endpoint.</span></span>

    <span data-ttu-id="9bc2b-181">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-181">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span> <span data-ttu-id="9bc2b-182">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-182">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span> <span data-ttu-id="9bc2b-183">Contact your cloud administrator if you’re not sure about your endpoint.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-183">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

    ![Attach name and key](./media/azure-stack-storage-connect-se/azure-stack-attach-name-and-key.png)

5. <span data-ttu-id="9bc2b-185">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-185">Select **Connect**.</span></span>
6. <span data-ttu-id="9bc2b-186">After the storage account is successfully attached, the storage account is displayed with (**External, Other**) appended to its name.</span><span class="sxs-lookup"><span data-stu-id="9bc2b-186">After the storage account is successfully attached, the storage account is displayed with (**External, Other**) appended to its name.</span></span>

    ![VMWINDISK](./media/azure-stack-storage-connect-se/azure-stack-vmwindisk.png)

## <a name="next-steps"></a><span data-ttu-id="9bc2b-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bc2b-188">Next steps</span></span>

* [<span data-ttu-id="9bc2b-189">Get started with storage explorer</span><span class="sxs-lookup"><span data-stu-id="9bc2b-189">Get started with storage explorer</span></span>](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="9bc2b-190">Azure Stack storage: differences and considerations</span><span class="sxs-lookup"><span data-stu-id="9bc2b-190">Azure Stack storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* <span data-ttu-id="9bc2b-191">To learn more about Azure storage, see [Introduction to Microsoft Azure storage](../../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="9bc2b-191">To learn more about Azure storage, see [Introduction to Microsoft Azure storage](../../storage/common/storage-introduction.md)</span></span>
