---
title: Test parameters for validation as a service Azure Stack | Microsoft Docs
description: Reference topic about the configuration file and test pass parameters for validation as a service Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: 9f042779e3463f0d75dc6327b3553156edbf162a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867265"
---
# <a name="test-parameters-for-validation-as-a-service-azure-stack"></a><span data-ttu-id="99b4c-103">Test parameters for validation as a service Azure Stack</span><span class="sxs-lookup"><span data-stu-id="99b4c-103">Test parameters for validation as a service Azure Stack</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="99b4c-104">Before executing any Test Suite from validations as a service (VaaS), select a Solution and create a test pass.</span><span class="sxs-lookup"><span data-stu-id="99b4c-104">Before executing any Test Suite from validations as a service (VaaS), select a Solution and create a test pass.</span></span>

- <span data-ttu-id="99b4c-105">Sign in with your registered VaaS tenant credentials.</span><span class="sxs-lookup"><span data-stu-id="99b4c-105">Sign in with your registered VaaS tenant credentials.</span></span>
- <span data-ttu-id="99b4c-106">Create a new Solution (by selecting **Add Solution**) or select any existing.</span><span class="sxs-lookup"><span data-stu-id="99b4c-106">Create a new Solution (by selecting **Add Solution**) or select any existing.</span></span>
- <span data-ttu-id="99b4c-107">Select the **Start** button from the **Test Passes** workflow tile.</span><span class="sxs-lookup"><span data-stu-id="99b4c-107">Select the **Start** button from the **Test Passes** workflow tile.</span></span>

> [!Note]  
> <span data-ttu-id="99b4c-108">Create a new solution entry for each unique machine set/hardware configuration that you're validating, and a new test pass for every build deployment on that machine set.</span><span class="sxs-lookup"><span data-stu-id="99b4c-108">Create a new solution entry for each unique machine set/hardware configuration that you're validating, and a new test pass for every build deployment on that machine set.</span></span>

<span data-ttu-id="99b4c-109">You will need to enter the parameters required to run the tests in the **Test Pass Information** page.</span><span class="sxs-lookup"><span data-stu-id="99b4c-109">You will need to enter the parameters required to run the tests in the **Test Pass Information** page.</span></span> <span data-ttu-id="99b4c-110">Provide these parameters when starting a new test pass or validation run.</span><span class="sxs-lookup"><span data-stu-id="99b4c-110">Provide these parameters when starting a new test pass or validation run.</span></span> <span data-ttu-id="99b4c-111">Most of the parameters have the same values that you provided when you deployed Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="99b4c-111">Most of the parameters have the same values that you provided when you deployed Azure Stack.</span></span>

