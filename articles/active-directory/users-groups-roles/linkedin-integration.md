---
title: Enable LinkedIn connections integration in Azure Active Directory | Microsoft Docs
description: Explains how to enable or disable LinkedIn account connections for Microsoft apps in Azure Active Directory
services: active-directory
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 09/11/2018
ms.author: curtand
ms.reviewer: beengen
ms.custom: it-pro
ms.openlocfilehash: 0eaa2656313ecd9b64503051265dc16285f0a1f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867639"
---
# <a name="linkedin-account-connections"></a><span data-ttu-id="087c3-103">LinkedIn account connections</span><span class="sxs-lookup"><span data-stu-id="087c3-103">LinkedIn account connections</span></span>

<span data-ttu-id="087c3-104">In this article, you can learn how to enable or disable LinkedIn account connections for your tenant in the Azure Active Directory (Azure AD) admin center.</span><span class="sxs-lookup"><span data-stu-id="087c3-104">In this article, you can learn how to enable or disable LinkedIn account connections for your tenant in the Azure Active Directory (Azure AD) admin center.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="087c3-105">The LinkedIn account connections setting is currently being rolled out to Azure AD tenants.</span><span class="sxs-lookup"><span data-stu-id="087c3-105">The LinkedIn account connections setting is currently being rolled out to Azure AD tenants.</span></span> <span data-ttu-id="087c3-106">When it is rolled out to your tenant, it is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="087c3-106">When it is rolled out to your tenant, it is enabled by default.</span></span> 
> 
> <span data-ttu-id="087c3-107">Exceptions:</span><span class="sxs-lookup"><span data-stu-id="087c3-107">Exceptions:</span></span>
> * <span data-ttu-id="087c3-108">The setting is not available for customers using Microsoft Cloud for US Government, Microsoft Cloud Germany, or Azure and Office 365 operated by 21Vianet in China.</span><span class="sxs-lookup"><span data-stu-id="087c3-108">The setting is not available for customers using Microsoft Cloud for US Government, Microsoft Cloud Germany, or Azure and Office 365 operated by 21Vianet in China.</span></span>
> * <span data-ttu-id="087c3-109">The setting is off by default for tenants provisioned in Germany.</span><span class="sxs-lookup"><span data-stu-id="087c3-109">The setting is off by default for tenants provisioned in Germany.</span></span> <span data-ttu-id="087c3-110">Note that the setting is not available for customers using Microsoft Cloud Germany.</span><span class="sxs-lookup"><span data-stu-id="087c3-110">Note that the setting is not available for customers using Microsoft Cloud Germany.</span></span>
> * <span data-ttu-id="087c3-111">The setting is off by default for tenants provisioned in France.</span><span class="sxs-lookup"><span data-stu-id="087c3-111">The setting is off by default for tenants provisioned in France.</span></span>

