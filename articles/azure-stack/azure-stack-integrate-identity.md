---
title: Azure Stack datacenter integration - Identity
description: Learn how to integrate Azure Stack AD FS with your datacenter AD FS
services: azure-stack
author: jeffgilb
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 08/07/2018
ms.author: jeffgilb
ms.reviewer: wfayed
keywords: ''
ms.openlocfilehash: 9bbe55e08d7a005d38c5608df39f9285d79eb203
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869498"
---
# <a name="azure-stack-datacenter-integration---identity"></a><span data-ttu-id="247f5-103">Azure Stack datacenter integration - Identity</span><span class="sxs-lookup"><span data-stu-id="247f5-103">Azure Stack datacenter integration - Identity</span></span>
<span data-ttu-id="247f5-104">You can deploy Azure Stack using Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) as the identity providers.</span><span class="sxs-lookup"><span data-stu-id="247f5-104">You can deploy Azure Stack using Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) as the identity providers.</span></span> <span data-ttu-id="247f5-105">You must make the choice before you deploy Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-105">You must make the choice before you deploy Azure Stack.</span></span> <span data-ttu-id="247f5-106">Deployment using AD FS is also referred to as deploying Azure Stack in disconnected mode.</span><span class="sxs-lookup"><span data-stu-id="247f5-106">Deployment using AD FS is also referred to as deploying Azure Stack in disconnected mode.</span></span>

<span data-ttu-id="247f5-107">The following table shows the differences between the two identity choices:</span><span class="sxs-lookup"><span data-stu-id="247f5-107">The following table shows the differences between the two identity choices:</span></span>

||<span data-ttu-id="247f5-108">Disconnected from the internet</span><span class="sxs-lookup"><span data-stu-id="247f5-108">Disconnected from the internet</span></span>|<span data-ttu-id="247f5-109">Connected to the internet</span><span class="sxs-lookup"><span data-stu-id="247f5-109">Connected to the internet</span></span>|
|---------|---------|---------|
|<span data-ttu-id="247f5-110">Billing</span><span class="sxs-lookup"><span data-stu-id="247f5-110">Billing</span></span>|<span data-ttu-id="247f5-111">Must be Capacity</span><span class="sxs-lookup"><span data-stu-id="247f5-111">Must be Capacity</span></span><br> <span data-ttu-id="247f5-112">Enterprise Agreement (EA) only</span><span class="sxs-lookup"><span data-stu-id="247f5-112">Enterprise Agreement (EA) only</span></span>|<span data-ttu-id="247f5-113">Capacity or Pay-as-you-use</span><span class="sxs-lookup"><span data-stu-id="247f5-113">Capacity or Pay-as-you-use</span></span><br><span data-ttu-id="247f5-114">EA or Cloud Solution Provider (CSP)</span><span class="sxs-lookup"><span data-stu-id="247f5-114">EA or Cloud Solution Provider (CSP)</span></span>|
|<span data-ttu-id="247f5-115">Identity</span><span class="sxs-lookup"><span data-stu-id="247f5-115">Identity</span></span>|<span data-ttu-id="247f5-116">Must be AD FS</span><span class="sxs-lookup"><span data-stu-id="247f5-116">Must be AD FS</span></span>|<span data-ttu-id="247f5-117">Azure AD or AD FS</span><span class="sxs-lookup"><span data-stu-id="247f5-117">Azure AD or AD FS</span></span>|
|<span data-ttu-id="247f5-118">Marketplace</span><span class="sxs-lookup"><span data-stu-id="247f5-118">Marketplace</span></span> |<span data-ttu-id="247f5-119">Supported</span><span class="sxs-lookup"><span data-stu-id="247f5-119">Supported</span></span><br><span data-ttu-id="247f5-120">BYOL licensing</span><span class="sxs-lookup"><span data-stu-id="247f5-120">BYOL licensing</span></span>|<span data-ttu-id="247f5-121">Supported</span><span class="sxs-lookup"><span data-stu-id="247f5-121">Supported</span></span><br><span data-ttu-id="247f5-122">BYOL licensing</span><span class="sxs-lookup"><span data-stu-id="247f5-122">BYOL licensing</span></span>|
|<span data-ttu-id="247f5-123">Registration</span><span class="sxs-lookup"><span data-stu-id="247f5-123">Registration</span></span>|<span data-ttu-id="247f5-124">Recommended, requires removable media</span><span class="sxs-lookup"><span data-stu-id="247f5-124">Recommended, requires removable media</span></span><br> <span data-ttu-id="247f5-125">and a separate connected device.</span><span class="sxs-lookup"><span data-stu-id="247f5-125">and a separate connected device.</span></span>|<span data-ttu-id="247f5-126">Automated</span><span class="sxs-lookup"><span data-stu-id="247f5-126">Automated</span></span>|
|<span data-ttu-id="247f5-127">Patch and update</span><span class="sxs-lookup"><span data-stu-id="247f5-127">Patch and update</span></span>|<span data-ttu-id="247f5-128">Required, requires removable media</span><span class="sxs-lookup"><span data-stu-id="247f5-128">Required, requires removable media</span></span><br> <span data-ttu-id="247f5-129">and a separate connected device.</span><span class="sxs-lookup"><span data-stu-id="247f5-129">and a separate connected device.</span></span>|<span data-ttu-id="247f5-130">Update package can be downloaded directly</span><span class="sxs-lookup"><span data-stu-id="247f5-130">Update package can be downloaded directly</span></span><br> <span data-ttu-id="247f5-131">from the Internet to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-131">from the Internet to Azure Stack.</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="247f5-132">You cannot switch the identity provider without redeploying the entire Azure Stack solution.</span><span class="sxs-lookup"><span data-stu-id="247f5-132">You cannot switch the identity provider without redeploying the entire Azure Stack solution.</span></span>