<span data-ttu-id="99b4c-112">You can enter the values manually listed in the [Test parameters table](#test-parameters), or upload the deployment configuration file, which contains the full Azure Stack stamp information.</span><span class="sxs-lookup"><span data-stu-id="99b4c-112">You can enter the values manually listed in the [Test parameters table](#test-parameters), or upload the deployment configuration file, which contains the full Azure Stack stamp information.</span></span> <span data-ttu-id="99b4c-113">Once uploaded, the portal loads the values from the file.</span><span class="sxs-lookup"><span data-stu-id="99b4c-113">Once uploaded, the portal loads the values from the file.</span></span>

> [!Note]  
> <span data-ttu-id="99b4c-114">You can searching for and typing the test parameter values by finding and loading the configuration file into the portal.</span><span class="sxs-lookup"><span data-stu-id="99b4c-114">You can searching for and typing the test parameter values by finding and loading the configuration file into the portal.</span></span>

## <a name="export-the-test-parameters-using-powershell"></a><span data-ttu-id="99b4c-115">Export the test parameters using PowerShell</span><span class="sxs-lookup"><span data-stu-id="99b4c-115">Export the test parameters using PowerShell</span></span>

1. <span data-ttu-id="99b4c-116">Sign in to DVM machine or any machine that has access to Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="99b4c-116">Sign in to DVM machine or any machine that has access to Azure Stack environment.</span></span>
2. <span data-ttu-id="99b4c-117">Open an elevated PowerShell window, and run:</span><span class="sxs-lookup"><span data-stu-id="99b4c-117">Open an elevated PowerShell window, and run:</span></span>

    ````PowerShell  
        $params = Invoke-RestMethod -Method Get -Uri 'https://ASAppGateway:4443/ServiceTypeId/4dde37cc-6ee0-4d75-9444-7061e156507f/CloudDefinition/GetStampInformation'
        ConvertTo-Json $params > stampinfoproperties.json
    ````

3. <span data-ttu-id="99b4c-118">Upload **stampinfoproperties.json** to the VaaS portal.</span><span class="sxs-lookup"><span data-stu-id="99b4c-118">Upload **stampinfoproperties.json** to the VaaS portal.</span></span>

## <a name="find-the-test-parameters-in-the-configuration-file"></a><span data-ttu-id="99b4c-119">Find the test parameters in the configuration file</span><span class="sxs-lookup"><span data-stu-id="99b4c-119">Find the test parameters in the configuration file</span></span>

<span data-ttu-id="99b4c-120">You can also find the test parameter values by opening the ECE **configuration file**.</span><span class="sxs-lookup"><span data-stu-id="99b4c-120">You can also find the test parameter values by opening the ECE **configuration file**.</span></span> <span data-ttu-id="99b4c-121">You can find the file at the following path on the DVM machine:</span><span class="sxs-lookup"><span data-stu-id="99b4c-121">You can find the file at the following path on the DVM machine:</span></span>  
`C:\EceStore\403314e1-d945-9558-fad2-42ba21985248\80e0921f-56b5-17d3-29f5-cd41bf862787`

## <a name="test-parameters"></a><span data-ttu-id="99b4c-122">Test parameters</span><span class="sxs-lookup"><span data-stu-id="99b4c-122">Test parameters</span></span> 

| <span data-ttu-id="99b4c-123">Parameter</span><span class="sxs-lookup"><span data-stu-id="99b4c-123">Parameter</span></span>    | <span data-ttu-id="99b4c-124">Description</span><span class="sxs-lookup"><span data-stu-id="99b4c-124">Description</span></span> |
|-------------|-----------------|
| <span data-ttu-id="99b4c-125">Azure Stack Build</span><span class="sxs-lookup"><span data-stu-id="99b4c-125">Azure Stack Build</span></span>                      | <span data-ttu-id="99b4c-126">Azure Stack Build or version number that was deployed for example, 1.0.170330.0</span><span class="sxs-lookup"><span data-stu-id="99b4c-126">Azure Stack Build or version number that was deployed for example, 1.0.170330.0</span></span> | 
| <span data-ttu-id="99b4c-127">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="99b4c-127">Tenant ID</span></span>                              | <span data-ttu-id="99b4c-128">Azure Active Directory Tenant specified during Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="99b4c-128">Azure Active Directory Tenant specified during Azure Stack deployment.</span></span> <span data-ttu-id="99b4c-129">Search for **AADTenant** in the configuration file and select the **GUID** value in the `Id` tag.</span><span class="sxs-lookup"><span data-stu-id="99b4c-129">Search for **AADTenant** in the configuration file and select the **GUID** value in the `Id` tag.</span></span> | 
| <span data-ttu-id="99b4c-130">Region</span><span class="sxs-lookup"><span data-stu-id="99b4c-130">Region</span></span>                                 | <span data-ttu-id="99b4c-131">Azure Stack deployment region.</span><span class="sxs-lookup"><span data-stu-id="99b4c-131">Azure Stack deployment region.</span></span> <span data-ttu-id="99b4c-132">Search for **Region** in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="99b4c-132">Search for **Region** in the configuration file.</span></span> | 
| <span data-ttu-id="99b4c-133">Tenant Resource Manager</span><span class="sxs-lookup"><span data-stu-id="99b4c-133">Tenant Resource Manager</span></span>                | <span data-ttu-id="99b4c-134">Tenant Azure Resource Manager endpoint, for example, `https://management.<ExternalFqdn>`</span><span class="sxs-lookup"><span data-stu-id="99b4c-134">Tenant Azure Resource Manager endpoint, for example, `https://management.<ExternalFqdn>`</span></span> | 
| <span data-ttu-id="99b4c-135">Admin Resource Manager</span><span class="sxs-lookup"><span data-stu-id="99b4c-135">Admin Resource Manager</span></span>                 | <span data-ttu-id="99b4c-136">Admin Azure Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="99b4c-136">Admin Azure Resource Manager endpoint.</span></span> <span data-ttu-id="99b4c-137">for example, `https://adminmanagement.<ExternalFqdn>`</span><span class="sxs-lookup"><span data-stu-id="99b4c-137">for example, `https://adminmanagement.<ExternalFqdn>`</span></span> | 
| <span data-ttu-id="99b4c-138">External FQDN</span><span class="sxs-lookup"><span data-stu-id="99b4c-138">External FQDN</span></span>                          | <span data-ttu-id="99b4c-139">External FQDN of the Environment.</span><span class="sxs-lookup"><span data-stu-id="99b4c-139">External FQDN of the Environment.</span></span> <span data-ttu-id="99b4c-140">Search for **ExternalFqdn** in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="99b4c-140">Search for **ExternalFqdn** in the configuration file.</span></span> | 
| <span data-ttu-id="99b4c-141">Tenant User</span><span class="sxs-lookup"><span data-stu-id="99b4c-141">Tenant User</span></span>                            | <span data-ttu-id="99b4c-142">Azure Active Directory Tenant Admin that was either provisioned already or needs to be provisioned by the Service Admin in the Azure AD Directory.</span><span class="sxs-lookup"><span data-stu-id="99b4c-142">Azure Active Directory Tenant Admin that was either provisioned already or needs to be provisioned by the Service Admin in the Azure AD Directory.</span></span> <span data-ttu-id="99b4c-143">For details on provisioning tenant account see [Add a new Azure Stack tenant account in Azure Active Directory](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-new-user-aad).</span><span class="sxs-lookup"><span data-stu-id="99b4c-143">For details on provisioning tenant account see [Add a new Azure Stack tenant account in Azure Active Directory](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-new-user-aad).</span></span> <span data-ttu-id="99b4c-144">This value is used by the test to perform tenant level operations such as deploying templates to provision resources (VM’s, storage accounts etc.) and execute workloads.</span><span class="sxs-lookup"><span data-stu-id="99b4c-144">This value is used by the test to perform tenant level operations such as deploying templates to provision resources (VM’s, storage accounts etc.) and execute workloads.</span></span> | 
| <span data-ttu-id="99b4c-145">Service Administrator User</span><span class="sxs-lookup"><span data-stu-id="99b4c-145">Service Administrator User</span></span>             | <span data-ttu-id="99b4c-146">Azure Active Directory Admin of the Azure AD Directory Tenant specified during Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="99b4c-146">Azure Active Directory Admin of the Azure AD Directory Tenant specified during Azure Stack deployment.</span></span> <span data-ttu-id="99b4c-147">Search for **AADTenant** in the configuration file and select the value in the `UniqueName` tag in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="99b4c-147">Search for **AADTenant** in the configuration file and select the value in the `UniqueName` tag in the configuration file.</span></span> | 

## <a name="checks-before-starting-the-tests"></a><span data-ttu-id="99b4c-148">Checks before starting the tests</span><span class="sxs-lookup"><span data-stu-id="99b4c-148">Checks before starting the tests</span></span>

<span data-ttu-id="99b4c-149">The tests perform remote operations.</span><span class="sxs-lookup"><span data-stu-id="99b4c-149">The tests perform remote operations.</span></span> <span data-ttu-id="99b4c-150">The machine that runs the tests must have access to the Azure Stack endpoints.</span><span class="sxs-lookup"><span data-stu-id="99b4c-150">The machine that runs the tests must have access to the Azure Stack endpoints.</span></span> <span data-ttu-id="99b4c-151">Otherwise the test will not work.</span><span class="sxs-lookup"><span data-stu-id="99b4c-151">Otherwise the test will not work.</span></span> <span data-ttu-id="99b4c-152">If you are using the VaaS on premises agent, use the machine where the agent will run.</span><span class="sxs-lookup"><span data-stu-id="99b4c-152">If you are using the VaaS on premises agent, use the machine where the agent will run.</span></span> <span data-ttu-id="99b4c-153">You can verify that your machine has access to the Azure Stack points by running the following checks.</span><span class="sxs-lookup"><span data-stu-id="99b4c-153">You can verify that your machine has access to the Azure Stack points by running the following checks.</span></span>

1. <span data-ttu-id="99b4c-154">Check that the Base URI can be reached.</span><span class="sxs-lookup"><span data-stu-id="99b4c-154">Check that the Base URI can be reached.</span></span> <span data-ttu-id="99b4c-155">Open a CMD prompt or bash shell, and run the following command:</span><span class="sxs-lookup"><span data-stu-id="99b4c-155">Open a CMD prompt or bash shell, and run the following command:</span></span>

    ```bash  
    nslookup adminmanagement.<EXTERNALFQDN>
    ```

2. <span data-ttu-id="99b4c-156">Open a web browser and navigate to `https://adminportal.<EXTERNALFQDN>` in order to check that the MAS Portal can be reached.</span><span class="sxs-lookup"><span data-stu-id="99b4c-156">Open a web browser and navigate to `https://adminportal.<EXTERNALFQDN>` in order to check that the MAS Portal can be reached.</span></span>

3. <span data-ttu-id="99b4c-157">Sign in using the Azure AD service administrator name and password values provided when creating the test pass.</span><span class="sxs-lookup"><span data-stu-id="99b4c-157">Sign in using the Azure AD service administrator name and password values provided when creating the test pass.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99b4c-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="99b4c-158">Next steps</span></span>

- <span data-ttu-id="99b4c-159">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="99b4c-159">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
