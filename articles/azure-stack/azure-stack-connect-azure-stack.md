---
title: Connect to Azure Stack | Microsoft Docs
description: Learn how to connect Azure Stack
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/29/2017
ms.author: sngun
ms.openlocfilehash: 5f391613a64a2bd666ef6d0b23241a2d611ce04a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555819"
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="ad381-103">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ad381-103">Connect to Azure Stack</span></span>
<span data-ttu-id="ad381-104">To manage resources, you must connect to the Azure Stack POC computer.</span><span class="sxs-lookup"><span data-stu-id="ad381-104">To manage resources, you must connect to the Azure Stack POC computer.</span></span> <span data-ttu-id="ad381-105">You can use either of the following connection options:</span><span class="sxs-lookup"><span data-stu-id="ad381-105">You can use either of the following connection options:</span></span>

* <span data-ttu-id="ad381-106">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the POC computer.</span><span class="sxs-lookup"><span data-stu-id="ad381-106">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the POC computer.</span></span>
* <span data-ttu-id="ad381-107">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span><span class="sxs-lookup"><span data-stu-id="ad381-107">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="ad381-108">Connect with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="ad381-108">Connect with Remote Desktop</span></span>
<span data-ttu-id="ad381-109">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span><span class="sxs-lookup"><span data-stu-id="ad381-109">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span> <span data-ttu-id="ad381-110">You can also use tools on the MAS-CON01 virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ad381-110">You can also use tools on the MAS-CON01 virtual machine.</span></span>