## <a name="active-directory-federation-services-and-graph"></a><span data-ttu-id="247f5-133">Active Directory Federation Services and Graph</span><span class="sxs-lookup"><span data-stu-id="247f5-133">Active Directory Federation Services and Graph</span></span>

<span data-ttu-id="247f5-134">Deploying with AD FS allows identities in an existing Active Directory forest to authenticate with resources in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-134">Deploying with AD FS allows identities in an existing Active Directory forest to authenticate with resources in Azure Stack.</span></span> <span data-ttu-id="247f5-135">This existing Active Directory forest requires a deployment of AD FS to allow the creation of an AD FS federation trust.</span><span class="sxs-lookup"><span data-stu-id="247f5-135">This existing Active Directory forest requires a deployment of AD FS to allow the creation of an AD FS federation trust.</span></span>

<span data-ttu-id="247f5-136">Authentication is one part of identity.</span><span class="sxs-lookup"><span data-stu-id="247f5-136">Authentication is one part of identity.</span></span> <span data-ttu-id="247f5-137">To manage Role Based Access Control (RBAC) in Azure Stack, the Graph component must be configured.</span><span class="sxs-lookup"><span data-stu-id="247f5-137">To manage Role Based Access Control (RBAC) in Azure Stack, the Graph component must be configured.</span></span> <span data-ttu-id="247f5-138">When access to a resource is delegated, the Graph component looks up the user account in the existing Active Directory forest using the LDAP protocol.</span><span class="sxs-lookup"><span data-stu-id="247f5-138">When access to a resource is delegated, the Graph component looks up the user account in the existing Active Directory forest using the LDAP protocol.</span></span>

![Azure Stack AD FS architecture](media/azure-stack-integrate-identity/Azure-Stack-ADFS-architecture.png)

<span data-ttu-id="247f5-140">The existing AD FS is the account security token service (STS) that sends claims to the Azure Stack AD FS (the resource STS).</span><span class="sxs-lookup"><span data-stu-id="247f5-140">The existing AD FS is the account security token service (STS) that sends claims to the Azure Stack AD FS (the resource STS).</span></span> <span data-ttu-id="247f5-141">In Azure Stack, automation creates the claims provider trust with the metadata endpoint for the existing AD FS.</span><span class="sxs-lookup"><span data-stu-id="247f5-141">In Azure Stack, automation creates the claims provider trust with the metadata endpoint for the existing AD FS.</span></span>

<span data-ttu-id="247f5-142">At the existing AD FS, a relying party trust must be configured.</span><span class="sxs-lookup"><span data-stu-id="247f5-142">At the existing AD FS, a relying party trust must be configured.</span></span> <span data-ttu-id="247f5-143">This step is not done by the automation, and must be configured by the operator.</span><span class="sxs-lookup"><span data-stu-id="247f5-143">This step is not done by the automation, and must be configured by the operator.</span></span> <span data-ttu-id="247f5-144">The Azure Stack metadata endpoint is documented in the AzureStackStampDeploymentInfo.JSON file, or via the privileged endpoint by running the command `Get-AzureStackInfo`.</span><span class="sxs-lookup"><span data-stu-id="247f5-144">The Azure Stack metadata endpoint is documented in the AzureStackStampDeploymentInfo.JSON file, or via the privileged endpoint by running the command `Get-AzureStackInfo`.</span></span>

<span data-ttu-id="247f5-145">The relying party trust configuration also requires you to configure the claim transformation rules that are provided by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="247f5-145">The relying party trust configuration also requires you to configure the claim transformation rules that are provided by Microsoft.</span></span>

<span data-ttu-id="247f5-146">For the Graph configuration, a service account must be provided that has Read permission in the existing Active Directory.</span><span class="sxs-lookup"><span data-stu-id="247f5-146">For the Graph configuration, a service account must be provided that has Read permission in the existing Active Directory.</span></span> <span data-ttu-id="247f5-147">This account is required as input for the automation to enable RBAC scenarios.</span><span class="sxs-lookup"><span data-stu-id="247f5-147">This account is required as input for the automation to enable RBAC scenarios.</span></span>

<span data-ttu-id="247f5-148">For the last step, a new owner is configured for the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="247f5-148">For the last step, a new owner is configured for the default provider subscription.</span></span> <span data-ttu-id="247f5-149">This account has full access to all resources when signed in to the Azure Stack administrator portal.</span><span class="sxs-lookup"><span data-stu-id="247f5-149">This account has full access to all resources when signed in to the Azure Stack administrator portal.</span></span>

<span data-ttu-id="247f5-150">Requirements:</span><span class="sxs-lookup"><span data-stu-id="247f5-150">Requirements:</span></span>


|<span data-ttu-id="247f5-151">Component</span><span class="sxs-lookup"><span data-stu-id="247f5-151">Component</span></span>|<span data-ttu-id="247f5-152">Requirement</span><span class="sxs-lookup"><span data-stu-id="247f5-152">Requirement</span></span>|
|---------|---------|
|<span data-ttu-id="247f5-153">Graph</span><span class="sxs-lookup"><span data-stu-id="247f5-153">Graph</span></span>|<span data-ttu-id="247f5-154">Microsoft Active Directory 2012/2012 R2/2016</span><span class="sxs-lookup"><span data-stu-id="247f5-154">Microsoft Active Directory 2012/2012 R2/2016</span></span>|
|<span data-ttu-id="247f5-155">AD FS</span><span class="sxs-lookup"><span data-stu-id="247f5-155">AD FS</span></span>|<span data-ttu-id="247f5-156">Windows Server 2012/2012 R2/2016</span><span class="sxs-lookup"><span data-stu-id="247f5-156">Windows Server 2012/2012 R2/2016</span></span>|