> <span data-ttu-id="087c3-112">The integration works only if you have it enabled *and* if you allow users to consent to apps accessing company data on their behalf.</span><span class="sxs-lookup"><span data-stu-id="087c3-112">The integration works only if you have it enabled *and* if you allow users to consent to apps accessing company data on their behalf.</span></span> <span data-ttu-id="087c3-113">For information about the consent setting, see [How to remove a user’s access to an application](https://docs.microsoft.com/azure/active-directory/application-access-assignment-how-to-remove-assignment).</span><span class="sxs-lookup"><span data-stu-id="087c3-113">For information about the consent setting, see [How to remove a user’s access to an application](https://docs.microsoft.com/azure/active-directory/application-access-assignment-how-to-remove-assignment).</span></span>

## <a name="enable-or-disable-linkedin-account-connections-for-your-tenant-in-the-azure-portal"></a><span data-ttu-id="087c3-114">Enable or disable LinkedIn account connections for your tenant in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="087c3-114">Enable or disable LinkedIn account connections for your tenant in the Azure portal</span></span>

<span data-ttu-id="087c3-115">You can enable or disable LinkedIn account connections for your entire tenant or for only selected users in your tenant.</span><span class="sxs-lookup"><span data-stu-id="087c3-115">You can enable or disable LinkedIn account connections for your entire tenant or for only selected users in your tenant.</span></span>

1. <span data-ttu-id="087c3-116">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com/) with an account that's a global admin for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="087c3-116">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com/) with an account that's a global admin for the Azure AD tenant.</span></span>
2. <span data-ttu-id="087c3-117">Select **Users**.</span><span class="sxs-lookup"><span data-stu-id="087c3-117">Select **Users**.</span></span>
3. <span data-ttu-id="087c3-118">On the **Users** blade, select **User settings**.</span><span class="sxs-lookup"><span data-stu-id="087c3-118">On the **Users** blade, select **User settings**.</span></span>
4. <span data-ttu-id="087c3-119">Under **LinkedIn account connections**:</span><span class="sxs-lookup"><span data-stu-id="087c3-119">Under **LinkedIn account connections**:</span></span>
  * <span data-ttu-id="087c3-120">Select **Yes** to enable LinkedIn account connections for all users in your tenant</span><span class="sxs-lookup"><span data-stu-id="087c3-120">Select **Yes** to enable LinkedIn account connections for all users in your tenant</span></span>
  * <span data-ttu-id="087c3-121">Select **Selected** to enable LinkedIn account connections for only selected tenant users</span><span class="sxs-lookup"><span data-stu-id="087c3-121">Select **Selected** to enable LinkedIn account connections for only selected tenant users</span></span>
  * <span data-ttu-id="087c3-122">Select **No** to disable LinkedIn account connections for all users ![Enabling LinkedIn account connections](./media/linkedin-integration/linkedin-integration.png)</span><span class="sxs-lookup"><span data-stu-id="087c3-122">Select **No** to disable LinkedIn account connections for all users ![Enabling LinkedIn account connections](./media/linkedin-integration/linkedin-integration.png)</span></span>
5. <span data-ttu-id="087c3-123">Save your settings when you're done by selecting **Save**.</span><span class="sxs-lookup"><span data-stu-id="087c3-123">Save your settings when you're done by selecting **Save**.</span></span>

## <a name="enable-or-disable-linkedin-account-connections-for-your-tenant-using-group-policy"></a><span data-ttu-id="087c3-124">Enable or disable LinkedIn account connections for your tenant using Group Policy</span><span class="sxs-lookup"><span data-stu-id="087c3-124">Enable or disable LinkedIn account connections for your tenant using Group Policy</span></span>

