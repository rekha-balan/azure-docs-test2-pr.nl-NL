---
title: Enable Remote Desktop Connection for a Role in Azure Cloud Services
description: How to configure your Azure cloud service application to allow remote desktop connections
services: cloud-services
author: ghogen
manager: douge
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/06/2018
ms.author: ghogen
ms.openlocfilehash: 703e969fe31def329be60037cceba27864063b4e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866028"
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-visual-studio"></a><span data-ttu-id="d4762-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4762-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using Visual Studio</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](cloud-services-role-enable-remote-desktop-visual-studio.md)

<span data-ttu-id="d4762-107">Remote Desktop enables you to access the desktop of a role running in Azure.</span><span class="sxs-lookup"><span data-stu-id="d4762-107">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="d4762-108">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span><span class="sxs-lookup"><span data-stu-id="d4762-108">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="d4762-109">The publish wizard that Visual Studio provides for cloud services includes an option to enable Remote Desktop during the publishing process, using credentials that you provide.</span><span class="sxs-lookup"><span data-stu-id="d4762-109">The publish wizard that Visual Studio provides for cloud services includes an option to enable Remote Desktop during the publishing process, using credentials that you provide.</span></span> <span data-ttu-id="d4762-110">Using this option is suitable when using Visual Studio 2017 version 15.4 and earlier.</span><span class="sxs-lookup"><span data-stu-id="d4762-110">Using this option is suitable when using Visual Studio 2017 version 15.4 and earlier.</span></span>

<span data-ttu-id="d4762-111">With Visual Studio 2017 version 15.5 and later, however, it's recommended that you avoid enabling Remote Desktop through the publish wizard unless you're working only as a single developer.</span><span class="sxs-lookup"><span data-stu-id="d4762-111">With Visual Studio 2017 version 15.5 and later, however, it's recommended that you avoid enabling Remote Desktop through the publish wizard unless you're working only as a single developer.</span></span> <span data-ttu-id="d4762-112">For any situation in which the project might be opened by other developers, you instead enable Remote Desktop through the Azure portal, through PowerShell, or from a release pipeline in a continuous deployment workflow.</span><span class="sxs-lookup"><span data-stu-id="d4762-112">For any situation in which the project might be opened by other developers, you instead enable Remote Desktop through the Azure portal, through PowerShell, or from a release pipeline in a continuous deployment workflow.</span></span> <span data-ttu-id="d4762-113">This recommendation is due to a change in how Visual Studio communicates with Remote Desktop on the cloud service VM, as is explained in this article.</span><span class="sxs-lookup"><span data-stu-id="d4762-113">This recommendation is due to a change in how Visual Studio communicates with Remote Desktop on the cloud service VM, as is explained in this article.</span></span>

## <a name="configure-remote-desktop-through-visual-studio-2017-version-154-and-earlier"></a><span data-ttu-id="d4762-114">Configure Remote Desktop through Visual Studio 2017 version 15.4 and earlier</span><span class="sxs-lookup"><span data-stu-id="d4762-114">Configure Remote Desktop through Visual Studio 2017 version 15.4 and earlier</span></span>

<span data-ttu-id="d4762-115">When using Visual Studio 2017 version 15.4 and earlier, you can use the **Enable Remote Desktop for all roles** option in the publish wizard.</span><span class="sxs-lookup"><span data-stu-id="d4762-115">When using Visual Studio 2017 version 15.4 and earlier, you can use the **Enable Remote Desktop for all roles** option in the publish wizard.</span></span> <span data-ttu-id="d4762-116">You can still use the wizard with Visual Studio 2017 version 15.5 and later, but don't use the Remote Desktop option.</span><span class="sxs-lookup"><span data-stu-id="d4762-116">You can still use the wizard with Visual Studio 2017 version 15.5 and later, but don't use the Remote Desktop option.</span></span>

1. <span data-ttu-id="d4762-117">In Visual Studio, start the publish wizard by right-clicking your cloud service project in Solution Explorer and choosing **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d4762-117">In Visual Studio, start the publish wizard by right-clicking your cloud service project in Solution Explorer and choosing **Publish**.</span></span>

2. <span data-ttu-id="d4762-118">Sign into your Azure subscription if needed and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4762-118">Sign into your Azure subscription if needed and select **Next**.</span></span>

3. <span data-ttu-id="d4762-119">On the **Settings** page, select **Enable Remote Desktop for all roles**, then select the **Settings...** link to open the **Remote Desktop Configuration** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d4762-119">On the **Settings** page, select **Enable Remote Desktop for all roles**, then select the **Settings...** link to open the **Remote Desktop Configuration** dialog box.</span></span>

