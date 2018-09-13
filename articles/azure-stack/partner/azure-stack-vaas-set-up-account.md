---
title: Set up your Azure Stack validation as a service account | Microsoft Docs
description: Learn how to set up your validation as a service account.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: b94d37d528739247cb4f94a17dadf3876c4db6bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870855"
---
# <a name="set-up-your-validation-as-a-service-account"></a><span data-ttu-id="ab3fc-103">Set up your validation as a service account</span><span class="sxs-lookup"><span data-stu-id="ab3fc-103">Set up your validation as a service account</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="ab3fc-104">Validation as a service (VaaS) is an Azure service that is made available to Microsoft Azure Stack partners who have a co-engineering agreement with Microsoft to design, develop, validate, sell, deploy, and support Azure Stack solutions in the market.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-104">Validation as a service (VaaS) is an Azure service that is made available to Microsoft Azure Stack partners who have a co-engineering agreement with Microsoft to design, develop, validate, sell, deploy, and support Azure Stack solutions in the market.</span></span>

<span data-ttu-id="ab3fc-105">Learn how to get your system ready for validation as service.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-105">Learn how to get your system ready for validation as service.</span></span> <span data-ttu-id="ab3fc-106">Set up the Azure Active Directory instance and perform other required tasks for getting ready to use VaaS.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-106">Set up the Azure Active Directory instance and perform other required tasks for getting ready to use VaaS.</span></span> 

<span data-ttu-id="ab3fc-107">The tasks include:</span><span class="sxs-lookup"><span data-stu-id="ab3fc-107">The tasks include:</span></span>

- <span data-ttu-id="ab3fc-108">Create an Azure Storage blob to store logs</span><span class="sxs-lookup"><span data-stu-id="ab3fc-108">Create an Azure Storage blob to store logs</span></span>
- <span data-ttu-id="ab3fc-109">Deploy the local agent</span><span class="sxs-lookup"><span data-stu-id="ab3fc-109">Deploy the local agent</span></span>
- <span data-ttu-id="ab3fc-110">Download test image virtual machines on the Azure Stack instance to be tested</span><span class="sxs-lookup"><span data-stu-id="ab3fc-110">Download test image virtual machines on the Azure Stack instance to be tested</span></span>

## <a name="create-an-azure-active-directory-tenant-id"></a><span data-ttu-id="ab3fc-111">Create an Azure Active Directory tenant ID</span><span class="sxs-lookup"><span data-stu-id="ab3fc-111">Create an Azure Active Directory tenant ID</span></span>