## <a name="setting-up-graph-integration"></a><span data-ttu-id="247f5-157">Setting up Graph integration</span><span class="sxs-lookup"><span data-stu-id="247f5-157">Setting up Graph integration</span></span>

<span data-ttu-id="247f5-158">Graph only supports integration with a single Active Directory forest.</span><span class="sxs-lookup"><span data-stu-id="247f5-158">Graph only supports integration with a single Active Directory forest.</span></span> <span data-ttu-id="247f5-159">If multiple forests exist, only the forest specified in the configuration will be used to fetch users and groups.</span><span class="sxs-lookup"><span data-stu-id="247f5-159">If multiple forests exist, only the forest specified in the configuration will be used to fetch users and groups.</span></span>

<span data-ttu-id="247f5-160">The following information is required as inputs for the automation parameters:</span><span class="sxs-lookup"><span data-stu-id="247f5-160">The following information is required as inputs for the automation parameters:</span></span>


|<span data-ttu-id="247f5-161">Parameter</span><span class="sxs-lookup"><span data-stu-id="247f5-161">Parameter</span></span>|<span data-ttu-id="247f5-162">Description</span><span class="sxs-lookup"><span data-stu-id="247f5-162">Description</span></span>|<span data-ttu-id="247f5-163">Example</span><span class="sxs-lookup"><span data-stu-id="247f5-163">Example</span></span>|
|---------|---------|---------|
|<span data-ttu-id="247f5-164">CustomADGlobalCatalog</span><span class="sxs-lookup"><span data-stu-id="247f5-164">CustomADGlobalCatalog</span></span>|<span data-ttu-id="247f5-165">FQDN of the target Active Directory forest</span><span class="sxs-lookup"><span data-stu-id="247f5-165">FQDN of the target Active Directory forest</span></span><br><span data-ttu-id="247f5-166">that you want to integrate with</span><span class="sxs-lookup"><span data-stu-id="247f5-166">that you want to integrate with</span></span>|<span data-ttu-id="247f5-167">Contoso.com</span><span class="sxs-lookup"><span data-stu-id="247f5-167">Contoso.com</span></span>|
|<span data-ttu-id="247f5-168">CustomADAdminCredentials</span><span class="sxs-lookup"><span data-stu-id="247f5-168">CustomADAdminCredentials</span></span>|<span data-ttu-id="247f5-169">A user with LDAP Read permission</span><span class="sxs-lookup"><span data-stu-id="247f5-169">A user with LDAP Read permission</span></span>|<span data-ttu-id="247f5-170">YOURDOMAIN\graphservice</span><span class="sxs-lookup"><span data-stu-id="247f5-170">YOURDOMAIN\graphservice</span></span>|

### <a name="create-user-account-in-the-existing-active-directory-optional"></a><span data-ttu-id="247f5-171">Create user account in the existing Active Directory (optional)</span><span class="sxs-lookup"><span data-stu-id="247f5-171">Create user account in the existing Active Directory (optional)</span></span>

<span data-ttu-id="247f5-172">Optionally, you can create an account for the Graph service in the existing Active Directory.</span><span class="sxs-lookup"><span data-stu-id="247f5-172">Optionally, you can create an account for the Graph service in the existing Active Directory.</span></span> <span data-ttu-id="247f5-173">Perform this step if you don't already have an account that you want to use.</span><span class="sxs-lookup"><span data-stu-id="247f5-173">Perform this step if you don't already have an account that you want to use.</span></span>

1. <span data-ttu-id="247f5-174">In the existing Active Directory, create the following user account (recommendation):</span><span class="sxs-lookup"><span data-stu-id="247f5-174">In the existing Active Directory, create the following user account (recommendation):</span></span>
   - <span data-ttu-id="247f5-175">**Username**: graphservice</span><span class="sxs-lookup"><span data-stu-id="247f5-175">**Username**: graphservice</span></span>
   - <span data-ttu-id="247f5-176">**Password**: use a strong password</span><span class="sxs-lookup"><span data-stu-id="247f5-176">**Password**: use a strong password</span></span><br><span data-ttu-id="247f5-177">Configure the password to never expire.</span><span class="sxs-lookup"><span data-stu-id="247f5-177">Configure the password to never expire.</span></span>

   <span data-ttu-id="247f5-178">No special permissions or membership is required.</span><span class="sxs-lookup"><span data-stu-id="247f5-178">No special permissions or membership is required.</span></span>

#### <a name="trigger-automation-to-configure-graph"></a><span data-ttu-id="247f5-179">Trigger automation to configure graph</span><span class="sxs-lookup"><span data-stu-id="247f5-179">Trigger automation to configure graph</span></span>

<span data-ttu-id="247f5-180">For this procedure, use a computer in your datacenter network that can communicate with the privileged endpoint in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-180">For this procedure, use a computer in your datacenter network that can communicate with the privileged endpoint in Azure Stack.</span></span>