1. <span data-ttu-id="ad381-111">Log in to the Azure Stack POC physical machine.</span><span class="sxs-lookup"><span data-stu-id="ad381-111">Log in to the Azure Stack POC physical machine.</span></span>
2. <span data-ttu-id="ad381-112">Open a Remote Desktop Connection and connect to MAS-CON01.</span><span class="sxs-lookup"><span data-stu-id="ad381-112">Open a Remote Desktop Connection and connect to MAS-CON01.</span></span> <span data-ttu-id="ad381-113">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password you provided during Azure Stack setup.</span><span class="sxs-lookup"><span data-stu-id="ad381-113">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password you provided during Azure Stack setup.</span></span>  
3. <span data-ttu-id="ad381-114">On the MAS-CON01 desktop, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span><span class="sxs-lookup"><span data-stu-id="ad381-114">On the MAS-CON01 desktop, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>
4. <span data-ttu-id="ad381-115">To open the user [portal](azure-stack-key-features.md#portal), navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span><span class="sxs-lookup"><span data-stu-id="ad381-115">To open the user [portal](azure-stack-key-features.md#portal), navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span>
    <span data-ttu-id="ad381-116">To open the administrator [portal](azure-stack-key-features.md#portal), navigate to (https://adminportal.local.azurestack.external/) and sign in using the Azure Active Directory credentials specified during installation.</span><span class="sxs-lookup"><span data-stu-id="ad381-116">To open the administrator [portal](azure-stack-key-features.md#portal), navigate to (https://adminportal.local.azurestack.external/) and sign in using the Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-with-vpn"></a><span data-ttu-id="ad381-117">Connect with VPN</span><span class="sxs-lookup"><span data-stu-id="ad381-117">Connect with VPN</span></span>

<span data-ttu-id="ad381-118">In an Azure Stack Proof of Concept (POC) environment, you can use a Virtual Private Network (VPN) to connect your local Windows-based computer to Azure Stack.VPN connectivity is supported for Azure Stack instances deployed through Azure Active Directory(AAD) or Active Directory Federation Services(AD FS) .</span><span class="sxs-lookup"><span data-stu-id="ad381-118">In an Azure Stack Proof of Concept (POC) environment, you can use a Virtual Private Network (VPN) to connect your local Windows-based computer to Azure Stack.VPN connectivity is supported for Azure Stack instances deployed through Azure Active Directory(AAD) or Active Directory Federation Services(AD FS) .</span></span> <span data-ttu-id="ad381-119">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span><span class="sxs-lookup"><span data-stu-id="ad381-119">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span>
 
<span data-ttu-id="ad381-120">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="ad381-120">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="ad381-121">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span><span class="sxs-lookup"><span data-stu-id="ad381-121">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

<span data-ttu-id="ad381-122">The following sections describe the steps that are required to establish VPN connectivity to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ad381-122">The following sections describe the steps that are required to establish VPN connectivity to Azure Stack.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ad381-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ad381-123">Prerequisites</span></span>

* [<span data-ttu-id="ad381-124">Install Azure Stack compatible Azure PowerShell on your local computer.</span><span class="sxs-lookup"><span data-stu-id="ad381-124">Install Azure Stack compatible Azure PowerShell on your local computer.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="ad381-125">Download the tools required to work with Azure Stack to your local computer.</span><span class="sxs-lookup"><span data-stu-id="ad381-125">Download the tools required to work with Azure Stack to your local computer.</span></span>](azure-stack-powershell-download.md)  

### <a name="import-the-connect-powershell-module"></a><span data-ttu-id="ad381-126">Import the Connect PowerShell module</span><span class="sxs-lookup"><span data-stu-id="ad381-126">Import the Connect PowerShell module</span></span>

<span data-ttu-id="ad381-127">After you download the tools, navigate to the downloaded folder and import the **Connect** PowerShell module by using the following command:</span><span class="sxs-lookup"><span data-stu-id="ad381-127">After you download the tools, navigate to the downloaded folder and import the **Connect** PowerShell module by using the following command:</span></span>

```PowerShell
Import-Module .\Connect\AzureStack.Connect.psm1 
```
<span data-ttu-id="ad381-128">When you import the module, if you receive an error that says “**AzureStack.Connect.psm1** is not digitally signed.</span><span class="sxs-lookup"><span data-stu-id="ad381-128">When you import the module, if you receive an error that says “**AzureStack.Connect.psm1** is not digitally signed.</span></span> <span data-ttu-id="ad381-129">The script will not execute on the system”.</span><span class="sxs-lookup"><span data-stu-id="ad381-129">The script will not execute on the system”.</span></span> <span data-ttu-id="ad381-130">To resolve this issue, run the following command in an elevated PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="ad381-130">To resolve this issue, run the following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="configure-vpn-to-azure-stack-poc-computer"></a><span data-ttu-id="ad381-131">Configure VPN to Azure Stack PoC computer</span><span class="sxs-lookup"><span data-stu-id="ad381-131">Configure VPN to Azure Stack PoC computer</span></span>

<span data-ttu-id="ad381-132">To create a VPN connection to the Azure Stack PoC computer, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ad381-132">To create a VPN connection to the Azure Stack PoC computer, use the following steps:</span></span>


1. <span data-ttu-id="ad381-133">Add the Azure Stack PoC computer’s host IP address & certificate authority (CA) to the list of trusted hosts on your client computer by running the following commands in an elevated PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="ad381-133">Add the Azure Stack PoC computer’s host IP address & certificate authority (CA) to the list of trusted hosts on your client computer by running the following commands in an elevated PowerShell session:</span></span>

    ```PowerShell
    #Change the IP address in the following command to match your Azure Stack host IP address
    $hostIP = "<Azure Stack host IP address>"
    
    # Change the password in the following command to administrator password that is provided when deploying Azure Stack. 
    $Password = ConvertTo-SecureString "<Administrator password provided when deploying Azure Stack>" -AsPlainText -Force
    
    #Add host IP and certificate authority to the to trusted hosts
    Set-Item wsman:\localhost\Client\TrustedHosts -Value $hostIP -Concatenate
    Set-Item wsman:\localhost\Client\TrustedHosts -Value mas-ca01.azurestack.local -Concatenate
    ```

2. <span data-ttu-id="ad381-134">Get the Azure Stack host computer’s NAT IP address.</span><span class="sxs-lookup"><span data-stu-id="ad381-134">Get the Azure Stack host computer’s NAT IP address.</span></span> <span data-ttu-id="ad381-135">If you do not remember the NAT IP address of the Azure Stack PoC instance you are trying to connect to, you can get it by using the **Get-AzureStackNatServerAddress** command:</span><span class="sxs-lookup"><span data-stu-id="ad381-135">If you do not remember the NAT IP address of the Azure Stack PoC instance you are trying to connect to, you can get it by using the **Get-AzureStackNatServerAddress** command:</span></span>

    ```PowerShell
    # Get host computer's NAT IP address
    $natIp = Get-AzureStackNatServerAddress -HostComputer $hostIP -Password $Password
    ```
    ![get NAT IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-connect-azure-stack/image1.png)  

    <span data-ttu-id="ad381-137">This command remotes into the **MAS-BGPNAT01** infrastructure VM and gets the NAT IP address.</span><span class="sxs-lookup"><span data-stu-id="ad381-137">This command remotes into the **MAS-BGPNAT01** infrastructure VM and gets the NAT IP address.</span></span>  

3. <span data-ttu-id="ad381-138">Create a VPN connection entry for your local user by using the **Add-AzureStackVpnConnection** command:</span><span class="sxs-lookup"><span data-stu-id="ad381-138">Create a VPN connection entry for your local user by using the **Add-AzureStackVpnConnection** command:</span></span>

    ```PowerShell
    Add-AzureStackVpnConnection -ServerAddress $natIp -Password $Password
    ```
    ![get VPN connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-connect-azure-stack/image2.png)  

    <span data-ttu-id="ad381-140">If the connection succeeds, you should see **azurestack** in your list of VPN connections.</span><span class="sxs-lookup"><span data-stu-id="ad381-140">If the connection succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

    ![Network connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-connect-azure-stack/image3.png)  


4.  <span data-ttu-id="ad381-142">Connect to the Azure Stack instance by using either of the following methods:</span><span class="sxs-lookup"><span data-stu-id="ad381-142">Connect to the Azure Stack instance by using either of the following methods:</span></span>  

    <span data-ttu-id="ad381-143">a.</span><span class="sxs-lookup"><span data-stu-id="ad381-143">a.</span></span>  <span data-ttu-id="ad381-144">**Connect-AzureStackVpn** command:</span><span class="sxs-lookup"><span data-stu-id="ad381-144">**Connect-AzureStackVpn** command:</span></span> 
    
    ```PowerShell
    Connect-AzureStackVpn -Password $Password
    ```
    
    ![connect with cmd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-connect-azure-stack/image4.png)  

    <span data-ttu-id="ad381-146">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** into your local computer’s certificate store.</span><span class="sxs-lookup"><span data-stu-id="ad381-146">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** into your local computer’s certificate store.</span></span> <span data-ttu-id="ad381-147">(the prompt might appear behind the PowerShell session window).</span><span class="sxs-lookup"><span data-stu-id="ad381-147">(the prompt might appear behind the PowerShell session window).</span></span> 

    <span data-ttu-id="ad381-148">b.</span><span class="sxs-lookup"><span data-stu-id="ad381-148">b.</span></span>  <span data-ttu-id="ad381-149">Open your local computer’s **Network Settings** > **VPN** >click **azurestack** > **connect**</span><span class="sxs-lookup"><span data-stu-id="ad381-149">Open your local computer’s **Network Settings** > **VPN** >click **azurestack** > **connect**</span></span>

    ![connect with UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-connect-azure-stack/image5.png)  

    <span data-ttu-id="ad381-151">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span><span class="sxs-lookup"><span data-stu-id="ad381-151">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span> <span data-ttu-id="ad381-152">If the connection succeeds, the azurestack VPN should be in a **connected** state.</span><span class="sxs-lookup"><span data-stu-id="ad381-152">If the connection succeeds, the azurestack VPN should be in a **connected** state.</span></span>

### <a name="validate-the-vpn-connectivity"></a><span data-ttu-id="ad381-153">Validate the VPN connectivity</span><span class="sxs-lookup"><span data-stu-id="ad381-153">Validate the VPN connectivity</span></span>

<span data-ttu-id="ad381-154">To test the portal connection, open an Internet browser and navigate to either the user portal (https://portal.local.azurestack.external/) or the administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span><span class="sxs-lookup"><span data-stu-id="ad381-154">To test the portal connection, open an Internet browser and navigate to either the user portal (https://portal.local.azurestack.external/) or the administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ad381-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad381-155">Next steps</span></span>
* [<span data-ttu-id="ad381-156">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span><span class="sxs-lookup"><span data-stu-id="ad381-156">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>](azure-stack-add-default-image.md)
* [<span data-ttu-id="ad381-157">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="ad381-157">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
* [<span data-ttu-id="ad381-158">Provision a storage account</span><span class="sxs-lookup"><span data-stu-id="ad381-158">Provision a storage account</span></span>](azure-stack-provision-storage-account.md)
* [<span data-ttu-id="ad381-159">Develop for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ad381-159">Develop for Azure Stack</span></span>](azure-stack-developer.md)






