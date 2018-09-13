---
title: Customizing Azure AD Attribute Mappings | Microsoft Docs
description: Learn what attribute mappings for SaaS apps in Azure Active Directory are how you can modify them to address your business needs.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b149973b457a2275b0606146ae313d2a4cd2ce6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540929"
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="2d764-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d764-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="2d764-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span><span class="sxs-lookup"><span data-stu-id="2d764-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="2d764-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span><span class="sxs-lookup"><span data-stu-id="2d764-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="2d764-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span><span class="sxs-lookup"><span data-stu-id="2d764-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="2d764-107">Some apps manage other types of objects, such as Groups or Contacts.</span><span class="sxs-lookup"><span data-stu-id="2d764-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="2d764-108">You can customize the default attribute mappings according to your business needs.</span><span class="sxs-lookup"><span data-stu-id="2d764-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="2d764-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span><span class="sxs-lookup"><span data-stu-id="2d764-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="2d764-110">In the Azure AD portal, you can access this feature by clicking Attributes in the toolbar of a SaaS application.</span><span class="sxs-lookup"><span data-stu-id="2d764-110">In the Azure AD portal, you can access this feature by clicking Attributes in the toolbar of a SaaS application.</span></span>

> [!NOTE]
> <span data-ttu-id="2d764-111">The **Attributes** link is only available if you have user provisioning enabled for a SaaS application.</span><span class="sxs-lookup"><span data-stu-id="2d764-111">The **Attributes** link is only available if you have user provisioning enabled for a SaaS application.</span></span> 
> 
> 

![Salesforce][1] 

<span data-ttu-id="2d764-113">When you click Attributes in the toolbar, the list of current mappings that are configured for a SaaS application.</span><span class="sxs-lookup"><span data-stu-id="2d764-113">When you click Attributes in the toolbar, the list of current mappings that are configured for a SaaS application.</span></span>

<span data-ttu-id="2d764-114">The following screenshot shows an example for this:</span><span class="sxs-lookup"><span data-stu-id="2d764-114">The following screenshot shows an example for this:</span></span>

![Salesforce][2]  

<span data-ttu-id="2d764-116">In the example above, you can see that the **firstName** attribute of a managed object in Salesforce is populated with the **givenName** value of the linked Azure AD object.</span><span class="sxs-lookup"><span data-stu-id="2d764-116">In the example above, you can see that the **firstName** attribute of a managed object in Salesforce is populated with the **givenName** value of the linked Azure AD object.</span></span>

<span data-ttu-id="2d764-117">If you either want to customize your attribute mappings or if you want to revert customized settings back to the default configuration, you can do this by clicking the related button in the toolbar on the bottom of an application.</span><span class="sxs-lookup"><span data-stu-id="2d764-117">If you either want to customize your attribute mappings or if you want to revert customized settings back to the default configuration, you can do this by clicking the related button in the toolbar on the bottom of an application.</span></span>

![Salesforce][3]  

<span data-ttu-id="2d764-119">There are attribute mappings that are required by a SaaS application to function correctly.</span><span class="sxs-lookup"><span data-stu-id="2d764-119">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="2d764-120">In the attributes table, the related attribute mappings have **Yes** as value for the **Required** attribute.</span><span class="sxs-lookup"><span data-stu-id="2d764-120">In the attributes table, the related attribute mappings have **Yes** as value for the **Required** attribute.</span></span> <span data-ttu-id="2d764-121">If an attribute mapping is required, you cannot delete it.</span><span class="sxs-lookup"><span data-stu-id="2d764-121">If an attribute mapping is required, you cannot delete it.</span></span> <span data-ttu-id="2d764-122">In this case, **Delete** feature is unavailable.</span><span class="sxs-lookup"><span data-stu-id="2d764-122">In this case, **Delete** feature is unavailable.</span></span>

<span data-ttu-id="2d764-123">To modify an existing attribute mapping, select the mapping, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="2d764-123">To modify an existing attribute mapping, select the mapping, and then click **Edit**.</span></span> <span data-ttu-id="2d764-124">This brings up a dialog page that enables you to modify the selected attribute mapping.</span><span class="sxs-lookup"><span data-stu-id="2d764-124">This brings up a dialog page that enables you to modify the selected attribute mapping.</span></span>

![Edit Attribute Mapping][4]  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="2d764-126">Understanding Attribute Mapping Types</span><span class="sxs-lookup"><span data-stu-id="2d764-126">Understanding Attribute Mapping Types</span></span>
<span data-ttu-id="2d764-127">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span><span class="sxs-lookup"><span data-stu-id="2d764-127">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="2d764-128">There are four different mapping types supported:</span><span class="sxs-lookup"><span data-stu-id="2d764-128">There are four different mapping types supported:</span></span>

* <span data-ttu-id="2d764-129">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d764-129">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="2d764-130">**Constant** – the target attribute is populated with a specific string you have specified.</span><span class="sxs-lookup"><span data-stu-id="2d764-130">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="2d764-131">**Expression** - the target attribute is populated based on the result of a script-like expression.</span><span class="sxs-lookup"><span data-stu-id="2d764-131">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="2d764-132">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="2d764-132">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="2d764-133">**None** - the target attribute is left unmodified.</span><span class="sxs-lookup"><span data-stu-id="2d764-133">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="2d764-134">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span><span class="sxs-lookup"><span data-stu-id="2d764-134">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="2d764-135">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of a **default** value assignment.</span><span class="sxs-lookup"><span data-stu-id="2d764-135">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of a **default** value assignment.</span></span> <span data-ttu-id="2d764-136">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span><span class="sxs-lookup"><span data-stu-id="2d764-136">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span>

<span data-ttu-id="2d764-137">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span><span class="sxs-lookup"><span data-stu-id="2d764-137">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="2d764-138">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span><span class="sxs-lookup"><span data-stu-id="2d764-138">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="2d764-139">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span><span class="sxs-lookup"><span data-stu-id="2d764-139">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="2d764-140">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span><span class="sxs-lookup"><span data-stu-id="2d764-140">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="2d764-141">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span><span class="sxs-lookup"><span data-stu-id="2d764-141">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="related-articles"></a><span data-ttu-id="2d764-142">Related Articles</span><span class="sxs-lookup"><span data-stu-id="2d764-142">Related Articles</span></span>
* [<span data-ttu-id="2d764-143">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d764-143">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="2d764-144">Automate User Provisioning/Deprovisioning to SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="2d764-144">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="2d764-145">Writing Expressions for Attribute Mappings</span><span class="sxs-lookup"><span data-stu-id="2d764-145">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="2d764-146">Scoping Filters for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="2d764-146">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="2d764-147">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="2d764-147">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="2d764-148">Account Provisioning Notifications</span><span class="sxs-lookup"><span data-stu-id="2d764-148">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="2d764-149">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="2d764-149">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-customizing-attribute-mappings/ic775421.png