2. <span data-ttu-id="247f5-181">Open an elevated Windows PowerShell session (run as administrator), and connect to the IP address of the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="247f5-181">Open an elevated Windows PowerShell session (run as administrator), and connect to the IP address of the privileged endpoint.</span></span> <span data-ttu-id="247f5-182">Use the credentials for **CloudAdmin** to authenticate.</span><span class="sxs-lookup"><span data-stu-id="247f5-182">Use the credentials for **CloudAdmin** to authenticate.</span></span>

   ```PowerShell  
   $creds = Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

3. <span data-ttu-id="247f5-183">Now that you're connected to the privileged endpoint, run the following command:</span><span class="sxs-lookup"><span data-stu-id="247f5-183">Now that you're connected to the privileged endpoint, run the following command:</span></span> 

   ```PowerShell  
   Register-DirectoryService -CustomADGlobalCatalog contoso.com
   ```

   <span data-ttu-id="247f5-184">When prompted, specify the credential for the user account that you want to use for the Graph service (such as graphservice).</span><span class="sxs-lookup"><span data-stu-id="247f5-184">When prompted, specify the credential for the user account that you want to use for the Graph service (such as graphservice).</span></span> <span data-ttu-id="247f5-185">The input for the Register-DirectoryService cmdlet must be the forest name / root domain in the forest rather than any other domain in the forest.</span><span class="sxs-lookup"><span data-stu-id="247f5-185">The input for the Register-DirectoryService cmdlet must be the forest name / root domain in the forest rather than any other domain in the forest.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="247f5-186">Wait for the credentials pop-up (Get-Credential is not supported in the privileged endpoint) and enter the Graph Service Account credentials.</span><span class="sxs-lookup"><span data-stu-id="247f5-186">Wait for the credentials pop-up (Get-Credential is not supported in the privileged endpoint) and enter the Graph Service Account credentials.</span></span>

#### <a name="graph-protocols-and-ports"></a><span data-ttu-id="247f5-187">Graph protocols and ports</span><span class="sxs-lookup"><span data-stu-id="247f5-187">Graph protocols and ports</span></span>

<span data-ttu-id="247f5-188">Graph service in Azure Stack uses the following protocols and ports to communicate with a writeable Global Catalog Server (GC) and Key Distribution Center (KDC) that can process login requests in the target Active Directory forest.</span><span class="sxs-lookup"><span data-stu-id="247f5-188">Graph service in Azure Stack uses the following protocols and ports to communicate with a writeable Global Catalog Server (GC) and Key Distribution Center (KDC) that can process login requests in the target Active Directory forest.</span></span>

<span data-ttu-id="247f5-189">Graph service in Azure Stack uses the following protocols and ports to communicate with the target Active Directory:</span><span class="sxs-lookup"><span data-stu-id="247f5-189">Graph service in Azure Stack uses the following protocols and ports to communicate with the target Active Directory:</span></span>

|<span data-ttu-id="247f5-190">Type</span><span class="sxs-lookup"><span data-stu-id="247f5-190">Type</span></span>|<span data-ttu-id="247f5-191">Port</span><span class="sxs-lookup"><span data-stu-id="247f5-191">Port</span></span>|<span data-ttu-id="247f5-192">Protocol</span><span class="sxs-lookup"><span data-stu-id="247f5-192">Protocol</span></span>|
|---------|---------|---------|
|<span data-ttu-id="247f5-193">LDAP</span><span class="sxs-lookup"><span data-stu-id="247f5-193">LDAP</span></span>|<span data-ttu-id="247f5-194">389</span><span class="sxs-lookup"><span data-stu-id="247f5-194">389</span></span>|<span data-ttu-id="247f5-195">TCP & UDP</span><span class="sxs-lookup"><span data-stu-id="247f5-195">TCP & UDP</span></span>|
|<span data-ttu-id="247f5-196">LDAP SSL</span><span class="sxs-lookup"><span data-stu-id="247f5-196">LDAP SSL</span></span>|<span data-ttu-id="247f5-197">636</span><span class="sxs-lookup"><span data-stu-id="247f5-197">636</span></span>|<span data-ttu-id="247f5-198">TCP</span><span class="sxs-lookup"><span data-stu-id="247f5-198">TCP</span></span>|
|<span data-ttu-id="247f5-199">LDAP GC</span><span class="sxs-lookup"><span data-stu-id="247f5-199">LDAP GC</span></span>|<span data-ttu-id="247f5-200">3268</span><span class="sxs-lookup"><span data-stu-id="247f5-200">3268</span></span>|<span data-ttu-id="247f5-201">TCP</span><span class="sxs-lookup"><span data-stu-id="247f5-201">TCP</span></span>|
|<span data-ttu-id="247f5-202">LDAP GC SSL</span><span class="sxs-lookup"><span data-stu-id="247f5-202">LDAP GC SSL</span></span>|<span data-ttu-id="247f5-203">3269</span><span class="sxs-lookup"><span data-stu-id="247f5-203">3269</span></span>|<span data-ttu-id="247f5-204">TCP</span><span class="sxs-lookup"><span data-stu-id="247f5-204">TCP</span></span>|

## <a name="setting-up-ad-fs-integration-by-downloading-federation-metadata"></a><span data-ttu-id="247f5-205">Setting up AD FS integration by downloading federation metadata</span><span class="sxs-lookup"><span data-stu-id="247f5-205">Setting up AD FS integration by downloading federation metadata</span></span>

<span data-ttu-id="247f5-206">The following information is required as input for the automation parameters:</span><span class="sxs-lookup"><span data-stu-id="247f5-206">The following information is required as input for the automation parameters:</span></span>

|<span data-ttu-id="247f5-207">Parameter</span><span class="sxs-lookup"><span data-stu-id="247f5-207">Parameter</span></span>|<span data-ttu-id="247f5-208">Description</span><span class="sxs-lookup"><span data-stu-id="247f5-208">Description</span></span>|<span data-ttu-id="247f5-209">Example</span><span class="sxs-lookup"><span data-stu-id="247f5-209">Example</span></span>|
|---------|---------|---------|
|<span data-ttu-id="247f5-210">CustomAdfsName</span><span class="sxs-lookup"><span data-stu-id="247f5-210">CustomAdfsName</span></span>|<span data-ttu-id="247f5-211">Name of the claims provider.<cr>It appears that way on the AD FS landing page.</span><span class="sxs-lookup"><span data-stu-id="247f5-211">Name of the claims provider.<cr>It appears that way on the AD FS landing page.</span></span>|<span data-ttu-id="247f5-212">Contoso</span><span class="sxs-lookup"><span data-stu-id="247f5-212">Contoso</span></span>|
|<span data-ttu-id="247f5-213">CustomAD</span><span class="sxs-lookup"><span data-stu-id="247f5-213">CustomAD</span></span><br><span data-ttu-id="247f5-214">FSFederationMetadataEndpointUri</span><span class="sxs-lookup"><span data-stu-id="247f5-214">FSFederationMetadataEndpointUri</span></span>|<span data-ttu-id="247f5-215">Federation metadata link</span><span class="sxs-lookup"><span data-stu-id="247f5-215">Federation metadata link</span></span>|https://ad01.contoso.com/federationmetadata/2007-06/federationmetadata.xml|


### <a name="trigger-automation-to-configure-claims-provider-trust-in-azure-stack"></a><span data-ttu-id="247f5-216">Trigger automation to configure claims provider trust in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="247f5-216">Trigger automation to configure claims provider trust in Azure Stack</span></span>

<span data-ttu-id="247f5-217">For this procedure, use a computer that can communicate with the privileged endpoint in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-217">For this procedure, use a computer that can communicate with the privileged endpoint in Azure Stack.</span></span> <span data-ttu-id="247f5-218">It is expected that the certificate used by the account **STS AD FS** is trusted by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-218">It is expected that the certificate used by the account **STS AD FS** is trusted by Azure Stack.</span></span>

1. <span data-ttu-id="247f5-219">Open an elevated Windows PowerShell session, and connect to the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="247f5-219">Open an elevated Windows PowerShell session, and connect to the privileged endpoint.</span></span>

   ```PowerShell  
   $creds = Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. <span data-ttu-id="247f5-220">Now that you're connected to the privileged endpoint, run the following command using the parameters appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="247f5-220">Now that you're connected to the privileged endpoint, run the following command using the parameters appropriate for your environment:</span></span>

   ```PowerShell  
   Register-CustomAdfs -CustomAdfsName Contoso -CustomADFSFederationMetadataEndpointUri https://win-SQOOJN70SGL.contoso.com/federationmetadata/2007-06/federationmetadata.xml
   ```

