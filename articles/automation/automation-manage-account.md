---
title: Manage Azure Automation account | Microsoft Docs
description: This article describes how to manage the configuration of your Automation account such as certificate renewal, deletion, and misconfiguration.
services: automation
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: dd62d124c8c90e92025c96188e00d1265d6e0876
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562794"
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="02afb-103">Manage Azure Automation account</span><span class="sxs-lookup"><span data-stu-id="02afb-103">Manage Azure Automation account</span></span>
<span data-ttu-id="02afb-104">At some point before your Automation account expires, you will need to renew the certificate.</span><span class="sxs-lookup"><span data-stu-id="02afb-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="02afb-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span><span class="sxs-lookup"><span data-stu-id="02afb-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="02afb-106">This section discusses how to perform these operations.</span><span class="sxs-lookup"><span data-stu-id="02afb-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="02afb-107">Self-signed certificate renewal</span><span class="sxs-lookup"><span data-stu-id="02afb-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="02afb-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span><span class="sxs-lookup"><span data-stu-id="02afb-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="02afb-109">You can renew it at any time before it expires.</span><span class="sxs-lookup"><span data-stu-id="02afb-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="02afb-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span><span class="sxs-lookup"><span data-stu-id="02afb-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="02afb-111">The certificate remains valid until its expiration date.</span><span class="sxs-lookup"><span data-stu-id="02afb-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="02afb-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="02afb-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="02afb-113">To renew the certificate, do the following:</span><span class="sxs-lookup"><span data-stu-id="02afb-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="02afb-114">In the Azure portal, open the Automation account.</span><span class="sxs-lookup"><span data-stu-id="02afb-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="02afb-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span><span class="sxs-lookup"><span data-stu-id="02afb-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Automation account properties pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="02afb-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span><span class="sxs-lookup"><span data-stu-id="02afb-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="02afb-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span><span class="sxs-lookup"><span data-stu-id="02afb-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Renew certificate for Run As account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="02afb-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="02afb-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="02afb-121">Delete a Run As or Classic Run As account</span><span class="sxs-lookup"><span data-stu-id="02afb-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="02afb-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="02afb-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="02afb-123">When you perform this action, the Automation account is retained.</span><span class="sxs-lookup"><span data-stu-id="02afb-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="02afb-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02afb-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="02afb-125">In the Azure portal, open the Automation account.</span><span class="sxs-lookup"><span data-stu-id="02afb-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="02afb-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span><span class="sxs-lookup"><span data-stu-id="02afb-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="02afb-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="02afb-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="02afb-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="02afb-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Delete Run As account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="02afb-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="02afb-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="02afb-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span><span class="sxs-lookup"><span data-stu-id="02afb-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Re-create the Automation Run As account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="02afb-133">Misconfiguration</span><span class="sxs-lookup"><span data-stu-id="02afb-133">Misconfiguration</span></span>
<span data-ttu-id="02afb-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span><span class="sxs-lookup"><span data-stu-id="02afb-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="02afb-135">The items include:</span><span class="sxs-lookup"><span data-stu-id="02afb-135">The items include:</span></span>

* <span data-ttu-id="02afb-136">Certificate asset</span><span class="sxs-lookup"><span data-stu-id="02afb-136">Certificate asset</span></span>
* <span data-ttu-id="02afb-137">Connection asset</span><span class="sxs-lookup"><span data-stu-id="02afb-137">Connection asset</span></span>
* <span data-ttu-id="02afb-138">Run As account has been removed from the contributor role</span><span class="sxs-lookup"><span data-stu-id="02afb-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="02afb-139">Service principal or application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="02afb-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="02afb-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span><span class="sxs-lookup"><span data-stu-id="02afb-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Incomplete Run As account configuration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="02afb-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span><span class="sxs-lookup"><span data-stu-id="02afb-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Incomplete Run As configuration warning message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="02afb-144">.</span><span class="sxs-lookup"><span data-stu-id="02afb-144">.</span></span>

<span data-ttu-id="02afb-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span><span class="sxs-lookup"><span data-stu-id="02afb-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02afb-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="02afb-146">Next steps</span></span>
* <span data-ttu-id="02afb-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="02afb-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="02afb-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="02afb-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="02afb-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="02afb-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>





