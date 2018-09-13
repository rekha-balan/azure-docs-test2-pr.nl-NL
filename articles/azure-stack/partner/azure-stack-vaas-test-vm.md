---
title: Deploy the local agent and test image virtual machines in Azure Stack validation as a service | Microsoft Docs
description: Deploy the local agent and test image virtual machines for Azure Stack validation as a service.
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
ms.openlocfilehash: 78136ab00dcba2f8a99df36ba99d384b49995882
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867453"
---
# <a name="deploy-the-local-agent-and-test-virtual-machines"></a><span data-ttu-id="f7ac4-103">Deploy the local agent and test virtual machines</span><span class="sxs-lookup"><span data-stu-id="f7ac4-103">Deploy the local agent and test virtual machines</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="f7ac4-104">Learn how to use the validation as a service (VaaS) local agent to check your hardware.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-104">Learn how to use the validation as a service (VaaS) local agent to check your hardware.</span></span> <span data-ttu-id="f7ac4-105">The local agent must be deployed on the Azure Stack solution being validated prior to running validation tests.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-105">The local agent must be deployed on the Azure Stack solution being validated prior to running validation tests.</span></span>

> [!Note]  
> <span data-ttu-id="f7ac4-106">You must make sure that the machine, where the local agent is running, doesn't lose access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-106">You must make sure that the machine, where the local agent is running, doesn't lose access to the Internet.</span></span> <span data-ttu-id="f7ac4-107">The machine must only be accessible to users who are authorized to use Azure Stack VaaS.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-107">The machine must only be accessible to users who are authorized to use Azure Stack VaaS.</span></span>

<span data-ttu-id="f7ac4-108">To test your virtual machines:</span><span class="sxs-lookup"><span data-stu-id="f7ac4-108">To test your virtual machines:</span></span>

1. <span data-ttu-id="f7ac4-109">Install the local agent</span><span class="sxs-lookup"><span data-stu-id="f7ac4-109">Install the local agent</span></span>
2. <span data-ttu-id="f7ac4-110">Inject faults into your system</span><span class="sxs-lookup"><span data-stu-id="f7ac4-110">Inject faults into your system</span></span>
3. <span data-ttu-id="f7ac4-111">Run the local agent</span><span class="sxs-lookup"><span data-stu-id="f7ac4-111">Run the local agent</span></span>

## <a name="download-and-start-the-local-agent"></a><span data-ttu-id="f7ac4-112">Download and start the local agent</span><span class="sxs-lookup"><span data-stu-id="f7ac4-112">Download and start the local agent</span></span>

<span data-ttu-id="f7ac4-113">Download the agent to a machine that meets the prerequisites in your datacenter that is not part of the Azure Stack system, but one that has access to all the Azure Stack endpoints.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-113">Download the agent to a machine that meets the prerequisites in your datacenter that is not part of the Azure Stack system, but one that has access to all the Azure Stack endpoints.</span></span>

### <a name="machine-prerequisites"></a><span data-ttu-id="f7ac4-114">Machine prerequisites</span><span class="sxs-lookup"><span data-stu-id="f7ac4-114">Machine prerequisites</span></span>

<span data-ttu-id="f7ac4-115">Check that your machine meets the following criteria:</span><span class="sxs-lookup"><span data-stu-id="f7ac4-115">Check that your machine meets the following criteria:</span></span>

- <span data-ttu-id="f7ac4-116">Access to all Azure Stack endpoints</span><span class="sxs-lookup"><span data-stu-id="f7ac4-116">Access to all Azure Stack endpoints</span></span>
- <span data-ttu-id="f7ac4-117">.NET 4.6 and PowerShell 5.0 installed</span><span class="sxs-lookup"><span data-stu-id="f7ac4-117">.NET 4.6 and PowerShell 5.0 installed</span></span>
- <span data-ttu-id="f7ac4-118">At least 8-GB RAM</span><span class="sxs-lookup"><span data-stu-id="f7ac4-118">At least 8-GB RAM</span></span>
- <span data-ttu-id="f7ac4-119">Minimum 8 core processors</span><span class="sxs-lookup"><span data-stu-id="f7ac4-119">Minimum 8 core processors</span></span>
- <span data-ttu-id="f7ac4-120">Minimum 200-GB disk space</span><span class="sxs-lookup"><span data-stu-id="f7ac4-120">Minimum 200-GB disk space</span></span>
- <span data-ttu-id="f7ac4-121">Stable network connectivity to the internet</span><span class="sxs-lookup"><span data-stu-id="f7ac4-121">Stable network connectivity to the internet</span></span>

