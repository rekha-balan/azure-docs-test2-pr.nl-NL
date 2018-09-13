---
title: 'Tutorial: Configure Workday for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Workday.
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: mtillman
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/18/2018
ms.author: asmalser
ms.openlocfilehash: 930ca49a63e34214ec197d8dd37f38361b34fe90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867640"
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-preview"></a><span data-ttu-id="91f8a-103">Tutorial: Configure Workday for automatic user provisioning (preview)</span><span class="sxs-lookup"><span data-stu-id="91f8a-103">Tutorial: Configure Workday for automatic user provisioning (preview)</span></span>

<span data-ttu-id="91f8a-104">The objective of this tutorial is to show you the steps you need to perform to import people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes to Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-104">The objective of this tutorial is to show you the steps you need to perform to import people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes to Workday.</span></span>

## <a name="overview"></a><span data-ttu-id="91f8a-105">Overview</span><span class="sxs-lookup"><span data-stu-id="91f8a-105">Overview</span></span>

<span data-ttu-id="91f8a-106">The [Azure Active Directory user provisioning service](../manage-apps/user-provisioning.md) integrates with the [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order to provision user accounts.</span><span class="sxs-lookup"><span data-stu-id="91f8a-106">The [Azure Active Directory user provisioning service](../manage-apps/user-provisioning.md) integrates with the [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order to provision user accounts.</span></span> <span data-ttu-id="91f8a-107">Azure AD uses this connection to enable the following user provisioning workflows:</span><span class="sxs-lookup"><span data-stu-id="91f8a-107">Azure AD uses this connection to enable the following user provisioning workflows:</span></span>

* <span data-ttu-id="91f8a-108">**Provisioning users to Active Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span><span class="sxs-lookup"><span data-stu-id="91f8a-108">**Provisioning users to Active Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span></span>

* <span data-ttu-id="91f8a-109">**Provisioning cloud-only users to Azure Active Directory** - In scenarios where on-premises Active Directory is not used, users can be provisioned directly from Workday to Azure Active Directory using the Azure AD user provisioning service.</span><span class="sxs-lookup"><span data-stu-id="91f8a-109">**Provisioning cloud-only users to Azure Active Directory** - In scenarios where on-premises Active Directory is not used, users can be provisioned directly from Workday to Azure Active Directory using the Azure AD user provisioning service.</span></span> 

* <span data-ttu-id="91f8a-110">**Writeback of email addresses to Workday** - The Azure AD user provisioning service can write the email addresses of Azure AD users  back to Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-110">**Writeback of email addresses to Workday** - The Azure AD user provisioning service can write the email addresses of Azure AD users  back to Workday.</span></span> 

### <a name="what-human-resources-scenarios-does-it-cover"></a><span data-ttu-id="91f8a-111">What human resources scenarios does it cover?</span><span class="sxs-lookup"><span data-stu-id="91f8a-111">What human resources scenarios does it cover?</span></span>

<span data-ttu-id="91f8a-112">The Workday user provisioning workflows supported by the Azure AD user provisioning service enable automation of the following human resources and identity lifecycle management scenarios:</span><span class="sxs-lookup"><span data-stu-id="91f8a-112">The Workday user provisioning workflows supported by the Azure AD user provisioning service enable automation of the following human resources and identity lifecycle management scenarios:</span></span>

* <span data-ttu-id="91f8a-113">**Hiring new employees** - When a new employee is added to Workday, a user account is automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md), with write-back of the email address to Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-113">**Hiring new employees** - When a new employee is added to Workday, a user account is automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md), with write-back of the email address to Workday.</span></span>

* <span data-ttu-id="91f8a-114">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-114">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md).</span></span>

* <span data-ttu-id="91f8a-115">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-115">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md).</span></span>

* <span data-ttu-id="91f8a-116">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) to Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-116">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) to Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](../manage-apps/user-provisioning.md).</span></span>

### <a name="who-is-this-user-provisioning-solution-best-suited-for"></a><span data-ttu-id="91f8a-117">Who is this user provisioning solution best suited for?</span><span class="sxs-lookup"><span data-stu-id="91f8a-117">Who is this user provisioning solution best suited for?</span></span>

<span data-ttu-id="91f8a-118">This Workday user provisioning solution is presently in public preview, and is ideally suited for:</span><span class="sxs-lookup"><span data-stu-id="91f8a-118">This Workday user provisioning solution is presently in public preview, and is ideally suited for:</span></span>

* <span data-ttu-id="91f8a-119">Organizations that desire a pre-built, cloud-based solution for Workday user provisioning</span><span class="sxs-lookup"><span data-stu-id="91f8a-119">Organizations that desire a pre-built, cloud-based solution for Workday user provisioning</span></span>

* <span data-ttu-id="91f8a-120">Organizations that require direct user provisioning from Workday to Active Directory, or Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f8a-120">Organizations that require direct user provisioning from Workday to Active Directory, or Azure Active Directory</span></span>

* <span data-ttu-id="91f8a-121">Organizations that require users to be provisioned using data obtained from the Workday HCM module (see [Get_Workers](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html))</span><span class="sxs-lookup"><span data-stu-id="91f8a-121">Organizations that require users to be provisioned using data obtained from the Workday HCM module (see [Get_Workers](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html))</span></span>

* <span data-ttu-id="91f8a-122">Organizations that require joining, moving, and leaving users to be synced to one or more Active Directory Forests, Domains, and OUs based only on change information detected in the Workday HCM module (see [Get_Workers](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html))</span><span class="sxs-lookup"><span data-stu-id="91f8a-122">Organizations that require joining, moving, and leaving users to be synced to one or more Active Directory Forests, Domains, and OUs based only on change information detected in the Workday HCM module (see [Get_Workers](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html))</span></span>

* <span data-ttu-id="91f8a-123">Organizations using Office 365 for email</span><span class="sxs-lookup"><span data-stu-id="91f8a-123">Organizations using Office 365 for email</span></span>

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-hybrid-note.md)]

## <a name="planning-your-solution"></a><span data-ttu-id="91f8a-124">Planning your solution</span><span class="sxs-lookup"><span data-stu-id="91f8a-124">Planning your solution</span></span>

<span data-ttu-id="91f8a-125">Before beginning your Workday integration, check the prerequisites below and read the following guidance on how to match your current Active Directory architecture and user provisioning requirements with the solution(s) provided by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-125">Before beginning your Workday integration, check the prerequisites below and read the following guidance on how to match your current Active Directory architecture and user provisioning requirements with the solution(s) provided by Azure Active Directory.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="91f8a-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91f8a-126">Prerequisites</span></span>