1. <span data-ttu-id="087c3-125">Download the [Office 2016 Administrative Template files (ADMX/ADML)](https://www.microsoft.com/download/details.aspx?id=49030)</span><span class="sxs-lookup"><span data-stu-id="087c3-125">Download the [Office 2016 Administrative Template files (ADMX/ADML)](https://www.microsoft.com/download/details.aspx?id=49030)</span></span>
2. <span data-ttu-id="087c3-126">Extract the **ADMX** files and copy them to your central store.</span><span class="sxs-lookup"><span data-stu-id="087c3-126">Extract the **ADMX** files and copy them to your central store.</span></span>
3. <span data-ttu-id="087c3-127">Open Group Policy Management.</span><span class="sxs-lookup"><span data-stu-id="087c3-127">Open Group Policy Management.</span></span>
4. <span data-ttu-id="087c3-128">Create a Group Policy Object with the following setting: **User Configuration** > **Administrative Templates** > **Microsoft Office 2016** > **Miscellaneous** > **Show LinkedIn features in Office applications**.</span><span class="sxs-lookup"><span data-stu-id="087c3-128">Create a Group Policy Object with the following setting: **User Configuration** > **Administrative Templates** > **Microsoft Office 2016** > **Miscellaneous** > **Show LinkedIn features in Office applications**.</span></span>
5. <span data-ttu-id="087c3-129">Select **Enabled** or **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="087c3-129">Select **Enabled** or **Disabled**.</span></span>
  
 <span data-ttu-id="087c3-130">State</span><span class="sxs-lookup"><span data-stu-id="087c3-130">State</span></span> | <span data-ttu-id="087c3-131">Effect</span><span class="sxs-lookup"><span data-stu-id="087c3-131">Effect</span></span>
------ | ------
<span data-ttu-id="087c3-132">**Enabled**</span><span class="sxs-lookup"><span data-stu-id="087c3-132">**Enabled**</span></span> | <span data-ttu-id="087c3-133">The **Show LinkedIn features in Office applications** setting in Office 2016 Options is enabled.</span><span class="sxs-lookup"><span data-stu-id="087c3-133">The **Show LinkedIn features in Office applications** setting in Office 2016 Options is enabled.</span></span> <span data-ttu-id="087c3-134">Users in your organization can use LinkedIn features in their Office applications.</span><span class="sxs-lookup"><span data-stu-id="087c3-134">Users in your organization can use LinkedIn features in their Office applications.</span></span>
 <span data-ttu-id="087c3-135">**Disabled**</span><span class="sxs-lookup"><span data-stu-id="087c3-135">**Disabled**</span></span> | <span data-ttu-id="087c3-136">The **Show LinkedIn features in Office applications** setting in Office 2016 Options is disabled and end users can't change this setting.</span><span class="sxs-lookup"><span data-stu-id="087c3-136">The **Show LinkedIn features in Office applications** setting in Office 2016 Options is disabled and end users can't change this setting.</span></span> <span data-ttu-id="087c3-137">Users in your organization can't use LinkedIn features in their Office 2016 applications.</span><span class="sxs-lookup"><span data-stu-id="087c3-137">Users in your organization can't use LinkedIn features in their Office 2016 applications.</span></span>

<span data-ttu-id="087c3-138">This group policy affects only Office 2016 apps for a local computer.</span><span class="sxs-lookup"><span data-stu-id="087c3-138">This group policy affects only Office 2016 apps for a local computer.</span></span> <span data-ttu-id="087c3-139">Users can see LinkedIn features in profile cards throughout Office 365 even if they disable LinkedIn in their Office 2016 apps.</span><span class="sxs-lookup"><span data-stu-id="087c3-139">Users can see LinkedIn features in profile cards throughout Office 365 even if they disable LinkedIn in their Office 2016 apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="087c3-140">Learn more</span><span class="sxs-lookup"><span data-stu-id="087c3-140">Learn more</span></span>

* [<span data-ttu-id="087c3-141">Integrate LinkedIn in your organization</span><span class="sxs-lookup"><span data-stu-id="087c3-141">Integrate LinkedIn in your organization</span></span>](linkedin-user-consent.md)

* [<span data-ttu-id="087c3-142">LinkedIn information and features in your Microsoft apps</span><span class="sxs-lookup"><span data-stu-id="087c3-142">LinkedIn information and features in your Microsoft apps</span></span>](https://go.microsoft.com/fwlink/?linkid=850740)

* [<span data-ttu-id="087c3-143">LinkedIn help center</span><span class="sxs-lookup"><span data-stu-id="087c3-143">LinkedIn help center</span></span>](https://www.linkedin.com/help/linkedin)

## <a name="next-steps"></a><span data-ttu-id="087c3-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="087c3-144">Next steps</span></span>
<span data-ttu-id="087c3-145">Use the following link to see your current LinkedIn account connections setting in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="087c3-145">Use the following link to see your current LinkedIn account connections setting in the Azure portal:</span></span>

[<span data-ttu-id="087c3-146">Configure LinkedIn account connections</span><span class="sxs-lookup"><span data-stu-id="087c3-146">Configure LinkedIn account connections</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/UserSettings) 