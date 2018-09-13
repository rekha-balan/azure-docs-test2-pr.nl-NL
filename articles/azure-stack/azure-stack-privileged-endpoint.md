---
title: Using the privileged endpoint in Azure Stack | Microsoft Docs
description: Shows how to use the privileged endpoint (PEP) in Azure Stack (for an Azure Stack operator).
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.reviewer: fiseraci
ms.openlocfilehash: d91ad42d4d84802c4579a4d228a35030970da8e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871604"
---
# <a name="using-the-privileged-endpoint-in-azure-stack"></a><span data-ttu-id="b6c42-103">Using the privileged endpoint in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b6c42-103">Using the privileged endpoint in Azure Stack</span></span>

<span data-ttu-id="b6c42-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="b6c42-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="b6c42-105">As an Azure Stack operator, you should use the administrator portal, PowerShell, or Azure Resource Manager APIs for most day-to-day management tasks.</span><span class="sxs-lookup"><span data-stu-id="b6c42-105">As an Azure Stack operator, you should use the administrator portal, PowerShell, or Azure Resource Manager APIs for most day-to-day management tasks.</span></span> <span data-ttu-id="b6c42-106">However, for some less common operations, you need to use the *privileged endpoint* (PEP).</span><span class="sxs-lookup"><span data-stu-id="b6c42-106">However, for some less common operations, you need to use the *privileged endpoint* (PEP).</span></span> <span data-ttu-id="b6c42-107">The PEP is a pre-configured remote PowerShell console that provides you with just enough capabilities to help you perform a required task.</span><span class="sxs-lookup"><span data-stu-id="b6c42-107">The PEP is a pre-configured remote PowerShell console that provides you with just enough capabilities to help you perform a required task.</span></span> <span data-ttu-id="b6c42-108">The endpoint uses [PowerShell JEA (Just Enough Administration)](https://docs.microsoft.com/powershell/jea/overview) to expose only a restricted set of cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b6c42-108">The endpoint uses [PowerShell JEA (Just Enough Administration)](https://docs.microsoft.com/powershell/jea/overview) to expose only a restricted set of cmdlets.</span></span> <span data-ttu-id="b6c42-109">To access the PEP and invoke the restricted set of cmdlets, a low-privileged account is used.</span><span class="sxs-lookup"><span data-stu-id="b6c42-109">To access the PEP and invoke the restricted set of cmdlets, a low-privileged account is used.</span></span> <span data-ttu-id="b6c42-110">No administrator accounts are required.</span><span class="sxs-lookup"><span data-stu-id="b6c42-110">No administrator accounts are required.</span></span> <span data-ttu-id="b6c42-111">For additional security, scripting is not allowed.</span><span class="sxs-lookup"><span data-stu-id="b6c42-111">For additional security, scripting is not allowed.</span></span>

<span data-ttu-id="b6c42-112">You can use the PEP to perform tasks such as the following:</span><span class="sxs-lookup"><span data-stu-id="b6c42-112">You can use the PEP to perform tasks such as the following:</span></span>

- <span data-ttu-id="b6c42-113">To perform low-level tasks, such as [collecting diagnostic logs](https://docs.microsoft.com/azure/azure-stack/azure-stack-diagnostics#log-collection-tool).</span><span class="sxs-lookup"><span data-stu-id="b6c42-113">To perform low-level tasks, such as [collecting diagnostic logs](https://docs.microsoft.com/azure/azure-stack/azure-stack-diagnostics#log-collection-tool).</span></span>
- <span data-ttu-id="b6c42-114">To perform many post-deployment datacenter integration tasks for integrated systems, such as adding Domain Name System (DNS) forwarders after deployment, setting up Microsoft Graph integration, Active Directory Federation Services (AD FS) integration, certificate rotation, etc.</span><span class="sxs-lookup"><span data-stu-id="b6c42-114">To perform many post-deployment datacenter integration tasks for integrated systems, such as adding Domain Name System (DNS) forwarders after deployment, setting up Microsoft Graph integration, Active Directory Federation Services (AD FS) integration, certificate rotation, etc.</span></span>
- <span data-ttu-id="b6c42-115">To work with Support to obtain temporary, high-level access for in-depth troubleshooting of an integrated system.</span><span class="sxs-lookup"><span data-stu-id="b6c42-115">To work with Support to obtain temporary, high-level access for in-depth troubleshooting of an integrated system.</span></span>

<span data-ttu-id="b6c42-116">The PEP logs every action (and its corresponding output) that you perform in the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="b6c42-116">The PEP logs every action (and its corresponding output) that you perform in the PowerShell session.</span></span> <span data-ttu-id="b6c42-117">This provides full transparency and complete auditing of operations.</span><span class="sxs-lookup"><span data-stu-id="b6c42-117">This provides full transparency and complete auditing of operations.</span></span> <span data-ttu-id="b6c42-118">You can retain these log files for future audits.</span><span class="sxs-lookup"><span data-stu-id="b6c42-118">You can retain these log files for future audits.</span></span>

> [!NOTE]
> <span data-ttu-id="b6c42-119">In the Azure Stack Development Kit (ASDK), you can run some of the commands available in the PEP directly from a PowerShell session on the development kit host.</span><span class="sxs-lookup"><span data-stu-id="b6c42-119">In the Azure Stack Development Kit (ASDK), you can run some of the commands available in the PEP directly from a PowerShell session on the development kit host.</span></span> <span data-ttu-id="b6c42-120">However, you may want to test some operations using the PEP, such as log collection, because this is the only method available to perform certain operations in an integrated systems environment.</span><span class="sxs-lookup"><span data-stu-id="b6c42-120">However, you may want to test some operations using the PEP, such as log collection, because this is the only method available to perform certain operations in an integrated systems environment.</span></span>

## <a name="access-the-privileged-endpoint"></a><span data-ttu-id="b6c42-121">Access the privileged endpoint</span><span class="sxs-lookup"><span data-stu-id="b6c42-121">Access the privileged endpoint</span></span>

<span data-ttu-id="b6c42-122">You access the PEP through a remote PowerShell session on the virtual machine that hosts the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-122">You access the PEP through a remote PowerShell session on the virtual machine that hosts the PEP.</span></span> <span data-ttu-id="b6c42-123">In the ASDK, this virtual machine is named **AzS-ERCS01**.</span><span class="sxs-lookup"><span data-stu-id="b6c42-123">In the ASDK, this virtual machine is named **AzS-ERCS01**.</span></span> <span data-ttu-id="b6c42-124">If you’re using an integrated system, there are three instances of the PEP, each running inside a virtual machine (*Prefix*-ERCS01, *Prefix*-ERCS02, or *Prefix*-ERCS03) on different hosts for resiliency.</span><span class="sxs-lookup"><span data-stu-id="b6c42-124">If you’re using an integrated system, there are three instances of the PEP, each running inside a virtual machine (*Prefix*-ERCS01, *Prefix*-ERCS02, or *Prefix*-ERCS03) on different hosts for resiliency.</span></span> 

<span data-ttu-id="b6c42-125">Before you begin this procedure for an integrated system, make sure you can access the PEP either by IP address, or through DNS.</span><span class="sxs-lookup"><span data-stu-id="b6c42-125">Before you begin this procedure for an integrated system, make sure you can access the PEP either by IP address, or through DNS.</span></span> <span data-ttu-id="b6c42-126">After the initial deployment of Azure Stack, you can access the PEP only by IP address because DNS integration is not yet set up.</span><span class="sxs-lookup"><span data-stu-id="b6c42-126">After the initial deployment of Azure Stack, you can access the PEP only by IP address because DNS integration is not yet set up.</span></span> <span data-ttu-id="b6c42-127">Your OEM hardware vendor will provide you with a JSON file named **AzureStackStampDeploymentInfo** that contains the PEP IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b6c42-127">Your OEM hardware vendor will provide you with a JSON file named **AzureStackStampDeploymentInfo** that contains the PEP IP addresses.</span></span>


> [!NOTE]
> <span data-ttu-id="b6c42-128">For security reasons, we require that you connect to the PEP only from a hardened virtual machine running on top of the hardware lifecycle host, or from a dedicated, secure computer, such as a [Privileged Access Workstation](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/privileged-access-workstations).</span><span class="sxs-lookup"><span data-stu-id="b6c42-128">For security reasons, we require that you connect to the PEP only from a hardened virtual machine running on top of the hardware lifecycle host, or from a dedicated, secure computer, such as a [Privileged Access Workstation](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/privileged-access-workstations).</span></span> <span data-ttu-id="b6c42-129">The original configuration of the hardware lifecycle host must not be modified from its original configuration, including installing new software, nor it should be used to connect to the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-129">The original configuration of the hardware lifecycle host must not be modified from its original configuration, including installing new software, nor it should be used to connect to the PEP.</span></span>

1. <span data-ttu-id="b6c42-130">Establish the trust.</span><span class="sxs-lookup"><span data-stu-id="b6c42-130">Establish the trust.</span></span>

    - <span data-ttu-id="b6c42-131">On an integrated system, run the following command from an elevated Windows PowerShell session to add the PEP as a trusted host on the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation.</span><span class="sxs-lookup"><span data-stu-id="b6c42-131">On an integrated system, run the following command from an elevated Windows PowerShell session to add the PEP as a trusted host on the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation.</span></span>

      ````PowerShell
        winrm s winrm/config/client '@{TrustedHosts="<IP Address of Privileged Endpoint>"}'
      ````
    - <span data-ttu-id="b6c42-132">If you’re running the ADSK, sign in to the development kit host.</span><span class="sxs-lookup"><span data-stu-id="b6c42-132">If you’re running the ADSK, sign in to the development kit host.</span></span>

2. <span data-ttu-id="b6c42-133">On the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation, open a Windows PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="b6c42-133">On the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation, open a Windows PowerShell session.</span></span> <span data-ttu-id="b6c42-134">Run the following commands to establish a remote session on the virtual machine that hosts the PEP:</span><span class="sxs-lookup"><span data-stu-id="b6c42-134">Run the following commands to establish a remote session on the virtual machine that hosts the PEP:</span></span>
 
    - <span data-ttu-id="b6c42-135">On an integrated system:</span><span class="sxs-lookup"><span data-stu-id="b6c42-135">On an integrated system:</span></span>
      ````PowerShell
        $cred = Get-Credential

        Enter-PSSession -ComputerName <IP_address_of_ERCS> `
          -ConfigurationName PrivilegedEndpoint -Credential $cred
      ````
      <span data-ttu-id="b6c42-136">The `ComputerName` parameter can be either the IP address or the DNS name of one of the virtual machines that hosts the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-136">The `ComputerName` parameter can be either the IP address or the DNS name of one of the virtual machines that hosts the PEP.</span></span> 
    - <span data-ttu-id="b6c42-137">If you’re running the ADSK:</span><span class="sxs-lookup"><span data-stu-id="b6c42-137">If you’re running the ADSK:</span></span>
     
      ````PowerShell
        $cred = Get-Credential

        Enter-PSSession -ComputerName azs-ercs01 `
          -ConfigurationName PrivilegedEndpoint -Credential $cred
      ```` 
   <span data-ttu-id="b6c42-138">When prompted, use the following credentials:</span><span class="sxs-lookup"><span data-stu-id="b6c42-138">When prompted, use the following credentials:</span></span>

      - <span data-ttu-id="b6c42-139">**User name**: Specify the CloudAdmin account, in the format **&lt;*Azure Stack domain*&gt;\cloudadmin**.</span><span class="sxs-lookup"><span data-stu-id="b6c42-139">**User name**: Specify the CloudAdmin account, in the format **&lt;*Azure Stack domain*&gt;\cloudadmin**.</span></span> <span data-ttu-id="b6c42-140">(For ASDK, the user name is **azurestack\cloudadmin**.)</span><span class="sxs-lookup"><span data-stu-id="b6c42-140">(For ASDK, the user name is **azurestack\cloudadmin**.)</span></span>
      - <span data-ttu-id="b6c42-141">**Password**: Enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span><span class="sxs-lookup"><span data-stu-id="b6c42-141">**Password**: Enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6c42-142">If you are unable to connect to the ERCS endpoint, try steps one and two again with the IP address of an ERCS VM to which you haven't already tried to connect.</span><span class="sxs-lookup"><span data-stu-id="b6c42-142">If you are unable to connect to the ERCS endpoint, try steps one and two again with the IP address of an ERCS VM to which you haven't already tried to connect.</span></span>

3.  <span data-ttu-id="b6c42-143">After you connect, the prompt will change to **[*IP address or ERCS VM name*]: PS>** or to **[azs-ercs01]: PS>**, depending on the environment.</span><span class="sxs-lookup"><span data-stu-id="b6c42-143">After you connect, the prompt will change to **[*IP address or ERCS VM name*]: PS>** or to **[azs-ercs01]: PS>**, depending on the environment.</span></span> <span data-ttu-id="b6c42-144">From here, run `Get-Command` to view the list of available cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b6c42-144">From here, run `Get-Command` to view the list of available cmdlets.</span></span>

    <span data-ttu-id="b6c42-145">Many of these cmdlets are intended only for integrated system environments (such as the cmdlets related to datacenter integration).</span><span class="sxs-lookup"><span data-stu-id="b6c42-145">Many of these cmdlets are intended only for integrated system environments (such as the cmdlets related to datacenter integration).</span></span> <span data-ttu-id="b6c42-146">In the ASDK, the following cmdlets have been validated:</span><span class="sxs-lookup"><span data-stu-id="b6c42-146">In the ASDK, the following cmdlets have been validated:</span></span>

    - <span data-ttu-id="b6c42-147">Clear-Host</span><span class="sxs-lookup"><span data-stu-id="b6c42-147">Clear-Host</span></span>
    - <span data-ttu-id="b6c42-148">Close-PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="b6c42-148">Close-PrivilegedEndpoint</span></span>
    - <span data-ttu-id="b6c42-149">Exit-PSSession</span><span class="sxs-lookup"><span data-stu-id="b6c42-149">Exit-PSSession</span></span>
    - <span data-ttu-id="b6c42-150">Get-AzureStackLog</span><span class="sxs-lookup"><span data-stu-id="b6c42-150">Get-AzureStackLog</span></span>
    - <span data-ttu-id="b6c42-151">Get-AzureStackStampInformation</span><span class="sxs-lookup"><span data-stu-id="b6c42-151">Get-AzureStackStampInformation</span></span>
    - <span data-ttu-id="b6c42-152">Get-Command</span><span class="sxs-lookup"><span data-stu-id="b6c42-152">Get-Command</span></span>
    - <span data-ttu-id="b6c42-153">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="b6c42-153">Get-FormatData</span></span>
    - <span data-ttu-id="b6c42-154">Get-Help</span><span class="sxs-lookup"><span data-stu-id="b6c42-154">Get-Help</span></span>
    - <span data-ttu-id="b6c42-155">Get-ThirdPartyNotices</span><span class="sxs-lookup"><span data-stu-id="b6c42-155">Get-ThirdPartyNotices</span></span>
    - <span data-ttu-id="b6c42-156">Measure-Object</span><span class="sxs-lookup"><span data-stu-id="b6c42-156">Measure-Object</span></span>
    - <span data-ttu-id="b6c42-157">New-CloudAdminUser</span><span class="sxs-lookup"><span data-stu-id="b6c42-157">New-CloudAdminUser</span></span>
    - <span data-ttu-id="b6c42-158">Out-Default</span><span class="sxs-lookup"><span data-stu-id="b6c42-158">Out-Default</span></span>
    - <span data-ttu-id="b6c42-159">Remove-CloudAdminUser</span><span class="sxs-lookup"><span data-stu-id="b6c42-159">Remove-CloudAdminUser</span></span>
    - <span data-ttu-id="b6c42-160">Select-Object</span><span class="sxs-lookup"><span data-stu-id="b6c42-160">Select-Object</span></span>
    - <span data-ttu-id="b6c42-161">Set-CloudAdminUserPassword</span><span class="sxs-lookup"><span data-stu-id="b6c42-161">Set-CloudAdminUserPassword</span></span>
    - <span data-ttu-id="b6c42-162">Test-AzureStack</span><span class="sxs-lookup"><span data-stu-id="b6c42-162">Test-AzureStack</span></span>
    - <span data-ttu-id="b6c42-163">Stop-AzureStack</span><span class="sxs-lookup"><span data-stu-id="b6c42-163">Stop-AzureStack</span></span>
    - <span data-ttu-id="b6c42-164">Get-ClusterLog</span><span class="sxs-lookup"><span data-stu-id="b6c42-164">Get-ClusterLog</span></span>

## <a name="tips-for-using-the-privileged-endpoint"></a><span data-ttu-id="b6c42-165">Tips for using the privileged endpoint</span><span class="sxs-lookup"><span data-stu-id="b6c42-165">Tips for using the privileged endpoint</span></span> 

<span data-ttu-id="b6c42-166">As mentioned above, the PEP is a [PowerShell JEA](https://docs.microsoft.com/powershell/jea/overview) endpoint.</span><span class="sxs-lookup"><span data-stu-id="b6c42-166">As mentioned above, the PEP is a [PowerShell JEA](https://docs.microsoft.com/powershell/jea/overview) endpoint.</span></span> <span data-ttu-id="b6c42-167">While providing a strong security layer, a JEA endpoint reduces some of the basic PowerShell capabilities, such as scripting or tab completion.</span><span class="sxs-lookup"><span data-stu-id="b6c42-167">While providing a strong security layer, a JEA endpoint reduces some of the basic PowerShell capabilities, such as scripting or tab completion.</span></span> <span data-ttu-id="b6c42-168">If you try any type of script operation, the operation fails with the error **ScriptsNotAllowed**.</span><span class="sxs-lookup"><span data-stu-id="b6c42-168">If you try any type of script operation, the operation fails with the error **ScriptsNotAllowed**.</span></span> <span data-ttu-id="b6c42-169">This is expected behavior.</span><span class="sxs-lookup"><span data-stu-id="b6c42-169">This is expected behavior.</span></span>

<span data-ttu-id="b6c42-170">So, for instance, to get the list of parameters for a given cmdlet, you run the following command:</span><span class="sxs-lookup"><span data-stu-id="b6c42-170">So, for instance, to get the list of parameters for a given cmdlet, you run the following command:</span></span>

```PowerShell
    Get-Command <cmdlet_name> -Syntax
```

<span data-ttu-id="b6c42-171">Alternatively, you can use the [Import-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Utility/Import-PSSession?view=powershell-5.1) cmdlet to import all the PEP cmdlets into the current session on your local machine.</span><span class="sxs-lookup"><span data-stu-id="b6c42-171">Alternatively, you can use the [Import-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Utility/Import-PSSession?view=powershell-5.1) cmdlet to import all the PEP cmdlets into the current session on your local machine.</span></span> <span data-ttu-id="b6c42-172">By doing so, all cmdlets and functions of the PEP are now available on your local machine, together with tab completion and, more in general, scripting.</span><span class="sxs-lookup"><span data-stu-id="b6c42-172">By doing so, all cmdlets and functions of the PEP are now available on your local machine, together with tab completion and, more in general, scripting.</span></span> 

<span data-ttu-id="b6c42-173">To import the PEP session on your local machine, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b6c42-173">To import the PEP session on your local machine, do the following steps:</span></span>

1. <span data-ttu-id="b6c42-174">Establish the trust.</span><span class="sxs-lookup"><span data-stu-id="b6c42-174">Establish the trust.</span></span>

    <span data-ttu-id="b6c42-175">-On an integrated system, run the following command from an elevated Windows PowerShell session to add the PEP as a trusted host on the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation.</span><span class="sxs-lookup"><span data-stu-id="b6c42-175">-On an integrated system, run the following command from an elevated Windows PowerShell session to add the PEP as a trusted host on the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation.</span></span>

      ````PowerShell
        winrm s winrm/config/client '@{TrustedHosts="<IP Address of Privileged Endpoint>"}'
      ````
    - <span data-ttu-id="b6c42-176">If you’re running the ADSK, sign in to the development kit host.</span><span class="sxs-lookup"><span data-stu-id="b6c42-176">If you’re running the ADSK, sign in to the development kit host.</span></span>

2. <span data-ttu-id="b6c42-177">On the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation, open a Windows PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="b6c42-177">On the hardened virtual machine running on the hardware lifecycle host or the Privileged Access Workstation, open a Windows PowerShell session.</span></span> <span data-ttu-id="b6c42-178">Run the following commands to establish a remote session on the virtual machine that hosts the PEP:</span><span class="sxs-lookup"><span data-stu-id="b6c42-178">Run the following commands to establish a remote session on the virtual machine that hosts the PEP:</span></span>
 
    - <span data-ttu-id="b6c42-179">On an integrated system:</span><span class="sxs-lookup"><span data-stu-id="b6c42-179">On an integrated system:</span></span>
      ````PowerShell
        $cred = Get-Credential

        $session = New-PSSession -ComputerName <IP_address_of_ERCS> `
          -ConfigurationName PrivilegedEndpoint -Credential $cred
      ````
      <span data-ttu-id="b6c42-180">The `ComputerName` parameter can be either the IP address or the DNS name of one of the virtual machines that hosts the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-180">The `ComputerName` parameter can be either the IP address or the DNS name of one of the virtual machines that hosts the PEP.</span></span> 
    - <span data-ttu-id="b6c42-181">If you’re running the ADSK:</span><span class="sxs-lookup"><span data-stu-id="b6c42-181">If you’re running the ADSK:</span></span>
     
      ````PowerShell
       $cred = Get-Credential

       $session = New-PSSession -ComputerName azs-ercs01 `
          -ConfigurationName PrivilegedEndpoint -Credential $cred
      ```` 
   <span data-ttu-id="b6c42-182">When prompted, use the following credentials:</span><span class="sxs-lookup"><span data-stu-id="b6c42-182">When prompted, use the following credentials:</span></span>

      - <span data-ttu-id="b6c42-183">**User name**: Specify the CloudAdmin account, in the format **&lt;*Azure Stack domain*&gt;\cloudadmin**.</span><span class="sxs-lookup"><span data-stu-id="b6c42-183">**User name**: Specify the CloudAdmin account, in the format **&lt;*Azure Stack domain*&gt;\cloudadmin**.</span></span> <span data-ttu-id="b6c42-184">(For ASDK, the user name is **azurestack\cloudadmin**.)</span><span class="sxs-lookup"><span data-stu-id="b6c42-184">(For ASDK, the user name is **azurestack\cloudadmin**.)</span></span>
      - <span data-ttu-id="b6c42-185">**Password**: Enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span><span class="sxs-lookup"><span data-stu-id="b6c42-185">**Password**: Enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span></span>

3. <span data-ttu-id="b6c42-186">Import the PEP session into your local machine</span><span class="sxs-lookup"><span data-stu-id="b6c42-186">Import the PEP session into your local machine</span></span>
    ````PowerShell 
        Import-PSSession $session
    ````
4. <span data-ttu-id="b6c42-187">Now, you can use tab-completion and do scripting as usual on your local PowerShell session with all the functions and cmdlets of the PEP, without decreasing the security posture of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b6c42-187">Now, you can use tab-completion and do scripting as usual on your local PowerShell session with all the functions and cmdlets of the PEP, without decreasing the security posture of Azure Stack.</span></span> <span data-ttu-id="b6c42-188">Enjoy!</span><span class="sxs-lookup"><span data-stu-id="b6c42-188">Enjoy!</span></span>


## <a name="close-the-privileged-endpoint-session"></a><span data-ttu-id="b6c42-189">Close the privileged endpoint session</span><span class="sxs-lookup"><span data-stu-id="b6c42-189">Close the privileged endpoint session</span></span>

 <span data-ttu-id="b6c42-190">As mentioned earlier, the PEP logs every action (and its corresponding output) that you perform in the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="b6c42-190">As mentioned earlier, the PEP logs every action (and its corresponding output) that you perform in the PowerShell session.</span></span> <span data-ttu-id="b6c42-191">You must close the session by using the  `Close-PrivilegedEndpoint` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6c42-191">You must close the session by using the  `Close-PrivilegedEndpoint` cmdlet.</span></span> <span data-ttu-id="b6c42-192">This cmdlet correctly closes the endpoint, and transfers the log files to an external file share for retention.</span><span class="sxs-lookup"><span data-stu-id="b6c42-192">This cmdlet correctly closes the endpoint, and transfers the log files to an external file share for retention.</span></span>

<span data-ttu-id="b6c42-193">To close the endpoint session:</span><span class="sxs-lookup"><span data-stu-id="b6c42-193">To close the endpoint session:</span></span>

1. <span data-ttu-id="b6c42-194">Create an external file share that is accessible by the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-194">Create an external file share that is accessible by the PEP.</span></span> <span data-ttu-id="b6c42-195">In a development kit environment, you can just create a file share on the development kit host.</span><span class="sxs-lookup"><span data-stu-id="b6c42-195">In a development kit environment, you can just create a file share on the development kit host.</span></span>
2. <span data-ttu-id="b6c42-196">Run the `Close-PrivilegedEndpoint` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6c42-196">Run the `Close-PrivilegedEndpoint` cmdlet.</span></span> 
3. <span data-ttu-id="b6c42-197">You're prompted for a path on which to store the transcript log file.</span><span class="sxs-lookup"><span data-stu-id="b6c42-197">You're prompted for a path on which to store the transcript log file.</span></span> <span data-ttu-id="b6c42-198">Specify the file share that you created earlier, in the format &#92;&#92;*servername*&#92;*sharename*.</span><span class="sxs-lookup"><span data-stu-id="b6c42-198">Specify the file share that you created earlier, in the format &#92;&#92;*servername*&#92;*sharename*.</span></span> <span data-ttu-id="b6c42-199">If you don’t specify a path, the cmdlet fails and the session remains open.</span><span class="sxs-lookup"><span data-stu-id="b6c42-199">If you don’t specify a path, the cmdlet fails and the session remains open.</span></span> 

    ![Close-PrivilegedEndpoint cmdlet output that shows where you specify the transcript destination path](media/azure-stack-privileged-endpoint/closeendpoint.png)

<span data-ttu-id="b6c42-201">After the transcript log files are successfully transferred to the file share, they're automatically deleted from the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-201">After the transcript log files are successfully transferred to the file share, they're automatically deleted from the PEP.</span></span> 

> [!NOTE]
> <span data-ttu-id="b6c42-202">If you close the PEP session by using the cmdlets `Exit-PSSession` or `Exit`, or you just close the PowerShell console, the transcript logs don't transfer to a file share.</span><span class="sxs-lookup"><span data-stu-id="b6c42-202">If you close the PEP session by using the cmdlets `Exit-PSSession` or `Exit`, or you just close the PowerShell console, the transcript logs don't transfer to a file share.</span></span> <span data-ttu-id="b6c42-203">They remain in the PEP.</span><span class="sxs-lookup"><span data-stu-id="b6c42-203">They remain in the PEP.</span></span> <span data-ttu-id="b6c42-204">The next time you run `Close-PrivilegedEndpoint` and include a file share, the transcript logs from the previous session(s) will also transfer.</span><span class="sxs-lookup"><span data-stu-id="b6c42-204">The next time you run `Close-PrivilegedEndpoint` and include a file share, the transcript logs from the previous session(s) will also transfer.</span></span> <span data-ttu-id="b6c42-205">Do not use `Exit-PSSession` or `Exit` to close the PEP session; use `Close-PrivilegedEndpoint` instead.</span><span class="sxs-lookup"><span data-stu-id="b6c42-205">Do not use `Exit-PSSession` or `Exit` to close the PEP session; use `Close-PrivilegedEndpoint` instead.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b6c42-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6c42-206">Next steps</span></span>
[<span data-ttu-id="b6c42-207">Azure Stack diagnostic tools</span><span class="sxs-lookup"><span data-stu-id="b6c42-207">Azure Stack diagnostic tools</span></span>](azure-stack-diagnostics.md)