<span data-ttu-id="91f8a-127">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="91f8a-127">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="91f8a-128">A valid Azure AD Premium P1 subscription with global administrator access</span><span class="sxs-lookup"><span data-stu-id="91f8a-128">A valid Azure AD Premium P1 subscription with global administrator access</span></span>
* <span data-ttu-id="91f8a-129">A Workday implementation tenant for testing and integration purposes</span><span class="sxs-lookup"><span data-stu-id="91f8a-129">A Workday implementation tenant for testing and integration purposes</span></span>
* <span data-ttu-id="91f8a-130">Administrator permissions in Workday to create a system integration user, and make changes to test employee data for testing purposes</span><span class="sxs-lookup"><span data-stu-id="91f8a-130">Administrator permissions in Workday to create a system integration user, and make changes to test employee data for testing purposes</span></span>
* <span data-ttu-id="91f8a-131">For user provisioning to Active Directory, a domain-joined server running Windows Service 2012 or greater is required to host the [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span><span class="sxs-lookup"><span data-stu-id="91f8a-131">For user provisioning to Active Directory, a domain-joined server running Windows Service 2012 or greater is required to host the [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span></span>
* <span data-ttu-id="91f8a-132">[Azure AD Connect](../connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span><span class="sxs-lookup"><span data-stu-id="91f8a-132">[Azure AD Connect](../connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span></span>

### <a name="solution-architecture"></a><span data-ttu-id="91f8a-133">Solution architecture</span><span class="sxs-lookup"><span data-stu-id="91f8a-133">Solution architecture</span></span>

<span data-ttu-id="91f8a-134">Azure AD provides a rich set of provisioning connectors to help you solve provisioning and identity life cycle management from Workday to Active Directory, Azure AD, SaaS apps, and beyond.</span><span class="sxs-lookup"><span data-stu-id="91f8a-134">Azure AD provides a rich set of provisioning connectors to help you solve provisioning and identity life cycle management from Workday to Active Directory, Azure AD, SaaS apps, and beyond.</span></span> <span data-ttu-id="91f8a-135">Which features you will use and how you set up the solution will vary depending on your organization's environment and requirements.</span><span class="sxs-lookup"><span data-stu-id="91f8a-135">Which features you will use and how you set up the solution will vary depending on your organization's environment and requirements.</span></span> <span data-ttu-id="91f8a-136">As a first step, take stock of how many of the following are present and deployed in your organization:</span><span class="sxs-lookup"><span data-stu-id="91f8a-136">As a first step, take stock of how many of the following are present and deployed in your organization:</span></span>

* <span data-ttu-id="91f8a-137">How many Active Directory Forests are in use?</span><span class="sxs-lookup"><span data-stu-id="91f8a-137">How many Active Directory Forests are in use?</span></span>
* <span data-ttu-id="91f8a-138">How many Active Directory Domains are in use?</span><span class="sxs-lookup"><span data-stu-id="91f8a-138">How many Active Directory Domains are in use?</span></span>
* <span data-ttu-id="91f8a-139">How many Active Directory Organizational Units (OUs) are in use?</span><span class="sxs-lookup"><span data-stu-id="91f8a-139">How many Active Directory Organizational Units (OUs) are in use?</span></span>
* <span data-ttu-id="91f8a-140">How many Azure Active Directory tenants are in use?</span><span class="sxs-lookup"><span data-stu-id="91f8a-140">How many Azure Active Directory tenants are in use?</span></span>
* <span data-ttu-id="91f8a-141">Are there users who need to be provisioned to both Active Directory and Azure Active Directory (for example "hybrid" users)?</span><span class="sxs-lookup"><span data-stu-id="91f8a-141">Are there users who need to be provisioned to both Active Directory and Azure Active Directory (for example "hybrid" users)?</span></span>
* <span data-ttu-id="91f8a-142">Are there users who need to be provisioned to Azure Active Directory, but not Active Directory (for example "cloud-only" users)?</span><span class="sxs-lookup"><span data-stu-id="91f8a-142">Are there users who need to be provisioned to Azure Active Directory, but not Active Directory (for example "cloud-only" users)?</span></span>
* <span data-ttu-id="91f8a-143">Do user email addresses need to be written back to Workday?</span><span class="sxs-lookup"><span data-stu-id="91f8a-143">Do user email addresses need to be written back to Workday?</span></span>

<span data-ttu-id="91f8a-144">Once you have answers to these questions, you can plan your Workday provisioning deployment by following the guidance below.</span><span class="sxs-lookup"><span data-stu-id="91f8a-144">Once you have answers to these questions, you can plan your Workday provisioning deployment by following the guidance below.</span></span>

#### <a name="using-provisioning-connector-apps"></a><span data-ttu-id="91f8a-145">Using provisioning connector apps</span><span class="sxs-lookup"><span data-stu-id="91f8a-145">Using provisioning connector apps</span></span>

<span data-ttu-id="91f8a-146">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="91f8a-146">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span></span>

<span data-ttu-id="91f8a-147">A single provisioning connector interfaces with the API of a single source system, and helps provision data to a single target system.</span><span class="sxs-lookup"><span data-stu-id="91f8a-147">A single provisioning connector interfaces with the API of a single source system, and helps provision data to a single target system.</span></span> <span data-ttu-id="91f8a-148">Most provisioning connectors that Azure AD supports are for a single source and target system (for example, Azure AD to ServiceNow), and can be set up by adding the app in question from the Azure AD app gallery (for example, ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="91f8a-148">Most provisioning connectors that Azure AD supports are for a single source and target system (for example, Azure AD to ServiceNow), and can be set up by adding the app in question from the Azure AD app gallery (for example, ServiceNow).</span></span>

<span data-ttu-id="91f8a-149">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="91f8a-149">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span></span>

| <span data-ttu-id="91f8a-150">Source System</span><span class="sxs-lookup"><span data-stu-id="91f8a-150">Source System</span></span> | <span data-ttu-id="91f8a-151">Target System</span><span class="sxs-lookup"><span data-stu-id="91f8a-151">Target System</span></span> |
| ---------- | ---------- |
| <span data-ttu-id="91f8a-152">Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="91f8a-152">Azure AD tenant</span></span> | <span data-ttu-id="91f8a-153">SaaS application</span><span class="sxs-lookup"><span data-stu-id="91f8a-153">SaaS application</span></span> |

<span data-ttu-id="91f8a-154">However, when working with Workday and Active Directory, there are multiple source and target systems to be considered:</span><span class="sxs-lookup"><span data-stu-id="91f8a-154">However, when working with Workday and Active Directory, there are multiple source and target systems to be considered:</span></span>

| <span data-ttu-id="91f8a-155">Source System</span><span class="sxs-lookup"><span data-stu-id="91f8a-155">Source System</span></span> | <span data-ttu-id="91f8a-156">Target System</span><span class="sxs-lookup"><span data-stu-id="91f8a-156">Target System</span></span> | <span data-ttu-id="91f8a-157">Notes</span><span class="sxs-lookup"><span data-stu-id="91f8a-157">Notes</span></span> |
| ---------- | ---------- | ---------- |
| <span data-ttu-id="91f8a-158">Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-158">Workday</span></span> | <span data-ttu-id="91f8a-159">Active Directory Forest</span><span class="sxs-lookup"><span data-stu-id="91f8a-159">Active Directory Forest</span></span> | <span data-ttu-id="91f8a-160">Each forest is treated as a distinct target system</span><span class="sxs-lookup"><span data-stu-id="91f8a-160">Each forest is treated as a distinct target system</span></span> |
| <span data-ttu-id="91f8a-161">Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-161">Workday</span></span> | <span data-ttu-id="91f8a-162">Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="91f8a-162">Azure AD tenant</span></span> | <span data-ttu-id="91f8a-163">As required for cloud-only users</span><span class="sxs-lookup"><span data-stu-id="91f8a-163">As required for cloud-only users</span></span> |
| <span data-ttu-id="91f8a-164">Active Directory Forest</span><span class="sxs-lookup"><span data-stu-id="91f8a-164">Active Directory Forest</span></span> | <span data-ttu-id="91f8a-165">Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="91f8a-165">Azure AD tenant</span></span> | <span data-ttu-id="91f8a-166">This flow is handled by AAD Connect today</span><span class="sxs-lookup"><span data-stu-id="91f8a-166">This flow is handled by AAD Connect today</span></span> |
| <span data-ttu-id="91f8a-167">Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="91f8a-167">Azure AD tenant</span></span> | <span data-ttu-id="91f8a-168">Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-168">Workday</span></span> | <span data-ttu-id="91f8a-169">For writeback of email addresses</span><span class="sxs-lookup"><span data-stu-id="91f8a-169">For writeback of email addresses</span></span> |

<span data-ttu-id="91f8a-170">To facilitate these multiple workflows to multiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from the Azure AD app gallery:</span><span class="sxs-lookup"><span data-stu-id="91f8a-170">To facilitate these multiple workflows to multiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from the Azure AD app gallery:</span></span>

![AAD App Gallery](./media/workday-inbound-tutorial/WD_Gallery.PNG)

* <span data-ttu-id="91f8a-172">**Workday to Active Directory Provisioning** - This app facilitates user account provisioning from Workday to a single Active Directory forest.</span><span class="sxs-lookup"><span data-stu-id="91f8a-172">**Workday to Active Directory Provisioning** - This app facilitates user account provisioning from Workday to a single Active Directory forest.</span></span> <span data-ttu-id="91f8a-173">If you have multiple forests, you can add one instance of this app from the Azure AD app gallery for each Active Directory forest you need to provision to.</span><span class="sxs-lookup"><span data-stu-id="91f8a-173">If you have multiple forests, you can add one instance of this app from the Azure AD app gallery for each Active Directory forest you need to provision to.</span></span>

* <span data-ttu-id="91f8a-174">**Workday to Azure AD Provisioning** - While AAD Connect is the tool that should be used to synchronize Active Directory users to Azure Active Directory, this app can be used to facilitate provisioning of cloud-only users from Workday to a single Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-174">**Workday to Azure AD Provisioning** - While AAD Connect is the tool that should be used to synchronize Active Directory users to Azure Active Directory, this app can be used to facilitate provisioning of cloud-only users from Workday to a single Azure Active Directory tenant.</span></span>

* <span data-ttu-id="91f8a-175">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory to Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-175">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory to Workday.</span></span>

> [!TIP]
> <span data-ttu-id="91f8a-176">The regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-176">The regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span></span> 

<span data-ttu-id="91f8a-177">How to set up and configure these special provisioning connector apps is the subject of the remaining sections of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="91f8a-177">How to set up and configure these special provisioning connector apps is the subject of the remaining sections of this tutorial.</span></span> <span data-ttu-id="91f8a-178">Which apps you choose to configure will depend on which systems you need to provision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span><span class="sxs-lookup"><span data-stu-id="91f8a-178">Which apps you choose to configure will depend on which systems you need to provision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span></span>

![Overview](./media/workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a><span data-ttu-id="91f8a-180">Configure a system integration user in Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-180">Configure a system integration user in Workday</span></span>
<span data-ttu-id="91f8a-181">A common requirement of all the Workday provisioning connectors is they require credentials for a Workday system integration account to connect to the Workday Human Resources API.</span><span class="sxs-lookup"><span data-stu-id="91f8a-181">A common requirement of all the Workday provisioning connectors is they require credentials for a Workday system integration account to connect to the Workday Human Resources API.</span></span> <span data-ttu-id="91f8a-182">This section describes how to create a system integrator account in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-182">This section describes how to create a system integrator account in Workday.</span></span>

> [!NOTE]
> <span data-ttu-id="91f8a-183">It is possible to bypass this procedure and instead use a Workday global administrator account as the system integration account.</span><span class="sxs-lookup"><span data-stu-id="91f8a-183">It is possible to bypass this procedure and instead use a Workday global administrator account as the system integration account.</span></span> <span data-ttu-id="91f8a-184">This may work fine for demos, but is not recommended for production deployments.</span><span class="sxs-lookup"><span data-stu-id="91f8a-184">This may work fine for demos, but is not recommended for production deployments.</span></span>

### <a name="create-an-integration-system-user"></a><span data-ttu-id="91f8a-185">Create an integration system user</span><span class="sxs-lookup"><span data-stu-id="91f8a-185">Create an integration system user</span></span>

<span data-ttu-id="91f8a-186">**To create an integration system user:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-186">**To create an integration system user:**</span></span>

1. <span data-ttu-id="91f8a-187">Sign into your Workday tenant using an administrator account.</span><span class="sxs-lookup"><span data-stu-id="91f8a-187">Sign into your Workday tenant using an administrator account.</span></span> <span data-ttu-id="91f8a-188">In the **Workday Workbench**, enter create user in the search box, and then click **Create Integration System User**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-188">In the **Workday Workbench**, enter create user in the search box, and then click **Create Integration System User**.</span></span>

    <span data-ttu-id="91f8a-189">![Create user](./media/workday-inbound-tutorial/IC750979.png "Create user")</span><span class="sxs-lookup"><span data-stu-id="91f8a-189">![Create user](./media/workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="91f8a-190">Complete the **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span><span class="sxs-lookup"><span data-stu-id="91f8a-190">Complete the **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="91f8a-191">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span><span class="sxs-lookup"><span data-stu-id="91f8a-191">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span>
 * <span data-ttu-id="91f8a-192">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span><span class="sxs-lookup"><span data-stu-id="91f8a-192">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span></span>

    <span data-ttu-id="91f8a-193">![Create Integration System User](./media/workday-inbound-tutorial/IC750980.png "Create Integration System User")</span><span class="sxs-lookup"><span data-stu-id="91f8a-193">![Create Integration System User](./media/workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

### <a name="create-a-security-group"></a><span data-ttu-id="91f8a-194">Create a security group</span><span class="sxs-lookup"><span data-stu-id="91f8a-194">Create a security group</span></span>
<span data-ttu-id="91f8a-195">You need to create an unconstrained integration system security group and assign the user to it.</span><span class="sxs-lookup"><span data-stu-id="91f8a-195">You need to create an unconstrained integration system security group and assign the user to it.</span></span>

<span data-ttu-id="91f8a-196">**To create a security group:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-196">**To create a security group:**</span></span>

1. <span data-ttu-id="91f8a-197">Enter create security group in the search box, and then click **Create Security Group**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-197">Enter create security group in the search box, and then click **Create Security Group**.</span></span>

    <span data-ttu-id="91f8a-198">![CreateSecurity Group](./media/workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span><span class="sxs-lookup"><span data-stu-id="91f8a-198">![CreateSecurity Group](./media/workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="91f8a-199">Complete the **Create Security Group** task.</span><span class="sxs-lookup"><span data-stu-id="91f8a-199">Complete the **Create Security Group** task.</span></span>  
3. <span data-ttu-id="91f8a-200">Select **Integration System Security Group (Unconstrained)** from the **Type of Tenanted Security Group** dropdown.</span><span class="sxs-lookup"><span data-stu-id="91f8a-200">Select **Integration System Security Group (Unconstrained)** from the **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="91f8a-201">Create a security group to which members will be explicitly added.</span><span class="sxs-lookup"><span data-stu-id="91f8a-201">Create a security group to which members will be explicitly added.</span></span>

    <span data-ttu-id="91f8a-202">![CreateSecurity Group](./media/workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span><span class="sxs-lookup"><span data-stu-id="91f8a-202">![CreateSecurity Group](./media/workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

### <a name="assign-the-integration-system-user-to-the-security-group"></a><span data-ttu-id="91f8a-203">Assign the integration system user to the security group</span><span class="sxs-lookup"><span data-stu-id="91f8a-203">Assign the integration system user to the security group</span></span>

<span data-ttu-id="91f8a-204">**To assign the integration system user:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-204">**To assign the integration system user:**</span></span>

1. <span data-ttu-id="91f8a-205">Enter edit security group in the search box, and then click **Edit Security Group**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-205">Enter edit security group in the search box, and then click **Edit Security Group**.</span></span>

    <span data-ttu-id="91f8a-206">![Edit Security Group](./media/workday-inbound-tutorial/IC750983.png "Edit Security Group")</span><span class="sxs-lookup"><span data-stu-id="91f8a-206">![Edit Security Group](./media/workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
1. <span data-ttu-id="91f8a-207">Search for, and select the new integration security group by name.</span><span class="sxs-lookup"><span data-stu-id="91f8a-207">Search for, and select the new integration security group by name.</span></span>

    <span data-ttu-id="91f8a-208">![Edit Security Group](./media/workday-inbound-tutorial/IC750984.png "Edit Security Group")</span><span class="sxs-lookup"><span data-stu-id="91f8a-208">![Edit Security Group](./media/workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
2. <span data-ttu-id="91f8a-209">Add the new integration system user to the new security group.</span><span class="sxs-lookup"><span data-stu-id="91f8a-209">Add the new integration system user to the new security group.</span></span> 

    <span data-ttu-id="91f8a-210">![System Security Group](./media/workday-inbound-tutorial/IC750985.png "System Security Group")</span><span class="sxs-lookup"><span data-stu-id="91f8a-210">![System Security Group](./media/workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

### <a name="configure-security-group-options"></a><span data-ttu-id="91f8a-211">Configure security group options</span><span class="sxs-lookup"><span data-stu-id="91f8a-211">Configure security group options</span></span>
<span data-ttu-id="91f8a-212">In this step, you'll grant domain security policy permissions for the worker data to the security group.</span><span class="sxs-lookup"><span data-stu-id="91f8a-212">In this step, you'll grant domain security policy permissions for the worker data to the security group.</span></span>

<span data-ttu-id="91f8a-213">**To configure security group options:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-213">**To configure security group options:**</span></span>

1. <span data-ttu-id="91f8a-214">Enter **Domain Security Policies** in the search box, and then click on the link **Domain Security Policies for Functional Area**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-214">Enter **Domain Security Policies** in the search box, and then click on the link **Domain Security Policies for Functional Area**.</span></span>  

    <span data-ttu-id="91f8a-215">![Domain Security Policies](./media/workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="91f8a-215">![Domain Security Policies](./media/workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="91f8a-216">Search for system and select the **System** functional area.</span><span class="sxs-lookup"><span data-stu-id="91f8a-216">Search for system and select the **System** functional area.</span></span>  <span data-ttu-id="91f8a-217">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-217">Click **OK**.</span></span>  

    <span data-ttu-id="91f8a-218">![Domain Security Policies](./media/workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="91f8a-218">![Domain Security Policies](./media/workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="91f8a-219">In the list of security policies for the System functional area, expand **Security Administration** and select the domain security policy **External Account Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-219">In the list of security policies for the System functional area, expand **Security Administration** and select the domain security policy **External Account Provisioning**.</span></span>  

    <span data-ttu-id="91f8a-220">![Domain Security Policies](./media/workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="91f8a-220">![Domain Security Policies](./media/workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
1. <span data-ttu-id="91f8a-221">Click **Edit Permissions**, and then, on the **Edit Permissions** dialog page, add the new security group to the list of security groups with **Get** and **Put** integration permissions.</span><span class="sxs-lookup"><span data-stu-id="91f8a-221">Click **Edit Permissions**, and then, on the **Edit Permissions** dialog page, add the new security group to the list of security groups with **Get** and **Put** integration permissions.</span></span>

    <span data-ttu-id="91f8a-222">![Edit Permission](./media/workday-inbound-tutorial/IC750989.png "Edit Permission")</span><span class="sxs-lookup"><span data-stu-id="91f8a-222">![Edit Permission](./media/workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  

1. <span data-ttu-id="91f8a-223">Repeat steps 1-4 above for each of these remaining security policies:</span><span class="sxs-lookup"><span data-stu-id="91f8a-223">Repeat steps 1-4 above for each of these remaining security policies:</span></span>

| <span data-ttu-id="91f8a-224">Operation</span><span class="sxs-lookup"><span data-stu-id="91f8a-224">Operation</span></span> | <span data-ttu-id="91f8a-225">Domain Security Policy</span><span class="sxs-lookup"><span data-stu-id="91f8a-225">Domain Security Policy</span></span> |
| ---------- | ---------- | 
| <span data-ttu-id="91f8a-226">Get and Put</span><span class="sxs-lookup"><span data-stu-id="91f8a-226">Get and Put</span></span> | <span data-ttu-id="91f8a-227">Worker Data: Public Worker Reports</span><span class="sxs-lookup"><span data-stu-id="91f8a-227">Worker Data: Public Worker Reports</span></span> |
| <span data-ttu-id="91f8a-228">Get and Put</span><span class="sxs-lookup"><span data-stu-id="91f8a-228">Get and Put</span></span> | <span data-ttu-id="91f8a-229">Worker Data: Work Contact Information</span><span class="sxs-lookup"><span data-stu-id="91f8a-229">Worker Data: Work Contact Information</span></span> |
| <span data-ttu-id="91f8a-230">Get</span><span class="sxs-lookup"><span data-stu-id="91f8a-230">Get</span></span> | <span data-ttu-id="91f8a-231">Worker Data: All Positions</span><span class="sxs-lookup"><span data-stu-id="91f8a-231">Worker Data: All Positions</span></span> |
| <span data-ttu-id="91f8a-232">Get</span><span class="sxs-lookup"><span data-stu-id="91f8a-232">Get</span></span> | <span data-ttu-id="91f8a-233">Worker Data: Current Staffing Information</span><span class="sxs-lookup"><span data-stu-id="91f8a-233">Worker Data: Current Staffing Information</span></span> |
| <span data-ttu-id="91f8a-234">Get</span><span class="sxs-lookup"><span data-stu-id="91f8a-234">Get</span></span> | <span data-ttu-id="91f8a-235">Worker Data: Business Title on Worker Profile</span><span class="sxs-lookup"><span data-stu-id="91f8a-235">Worker Data: Business Title on Worker Profile</span></span> |


### <a name="activate-security-policy-changes"></a><span data-ttu-id="91f8a-236">Activate security policy changes</span><span class="sxs-lookup"><span data-stu-id="91f8a-236">Activate security policy changes</span></span>

<span data-ttu-id="91f8a-237">**To activate security policy changes:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-237">**To activate security policy changes:**</span></span>

1. <span data-ttu-id="91f8a-238">Enter activate in the search box, and then click on the link **Activate Pending Security Policy Changes**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-238">Enter activate in the search box, and then click on the link **Activate Pending Security Policy Changes**.</span></span>

    <span data-ttu-id="91f8a-239">![Activate](./media/workday-inbound-tutorial/IC750992.png "Activate")</span><span class="sxs-lookup"><span data-stu-id="91f8a-239">![Activate](./media/workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="91f8a-240">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-240">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 

    <span data-ttu-id="91f8a-241">![Activate Pending Security](./media/workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span><span class="sxs-lookup"><span data-stu-id="91f8a-241">![Activate Pending Security](./media/workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>  
1. <span data-ttu-id="91f8a-242">Complete the task on the next screen by checking the checkbox **Confirm**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-242">Complete the task on the next screen by checking the checkbox **Confirm**, and then click **OK**.</span></span>

    <span data-ttu-id="91f8a-243">![Activate Pending Security](./media/workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span><span class="sxs-lookup"><span data-stu-id="91f8a-243">![Activate Pending Security](./media/workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configuring-user-provisioning-from-workday-to-active-directory"></a><span data-ttu-id="91f8a-244">Configuring user provisioning from Workday to Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f8a-244">Configuring user provisioning from Workday to Active Directory</span></span>
<span data-ttu-id="91f8a-245">Follow these instructions to configure user account provisioning from Workday to each Active Directory forest that you require provisioning to.</span><span class="sxs-lookup"><span data-stu-id="91f8a-245">Follow these instructions to configure user account provisioning from Workday to each Active Directory forest that you require provisioning to.</span></span>

### <a name="planning"></a><span data-ttu-id="91f8a-246">Planning</span><span class="sxs-lookup"><span data-stu-id="91f8a-246">Planning</span></span>

<span data-ttu-id="91f8a-247">Before configuring user provisioning to an Active Directory forest, consider the following questions.</span><span class="sxs-lookup"><span data-stu-id="91f8a-247">Before configuring user provisioning to an Active Directory forest, consider the following questions.</span></span> <span data-ttu-id="91f8a-248">The answers to these questions will determine how your scoping filters and attribute mappings need to be set.</span><span class="sxs-lookup"><span data-stu-id="91f8a-248">The answers to these questions will determine how your scoping filters and attribute mappings need to be set.</span></span> 

* <span data-ttu-id="91f8a-249">**What users in Workday need to be provisioned to this Active Directory forest?**</span><span class="sxs-lookup"><span data-stu-id="91f8a-249">**What users in Workday need to be provisioned to this Active Directory forest?**</span></span>

   * <span data-ttu-id="91f8a-250">*Example: Users where the Workday "Company" attribute contains the value "Contoso", and the "Worker_Type" attribute contains "Regular"*</span><span class="sxs-lookup"><span data-stu-id="91f8a-250">*Example: Users where the Workday "Company" attribute contains the value "Contoso", and the "Worker_Type" attribute contains "Regular"*</span></span>

* <span data-ttu-id="91f8a-251">**How are users routed into different organization units (OUs)?**</span><span class="sxs-lookup"><span data-stu-id="91f8a-251">**How are users routed into different organization units (OUs)?**</span></span>

   * <span data-ttu-id="91f8a-252">*Example: Users are routed to OUs that correspond to an office location, as defined in the Workday "Municipality" and "Country_Region_Reference" attributes*</span><span class="sxs-lookup"><span data-stu-id="91f8a-252">*Example: Users are routed to OUs that correspond to an office location, as defined in the Workday "Municipality" and "Country_Region_Reference" attributes*</span></span>

* <span data-ttu-id="91f8a-253">**How should the following attributes be populated in the Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="91f8a-253">**How should the following attributes be populated in the Active Directory?**</span></span>

   * <span data-ttu-id="91f8a-254">Common Name (cn)</span><span class="sxs-lookup"><span data-stu-id="91f8a-254">Common Name (cn)</span></span>
      * <span data-ttu-id="91f8a-255">*Example: Use the Workday User_ID value, as set by human resources*</span><span class="sxs-lookup"><span data-stu-id="91f8a-255">*Example: Use the Workday User_ID value, as set by human resources*</span></span>
      
   * <span data-ttu-id="91f8a-256">Employee ID (employeeId)</span><span class="sxs-lookup"><span data-stu-id="91f8a-256">Employee ID (employeeId)</span></span>
      * <span data-ttu-id="91f8a-257">*Example: Use the Workday Worker_ID value*</span><span class="sxs-lookup"><span data-stu-id="91f8a-257">*Example: Use the Workday Worker_ID value*</span></span>
      
   * <span data-ttu-id="91f8a-258">SAM Account Name (sAMAccountName)</span><span class="sxs-lookup"><span data-stu-id="91f8a-258">SAM Account Name (sAMAccountName)</span></span>
      * <span data-ttu-id="91f8a-259">*Example: Use the Workday User_ID value, filtered through an Azure AD provisioning expression to remove illegal characters*</span><span class="sxs-lookup"><span data-stu-id="91f8a-259">*Example: Use the Workday User_ID value, filtered through an Azure AD provisioning expression to remove illegal characters*</span></span>
      
   * <span data-ttu-id="91f8a-260">User Principal Name (userPrincipalName)</span><span class="sxs-lookup"><span data-stu-id="91f8a-260">User Principal Name (userPrincipalName)</span></span>
      * <span data-ttu-id="91f8a-261">*Example: Use the Workday User_ID value, with an Azure AD provisioning expression to append a domain name*</span><span class="sxs-lookup"><span data-stu-id="91f8a-261">*Example: Use the Workday User_ID value, with an Azure AD provisioning expression to append a domain name*</span></span>

* <span data-ttu-id="91f8a-262">**How should users be matched between Workday and Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="91f8a-262">**How should users be matched between Workday and Active Directory?**</span></span>

  * <span data-ttu-id="91f8a-263">*Example: Users with a specific Workday "Worker_ID" value are matched with Active Directory users where "employeeID" has the same value. If the Worker_ID value is not found in Active Directory, then create a new user.*</span><span class="sxs-lookup"><span data-stu-id="91f8a-263">*Example: Users with a specific Workday "Worker_ID" value are matched with Active Directory users where "employeeID" has the same value. If the Worker_ID value is not found in Active Directory, then create a new user.*</span></span>
  
* <span data-ttu-id="91f8a-264">**Does the Active Directory forest already contain the user IDs required for the matching logic to work?**</span><span class="sxs-lookup"><span data-stu-id="91f8a-264">**Does the Active Directory forest already contain the user IDs required for the matching logic to work?**</span></span>

  * <span data-ttu-id="91f8a-265">*Example: If this is a new Workday deployment, it is strongly recommended that Active Directory be pre-populated with the correct Workday Worker_ID values (or unique ID value of choice) to keep the matching logic as simple as possible.*</span><span class="sxs-lookup"><span data-stu-id="91f8a-265">*Example: If this is a new Workday deployment, it is strongly recommended that Active Directory be pre-populated with the correct Workday Worker_ID values (or unique ID value of choice) to keep the matching logic as simple as possible.*</span></span>
    
    
### <a name="part-1-adding-the-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="91f8a-266">Part 1: Adding the provisioning connector app and creating the connection to Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-266">Part 1: Adding the provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="91f8a-267">**To configure Workday to Active Directory provisioning:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-267">**To configure Workday to Active Directory provisioning:**</span></span>

1.  <span data-ttu-id="91f8a-268">Go to <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="91f8a-268">Go to <https://portal.azure.com></span></span>

2.  <span data-ttu-id="91f8a-269">In the left navigation bar, select **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="91f8a-269">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="91f8a-270">Select **Enterprise Applications**, then **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-270">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="91f8a-271">Select **Add an application**, and select the **All** category.</span><span class="sxs-lookup"><span data-stu-id="91f8a-271">Select **Add an application**, and select the **All** category.</span></span>

5.  <span data-ttu-id="91f8a-272">Search for **Workday Provisioning to Active Directory**, and add that app from the gallery.</span><span class="sxs-lookup"><span data-stu-id="91f8a-272">Search for **Workday Provisioning to Active Directory**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="91f8a-273">After the app is added and the app details screen is shown, select **Provisioning**</span><span class="sxs-lookup"><span data-stu-id="91f8a-273">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="91f8a-274">Change the **Provisioning** **Mode** to **Automatic**</span><span class="sxs-lookup"><span data-stu-id="91f8a-274">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="91f8a-275">Complete the **Admin Credentials** section as follows:</span><span class="sxs-lookup"><span data-stu-id="91f8a-275">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="91f8a-276">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span><span class="sxs-lookup"><span data-stu-id="91f8a-276">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="91f8a-277">**Should look something like: username@contoso4**</span><span class="sxs-lookup"><span data-stu-id="91f8a-277">**Should look something like: username@contoso4**</span></span>

   * <span data-ttu-id="91f8a-278">**Admin password –** Enter the password of the Workday    integration system account</span><span class="sxs-lookup"><span data-stu-id="91f8a-278">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="91f8a-279">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-279">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="91f8a-280">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string.</span><span class="sxs-lookup"><span data-stu-id="91f8a-280">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string.</span></span>

   * <span data-ttu-id="91f8a-281">**Active Directory Forest -** The “Name” of your Active Directory forest, as returned by the Get-ADForest powershell commandlet.</span><span class="sxs-lookup"><span data-stu-id="91f8a-281">**Active Directory Forest -** The “Name” of your Active Directory forest, as returned by the Get-ADForest powershell commandlet.</span></span> <span data-ttu-id="91f8a-282">This is typically a string like: *contoso.com*</span><span class="sxs-lookup"><span data-stu-id="91f8a-282">This is typically a string like: *contoso.com*</span></span>

   * <span data-ttu-id="91f8a-283">**Active Directory Container -** Enter the container string that contains all users in your AD forest.</span><span class="sxs-lookup"><span data-stu-id="91f8a-283">**Active Directory Container -** Enter the container string that contains all users in your AD forest.</span></span> <span data-ttu-id="91f8a-284">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span><span class="sxs-lookup"><span data-stu-id="91f8a-284">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span></span>

   * <span data-ttu-id="91f8a-285">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span><span class="sxs-lookup"><span data-stu-id="91f8a-285">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="91f8a-286">Click the **Test Connection** button.</span><span class="sxs-lookup"><span data-stu-id="91f8a-286">Click the **Test Connection** button.</span></span> <span data-ttu-id="91f8a-287">If the connection test succeeds, click the **Save** button at the top.</span><span class="sxs-lookup"><span data-stu-id="91f8a-287">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="91f8a-288">If it fails, double-check that the Workday credentials are valid in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-288">If it fails, double-check that the Workday credentials are valid in Workday.</span></span> 

![Azure portal](./media/workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="91f8a-290">Part 2: Configure attribute mappings</span><span class="sxs-lookup"><span data-stu-id="91f8a-290">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="91f8a-291">In this section, you will configure how user data flows from Workday to Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-291">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="91f8a-292">On the Provisioning tab under **Mappings**, click **Synchronize Workday Workers to OnPremises**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-292">On the Provisioning tab under **Mappings**, click **Synchronize Workday Workers to OnPremises**.</span></span>

2.  <span data-ttu-id="91f8a-293">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to AD, by defining a set of attribute-based filters.</span><span class="sxs-lookup"><span data-stu-id="91f8a-293">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="91f8a-294">The default scope is “all users in Workday”.</span><span class="sxs-lookup"><span data-stu-id="91f8a-294">The default scope is “all users in Workday”.</span></span> <span data-ttu-id="91f8a-295">Example filters:</span><span class="sxs-lookup"><span data-stu-id="91f8a-295">Example filters:</span></span>

   * <span data-ttu-id="91f8a-296">Example: Scope to users with Worker IDs between 1000000 and    2000000</span><span class="sxs-lookup"><span data-stu-id="91f8a-296">Example: Scope to users with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="91f8a-297">Attribute: WorkerID</span><span class="sxs-lookup"><span data-stu-id="91f8a-297">Attribute: WorkerID</span></span>

      * <span data-ttu-id="91f8a-298">Operator: REGEX Match</span><span class="sxs-lookup"><span data-stu-id="91f8a-298">Operator: REGEX Match</span></span>

      * <span data-ttu-id="91f8a-299">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="91f8a-299">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="91f8a-300">Example: Only employees and not contingent workers</span><span class="sxs-lookup"><span data-stu-id="91f8a-300">Example: Only employees and not contingent workers</span></span> 

      * <span data-ttu-id="91f8a-301">Attribute: EmployeeID</span><span class="sxs-lookup"><span data-stu-id="91f8a-301">Attribute: EmployeeID</span></span>

      * <span data-ttu-id="91f8a-302">Operator: IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="91f8a-302">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="91f8a-303">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-303">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Active Directory.</span></span> <span data-ttu-id="91f8a-304">**Create** and **Update** are most common.</span><span class="sxs-lookup"><span data-stu-id="91f8a-304">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="91f8a-305">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span><span class="sxs-lookup"><span data-stu-id="91f8a-305">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span>

5. <span data-ttu-id="91f8a-306">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span><span class="sxs-lookup"><span data-stu-id="91f8a-306">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span></span> <span data-ttu-id="91f8a-307">An individual attribute mapping supports these properties:</span><span class="sxs-lookup"><span data-stu-id="91f8a-307">An individual attribute mapping supports these properties:</span></span>

      * <span data-ttu-id="91f8a-308">**Mapping Type**</span><span class="sxs-lookup"><span data-stu-id="91f8a-308">**Mapping Type**</span></span>

         * <span data-ttu-id="91f8a-309">**Direct** – Writes the value of the Workday attribute      to the AD attribute, with no changes</span><span class="sxs-lookup"><span data-stu-id="91f8a-309">**Direct** – Writes the value of the Workday attribute      to the AD attribute, with no changes</span></span>

         * <span data-ttu-id="91f8a-310">**Constant** - Write a static, constant string value to      the AD attribute</span><span class="sxs-lookup"><span data-stu-id="91f8a-310">**Constant** - Write a static, constant string value to      the AD attribute</span></span>

         * <span data-ttu-id="91f8a-311">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span><span class="sxs-lookup"><span data-stu-id="91f8a-311">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="91f8a-312">[For more info, see this article on expressions](../manage-apps/functions-for-customizing-application-data.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-312">[For more info, see this article on expressions](../manage-apps/functions-for-customizing-application-data.md).</span></span>

      * <span data-ttu-id="91f8a-313">**Source attribute** - The user attribute from Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-313">**Source attribute** - The user attribute from Workday.</span></span> <span data-ttu-id="91f8a-314">If the attribute you are looking for is not present, see [Customizing the list of Workday user attributes](#customizing-the-list-of-workday-user-attributes).</span><span class="sxs-lookup"><span data-stu-id="91f8a-314">If the attribute you are looking for is not present, see [Customizing the list of Workday user attributes](#customizing-the-list-of-workday-user-attributes).</span></span>

      * <span data-ttu-id="91f8a-315">**Default value** – Optional.</span><span class="sxs-lookup"><span data-stu-id="91f8a-315">**Default value** – Optional.</span></span> <span data-ttu-id="91f8a-316">If the source attribute has an empty value, the mapping will write this value instead.</span><span class="sxs-lookup"><span data-stu-id="91f8a-316">If the source attribute has an empty value, the mapping will write this value instead.</span></span>
            <span data-ttu-id="91f8a-317">Most common configuration is to leave this blank.</span><span class="sxs-lookup"><span data-stu-id="91f8a-317">Most common configuration is to leave this blank.</span></span>

      * <span data-ttu-id="91f8a-318">**Target attribute** – The user attribute in Active     Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-318">**Target attribute** – The user attribute in Active     Directory.</span></span>

      * <span data-ttu-id="91f8a-319">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-319">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Active Directory.</span></span> <span data-ttu-id="91f8a-320">This is typically set on the Worker ID field for Workday, which is typically mapped to one of the Employee ID attributes in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-320">This is typically set on the Worker ID field for Workday, which is typically mapped to one of the Employee ID attributes in Active Directory.</span></span>

      * <span data-ttu-id="91f8a-321">**Matching precedence** – Multiple matching attributes can be set.</span><span class="sxs-lookup"><span data-stu-id="91f8a-321">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="91f8a-322">When there are multiple, they are evaluated in the order defined by this field.</span><span class="sxs-lookup"><span data-stu-id="91f8a-322">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="91f8a-323">As soon as a match is found, no further matching attributes are evaluated.</span><span class="sxs-lookup"><span data-stu-id="91f8a-323">As soon as a match is found, no further matching attributes are evaluated.</span></span>

      * <span data-ttu-id="91f8a-324">**Apply this mapping**</span><span class="sxs-lookup"><span data-stu-id="91f8a-324">**Apply this mapping**</span></span>
       
         * <span data-ttu-id="91f8a-325">**Always** – Apply this mapping on both user creation      and update actions</span><span class="sxs-lookup"><span data-stu-id="91f8a-325">**Always** – Apply this mapping on both user creation      and update actions</span></span>

         * <span data-ttu-id="91f8a-326">**Only during creation** - Apply this mapping only on      user creation actions</span><span class="sxs-lookup"><span data-stu-id="91f8a-326">**Only during creation** - Apply this mapping only on      user creation actions</span></span>

6. <span data-ttu-id="91f8a-327">To save your mappings, click **Save** at the top of the      Attribute-Mapping section.</span><span class="sxs-lookup"><span data-stu-id="91f8a-327">To save your mappings, click **Save** at the top of the      Attribute-Mapping section.</span></span>

![Azure portal](./media/workday-inbound-tutorial/WD_2.PNG)

<span data-ttu-id="91f8a-329">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span><span class="sxs-lookup"><span data-stu-id="91f8a-329">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span></span>

-   <span data-ttu-id="91f8a-330">The expression that maps to the parentDistinguishedName attribute is used to provision a users to different OUs based on one or more Workday source attributes.</span><span class="sxs-lookup"><span data-stu-id="91f8a-330">The expression that maps to the parentDistinguishedName attribute is used to provision a users to different OUs based on one or more Workday source attributes.</span></span> <span data-ttu-id="91f8a-331">This example here places users in different OUs based on what city they are in.</span><span class="sxs-lookup"><span data-stu-id="91f8a-331">This example here places users in different OUs based on what city they are in.</span></span>

-   <span data-ttu-id="91f8a-332">The userPrincipalName attribute in Active Directory is generated by concatenating the Workday user ID with a domain suffix</span><span class="sxs-lookup"><span data-stu-id="91f8a-332">The userPrincipalName attribute in Active Directory is generated by concatenating the Workday user ID with a domain suffix</span></span>

-   <span data-ttu-id="91f8a-333">[There is documentation on writing expressions here](../manage-apps/functions-for-customizing-application-data.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-333">[There is documentation on writing expressions here](../manage-apps/functions-for-customizing-application-data.md).</span></span> <span data-ttu-id="91f8a-334">This includes examples on how to remove special characters.</span><span class="sxs-lookup"><span data-stu-id="91f8a-334">This includes examples on how to remove special characters.</span></span>

  
| <span data-ttu-id="91f8a-335">WORKDAY ATTRIBUTE</span><span class="sxs-lookup"><span data-stu-id="91f8a-335">WORKDAY ATTRIBUTE</span></span> | <span data-ttu-id="91f8a-336">ACTIVE DIRECTORY ATTRIBUTE</span><span class="sxs-lookup"><span data-stu-id="91f8a-336">ACTIVE DIRECTORY ATTRIBUTE</span></span> |  <span data-ttu-id="91f8a-337">MATCHING ID?</span><span class="sxs-lookup"><span data-stu-id="91f8a-337">MATCHING ID?</span></span> | <span data-ttu-id="91f8a-338">CREATE / UPDATE</span><span class="sxs-lookup"><span data-stu-id="91f8a-338">CREATE / UPDATE</span></span> |
| ---------- | ---------- | ---------- | ---------- |
| <span data-ttu-id="91f8a-339">**WorkerID**</span><span class="sxs-lookup"><span data-stu-id="91f8a-339">**WorkerID**</span></span>  |  <span data-ttu-id="91f8a-340">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="91f8a-340">EmployeeID</span></span> | <span data-ttu-id="91f8a-341">**Yes**</span><span class="sxs-lookup"><span data-stu-id="91f8a-341">**Yes**</span></span> | <span data-ttu-id="91f8a-342">Written on create only</span><span class="sxs-lookup"><span data-stu-id="91f8a-342">Written on create only</span></span> |
| <span data-ttu-id="91f8a-343">**UserID**</span><span class="sxs-lookup"><span data-stu-id="91f8a-343">**UserID**</span></span>    |  <span data-ttu-id="91f8a-344">cn</span><span class="sxs-lookup"><span data-stu-id="91f8a-344">cn</span></span>    |   |   <span data-ttu-id="91f8a-345">Written on create only</span><span class="sxs-lookup"><span data-stu-id="91f8a-345">Written on create only</span></span> |
| <span data-ttu-id="91f8a-346">**Join("@", [UserID], "contoso.com")**</span><span class="sxs-lookup"><span data-stu-id="91f8a-346">**Join("@", [UserID], "contoso.com")**</span></span>   | <span data-ttu-id="91f8a-347">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="91f8a-347">userPrincipalName</span></span>     |     | <span data-ttu-id="91f8a-348">Written on create only</span><span class="sxs-lookup"><span data-stu-id="91f8a-348">Written on create only</span></span> 
| <span data-ttu-id="91f8a-349">**Replace(Mid(Replace(\[UserID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)\*$)", , "", , )**</span><span class="sxs-lookup"><span data-stu-id="91f8a-349">**Replace(Mid(Replace(\[UserID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)\*$)", , "", , )**</span></span>      |    <span data-ttu-id="91f8a-350">sAMAccountName</span><span class="sxs-lookup"><span data-stu-id="91f8a-350">sAMAccountName</span></span>            |     |         <span data-ttu-id="91f8a-351">Written on create only</span><span class="sxs-lookup"><span data-stu-id="91f8a-351">Written on create only</span></span> |
| <span data-ttu-id="91f8a-352">**Switch(\[Active\], , "0", "True", "1",)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-352">**Switch(\[Active\], , "0", "True", "1",)**</span></span> |  <span data-ttu-id="91f8a-353">accountDisabled</span><span class="sxs-lookup"><span data-stu-id="91f8a-353">accountDisabled</span></span>      |     | <span data-ttu-id="91f8a-354">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-354">Create + update</span></span> |
| <span data-ttu-id="91f8a-355">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="91f8a-355">**FirstName**</span></span>   | <span data-ttu-id="91f8a-356">givenName</span><span class="sxs-lookup"><span data-stu-id="91f8a-356">givenName</span></span>       |     |    <span data-ttu-id="91f8a-357">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-357">Create + update</span></span> |
| <span data-ttu-id="91f8a-358">**LastName**</span><span class="sxs-lookup"><span data-stu-id="91f8a-358">**LastName**</span></span>   |   <span data-ttu-id="91f8a-359">sn</span><span class="sxs-lookup"><span data-stu-id="91f8a-359">sn</span></span>   |     |  <span data-ttu-id="91f8a-360">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-360">Create + update</span></span> |
| <span data-ttu-id="91f8a-361">**PreferredNameData**</span><span class="sxs-lookup"><span data-stu-id="91f8a-361">**PreferredNameData**</span></span>  |  <span data-ttu-id="91f8a-362">displayName</span><span class="sxs-lookup"><span data-stu-id="91f8a-362">displayName</span></span> |     |   <span data-ttu-id="91f8a-363">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-363">Create + update</span></span> |
| <span data-ttu-id="91f8a-364">**Company**</span><span class="sxs-lookup"><span data-stu-id="91f8a-364">**Company**</span></span>         | <span data-ttu-id="91f8a-365">company</span><span class="sxs-lookup"><span data-stu-id="91f8a-365">company</span></span>   |     |  <span data-ttu-id="91f8a-366">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-366">Create + update</span></span> |
| <span data-ttu-id="91f8a-367">**SupervisoryOrganization**</span><span class="sxs-lookup"><span data-stu-id="91f8a-367">**SupervisoryOrganization**</span></span>  | <span data-ttu-id="91f8a-368">department</span><span class="sxs-lookup"><span data-stu-id="91f8a-368">department</span></span>  |     |  <span data-ttu-id="91f8a-369">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-369">Create + update</span></span> |
| <span data-ttu-id="91f8a-370">**ManagerReference**</span><span class="sxs-lookup"><span data-stu-id="91f8a-370">**ManagerReference**</span></span>   | <span data-ttu-id="91f8a-371">manager</span><span class="sxs-lookup"><span data-stu-id="91f8a-371">manager</span></span>  |     |  <span data-ttu-id="91f8a-372">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-372">Create + update</span></span> |
| <span data-ttu-id="91f8a-373">**BusinessTitle**</span><span class="sxs-lookup"><span data-stu-id="91f8a-373">**BusinessTitle**</span></span>   |  <span data-ttu-id="91f8a-374">title</span><span class="sxs-lookup"><span data-stu-id="91f8a-374">title</span></span>     |     |  <span data-ttu-id="91f8a-375">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-375">Create + update</span></span> | 
| <span data-ttu-id="91f8a-376">**AddressLineData**</span><span class="sxs-lookup"><span data-stu-id="91f8a-376">**AddressLineData**</span></span>    |  <span data-ttu-id="91f8a-377">streetAddress</span><span class="sxs-lookup"><span data-stu-id="91f8a-377">streetAddress</span></span>  |     |   <span data-ttu-id="91f8a-378">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-378">Create + update</span></span> |
| <span data-ttu-id="91f8a-379">**Municipality**</span><span class="sxs-lookup"><span data-stu-id="91f8a-379">**Municipality**</span></span>   |   <span data-ttu-id="91f8a-380">l</span><span class="sxs-lookup"><span data-stu-id="91f8a-380">l</span></span>   |     | <span data-ttu-id="91f8a-381">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-381">Create + update</span></span> |
| <span data-ttu-id="91f8a-382">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="91f8a-382">**CountryReferenceTwoLetter**</span></span>      |   <span data-ttu-id="91f8a-383">co</span><span class="sxs-lookup"><span data-stu-id="91f8a-383">co</span></span> |     |   <span data-ttu-id="91f8a-384">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-384">Create + update</span></span> |
| <span data-ttu-id="91f8a-385">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="91f8a-385">**CountryReferenceTwoLetter**</span></span>    |  <span data-ttu-id="91f8a-386">c</span><span class="sxs-lookup"><span data-stu-id="91f8a-386">c</span></span>  |     |         <span data-ttu-id="91f8a-387">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-387">Create + update</span></span> |
| <span data-ttu-id="91f8a-388">**CountryRegionReference**</span><span class="sxs-lookup"><span data-stu-id="91f8a-388">**CountryRegionReference**</span></span> |  <span data-ttu-id="91f8a-389">st</span><span class="sxs-lookup"><span data-stu-id="91f8a-389">st</span></span>     |     | <span data-ttu-id="91f8a-390">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-390">Create + update</span></span> |
| <span data-ttu-id="91f8a-391">**WorkSpaceReference**</span><span class="sxs-lookup"><span data-stu-id="91f8a-391">**WorkSpaceReference**</span></span> | <span data-ttu-id="91f8a-392">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="91f8a-392">physicalDeliveryOfficeName</span></span>    |     |  <span data-ttu-id="91f8a-393">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-393">Create + update</span></span> |
| <span data-ttu-id="91f8a-394">**PostalCode**</span><span class="sxs-lookup"><span data-stu-id="91f8a-394">**PostalCode**</span></span>  |   <span data-ttu-id="91f8a-395">postalCode</span><span class="sxs-lookup"><span data-stu-id="91f8a-395">postalCode</span></span>  |     | <span data-ttu-id="91f8a-396">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-396">Create + update</span></span> |
| <span data-ttu-id="91f8a-397">**PrimaryWorkTelephone**</span><span class="sxs-lookup"><span data-stu-id="91f8a-397">**PrimaryWorkTelephone**</span></span>  |  <span data-ttu-id="91f8a-398">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="91f8a-398">telephoneNumber</span></span>   |     | <span data-ttu-id="91f8a-399">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-399">Create + update</span></span> |
| <span data-ttu-id="91f8a-400">**Fax**</span><span class="sxs-lookup"><span data-stu-id="91f8a-400">**Fax**</span></span>      | <span data-ttu-id="91f8a-401">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="91f8a-401">facsimileTelephoneNumber</span></span>     |     |    <span data-ttu-id="91f8a-402">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-402">Create + update</span></span> |
| <span data-ttu-id="91f8a-403">**Mobile**</span><span class="sxs-lookup"><span data-stu-id="91f8a-403">**Mobile**</span></span>  |    <span data-ttu-id="91f8a-404">mobile</span><span class="sxs-lookup"><span data-stu-id="91f8a-404">mobile</span></span>       |     |       <span data-ttu-id="91f8a-405">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-405">Create + update</span></span> |
| <span data-ttu-id="91f8a-406">**LocalReference**</span><span class="sxs-lookup"><span data-stu-id="91f8a-406">**LocalReference**</span></span> |  <span data-ttu-id="91f8a-407">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="91f8a-407">preferredLanguage</span></span>  |     |  <span data-ttu-id="91f8a-408">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-408">Create + update</span></span> |                                               
| <span data-ttu-id="91f8a-409">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span><span class="sxs-lookup"><span data-stu-id="91f8a-409">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span></span>  | <span data-ttu-id="91f8a-410">parentDistinguishedName</span><span class="sxs-lookup"><span data-stu-id="91f8a-410">parentDistinguishedName</span></span>     |     |  <span data-ttu-id="91f8a-411">Create + update</span><span class="sxs-lookup"><span data-stu-id="91f8a-411">Create + update</span></span> |
  
### <a name="part-3-configure-the-on-premises-synchronization-agent"></a><span data-ttu-id="91f8a-412">Part 3: Configure the on-premises synchronization agent</span><span class="sxs-lookup"><span data-stu-id="91f8a-412">Part 3: Configure the on-premises synchronization agent</span></span>

<span data-ttu-id="91f8a-413">In order to provision to Active Directory on-premises, an agent must be installed on a domain-joined server in the desire Active Directory forest.</span><span class="sxs-lookup"><span data-stu-id="91f8a-413">In order to provision to Active Directory on-premises, an agent must be installed on a domain-joined server in the desire Active Directory forest.</span></span> <span data-ttu-id="91f8a-414">Domain admin (or Enterprise admin) credentials are required to complete the procedure.</span><span class="sxs-lookup"><span data-stu-id="91f8a-414">Domain admin (or Enterprise admin) credentials are required to complete the procedure.</span></span>

<span data-ttu-id="91f8a-415">**[You can download the on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-415">**[You can download the on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span></span>

<span data-ttu-id="91f8a-416">After installing agent, run the Powershell commands below to configure the agent for your environment.</span><span class="sxs-lookup"><span data-stu-id="91f8a-416">After installing agent, run the Powershell commands below to configure the agent for your environment.</span></span>

<span data-ttu-id="91f8a-417">**Command #1**</span><span class="sxs-lookup"><span data-stu-id="91f8a-417">**Command #1**</span></span>

> <span data-ttu-id="91f8a-418">cd "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Modules\AADSyncAgent" Agent\\Modules\\AADSyncAgent</span><span class="sxs-lookup"><span data-stu-id="91f8a-418">cd "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Modules\AADSyncAgent" Agent\\Modules\\AADSyncAgent</span></span>

> <span data-ttu-id="91f8a-419">Import-Module "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Modules\AADSyncAgent\AADSyncAgent.psd1"</span><span class="sxs-lookup"><span data-stu-id="91f8a-419">Import-Module "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Modules\AADSyncAgent\AADSyncAgent.psd1"</span></span>

<span data-ttu-id="91f8a-420">**Command #2**</span><span class="sxs-lookup"><span data-stu-id="91f8a-420">**Command #2**</span></span>

> <span data-ttu-id="91f8a-421">Add-ADSyncAgentActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="91f8a-421">Add-ADSyncAgentActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="91f8a-422">Input: For "Directory Name", enter the AD Forest name, as entered in part \#2</span><span class="sxs-lookup"><span data-stu-id="91f8a-422">Input: For "Directory Name", enter the AD Forest name, as entered in part \#2</span></span>
* <span data-ttu-id="91f8a-423">Input: Admin username and password for Active Directory forest</span><span class="sxs-lookup"><span data-stu-id="91f8a-423">Input: Admin username and password for Active Directory forest</span></span>

>[!TIP]
> <span data-ttu-id="91f8a-424">If you receive the error message "The relationship between the primary domain and the trusted domain failed", it is because the local machine is in an environment where multiple Active Directory forests or domains are configured, and at least one configured trust relationship is either failing or not operational.</span><span class="sxs-lookup"><span data-stu-id="91f8a-424">If you receive the error message "The relationship between the primary domain and the trusted domain failed", it is because the local machine is in an environment where multiple Active Directory forests or domains are configured, and at least one configured trust relationship is either failing or not operational.</span></span> <span data-ttu-id="91f8a-425">To resolve the issue, either correct or remove the broken trust relationship.</span><span class="sxs-lookup"><span data-stu-id="91f8a-425">To resolve the issue, either correct or remove the broken trust relationship.</span></span>

<span data-ttu-id="91f8a-426">**Command #3**</span><span class="sxs-lookup"><span data-stu-id="91f8a-426">**Command #3**</span></span>

> <span data-ttu-id="91f8a-427">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="91f8a-427">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="91f8a-428">Input: Global admin username and password for your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="91f8a-428">Input: Global admin username and password for your Azure AD tenant</span></span>

>[!IMPORTANT]
><span data-ttu-id="91f8a-429">There is presently a known issue with global administrator credentials not working if they use a custom domain (example: admin@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="91f8a-429">There is presently a known issue with global administrator credentials not working if they use a custom domain (example: admin@contoso.com).</span></span> <span data-ttu-id="91f8a-430">As a workaround, create and use a global administrator account with an onmicrosoft.com domain (example: admin@contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="91f8a-430">As a workaround, create and use a global administrator account with an onmicrosoft.com domain (example: admin@contoso.onmicrosoft.com)</span></span>

>[!IMPORTANT]
><span data-ttu-id="91f8a-431">There is presently a known issue with global administrator credentials not working if they have multi-factor authentication enabled.</span><span class="sxs-lookup"><span data-stu-id="91f8a-431">There is presently a known issue with global administrator credentials not working if they have multi-factor authentication enabled.</span></span> <span data-ttu-id="91f8a-432">As a workaround, disable multi-factor authentication for the global administrator.</span><span class="sxs-lookup"><span data-stu-id="91f8a-432">As a workaround, disable multi-factor authentication for the global administrator.</span></span>

<span data-ttu-id="91f8a-433">**Command #4**</span><span class="sxs-lookup"><span data-stu-id="91f8a-433">**Command #4**</span></span>

> <span data-ttu-id="91f8a-434">Get-AdSyncAgentProvisioningTasks</span><span class="sxs-lookup"><span data-stu-id="91f8a-434">Get-AdSyncAgentProvisioningTasks</span></span>

* <span data-ttu-id="91f8a-435">Action: Confirm data is returned.</span><span class="sxs-lookup"><span data-stu-id="91f8a-435">Action: Confirm data is returned.</span></span> <span data-ttu-id="91f8a-436">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-436">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span></span> <span data-ttu-id="91f8a-437">Example output:</span><span class="sxs-lookup"><span data-stu-id="91f8a-437">Example output:</span></span>

> <span data-ttu-id="91f8a-438">Name          : My AD Forest</span><span class="sxs-lookup"><span data-stu-id="91f8a-438">Name          : My AD Forest</span></span>
>
> <span data-ttu-id="91f8a-439">Enabled       : True</span><span class="sxs-lookup"><span data-stu-id="91f8a-439">Enabled       : True</span></span>
>
> <span data-ttu-id="91f8a-440">DirectoryName : mydomain.contoso.com</span><span class="sxs-lookup"><span data-stu-id="91f8a-440">DirectoryName : mydomain.contoso.com</span></span>
>
> <span data-ttu-id="91f8a-441">Credentialed  : False</span><span class="sxs-lookup"><span data-stu-id="91f8a-441">Credentialed  : False</span></span>
>
> <span data-ttu-id="91f8a-442">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span><span class="sxs-lookup"><span data-stu-id="91f8a-442">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span></span>

<span data-ttu-id="91f8a-443">**Command #5**</span><span class="sxs-lookup"><span data-stu-id="91f8a-443">**Command #5**</span></span>

> <span data-ttu-id="91f8a-444">Start-AdSyncAgentSynchronization -Automatic</span><span class="sxs-lookup"><span data-stu-id="91f8a-444">Start-AdSyncAgentSynchronization -Automatic</span></span>

<span data-ttu-id="91f8a-445">**Command #6**</span><span class="sxs-lookup"><span data-stu-id="91f8a-445">**Command #6**</span></span>

> <span data-ttu-id="91f8a-446">net stop aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="91f8a-446">net stop aadsyncagent</span></span>

<span data-ttu-id="91f8a-447">**Command #7**</span><span class="sxs-lookup"><span data-stu-id="91f8a-447">**Command #7**</span></span>

> <span data-ttu-id="91f8a-448">net start aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="91f8a-448">net start aadsyncagent</span></span>

>[!TIP]
><span data-ttu-id="91f8a-449">In addition to the "net" commands in Powershell, the synchronization agent service can also be started and stopped using **Services.msc**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-449">In addition to the "net" commands in Powershell, the synchronization agent service can also be started and stopped using **Services.msc**.</span></span> <span data-ttu-id="91f8a-450">If you get errors when running the Powershell commands, ensure that the **Microsoft Azure AD Connect Provisioning Agent** is running in **Services.msc**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-450">If you get errors when running the Powershell commands, ensure that the **Microsoft Azure AD Connect Provisioning Agent** is running in **Services.msc**.</span></span>

![Services](./media/workday-inbound-tutorial/Services.png)  

<span data-ttu-id="91f8a-452">**Additional configuration for customers in the European Union**</span><span class="sxs-lookup"><span data-stu-id="91f8a-452">**Additional configuration for customers in the European Union**</span></span>

<span data-ttu-id="91f8a-453">If your Azure Active Directory tenant is located in one of the EU data centers, then follow the additional steps below.</span><span class="sxs-lookup"><span data-stu-id="91f8a-453">If your Azure Active Directory tenant is located in one of the EU data centers, then follow the additional steps below.</span></span>

1. <span data-ttu-id="91f8a-454">Open **Services.msc**, and stop the **Microsoft Azure AD Connect Provisioning Agent** service.</span><span class="sxs-lookup"><span data-stu-id="91f8a-454">Open **Services.msc**, and stop the **Microsoft Azure AD Connect Provisioning Agent** service.</span></span>
2. <span data-ttu-id="91f8a-455">Go to the agent installation folder (example: C:\Program Files\Microsoft Azure AD Connect Provisioning Agent).</span><span class="sxs-lookup"><span data-stu-id="91f8a-455">Go to the agent installation folder (example: C:\Program Files\Microsoft Azure AD Connect Provisioning Agent).</span></span>
3. <span data-ttu-id="91f8a-456">Open **SyncAgnt.exe.config** in a text editor.</span><span class="sxs-lookup"><span data-stu-id="91f8a-456">Open **SyncAgnt.exe.config** in a text editor.</span></span>
4. <span data-ttu-id="91f8a-457">Replace https://manage.hub.syncfabric.windowsazure.com/Management with **https://eu.manage.hub.syncfabric.windowsazure.com/Management**</span><span class="sxs-lookup"><span data-stu-id="91f8a-457">Replace https://manage.hub.syncfabric.windowsazure.com/Management with **https://eu.manage.hub.syncfabric.windowsazure.com/Management**</span></span>
5. <span data-ttu-id="91f8a-458">Replace https://provision.hub.syncfabric.windowsazure.com/Provisioning with **https://eu.provision.hub.syncfabric.windowsazure.com/Provisioning**</span><span class="sxs-lookup"><span data-stu-id="91f8a-458">Replace https://provision.hub.syncfabric.windowsazure.com/Provisioning with **https://eu.provision.hub.syncfabric.windowsazure.com/Provisioning**</span></span>
6. <span data-ttu-id="91f8a-459">Save the **SyncAgnt.exe.config** file.</span><span class="sxs-lookup"><span data-stu-id="91f8a-459">Save the **SyncAgnt.exe.config** file.</span></span>
7. <span data-ttu-id="91f8a-460">Open **Services.msc**, and start the **Microsoft Azure AD Connect Provisioning Agent** service.</span><span class="sxs-lookup"><span data-stu-id="91f8a-460">Open **Services.msc**, and start the **Microsoft Azure AD Connect Provisioning Agent** service.</span></span>

<span data-ttu-id="91f8a-461">**Agent troubleshooting**</span><span class="sxs-lookup"><span data-stu-id="91f8a-461">**Agent troubleshooting**</span></span>

<span data-ttu-id="91f8a-462">The [Windows Event Log](https://technet.microsoft.com/library/cc722404(v=ws.11).aspx) on the Windows Server machine hosting the agent contains events for all operations performed by the agent.</span><span class="sxs-lookup"><span data-stu-id="91f8a-462">The [Windows Event Log](https://technet.microsoft.com/library/cc722404(v=ws.11).aspx) on the Windows Server machine hosting the agent contains events for all operations performed by the agent.</span></span> <span data-ttu-id="91f8a-463">To view these events:</span><span class="sxs-lookup"><span data-stu-id="91f8a-463">To view these events:</span></span>
    
1. <span data-ttu-id="91f8a-464">Open **Eventvwr.msc**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-464">Open **Eventvwr.msc**.</span></span>
2. <span data-ttu-id="91f8a-465">Select **Windows Logs > Application**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-465">Select **Windows Logs > Application**.</span></span>
3. <span data-ttu-id="91f8a-466">View all events logged under the source **AADSyncAgent**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-466">View all events logged under the source **AADSyncAgent**.</span></span> 
4. <span data-ttu-id="91f8a-467">Check for errors and warnings.</span><span class="sxs-lookup"><span data-stu-id="91f8a-467">Check for errors and warnings.</span></span>

<span data-ttu-id="91f8a-468">If there is a permissions problem with either the Active Directory or Azure Active Directory credentials provided in the Powershell commands, you will see an error such as this one:</span><span class="sxs-lookup"><span data-stu-id="91f8a-468">If there is a permissions problem with either the Active Directory or Azure Active Directory credentials provided in the Powershell commands, you will see an error such as this one:</span></span> 
    
![Event logs](./media/workday-inbound-tutorial/Windows_Event_Logs.png) 


### <a name="part-4-start-the-service"></a><span data-ttu-id="91f8a-470">Part 4: Start the service</span><span class="sxs-lookup"><span data-stu-id="91f8a-470">Part 4: Start the service</span></span>
<span data-ttu-id="91f8a-471">Once parts 1-3 have been completed, you can start the provisioning service back in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91f8a-471">Once parts 1-3 have been completed, you can start the provisioning service back in the Azure portal.</span></span>

1.  <span data-ttu-id="91f8a-472">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-472">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="91f8a-473">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-473">Click **Save**.</span></span>

3. <span data-ttu-id="91f8a-474">This will start the initial sync, which can take a variable number of hours depending on how many users are in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-474">This will start the initial sync, which can take a variable number of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="91f8a-475">At any time, check the **Audit logs** tab in the Azure portal to see what actions the provisioning service has performed.</span><span class="sxs-lookup"><span data-stu-id="91f8a-475">At any time, check the **Audit logs** tab in the Azure portal to see what actions the provisioning service has performed.</span></span> <span data-ttu-id="91f8a-476">The audit logs lists all individual sync events performed by the provisioning service, such as which users are being read out of Workday and then subsequently added or updated to Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-476">The audit logs lists all individual sync events performed by the provisioning service, such as which users are being read out of Workday and then subsequently added or updated to Active Directory.</span></span> <span data-ttu-id="91f8a-477">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](../manage-apps/check-status-user-account-provisioning.md)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-477">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](../manage-apps/check-status-user-account-provisioning.md)**</span></span>

1.  <span data-ttu-id="91f8a-478">Check the [Windows Event Log](https://technet.microsoft.com/library/cc722404(v=ws.11).aspx) on the Windows Server machine hosting the agent for any new errors or warnings.</span><span class="sxs-lookup"><span data-stu-id="91f8a-478">Check the [Windows Event Log](https://technet.microsoft.com/library/cc722404(v=ws.11).aspx) on the Windows Server machine hosting the agent for any new errors or warnings.</span></span> <span data-ttu-id="91f8a-479">These events are viewable by launching **Eventvwr.msc** on the server and selecting **Windows Logs > Application**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-479">These events are viewable by launching **Eventvwr.msc** on the server and selecting **Windows Logs > Application**.</span></span> <span data-ttu-id="91f8a-480">All provisioning-related messages are logged under the source **AADSyncAgent**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-480">All provisioning-related messages are logged under the source **AADSyncAgent**.</span></span>

6. <span data-ttu-id="91f8a-481">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span><span class="sxs-lookup"><span data-stu-id="91f8a-481">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

![Azure portal](./media/workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-to-azure-active-directory"></a><span data-ttu-id="91f8a-483">Configuring user provisioning to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f8a-483">Configuring user provisioning to Azure Active Directory</span></span>
<span data-ttu-id="91f8a-484">How you configure provisioning to Azure Active Directory will depend on your provisioning requirements, as detailed in the table below.</span><span class="sxs-lookup"><span data-stu-id="91f8a-484">How you configure provisioning to Azure Active Directory will depend on your provisioning requirements, as detailed in the table below.</span></span>

| <span data-ttu-id="91f8a-485">Scenario</span><span class="sxs-lookup"><span data-stu-id="91f8a-485">Scenario</span></span> | <span data-ttu-id="91f8a-486">Solution</span><span class="sxs-lookup"><span data-stu-id="91f8a-486">Solution</span></span> |
| -------- | -------- |
| <span data-ttu-id="91f8a-487">**Users need to be provisioned to Active Directory and Azure AD**</span><span class="sxs-lookup"><span data-stu-id="91f8a-487">**Users need to be provisioned to Active Directory and Azure AD**</span></span> | <span data-ttu-id="91f8a-488">Use **[AAD Connect](../connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-488">Use **[AAD Connect](../connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="91f8a-489">**Users need to be provisioned to Active Directory only**</span><span class="sxs-lookup"><span data-stu-id="91f8a-489">**Users need to be provisioned to Active Directory only**</span></span> | <span data-ttu-id="91f8a-490">Use **[AAD Connect](../connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-490">Use **[AAD Connect](../connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="91f8a-491">**Users need to be provisioned to Azure AD only (cloud only)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-491">**Users need to be provisioned to Azure AD only (cloud only)**</span></span> | <span data-ttu-id="91f8a-492">Use the **Workday to Azure Active Directory provisioning** app in the app gallery</span><span class="sxs-lookup"><span data-stu-id="91f8a-492">Use the **Workday to Azure Active Directory provisioning** app in the app gallery</span></span> |

<span data-ttu-id="91f8a-493">For instructions on setting up Azure AD Connect, see the [Azure AD Connect documentation](../connect/active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-493">For instructions on setting up Azure AD Connect, see the [Azure AD Connect documentation](../connect/active-directory-aadconnect.md).</span></span>

<span data-ttu-id="91f8a-494">The following sections describe setting up a connection between Workday and Azure AD to provision cloud-only users.</span><span class="sxs-lookup"><span data-stu-id="91f8a-494">The following sections describe setting up a connection between Workday and Azure AD to provision cloud-only users.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91f8a-495">Only follow the procedure below if you have cloud-only users that need to be provisioned to Azure AD and not on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-495">Only follow the procedure below if you have cloud-only users that need to be provisioned to Azure AD and not on-premises Active Directory.</span></span>

### <a name="part-1-adding-the-azure-ad-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="91f8a-496">Part 1: Adding the Azure AD provisioning connector app and creating the connection to Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-496">Part 1: Adding the Azure AD provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="91f8a-497">**To configure Workday to Azure Active Directory provisioning for cloud-only users:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-497">**To configure Workday to Azure Active Directory provisioning for cloud-only users:**</span></span>

1.  <span data-ttu-id="91f8a-498">Go to <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="91f8a-498">Go to <https://portal.azure.com>.</span></span>

2.  <span data-ttu-id="91f8a-499">In the left navigation bar, select **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="91f8a-499">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="91f8a-500">Select **Enterprise Applications**, then **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-500">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="91f8a-501">Select **Add an application**, and then select the **All** category.</span><span class="sxs-lookup"><span data-stu-id="91f8a-501">Select **Add an application**, and then select the **All** category.</span></span>

5.  <span data-ttu-id="91f8a-502">Search for **Workday to Azure AD provisioning**, and add that app from the gallery.</span><span class="sxs-lookup"><span data-stu-id="91f8a-502">Search for **Workday to Azure AD provisioning**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="91f8a-503">After the app is added and the app details screen is shown, select **Provisioning**</span><span class="sxs-lookup"><span data-stu-id="91f8a-503">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="91f8a-504">Change the **Provisioning** **Mode** to **Automatic**</span><span class="sxs-lookup"><span data-stu-id="91f8a-504">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="91f8a-505">Complete the **Admin Credentials** section as follows:</span><span class="sxs-lookup"><span data-stu-id="91f8a-505">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="91f8a-506">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span><span class="sxs-lookup"><span data-stu-id="91f8a-506">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="91f8a-507">Should look something like: username@contoso4</span><span class="sxs-lookup"><span data-stu-id="91f8a-507">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="91f8a-508">**Admin password –** Enter the password of the Workday    integration system account</span><span class="sxs-lookup"><span data-stu-id="91f8a-508">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="91f8a-509">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-509">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="91f8a-510">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string.</span><span class="sxs-lookup"><span data-stu-id="91f8a-510">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string.</span></span> <span data-ttu-id="91f8a-511">If this URL is not known, please work with your Workday integration partner or support representative to determine the correct URL to use.</span><span class="sxs-lookup"><span data-stu-id="91f8a-511">If this URL is not known, please work with your Workday integration partner or support representative to determine the correct URL to use.</span></span>

   * <span data-ttu-id="91f8a-512">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span><span class="sxs-lookup"><span data-stu-id="91f8a-512">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="91f8a-513">Click the **Test Connection** button.</span><span class="sxs-lookup"><span data-stu-id="91f8a-513">Click the **Test Connection** button.</span></span>

   * <span data-ttu-id="91f8a-514">If the connection test succeeds, click the **Save** button at the top.</span><span class="sxs-lookup"><span data-stu-id="91f8a-514">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="91f8a-515">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-515">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span></span>

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="91f8a-516">Part 2: Configure attribute mappings</span><span class="sxs-lookup"><span data-stu-id="91f8a-516">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="91f8a-517">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span><span class="sxs-lookup"><span data-stu-id="91f8a-517">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span></span>

1. <span data-ttu-id="91f8a-518">On the Provisioning tab under **Mappings**, click **Synchronize  Workers to Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-518">On the Provisioning tab under **Mappings**, click **Synchronize  Workers to Azure AD**.</span></span>

2. <span data-ttu-id="91f8a-519">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to Azure AD, by defining a set of attribute-based filters.</span><span class="sxs-lookup"><span data-stu-id="91f8a-519">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to Azure AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="91f8a-520">The default scope is “all users in Workday”.</span><span class="sxs-lookup"><span data-stu-id="91f8a-520">The default scope is “all users in Workday”.</span></span> <span data-ttu-id="91f8a-521">Example filters:</span><span class="sxs-lookup"><span data-stu-id="91f8a-521">Example filters:</span></span>

   * <span data-ttu-id="91f8a-522">Example: Scope to users with Worker IDs between 1000000 and    2000000</span><span class="sxs-lookup"><span data-stu-id="91f8a-522">Example: Scope to users with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="91f8a-523">Attribute: WorkerID</span><span class="sxs-lookup"><span data-stu-id="91f8a-523">Attribute: WorkerID</span></span>

      * <span data-ttu-id="91f8a-524">Operator: REGEX Match</span><span class="sxs-lookup"><span data-stu-id="91f8a-524">Operator: REGEX Match</span></span>

      * <span data-ttu-id="91f8a-525">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="91f8a-525">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="91f8a-526">Example: Only contingent workers and not regular employees</span><span class="sxs-lookup"><span data-stu-id="91f8a-526">Example: Only contingent workers and not regular employees</span></span>

      * <span data-ttu-id="91f8a-527">Attribute: ContingentID</span><span class="sxs-lookup"><span data-stu-id="91f8a-527">Attribute: ContingentID</span></span>

      * <span data-ttu-id="91f8a-528">Operator: IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="91f8a-528">Operator: IS NOT NULL</span></span>

3. <span data-ttu-id="91f8a-529">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f8a-529">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Azure AD.</span></span> <span data-ttu-id="91f8a-530">**Create** and **Update** are most common.</span><span class="sxs-lookup"><span data-stu-id="91f8a-530">**Create** and **Update** are most common.</span></span>

4. <span data-ttu-id="91f8a-531">In the **Attribute mappings** section, you can define how individual  Workday attributes map to Active Directory attributes.</span><span class="sxs-lookup"><span data-stu-id="91f8a-531">In the **Attribute mappings** section, you can define how individual  Workday attributes map to Active Directory attributes.</span></span>

5. <span data-ttu-id="91f8a-532">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span><span class="sxs-lookup"><span data-stu-id="91f8a-532">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span></span> <span data-ttu-id="91f8a-533">An individual attribute mapping supports these properties:</span><span class="sxs-lookup"><span data-stu-id="91f8a-533">An individual attribute mapping supports these properties:</span></span>

   * <span data-ttu-id="91f8a-534">**Mapping Type**</span><span class="sxs-lookup"><span data-stu-id="91f8a-534">**Mapping Type**</span></span>

      * <span data-ttu-id="91f8a-535">**Direct** – Writes the value of the Workday attribute         to the AD attribute, with no changes</span><span class="sxs-lookup"><span data-stu-id="91f8a-535">**Direct** – Writes the value of the Workday attribute         to the AD attribute, with no changes</span></span>

      * <span data-ttu-id="91f8a-536">**Constant** - Write a static, constant string value to         the AD attribute</span><span class="sxs-lookup"><span data-stu-id="91f8a-536">**Constant** - Write a static, constant string value to         the AD attribute</span></span>

      * <span data-ttu-id="91f8a-537">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span><span class="sxs-lookup"><span data-stu-id="91f8a-537">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="91f8a-538">[For more info, see this article on expressions](../manage-apps/functions-for-customizing-application-data.md).</span><span class="sxs-lookup"><span data-stu-id="91f8a-538">[For more info, see this article on expressions](../manage-apps/functions-for-customizing-application-data.md).</span></span>

   * <span data-ttu-id="91f8a-539">**Source attribute** - The user attribute from Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-539">**Source attribute** - The user attribute from Workday.</span></span> <span data-ttu-id="91f8a-540">If the attribute you are looking for is not present, see [Customizing the list of Workday user attributes](#customizing-the-list-of-workday-user-attributes).</span><span class="sxs-lookup"><span data-stu-id="91f8a-540">If the attribute you are looking for is not present, see [Customizing the list of Workday user attributes](#customizing-the-list-of-workday-user-attributes).</span></span>

   * <span data-ttu-id="91f8a-541">**Default value** – Optional.</span><span class="sxs-lookup"><span data-stu-id="91f8a-541">**Default value** – Optional.</span></span> <span data-ttu-id="91f8a-542">If the source attribute has an empty value, the mapping will write this value instead.</span><span class="sxs-lookup"><span data-stu-id="91f8a-542">If the source attribute has an empty value, the mapping will write this value instead.</span></span>
            <span data-ttu-id="91f8a-543">Most common configuration is to leave this blank.</span><span class="sxs-lookup"><span data-stu-id="91f8a-543">Most common configuration is to leave this blank.</span></span>

   * <span data-ttu-id="91f8a-544">**Target attribute** – The user attribute in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f8a-544">**Target attribute** – The user attribute in Azure AD.</span></span>

   * <span data-ttu-id="91f8a-545">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f8a-545">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Azure AD.</span></span> <span data-ttu-id="91f8a-546">This is typically set on the Worker ID field for Workday, which is typically mapped to the Employee ID attribute (new) or an extension attribute in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f8a-546">This is typically set on the Worker ID field for Workday, which is typically mapped to the Employee ID attribute (new) or an extension attribute in Azure AD.</span></span>

   * <span data-ttu-id="91f8a-547">**Matching precedence** – Multiple matching attributes can be set.</span><span class="sxs-lookup"><span data-stu-id="91f8a-547">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="91f8a-548">When there are multiple, they are evaluated in the order defined by this field.</span><span class="sxs-lookup"><span data-stu-id="91f8a-548">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="91f8a-549">As soon as a match is found, no further matching attributes are evaluated.</span><span class="sxs-lookup"><span data-stu-id="91f8a-549">As soon as a match is found, no further matching attributes are evaluated.</span></span>

   * <span data-ttu-id="91f8a-550">**Apply this mapping**</span><span class="sxs-lookup"><span data-stu-id="91f8a-550">**Apply this mapping**</span></span>

     * <span data-ttu-id="91f8a-551">**Always** – Apply this mapping on both user creation          and update actions</span><span class="sxs-lookup"><span data-stu-id="91f8a-551">**Always** – Apply this mapping on both user creation          and update actions</span></span>

     * <span data-ttu-id="91f8a-552">**Only during creation** - Apply this mapping only on          user creation actions</span><span class="sxs-lookup"><span data-stu-id="91f8a-552">**Only during creation** - Apply this mapping only on          user creation actions</span></span>

6. <span data-ttu-id="91f8a-553">To save your mappings, click **Save** at the top of the      Attribute-Mapping section.</span><span class="sxs-lookup"><span data-stu-id="91f8a-553">To save your mappings, click **Save** at the top of the      Attribute-Mapping section.</span></span>

### <a name="part-3-start-the-service"></a><span data-ttu-id="91f8a-554">Part 3: Start the service</span><span class="sxs-lookup"><span data-stu-id="91f8a-554">Part 3: Start the service</span></span>
<span data-ttu-id="91f8a-555">Once parts 1-2 have been completed, you can start the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="91f8a-555">Once parts 1-2 have been completed, you can start the provisioning service.</span></span>

1. <span data-ttu-id="91f8a-556">In the **Provisioning** tab, set the **Provisioning Status** to  **On**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-556">In the **Provisioning** tab, set the **Provisioning Status** to  **On**.</span></span>

2. <span data-ttu-id="91f8a-557">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-557">Click **Save**.</span></span>

3. <span data-ttu-id="91f8a-558">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-558">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="91f8a-559">Individual sync events can be viewed in the **Audit Logs** tab. **[See the provisioning reporting guide for detailed instructions on how to read the audit logs](../manage-apps/check-status-user-account-provisioning.md)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-559">Individual sync events can be viewed in the **Audit Logs** tab. **[See the provisioning reporting guide for detailed instructions on how to read the audit logs](../manage-apps/check-status-user-account-provisioning.md)**</span></span>

5. <span data-ttu-id="91f8a-560">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span><span class="sxs-lookup"><span data-stu-id="91f8a-560">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="configuring-writeback-of-email-addresses-to-workday"></a><span data-ttu-id="91f8a-561">Configuring writeback of email addresses to Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-561">Configuring writeback of email addresses to Workday</span></span>
<span data-ttu-id="91f8a-562">Follow these instructions to configure writeback of user email addresses from Azure Active Directory to Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-562">Follow these instructions to configure writeback of user email addresses from Azure Active Directory to Workday.</span></span>

### <a name="part-1-adding-the-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="91f8a-563">Part 1: Adding the provisioning connector app and creating the connection to Workday</span><span class="sxs-lookup"><span data-stu-id="91f8a-563">Part 1: Adding the provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="91f8a-564">**To configure Workday to Active Directory provisioning:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-564">**To configure Workday to Active Directory provisioning:**</span></span>

1. <span data-ttu-id="91f8a-565">Go to <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="91f8a-565">Go to <https://portal.azure.com></span></span>

2. <span data-ttu-id="91f8a-566">In the left navigation bar, select **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="91f8a-566">In the left navigation bar, select **Azure Active Directory**</span></span>

3. <span data-ttu-id="91f8a-567">Select **Enterprise Applications**, then **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-567">Select **Enterprise Applications**, then **All Applications**.</span></span>

4. <span data-ttu-id="91f8a-568">Select **Add an application**, then select the **All** category.</span><span class="sxs-lookup"><span data-stu-id="91f8a-568">Select **Add an application**, then select the **All** category.</span></span>

5. <span data-ttu-id="91f8a-569">Search for **Workday Writeback**, and add that app from the gallery.</span><span class="sxs-lookup"><span data-stu-id="91f8a-569">Search for **Workday Writeback**, and add that app from the gallery.</span></span>

6. <span data-ttu-id="91f8a-570">After the app is added and the app details screen is shown, select **Provisioning**</span><span class="sxs-lookup"><span data-stu-id="91f8a-570">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7. <span data-ttu-id="91f8a-571">Change the **Provisioning** **Mode** to **Automatic**</span><span class="sxs-lookup"><span data-stu-id="91f8a-571">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8. <span data-ttu-id="91f8a-572">Complete the **Admin Credentials** section as follows:</span><span class="sxs-lookup"><span data-stu-id="91f8a-572">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="91f8a-573">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span><span class="sxs-lookup"><span data-stu-id="91f8a-573">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="91f8a-574">Should look something like: username@contoso4</span><span class="sxs-lookup"><span data-stu-id="91f8a-574">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="91f8a-575">**Admin password –** Enter the password of the Workday    integration system account</span><span class="sxs-lookup"><span data-stu-id="91f8a-575">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="91f8a-576">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-576">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="91f8a-577">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string (if necessary).</span><span class="sxs-lookup"><span data-stu-id="91f8a-577">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string (if necessary).</span></span>

   * <span data-ttu-id="91f8a-578">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span><span class="sxs-lookup"><span data-stu-id="91f8a-578">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="91f8a-579">Click the **Test Connection** button.</span><span class="sxs-lookup"><span data-stu-id="91f8a-579">Click the **Test Connection** button.</span></span> <span data-ttu-id="91f8a-580">If the connection test succeeds, click the **Save** button at the top.</span><span class="sxs-lookup"><span data-stu-id="91f8a-580">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="91f8a-581">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-581">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span></span>

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="91f8a-582">Part 2: Configure attribute mappings</span><span class="sxs-lookup"><span data-stu-id="91f8a-582">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="91f8a-583">In this section, you will configure how user data flows from Workday to Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91f8a-583">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1. <span data-ttu-id="91f8a-584">On the Provisioning tab under **Mappings**, click **Synchronize  Azure AD Users to Workday**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-584">On the Provisioning tab under **Mappings**, click **Synchronize  Azure AD Users to Workday**.</span></span>

2. <span data-ttu-id="91f8a-585">In the **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back to Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-585">In the **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back to Workday.</span></span> <span data-ttu-id="91f8a-586">The default scope is “all users in Azure AD”.</span><span class="sxs-lookup"><span data-stu-id="91f8a-586">The default scope is “all users in Azure AD”.</span></span> 

3. <span data-ttu-id="91f8a-587">In the **Attribute mappings** section, update the matching ID to indicate the attribute in Azure Active Directory where the Workday worker ID or employee ID is stored.</span><span class="sxs-lookup"><span data-stu-id="91f8a-587">In the **Attribute mappings** section, update the matching ID to indicate the attribute in Azure Active Directory where the Workday worker ID or employee ID is stored.</span></span> <span data-ttu-id="91f8a-588">A popular matching method is to synchronize the Workday worker ID or employee ID to extensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD to match users back in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-588">A popular matching method is to synchronize the Workday worker ID or employee ID to extensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD to match users back in Workday.</span></span> 

4. <span data-ttu-id="91f8a-589">To save your mappings, click **Save** at the top of the Attribute-Mapping section.</span><span class="sxs-lookup"><span data-stu-id="91f8a-589">To save your mappings, click **Save** at the top of the Attribute-Mapping section.</span></span>

### <a name="part-3-start-the-service"></a><span data-ttu-id="91f8a-590">Part 3: Start the service</span><span class="sxs-lookup"><span data-stu-id="91f8a-590">Part 3: Start the service</span></span>
<span data-ttu-id="91f8a-591">Once parts 1-2 have been completed, you can start the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="91f8a-591">Once parts 1-2 have been completed, you can start the provisioning service.</span></span>

1. <span data-ttu-id="91f8a-592">In the **Provisioning** tab, set the **Provisioning Status** to  **On**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-592">In the **Provisioning** tab, set the **Provisioning Status** to  **On**.</span></span>

2. <span data-ttu-id="91f8a-593">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-593">Click **Save**.</span></span>

3. <span data-ttu-id="91f8a-594">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span><span class="sxs-lookup"><span data-stu-id="91f8a-594">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="91f8a-595">Individual sync events can be viewed in the **Audit Logs** tab. **[See the provisioning reporting guide for detailed instructions on how to read the audit logs](../manage-apps/check-status-user-account-provisioning.md)**</span><span class="sxs-lookup"><span data-stu-id="91f8a-595">Individual sync events can be viewed in the **Audit Logs** tab. **[See the provisioning reporting guide for detailed instructions on how to read the audit logs](../manage-apps/check-status-user-account-provisioning.md)**</span></span>

5. <span data-ttu-id="91f8a-596">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span><span class="sxs-lookup"><span data-stu-id="91f8a-596">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="customizing-the-list-of-workday-user-attributes"></a><span data-ttu-id="91f8a-597">Customizing the list of Workday user attributes</span><span class="sxs-lookup"><span data-stu-id="91f8a-597">Customizing the list of Workday user attributes</span></span>
<span data-ttu-id="91f8a-598">The Workday provisioning apps for Active Directory and Azure AD both include a default list of Workday user attributes you can select from.</span><span class="sxs-lookup"><span data-stu-id="91f8a-598">The Workday provisioning apps for Active Directory and Azure AD both include a default list of Workday user attributes you can select from.</span></span> <span data-ttu-id="91f8a-599">However, these lists are not comprehensive.</span><span class="sxs-lookup"><span data-stu-id="91f8a-599">However, these lists are not comprehensive.</span></span> <span data-ttu-id="91f8a-600">Workday supports many hundreds of possible user attributes, which can either be standard or unique to your Workday tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-600">Workday supports many hundreds of possible user attributes, which can either be standard or unique to your Workday tenant.</span></span> 

<span data-ttu-id="91f8a-601">The Azure AD provisioning service supports the ability to customize your list or Workday attribute to include any attributes exposed in the [Get_Workers](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) operation of the Human Resources API.</span><span class="sxs-lookup"><span data-stu-id="91f8a-601">The Azure AD provisioning service supports the ability to customize your list or Workday attribute to include any attributes exposed in the [Get_Workers](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) operation of the Human Resources API.</span></span>

<span data-ttu-id="91f8a-602">To do this, you must use [Workday Studio](https://community.workday.com/studio-download) to extract the XPath expressions that represent the attributes you wish to use, and then add them to your provisioning configuration using the advanced attribute editor in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91f8a-602">To do this, you must use [Workday Studio](https://community.workday.com/studio-download) to extract the XPath expressions that represent the attributes you wish to use, and then add them to your provisioning configuration using the advanced attribute editor in the Azure portal.</span></span>

<span data-ttu-id="91f8a-603">**To retrieve an XPath expression for a Workday user attribute:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-603">**To retrieve an XPath expression for a Workday user attribute:**</span></span>

1. <span data-ttu-id="91f8a-604">Download and install [Workday Studio](https://community.workday.com/studio-download).</span><span class="sxs-lookup"><span data-stu-id="91f8a-604">Download and install [Workday Studio](https://community.workday.com/studio-download).</span></span> <span data-ttu-id="91f8a-605">You will need a Workday community account to access the installer.</span><span class="sxs-lookup"><span data-stu-id="91f8a-605">You will need a Workday community account to access the installer.</span></span>

2. <span data-ttu-id="91f8a-606">Download the Workday Human_Resources WDSL file from this URL: https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Human_Resources.wsdl</span><span class="sxs-lookup"><span data-stu-id="91f8a-606">Download the Workday Human_Resources WDSL file from this URL: https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Human_Resources.wsdl</span></span>

3. <span data-ttu-id="91f8a-607">Launch Workday Studio.</span><span class="sxs-lookup"><span data-stu-id="91f8a-607">Launch Workday Studio.</span></span>

4. <span data-ttu-id="91f8a-608">From the command bar, select the  **Workday > Test Web Service in Tester** option.</span><span class="sxs-lookup"><span data-stu-id="91f8a-608">From the command bar, select the  **Workday > Test Web Service in Tester** option.</span></span>

5. <span data-ttu-id="91f8a-609">Select **External**, and select the Human_Resources WSDL file you downloaded in step 2.</span><span class="sxs-lookup"><span data-stu-id="91f8a-609">Select **External**, and select the Human_Resources WSDL file you downloaded in step 2.</span></span>

    ![Workday Studio](./media/workday-inbound-tutorial/WDstudio1.PNG)

6. <span data-ttu-id="91f8a-611">Set the **Location** field to `https://IMPL-CC.workday.com/ccx/service/TENANT/Human_Resources`, but replacing "IMPL-CC" with your actual instance type, and "TENANT" with your real tenant name.</span><span class="sxs-lookup"><span data-stu-id="91f8a-611">Set the **Location** field to `https://IMPL-CC.workday.com/ccx/service/TENANT/Human_Resources`, but replacing "IMPL-CC" with your actual instance type, and "TENANT" with your real tenant name.</span></span>

7. <span data-ttu-id="91f8a-612">Set **Operation** to **Get_Workers**</span><span class="sxs-lookup"><span data-stu-id="91f8a-612">Set **Operation** to **Get_Workers**</span></span>

8.  <span data-ttu-id="91f8a-613">Click the small **configure** link below the Request/Response panes to set your Workday credentials.</span><span class="sxs-lookup"><span data-stu-id="91f8a-613">Click the small **configure** link below the Request/Response panes to set your Workday credentials.</span></span> <span data-ttu-id="91f8a-614">Check **Authentication**, and then enter the user name and password for your Workday integration system account.</span><span class="sxs-lookup"><span data-stu-id="91f8a-614">Check **Authentication**, and then enter the user name and password for your Workday integration system account.</span></span> <span data-ttu-id="91f8a-615">Be sure to format the user name as name@tenant, and leave the **WS-Security UsernameToken** option selected.</span><span class="sxs-lookup"><span data-stu-id="91f8a-615">Be sure to format the user name as name@tenant, and leave the **WS-Security UsernameToken** option selected.</span></span>

    ![Workday Studio](./media/workday-inbound-tutorial/WDstudio2.PNG)

9. <span data-ttu-id="91f8a-617">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-617">Select **OK**.</span></span>

10. <span data-ttu-id="91f8a-618">The **Request** pane, paste in the XML below and set **Employee_ID** to the employee ID of a real user in your Workday tenant.</span><span class="sxs-lookup"><span data-stu-id="91f8a-618">The **Request** pane, paste in the XML below and set **Employee_ID** to the employee ID of a real user in your Workday tenant.</span></span> <span data-ttu-id="91f8a-619">Select a user that has the attribute populated that you wish to extract.</span><span class="sxs-lookup"><span data-stu-id="91f8a-619">Select a user that has the attribute populated that you wish to extract.</span></span>

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <env:Envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
      <env:Body>
        <wd:Get_Workers_Request xmlns:wd="urn:com.workday/bsvc" wd:version="v21.1">
          <wd:Request_References wd:Skip_Non_Existing_Instances="true">
            <wd:Worker_Reference>
              <wd:ID wd:type="Employee_ID">21008</wd:ID>
            </wd:Worker_Reference>
          </wd:Request_References>
          <wd:Response_Group>
            <wd:Include_Reference>true</wd:Include_Reference>
            <wd:Include_Personal_Information>true</wd:Include_Personal_Information>
            <wd:Include_Employment_Information>true</wd:Include_Employment_Information>
            <wd:Include_Management_Chain_Data>true</wd:Include_Management_Chain_Data>
            <wd:Include_Organizations>true</wd:Include_Organizations>
            <wd:Include_Reference>true</wd:Include_Reference>
            <wd:Include_Transaction_Log_Data>true</wd:Include_Transaction_Log_Data>
            <wd:Include_Photo>true</wd:Include_Photo>
            <wd:Include_User_Account>true</wd:Include_User_Account>
            <wd:Include_Roles>true</wd:Include_Roles>
          </wd:Response_Group>
        </wd:Get_Workers_Request>
      </env:Body>
    </env:Envelope>
    ```
 
11. <span data-ttu-id="91f8a-620">Click the **Send Request** (green arrow) to execute the command.</span><span class="sxs-lookup"><span data-stu-id="91f8a-620">Click the **Send Request** (green arrow) to execute the command.</span></span> <span data-ttu-id="91f8a-621">If successful, the response should appear in the **Response** pane.</span><span class="sxs-lookup"><span data-stu-id="91f8a-621">If successful, the response should appear in the **Response** pane.</span></span> <span data-ttu-id="91f8a-622">Check the response to ensure it has the data of the user ID you entered, and not an error.</span><span class="sxs-lookup"><span data-stu-id="91f8a-622">Check the response to ensure it has the data of the user ID you entered, and not an error.</span></span>

12. <span data-ttu-id="91f8a-623">If successful, copy the XML from the **Response** pane and save it as an XML file.</span><span class="sxs-lookup"><span data-stu-id="91f8a-623">If successful, copy the XML from the **Response** pane and save it as an XML file.</span></span>

13. <span data-ttu-id="91f8a-624">In the command bar of Workday Studio, select **File > Open File...** and open the XML file you saved.</span><span class="sxs-lookup"><span data-stu-id="91f8a-624">In the command bar of Workday Studio, select **File > Open File...** and open the XML file you saved.</span></span> <span data-ttu-id="91f8a-625">This opens it in the Workday Studio XML editor.</span><span class="sxs-lookup"><span data-stu-id="91f8a-625">This opens it in the Workday Studio XML editor.</span></span>

    ![Workday Studio](./media/workday-inbound-tutorial/WDstudio3.PNG)

14. <span data-ttu-id="91f8a-627">In the file tree, navigate through **/env: Envelope > env: Body > wd:Get_Workers_Response > wd:Response_Data > wd: Worker** to find your user's data.</span><span class="sxs-lookup"><span data-stu-id="91f8a-627">In the file tree, navigate through **/env: Envelope > env: Body > wd:Get_Workers_Response > wd:Response_Data > wd: Worker** to find your user's data.</span></span> 

15. <span data-ttu-id="91f8a-628">Under **wd: Worker**, find the attribute that you wish to add, and select it.</span><span class="sxs-lookup"><span data-stu-id="91f8a-628">Under **wd: Worker**, find the attribute that you wish to add, and select it.</span></span>

16. <span data-ttu-id="91f8a-629">Copy the XPath expression for your selected attribute out of the **Document Path** field.</span><span class="sxs-lookup"><span data-stu-id="91f8a-629">Copy the XPath expression for your selected attribute out of the **Document Path** field.</span></span>

1. <span data-ttu-id="91f8a-630">Remove the **/env:Envelope/env:Body/wd:Get_Workers_Response/wd:Response_Data/** prefix from the copied expression.</span><span class="sxs-lookup"><span data-stu-id="91f8a-630">Remove the **/env:Envelope/env:Body/wd:Get_Workers_Response/wd:Response_Data/** prefix from the copied expression.</span></span>

18. <span data-ttu-id="91f8a-631">If the last item in the copied expression is a node (example: "/wd: Birth_Date"), then append **/text()** at the end of the expression.</span><span class="sxs-lookup"><span data-stu-id="91f8a-631">If the last item in the copied expression is a node (example: "/wd: Birth_Date"), then append **/text()** at the end of the expression.</span></span> <span data-ttu-id="91f8a-632">This is not necessary if the last item is an attribute (example: "/@wd: type").</span><span class="sxs-lookup"><span data-stu-id="91f8a-632">This is not necessary if the last item is an attribute (example: "/@wd: type").</span></span>

19. <span data-ttu-id="91f8a-633">The result should be something like `wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Birth_Date/text()`.</span><span class="sxs-lookup"><span data-stu-id="91f8a-633">The result should be something like `wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Birth_Date/text()`.</span></span> <span data-ttu-id="91f8a-634">This is what you will copy into the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91f8a-634">This is what you will copy into the Azure portal.</span></span>


<span data-ttu-id="91f8a-635">**To add your custom Workday user attribute to your provisioning configuration:**</span><span class="sxs-lookup"><span data-stu-id="91f8a-635">**To add your custom Workday user attribute to your provisioning configuration:**</span></span>

1. <span data-ttu-id="91f8a-636">Launch the [Azure portal](https://portal.azure.com), and navigate to the Provisioning section of your Workday provisioning application, as described earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="91f8a-636">Launch the [Azure portal](https://portal.azure.com), and navigate to the Provisioning section of your Workday provisioning application, as described earlier in this tutorial.</span></span>

2. <span data-ttu-id="91f8a-637">Set **Provisioning Status** to **Off**, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-637">Set **Provisioning Status** to **Off**, and select **Save**.</span></span> <span data-ttu-id="91f8a-638">This will help ensure your changes will take effect only when you are ready.</span><span class="sxs-lookup"><span data-stu-id="91f8a-638">This will help ensure your changes will take effect only when you are ready.</span></span>

3. <span data-ttu-id="91f8a-639">Under **Mappings**, select **Synchronize Workers to OnPremises** (or **Synchronize Workers to Azure AD**).</span><span class="sxs-lookup"><span data-stu-id="91f8a-639">Under **Mappings**, select **Synchronize Workers to OnPremises** (or **Synchronize Workers to Azure AD**).</span></span>

4. <span data-ttu-id="91f8a-640">Scroll to the bottom of the next screen, and select **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-640">Scroll to the bottom of the next screen, and select **Show advanced options**.</span></span>

5. <span data-ttu-id="91f8a-641">Select **Edit attribute list for Workday**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-641">Select **Edit attribute list for Workday**.</span></span>

    ![Workday Studio](./media/workday-inbound-tutorial/WDstudio_AAD1.PNG)

6. <span data-ttu-id="91f8a-643">Scroll to the bottom of the attribute list to where the input fields are.</span><span class="sxs-lookup"><span data-stu-id="91f8a-643">Scroll to the bottom of the attribute list to where the input fields are.</span></span>

7. <span data-ttu-id="91f8a-644">For **Name**, enter a display name for your attribute.</span><span class="sxs-lookup"><span data-stu-id="91f8a-644">For **Name**, enter a display name for your attribute.</span></span>

8. <span data-ttu-id="91f8a-645">For **Type**, select type that appropriately corresponds to your attribute (**String** is most common).</span><span class="sxs-lookup"><span data-stu-id="91f8a-645">For **Type**, select type that appropriately corresponds to your attribute (**String** is most common).</span></span>

9. <span data-ttu-id="91f8a-646">For **API Expression**, enter the XPath expression you copied from Workday Studio.</span><span class="sxs-lookup"><span data-stu-id="91f8a-646">For **API Expression**, enter the XPath expression you copied from Workday Studio.</span></span> <span data-ttu-id="91f8a-647">Example: `wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Birth_Date/text()`</span><span class="sxs-lookup"><span data-stu-id="91f8a-647">Example: `wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Birth_Date/text()`</span></span>

10. <span data-ttu-id="91f8a-648">Select **Add Attribute**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-648">Select **Add Attribute**.</span></span>

    ![Workday Studio](./media/workday-inbound-tutorial/WDstudio_AAD2.PNG)

11. <span data-ttu-id="91f8a-650">Select **Save** above, and then **Yes** to the dialog.</span><span class="sxs-lookup"><span data-stu-id="91f8a-650">Select **Save** above, and then **Yes** to the dialog.</span></span> <span data-ttu-id="91f8a-651">Close the Attribute-Mapping screen if it is still open.</span><span class="sxs-lookup"><span data-stu-id="91f8a-651">Close the Attribute-Mapping screen if it is still open.</span></span>

12. <span data-ttu-id="91f8a-652">Back on the main **Provisioning** tab, select **Synchronize Workers to OnPremises** (or **Synchronize Workers to Azure AD**) again.</span><span class="sxs-lookup"><span data-stu-id="91f8a-652">Back on the main **Provisioning** tab, select **Synchronize Workers to OnPremises** (or **Synchronize Workers to Azure AD**) again.</span></span>

13. <span data-ttu-id="91f8a-653">Select **Add new mapping**.</span><span class="sxs-lookup"><span data-stu-id="91f8a-653">Select **Add new mapping**.</span></span>

14. <span data-ttu-id="91f8a-654">Your new attribute should now appear in the **Source attribute** list.</span><span class="sxs-lookup"><span data-stu-id="91f8a-654">Your new attribute should now appear in the **Source attribute** list.</span></span>

15. <span data-ttu-id="91f8a-655">Add a mapping for your new attribute as desired.</span><span class="sxs-lookup"><span data-stu-id="91f8a-655">Add a mapping for your new attribute as desired.</span></span>

16. <span data-ttu-id="91f8a-656">When finished, remember to set **Provisioning Status** back to **On** and save.</span><span class="sxs-lookup"><span data-stu-id="91f8a-656">When finished, remember to set **Provisioning Status** back to **On** and save.</span></span>

## <a name="known-issues"></a><span data-ttu-id="91f8a-657">Known issues</span><span class="sxs-lookup"><span data-stu-id="91f8a-657">Known issues</span></span>

* <span data-ttu-id="91f8a-658">When running the **Add-ADSyncAgentAzureActiveDirectoryConfiguration** Powershell command, there is presently a known issue with global administrator credentials not working if they use a custom domain (example: admin@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="91f8a-658">When running the **Add-ADSyncAgentAzureActiveDirectoryConfiguration** Powershell command, there is presently a known issue with global administrator credentials not working if they use a custom domain (example: admin@contoso.com).</span></span> <span data-ttu-id="91f8a-659">As a workaround, create and use a global administrator account in Azure AD with an onmicrosoft.com domain (example: admin@contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="91f8a-659">As a workaround, create and use a global administrator account in Azure AD with an onmicrosoft.com domain (example: admin@contoso.onmicrosoft.com).</span></span>

* <span data-ttu-id="91f8a-660">Writing data to the thumbnailPhoto user attribute in on-premises Active Directory is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="91f8a-660">Writing data to the thumbnailPhoto user attribute in on-premises Active Directory is not currently supported.</span></span>

* <span data-ttu-id="91f8a-661">The "Workday to Azure AD" connector is not currently supported on Azure AD tenants where AAD Connect is enabled.</span><span class="sxs-lookup"><span data-stu-id="91f8a-661">The "Workday to Azure AD" connector is not currently supported on Azure AD tenants where AAD Connect is enabled.</span></span>  

* <span data-ttu-id="91f8a-662">A previous issue with audit logs not appearing in Azure AD tenants located in the European Union has been resolved.</span><span class="sxs-lookup"><span data-stu-id="91f8a-662">A previous issue with audit logs not appearing in Azure AD tenants located in the European Union has been resolved.</span></span> <span data-ttu-id="91f8a-663">However, additional agent configuration is required for Azure AD tenants in the EU.</span><span class="sxs-lookup"><span data-stu-id="91f8a-663">However, additional agent configuration is required for Azure AD tenants in the EU.</span></span> <span data-ttu-id="91f8a-664">For details, see [Part 3: Configure the on-premises synchronization agent](#Part 3: Configure the on-premises synchronization agent)</span><span class="sxs-lookup"><span data-stu-id="91f8a-664">For details, see [Part 3: Configure the on-premises synchronization agent](#Part 3: Configure the on-premises synchronization agent)</span></span>

## <a name="managing-personal-data"></a><span data-ttu-id="91f8a-665">Managing personal data</span><span class="sxs-lookup"><span data-stu-id="91f8a-665">Managing personal data</span></span>

<span data-ttu-id="91f8a-666">The Workday provisioning solution for Active Directory requires a synchronization agent to be installed on a domain-joined server, and this agent creates logs in the Windows Event log which can contain personally-identifiable information.</span><span class="sxs-lookup"><span data-stu-id="91f8a-666">The Workday provisioning solution for Active Directory requires a synchronization agent to be installed on a domain-joined server, and this agent creates logs in the Windows Event log which can contain personally-identifiable information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91f8a-667">Next steps</span><span class="sxs-lookup"><span data-stu-id="91f8a-667">Next steps</span></span>

* [<span data-ttu-id="91f8a-668">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="91f8a-668">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)
* [<span data-ttu-id="91f8a-669">Learn how to configure single sign-on between Workday and Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f8a-669">Learn how to configure single sign-on between Workday and Azure Active Directory</span></span>](workday-tutorial.md)
* [<span data-ttu-id="91f8a-670">Learn how to integrate other SaaS applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f8a-670">Learn how to integrate other SaaS applications with Azure Active Directory</span></span>](tutorial-list.md)