3. <span data-ttu-id="247f5-221">Run the following command to update the owner of the default provider subscription, using the parameters appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="247f5-221">Run the following command to update the owner of the default provider subscription, using the parameters appropriate for your environment:</span></span>

   ```PowerShell  
   Set-ServiceAdminOwner -ServiceAdminOwnerUpn "administrator@contoso.com"
   ```

## <a name="setting-up-ad-fs-integration-by-providing-federation-metadata-file"></a><span data-ttu-id="247f5-222">Setting up AD FS integration by providing federation metadata file</span><span class="sxs-lookup"><span data-stu-id="247f5-222">Setting up AD FS integration by providing federation metadata file</span></span>

<span data-ttu-id="247f5-223">Beginning with version 1807, use this method if the either of the following conditions are true:</span><span class="sxs-lookup"><span data-stu-id="247f5-223">Beginning with version 1807, use this method if the either of the following conditions are true:</span></span>

- <span data-ttu-id="247f5-224">The certificate chain is different for AD FS compared to all other endpoints in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="247f5-224">The certificate chain is different for AD FS compared to all other endpoints in Azure Stack.</span></span>
- <span data-ttu-id="247f5-225">There’s no network connectivity to the existing AD FS server from Azure Stack’s AD FS instance.</span><span class="sxs-lookup"><span data-stu-id="247f5-225">There’s no network connectivity to the existing AD FS server from Azure Stack’s AD FS instance.</span></span>

<span data-ttu-id="247f5-226">The following information is required as input for the automation parameters:</span><span class="sxs-lookup"><span data-stu-id="247f5-226">The following information is required as input for the automation parameters:</span></span>


|<span data-ttu-id="247f5-227">Parameter</span><span class="sxs-lookup"><span data-stu-id="247f5-227">Parameter</span></span>|<span data-ttu-id="247f5-228">Description</span><span class="sxs-lookup"><span data-stu-id="247f5-228">Description</span></span>|<span data-ttu-id="247f5-229">Example</span><span class="sxs-lookup"><span data-stu-id="247f5-229">Example</span></span>|
|---------|---------|---------|
|<span data-ttu-id="247f5-230">CustomAdfsName</span><span class="sxs-lookup"><span data-stu-id="247f5-230">CustomAdfsName</span></span>|<span data-ttu-id="247f5-231">Name of the claims provider.</span><span class="sxs-lookup"><span data-stu-id="247f5-231">Name of the claims provider.</span></span> <span data-ttu-id="247f5-232">It appears that way on the AD FS landing page.</span><span class="sxs-lookup"><span data-stu-id="247f5-232">It appears that way on the AD FS landing page.</span></span>|<span data-ttu-id="247f5-233">Contoso</span><span class="sxs-lookup"><span data-stu-id="247f5-233">Contoso</span></span>|
|<span data-ttu-id="247f5-234">CustomADFSFederationMetadataFileContent</span><span class="sxs-lookup"><span data-stu-id="247f5-234">CustomADFSFederationMetadataFileContent</span></span>|<span data-ttu-id="247f5-235">Metadata content</span><span class="sxs-lookup"><span data-stu-id="247f5-235">Metadata content</span></span>|<span data-ttu-id="247f5-236">$using:federationMetadataFileContent</span><span class="sxs-lookup"><span data-stu-id="247f5-236">$using:federationMetadataFileContent</span></span>|



