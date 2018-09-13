---
title: Connect to Azure Stack | Microsoft Docs
description: Learn how to connect Azure Stack
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/10/2018
ms.author: mabrigg
ms.openlocfilehash: e982df514784c37de29c9931da063f37d6886655
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870513"
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="dd88a-103">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="dd88a-103">Connect to Azure Stack</span></span>

<span data-ttu-id="dd88a-104">To manage resources, you must connect to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dd88a-104">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="dd88a-105">This article details the steps required to connect to the development kit.</span><span class="sxs-lookup"><span data-stu-id="dd88a-105">This article details the steps required to connect to the development kit.</span></span> <span data-ttu-id="dd88a-106">You can use either of the following connection options:</span><span class="sxs-lookup"><span data-stu-id="dd88a-106">You can use either of the following connection options:</span></span>

* <span data-ttu-id="dd88a-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span><span class="sxs-lookup"><span data-stu-id="dd88a-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="dd88a-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span><span class="sxs-lookup"><span data-stu-id="dd88a-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="dd88a-109">Connect to Azure Stack with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="dd88a-109">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="dd88a-110">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span><span class="sxs-lookup"><span data-stu-id="dd88a-110">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="dd88a-111">Open a Remote Desktop Connection and connect to the development kit.</span><span class="sxs-lookup"><span data-stu-id="dd88a-111">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="dd88a-112">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password that you provided during Azure Stack setup.</span><span class="sxs-lookup"><span data-stu-id="dd88a-112">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="dd88a-113">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span><span class="sxs-lookup"><span data-stu-id="dd88a-113">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="dd88a-114">To open the  portal, navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span><span class="sxs-lookup"><span data-stu-id="dd88a-114">To open the  portal, navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span>


## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="dd88a-115">Connect to Azure Stack with VPN</span><span class="sxs-lookup"><span data-stu-id="dd88a-115">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="dd88a-116">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dd88a-116">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="dd88a-117">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="dd88a-117">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="dd88a-118">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span><span class="sxs-lookup"><span data-stu-id="dd88a-118">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="dd88a-119">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span><span class="sxs-lookup"><span data-stu-id="dd88a-119">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="dd88a-120">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span><span class="sxs-lookup"><span data-stu-id="dd88a-120">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="dd88a-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd88a-121">Prerequisites</span></span>

* <span data-ttu-id="dd88a-122">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span><span class="sxs-lookup"><span data-stu-id="dd88a-122">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="dd88a-123">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="dd88a-123">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="dd88a-124">Configure VPN connectivity</span><span class="sxs-lookup"><span data-stu-id="dd88a-124">Configure VPN connectivity</span></span>

<span data-ttu-id="dd88a-125">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the IP address and password values for your environment):</span><span class="sxs-lookup"><span data-stu-id="dd88a-125">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for the local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="dd88a-126">If the set-up succeeds, you should see **azurestack** in your list of VPN connections.</span><span class="sxs-lookup"><span data-stu-id="dd88a-126">If the set-up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Network connections](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="dd88a-128">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="dd88a-128">Connect to Azure Stack</span></span>

<span data-ttu-id="dd88a-129">Connect to the Azure Stack instance by using either of the following two methods:</span><span class="sxs-lookup"><span data-stu-id="dd88a-129">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="dd88a-130">By using the `Connect-AzsVpn ` command:</span><span class="sxs-lookup"><span data-stu-id="dd88a-130">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="dd88a-131">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span><span class="sxs-lookup"><span data-stu-id="dd88a-131">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="dd88a-132">(the prompt might appear behind the PowerShell session window).</span><span class="sxs-lookup"><span data-stu-id="dd88a-132">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="dd88a-133">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span><span class="sxs-lookup"><span data-stu-id="dd88a-133">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="dd88a-134">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span><span class="sxs-lookup"><span data-stu-id="dd88a-134">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="dd88a-135">Test the VPN connectivity</span><span class="sxs-lookup"><span data-stu-id="dd88a-135">Test the VPN connectivity</span></span>

<span data-ttu-id="dd88a-136">To test the portal connection, open an Internet browser and navigate to the user portal (https://portal.local.azurestack.external/), sign in and create resources.</span><span class="sxs-lookup"><span data-stu-id="dd88a-136">To test the portal connection, open an Internet browser and navigate to the user portal (https://portal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="dd88a-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd88a-137">Next steps</span></span>