<span data-ttu-id="f7ac4-122">Azure Stack is the system under test.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-122">Azure Stack is the system under test.</span></span> <span data-ttu-id="f7ac4-123">The machine should not be part of Azure Stack or hosted in the Azure Stack cloud.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-123">The machine should not be part of Azure Stack or hosted in the Azure Stack cloud.</span></span>

### <a name="download-and-install-the-agent"></a><span data-ttu-id="f7ac4-124">Download and install the agent</span><span class="sxs-lookup"><span data-stu-id="f7ac4-124">Download and install the agent</span></span>

1. <span data-ttu-id="f7ac4-125">Open Windows PowerShell in an elevated prompt on the machine you will use to run the tests.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-125">Open Windows PowerShell in an elevated prompt on the machine you will use to run the tests.</span></span>
2. <span data-ttu-id="f7ac4-126">Run the following command to download the local agent:</span><span class="sxs-lookup"><span data-stu-id="f7ac4-126">Run the following command to download the local agent:</span></span>

    ```PowerShell  
        Invoke-WebRequest -Uri "https://storage.azurestackvalidation.com/packages/Microsoft.VaaSOnPrem.TaskEngineHost.3.2.0.nupkg" -outfile "OnPremAgent.zip"
        Expand-Archive -Path ".\OnPremAgent.zip" -DestinationPath VaaSOnPremAgent.3.2.0 -Force
        Set-Location VaaSOnPremAgent.3.2.0\lib\net46
    ````

3. <span data-ttu-id="f7ac4-127">Run the following command to install the local agent dependencies:</span><span class="sxs-lookup"><span data-stu-id="f7ac4-127">Run the following command to install the local agent dependencies:</span></span>

    ```PowerShell  
        $ServiceAdminCreds = New-Object System.Management.Automation.PSCredential "<aadServiceAdminUser>", (ConvertTo-SecureString "<aadServiceAdminPassword>" -AsPlainText -Force)
        Import-Module .\VaaSPreReqs.psm1 -Force
        Install-VaaSPrerequisites -AadTenantId <AadTenantId> `
        -ServiceAdminCreds <ServiceAdminCreds> `
        -ArmEndpoint https://adminmanagement.<ExternalFqdn> `
        -Region <Region>
    ````

    <span data-ttu-id="f7ac4-128">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="f7ac4-128">**Parameters**</span></span>

    | <span data-ttu-id="f7ac4-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="f7ac4-129">Parameter</span></span> | <span data-ttu-id="f7ac4-130">Description</span><span class="sxs-lookup"><span data-stu-id="f7ac4-130">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="f7ac4-131">aadServiceAdminUser</span><span class="sxs-lookup"><span data-stu-id="f7ac4-131">aadServiceAdminUser</span></span> | <span data-ttu-id="f7ac4-132">The global admin user for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-132">The global admin user for your Azure AD tenant.</span></span> <span data-ttu-id="f7ac4-133">For example it may be, vaasadmin@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-133">For example it may be, vaasadmin@contoso.onmicrosoft.com.</span></span> |
    | <span data-ttu-id="f7ac4-134">aadServiceAdminPassword</span><span class="sxs-lookup"><span data-stu-id="f7ac4-134">aadServiceAdminPassword</span></span> | <span data-ttu-id="f7ac4-135">The password for the global admin user.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-135">The password for the global admin user.</span></span> |
    | <span data-ttu-id="f7ac4-136">AadTenantId</span><span class="sxs-lookup"><span data-stu-id="f7ac4-136">AadTenantId</span></span> | <span data-ttu-id="f7ac4-137">Azure AD tenant ID for the Azure account registered with Validation as a Service.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-137">Azure AD tenant ID for the Azure account registered with Validation as a Service.</span></span> |
    | <span data-ttu-id="f7ac4-138">ExternalFqdn</span><span class="sxs-lookup"><span data-stu-id="f7ac4-138">ExternalFqdn</span></span> | <span data-ttu-id="f7ac4-139">You can get the fully qualified domain name from the configuration file.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-139">You can get the fully qualified domain name from the configuration file.</span></span> <span data-ttu-id="f7ac4-140">For instruction, see [Test parameters for validation as a service Azure Stack](azure-stack-vaas-parameters-test.md).</span><span class="sxs-lookup"><span data-stu-id="f7ac4-140">For instruction, see [Test parameters for validation as a service Azure Stack](azure-stack-vaas-parameters-test.md).</span></span> |
    | <span data-ttu-id="f7ac4-141">Region</span><span class="sxs-lookup"><span data-stu-id="f7ac4-141">Region</span></span> | <span data-ttu-id="f7ac4-142">The region of your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-142">The region of your Azure AD tenant.</span></span> |

