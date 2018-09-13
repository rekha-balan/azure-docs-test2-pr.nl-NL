---
title: Certificate assets in Azure Automation | Microsoft Docs
description: Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations to authenticate against Azure and third party resources.  This article explains the details of certificates and how to work with them in both textual and graphical authoring.
services: automation
documentationcenter: ''
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10252c41aaffcd2706fc199326900c3a41123947
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554824"
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="e5483-104">Certificate assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e5483-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="e5483-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="e5483-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="e5483-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span><span class="sxs-lookup"><span data-stu-id="e5483-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="e5483-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span><span class="sxs-lookup"><span data-stu-id="e5483-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="e5483-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span><span class="sxs-lookup"><span data-stu-id="e5483-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="e5483-109">This key is encrypted by a master certificate and stored in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5483-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="e5483-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span><span class="sxs-lookup"><span data-stu-id="e5483-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="e5483-111">Windows PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="e5483-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="e5483-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5483-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="e5483-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="e5483-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="e5483-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="e5483-114">Cmdlets</span></span>|<span data-ttu-id="e5483-115">Description</span><span class="sxs-lookup"><span data-stu-id="e5483-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="e5483-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e5483-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="e5483-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="e5483-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="e5483-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span><span class="sxs-lookup"><span data-stu-id="e5483-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="e5483-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e5483-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="e5483-120">Creates a new certificate into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5483-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="e5483-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e5483-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="e5483-122">Removes a certificate from Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5483-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="e5483-123">Creates a new certificate into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5483-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="e5483-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e5483-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="e5483-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span><span class="sxs-lookup"><span data-stu-id="e5483-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="e5483-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="e5483-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="e5483-127">Uploads a service certificate for the specified cloud service.</span><span class="sxs-lookup"><span data-stu-id="e5483-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="e5483-128">Creating a new certificate</span><span class="sxs-lookup"><span data-stu-id="e5483-128">Creating a new certificate</span></span>

<span data-ttu-id="e5483-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5483-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="e5483-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span><span class="sxs-lookup"><span data-stu-id="e5483-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="e5483-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="e5483-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="e5483-132">To create a new certificate with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e5483-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="e5483-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span><span class="sxs-lookup"><span data-stu-id="e5483-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="e5483-134">Click the **Certificates** tile to open the **Certificates** blade.</span><span class="sxs-lookup"><span data-stu-id="e5483-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="e5483-135">Click **Add a certificate** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="e5483-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="e5483-136">Type a name for the certificate in the **Name** box.</span><span class="sxs-lookup"><span data-stu-id="e5483-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="e5483-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span><span class="sxs-lookup"><span data-stu-id="e5483-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="e5483-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span><span class="sxs-lookup"><span data-stu-id="e5483-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="e5483-139">Click **Create** to save the new certificate asset.</span><span class="sxs-lookup"><span data-stu-id="e5483-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="e5483-140">To create a new certificate with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5483-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="e5483-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span><span class="sxs-lookup"><span data-stu-id="e5483-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="e5483-142">This imports an existing .pfx file.</span><span class="sxs-lookup"><span data-stu-id="e5483-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="e5483-143">Using a certificate</span><span class="sxs-lookup"><span data-stu-id="e5483-143">Using a certificate</span></span>

<span data-ttu-id="e5483-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span><span class="sxs-lookup"><span data-stu-id="e5483-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="e5483-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span><span class="sxs-lookup"><span data-stu-id="e5483-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="e5483-146">Textual runbook sample</span><span class="sxs-lookup"><span data-stu-id="e5483-146">Textual runbook sample</span></span>

<span data-ttu-id="e5483-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span><span class="sxs-lookup"><span data-stu-id="e5483-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="e5483-148">In this sample, the password is retrieved from an encrypted automation variable.</span><span class="sxs-lookup"><span data-stu-id="e5483-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="e5483-149">Graphical runbook sample</span><span class="sxs-lookup"><span data-stu-id="e5483-149">Graphical runbook sample</span></span>

<span data-ttu-id="e5483-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span><span class="sxs-lookup"><span data-stu-id="e5483-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Add certificate to the canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="e5483-152">The following image shows an example of using a certificate in a graphical runbook.</span><span class="sxs-lookup"><span data-stu-id="e5483-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="e5483-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span><span class="sxs-lookup"><span data-stu-id="e5483-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="e5483-154">Example Graphical Authoring</span><span class="sxs-lookup"><span data-stu-id="e5483-154">Example Graphical Authoring</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="e5483-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5483-155">Next steps</span></span>

- <span data-ttu-id="e5483-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="e5483-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 