### <a name="create-federation-metadata-file"></a><span data-ttu-id="247f5-237">Create federation metadata file</span><span class="sxs-lookup"><span data-stu-id="247f5-237">Create federation metadata file</span></span>

<span data-ttu-id="247f5-238">For the following procedure, you must use a computer that has network connectivity to the existing AD FS deployment, which becomes the account STS.</span><span class="sxs-lookup"><span data-stu-id="247f5-238">For the following procedure, you must use a computer that has network connectivity to the existing AD FS deployment, which becomes the account STS.</span></span> <span data-ttu-id="247f5-239">Also, the necessary certificates must be installed.</span><span class="sxs-lookup"><span data-stu-id="247f5-239">Also, the necessary certificates must be installed.</span></span>

1. <span data-ttu-id="247f5-240">Open an elevated Windows PowerShell session, and run the following command, using the parameters appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="247f5-240">Open an elevated Windows PowerShell session, and run the following command, using the parameters appropriate for your environment:</span></span>

   ```PowerShell  
   [XML]$Metadata = Invoke-WebRequest -URI https://win-SQOOJN70SGL.contoso.com/federationmetadata/2007-06/federationmetadata.xml -UseBasicParsing

   $Metadata.outerxml|out-file c:\metadata.xml
   ```

2. <span data-ttu-id="247f5-241">Copy the metadata file to a computer that can communicate with the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="247f5-241">Copy the metadata file to a computer that can communicate with the privileged endpoint.</span></span>

### <a name="trigger-automation-to-configure-claims-provider-trust-in-azure-stack"></a><span data-ttu-id="247f5-242">Trigger automation to configure claims provider trust in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="247f5-242">Trigger automation to configure claims provider trust in Azure Stack</span></span>

<span data-ttu-id="247f5-243">For this procedure, use a computer that can communicate with the privileged endpoint in Azure Stack and has access to the metadata file you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="247f5-243">For this procedure, use a computer that can communicate with the privileged endpoint in Azure Stack and has access to the metadata file you created in a previous step.</span></span>

1. <span data-ttu-id="247f5-244">Open an elevated Windows PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="247f5-244">Open an elevated Windows PowerShell session.</span></span>

   ```PowerShell  
   $federationMetadataFileContent = get-content c:\metadata.cml
   $creds=Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   Register-CustomAdfs -CustomAdfsName Contoso -CustomADFSFederationMetadataFileContent $using:federationMetadataFileContent
   ```

2. <span data-ttu-id="247f5-245">Run the following command to update the owner of the default provider subscription, using the parameters appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="247f5-245">Run the following command to update the owner of the default provider subscription, using the parameters appropriate for your environment:</span></span>

   ```PowerShell  
   Set-ServiceAdminOwner -ServiceAdminOwnerUpn "administrator@contoso.com"
   ```

## <a name="configure-relying-party-on-existing-ad-fs-deployment-account-sts"></a><span data-ttu-id="247f5-246">Configure relying party on existing AD FS deployment (account STS)</span><span class="sxs-lookup"><span data-stu-id="247f5-246">Configure relying party on existing AD FS deployment (account STS)</span></span>

<span data-ttu-id="247f5-247">Microsoft provides a script that configures the relying party trust, including the claim transformation rules.</span><span class="sxs-lookup"><span data-stu-id="247f5-247">Microsoft provides a script that configures the relying party trust, including the claim transformation rules.</span></span> <span data-ttu-id="247f5-248">Using the script is optional as you can run the commands manually.</span><span class="sxs-lookup"><span data-stu-id="247f5-248">Using the script is optional as you can run the commands manually.</span></span>

