---
title: Azure Storage Account List
description: Manage your storage account settings using the Azure Toolkit for Eclipse
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: a99152bc00aec5302342ac00436975739ae5ff4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564202"
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="05bd1-103">Azure Storage Account List</span><span class="sxs-lookup"><span data-stu-id="05bd1-103">Azure Storage Account List</span></span>
<span data-ttu-id="05bd1-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span><span class="sxs-lookup"><span data-stu-id="05bd1-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="05bd1-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span><span class="sxs-lookup"><span data-stu-id="05bd1-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="05bd1-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="05bd1-107">The following shows the **Storage Accounts** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="05bd1-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span><span class="sxs-lookup"><span data-stu-id="05bd1-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="05bd1-109">The **JDK** tab of the **Server Configuration** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="05bd1-110">The **Server** tab of the **Server Configuration** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="05bd1-111">The **Add Component** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="05bd1-112">The **Caching** properties dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="05bd1-113">To import your storage accounts using a publish settings file</span><span class="sxs-lookup"><span data-stu-id="05bd1-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="05bd1-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>
2. <span data-ttu-id="05bd1-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="05bd1-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span><span class="sxs-lookup"><span data-stu-id="05bd1-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="05bd1-117">Then you'll be prompted to save an Azure publish settings file.</span><span class="sxs-lookup"><span data-stu-id="05bd1-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="05bd1-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span><span class="sxs-lookup"><span data-stu-id="05bd1-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>
3. <span data-ttu-id="05bd1-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>
4. <span data-ttu-id="05bd1-120">Click **OK** to close the **Import Subscription Information** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="05bd1-121">To create a new storage account</span><span class="sxs-lookup"><span data-stu-id="05bd1-121">To create a new storage account</span></span>
1. <span data-ttu-id="05bd1-122">Within the **Storage Accounts** dialog, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>
2. <span data-ttu-id="05bd1-123">Within the **Add Storage Account** dialog, click **New**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-123">Within the **Add Storage Account** dialog, click **New**.</span></span>
3. <span data-ttu-id="05bd1-124">Within the **New Storage Account** dialog, specify values for the following:</span><span class="sxs-lookup"><span data-stu-id="05bd1-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>
   * <span data-ttu-id="05bd1-125">Storage account name.</span><span class="sxs-lookup"><span data-stu-id="05bd1-125">Storage account name.</span></span>
   * <span data-ttu-id="05bd1-126">Location of the storage account.</span><span class="sxs-lookup"><span data-stu-id="05bd1-126">Location of the storage account.</span></span>
   * <span data-ttu-id="05bd1-127">Description of the storage account.</span><span class="sxs-lookup"><span data-stu-id="05bd1-127">Description of the storage account.</span></span>
   * <span data-ttu-id="05bd1-128">The subscription to which the storage account belongs.</span><span class="sxs-lookup"><span data-stu-id="05bd1-128">The subscription to which the storage account belongs.</span></span>
4. <span data-ttu-id="05bd1-129">Click **OK** to close the **New Storage Account** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="05bd1-130">It may take several minutes for your storage account to be created.</span><span class="sxs-lookup"><span data-stu-id="05bd1-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="05bd1-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span><span class="sxs-lookup"><span data-stu-id="05bd1-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="05bd1-132">To add an existing storage account to the list</span><span class="sxs-lookup"><span data-stu-id="05bd1-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="05bd1-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span><span class="sxs-lookup"><span data-stu-id="05bd1-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="05bd1-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="05bd1-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>
2. <span data-ttu-id="05bd1-135">Within the **Storage Accounts** dialog, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>
3. <span data-ttu-id="05bd1-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="05bd1-137">The account name and access key must be for an existing Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="05bd1-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="05bd1-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span><span class="sxs-lookup"><span data-stu-id="05bd1-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="05bd1-139">Your **Add Storage Account** dialog will look similar to the following.</span><span class="sxs-lookup"><span data-stu-id="05bd1-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
    ![][ic719497]
4. <span data-ttu-id="05bd1-140">Click **OK** to close the **Add Storage Account** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="05bd1-141">To modify a storage account to use a new access key</span><span class="sxs-lookup"><span data-stu-id="05bd1-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="05bd1-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>
2. <span data-ttu-id="05bd1-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span><span class="sxs-lookup"><span data-stu-id="05bd1-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>
3. <span data-ttu-id="05bd1-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span><span class="sxs-lookup"><span data-stu-id="05bd1-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="05bd1-145">To remove a storage account from the list maintained in Eclipse</span><span class="sxs-lookup"><span data-stu-id="05bd1-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="05bd1-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="05bd1-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>
2. <span data-ttu-id="05bd1-147">Click **OK** when prompted to remove the storage account.</span><span class="sxs-lookup"><span data-stu-id="05bd1-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="05bd1-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span><span class="sxs-lookup"><span data-stu-id="05bd1-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="05bd1-149">It does not remove the storage account from your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="05bd1-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="05bd1-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span><span class="sxs-lookup"><span data-stu-id="05bd1-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="05bd1-151">See Also</span><span class="sxs-lookup"><span data-stu-id="05bd1-151">See Also</span></span>
<span data-ttu-id="05bd1-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="05bd1-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="05bd1-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="05bd1-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="05bd1-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="05bd1-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="05bd1-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="05bd1-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->