4. <span data-ttu-id="d4762-120">At the bottom of the dialog box, select **More Options**.</span><span class="sxs-lookup"><span data-stu-id="d4762-120">At the bottom of the dialog box, select **More Options**.</span></span> <span data-ttu-id="d4762-121">This command displays a drop-down list in which you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span><span class="sxs-lookup"><span data-stu-id="d4762-121">This command displays a drop-down list in which you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>

   > [!Note]
   > The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations. The remote access certificate must have a private key.

5. <span data-ttu-id="d4762-124">Select a certificate from the list or choose **&lt;Create...&gt;**.</span><span class="sxs-lookup"><span data-stu-id="d4762-124">Select a certificate from the list or choose **&lt;Create...&gt;**.</span></span> <span data-ttu-id="d4762-125">If creating a new certificate, provide a friendly name for the new certificate when prompted and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4762-125">If creating a new certificate, provide a friendly name for the new certificate when prompted and select **OK**.</span></span> <span data-ttu-id="d4762-126">The new certificate appears in the drop-down list box.</span><span class="sxs-lookup"><span data-stu-id="d4762-126">The new certificate appears in the drop-down list box.</span></span>

6. <span data-ttu-id="d4762-127">Provide a user name and a password.</span><span class="sxs-lookup"><span data-stu-id="d4762-127">Provide a user name and a password.</span></span> <span data-ttu-id="d4762-128">You can’t use an existing account.</span><span class="sxs-lookup"><span data-stu-id="d4762-128">You can’t use an existing account.</span></span> <span data-ttu-id="d4762-129">Don’t use "Administrator" as the user name for the new account.</span><span class="sxs-lookup"><span data-stu-id="d4762-129">Don’t use "Administrator" as the user name for the new account.</span></span>

7. <span data-ttu-id="d4762-130">Choose a date on which the account will expire and after which Remote Desktop connections will be blocked.</span><span class="sxs-lookup"><span data-stu-id="d4762-130">Choose a date on which the account will expire and after which Remote Desktop connections will be blocked.</span></span>

8. <span data-ttu-id="d4762-131">After you've provided all the required information, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4762-131">After you've provided all the required information, select **OK**.</span></span> <span data-ttu-id="d4762-132">Visual Studio adds the Remote Desktop settings to your project's `.cscfg` and `.csdef` files, including the password that's encrypted using the chosen certificate.</span><span class="sxs-lookup"><span data-stu-id="d4762-132">Visual Studio adds the Remote Desktop settings to your project's `.cscfg` and `.csdef` files, including the password that's encrypted using the chosen certificate.</span></span>

9. <span data-ttu-id="d4762-133">Complete any remaining steps using the **Next** button, then select **Publish** when you’re ready to publish your cloud service.</span><span class="sxs-lookup"><span data-stu-id="d4762-133">Complete any remaining steps using the **Next** button, then select **Publish** when you’re ready to publish your cloud service.</span></span> <span data-ttu-id="d4762-134">If you're not ready to publish, select **Cancel** and answer **Yes** when prompted to save changes.</span><span class="sxs-lookup"><span data-stu-id="d4762-134">If you're not ready to publish, select **Cancel** and answer **Yes** when prompted to save changes.</span></span> <span data-ttu-id="d4762-135">You can publish your cloud service later with these settings.</span><span class="sxs-lookup"><span data-stu-id="d4762-135">You can publish your cloud service later with these settings.</span></span>

## <a name="configure-remote-desktop-when-using-visual-studio-2017-version-155-and-later"></a><span data-ttu-id="d4762-136">Configure Remote Desktop when using Visual Studio 2017 version 15.5 and later</span><span class="sxs-lookup"><span data-stu-id="d4762-136">Configure Remote Desktop when using Visual Studio 2017 version 15.5 and later</span></span>

<span data-ttu-id="d4762-137">With Visual Studio 2017 version 15.5 and later, you can still use the publish wizard with a cloud service project.</span><span class="sxs-lookup"><span data-stu-id="d4762-137">With Visual Studio 2017 version 15.5 and later, you can still use the publish wizard with a cloud service project.</span></span> <span data-ttu-id="d4762-138">You can also use the **Enable Remote Desktop for all roles** option if you're working only as a single developer.</span><span class="sxs-lookup"><span data-stu-id="d4762-138">You can also use the **Enable Remote Desktop for all roles** option if you're working only as a single developer.</span></span>

<span data-ttu-id="d4762-139">If you're working as part of a team, you should instead enable remote desktop on the Azure cloud service by using either the [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md) or [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4762-139">If you're working as part of a team, you should instead enable remote desktop on the Azure cloud service by using either the [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md) or [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md).</span></span>