1. <span data-ttu-id="ab3fc-112">Create an Azure Active Directory tenant in the [Azure portal](https://portal.azure.com) or use an existing tenant.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-112">Create an Azure Active Directory tenant in the [Azure portal](https://portal.azure.com) or use an existing tenant.</span></span>

    <span data-ttu-id="ab3fc-113">It is recommended to create a tenant specifically for use with VaaS with a descriptive name, such as, ContosoVaaS@onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-113">It is recommended to create a tenant specifically for use with VaaS with a descriptive name, such as, ContosoVaaS@onmicrosoft.com.</span></span> <span data-ttu-id="ab3fc-114">The Role-based access control (RBAC) features of the tenant will be used by the partner to manage who in the partner organization can use VaaS.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-114">The Role-based access control (RBAC) features of the tenant will be used by the partner to manage who in the partner organization can use VaaS.</span></span>  
    
    <span data-ttu-id="ab3fc-115">More information, see [Manage your Azure AD directory](https://docs.microsoft.com/azure/active-directory/active-directory-administer).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-115">More information, see [Manage your Azure AD directory](https://docs.microsoft.com/azure/active-directory/active-directory-administer).</span></span>

    > [!Note]  
    > <span data-ttu-id="ab3fc-116">For more information about creating new Azure Active Directory tenants, see [Get started with Azure AD](https://docs.microsoft.com/azure/active-directory/get-started-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-116">For more information about creating new Azure Active Directory tenants, see [Get started with Azure AD](https://docs.microsoft.com/azure/active-directory/get-started-azure-ad).</span></span>

2. <span data-ttu-id="ab3fc-117">Add members of your organization who will be responsible for using the service to the tenant.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-117">Add members of your organization who will be responsible for using the service to the tenant.</span></span> <span data-ttu-id="ab3fc-118">Assign each user in the tenant one of the following roles to control their access level to VaaS:</span><span class="sxs-lookup"><span data-stu-id="ab3fc-118">Assign each user in the tenant one of the following roles to control their access level to VaaS:</span></span>

    | <span data-ttu-id="ab3fc-119">Role Name</span><span class="sxs-lookup"><span data-stu-id="ab3fc-119">Role Name</span></span> | <span data-ttu-id="ab3fc-120">Description</span><span class="sxs-lookup"><span data-stu-id="ab3fc-120">Description</span></span> |
    |---------------------|------------------------------------------|
    | <span data-ttu-id="ab3fc-121">Owner</span><span class="sxs-lookup"><span data-stu-id="ab3fc-121">Owner</span></span> | <span data-ttu-id="ab3fc-122">Has full access to all resources.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-122">Has full access to all resources.</span></span> |
    | <span data-ttu-id="ab3fc-123">Reader</span><span class="sxs-lookup"><span data-stu-id="ab3fc-123">Reader</span></span> | <span data-ttu-id="ab3fc-124">Can view all resources but not edit.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-124">Can view all resources but not edit.</span></span> |
    | <span data-ttu-id="ab3fc-125">Test Contributor</span><span class="sxs-lookup"><span data-stu-id="ab3fc-125">Test Contributor</span></span> | <span data-ttu-id="ab3fc-126">Can manage test resources.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-126">Can manage test resources.</span></span> |
    | <span data-ttu-id="ab3fc-127">Catalog Contributor</span><span class="sxs-lookup"><span data-stu-id="ab3fc-127">Catalog Contributor</span></span> | <span data-ttu-id="ab3fc-128">Can manage solution publishing resources.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-128">Can manage solution publishing resources.</span></span> |

## <a name="set-up-your-tenant"></a><span data-ttu-id="ab3fc-129">Set up your tenant</span><span class="sxs-lookup"><span data-stu-id="ab3fc-129">Set up your tenant</span></span>

<span data-ttu-id="ab3fc-130">Set up your tenant in the **Azure Stack Validation Service** application.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-130">Set up your tenant in the **Azure Stack Validation Service** application.</span></span> 

1. <span data-ttu-id="ab3fc-131">Send the following information about the tenant to Microsoft at vaashelp@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-131">Send the following information about the tenant to Microsoft at vaashelp@microsoft.com.</span></span>

    | <span data-ttu-id="ab3fc-132">Data</span><span class="sxs-lookup"><span data-stu-id="ab3fc-132">Data</span></span> | <span data-ttu-id="ab3fc-133">Description</span><span class="sxs-lookup"><span data-stu-id="ab3fc-133">Description</span></span> |
    |--------------------------------|---------------------------------------------------------------------------------------------|
    | <span data-ttu-id="ab3fc-134">Organization Name</span><span class="sxs-lookup"><span data-stu-id="ab3fc-134">Organization Name</span></span> | <span data-ttu-id="ab3fc-135">Official organization name.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-135">Official organization name.</span></span> |
    | <span data-ttu-id="ab3fc-136">Azure AD Tenant Directory Name</span><span class="sxs-lookup"><span data-stu-id="ab3fc-136">Azure AD Tenant Directory Name</span></span> | <span data-ttu-id="ab3fc-137">Azure AD Tenant Directory name being registered.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-137">Azure AD Tenant Directory name being registered.</span></span> |
    | <span data-ttu-id="ab3fc-138">Azure AD Tenant Directory Id</span><span class="sxs-lookup"><span data-stu-id="ab3fc-138">Azure AD Tenant Directory Id</span></span> | <span data-ttu-id="ab3fc-139">Azure AD Tenant Directory GUID associated with the directory.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-139">Azure AD Tenant Directory GUID associated with the directory.</span></span><br> <span data-ttu-id="ab3fc-140">For information on how to find your Azure AD Tenant Directory ID can be found, see "[Get tenant ID](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)."</span><span class="sxs-lookup"><span data-stu-id="ab3fc-140">For information on how to find your Azure AD Tenant Directory ID can be found, see "[Get tenant ID](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)."</span></span> |

    

2. <span data-ttu-id="ab3fc-141">The Azure Stack team provides confirmation that your tenant can use the VaaS portal.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-141">The Azure Stack team provides confirmation that your tenant can use the VaaS portal.</span></span>

3. <span data-ttu-id="ab3fc-142">Use the global admin credentials for the tenant to sign into the [VaaS portal](https://azurestackvalidation.com/
).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-142">Use the global admin credentials for the tenant to sign into the [VaaS portal](https://azurestackvalidation.com/
).</span></span> <span data-ttu-id="ab3fc-143">Select **My Account**.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-143">Select **My Account**.</span></span>

    ![Sign to the VaaS portal](media/vaas_portalsignin.png)

3. <span data-ttu-id="ab3fc-145">The site will prompted you to grant access for VaaS.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-145">The site will prompted you to grant access for VaaS.</span></span> <span data-ttu-id="ab3fc-146">Accept the terms to proceed.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-146">Accept the terms to proceed.</span></span>

## <a name="assign-user-roles"></a><span data-ttu-id="ab3fc-147">Assign user roles</span><span class="sxs-lookup"><span data-stu-id="ab3fc-147">Assign user roles</span></span>

<span data-ttu-id="ab3fc-148">To assign a user role:</span><span class="sxs-lookup"><span data-stu-id="ab3fc-148">To assign a user role:</span></span>

1. <span data-ttu-id="ab3fc-149">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-149">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ab3fc-150">Select **All Services** > **Azure Active Directory** in the **Identity** group.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-150">Select **All Services** > **Azure Active Directory** in the **Identity** group.</span></span>
3. <span data-ttu-id="ab3fc-151">Select **Enterprise Applications** > **Azure Stack Validation Service** application.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-151">Select **Enterprise Applications** > **Azure Stack Validation Service** application.</span></span>
4. <span data-ttu-id="ab3fc-152">Select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-152">Select **Users and groups**.</span></span> <span data-ttu-id="ab3fc-153">The **Azure Stack Validation Service - Users and group** blade lists the users with permission to use the application.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-153">The **Azure Stack Validation Service - Users and group** blade lists the users with permission to use the application.</span></span>
5. <span data-ttu-id="ab3fc-154">Select **+ Add user** to add an assignment.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-154">Select **+ Add user** to add an assignment.</span></span>

## <a name="create-an-azure-storage-blob-to-store-logs"></a><span data-ttu-id="ab3fc-155">Create an Azure storage blob to store logs</span><span class="sxs-lookup"><span data-stu-id="ab3fc-155">Create an Azure storage blob to store logs</span></span>

<span data-ttu-id="ab3fc-156">VaaS creates diagnostic logs when running the validation tests.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-156">VaaS creates diagnostic logs when running the validation tests.</span></span> <span data-ttu-id="ab3fc-157">You need a location an Azure blob service SAS URL to store your logs.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-157">You need a location an Azure blob service SAS URL to store your logs.</span></span> <span data-ttu-id="ab3fc-158">The storage account may also be used to the store the OEM customization packages.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-158">The storage account may also be used to the store the OEM customization packages.</span></span>

<span data-ttu-id="ab3fc-159">These steps walk through how to set up and generate a storage-as-a-service (SAS) URI for an Azure storage account, and where to specify the storage account in the VaaS portal when starting tests in the portal.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-159">These steps walk through how to set up and generate a storage-as-a-service (SAS) URI for an Azure storage account, and where to specify the storage account in the VaaS portal when starting tests in the portal.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="ab3fc-160">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="ab3fc-160">Create an Azure storage account</span></span>

1. <span data-ttu-id="ab3fc-161">To create a storage account, follow the instructions, [Create a storage account](../../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-161">To create a storage account, follow the instructions, [Create a storage account](../../storage/common/storage-quickstart-create-account.md).</span></span>

2. <span data-ttu-id="ab3fc-162">When selecting the type of storage account, select the **Blob storage** account type.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-162">When selecting the type of storage account, select the **Blob storage** account type.</span></span>

### <a name="generate-a-sas-url-for-the-storage-account"></a><span data-ttu-id="ab3fc-163">Generate a SAS URL for the storage account</span><span class="sxs-lookup"><span data-stu-id="ab3fc-163">Generate a SAS URL for the storage account</span></span>

1. <span data-ttu-id="ab3fc-164">Navigate to the storage account created above.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-164">Navigate to the storage account created above.</span></span>

2. <span data-ttu-id="ab3fc-165">On the blade under **Settings**, select **Shared access signature**.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-165">On the blade under **Settings**, select **Shared access signature**.</span></span>

3. <span data-ttu-id="ab3fc-166">Check only **Blob** from **Allowed Services options** (uncheck the remaining).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-166">Check only **Blob** from **Allowed Services options** (uncheck the remaining).</span></span>

4. <span data-ttu-id="ab3fc-167">Check **Service**, \*\*Container, and **Object** from **Allowed resource types**.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-167">Check **Service**, \*\*Container, and **Object** from **Allowed resource types**.</span></span>

5. <span data-ttu-id="ab3fc-168">Check **Read**, **Write**, **List**, **Add**, **Create** from **Allowed permissions** (uncheck the remaining).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-168">Check **Read**, **Write**, **List**, **Add**, **Create** from **Allowed permissions** (uncheck the remaining).</span></span>

6. <span data-ttu-id="ab3fc-169">Set **Start time** to the current time, and **End time** to three months from the current time.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-169">Set **Start time** to the current time, and **End time** to three months from the current time.</span></span>

7. <span data-ttu-id="ab3fc-170">Select **Generate SAS and connection string** and save the **Blob service SAS URL** string.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-170">Select **Generate SAS and connection string** and save the **Blob service SAS URL** string.</span></span>

> [!Note]  
> <span data-ttu-id="ab3fc-171">The SAS URL expires at the end time set when the URL was generated.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-171">The SAS URL expires at the end time set when the URL was generated.</span></span> <span data-ttu-id="ab3fc-172">Ensure that the URL is sufficiently valid before sharing it with product team for debugging, or that the URL is valid for more than 30 days when scheduling tests.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-172">Ensure that the URL is sufficiently valid before sharing it with product team for debugging, or that the URL is valid for more than 30 days when scheduling tests.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab3fc-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab3fc-173">Next steps</span></span>

- <span data-ttu-id="ab3fc-174">Use the VaaS local agent to check your hardware.</span><span class="sxs-lookup"><span data-stu-id="ab3fc-174">Use the VaaS local agent to check your hardware.</span></span> <span data-ttu-id="ab3fc-175">For instruction, see [Deploy the local agent and test virtual machines](azure-stack-vaas-test-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-175">For instruction, see [Deploy the local agent and test virtual machines](azure-stack-vaas-test-vm.md).</span></span>
- <span data-ttu-id="ab3fc-176">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="ab3fc-176">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>