<span data-ttu-id="247f5-249">You can download the helper script from [Azure Stack Tools](https://github.com/Azure/AzureStack-Tools/tree/vnext/DatacenterIntegration/Identity) on Github.</span><span class="sxs-lookup"><span data-stu-id="247f5-249">You can download the helper script from [Azure Stack Tools](https://github.com/Azure/AzureStack-Tools/tree/vnext/DatacenterIntegration/Identity) on Github.</span></span>

<span data-ttu-id="247f5-250">If you decide to manually run the commands, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="247f5-250">If you decide to manually run the commands, follow these steps:</span></span>

1. <span data-ttu-id="247f5-251">Copy the following content into a .txt file (for example, saved as c:\ClaimRules.txt) on your datacenter's AD FS instance or farm member:</span><span class="sxs-lookup"><span data-stu-id="247f5-251">Copy the following content into a .txt file (for example, saved as c:\ClaimRules.txt) on your datacenter's AD FS instance or farm member:</span></span>

   ```text
   @RuleTemplate = "LdapClaims"
   @RuleName = "Name claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
   => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"), query = ";userPrincipalName;{0}", param = c.Value);

   @RuleTemplate = "LdapClaims"
   @RuleName = "UPN claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
   => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

   @RuleTemplate = "LdapClaims"
   @RuleName = "ObjectID claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"]
   => issue(Type = "http://schemas.microsoft.com/identity/claims/objectidentifier", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, Value = c.Value, ValueType = c.ValueType);

   @RuleName = "Family Name and Given claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
   => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname", "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"), query = ";sn,givenName;{0}", param = c.Value);

   @RuleTemplate = "PassThroughClaims"
   @RuleName = "Pass through all Group SID claims"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"]
   => issue(claim = c);

   @RuleTemplate = "PassThroughClaims"
   @RuleName = "Pass through all windows account name claims"
   c:[Type == http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname]
   => issue(claim = c);
   ```

2. <span data-ttu-id="247f5-252">To enable Windows Forms-based authentication, open a Windows PowerShell session as an elevated user, and run the following command:</span><span class="sxs-lookup"><span data-stu-id="247f5-252">To enable Windows Forms-based authentication, open a Windows PowerShell session as an elevated user, and run the following command:</span></span>

   ```PowerShell  
   Set-AdfsProperties -WIASupportedUserAgents @("MSAuthHost/1.0/In-Domain","MSIPC","Windows Rights Management Client","Kloud")
   ```

3. <span data-ttu-id="247f5-253">To add the relying party trust, run the following Windows PowerShell command on your AD FS instance or a farm member.</span><span class="sxs-lookup"><span data-stu-id="247f5-253">To add the relying party trust, run the following Windows PowerShell command on your AD FS instance or a farm member.</span></span> <span data-ttu-id="247f5-254">Make sure to update the AD FS endpoint, and point to the file created in Step 1.</span><span class="sxs-lookup"><span data-stu-id="247f5-254">Make sure to update the AD FS endpoint, and point to the file created in Step 1.</span></span>

   <span data-ttu-id="247f5-255">**For AD FS 2016**</span><span class="sxs-lookup"><span data-stu-id="247f5-255">**For AD FS 2016**</span></span>

   ```PowerShell  
   Add-ADFSRelyingPartyTrust -Name AzureStack -MetadataUrl "https://YourAzureStackADFSEndpoint/FederationMetadata/2007-06/FederationMetadata.xml" -IssuanceTransformRulesFile "C:\ClaimIssuanceRules.txt" -AutoUpdateEnabled:$true -MonitoringEnabled:$true -enabled:$true -AccessControlPolicyName "Permit everyone"
   ```

   <span data-ttu-id="247f5-256">**For AD FS 2012/2012 R2**</span><span class="sxs-lookup"><span data-stu-id="247f5-256">**For AD FS 2012/2012 R2**</span></span>

   ```PowerShell  
   Add-ADFSRelyingPartyTrust -Name AzureStack -MetadataUrl "https://YourAzureStackADFSEndpoint/FederationMetadata/2007-06/FederationMetadata.xml" -IssuanceTransformRulesFile "C:\ClaimIssuanceRules.txt" -AutoUpdateEnabled:$true -MonitoringEnabled:$true -enabled:$true
   ```

   > [!IMPORTANT]
   > <span data-ttu-id="247f5-257">You must use the AD FS MMC snap-in to configure the Issuance Authorization Rules when using Windows Server 2012 or 2012 R2 AD FS.</span><span class="sxs-lookup"><span data-stu-id="247f5-257">You must use the AD FS MMC snap-in to configure the Issuance Authorization Rules when using Windows Server 2012 or 2012 R2 AD FS.</span></span>

4. <span data-ttu-id="247f5-258">When you use Internet Explorer or the Edge browser to access Azure Stack, you must ignore token bindings.</span><span class="sxs-lookup"><span data-stu-id="247f5-258">When you use Internet Explorer or the Edge browser to access Azure Stack, you must ignore token bindings.</span></span> <span data-ttu-id="247f5-259">Otherwise, the sign-in attempts fail.</span><span class="sxs-lookup"><span data-stu-id="247f5-259">Otherwise, the sign-in attempts fail.</span></span> <span data-ttu-id="247f5-260">On your AD FS instance or a farm member, run the following command:</span><span class="sxs-lookup"><span data-stu-id="247f5-260">On your AD FS instance or a farm member, run the following command:</span></span>

   > [!note]  
   > <span data-ttu-id="247f5-261">This step is not applicable when using Windows Server 2012 or 2012 R2 AD FS.</span><span class="sxs-lookup"><span data-stu-id="247f5-261">This step is not applicable when using Windows Server 2012 or 2012 R2 AD FS.</span></span> <span data-ttu-id="247f5-262">It is safe to skip this command and continue with the integration.</span><span class="sxs-lookup"><span data-stu-id="247f5-262">It is safe to skip this command and continue with the integration.</span></span>

   ```PowerShell  
   Set-AdfsProperties -IgnoreTokenBinding $true
   ```

5. <span data-ttu-id="247f5-263">The Azure Stack portals and tooling (Visual Studio) require refresh tokens.</span><span class="sxs-lookup"><span data-stu-id="247f5-263">The Azure Stack portals and tooling (Visual Studio) require refresh tokens.</span></span> <span data-ttu-id="247f5-264">These must be configured by relying on party trust.</span><span class="sxs-lookup"><span data-stu-id="247f5-264">These must be configured by relying on party trust.</span></span> <span data-ttu-id="247f5-265">Open an elevated Windows PowerShell session, and run the following command:</span><span class="sxs-lookup"><span data-stu-id="247f5-265">Open an elevated Windows PowerShell session, and run the following command:</span></span>

   ```PowerShell  
   Set-ADFSRelyingPartyTrust -TargetName AzureStack -TokenLifeTime 1440
   ```

## <a name="spn-creation"></a><span data-ttu-id="247f5-266">SPN creation</span><span class="sxs-lookup"><span data-stu-id="247f5-266">SPN creation</span></span>

<span data-ttu-id="247f5-267">There are many scenarios that require the use of a service principal name (SPN) for authentication.</span><span class="sxs-lookup"><span data-stu-id="247f5-267">There are many scenarios that require the use of a service principal name (SPN) for authentication.</span></span> <span data-ttu-id="247f5-268">The following are some examples:</span><span class="sxs-lookup"><span data-stu-id="247f5-268">The following are some examples:</span></span>

- <span data-ttu-id="247f5-269">CLI usage with AD FS deployment of Azure Stack</span><span class="sxs-lookup"><span data-stu-id="247f5-269">CLI usage with AD FS deployment of Azure Stack</span></span>
- <span data-ttu-id="247f5-270">System Center Management Pack for Azure Stack when deployed with AD FS</span><span class="sxs-lookup"><span data-stu-id="247f5-270">System Center Management Pack for Azure Stack when deployed with AD FS</span></span>
- <span data-ttu-id="247f5-271">Resource providers in Azure Stack when deployed with AD FS</span><span class="sxs-lookup"><span data-stu-id="247f5-271">Resource providers in Azure Stack when deployed with AD FS</span></span>
- <span data-ttu-id="247f5-272">Various applications</span><span class="sxs-lookup"><span data-stu-id="247f5-272">Various applications</span></span>
- <span data-ttu-id="247f5-273">You require a non-interactive logon</span><span class="sxs-lookup"><span data-stu-id="247f5-273">You require a non-interactive logon</span></span>

> [!Important]  
> <span data-ttu-id="247f5-274">AD FS only supports interactive logon sessions.</span><span class="sxs-lookup"><span data-stu-id="247f5-274">AD FS only supports interactive logon sessions.</span></span> <span data-ttu-id="247f5-275">If you require a non-interactive logon for an automated scenario, you must use a SPN.</span><span class="sxs-lookup"><span data-stu-id="247f5-275">If you require a non-interactive logon for an automated scenario, you must use a SPN.</span></span>

<span data-ttu-id="247f5-276">For more information about creating an SPN, see [Create service principal for AD FS](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="247f5-276">For more information about creating an SPN, see [Create service principal for AD FS](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#create-service-principal-for-ad-fs).</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="247f5-277">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="247f5-277">Troubleshooting</span></span>

### <a name="configuration-rollback"></a><span data-ttu-id="247f5-278">Configuration Rollback</span><span class="sxs-lookup"><span data-stu-id="247f5-278">Configuration Rollback</span></span>

<span data-ttu-id="247f5-279">If an error occurs that leaves the environment in a state where you can no longer authenticate, a rollback option is available.</span><span class="sxs-lookup"><span data-stu-id="247f5-279">If an error occurs that leaves the environment in a state where you can no longer authenticate, a rollback option is available.</span></span>

1. <span data-ttu-id="247f5-280">Open an elevated Windows PowerShell session and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="247f5-280">Open an elevated Windows PowerShell session and run the following commands:</span></span>

   ```PowerShell  
   $creds = Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. <span data-ttu-id="247f5-281">Then run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="247f5-281">Then run the following cmdlet:</span></span>

   ```PowerShell  
   Reset-DatacenterIntegationConfiguration
   ```

   <span data-ttu-id="247f5-282">After running the rollback action, all configuration changes are rolled back.</span><span class="sxs-lookup"><span data-stu-id="247f5-282">After running the rollback action, all configuration changes are rolled back.</span></span> <span data-ttu-id="247f5-283">Only authentication with the built-in **CloudAdmin** user is possible.</span><span class="sxs-lookup"><span data-stu-id="247f5-283">Only authentication with the built-in **CloudAdmin** user is possible.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="247f5-284">You must configure the original owner of the default provider subscription</span><span class="sxs-lookup"><span data-stu-id="247f5-284">You must configure the original owner of the default provider subscription</span></span>

   ```PowerShell  
   Set-ServiceAdminOwner -ServiceAdminOwnerUpn "azurestackadmin@[Internal Domain]"
   ```

### <a name="collecting-additional-logs"></a><span data-ttu-id="247f5-285">Collecting additional logs</span><span class="sxs-lookup"><span data-stu-id="247f5-285">Collecting additional logs</span></span>

<span data-ttu-id="247f5-286">If any of the cmdlets fail, you can collect additional logs by using the `Get-Azurestacklogs` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="247f5-286">If any of the cmdlets fail, you can collect additional logs by using the `Get-Azurestacklogs` cmdlet.</span></span>

1. <span data-ttu-id="247f5-287">Open an elevated Windows PowerShell session, and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="247f5-287">Open an elevated Windows PowerShell session, and run the following commands:</span></span>

   ```PowerShell  
   $creds = Get-Credential
   Enter-pssession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. <span data-ttu-id="247f5-288">Then, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="247f5-288">Then, run the following cmdlet:</span></span>

   ```PowerShell  
   Get-AzureStackLog -OutputPath \\myworstation\AzureStackLogs -FilterByRole ECE
   ```


## <a name="next-steps"></a><span data-ttu-id="247f5-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="247f5-289">Next steps</span></span>

[<span data-ttu-id="247f5-290">Integrate external monitoring solutions</span><span class="sxs-lookup"><span data-stu-id="247f5-290">Integrate external monitoring solutions</span></span>](azure-stack-integrate-monitor.md)