<span data-ttu-id="d4762-140">This recommendation is due to a change in how Visual Studio 2017 version 15.5 and later communicates with the cloud service VM.</span><span class="sxs-lookup"><span data-stu-id="d4762-140">This recommendation is due to a change in how Visual Studio 2017 version 15.5 and later communicates with the cloud service VM.</span></span> <span data-ttu-id="d4762-141">When enabling Remote Desktop through the publish wizard, earlier versions of Visual Studio communicate with the VM through what's called the "RDP plugin."</span><span class="sxs-lookup"><span data-stu-id="d4762-141">When enabling Remote Desktop through the publish wizard, earlier versions of Visual Studio communicate with the VM through what's called the "RDP plugin."</span></span> <span data-ttu-id="d4762-142">Visual Studio 2017 version 15.5 and later communicates instead using the "RDP extension" that is more secure and more flexible.</span><span class="sxs-lookup"><span data-stu-id="d4762-142">Visual Studio 2017 version 15.5 and later communicates instead using the "RDP extension" that is more secure and more flexible.</span></span> <span data-ttu-id="d4762-143">This change also aligns with the fact that the Azure portal and PowerShell methods to enable Remote Desktop also use the RDP extension.</span><span class="sxs-lookup"><span data-stu-id="d4762-143">This change also aligns with the fact that the Azure portal and PowerShell methods to enable Remote Desktop also use the RDP extension.</span></span>

<span data-ttu-id="d4762-144">When Visual Studio communicates with the RDP extension, it transmit a plain text password over SSL.</span><span class="sxs-lookup"><span data-stu-id="d4762-144">When Visual Studio communicates with the RDP extension, it transmit a plain text password over SSL.</span></span> <span data-ttu-id="d4762-145">However, the project's configuration files store only an encrypted password, which can be decrypted into plain text only with the local certificate that was originally used to encrypt it.</span><span class="sxs-lookup"><span data-stu-id="d4762-145">However, the project's configuration files store only an encrypted password, which can be decrypted into plain text only with the local certificate that was originally used to encrypt it.</span></span>

<span data-ttu-id="d4762-146">If you deploy the cloud service project from the same development computer each time, then that local certificate is available.</span><span class="sxs-lookup"><span data-stu-id="d4762-146">If you deploy the cloud service project from the same development computer each time, then that local certificate is available.</span></span> <span data-ttu-id="d4762-147">In this case, you can still use the **Enable Remote Desktop for all roles** option in the publish wizard.</span><span class="sxs-lookup"><span data-stu-id="d4762-147">In this case, you can still use the **Enable Remote Desktop for all roles** option in the publish wizard.</span></span>

<span data-ttu-id="d4762-148">If you or other developers want to deploy the cloud service project from different computers, however, then those other computers won't have the necessary certificate to decrypt the password.</span><span class="sxs-lookup"><span data-stu-id="d4762-148">If you or other developers want to deploy the cloud service project from different computers, however, then those other computers won't have the necessary certificate to decrypt the password.</span></span> <span data-ttu-id="d4762-149">As a result, you see the following error message:</span><span class="sxs-lookup"><span data-stu-id="d4762-149">As a result, you see the following error message:</span></span>

```output
Applying remote desktop protocol (RDP) extension.
Certificate with thumbprint [thumbprint] doesn't exist.
```

<span data-ttu-id="d4762-150">You could change the password every time you deploy the cloud service, but that action becomes inconvenient for everyone who needs to use Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="d4762-150">You could change the password every time you deploy the cloud service, but that action becomes inconvenient for everyone who needs to use Remote Desktop.</span></span>