<span data-ttu-id="f7ac4-143">The command downloads a public image repository (PIR) image (OS VHD) and copy from an Azure blob storage to your Azure Stack storage.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-143">The command downloads a public image repository (PIR) image (OS VHD) and copy from an Azure blob storage to your Azure Stack storage.</span></span> 

![Download prerequisites](media/installingprereqs.png)

> [!Note]  
> <span data-ttu-id="f7ac4-145">If you're experiencing slow network speed when downloading these images, download them separately to a local share and specify the parameter **-LocalPackagePath** *FileShareOrLocalPath*.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-145">If you're experiencing slow network speed when downloading these images, download them separately to a local share and specify the parameter **-LocalPackagePath** *FileShareOrLocalPath*.</span></span> <span data-ttu-id="f7ac4-146">You can find more guidance on your PIR download in the section [Handle slow network connectivity](azure-stack-vaas-troubleshoot.md#handle-slow-network-connectivity) of [Troubleshoot validation as a service](azure-stack-vaas-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="f7ac4-146">You can find more guidance on your PIR download in the section [Handle slow network connectivity](azure-stack-vaas-troubleshoot.md#handle-slow-network-connectivity) of [Troubleshoot validation as a service](azure-stack-vaas-troubleshoot.md).</span></span>

## <a name="fault-injection"></a><span data-ttu-id="f7ac4-147">Fault injection</span><span class="sxs-lookup"><span data-stu-id="f7ac4-147">Fault injection</span></span>

<span data-ttu-id="f7ac4-148">Microsoft designed Azure Stack for resilience and to tolerate multiple types of software and hardware faults.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-148">Microsoft designed Azure Stack for resilience and to tolerate multiple types of software and hardware faults.</span></span> <span data-ttu-id="f7ac4-149">Fault injection increases the rate of faults in the system.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-149">Fault injection increases the rate of faults in the system.</span></span> <span data-ttu-id="f7ac4-150">This increase helps you uncover issues earlier so that you can reduce the number of incidents that bring the system down.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-150">This increase helps you uncover issues earlier so that you can reduce the number of incidents that bring the system down.</span></span>

<span data-ttu-id="f7ac4-151">Run the following commands to inject faults into your system.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-151">Run the following commands to inject faults into your system.</span></span>

1. <span data-ttu-id="f7ac4-152">Open Windows PowerShell in an elevated prompt.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-152">Open Windows PowerShell in an elevated prompt.</span></span>

2. <span data-ttu-id="f7ac4-153">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="f7ac4-153">Run the following command:</span></span>

    ```PowerShell  
        Import-Module .\VaaSPreReqs.psm1 -Force
        Install-ServiceFabricSDK Install-ServiceFabricSDK
    ```

## <a name="run-the-agent"></a><span data-ttu-id="f7ac4-154">Run the agent</span><span class="sxs-lookup"><span data-stu-id="f7ac4-154">Run the agent</span></span>

1. <span data-ttu-id="f7ac4-155">Open Windows PowerShell in an elevated prompt.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-155">Open Windows PowerShell in an elevated prompt.</span></span>

2. <span data-ttu-id="f7ac4-156">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="f7ac4-156">Run the following command:</span></span>

    ````PowerShell  
    .\Microsoft.VaaSOnPrem.TaskEngineHost.exe -u <VaaSUserId> -t <VaaSTenantId>
    ````

      <span data-ttu-id="f7ac4-157">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="f7ac4-157">**Parameters**</span></span>  
    
    | <span data-ttu-id="f7ac4-158">Parameter</span><span class="sxs-lookup"><span data-stu-id="f7ac4-158">Parameter</span></span> | <span data-ttu-id="f7ac4-159">Description</span><span class="sxs-lookup"><span data-stu-id="f7ac4-159">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="f7ac4-160">VaaSUserId</span><span class="sxs-lookup"><span data-stu-id="f7ac4-160">VaaSUserId</span></span> | <span data-ttu-id="f7ac4-161">User ID used to sign in to the VaaS Portal (for example, UserName@Contoso.com)</span><span class="sxs-lookup"><span data-stu-id="f7ac4-161">User ID used to sign in to the VaaS Portal (for example, UserName@Contoso.com)</span></span> |
    | <span data-ttu-id="f7ac4-162">VaaSTenantId</span><span class="sxs-lookup"><span data-stu-id="f7ac4-162">VaaSTenantId</span></span> | <span data-ttu-id="f7ac4-163">Azure AD tenant ID for the Azure account registered with Validation as a Service.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-163">Azure AD tenant ID for the Azure account registered with Validation as a Service.</span></span> |

    > [!Note]  
    > <span data-ttu-id="f7ac4-164">When you run the agent, the current working directory must be the location of the task engine host executable, **Microsoft.VaaSOnPrem.TaskEngineHost.exe.**</span><span class="sxs-lookup"><span data-stu-id="f7ac4-164">When you run the agent, the current working directory must be the location of the task engine host executable, **Microsoft.VaaSOnPrem.TaskEngineHost.exe.**</span></span>

<span data-ttu-id="f7ac4-165">If you don't see any errors reported, then the local agent has succeeded.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-165">If you don't see any errors reported, then the local agent has succeeded.</span></span> <span data-ttu-id="f7ac4-166">The following example text appears on the console window.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-166">The following example text appears on the console window.</span></span>

`Heartbeat Callback at 11/8/2016 4:45:38 PM`

![Started agent](media/startedagent.png)

<span data-ttu-id="f7ac4-168">An agent is uniquely identified by its name.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-168">An agent is uniquely identified by its name.</span></span> <span data-ttu-id="f7ac4-169">By default, it uses the fully qualified domain name (FQDN) name of the machine from where it was started.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-169">By default, it uses the fully qualified domain name (FQDN) name of the machine from where it was started.</span></span> <span data-ttu-id="f7ac4-170">You must minimize the window to avoid any accidental clicks on the window as changing the focus pauses all other actions.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-170">You must minimize the window to avoid any accidental clicks on the window as changing the focus pauses all other actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7ac4-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7ac4-171">Next steps</span></span>

- [<span data-ttu-id="f7ac4-172">Validate a new Azure Stack solution</span><span class="sxs-lookup"><span data-stu-id="f7ac4-172">Validate a new Azure Stack solution</span></span>](azure-stack-vaas-validate-solution-new.md)  
- <span data-ttu-id="f7ac4-173">If you have slow or intermittent Internet connectivity, you can download the PIR image.</span><span class="sxs-lookup"><span data-stu-id="f7ac4-173">If you have slow or intermittent Internet connectivity, you can download the PIR image.</span></span> <span data-ttu-id="f7ac4-174">For more information, see [Handle slow network connectivity](azure-stack-vaas-troubleshoot.md#handle-slow-network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="f7ac4-174">For more information, see [Handle slow network connectivity](azure-stack-vaas-troubleshoot.md#handle-slow-network-connectivity).</span></span>
- <span data-ttu-id="f7ac4-175">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="f7ac4-175">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