<span data-ttu-id="d4762-151">If you're sharing the project with a team, then, it's best to clear the option in the publish wizard and instead enable Remote Desktop directly through the [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md) or by using [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4762-151">If you're sharing the project with a team, then, it's best to clear the option in the publish wizard and instead enable Remote Desktop directly through the [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md) or by using [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md).</span></span>

### <a name="deploying-from-a-build-server-with-visual-studio-2017-version-155-and-later"></a><span data-ttu-id="d4762-152">Deploying from a build server with Visual Studio 2017 version 15.5 and later</span><span class="sxs-lookup"><span data-stu-id="d4762-152">Deploying from a build server with Visual Studio 2017 version 15.5 and later</span></span>

<span data-ttu-id="d4762-153">You can deploy a cloud service project from a build server (for example, with Azure DevOps Services) on which Visual Studio 2017 version 15.5 or later is installed in the build agent.</span><span class="sxs-lookup"><span data-stu-id="d4762-153">You can deploy a cloud service project from a build server (for example, with Azure DevOps Services) on which Visual Studio 2017 version 15.5 or later is installed in the build agent.</span></span> <span data-ttu-id="d4762-154">With this arrangement, deployment happens from the same computer on which the encryption certificate is available.</span><span class="sxs-lookup"><span data-stu-id="d4762-154">With this arrangement, deployment happens from the same computer on which the encryption certificate is available.</span></span>

<span data-ttu-id="d4762-155">To use the RDP extension from Azure DevOps Services, include the following details in your build pipeline:</span><span class="sxs-lookup"><span data-stu-id="d4762-155">To use the RDP extension from Azure DevOps Services, include the following details in your build pipeline:</span></span>

1. <span data-ttu-id="d4762-156">Include `/p:ForceRDPExtensionOverPlugin=true` in your MSBuild arguments to make sure the deployment works with the RDP extension rather than the RDP plugin.</span><span class="sxs-lookup"><span data-stu-id="d4762-156">Include `/p:ForceRDPExtensionOverPlugin=true` in your MSBuild arguments to make sure the deployment works with the RDP extension rather than the RDP plugin.</span></span> <span data-ttu-id="d4762-157">For example:</span><span class="sxs-lookup"><span data-stu-id="d4762-157">For example:</span></span>

    ```
    msbuild AzureCloudService5.ccproj /t:Publish /p:TargetProfile=Cloud /p:DebugType=None
        /p:SkipInvalidConfigurations=true /p:ForceRDPExtensionOverPlugin=true
    ```

1. <span data-ttu-id="d4762-158">After your build steps, add the **Azure Cloud Service Deployment** step and set its properties.</span><span class="sxs-lookup"><span data-stu-id="d4762-158">After your build steps, add the **Azure Cloud Service Deployment** step and set its properties.</span></span>

1. <span data-ttu-id="d4762-159">After the deployment step, add an **Azure Powershell** step, set its **Display name** property to "Azure Deployment: Enable RDP Extension" (or another suitable name), and select your appropriate Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d4762-159">After the deployment step, add an **Azure Powershell** step, set its **Display name** property to "Azure Deployment: Enable RDP Extension" (or another suitable name), and select your appropriate Azure subscription.</span></span>

1. <span data-ttu-id="d4762-160">Set **Script Type** to "Inline" and paste the code below into the **Inline Script** field.</span><span class="sxs-lookup"><span data-stu-id="d4762-160">Set **Script Type** to "Inline" and paste the code below into the **Inline Script** field.</span></span> <span data-ttu-id="d4762-161">(You can also create a `.ps1` file in your project with this script, set **Script Type** to "Script File Path", and set **Script Path** to point to the file.)</span><span class="sxs-lookup"><span data-stu-id="d4762-161">(You can also create a `.ps1` file in your project with this script, set **Script Type** to "Script File Path", and set **Script Path** to point to the file.)</span></span>

    ```ps
    Param(
        [Parameter(Mandatory=$True)]
        [string]$username,

        [Parameter(Mandatory=$True)]
        [string]$password,

        [Parameter(Mandatory=$True)]
        [string]$serviceName,

        [Datetime]$expiry = ($(Get-Date).AddYears(1))
    )

    Write-Host "Service Name: $serviceName"
    Write-Host "User Name: $username"
    Write-Host "Expiry: $expiry"

    $securepassword = ConvertTo-SecureString -String $password -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential $username,$securepassword

    # Try to remote existing RDP Extensions
    try
    {
        $existingRDPExtension = Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
        if ($existingRDPExtension -ne $null)
        {
            Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
        }
    }
    catch
    {
    }

    Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry -Verbose
    ```

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a><span data-ttu-id="d4762-162">Connect to an Azure Role by using Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="d4762-162">Connect to an Azure Role by using Remote Desktop</span></span>

<span data-ttu-id="d4762-163">After you publish your cloud service on Azure and have enabled Remote Desktop, you can use Visual Studio Server Explorer to log into the cloud service VM:</span><span class="sxs-lookup"><span data-stu-id="d4762-163">After you publish your cloud service on Azure and have enabled Remote Desktop, you can use Visual Studio Server Explorer to log into the cloud service VM:</span></span>

1. <span data-ttu-id="d4762-164">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span><span class="sxs-lookup"><span data-stu-id="d4762-164">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span></span>

2. <span data-ttu-id="d4762-165">Right-click an instance node and select **Connect Using Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="d4762-165">Right-click an instance node and select **Connect Using Remote Desktop**.</span></span>

3. <span data-ttu-id="d4762-166">Enter the user name and password that you created previously.</span><span class="sxs-lookup"><span data-stu-id="d4762-166">Enter the user name and password that you created previously.</span></span> <span data-ttu-id="d4762-167">You are now logged into your remote session.</span><span class="sxs-lookup"><span data-stu-id="d4762-167">You are now logged into your remote session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4762-168">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d4762-168">Additional resources</span></span>

[<span data-ttu-id="d4762-169">How to Configure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d4762-169">How to Configure Cloud Services</span></span>](cloud-services-how-to-configure-portal.md)
